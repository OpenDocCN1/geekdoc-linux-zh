
或者，：

现在，你可能认为 Sendmail 听起来像一个全能的邮件系统——并非如此。最后那小部分，即 Martin 如何从他的本地邮件服务器接收消息，并不使用 SMTP，因此完全不涉及 Sendmail！互联网世界的大部分，邮件旅程的这一段通常使用以下三种协议之一：

- POP2（邮局协议第 2 版）
- POP3（邮局协议第 3 版）
- IMAP4（互联网消息应用协议第 4 版）

而且这些并不是唯一的可能性。如果 Martin 的公司使用 Exchange 作为他的邮件服务器（从邮件服务器的名字来看这很有可能），那么 Outlook 客户端将使用一种名为消息应用程序编程接口（MAPI）的微软协议与 Exchange 服务器通信。然而，Exchange 也可以允许你通过 POP3 访问邮件，因此如果你在服务器上使用 Exchange，就不需要在桌面上使用 Outlook 了。

这对你意味着什么？意味着为了运行一个功能完整的邮件服务器，你不仅需要 SMTP 软件——即 Sendmail——还需要 POP3 软件。

# 验证 Sendmail 安装

由于 Sendmail 对所有 Linux 服务器来说都是非常基础的，它几乎总是标准安装的一部分。你可能会发现它目前正在你的系统上运行。尝试使用 `ps` 来查看它是否存在：

```
# ps aux | grep sendmail
root 504 0.0 0.2 316 32 ? S Jun28 0:01 sendmail
#
```

如果它还没有运行，你可以在以 root 身份登录时使用命令验证它是否存在于你的系统中：

```
# which sendmail
/usr/sbin/sendmail
```

你应该会发现它位于 `/usr/sbin`。如果你的系统没有安装 Sendmail，那么你可以（如果你的系统使用 RPM）尝试：

```
# rpm -q sendmail
sendmail-8.11.16-15
```

如果由于某种原因它没有安装，我猜你必须安装它了。

# 安装 Sendmail

到此时，你可能已经熟悉这个安装程序了。在基于 RPM 的系统上，你需要找到 `rpm` 文件（来自安装介质或互联网），然后执行命令：

```
rpm -ivh sendmail-8.11.16-15.i386.rpm
```

# 验证 POP3 是否安装

我们可以使用 IMAP4、POP2 或 POP3 作为传输协议，但让我们设置 POP3 吧。我见过的 Linux 上实现 POP3 的程序名为 `ipop3d`，执行以下操作查看它是否已安装：

```
which ipop3d
```

你可能会在 `/usr/sbin` 中找到它。如果没有，你必须通过此命令使用 Red Hat 光盘中的 RPM 来安装它：

```
rpm -ivh/misc/cdrom/RedHat/RPMS/imap*
```

该 RPM 将自动安装 `xinetd` 必需的碎片。Red Hat 7.3 默认禁用 `ipop3d`，因此你需要修改文件 `/etc/xinetd/ipop3`，并将显示 `disable=yes` 的行改为 `disable=no`。然后重启 `xinetd` 以注册你的更改：

```
/etc/rc.d/init.d/xinetd restart
```

# 启动和停止 Sendmail

无论你是否需要安装 Sendmail，你都可以像大多数其他服务器服务一样，通过运行位于 `/etc/rc.d/init.d`（大多数发行版）中的初始化脚本来控制它。如果你想手动执行命令启动 Sendmail，可以这样做：

```
# /etc/rc.d/init.d/sendmail start
启动 Sendmail... [
# /etc/rc.d/init.d/sendmail stop
停止 Sendmail... [
# /etc/rc.d/init.d/sendmail restart
重启 Sendmail... [
```

# Linux 作为邮件服务器：Sendmail 349

