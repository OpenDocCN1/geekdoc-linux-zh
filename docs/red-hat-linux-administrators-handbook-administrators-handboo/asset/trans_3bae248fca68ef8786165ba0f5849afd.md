
## 用于访问网络服务的用户命令

本节讨论的命令使您能够访问各种网络服务。

### finger

语法：

```
finger user@host
```

此程序允许您查询指定主机上的 finger 守护进程。例如，

```
finger kabir@blackhole.integrationlogic.com
```

请求连接到 blackhole.integrationlogic.com 服务器上运行的 finger 守护进程。如果指定主机不允许 finger 连接，此尝试将失败。成功后，finger 请求会显示有关指定用户的信息。如果用户在主目录中有 .plan 文件，大多数传统 finger 守护进程也会显示此文件。由于 finger 已被用于造成安全问题，大多数系统管理员会在其域之外禁用 finger 服务。

### ftp

语法：

```
ftp hostname or IP address
```

这是默认的 FTP 客户端程序。您可以使用此程序连接到 FTP 服务器。例如，

```
ftp ftp.cdrom.com
```

打开到 ftp.cdrom.com 的 FTP 连接并提示您输入用户名和密码。如果您知道用户名和密码，您可以登录 FTP 服务器并上传或下载文件。在 FTP 提示符下，您可以输入 help 或 ? 来获取 FTP 命令的帮助。

### lynx

语法：

```
lynx [-dump] [-head] [URL]
```

lynx 是最流行的交互式文本网页浏览器。要运行浏览器，只需将所需的 URL 作为命令行参数输入即可。例如，

```
lynx http://www.integrationlogic.com/
```

显示该站点的首页。lynx 是一个非常实用的程序。例如，要快速了解站点使用何种类型的 Web 服务器，而无需询问网站管理员，请运行以下命令：

```
lynx -head http://www.integrationlogic.com/
```

上述命令显示 lynx 浏览器从 Web 服务器接收到的 HTTP 头。其输出示例如下所示：

```
HTTP/1.1 302 Moved
Date: Tue, 02 Mar 1999 06:47:27 GMT
Server: Apache/1.3.3 (Unix)
Location: http://www.integrationlogic.com/index.shtml
Connection: close
Content-Type: text/html
```

此头部显示 www.integrationlogic.com 运行在 UNIX 平台上的 Apache 1.3.3 Web 服务器上。请注意，并非所有网站都会公开其 Web 服务器平台信息，但大多数会。如果您想避免交互模式，可以使用 -dump 选项将页面转储到屏幕（STDOUT）。例如，

```
lynx -dump -head http://www.integrationlogic.com/
```

将头部转储到 stdout。-dump 功能非常方便。例如，

```
lynx -dump -head http://webserver/new.gif > new.gif
```

允许您将 Web 服务器主机上的 new.gif 保存到本地名为 new.gif 的文件中。

交互模式允许您以相当不错的方式浏览适合文本浏览器的站点。

### mail

语法：

```
mail user@host [-s subject] [< filename]
```

mail 是默认的 SMTP 邮件客户端程序。您可以使用此程序从系统发送或接收邮件。例如，如果您在不带任何参数的情况下运行此程序，它会显示一个 & 提示符并通过数字列表显示当前未读邮件。要读取邮件，输入索引号，邮件将被显示。要了解有关 mail 的更多信息，请在 & 提示符下使用 ? 命令。

要向名为 kabir@integrationlogic.com 的用户发送主题为 "About your Red Hat book" 的邮件，请运行

```
mail kabir@integrationlogic.com -s "About your Red Hat book"
```

然后您可以输入邮件内容并按 Ctrl+D 结束邮件。在撰写模式下，您可以在行首输入 ~v 切换到默认文本编辑器。

如果您已在文件中准备好邮件，请使用如下命令发送：

```
mail kabir@nitec.com -s "About your Red Hat book" << feedback.txt
```

