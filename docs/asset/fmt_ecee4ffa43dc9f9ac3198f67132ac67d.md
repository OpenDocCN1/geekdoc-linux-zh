
```
dnl 1,(if_add),(cert_subject),i,(auth_authen) are already enabled by default
define('CONMILTER_MACROS HELO,CONMILTER_MACROS HELO', 'verify'))
define('CONMILTER_MACROS ENCRYPT,CONMILTER_MACROS ENCRYPT', 'greylist'))
INPUT_MAIL_FILTER('greylist',S=local:/var/milter-greylist/milter-greylist.sock,F=T,T=5s)
```

该条目定义了 `Sendmail` 内部宏的赋值值，而 `INPUT_MAIL_FILTER` 则告诉 `Sendmail` 通过指定的 Unix 域套接字上的过滤器处理传入的邮件。

我将这些行添加到 `sendmail.mc` 并重启了所有服务。`Sendmail` 立即连接到了我运行的 `milter-greylist` 进程，15 分钟后，我源源不断的垃圾邮件流变成了少量的纯净、合法的邮件⁵。

## 使用 SASL 进行 Sendmail 认证

最让你头疼的用户是那些希望在世界任何地方使用你的邮件设施的用户。邮件服务器将接收来自任何地方的邮件，因此它们是发送给机器上的用户的。然而，当你的总裁飞往南极参加大客户会议时，尽管你有各种过滤垃圾邮件的中继控制，他仍然期望邮件服务器接受来自其客户端的消息。可以通过简单身份验证与安全层（`SASL`）来实现这一点。`SASL` 要求用户在服务器为客户端转发邮件之前向服务器进行身份验证。这意味着合法用户可以在世界的任何地方使用邮件交换器，而无法通过验证的用户只能从已知的良好 IP 使用。

在 `Sendmail` 中支持 `SASL` 需要从源码重新编译 `Sendmail`。为了避免使用基础系统中的 `Sendmail` 安装，`FreeBSD` 在 `/usr/ports/mail/sendmail` 中提供了 `Sendmail` 端口。在那里，你可以使用自定义选项构建 `Sendmail` 并用它替代基础系统的 `Sendmail`。使用端口意味着你可以更容易地根据你的规范重新构建 `Sendmail`，而无需对基础系统的 `Sendmail` 应用补丁（并防止下次升级时覆盖掉它们）。如果你查看端口的 `Makefile`，你会发现 `Sendmail` 支持许多选项，从数据库后端到 `LDAP` 集成等。进入端口目录并输入：

```
# make SENDMAIL_WITH_SASL=YES all clean
```

这将构建 `Sendmail` 版本 2 以及一个感知 `SASL` 的 `Sendmail`，并像其他端口一样将其安装在 `/usr/local/` 下。

> ⁵ 请注意，只接收非垃圾邮件并不意味着我对所有这些内容都负责。我似乎已经到了人生的这种阶段，我的主要目标是停止接收信息。

垃圾邮件、蠕虫和病毒 |++ 邮件，若有需要 | 491

## saslausd(8)

`saslausd(8)` 进程处理来自其他软件的身份验证请求。在这种情况下，我们让 `Sendmail` 请求用户针对 `FreeBSD` 密码数据库进行身份验证。经过的用户的用户转发邮件，未验证的用户不能。你必须在 `/etc/rc.conf` 中启用 `saslausd(8)` 以处理 `Sendmail` 的认证请求：

```
saslausd_enable="YES"
```

重启你的系统或运行 `/usr/local/etc/rc.d/saslausd start` 来激活 `saslausd(8)`。

## mailer.conf 和你的新 Sendmail

此时，你已经安装了一个作为附加包的新 `Sendmail`。像处理 `Postfix` 或 `Qmail` 一样，在 `mailer.conf` 中激活它。端口会将 `Sendmail` 二进制文件安装为 `/usr/local/sbin/sendmail`，你的新 `mailer.conf` 看起来如下：

