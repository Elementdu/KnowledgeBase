---
title: Расширенные (низкоуровневые) настройки
sidebar_position: 7
---

Previously known as low-level settings, Advanced Settings mostly contain options that go beyond the average user competence and aren't applied in everyday use. AdGuard for Windows is designed to work without ever having to change any of them, but they will provide additional features in some corner cases or when solving an uncommon problem.

> Изменение *Расширенных настроек* может вызвать проблемы с производительностью AdGuard, нарушить подключение к интернету или поставить под угрозу вашу безопасность и конфиденциальность. Вносить изменения в эти настройки следует только в том случае, если вы уверены в том, что делаете, или если об этом вас попросила наша служба поддержки.

## Как перейти к Расширенным настройкам

Чтобы попасть в *Расширенные настройки*, на главном экране откройте *Настройки → Основные настройки* и прокрутите вниз до *Расширенных настроек*. Или выберите *Расширенные → Расширенные настройки...* в трей-меню.

## Расширенные настройки

После того как вы откроете Расширенные настройки, вам будут представлены следующие опции:

### Блокировать TCP Fast Open

Если эта функция включена, AdGuard будет блокировать TCP Fast Open в браузере Edge. Чтобы применить настройки, необходимо перезапустить браузер.

### Use Encrypted ClientHello

Every encrypted Internet connection has an unencrypted part. This is the very first packet which contains the name of the server you are connecting to. Encrypted Client Hello technology is supposed to solve this issue and encrypt that last bit of unencrypted information. To benefit from it, enable the *Use Encrypted ClientHello* option. It uses a local DNS proxy to look for ECH configuration for the domain. If it is found, ClientHello packet will be encrypted.

### Check websites' certificate transparency

Проверяет подлинность всех сертификатов для домена на основе политики прозрачности сертификатов Chrome. If the certificate does not comply with the Chrome CT Policy, AdGuard will not filter the website. Chrome, in turn, will block it.

### Enable SSL/TLS certificate revocation checks

Once enabled, this option runs asynchronous OCSP checks to check whether the website’s SSL/TLS certificate is revoked.

If the OCSP check completes within the minimum timeout, AdGuard will immediately apply the result: block the connection if the certificate is revoked or establish a connection if the certificate is valid.

If the verification takes too long, AdGuard will establish a connection and continue checking in the background. If the certificate is revoked, current and future connections to the domain will be blocked.

### Show AdGuard VPN in Settings

Enabling this option allows you to display the AdGuard VPN tab in Settings for easy opening of the app and the product's website.

### Исключите приложение из фильтрации, введя полный путь

Если вы хотите, чтобы AdGuard не фильтровал конкретные приложения, укажите полный путь к ним, и приложения будут исключены из фильтрации. Разделите разные пути точкой с запятой.

### Включить всплывающие уведомления AdGuard

Включите эту функцию, чтобы видеть всплывающие уведомления AdGuard. Они появляются не слишком часто и содержат только важную информацию. Вы также можете использовать трей-меню, чтобы вызвать последнее всплывающее уведомление.

### Автоматически перехватывать URL-адрес фильтра

Включите эту функцию, если вы хотите, чтобы AdGuard автоматически перехватывал URL фильтра (например, `abp:subscribe` и т.п.) и открывал диалог установки пользовательского фильтра.

### Использовать драйвер в режиме перенаправления

Если эта опция включена, AdGuard перехватывает весь трафик и перенаправляет его на локальный прокси-сервер для дальнейшей фильтрации.

В противном случае AdGuard будет фильтровать весь трафик на лету, без перенаправления. При этом система будет считать AdGuard единственным приложением, которое подключается к интернету (другие приложения будут направляться через него). Минусом является то, что это сделает системный брандмауэр менее эффективным. А плюсом — то, что этот подход работает немного быстрее.

### Открывать главное окно при запуске системы

Включите эту опцию, чтобы главное окно AdGuard открывалось при каждом запуске системы. Обратите внимание, что эта настройка не влияет на то, запущена ли реальная фильтрация или нет. Она находится в разделе *Настройки → Общие настройки*

### Enable filtering at system start-up

