
这是一个简单的电子邮件客户端。在主题行输入任何想要的内容，然后你输入的所有内容都是你正在编写的消息的一部分。在行首输入句号 (`.`) 然后按回车键即可完成消息。在 `CC:` 处再次按一次回车键。

如果你与 ISP 有 `PPP` 连接，那么你的消息将立即投递。否则，你的拨号程序将建立连接并投递你的消息。登录你的 ISP 账户检查你的消息。如果运行正常就太好了，但如果没有，请检查本章中的“故障排除”部分。

重启 `sendmail` 守护进程让其重新读取配置文件。

```
/etc/rc.d/init.d/sendmail restart
```

## 安装 imap

为了让 Netscape 客户端能够访问 `sendmail` 分发的电子邮件，需要安装 `map` RPM 包。以 `root` 登录并按如下方式操作：

```
rpm -ivh /mnt/cdrom/RedHat/RPMS/imap*
```

`imapd` 守护进程由 `inetd` 守护进程启动。如果你查看 `/etc/inetd.conf` 文件，你会发现有一个 `imapd` 的条目。每当 Netscape 或任何基于 `imap` 的电子邮件客户端查询 `atlas`（邮件服务器）时，`imapd` 守护进程就会启动并协商邮件的投递。

## 第三部分：将你的网络连接到互联网

> 你可以使用邮局协议 (`POP`) 来实现此功能。然而，`POP` 不负责投递出站邮件，这将要求你在每个客户端工作站上都设置 `sendmail`。这并不困难，但如果你从除 `atlas` 之外的每个 Linux 工作站中完全移除 `sendmail`，将提高安全性。此外，Windows 不运行 `sendmail`，因此唯一的全站位置是使用 `usesqcup`。

## 配置 Fetchmail 用于外部获取

`Fetchmail` 可用于获取远程账户上单个用户的队列邮件。当用于单个用户时，它的工作方式与你使用 Netscape 电子邮件相同。参见“为单个用户配置 Fetchmail”节。

`Fetchmail` 还可以下载多个用户的电子邮件。这被称为多拨模式 (`multidrop mode`)。参见“为多个用户配置 Fetchmail”节。

为了使用多拨模式，你必须有一个注册域名。下面的“注册你的域名”节描述了该过程。

## 注册域名

本章描述的本地电子邮件服务器依赖于将所有邮件通过单个账户。你可能已经在 `InterNIC` 注册了域名。截至 1999 年春季，注册两年费用为 70 美元。

> 注册域名并通过单个账户路由所有邮件的替代方案是付你的 ISP 为每个用户创建一个账户。你需要创建一个独立的 `fetchmail` 进程来获取每个用户的邮件。

## 为单个用户配置 Fetchmail

`Fetchmail` 从用户主目录下的 `.fetchmailrc` 文件获取配置。`fetchconf` 程序提供了一个交互式配置 GUI。然而，这里提供了一个可以用于 `paunchy.net` 网络的示例配置文件。在本示例中它用于用户 `rod bush`。

要配置你自己的 `fetchmail`，登录 `root`，挂载 CD-ROM 并安装 `fetchmail`。

```
rpm -ivh /mnt/cdrom/RedHat/RPMS/fetchmail*
```

创建示例用户 `Rod Bush`。

```
useradd rbush
passwd iwantmail
```

从随附 CD-ROM 拷贝配置文件。

```
cd /home/rubush
cp /mnt/cdrom/IG/e-mail/fetchmailrc.sampleuser ./fetchmail
chown rubush.rubush /home/rubush/.fetchmail
```

将其更改为包含你的 ISP 登录名和密码。

```
# Configuration created Fri Apr 9 22:28:57 1999 by fetchmail
set postmaster "root"
poll mail.myisp.com with proto POP3
user rbush there with password "iwantmail" is rbush here
options fetchmail
```

