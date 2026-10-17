
```text
# maximum message size
O MaxMessageSize=2500000

# This sets the maximum size at 2.5 megabytes.  The default is set
at one megabyte.

# No email over 2.5 megabytes in size   will be allowed to pass.
# privacy flags
O PrivacyOptions=goneaway
# This adjusts the types of connections users from outside might run
into.

# default UID (can be username or userid:groupid)
O DefaultUser=1:1

# If you want to run sendmail as root, the above settings will work.
# Remember that UID and GID 1 are both reserved for root.
# Here you can place an alternate user to run sendmail.
# maximum number of recipients per SMTP envelope
O MaxRecipientsPerMessage=100
# This option prevents a user from sending out emails to more than
100 people using the single email they wrote.
# This prevents those sending out spam and junk emails.
```

一旦您对 `sendmail.cf` 文件进行了任何更改，您的 `sendmail` 守护进程必须重新读取配置。为了确保这种情况发生，您可以向守护进程发送 `-HUP` 或 `kill -1` 信号，或者在 `rc.d` 文件中重启守护进程。若要使用前一种方法，首先确定 `sendmail` 进程的 PID：

```
# ps aux | grep sendmail | grep root
```

添加的 `grep root` 命令隔离了初始 `sendmail` 进程，使其与任何 fork 出的子进程分离。一旦获得 PID，请输入以下命令：

```
# kill -HUP <PID>
```

或者，如果您使用的是 `sendmail` RPM，只需重启该进程：

```
# /etc/rc.d/init.d/sendmail restart
```

务必使用 Telnet 访问 25 端口或检查 `sendmail` 守护进程的状态来验证 `sendmail` 是否仍在运行：

```
# /etc/rc.d/init.d/sendmail status
```

这些只是 `sendmail.cf` 文件下的少数可用选项。请自行测试这些变量，找出最适合您的那些。

## 保护邮件服务器

入侵 Linux 服务器的两种最快方法是对旧版 `sendmail` 程序进行漏洞利用，或利用 Linux 盒子上的旧版 BIND 程序。`sendmail` 程序有一系列存在可被利用的安全问题历史；然而，如果您保持使用最新的 `sendmail` 版本，就可以避免许多标准问题或安全担忧。如果您没有将 Linux 盒子用作邮件服务器，请务必彻底关闭 SMTP 进程。保持任何类型的进程或端口开放都是对入侵尝试的邀请。

本节介绍了如果您将在服务器上运行 `sendmail`，保护邮件服务器进程的一些其他方法。

### 防止通过您的邮件服务器中继

设置安全邮件服务器面临的最大障碍之一是中继问题。中继是指来自内部或外部的某人系统使用你的邮件系统将他们的电子邮件转发到另一个外部主机。你的机器充当两点之间的中继。向中继开放的 Linux 机器容易受到不良垃圾邮件发送者的滥用。垃圾邮件是由疏忽或天真的系统管理员分发的未经请求的垃圾邮件。垃圾邮件发送者会寻找使用较旧 `sendmail` 发行版且存在已知问题或安全漏洞的机器。在你甚至意识到你的机器已被用于垃圾邮件目的之前，可能已经有成千上万封电子邮件通过了。然后你就得面对来自众多收到该邮件的人的投诉这一混乱局面。

幸运的是，最新版本的 `sendmail` 默认拒绝中继。这堵住了一些旧版本中的一个重大安全漏洞。除非你希望他人通过你的邮件服务器进行中继（这是极不建议的），否则 `sendmail` 通常会将其配置为必须开放特定域或 IP 地址以允许中继。

### 改进访问文件

与之前版本的 `sendmail` 相比，一个显著的改进是引入了访问文件，通常位于 `/etc/mail` 目录中。在这里，你可以放置你希望允许通过你进行中继的机器域或 IP 地址。你还可以在此文件中列出臭名昭著的垃圾邮件发送者的已知域，并拒绝他们访问你的机器。访问数据库使邮件管理员能够按个别域来允许访问邮件服务器。