Starting from v7.12, by default, AdGuard's service does not filter traffic after OS startup if the option Launch AdGuard at system start-up is disabled. In other words, the AdGuard's service is started in “idle” mode. Enable this option to make AdGuard filter traffic even if the app is not launched.

*Note that before v7.12 the AdGuard's service started in filtering mode by default (even if the *Launch AdGuard at system start-up” was disabled). If you were satisfied with the old behavior, enable this option.*

### Фильтровать локальные адреса

Если вы хотите, чтобы AdGuard фильтровал соединения loopback, установите флажок. Эта опция всегда будет включена, если у вас установлен AdGuard VPN, потому что в противном случае он не сможет работать.

### Exclude specified IP ranges from filtering

If you don't want AdGuard to filter particular subnets, enable this feature and specify the IP ranges in the CIDR notation (e.g. 98.51.100.14/24) in the **IP ranges excluded from filtering** section below.

### Включить запись HAR

Эта опция должна быть включена **только в целях отладки**. Если вы установите флажок, AdGuard создаст файл, содержащий информацию обо всех отфильтрованных HTTP-запросах в формате HAR 1.2. Этот файл можно проанализировать с помощью приложения Fiddler. Обратите внимание, что это может значительно замедлить просмотр веб-страниц.

### Add an extra space to the plain HTTP request

Adds extra space between the HTTP method and the URL and removes space after the "Host:" field to avoid deep packet inspection. For instance, the request

`GET /foo/bar/ HTTP/1.1
Host: example.org`

will be converted to

`GET  /foo/bar/ HTTP/1.1
Host:example.org`

This option is only applied when the *Protect from DPI* Stealth mode option is enabled.

### Adjust size of fragmentation of initial TLS packet

Specifies the size of the TCP packet fragmentation, avoiding deep packet inspection. This option only affects secured HTTPS traffic.

If this option is enabled, AdGuard splits the initial TLS packet (the ClientHello packet) into two parts: the first one has the specified length and the second one has the rest, up to the length of the whole initial TLS packet.

Acceptable values: 1–1500. If invalid size is specified, the value selected by the system will be used. This option is only applied when the *Protect from DPI* Stealth mode option is enabled.

### Plain HTTP request fragment size

Настраивает размер фрагментации HTTP-запроса. This option only affects plain HTTP traffic. If this option is enabled, AdGuard splits the initial packet into two parts: the first one has the specified length and the second one has the rest, up to the length of the whole original packet.

Acceptable values: 1–1500. If invalid size is specified, the value selected by the system will be used. This option is only applied when the *Protect from DPI* Stealth mode option is enabled.

### Показывать QUIC

Позволяет отображать записи протокола QUIC в отчёте журнала фильтрации. Эта опция работает только для заблокированных запросов.

### Enable TCP keepalive

Periodically sends TCP packets over idle connection to ensure it is alive and to renew NAT timeouts. This option can be useful to bypass the strict network address translation (NAT) settings that some ISPs use.

### TCP keepalive interval

Here you can specify an idle time period, in seconds, before sending a keepalive probe. Если указано 0, будет использоваться значение, установленное системой.

Note that this setting only works when the *Enable TCP keepalive* option is enabled.

### TCP keepalive timeout

Here you can specify time, in seconds, before sending another keepalive probe to an unresponsive peer. Если указано 0, будет использоваться значение, установленное системой.

Note that this setting only works when the *Enable TCP keepalive* option is enabled.

### Блокировать Java

Некоторые сайты и веб-сервисы до сих пор используют устаревшие технологии поддержки Java-плагинов. API-интерфейс, лежащий в основе Java-плагинов, небезопасен. Вы можете отключить такие плагины в целях безопасности. Тем не менее, даже если вы решите использовать опцию *Блокировать Java*, JavaScript будет по-прежнему включён.

### Время ожидания ответа DNS-сервера

В этом поле вы можете указать время в миллисекундах, в течение которого AdGuard будет ждать ответа от выбранного DNS-сервера, прежде чем прибегнуть к резервному. Если вы не заполните это поле или введёте недопустимое значение, будет использовано значение 5000.

### Use HTTP/3 for DNS-over-HTTPS

