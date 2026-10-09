
第一条规则对其处理的每封邮件添加一个 `X-Spam-Flag` 行。第二条规则检查此邮件上此标记的值。如果 `X-Spam-Flag` 行包含 `YES`，第二条规则将邮件移动到名为 `spam`（垃圾邮件）的文件夹（见图 20-2）。由于在“高级”（Advanced）选项卡中勾选了“如果过滤器匹配，停止处理”（If filter matches, stop processing here），KMail 将不再进一步处理标记为垃圾邮件的消息。未被标记为垃圾邮件的消息可以由其他规则处理。

# 图 20-2. 第二条规则检查 X-Spam-Flag

[查看全尺寸图像]

![](img/0f75ae90508d45878c00a5b098fe29d4_871_1.png)

### SELinux

当 SELinux 设置为使用目标策略（targeted policy）时，垃圾邮件守护进程 `spam` 会受 SELinux 保护。如有必要，你可以禁用此保护。更多信息请参阅第 402 页的“使用 system-config-securitylevel 设置目标策略”。

## 网页邮箱 (Webmail)

传统上，你使用如 KMail 等专用邮件客户端读取邮件。最近，使用 Web 应用程序读取邮件已变得越来越普遍。如果你拥有 Gmail、HotMail 或 Yahoo! Mail 等商业提供商的邮箱账户，你可以使用 Web 浏览器读取邮件。以这种方式读取的邮件被称为`网页邮箱（Webmail）`。与专用客户端上的邮件不同，你可以在互联网上任何可以打开浏览器的地方读取网页邮箱：例如，你可以在网吧或或朋友的电脑上检查邮件。

`SquirrelMail`（`squirrelmail`）软件包提供 Web 服务；`SquirrelMail` 文件位于 `/usr/share/squirrelmail` 内部。如果你想运行 `SquirrelMail`，你必须运行 `IMAP (647)`，因为 `SquirrelMail` 使用 `IMAP` 来接收和身份验证邮件。你还必须运行 `Apache`，以便用户可以使用浏览器连接到 `SquirrelMail`。

`SquirrelMail` 是模块化的：你可以使用插件轻松添加功能。有些插件允许你共享日历，有些插件允许你通过 Webmail 界面更改密码。更多信息请参阅 `SquirrelMail` 网站的插件部分。

创建以下链接以便通过 Web 访问 `SquirrelMail`：

```bash
ln -s /usr/share/squirrelmail /var/www/html/mail
```

建立此链接后，你可以将 Web 浏览器指向 `http://localhost/mail` 来显示 `SquirrelMail` 登录页面（见图 20-3）。

# 图 20-3. SquirrelMail 登录页面

[查看全尺寸图像]

![](img/0f75ae90508d45878c00a5b098fe29d4_873_0.png)

接下来使用 `/usr/share/squirrelmail/config` 中的 `conf.pl` 脚本配置 `SquirrelMail`：

```bash
# cd /usr/share/squirrelmail/config
# ./conf.pl
SquirrelMail Configuration : Read: config_default.php (1.4.0)
```

主菜单：

1. 组织偏好
2. 服务器设置
3. 文件夹默认值
4. 通用选项
5. 主题
6. 地址簿
7. 每日消息 (MOTD)
8. 插件
9. 数据库
10. 语言

- `D`: 为特定的 IMAP 服务器设置预定义设置
- `C`: 开启颜色
- `S`: 保存数据
- `Q`: 退出

命令：

要让 `SquirrelMail` 工作，你必须设置的项目是服务器的域名（从“服务器设置”页面获取）。

## 邮件列表

如果你需要向大群人员发送邮件，邮件列表可以成为一项资产。与在邮件的“收件人”（To）或“抄送”（Cc）中列出大量收件人或逐一发送邮件相比，邮件列表具有多个优势：

- 匿名性：收件人看不到其他收件人的地址。
- 存档：发送的邮件将存储在中心位置。
- 访问控制：你可以轻松控制谁可以发送邮件。
- 一致性：向邮件列表发送的邮件将保持一致。
- 效率：邮件列表不会导致服务器过载。

邮件列表支持 `IMAP` 和 `POP3` 协议。邮件列表允许用户通过这些协议接收邮件。邮件列表的配置存储在 `/etc/dovecot` 中。在配置邮件列表之前，你可能需要修改 `/etc/dovecot.conf`。查看 `/usr/share/dovecot` 以获取更多信息。