这将发送一封带有指定主题行的邮件；邮件内容为 feedback.txt 文件的内容。

### pine

语法：

```
pine
```

pine 是一个全屏 SMTP 邮件客户端，使用起来非常友好。如果您通常通过 Telnet 使用邮件客户端，您一定应该尝试此程序。

由于其用户友好的界面，它适合尚未熟悉 Linux 的 Linux 用户。

### rlogin

语法：

```
rlogin [-l username] host
```

rlogin 命令允许您远程登录到主机。例如，要登录名为 shell.myhost.com 的主机，请运行

```
rlogin shell.myhost.com
```

由于 rlogin 不被认为安全，我建议您仅在封闭的局域网环境中使用它。-l 选项允许您指定用于身份验证的用户名。如果您想在不输入密码的情况下远程登录主机，请在用户主目录中创建 .rhosts 文件。添加您将用于发出 rlogin 请求的计算机的主机名或 IP 地址。再次强调，由于许多人认为这是一种安全风险，我不建议广泛使用 rlogin。

### talk

语法：

```
talk username tty
```

如果您需要向另一用户发送消息，电子邮件效果很好。但是，如果您需要与另一用户实时通信，类似于电话交谈，请使用 talk 命令。要与已登录的另一用户交谈，请使用以下命令：talk ronak@csus.edu 您请求的 user 必须接受您的 talk 请求。用户接受您的 talk 请求后，您可以开始互相交谈（输入）。talk 程序在任一方执行 Ctrl+C（intr 键）时终止。

### telnet

语法：

```
telnet hostname or IP address [port]
```

这是默认的 Telnet 客户端程序。您可以使用此程序连接到 Telnet 服务器。例如，如果指定主机运行 Telnet 服务器，以下命令将打开到 shell.myportal.com 系统的 Telnet 连接：

```
telnet shell.myportal.com
```

连接打开后，您将被提示输入用户名和密码。登录成功后，您可以访问 Telnet 服务器上的本地用户账户。

### wall

语法：

```
wall
```

wall 命令允许您向所有用户的终端发送文本消息，只要他们未通过 mesg 命令禁用其 tty 的写访问权限。输入 wall 后，您可以输入单行或多行消息，然后按 Ctrl+D 发送。

## 网络管理员命令

本节讨论的命令使您能够收集有关网络服务和网络本身的信息。

### host

语法：

```
host [-a] host IP address
```

默认情况下，host 程序允许您快速检查主机 IP 地址。如果使用 -a 选项，host 会返回有关指定主机或 IP 地址的各种 DNS 信息。

### hostname

语法：

```
hostname
```

此程序显示系统的主机名。

### ifconfig

语法：

```
ifconfig [interface] [up | down] [netmask mask]
```

ifconfig 程序允许您配置网络接口。您也可以使用此程序查看接口的状态。例如，如果您之前已为 Red Hat Linux 系统配置了网络，并且有一个预配置的网络接口设备 eth0，您可以运行以下命令：

```
ifconfig eth0
```

您应该会看到类似以下内容的输出：

```
eth0 Link encap:Ethernet HWaddr 00:C0:F6:98:37:37
inet addr:206.171.50.50 Bcast:206.171.50.63
Mask:255.255.255.240
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:9470 errors:0 dropped:0 overruns:0 frame:0
TX packets:7578 errors:0 overruns:0 carrier:0
collisions:0
Interrupt:5 Base address:0x340
```

这里，ifconfig 报告网络接口设备 eth0 具有 Internet 地址（inet addr）206.171.50.50、广播地址（Bcast）206.171.50.63 和网络掩码（255.255.255.240）。其余信息显示该接口迄今为止接收了多少数据包（RX packets）、发送了多少数据包（TX packets）、迄今为止发生了多少种不同类型的错误、该设备使用什么中断地址线、使用什么 I/O 地址基址等等。
