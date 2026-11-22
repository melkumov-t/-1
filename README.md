# Практична робота № 1

**Дисципліна:** Основи побудови інформаційних систем та мереж

**Тема:** Спостереження за процесом звернення до вебресурсу. Побудова власної моделі рівнів взаємодії

| Поле | Значення |
|---|---|
| **Прізвище, ім'я** |Мелькумов Тимур |
| **Група** |ЗКІ-21 |
| **Номер варіанта** | 7 |
| **Домен варіанта** | w3.org|
| **Середовище виконання** | Windows |
| **Версія curl** | curl 8.22.0 (Windows) libcurl/8.22.0 Schannel zlib/1.3.2 WinIDN WinLDAP|
| **Дата виконання** | 22.11.2026|

---

## Частина A. Збір експериментальних даних

### A.1. Запит із діагностичним виводом

**Команда:**

```
curl -v https://w3.org
```

**Вивід:**

```
C:\Users\Тимур> curl -v https://w3.org
* Host w3.org:443 was resolved.
* IPv6: 2606:4700::6812:1613, 2606:4700::6812:1713
* IPv4: 104.18.23.19, 104.18.22.19
*   Trying [2606:4700::6812:1613]:443...
*   Trying 104.18.23.19:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* Established connection to w3.org (104.18.23.19 port 443) from 192.168.0.102 port 61517
* using HTTP/1.x
> GET / HTTP/1.1
> Host: w3.org
> User-Agent: curl/8.22.0
> Accept: */*
>
* Request completely sent off
* schannel: remote party requests renegotiation
* schannel: renegotiating SSL/TLS connection
* schannel: SSL/TLS connection renegotiated
< HTTP/1.1 301 Moved Permanently
< Date: Sun, 22 Nov 2026 13:49:27 GMT
< Content-Type: text/html; charset=UTF-8
< Transfer-Encoding: chunked
< Connection: keep-alive
< Location: https://www.w3.org/
< set-cookie: __cf_bm=DysPlrLckvXVNX9llnSG0T29liFu8pc6G2Hi..ZRcC4-1795355367.3178-1.0.1.1-wCBjZoBHDrUKontTq2egYyXQ_bYxBVq.bVKcNiHXUiTFcza67E0F5Ku0cgmiAgjsKdq_R0GrU5wCc2Iydb8mNdv45MosHNO6fNXN1SzPDjbuaMhdk_be5trwhE.mlEb6; HttpOnly; SameSite=None; Partitioned; Secure; Path=/; Domain=w3.org; Expires=Sun, 22 Nov 2026 14:19:27 GMT
< X-Content-Type-Options: nosniff
< Server: cloudflare
< CF-RAY: a5e865c5bc18508e-WAW
< alt-svc: h3=":443"; ma=86400
<
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>cloudflare</center>
</body>
</html>
* Connection #0 to host w3.org:443 left intact

```

---

### A.2. Запит без захисту з'єднання

**Команда:**

```
curl -v http://neverssl.com
```

**Вивід:**

```
* Host neverssl.com:80 was resolved.
* IPv6: (none)
* IPv4: 34.223.124.45
*   Trying 34.223.124.45:80...
* connect to 34.223.124.45 port 80 from 0.0.0.0 port 58018 failed: Timed out
* Failed to connect to neverssl.com:80 after 21162 ms: Could not connect to server
* closing connection #0
curl: (28) Failed to connect to neverssl.com:80 after 21162 ms: Could not connect to server
```

---

### A.3. Запит до служби доменних імен

*Windows: Resolve-DnsName w3.org*

**Команда (перше виконання):**

**Вивід:**

```
Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
w3.org                                         AAAA   600   Answer     2606:4700::6812:1713
w3.org                                         AAAA   600   Answer     2606:4700::6812:1613
w3.org                                         A      600   Answer     104.18.23.19
w3.org                                         A      600   Answer     104.18.22.19dig w3.org

```

**Команда (повторне виконання через 5–7 хвилин):**

**Вивід:**

```
Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
w3.org                                         AAAA   149   Answer     2606:4700::6812:1713
w3.org                                         AAAA   149   Answer     2606:4700::6812:1613
w3.org                                         A      149   Answer     104.18.22.19
w3.org                                         A      149   Answer     104.18.23.19

```

---

### A.4. Контрольний ресурс

**Команда:**

```
curl -v https://google.com
```

**Вивід:**

