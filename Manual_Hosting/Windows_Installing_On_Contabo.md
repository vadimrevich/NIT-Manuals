# Алгоритм установки Microsoft Windows на сервер Contabo

- Оплатите хостинг Contabo с Linux-подобной операционной системой и дождитесь её установки (вам придёт письмо).
- Зайдите в панель управления Вашими серверами на Contabo.
- Загрузите операционную систему в режиме восстановления (ClonZilla)
- Зайдите в систему через VNC-клиент (логин и пароль для временного входа в консоль восстановления Вам придёт на почту).
- Войдите в оболочку
- Залогинтесь как root

```
#sudo su - root

```

- Создайте разделы на диске с помощью команды fdisk или parted:
- `#parted /dev/sda`
- Создаёте таблицу mbr
- Создайте три раздела:
1. 0 Gb -> 8Gb ntfs;
2. 8 Gb -> 28 Gb ext4
3. 28 Gb -> max-size -- любая
- Сделайте раздел 1 загрузочным и "живым" ` (parted) set 1 boot on`
- Отформатируйте разделы:
1. `#mkfs.ntfs -f /dev/sda1`
2. `#mkfs.ext4 /dev/sda2`
- Смонтируйте эти разделы командами:
```
#mkdir /mnt/sda1 && mount /dev/sda1 /mnt/sda1
#mkdir /mnt/sda2 && mount /dev/sda3 /mnt/sda2
```
- Перейти во временное хранилище: `#cd /mnt/sda2`
- Закачать образ операционной системы Microsoft Windows (образ системы должен быть подготовлен и загружен в Интернет):
```
#wget https://windows101tricks.com/1903-iso-64 (у Вас будет собственный адрес)
```
- Загрузите драйвера Vitrio:
```
 Download virtio drivers 
#wget https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso
```
- Смонтируйте образ операционной системы Windows на временный диск:
```
#mkdir /mnt/cd
#mount -o loop /mnt/sda3/1903-iso-64 /mnt/cd
```
- Скопируйте все файлы с DVD в первый раздел диска и размонтируйте DVD
```
#cp -av /mnt/cd/* /mnt/sda1/
#umount /mnt/cd
```
- Установите wimtools. На современных операционных системах эта нетривиальная задача. Распишем её по-порядку:
- Скачивание и установка в Ubuntu 20.04:
```
#wget http://archive.ubuntu.com/ubuntu/pool/main/g/glibc/libc6_2.31-0ubuntu9_amd64.deb
#wget http://archive.ubuntu.com/ubuntu/pool/main/g/glibc/libc6-amd64_2.31-0ubuntu9.1_i386.deb
#wget http://ftp.br.debian.org/debian/pool/main/w/wimlib/libwim15_1.13.3-1_amd64.deb
#wget http://mirrors.kernel.org/ubuntu/pool/universe/w/wimlib/libwim15_1.13.2-1_amd64.deb
#wget http://mirrors.kernel.org/ubuntu/pool/universe/w/wimlib/wimtools_1.13.2-1_amd64.deb
#dpkg -i ./libc6_2.31-0ubuntu9_amd64.deb
#dpkg -i ./libc6-amd64_2.31-0ubuntu9.1_i386.deb
#dpkg -i ./libwim15_1.13.2-1_amd64.deb
#dpkg -i ./wimtools_1.13.2-1_amd64.deb
```
- Скачивание и установка в Ubuntu 18.04
```
#wget http://archive.ubuntu.com/ubuntu/pool/main/g/glibc/libc6_2.27-3ubuntu1_amd64.deb
#wget http://archive.ubuntu.com/ubuntu/pool/main/g/glibc/libc6-amd64_2.27-3ubuntu1.4_i386.deb
#wget http://mirrors.kernel.org/ubuntu/pool/universe/w/wimlib/libwim15_1.13.2-1_amd64.deb
#wget http://ftp.br.debian.org/debian/pool/main/w/wimlib/libwim15_1.13.3-1_amd64.deb
#wget http://mirrors.kernel.org/ubuntu/pool/universe/w/wimlib/wimtools_1.13.2-1_amd64.deb
#dpkg -i ./libc6_2.27-3ubuntu1_amd64.deb
#dpkg -i ./libc6-amd64_2.27-3ubuntu1.4_i386.deb
#dpkg -i ./libwim15_1.13.2-1_amd64.deb
#dpkg -i ./wimtools_1.13.2-1_amd64.deb
```
- Создаём каталог wim `#mkdir /mnt/wim`
- Монтируем образ vitrio.iso и копируем его на первый раздел диска:
```
#mount /mnt/sda2/virtio-win.iso /mnt/cd
#mkdir /mnt/sda1/virtio && cp -av /mnt/cd/* /mnt/sda1/virtio
```
- Копируем в wim:
```
#wimmountrw /mnt/sda1/sources/boot.wim 1 /mnt/wim
#mkdir /mnt/wim/virtio
#cp -av /mnt/cd/* /mnt/wim/virtio
#wimunmount --commit /mnt/wim
```
Вывод будет что-то вроде следующего:
```
root@debian:/mnt/sda1#wimunmount --commit /mnt/wim
Commiting change to /mnt/sda1/sources/boot.wim (image 1)
Using LZX Compression with 4 threads
Archiving file data:352 MiB of 352 MiB (100%) done
```
- Копируем в wim2:
```
#wimmountrw /mnt/sda1/sources/boot.wim 2 /mnt/wim
#mkdir /mnt/wim/virtio
#cp -av /mnt/cd/* /mnt/wim/virtio
#wimunmount --commit /mnt/wim
```
Вывод будет что-то вроде следующего:
```
root@debian:/mnt/sda1#wimunmount --commit /mnt/wim
Commiting change to /mnt/sda1/sources/boot.wim (image 2)
Using LZX Compression with 4 threads
Archiving file data:0 bytes of 0 bytes (0%) done
```
- Подаём команду: `#sync`
- Размонтируем всё:
```
#cd /tmp
#umount /mnt/cd
#umount /mnt/sda1
```
- Скачиваем пакет ms-sys:
```
#wget http://prdownloads.sourceforge.net/ms-sys/ms-sys-2.6.0.tar.gz
#tar -xzvf ms-sys-2.6.0.tar.gz
#cd ./ms-sys-2.6.0
#make
#chmod +x ms-sys
```
- Создаём загрузочный сектор команды и вывод будет что-то вроде следующего:
```
root@debian:/tmp/ms-sys-2.6.0#ms-sys -n /dev/sda1
NTFS Windows 7 boot record successfully written to /dev/sda1
root@debian:/tmp/ms-sys-2.6.0#ms-sys -7 /dev/sda
Windows 7 master boot record successfully written to /dev/sda
```
- Далее подаём команды:
```
#sync
#reboot
```
- Начнётся установка Microsoft Windows как обычно.
- Когда системе потребуется драйвер дисковода, найдите его в X:/virtio/amd64/ и дальше по каталогу.
- Далее Вы удаляете разделы 2 и 3 и устанавливаете Windows в эту неразмеченную область.
- После установки Microsoft Windows найдите недостающие драйвера в папке D:\vitrio
- Настройте удалённый доступ к системе.
- Диск D: теперь потребуется только для перестановки Windows без удаления разделов