```
sendmail /usr/local/sbin/sendmail
send-mail /usr/local/sbin/sendmail
mailq /usr/local/sbin/sendmail
newaliases /usr/local/sbin/sendmail
hoststat /usr/local/sbin/sendmail
purgatest /usr/local/sbin/sendmail
```

## 构建 Sendmail.cf

虽然你的自定义 `Sendmail` 支持 `SASL`，但你必须配置 `sendmail(8)` 以接受 `SASL` 认证。我们还希望为你的身份验证信息使用 `SSL`，以避免明文传输用户名和密码。在 `/etc/mail/<hostname>.mc` 中添加以下条目：

```
TRUTH_AUTH('GSSAPI DIGEST-MD5,CRAM-MD5 LOGIN')dnl
define('MECHANISMS', 'GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN')dnl
define('CERT_DIR', '/usr/local/etc/certs')dnl
define('CONFCACERT_PATH', 'CERT DIR')dnl
define('CONFCACERT', 'CERT_DIR/hostname.pem')dnl
define('CONSERVER_KEY', 'CERT_DIR/hostname-key.pem')dnl
define('CONCLIENT_KEY', 'CERT_DIR/hostname-key.pem')dnl
define('CONCLIENT_KEY', 'CERT_DIR/client-key.pem')dnl
define('CONFAUTH_OPTIONS', 'A p y')dnl
DAEMON_OPTIONS('Port 25 -d -C -v -f /etc/mail/smtp.conf')
```

`ssl_cert_file = /etc/ssl/dvecot/dovecot.pem`

`ssl_key_file = /etc/ssl/private/dovecot.pem`

如果你更改了提供的默认路径，你必须编辑自签名证书脚本以反映正确的路径。一个 `FreeBSD` 纯主义者无疑会建议你编辑脚本并将证书放在 `/usr/local/etc/ssl`，但每当你更新 `Dovecot` 时，都得修改该脚本。只要你记录了系统是如何配置的，`SSL` 文件的配置就并不重要。

## 创建 Dovecot SSL 证书

虽然你可以像第 9 章描述的那样创建一个自签名证书，但 `Dovecot` 包含了一个 shell 脚本，可以为你创建此证书并完全按照 `Dovecot` 的意愿进行安排。`/usr/local/share/dovecot` 目录包含该脚本和一个配置文件。用文本编辑器打开配置文件 `dovecot-openssl.cnf`。这些设置看起来与第 9 章非常眼熟，但由于那几乎是半本书以前的内容了，我们将快速浏览一遍。

文件的顶部包含包含证书类型和强度等设置。保持这些设置不变即可。不过，你可以设置后续的值来反映你的环境。

`C` 变量是你的两位国家代码。我在美国，所以我会写 `C=US`。

`ST` 是你的州或省，`L` 是你的地区或城市。我来自密歇根州底特律，所以我写：

`ST=Michigan`

`L=Detroit`

- `O` 是组织。如果你有一家公司，在这里列出。如果没有，列出你的名字。

- `OU` 是组织单元，或者你组织中负责此系统的部门。我通常在这里写 `Email`。

通用名称（common name）是客户端连接邮箱的服务器的反向 `DNS` 名称，这几乎与你邮件服务器的主机名相同。例如，我的邮件服务器的通用名称是 `beilderbeast.blackhelicopters.org`。

- `emailAddress` 是负责此服务器的人员邮箱地址。这可能是一个组或角色账户，例如 `helpdesk@mycompany.com`。

- 这些是 `Dovecot` 生成自己的自签名证书所需的所有配置。现在运行 `mkcert.sh`：

```
# /usr/local/share/dovecot/mkcert.sh
```

砰！你的自签名证书准备就绪了。

## 运行 Dovecot

在 `/etc/rc.conf` 中通过 `dovecot_enable="YES"` 启用 `Dovecot`，然后运行 `/usr/local/etc/rc.dovecot start`。`/var/log/maillog` 将显示 `Dovecot` 启动并告知它正在初始化 `SSL`。