Enables HTTP/3 for DNS-over-HTTPS upstreams to accelerate connection if the selected upstream supports this protocol. This means that enabling this option does not guarantee that all DNS requests will be sent via HTTP/3.

### Use fallback DNS upstreams

If enabled, normal queries will be redirected to the fallback upstream if all DNS requests to the selected upstreams fail.

### Query DNS upstreams in parallel

Once enabled, all upstreams are queried in parallel and the first successful response is returned. Since DNS queries are made in parallel, enabling this feature increases the Internet speed.

### Always respond to failed DNS queries

If address resolving failed on each of the forwarded upstreams, as well as on the fallback domains, then the response to the DNS request will be `SERVFAIL`.

### Включить фильтрацию зашифрованных DNS-запросов

Если опция включена, AdGuard перенаправляет зашифрованные DNS-запросы на локальный DNS-прокси в дополнение к обычным DNS-запросам.

### Blocking mode for hosts rules

Here you can select the way AdGuard will respond to domains blocked by DNS rules based on [hosts rule syntax](https://adguard-dns.io/kb/general/dns-filtering-syntax/#etc-hosts-syntax).

* Reply with “Refused” error
* Reply with “NxDomain” error
* Ответ пользовательским IP-адресом

### Blocking mode for adblock-style rules

Here you can select the way AdGuard will respond to domains blocked by DNS rules based on [adblock-style syntax](https://adguard-dns.io/kb/general/dns-filtering-syntax/#adblock-style-syntax).

* Reply with “Refused” error
* Reply with “NxDomain” error
* Ответ пользовательским IP-адресом

### Пользовательский IPv4-адрес

If Custom IP address is selected in Blocking mode for hosts rules or Blocking mode for adblock-style rules, this IP address will be returned in response to blocked A requests. If none are specified, AdGuard will reply with the default Refused error.

### Пользовательский IPv6-адрес

If Custom IP address is selected in Blocking mode for hosts rules or Blocking mode for adblock-style rules, this IP address will be returned in response to blocked AAAA requests. Если он не указан, AdGuard ответит ошибкой «Refused» по умолчанию.

### Резервные (fallback) серверы

Здесь вы можете указать альтернативный DNS-сервер, на который будет перенаправлен DNS-запрос, если основной сервер не ответит в течение времени ожидания, указанного в следующем разделе. Есть три варианта на выбор:

* Не использовать резервные серверы;
* Использовать системные серверы;
* Использовать пользовательские серверы.

### Блокировать ECH

Если опция включена, AdGuard удаляет из ответов параметры Encrypted Client Hello.

### Список пользовательских резервных (fallback) серверов

Если вы хотите, чтобы AdGuard использовал пользовательские fallback-серверы, перечислите их в этом разделе, по одному в строке.

### Список пользовательских bootstrap-адресов

Bootstrap — это промежуточный DNS-сервер, используемый для получения IP-адреса безопасного DNS-сервера, который вы выбрали ранее в разделе *DNS-защита*. Такое «промежуточное звено» нужно при использовании протоколов, которые обозначают адрес сервера буквами (например, DNS-over-TLS). В этом случае bootstrap выступает в роли переводчика, трансформируя буквы в цифры, понятные вашей системе.

По умолчанию используется системный DNS-резолвер, а первоначальный bootstrap-запрос идёт через 53 порт. Если вас это не устраивает, перечислите здесь IP-адреса DNS-серверов, которые будут использоваться для определения адреса зашифрованного DNS-сервера. Указанные IP-адреса будут применены в порядке перечисления. Если вы укажете некорректные адреса или не укажете их вовсе, будут использованы системные IP-адреса.

### DNS-исключения

Все DNS-запросы к перечисленным здесь доменам будут перенаправляться на системный DNS-сервер вместо DNS-сервера, указанного в настройках приложения. Также к таким запросам не будут применяться правила DNS-фильтрации.

### Exclude specified Wi-Fi networks names (SSIDs) from the DNS filtering

DNS protection will not work for the Wi-Fi networks listed in this section. Specify Wi-Fi networks names (SSIDs) one per line. This can be useful if a particular Wi-Fi network is already protected by AdGuard Home or another DNS protection system. In this case, it is superfluous to filter DNS requests again.