在 `dovecot.conf` 中添加以下行，以允许邮件列表使用 `SSL`：

```conf
ssl = yes
```

在 `/etc/dovecot/conf.d/10-master.conf` 中，添加或修改以下端口：

```conf
pop3_port = 995
```

为了启用 `SSL`，你需要修改 `/etc/dovecot.conf`。

**`dovecot` SSL 证书**

在 `/etc/dovecot/conf.d/ssl.conf` 中添加以下内容：

```conf
ssl_cert = /etc/ssl/certs/dovecot.pem
ssl_key = /etc/ssl/private/dovecot.pem
```

`dovecot` 默认使用这些证书。你可以使用以下命令生成它们：

```bash
openssl req -x509 -nodes -newkey rsa:2048 -keyout -out /etc/ssl/certs/dovecot.pem -days 365
```

在 `/etc/dovecot/conf.d/10-auth.conf` 中，添加以下内容以允许明文登录：

```conf
auth_mechanisms = login
```

在 `/etc/dovecot/conf.d/10-ssl.conf` 中，添加以下内容以启用 `SSL`：

```conf
ssl = yes
ssl_cert = /etc/ssl/certs/dovecot.pem
ssl_key = /etc/ssl/private/dovecot.pem
```

重启 `dovecot` 以应用更改：

```bash
service dovecot restart
```

# 发送和接收消息设置

| 名称 | 类型 |
| --- | --- |
| Rose | smtp (默认) |

## 身份

KMail 为你设置了一个基础身份。点击`身份 (Identities)` 按钮显示身份页面。在此页面中，你可以创建新身份并修改现有身份，例如 KMail 为你创建的默认身份。你可以指定你的电子邮件地址、回复地址（如果与你的电子邮件地址不同）、KMail 自动附加到你发出的邮件中的签名以及更多设置。

## 帮助

KMail 提供有关如何设置 KMail 发送和接收电子邮件的帮助。点击任何 KMail 窗口左下角的`帮助 (Help)` 按钮，即可显示在线配置 KMail 手册（KDE 帮助中心的一部分）的相应页面。

## 账户

一旦你有了身份，就需要设置传入和出站账户。点击`账户 (Accounts)` 按钮显示账户页面，你可以在此处设置发送和接收消息的账户。该页面有两个标签页：发送和接收。

## 出站账户