* `postmaster` 参数告知 `sendmail` 程序，未识别的或此类消息应转发给 `root` 用户。
* `poll mail.myisp.com with proto POP3` 告诉 `fetchmail` 去你的 ISP 邮件服务器并使用 `POP3` 协议（`IMAP` 和其他协议也可以使用）。
* `user` 行告诉 `fetchmail` 你的 ISP 用户名和密码分别是 `rbush` 和 `iwantmail`，并且该账户中的任何电子邮件都应该发送到本地用户 `Rod Bush`。
* `fetch` 选项告诉 `fetchmail` 下载 `widget_inc` 邮件队列中的所有消息。

你的 `.fetchmail` 文件包含你的 ISP 密码，因此请通过输入命令更改权限，使得只有用户可以读写该文件：

```
chmod 0600 .fetchmailrc
```

一旦运行 `fetchmail` 并下载了给 `rod_bush` 的电子邮件，就可以使用 Netscape 邮件客户端（或任何支持 `POP` 或 `IMAP` 的邮件程序）来查看邮件了。

你可以通过更改本地用户名来修改 `.fetchmail` 文件，以获取另一个用户的电子邮件。例如，要使用该脚本获取 `gabe_aragon` 的邮件，请按如下方式修改 `user` 行（你也应该创建该账户 - 执行 `adduser gabe_aragon`）：

```
user "rbush" there with password "iwantmail" is garagon
```

这种方法的问题在于，每个想要接收电子邮件的人都需要在 ISP 拥有一个独立的账户。这完全可以安排，而且价格不会昂贵。它的工作原理与之前在“使用 Netscape 邮件客户端”章节中描述的直接使用 Netscape 访问 ISP 的相同。个人使用 `fetchmail` 的优势在于，它可以自动下载特定用户的电子邮件，而无需配置本地的 `sendmail`、`fetchmail` 和 `procmail` 系统。当你从邮件列表接收邮件时，投递可能会成为问题。列表通常没有你的显式电子邮件地址。个人单独使用 `fetchmail` 解决了这个问题，因为每条消息都会直接下载到每个用户的本地账户。

## 为多个用户配置 FETCHMAIL

`Fetchmail` 可以由 `root` 运行，以检索整个私有网络的电子邮件。这被称为多拨模式（`multidrop mode`），在这种模式下，`fetchmail` 被配置为读取邮件的目标字段并将其转换为本地域名。如果这两个字段不匹配（例如，我收到了来自 `samba@samba.anu.au` 列表的邮件，这与我的 ISP 用户名不匹配），邮件将不会投递到你的本地账户。相反，它会被发送给管理员（在本例中是 `root`）。

使用此方法以 `root` 身份登录并创建如下：

```
adduser widget_inc
passwd widget_inc
```

### 第 13 章：配置 Linux 邮件服务器

将多拨模式的 `.fetchmailrc` 文件复制到 `root` 的家目录。

```
cp /mnt/cdrom/email/fetchmailrc.multidrop /root/.fetchmailrc
```

你的 `.fetchmail` 文件包含你的 ISP 密码，因此请更改权限，使得只有用户可以读写该文件。

```
chmod 0600 .fetchmailrc
```

下面是带有多拨模式的 `fetchmail` 配置文件。

```
# Configuration created Fri Apr 9 22:08:58 1999 by fetchmailconf
set postmaster "root"
poll mail.misp.com with POP3
  localdomains paunchy.net
    user "widget_inc" there with password "iwantemail" is * here
  options fetchmail
```

* `localdomains` 行告知 `fetchmail`，它正在服务的私有网络域名是 `paunchy.net`。这告诉 `fetchmail` 将邮件从一个域名传输到另一个域名。例如，在你的 ISP 账户 `widget_inc` 中显示的 `rod_bush@paunchy.net` 邮件将被传输到 `rod_bush` 的本地邮件账户。
* `user` 行使用星号 (`*`) 表示单个用户用户名。这通知 `fetchmail`，任何显示为 `paunchy.net` 域名的邮件都将被下载并转换为相应的邮件账户。

现在尝试通过你的多拨模式 `fetchmail` 获取邮件。登录你的用户账户，并向你的两个或多个本地用户发送邮件。

从你的 Linux 邮件服务器 (`atlas`) 以 `root` 身份登录并运行 `fetchmail`。你的拨号器应该拨接到你的 ISP 并建立 `PPP` 连接。

## 调度 FETCHMAIL 获取
