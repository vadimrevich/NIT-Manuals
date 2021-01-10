# Хостинг на Hetzner

По организации хостинга на серверах Hetzner довольно много руководств, только в основном она на английском и немецком языках. Привожу здесь краткое руководство:

**Что такое немцы, и с чем их едят?**

Во-первых, немцы это немцы, и это надо понимать. Никакой поддержки в компании hetzner.de нет. Вам не будут помогать настраивать почту, или поднимать вам ftp сервер. Даже за деньги не будут. Даже если очень попросите. Нанимать администратора это ваша задача. Такова их логика. Они просто дают вам свои ресурсы в аренду, с учетом того, что администрируете вы их сами. Такой вот немецкий low cost. Если вы слабо разбираетесь в технологиях, и вас, к примеру, пугает по непонятной для вас причине, неработающий ftp сервер, то закупать сервера на hetzner.de не имеет смысла, ну разве что с недавнего времени у компании появилась услуга [webhosting,](http://www.hetzner.de/hosting/produktmatrix/webhosting-produktmatrix) которая позволяет купить любимый пользователями shared hosting, но это не наш путь!

Я зарегистрировал себе [vServer](http://www.hetzner.de/hosting/produktmatrix_vserver/vserver-produktmatrix) (VPS) сначала по тарифу [vq7](http://www.hetzner.de/hosting/produkte_vserver/vq7), а чуть позже перешел на следующий тариф [vq12](http://www.hetzner.de/hosting/produkte_vserver/vq12)

Обратите внимание, что при переходе с тарифа на тариф меняется IP адрес. То есть вы закрываете один сервер и открываете другой сервер. Никакого такого апгрейда не происходит.

**Как происходит регистрация?**

На сайте вы выбираете подходящий вам тарифный план. Выбор идет между [Web Hosting,](http://www.hetzner.de/en/hosting/produktmatrix/webhosting-produktmatrix) [Dedicated Server](http://www.hetzner.de/en/hosting/produktmatrix/rootserver), [vServer](http://www.hetzner.de/en/hosting/produktmatrix_vserver/vserver-produktmatrix), [Managed Server,](http://www.hetzner.de/en/hosting/produktmatrix/managed-server-produktmatrix) [Colocation](http://www.hetzner.de/en/hosting/produktmatrix/racks) а также вы можете регистрировать [Domains & Services](http://www.hetzner.de/en/hosting/domains/domainregistrierung)

Алгоритм регистрации достаточно простой. Вы выбираете подходящий тарифный план и нажимаете на кнопку **order now**.

[![hetzner_order](http://serg-smirnoff.com/wp-content/uploads/2014/11/hetzner_vq12_1-595x377.png)](http://serg-smirnoff.com/wp-content/uploads/2014/11/hetzner_vq12_1.png)

После этого вы переходите на страницу где осуществляете заказ и подтверждаете согласие с оплатой.

[![hetzner_vq12_2](http://serg-smirnoff.com/wp-content/uploads/2014/11/hetzner_vq12_2-1024x661.png)](http://serg-smirnoff.com/wp-content/uploads/2014/11/hetzner_vq12_2.png)

Здесь вам предлагают выбрать настройки вашего VPS.

Во-первых, вы можете выбрать **resque system** это минимальная Linux-система с необходимыми инструментами. То есть если вы выберите этот параметр, то все манипуляции по установке программного обеспечения вы будете проводить самостоятельно.

Во-вторых, вы можете выбрать предустановленную операционную систему. Выбор лежит между **CentOS**, **Debian**, **Ubuntu** и даже **Windows Server**. Вы также можете выбрать вариант установки операционной системы с предустановленной панелью управления **Plesk**.

Обратите внимание что между Debian 7.7 LAMP и Debian 7.7 minimal есть разница. Разница эта в LAMP (Linux, Apache, MySQL, PHP). Если вы не хотите ставить это все руками, то выбирайте опцию **Debian 7.7 LAMP** и на выходе вы получаете VPS со всем добром на борту. Настройка оставляет желать лучшего, поэтому конфиги вам конечно придется переписывать и не однократно. Если же вы любитель установить все с чистого листа, то ваш выбор **Debian 7.7 minimal** 

В-третьих, можно выбрать архитектуру между **32 bit** и **64 bit**

Вот и все. Выбираете соответствующие опции. Нажимаете **add to shoping card** (добавить в корзину) и производите **checkout** (оплата).

[![hetzner_vq12_3](http://serg-smirnoff.com/wp-content/uploads/2014/11/hetzner_vq12_3-1024x649.png)](http://serg-smirnoff.com/wp-content/uploads/2014/11/hetzner_vq12_3.png)

Обратите внимание, что оплата будет произведена за вычетом **VAT 19%** (НДС) если вы являетесь не резидентом Германии. То есть при тарифе **12,9** € хостинг обойдется вам в **10,84** € что несколько дешевле.

[![hetzner_vq12_4](http://serg-smirnoff.com/wp-content/uploads/2014/11/hetzner_vq12_4-1024x649.png)](http://serg-smirnoff.com/wp-content/uploads/2014/11/hetzner_vq12_4.png)

Понять резидент вы или нет, можно после регистрации аккаунта. Так как вы не можете передать системе свой **VAT ID** (ИНН) то система считает вас не резидентом Германии.

Вот и все.

После создания нового аккаунта вам придет уведомление следующего содержания

```

Dear Mr Sergey Smirnov, Thank you very much for ordering and placing your trust in us.

Please check your data for correctness. If you have any requests for changes or the order was sent by mistake, please email us at [server\_bestellung@hetzner.de](mailto:server_bestellung@hetzner.de).

==============================================
Contact address (also the invoice address):
==============================================
Company: 
Title: Herr
Name: 
Surname: 
Street: 
Postal code: 
City: 
Country: RUSSIAN FEDERATION
Phone: 
Mobile phone: 
Fax: 
VAT ID: 
Email: 

==============================================
Your order:
==============================================
 1 x vServer VQ 7
     \* Debian 6.0 LAMP (English, 64 bit)

==============================================
Payment method:  
==============================================
Credit card
The next step is to receive an order confirmation from us. If your order is a special configuration or if it is the first time you have placed an order, your order will be checked manually. This takes place during our office hours which are Mon - Fri 8.00 am - 6.00 pm. On receiving the order confirmation, your server will be released for installation and you will usually receive your server access data within a few hours. Special configuration servers may require a few days for completion.
Please visit [http://www.hetzner.de/en/hosting/produktmatrix/rootserver-produktmatrix](http://www.hetzner.de/en/hosting/produktmatrix/rootserver-produktmatrix) to get prices and details for root servers.
Please visit [http://wiki.hetzner.de/index.php/Auftragsbearbeitungen/](http://wiki.hetzner.de/index.php/Auftragsbearbeitungen/) to view the current order status.
Our competent support-team is ready to answer your questions. Please visit our website at [http://www.hetzner.de/en/hosting/kontakt/support-center](http://www.hetzner.de/en/hosting/kontakt/support-center)
Yours sincerely,
Hetzner Online AG
Stuttgarter Str. 1
91710 Gunzenhausen
Tel: +49-9831-610061
Fax: +49-9831-610062
[info@hetzner.de](mailto:info@hetzner.de)
[http://www.hetzner.de](http://www.hetzner.de/)
Register Court: Registergericht Ansbach, HRB 3204
Management Board: Dipl. Ing. (FH) Martin Hetzner
Chairwoman of the Supervisory Board: Diana Rothhan

```

Это перечисление услуг, которые вы заказали, и просьба еще раз проверить и подтвердить данные вашей кредитной карты, и вашего аккаунта, для выставления вам **invoice** (счетов на оплату) в дальнейшем.

После подтверждения вам придет еще одно письмо, с доступами к вашему аккаунту. Адрес в панель управления, логин и пароль.

Скажу сразу, в панели управления по-умолчанию не включен **Nameserver robot.** Это система управления NS серверами которая понадобиться вам для подключения доменных имен.

```
==============================================
Your order:
==============================================
 1 x Nameserver Robot
```

Так же можно подписать договор с hetzner.de на возможность регистрации доменных имен через них. То есть включить услугу **Domain Robot**

Теперь после подключения этой услуги, вы можете регистрировать доменные имена в некоторых зонах через немецкого регистратора являясь нерезидентном Германии. Зачем это нужно? Да бог его знает.

Эта услуга тоже бесплатная, но тут уже не достаточно простых нажатий кнопок, а с компанией придется обменяться документацией. То есть распечатать и подписать договор и отправить его в Германию, получив обратно свою копию.

```
==============================================
Your order:
==============================================
 1 x Domain Robot
```

Также, если вы не выбрали установку панели управления **PLESK** в момент покупки **VPS**, то лучше поставить **ISP-Manager** которую можно купить отдельно, и стоит это что-то около **11€** На мой взгляд она более userfriendly :-)

Счет на оплату услуг, будет выставлен позднее. Услугу предоставляют авансом. Деньги автоматически будут списаны с вашей кредитной карты. Обычно списание происходит в течение 5 дней после выставления инвойса.

В случае отсутствия средств на карте, вам будет выслано предупреждение из бухгалтерии. Если вы не оплатите и после этого, то есть риск выключения серверов. Но в Интернете пишут, что растягивали сроки оплаты и до 2х месяцев. Мне в это слабо верится, отключат в течение недели.

Вот и все. Теперь вы можете получить полностью контролируемый вами сервер за доступные деньги, размещать там как свои сайты так и сайты клиентов, или просто тренироваться и развивать навыки работы в unix системах! Рекомендую!

# Дополнительные замечания

Страница входа в аккаунт Hetzner <https://accounts.hetzner.com/login>
Страница входа в облачные виртуальные сервера: <https://console.hetzner.cloud/projects>
Центр поддержки Hetzner <https://ru.hetzner.com/hosting/kontakt/support-center/>

# Описание

Войдя в Hetzner Cloud Console Вы увидете слева панель управления. Самым первым её пунктом будут сервера. Здесь можно выбрать заказанный сервер, управлять его состоянием (включён, выключен, перезагрузка), можно пересоздать сервер, если на нём испорчена конфигурация вследствие неумелых действий, а также подключиться к консоли через VNC клиент Hetzner.

Интерфейс панели минималистичен, но более чем достаточен для управления сервером.

При желании на компьютер можно установить соответствующее программное обеспечение и управлять своим аккаунтом из командной строки с помощью API. Для этого на панели управления нужно перейти в пункт "Security" -> "API Tokens" и нажать "Generate API Tocken". Просмотреть токен можно только один раз, в процессе генерации, повторно затребовать у Вас возможности нет. Поэтому хорошим решением будет записать токен в тестовый файл и поместить в защищённое облако.

Собственно программное обеспечение, необходимое для работы с API, автор здесь не приводит. Смотрите мануалы по системе Hetzner на 

## Недостатки хостинга

1. Хостинг имеет очень сложную и неудобную систему установки операционных систем с собственных носителей. Так что установить собственную операционную систему Вам будет затруднительно.

2. Хостинг не позволяет создавать открытые порты 139 и 445. В противном случае Вам пришлют абуз. Если открыть эти порты всё-таки нужно, ограничивайте в брандмауэре диапазон прослушивающих IP адресов.