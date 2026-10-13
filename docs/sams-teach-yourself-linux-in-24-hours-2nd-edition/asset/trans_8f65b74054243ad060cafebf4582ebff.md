
## 您需要从 ISP 获取的信息

为了通过您的 ISP 使用 PPP 连接到 Internet，您首先，显然，需要一个 PPP 账号。注册服务时，您的 ISP 账号代表很可能假设您想要适用于 Windows 或 Macintosh 计算机系统的设置和软件。如果您说“都不是。我使用的是 Caldera 的 OpenLinux”，而得到的回应是空白的凝视、电话里死一般的寂静，或是“什么是 Linux？”，不要惊慌！

您可能会很幸运。Linux 的普及度正在增长，美国和世界各地的许多 ISP 都认可并支持 Linux 用户。如果您的 ISP 知道 Linux，请询问最低系统要求、任何设置指南或安装提示。本书的 CD-ROM 包含您所需软件的最新稳定版本，所以无论如何您也不必担心。

假设您的 ISP 不了解 Linux，以下是您需要从 ISP 获取的信息：

- 您的账号信息，即用户名（登录名）和密码，以便您可以登录到 ISP 的计算机。
- 您的 ISP 的调制解调器连接号码，以便您可以拨号并连接。
- 您的 ISP 是为您分配静态 Internet 协议（IP）地址还是动态分配 IP 地址（本小时的示例假设使用动态地址，但我会说明在哪里可以为静态 IP 地址进行更改）。
- 您的 ISP 的主域名服务器和辅助域名服务器的 IP 地址和名称。此信息将写入 /etc/resolv.conf 文件（第一示例中已在“编辑 resolv.conf 文件”一节中说明）。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_249_0.png)

DNS IP 地址的形式为四个 8 位数字，看起来像 205.198.114.1 或 205.198.114.20。这些是 ISP 使用或维护的服务器的地址，用于将主机名（如 metalab.unc.edu）翻译成数字 IP 地址，以便您可以连接、查询或寻址世界各地的其他计算机和用户。本节不涉及 IP 地址机制的细节，本书也不涵盖 Linux 下网络的所有方面。如果您想要更完整的细节，请参阅 /usr/doc/LDP/nag 目录下的 Linux Network Administrators Guide。

- 您的 ISP 邮件服务器的名称或 IP 地址，以便您可以发送和接收邮件（您可能还需要 ISP 邮件服务器的单独用户名和密码）。您需要在第 11 小时“配置 Internet 电子邮件”中使用此信息。
- 您的 ISP 新闻服务器的名称或 IP 地址，以便您可以阅读 Usenet 新闻并订阅新闻组。您需要在第 12 小时“配置 Internet 新闻”中使用此信息。

最后，请询问 ISP 的万维网主页以及您的主页的统一资源定位符（URL），如果 ISP 提供此服务。ISP 的网页可能提供技术公告、帮助文件或其他有助于故障排除连接的信息。

## 手动设置 PPP 连接

掌握这些信息后，您现在可以学习如何指定 ISP 的 DNS 服务器以及如何创建或编辑连接脚本 ppp-on。虽然指定 ISP 的 DNS 服务器（们）对于启动或维护连接并非必要，但您稍后在使用 kppp 和 xisp 客户端以及学习 Internet 电子邮件和新闻时需要这些信息。

### 编辑 resolv.conf 文件

这是一个简单的过程。首先，确保您以 root 操作员身份登录。然后在 /etc 目录中查找名为 resolv.conf 的文件。如果存在，请使用您喜欢的文本编辑器（如 pico（参见第 14 小时“文本处理”））打开它，并添加 search 关键字，后跟 ISP 的域名，以及 ISP 的 DNS 服务器的 IP 地址。如果 ISP 只有一个，那也没问题。如果 ISP 有多个，也没问题。像这样创建并打开文件：

```
# pico /etc/resolv.conf
```

输入以下格式的行：

```
search erols.com
nameserver 205.198.114.1
nameserver 205.198.114.20
```

关闭文件。就这么简单！接下来，您创建或编辑一个可用于启动 PPP 连接的脚本。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_250_0.png)

## 编辑 PPP 连接脚本

开始之前，您应该知道使用此脚本只是启动 PPP 连接的一种方式。这种方法要求您以 root 操作员身份登录。本章后面您还将学习一种更简单的方法。

我不详细介绍方法，因为我想尽快让您上线。当您获得一个可用的连接后，我建议您查看 pppd 手册页、/usr/doc/HOWTO 目录下的 Robert Hart 的 PPP-HOWTO、/usr/doc/FAQ/PPP-HOWTO 目录下的 Al Longyear 的 PPP-FAQ、ISP-Connectivity mini HOWTO，或 /usr/doc/LDP/nag 目录下 Linux Network Administrators Guide 中的相关章节。

