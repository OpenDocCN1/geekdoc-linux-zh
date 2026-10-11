
```bash
$ dig -t txt -c chaos VERSION.BIND @192.168.1.1
; <<>> DiG 9.2.1 <<> -t txt -c chaos VERSION.BIND @192.168.1.1
; global options: printcmd
; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 22464
; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL:0

; QUESTION SECTION:
;VERSION.BIND.                CH      TXT

; ANSWER SECTION:
VERSION.BIND.                 0   CH  TXT   "8.3.3-REL"

; Query time: 40 msec
; SERVER: 192.168.1.1#53(192.168.1.1)
; WHEN: Wed Jan 15 09:46:22 2003
; MSG SIZE  rcvd: 64
```

## 枚举远程服务

## 配置 BIND 不显示版本信息

编辑 BIND 配置文件 `named.conf`，并覆盖版本号：

```
options { version "Not available"; }
```

您可能还希望使用特定的 ACL 配置 BIND，并限制来自特定主机的查询。有关详细信息，请参阅 BIND 文档。有关 BIND 的更多信息可在 `http://www.isc.org/products/BIND/` 找到。

## Finger：79（TCP）

Finger 是一个用户信息查询程序。对远程主机执行 Finger 操作将提供诸如用户名、IP 地址、空闲时间以及当时登录该主机的个人的真实姓名等信息。

### 使用 Finger 命令枚举远程用户

如果远程主机正在运行 `finger` 守护进程，可以使用命令行 `finger` 工具来查询该主机：

```
finger @host
```

示例：

```
$ finger @192.168.1.1
Login    Name          TTY     Idle   When     Where
bob      Bob             pts/1    8     Wed 14:26   bobaddress.bobsisp.org
rob      Robert Smith    pts/4   51     Wed 12:46   dhcp.robshomeisp.org
tang     Thomas Tang     pts/3   1:08   Wed 10:07   somecasanexample.com
```

也可以对特定用户名执行 `finger` 操作。即使用户在当时未登录，查询特定用户名也会返回有关该用户的一些信息：

```
finger username@host
```

示例：

```
$ finger root@192.168.1.1
Login name:  root        In real life: Sys Admin
Directory: /        Shell: /usr/local/bin/tcsh
Last login Jan 11 14:26:51 on tty2
```

New mail received Wed Jan 15 14:36:29 2003;

unread since Wed Jan 11 14:29:54 2003

No Plan.

Solaris 的旧版 `finger`（`finger` 守护进程）已知包含一个漏洞，如果使用诸如“`a b c d e f g h`”这样的字符串进行查询，它将泄露该主机上所有用户名的列表：

```
`finger 'a b c d e f g h'@host`
```

有关此漏洞的更多信息，请参阅 `http://www.securityfocus.com/bid/3457/info/`。

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_97_0.png)

### 禁用 Finger

如果您正在运行 `finger` 服务器，强烈建议考虑以下建议：

- 如果可能，请考虑禁用 `finger` 服务。它向本地用户和入侵者提供了有关您系统的过多信息。如果您使用 `inetd`，可以通过注释掉 `/etc/inetd.conf` 中相应的行来禁用 `finger`。如果您使用 `xinetd`，请编辑 `xinetd.d` 目录中名为 `finger` 的文件，并确保存在以下行：

  `disable = yes`

为了使更改生效，您必须重新启动 `inetd` 或 `xinetd`。

- 如果您必须运行 `finger` 服务器，请配置您的防火墙以丢弃到端口 `79` 的传入连接。这将防止外部网络上的用户查询您的主机。

## HTTP（超文本传输协议）：80（TCP）

HTTP 是一种无状态协议，用于分發各种超媒体。它最广泛的用途是提供 WWW（万维网）内容。

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_97_1.png)

### 获取 HTTP 服务器横幅

为了从 HTTP 服务器获取横幅信息，请通过 `telnet` 连接到它们正在监听的端口，并发出以下请求：

```
`HEAD / HTTP/1.0[enter][enter]`
```

例如：

```
`(bash)$ telnet www.somecompanyasanexample.com 80`
`Trying 10.0.0.100...`
`Connected to www.somecompanyasanexample.com.`
```

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_97_2.png)

转义字符为 `'^"'`。

`HEAD / HTTP/1.0 [enter]`

`[enter]`

`HTTP/1.1 200 OK`

`Date: Wed, 15 Jan 2003 17:59:12 GMT`

`Server: Apache/1.3.27 (Unix) PHP/4.2.1 mod_jk/1.2.0 mod_ssl/2.8.12 OpenSSL/0.9.6b`

`Content-Location: index.html.en`

`Vary: negotiate,accept-language,accept-charset`

`TCN: choice`

`Last-Modified: Thu, 09 May 2002 19:47:31 GMT`

`Accept-Ranges: bytes`

`Content-Length: 2673`

`Connection: close`

`Content-Type: text/html`

`Content-Language: en`

`Expires: Wed, 15 Jan 2003 17:59:12 GMT`

`Connection closed by foreign host.`

某些 Web 服务器不允许 `HEAD` 请求。在这种情况下，我们必须执行 `GET` 查询：

`GET / HTTP/1.0[enter][enter]`

此查询将返回横幅信息，以及默认的索引页面（如 `index.html`）。

如果您想请求特定的 Web 页面，例如 `contact.html`，您需要在其名称和路径后附加 `GET` 请求：

`GET /contact.html HTTP/1.0[enter][enter]`

> 有时，单个 Web 服务器可用于提供多个域名的内容。在这种情况下，必须在请求中指定特定的域名。这可以通过在 `GET` 请求后键入 `Host: domain-name` 来完成。例如：

> `GET / HTTP/1.0[enter]`

> `Host: www.domainname.com[enter][enter]`

### 更改 HTTP 服务器横幅

如果您正在运行 Apache，请编辑您的 `httpd.conf` 文件并确保存在以下指令：

`ServerSignature Off`

`ServerTokens Prod`

禁用 `ServerSignature` 标记会指示 Apache 在显示诸如“404-Not Found”错误页面时不打印版本信息。当 `ServerTokens` 指令设置为 `Prod` 时，它会指示 Apache 仅在横幅中显示“Server: Apache”。如果您不想在 Server 标签中显示“Apache”，但想显示诸如“Server: Not-allowed”这样的虚假信息，您需要：

1. 下载 Apache 源代码。
2. 编辑文件 `httpd.h` 并更改行中字符串 “Apache” 的值
