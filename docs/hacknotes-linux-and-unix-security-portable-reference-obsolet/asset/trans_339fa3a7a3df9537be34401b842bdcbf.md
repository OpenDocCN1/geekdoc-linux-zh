
# HTTP（超文本传输协议）：80（TCP）

HTTP 是一种无状态协议，用于分发各种超媒体。它最常用于提供万维网（WWW）内容。

> 手动检查所有可能的 HTTP 错误配置和漏洞是不可能的。诸如 Nikto 之类的自动化工具（可从 [http://www.cirt.net/code/nikto.shtml](http://www.cirt.net/code/nikto.shtml) 获取）在 Web 服务器和应用评估方面表现良好，应使用这些工具来检查错误配置和漏洞。

## 暴力破解
可以使用 Hydra 等工具对 HTTP 身份验证进行暴力破解。

## 暴力破解 HTTP 身份验证

Hydra 是一种支持 HTTP 的暴力破解工具，可用于暴力破解受密码保护的 HTTP 资源。以下是使用 Hydra 暴力破解 HTTP 身份验证的示例：

```
hydra -L usernames.txt -P passwords.txt www.somecompanyanexample.com http
```

## 预防 HTTP 暴力破解

请参阅“针对暴力破解攻击的常见防御措施”。

## 嗅探
由于 HTTP 是明文协议，网络段上的恶意用户可以监视另一个用户的 HTTP 流量。

## 嗅探 URL

随 Dsniff 分发的 urlsnarf 程序可用于嗅探用户在网络上发送的 HTTP 请求：

```
[bash]$ urlsnarf
Kernel filter, protocol ALL, raw packet socket
urlsnarf: listening on eth0 [tcp port 80 or port 8080 or port 3128]
10.0.0.1 -- [19/Feb/2003:21:50:16 -0800] "GET http://
www.mozilla.org/start/ HTTP/1.1" -- - *"Mozilla/5.0 (X11; U; Linux
1686; en-US; rv:1.3a) Gecko/20021212"*
10.0.0.1 -- [19/Feb/2003:21:50:42 -0800] "GET http://cirt.net/
HTTP/1.1" -- - *"Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.3a) Gecko/
20021212"*
10.0.0.1 -- [19/Feb/2003:21:50:42 -0800] "GET http://cirt.net/
images/bg.gif HTTP/1.1" -- - *"Mozilla/5.0 (X11; U;
Linux i686; en-US; rv:1.3a) Gecko/20021212"*
10.0.0.1 -- [19/Feb/2003:21:50:42 -0800] "GET http://cirt.net/images/cirt_headline.gif HTTP/1.1" -- "http://cirt.net/" "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.3a) Gecko/20021212" 
10.0.0.1 -- [19/Feb/2003:21:50:42 -0800] "GET http://cirt.net/images/pix.gif HTTP/1.1" -- "http://cirt.net/" "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.3a) Gecko/20021212"
```

同样随 Dsniff 分发的 webspy 程序是另一个出色的 HTTP 嗅探工具。一旦它在网络上检测到 HTTP 请求，就会将其发送到正在运行的 Netscape 进程。这使得网络上的恶意用户能够实时监视受害者的 HTTP 会话。

## 嗅探 HTTP 数据

Etercap 可用于嗅探网络上发送的 HTTP 流量：

```
[bash]$ ettercap -t cpc -N -8 ANY:80

ettercap 0.6.7 (c) 2002 ALoR & NaGA Your IP: 10.0.0.1 with MAC: 00:01:01:3a:4a:b2 on Iface: eth0
Loading plugins... Done.
Resolving 1 hostnames...
* |=================================================> 100.00 %
Press 'h' for help...
Sniffing (IP based): ANY:80 <--> ANY:0 TCP packets only...

22:15:33 10.0.0.1:37725 --> 192.168.1.1:80 proto: T
GET / HTTP/1.0.
Host: mozilla.org.
Accept: text/html, text/plain, application/vnd.sun.xml.writer, application/vnd.sun.xml.writer.global, application/vnd.stardivision.writer, application/vnd.stardivision.writer-globol, application/x-starwriter, application/vnd.sun.xml.writer.template.
Accept: application/vnd.sun.xml.calc, application/vnd.stardivision.calc, application/x-starcalc, application/vnd.sun.xml.calc.template, application/vnd.sun.xml.impress, application/vnd.stardivision.impress, application/vnd.stardivision.impress-packed.
Accept: application/x-starimpress, application/vnd.sun.xml.impress.template, application/vnd.sun.xml.draw, application/vnd.stardivision.draw, application/x-star draw, application/vnd.stardivision.math, application/vnd.sun.xml.math, Accept: application/vnd.stardivision.math, application/x-starmath, audio/mod, image/*, video/mpeg, video/*, application/pgp, application/pdf, application/postscript, message/partial, message/external-body, x-bez, application/andrew-inset, text/richtext.
Accept: text/enriched, x-sun-attachfile, audio/file, posterxml-file, default, mail-file, sun-dekoket-message, application/x-metamail-patch, application/mseword, audio/x-pn-realaudio, audio/vnd.rn-realaudio, application/emil, text/vnd.rn-richtext.
Accept: application/x-shockwave-flash2-preview, application/sdp, application/x-sdp, application/vnd.rn-realmmedia, audio/wav, audio/x-wav, audio/x-pn-wav, audio/x-pn-windows-acm, audio/basic, audio/x-pn-au, audio/aiff, audio/x-aiff, audio/x-pn-aiff, Accept: text/sgml, */*; q=0.01.
Accept-Encoding: gzip, q=compress.
Accept-Language: en.
User-Agent: Lynx/2.8.5dev.7 libwww-FM/2.14 SSL-MM/1.4.1 OpenSSL/0.9.6b

22:15:33 192.168.1.1:80 --> 10.0.0.1:37725 proto: T
HTTP/1.1 200 OK.
Date: Thu, 20 Feb 2003 06:21:30 GMT.
Content-Type: text/html.
Last-modified: Wed, 12 Feb 2003 13:13:05 GMT.
Content-length: 17831.
Accept-ranges: bytes.
Connection: close.

22:15:33 192.168.1.1:80 --> 10.0.0.1:37725 proto: T

<HTML>
<TITLE>Welcome to somecompanyasanexample.com's Web-Site:</TITLE>
</HEAD>
<BODY>
<H1>Welcome!</H1>
</BODY>
</HTML>
```

## 嗅探 HTTP 身份验证

受限的 HTTP 位置需要身份验证。由于 HTTP 是明文的，这些信息可以被 Ettercap 嗅探到：

```
[bash]$ ettercap -m -C -N

ettercap 0.6.7 (c) 2002 ALoR & NaGA

Your IP: 192.168.1.1 with MAC: 00:00:02:13:C1:13 on iface: eth0
Loading plugins... Done.
Resolving 1 hostnames...
* |=============================================================================>| 100.00 %

Press 'h' for help...

Sniffing (MAC based): ANY <--> ANY
TCP + UDP packets... (default)
Collecting passwords...

23:54:24 192.168.1.1:36304 <--> 10.0.0.1:80                 http
USER: root
PASS: myApach3BOX!@#

http://10.0.0.1/intranet/private/administration
```

## 使用 HTTPS

在提供关键和私人数据时，使用 HTTPS 代替 HTTP。

## HTTP 错误配置
通常，Web 服务器会被错误配置，或者以默认配置放入生产网络中。接下来的几段描述了一些常见的利用错误配置。

## 自动索引
当开启自动索引时，如果不存在索引文件（如 index.html），Web 服务器将显示目录的内容。

通常，Web 内容作者错误地将包含敏感信息的文件放置在 Web 根目录内，如果显示目录内容，未经身份验证的用户可以轻松查看这些文件。

## 关闭索引
Apache 用户可以在 `httpd.conf` 中使用 `IndexIgnore` 指令指示服务器关闭索引。

## 获取源代码、配置、统计和密码资源
许多 HTTP 服务器被错误配置，以至于提供了关键文件。以下是一些示例：

- CGI 应用程序的源代码可能包含数据库的用户名和密码。许多 Web 应用程序使用后缀为 .inc 或 .conf 的配置文件。这些文件可能包含系统和密码信息，并且经常被错误配置的 Web 服务器提供。
- Web 服务器统计程序将结果输出到诸如 /stats 等目录，这些目录通常位于 Web 根目录内。
- Apache 允许用户通过在目录中放置名为 .htaccess 的文件来保护目录免受密码保护。.htaccess 文件包含关于密码文件（通常称为 .htpasswd）位置的信息，该文件包含允许账户的密码哈希值。通常，Apache 未配置为限制提供 .htaccess 和 .htpasswd 文件。一旦入侵者访问了 .htpasswd 文件，就可以使用诸如 john 这样的暴力破解工具进行破解。

## 不要提供关键资源
配置您的 Web 服务器以不提供敏感文件。如果使用 Apache，请编辑 `httpd.conf` 文件以拒绝提供具有特定后缀的文件。例如，以下指令禁止提供文件名以 .ht 开头的文件：

```
<Files ~ "^\.ht"> 
    Order allow,deny 
    Deny from all
</Files>
```

![](img/77287f6ef97ef0bed6e23f6610950d06_135_0.png)