点击账户页面上的`发送 (Sending)` 标签页显示出站账户。出站账户默认使用本地系统上的 `sendmail`。如果你使用本地 `sendmail`，则需要按照第 60 页的[快速入门 I：在客户端上配置 sendmail](http://www.bisenter.com) 中的说明进行配置。如果你正在使用 `SMTP`，则需要删除 `sendmail` 账户并添加 `SMTP` 账户。要执行此操作，高亮 `sendmail` 账户并点击`删除 (Remove)`，然后点击`添加 (Add)` 显示添加传输窗口，你可以在其中选择 `sendmail` 或 `SMTP`。

## 传入账户

点击账户页面上的`接收 (Receiving)` 标签页显示传入账户；没有默认的传入账户。点击`添加 (Add)` 显示添加账户窗口，你可以在此处选择账户，如本地邮箱箱、`POP` 或 `IMAP`。如果你从本地和 ISP 接收邮件，你需要设置两个账户。对于 `POP` 或 `IMAP` 账户，你需要指定服务器（主机）以及你在服务器上的用户名和密码。如果你想让 KMail 定期检查邮件，请开启`启用间隔邮件检查 (Enable interval mail checking)` 并指定 KMail 检查邮件的频率。

你不需要更改其他页面上的任何设置。以下是你在配置 KMail 页面上将找到内容的摘要：

- **身份 (Identities)**：在“常规”标签页中指定一个或多个包含名称和地址的身份；在“签名”标签页中指定签名；在“配置”标签页中使用 PGP 或 GnuPG (92) 以及你的 OpenPGP 密钥。
- **账户 (Accounts)**：指定 KMail 的工作方式，包括字体、颜色、布局和头部。
- **外观 (Appearance)**：指定发送消息的外观以及在回复或转发消息时包含哪些头部。
- **安全 (Security)**：安全功能，包括你想以 HTML 还是纯文本接收 HTML 消息。以 HTML 接收 HTML 消息可能会降低系统的安全性。
- **杂项 (Misc)**：KMail 的其他选项，包括你收到的警告、已读邮件的标记方式以及退出 KMail 时发生的情况。

KMail 有很多选项。使用`帮助 (Help)` 按钮获取协助。将 KMail 设置为基础非常简单。随着你越来越熟悉它的使用，可以更大程度配置 KMail 来替你处理更多任务。

## 身份验证中继

如果你带着笔记本电脑等便携式电脑旅行，可能会在每个工作地点通过不同的连接到互联网。也许你为了工作而旅行，或者你只是在晚上将笔记本带回家。

如果你始终通过 ISP 拨号接入网络，则本节不适用。在这种情况下，你始终连接到 ISP 的网络，就像你从未移动过电脑一样。

在笔记本电脑上，你并不使用 `sendmail` 实例来发送电子邮件。相反，使用 `SMTP` 连接到 ISP 的 SMTP 服务器，由其中继发出的邮件。为了避免为任何人中继邮件（包括发送垃圾邮件的恶意用户），SMTP 服务器会限制其邮件中继。通过实施身份验证，你可以让 SMTP 服务器根据用户识别进行身份验证。此外，当你从邮件客户端发送邮件并使用 SMTP 服务器时，SMTP 可以对通信进行加密。

与普通连接相比，经过身份验证的中继具有以下优势：

- 你可以从任何互联网连接发送电子邮件。
- 安全连接使得邮件在通过互联网传输时更难被拦截。
- 出站邮件服务器需要身份验证，防止其被用于发送垃圾邮件。

你通过创建 SSL 证书或使用现有的证书来设置身份验证中继，在 sendmail 中启用 SSL，并告诉你的邮件客户端使用 SSL 连接到 SMTP 服务器。如果你有来自 Verisign 等公司的 SSL 证书，可以跳过下一节（在下一节中创建一个自签名证书）。

# 为 sendmail 创建自签名证书

## FEDORA

SSL 证书的默认位置是 `/etc/pki/tls/certs`（PKI 代表公钥基础设施）。以 root 身份操作，如有必要使用 `mkdir` 创建此目录，并使用该目录下的 `Makefile` 生成所需的证书。Apache 使用特定程序创建证书（第 822 页）。

```bash
# cd /etc/pki/tls/certs
# make sendmail.pem
```

正在生成 1024 位 RSA 私钥
......
++++++++
正在将新私钥写入 '/tmp/openssl.q15963'
...

文档由一个未注册的 Chmag 创建，请访问 http://www.bisenter.com 注册它。谢谢。

你将被要求输入将整合到你的证书中的信息。

你即将输入的内容被称为别名（Distinguished Name，简称 DN）。

有许多字段可以留空
某些字段将有一个默认值，
如果你直接回车，该字段将留空。

- 国家名称（2 位代码） [GB] US
- 州或省（名称） [Berkshire] California
- 所在地（例如，城市） [Newbury] San Francisco
- 组织名称（例如，公司） [My Company Ltd] Sobell Associates Inc.
- 组织单位名称（例如，部门）[]
- 通用名称（例如，你的名称或服务器主机名）[] sobell.com
- 电子邮件地址 [mgs@sobell.com]

你可以在证书中输入你想要的任何信息。

## RHEL

SSL 证书的默认位置是 `/usr/share/ssl`。在执行如上面说明的 `make sendmail.pem` 命令之前，如有必要，使用 `mkdir` 创建此目录，然后进入该目录。

## 在 sendmail 中启用 SSL

一旦你有了证书，通过向 `sendmail.mc` 添加以下行来指示 `sendmail` 使用它：

```conf
define(AUTH_OPTIONS, 'a p')
TRUST_AUTH_MECH('EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN')
```

这些行中的第一行使用 `sendmail` 验证用户中继。接下来的两行指定身份验证机制。
`AUTH_OPTIONS` 的第一个选项 `A` 指示 `sendmail` 在身份验证成功时使用 `AUTH` 参数。第二个选项 `P` 指示 `sendmail` 在不安全的连接允许允许被数据嗅探器破解的身份验证方法。

现在向 `sendmail.mc` 添加以下行以告知 `sendmail` 证书的位置：

```conf
define('CERT_DIR','etc/pki/certs')
define('CACERT_PATH','CERT_DIR')
define('CACERT_CERT','CERT_DIR/sendmail.pem')
define('SERVER_CERT','CERT_DIR/sendmail.pem')
define('SERVER_KEY','CERT_DIR/sendmail.pem')
define('CLIENT_CERT','CERT_DIR/sendmail.pem')
define('CLIENT_KEY','CERT_DIR/sendmail.pem')
```