## Более простой способ установки (с использованием скриптов)

- Оплатите хостинг Contabo с Linux-подобной операционной системой и дождитесь её установки (вам придёт письмо).
- Зайдите в панель управления Вашими серверами на Contabo.
- Загрузите операционную систему в режиме восстановления (ClonZilla)
- Зайдите в систему через VNC-клиент (логин и пароль для временного входа в консоль восстановления Вам придёт на почту).
- Войдите в оболочку
- Залогинтесь как root

```
#sudo su - root

```

- Перейдите в каталог tmp и скачайте архив со скриптами:
```
#cd /tmp
#wget https://windows101tricks.com/towin.scripts.tgz (у Вас будет собственный адрес)
````
- Распакуйте скрипты командой `#tar -xzvf towin.scripts.tgz`
- Исправьте в скрипте *towinpart0.sh* значение 127G на свой максимальный размер диска
- Выполните последовательно команды:
```
#/tmp/towinpart0.sh
#/tmp/load_win2008r2.sh (или какая там у Вас версия Windows)
#/tmp/prepare-win.sh
#/tmp/postinstall.sh
#/tmp/wimtools.18.04.sh 
(или wimtools.20.04.sh в зависимости от версии Ubuntu)
#/tmp/wim-prepare.sh
#/tmp/ms-sys-prepare.sh
```

Команды запускать «как есть» из текущего каталога, который при выполнении программ будет меняться. Ни в коем случае не меняйте рабочие каталоги во время запуска последовательности скриптов. Внимательно смотрите вывод программ, и в случае ошибок переключайтесь на ручной способ подготовки дисков.

- Подайте команду `#reboot` и следуйте мастеру установки Windows, не забывая подгружать драйвера.

### Змечание

Этот способ установки должен работать и при установке операционной системы с диска и на других хостингах, которые позволяют устанавливать свои операционные системы из образов. В этом случае в качестве первичного образа диска надо «скормить» образ CloneZilla Server Edition и запустить установку из неё. Перед перезагрузкой виртуальной машины и установкой Windows необходимо размонтировать образ CloneZilla.