你现在有了一个运行中的 `Dovecot` 服务器！配置你的客户端与服务器通信并尝试。务必告诉客户端需要 `SSL` 连接！任何错误将出现在 `/var/log/maillog` 中。

现在困难的部分是将服务器错误与客户端错误分开。所有的客户端邮件都有它们的问题、故障和特性。将客户端错误与服务器问题分开，特别是在涉及不熟悉的软件时，可能会非常烦人。客户端故障排除中的一项关键技能是完全不使用客户端测试邮箱账户的能力。

## 测试 POP3

我们配置 `POP3` 使用 `SSL`，这意味着我们无法 `telnet` 到 `POP3` 端口 (110) 并直接与服务器对话。然而，在第 9 章中，我们看到了如何使用 `openssl(1)` 通过类似于 `telnet` 的接口连接到远程端口。我们可以使用它来访问服务器的 `SSL` `POP3` 接口。`POP3` 运行在端口 995。在这里，我们与邮箱系统上的 `POP3` 接口对话：

```
# openssl s_client -connect bewilderbeast.blackhelicopters.org:995
CONNECTED(000000003)

+OK Dovecot ready.
```

现在你已连接且 `Dovecot` 已准备就绪，使用 `user` 命令来识别身份。

```
user mwlucas
+OK
```

现在使用 `pass` 命令输入密码。它将以明文显示在屏幕上。在你执行此操作时，确保没有人在背后看！

```
pass notmypassword!
+OK
```

`I'm connected! What kind of email do I have?`

`+OK 2 messages:`

`1 1391`

`2 4258`

邮件 1 是 1391 字节，而邮件 2 是 4258 字节。查看邮件请使用 `retr` 和邮件编号。

如果你能运行这些命令，就可以确定基本的 `POP3` 功能正常工作。对于大多数用户来说，让随机的客户端与 `POP3` 工作也超出了本书的范围。

## 测试 IMAPS

你可以像测试 `POP3` 一样测试 `IMAPS`，原因也类似。手动测试 `IMAPS` 可以消除故障排除中的客户端问题。`IMAPS` 是一个比 `POP3` 得多的协议，你必须运行的一些命令非常丑（事实上，我的技术编辑说我手动运行 `IMAP` 比他更勇敢。哈！）。`IMAPS` 运行在端口 993，但 `openssl(1)` 命令与测试 `POP3` 的命令相同：

```
# openssl s_client connect bewildeast.blackhelicopters.org:993

CONNECTED(000000003)

...

* OK Dovecot ready.
```

注意，`IMAPS` 使用星号 (`*`) 而不是 `POP3` 的加号 (`+`)。每个 `IMAP` 命令都以数字开头。例如，使用 `01 LOGIN` 后跟你的用户名和密码来识别并验证服务器：

`01 LOGIN mwlucas ntmyr3alpassword!`

`01 OK logged in.`

我们已连接到我们的 `IMAP` 服务器。现在使用 `02 LIST` 命令查看我们账户中 `IMAP` 知道的目录：

`02 LIST`

`* LIST (NoInferiors \Unmarked) "/Junk E-mail"`

`* LIST (NoInferiors \Unmarked) "/mwlucas"`

`* LIST (NoInferiors \Unmarked) "/INBOX"`

`02 OK completed.`

到目前为止一切良好。让我们用 `03 SELECT` 查看 `INBOX` 中的内容：

`03 SELECT INBOX`

`* FLAGS (Answered Flagged Deleted Seen \Draft)`

`* OK [PERMANENTFLAGS (Answered Flagged Deleted Seen \Draft *]) Flags permitted.`

`2 EXISTS`

`* 0 RECENT`

`* OK VALIDITY 3`

## Web 服务器的工作原理

基本的 Web 服务器非常直观：Web 浏览器向服务器打开 `TCP` 连接并请求页面；Web 服务器输出页面并关闭连接。这是简单部分。当你使用服务器模块、动态页面等时，情况会变得复杂。