首先要做的是确保您以 root 操作员身份登录。然后，在 /etc/ppp 目录中查找名为 ppp-on 的文件。如果存在，首先制作一个副本（您可以随意命名），或将 ppp-on 重命名为 ppp-on.org。如果没有 ppp-on，请从 /usr/doc/ppp-2.2b 目录复制它。清单 10.1 显示了由 Al Longyear 编写的脚本的部分内容：

### 清单 10.1 ppp-on 连接脚本

```
...
TELEPHONE=555-1212  # The telephone number for the connection
ACCOUNT=username  # The account name for logon (as in 'George Burns')
PASSWORD=password  # The password for this account (and 'Gracie Allen')
LOCAL_IP=0.0.0.0  # Local IP address if known. Dynamic = 0.0.0.0
REMOTE_IP=0.0.0.0  # Remote IP address if desired. Normally 0.0.0.0
...
DIALER_SCRIPT=/etc/ppp/ppp-on-dialer
exec /usr/sbin/pppd lock modem crtscts /dev/modem 57600 \
asyncmap 20A0000 escape FF $LOCAL_IP:$REMOTE_IP \
noipdefault netmask $NETMASK defaultroute connect \
$DIALER_SCRIPT &
```

您需要更改此脚本的几个部分。大多数情况下，您只需要进行少量更改。一些关键元素如下：

- TELEPHONE—在此输入您的 ISP 的调制解调器连接号码。
- ACCOUNT—输入您的用户名或登录名（通常由 ISP 分配）。
- PASSWORD—在此输入您的密码（通常由 ISP 分配）。

DIALER_SCRIPT—输入拨号脚本的完整路径名，该脚本使用 pppd 守护进程的配套 chat 程序。chat 程序会为您进行拨号、连接和登录。如果找不到此脚本的副本，该脚本名为 ppp-on-dialer，请在 /usr/doc/ppp-2.2.0f 目录下查找。（清单 10.2 显示了 ppp-on-dialer 脚本。）

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_252_0.png)

> 如果您的 ISP 计算机未显示 login: 和 password: 提示，您必须在此脚本中将 login: 和 password: 字符串更改为与 ISP 相同的字符串。

### 清单 10.2 ppp-on-dialer 拨号脚本

```
...
exec /usr/sbin/chat -v
TIMEOUT 3
ABORT '\nBUSY\r'
ABORT '\nNO ANSWER\r'
ABORT '\nRINGING\r\n\r\n\r\nRINGING\r'
''
'OK-+++\c-OK' ATH0
TIMEOUT 30
OK ATDT$TELEPHONE
CONNECT ''
login: -login: $ACCOUNT
password: $PASSWORD
```

接下来，检查 ppp-on 脚本中的 pppd 命令行，并将 /dev/modem 更改为与调制解调器连接的设备相匹配。如果您愿意，可以使用第 9 小时《使用通信程序》中概述的方法，从调制解调器的串行端口创建到 /dev/modem 的符号链接。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_252_1.png)

> 如果您使用的是 14.4 调制解调器，请使用 19200 作为数值；如果您使用的是 28.8 或 33.6 调制解调器，请尝试 57600。如果您使用的是 56K 或 V.90 调制解调器，请尝试使用 115200 的值。您可能能够以更快的速度连接，尤其是在较新的调制解调器上。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_252_2.png)

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_253_0.png)

> 如果您的 ISP 自动分配 IP 地址（动态 IP 地址，或每次登录时可能不同的地址），您就准备就绪了。但如果您必须连接到特定的（静态或固定）IP 地址，您需要从清单 10.1 中的 pppd 命令行中删除 noipdefault 选项。您还需要将 $REMOTE_IP 字符串更改为 ISP 提供的 IP 地址（您可以在 pppd 命令行中或脚本中 $REMOTE_IP 变量的上方进行此操作）。

最后，确保 ppp-on 和 ppp-on-dialer 脚本都可执行，可以通过 ls -l 检查或使用 chmod 程序修改：

```
# chmod +x /etc/ppp/ppp-on*
```

现在您已准备就绪，假设您的调制解调器已连接到计算机，并且电话线已连接到调制解调器，您可以尝试连接。

## 手动启动和停止 PPP 连接

本节向您展示如何连接到 ISP 并启动 Internet 会话。有几种方法可以做到这一点。您首先看到的是最基本的方法，即不使用刚刚创建的脚本，使用 minicom 程序连接。然后，您将学习如何使用 PPP 连接脚本 ppp-on。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_253_1.png)

> minicom 程序在第 9 小时中讨论过，它是一个通信程序，您可以使用它拨号并连接到其他计算机或信息服务，例如公告板系统（BBS）。请参阅 minicom 手册页获取更多信息。

### 使用 minicom 连接

使用 minicom 连接到 ISP 的优点在于，您的账号信息和密码不会记录在 /var/log 目录下的系统日志中。您每次想要使用 Internet 时都可以使用 minicom，但您可能会觉得这个过程很繁琐。我首先展示这种方法，因为您可能会发现它有助于验证您在 ppp-on-dialer 脚本中指定的登录名和密码条目是否有效。