正如主网站 `www.sendmail.org` 页面上所述，每个数据库条目由作为键的域名或 IP 地址以及作为值的动作组成。键可以是完全限定或部分限定的主机或域名，例如 `host.subdomain.domain.com`、`subdomain.domain.com` 或 `domain.com`。后两种形式匹配指定域下的任何主机或子域。如果你的 `generic.mf` 文件中设置了值 `FEATURE(relay_hosts_only)`，则只有第一种形式有效。

键也可以是网络地址或子网，例如 `205.199.2.250`、`205.199.2.0` 或 `205.199.2.`。后两种形式匹配指示子网中的任何主机。请注意，对于针对范围而非仅针对单个 IP 地址的 IP 地址，你必须在域地址末尾添加一个点。这会阻止或授予所有拥有该整个类别内地址的用户的访问权限。

最后，键也可以是 `user@host.domain`，以拒绝来自特定用户的邮件。最后一项对于尝试阻止特定用户分发不受欢迎内容的情况尤其关键。

值可以是以下任意一种：

- `REJECT`，拒绝来自主机的发送请求
- `DISCARD`，接受消息但静默丢弃它（发件人会认为它已被接受）
- `OK`，允许访问并覆盖其他内置检查
- `RELAY`，允许访问，包括允许 SMTP 通过你的机器进行中继
- 任意消息，如“Spammers go away”，以专门拒绝邮件并向有过失方发送简短消息

尝试使用属于最后一个类别的任何域进行连接的人将会看到该消息，并应该明白其中的暗示。

表 17.2 列出了一个良好的访问文件可能包含的键和值。

#### 表 17.2 你希望允许访问或拒绝为你邮件服务器提供服务的用户域和 IP 地址示例列表

| 键 | 值 |
|:---|:---|
| cyberpromo.com | REJECT |
| badpoorsite.com | REJECT |
| friend@noname.org | DISCARD |
| nobody@mydomain.com | DISCARD |
| astronomy.org | RELAY |
| 206.71.77. | RELAY |
| spam@buyme.com | 550 Spammers go away! |
| adsgalore.com | Spamming not tolerated here |

前两项条目拒绝了来自 `cyberpromo.com` 和 `badpoorsite.com` 域中任何主机的所有邮件。互联网上可以下载已知垃圾邮件域列表并将其纳入访问文件。明智的做法是查看一下，并将那些更具滥用性质的域名输入到你的访问文件中。第三行和第四行对发件人来说似乎已被接收，但实际上他们的邮件已被静默丢弃。除非你希望追踪任何有过失的方，否则使用 `DISCARD` 设置没有什么理由。第五行和第六行允许在 `astronomy.org` 域中或从位于 `206.71.77.` 的任何 IP 地址的任何主机进行进或出的中继。最后两行向任何试图通过邮件服务器进行中转或试图向特定本地用户发送邮件的方发送个性化消息。

### 运行 makemap 命令

在根据你的规范自定义访问文件后，你需要使用 `hash` 命令重新制作或刷新数据库。如果你的访问数据库位于 `/etc/mail`（这是大多数 Red Hat 安装的标准配置），你应该运行以下命令：

```
makemap -r hash /etc/mail/access.db < /etc/mail/access
```

此命令自动使用新条目重做数据库，并允许 `sendmail` 适应这些变化。请务必向 `sendmail` 进程发送挂断或 `-HUP` 信号，以便程序重新读取任何更改过的配置文件。如果修改访问文件后你发现仍在收到来自被拒绝域的邮件，请使用 `makemap` 验证你是否已重新处理了你的访问文件。

### 验证你的配置

要查看你的中继是否开放，请尝试以下简单测试。关于 `sendmail`，需要记住的一点是，它会查看你登录来源主机的 IP 地址。如果你打算测试你的系统，请从完全在你的系统之外的域或 IP 地址尝试。