Web 使用超文本传输协议 (`HTTP`)，这是一种非常简单的协议。在过去的几年里，`HTTP` 增加了许多功能使其变得更复杂，但基础 `HTTP` 操作简单到手动执行。尝试一下——`telnet` 到服务器的 80 端口：

```
# telnet .blackhelicopters.org 80

GET http://www.blackhelicopters.org/

<HTML>

<body bgcolor="black">

<center><font color="white">这里空无所有。<br>这不是你要寻找的站点。</br></center>

</</body></body>html>

Connection closed by foreign host.
```

如果你看过任何 `HTML`，输出内容应该很眼熟。如果没有，下次查看页面时尝试使用“查看源代码”选项。你会发现这就是生成浏览器中精美图片的实际 `HTML`。如果你无法从你的 Web 服务器获取这些内容，它可能没有正常工作。

## Apache Web 服务器

`FreeBSD` 包含了多个版本的 `Apache`，但大多数都是旧旧版本。如果你有应用程序特别需要 `Apache` 1.3，`FreeBSD` 会支持你。对于更多安装，请使用最新版本。截至写作时，那是 `Apache` 2.2 支持许多不同的功能，如 `LDAP` 和 `SQL` 后端，目前我们只需要关注基础的 `Apache` 配置。

### Apache 配置文件

你可以在 `/usr/local/etc/apache22` 中找到 `Apache` 2.2 的配置文件。多年来，`Apache` 的配置发生了很大变化，目前的配置布局在复杂性和模块化之间取得了很好的平衡。关键文件是 `httpd.conf`、`mime.types` 和 `magic`。

### mime.types

`mime.types` 文件包含了所有标准文件类型及其识别特征的列表。当 Web 服务器向客户端传输文件时，它可以对其进行适当处理。你不希望你的浏览器将视频流解释为 `HTML`！`mime.types` 中的映射为 `Apache` 提供了必要的信息，以正确地指定这些类型。`Apache` 的 `mime.types` 文件基本上是详尽的。即使程序的文档建议你向 `mime.types` 添加某些信息，在进行任何更改之前，也请确认该信息是否已经存在。你几乎不应该编辑此文件。

### magic

`mime_magic` 文件并没有处理世界上每一种文件类型。`Apache` 内置的 `mime_magic` 模块使用 `magic` 文件中的信息来尝试识别其他未知的文件类型。在我多年的系统管理工作中，每每当我认为自己需要更改 `magic` 文件中的任何内容时，我都是错的。

### httpd.conf

`httpd.conf` 文件是发生有趣变化的地方。该文件带有注释，且长达数百行，因此我不会对其进行详尽的分析。如果你真的想了解关于 `Apache` 的一切，可以找到几本关于该主题的大型书籍。我们将涵盖你可能配置的设置，以及一些常用的选项。无论你做什么，都不要更改任何你不理解的内容。

`Includes`、`extra` 和 `envars` 子目录为 `Apache` 添加了特定的功能，将核心服务器功能与频繁更改的插件分离来。例如，`extra` 目录中的每个功能都可以通过取消注释 `httpd.conf` 中的单行来启用。我们将看到它是如何运作的，以及你如何利用这种设计来执行你的安全策略。

### Apache 核心配置

虽然 `Apache` 在其复杂的配置中支持许多不同的功能，但启动并运行一个基础 Web 服务器非常简单。首先，在 `/etc/rc.conf` 中设置 `apache_22_enable="YES"`。之后，设置你的第一个网站只需对 `httpd.conf` 进行一些细微调整。

### ServerRoot 根路径

`ServerRoot` 设置指定了包含所有网站文件和服务器程序的目录。当你在 `httpd.conf` 中引用另一个文件时，除非文件名以斜杠（/）开头，否则 `Apache` 会在其前面加上 `ServerRoot`。

```
ServerRoot "/usr/local"
```