但首先，让我们聊聊 Sendmail 是什么以及不是什么。在邮件世界中，Sendmail 是一个邮件传输代理（MTA）。它完全通过简单邮件传输协议（SMTP）工作，将邮件传递给本地和远程用户。用英语表达的意思是：假设你想给你的朋友 `martin@thoseguys.com` 发送一封邮件。你坐在一台运行 Outlook 的 Windows 机器上，为 `martin@thoseguys.com` 编写了这封邮件。Outlook 知道（因为你告诉过它你已经配置好了）要与运行 Sendmail 的 Linux 机器通信以发送该消息。从你桌面的 Outlook 到 Linux 服务器的通信使用 SMTP 协议；Sendmail 已准备就绪，并且能够接受如 Outlook、Netscape Messenger 或 Eudora 等邮件客户端程序的此类通信。然后，Sendmail 通过询问 DNS 查询 `thoseguys.com` 域的 MX 记录来找到 `thoseguys.com` 域的邮件服务器。`thoseguys.com` 的 DNS 服务器可能会响应说 `thoseguys.com` 确实有一个 MX 记录，记录指示将邮件发送到名为 `exchange01.thoseguys.com` 的机器。

> 注意：如果你不清楚邮件如何使用 DNS 和 MX 记录查找邮件服务器，请参阅《Mastering Windows Server 4》第 14 章或《Mastering Windows 2000 Server》第 6 和 7 章。

Sendmail 再次使用 SMTP 协议将你的电子邮件传输到 `exchange01.thoseguys.com`。消息现在位于 Martin 的本地邮件服务器上，等待他启动邮件客户端（Outlook、Messenger、Eudora 或任何程序）并从 `exchange01.thoseguys.com` 获取消息。它的大部分旅程已经结束了。

# Sendmail 不做的事情

现在，你可能认为 Sendmail 听起来像一个全能的邮件系统——并非如此。最后那小部分，即 Martin 如何从他的本地邮件服务器接收消息，并不使用 SMTP，因此完全不涉及 Sendmail！互联网世界的大部分，邮件旅程的这一段通常使用以下三种协议之一：

- POP2（邮局协议第 2 版）
- POP3（邮局协议第 3 版）
- IMAP4（互联网消息应用协议第 4 版）

而且这些并不是唯一的可能性。如果 Martin 的公司使用 Exchange 作为他的邮件服务器（从邮件服务器的名字来看这很有可能），那么 Outlook 客户端将使用一种名为消息应用程序编程接口（MAPI）的微软协议与 Exchange 服务器通信。然而，Exchange 也可以允许你通过 POP3 访问邮件，因此如果你在服务器上使用 Exchange，就不需要在桌面上使用 Outlook 了。

这对你意味着什么？意味着为了运行一个功能完整的邮件服务器，你不仅需要 SMTP 软件——即 Sendmail——还需要 POP3 软件。

# 验证 Sendmail 安装

由于 Sendmail 对所有 Linux 服务器来说都是非常基础的，它几乎总是标准安装的一部分。你可能会发现它目前正在你的系统上运行。尝试使用 `ps` 来查看它是否存在：

```
# ps aux | grep sendmail
root 504 0.0 0.2 316 32 ? S Jun28 0:01 sendmail
#
```

如果它还没有运行，你可以在以 root 身份登录时使用命令验证它是否存在于你的系统中：

```
# which sendmail
/usr/sbin/sendmail
```

你应该会发现它位于 `/usr/sbin`。如果你的系统没有安装 Sendmail，那么你可以（如果你的系统使用 RPM）尝试：

```
# rpm -q sendmail
sendmail-8.11.16-15
```

如果由于某种原因它没有安装，我猜你必须安装它了。

# 安装 Sendmail

到此时，你可能已经熟悉这个安装程序了。在基于 RPM 的系统上，你需要找到 `rpm` 文件（来自安装介质或互联网），然后执行命令：

```
rpm -ivh sendmail-8.11.16-15.i386.rpm
```

# 验证 POP3 是否安装

我们可以使用 IMAP4、POP2 或 POP3 作为传输协议，但让我们设置 POP3 吧。我见过的 Linux 上实现 POP3 的程序名为 `ipop3d`，执行以下操作查看它是否已安装：

```
which ipop3d
```

你可能会在 `/usr/sbin` 中找到它。如果没有，你必须通过此命令使用 Red Hat 光盘中的 RPM 来安装它：

```
rpm -ivh/misc/cdrom/RedHat/RPMS/imap*
```