```
* Host google.com:443 was resolved.
* IPv6: (none)
* IPv4: 142.250.109.102, 142.250.109.113, 142.250.109.138, 142.250.109.101, 142.250.109.139, 142.250.109.100
*   Trying 142.250.109.102:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* Established connection to google.com (142.250.109.102 port 443) from 192.168.0.102 port 58097
* using HTTP/1.x
> GET / HTTP/1.1
> Host: google.com
> User-Agent: curl/8.22.0
> Accept: */*
>
* Request completely sent off
* schannel: remote party requests renegotiation
* schannel: renegotiating SSL/TLS connection
* schannel: SSL/TLS connection renegotiated
< HTTP/1.1 301 Moved Permanently
< Location: https://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-cgp6ahov0XpNfVSBPimegw' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
< Date: Sun, 22 Nov 2026 14:38:56 GMT
< Expires: Tue, 22 Dec 2026 14:38:56 GMT
< Cache-Control: public, max-age=2592000
< Server: gws
< Content-Length: 220
< X-XSS-Protection: 0
< X-Frame-Options: SAMEORIGIN
< Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000
<
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host google.com:443 left intact
```

---

### A.5. Ресурси з некоректною конфігурацією сертифіката

**Випадок 1**

```
curl -v https://expired.badssl.com
```

Вивід:

```
curl : Базовое соединение закрыто: Не удалось установить доверительные отношения для защищенного канала SSL/TLS.
строка:1 знак:1
+ curl -v https://expired.badssl.com
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (System.Net.HttpWebRequest:HttpWebRequest) [Invoke-WebRequest], WebExc
   eption
    + FullyQualifiedErrorId : WebCmdletWebResponseException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand

```

**Випадок 2**

```
curl -v https://wrong.host.badssl.com
```

Вивід:

```
curl : Базовое соединение закрыто: Не удалось установить доверительные отношения для защищенного канала SSL/TLS.
строка:1 знак:1
+ curl -v https://wrong.host.badssl.com
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (System.Net.HttpWebRequest:HttpWebRequest) [Invoke-WebRequest], WebExc
   eption
    + FullyQualifiedErrorId : WebCmdletWebResponseException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand 

```

**Випадок 3**

```
curl -v https://self-signed.badssl.com
```
Вивід:

```
curl -v https://self-signed.badssl.com
curl : Базовое соединение закрыто: Не удалось установить доверительные отношения для защищенного канала SSL/TLS.
строка:1 знак:1
+ curl -v https://self-signed.badssl.com
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (System.Net.HttpWebRequest:HttpWebRequest) [Invoke-WebRequest], WebExc
   eption
    + FullyQualifiedErrorId : WebCmdletWebResponseException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand

```
## Частина B. Власна модель рівнів

**Кількість виділених груп:** 5

| **№** | **Назва групи (власне формулювання)** | **Рядки виводу, віднесені до групи** | **Обґрунтування** |
|---|---|---|---|
| 1 | Запит з діагностикою | &lt;* Request completely sent off * schannel: remote party requests renegotiation * schannel: renegotiating SSL/TLS connection * schannel: SSL/TLS connection renegotiated HTTP/1.1 301 Moved Permanently Date: Sun, 22 Nov 2026 13:49:27 GMT Content-Type: text/html; charset=UTF-8 Transfer-Encoding: chunked < Connection: keep-alive | Пошук домена з діагностикою його вмісту для подальшого використання або діагностики вмісту, для подальших дій. |
| 2 | Доменні імена | >Type   TTL   Section    IPAddress w3.org AAAA   600   Answer     2606:4700::6812:1713 w3.org AAAA   600   Answer     2606:4700::6812:1613 w3.org A      600   Answer     104.18.23.19 w3.org  A      600   Answer     104.18.22.19dig w3.org |Вивід доменних імен з їх TTL та наглядне зображення їх відмінності після різного проміжку часу запиту. |
| 3 | Запит без захисту  | * Host neverssl.com:80 was resolved.* IPv6: (none) * IPv4: 34.223.124.45 *Trying 34.223.124.45:80... * connect to 34.223.124.45 port 80 from 0.0.0.0 port 58018 failed: Timed out * Failed to connect to neverssl.com:80 after 21162 ms: Could not connect to server * closing connection #0 curl: (28) Failed to connect to neverssl.com:80 after 21162 ms: Could not connect to server| Без захисту не вдалося підключитися до neverssl.com, що каже нам про захищення HTTPS |

