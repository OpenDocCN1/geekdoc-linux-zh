
如前所述，`.fetchmailrc` 文件中可以包含的选项比这里列出的要多得多。然而，这些选项足以让你通过基础配置开始运行。

为了获得额外的灵活性，你可以定义多个 `.fetchmailrc` 文件以便使用同一个 Linux 账户从不同的远程服务器检索邮件。例如，你可以为你最常用的账户定义设置并将其保存在默认的 `.fetchmailrc` 文件中。可以这样快速检索邮件：

```
$ fetchmail -a
```

1 message for bball at mail.myserver.com (1108 octets).

reading message 1 of 1 (1108 octets) . flushed

通过使用 `fetchmail` 的 `-f` 选项，你可以指定一个备资源文件，然后轻松地从另一个服务器检索邮件：

```
$ fetchmail -f .othermailrc
```

2 messages for bball at othermailer.org (5407 octets).

reading message 1 of 2 (3440 octets) ... flushed

reading message 2 of 2 (1967 octets) . flushed

You have new mail in `/var/spool/mail/bball`

通过使用 `-d` 选项配合时间间隔（秒），你可以以进程（daemon）或后台模式使用 Fetchmail。该命令将作为后台进程启动，并在指定的间隔从指定的远程服务器检索邮件。有关更高级的选项，请参阅 Fetchmail 页面，该页面非常著名并详细记录了所有选项。

> 注意
>
> 因为 `.fetchmailrc` 文件包含你的邮件服务器密码，它应该只对你可读。这意味着它属于你，且权限不应大于 600。如果 `.fetchmailrc` 文件的权限大于此，Fetchmail 将报错并拒绝启动。

# 选择邮件投递代理 (MDA)

第一行，当然，只是指定了用于登录邮件服务器的用户名，第二行指定了该用户的密码。许多关注安全的部门对于在配置文件中放置明文密码的想法感到不忍。唯一的保护措施是确保该文件仅对所有者可读；即设置文件权限为 600。

第三行告诉 Fetchmail，它应该从服务器获取所有消息，即使这些消息已经被读取过。

第四行告诉 Fetchmail，在完成消息下载后，它应该从邮件服务器中删除这些消息。这是默认设置，因此我们不需要显式指定此选项。如果你想在下载消息后将消息留在服务器上，请使用 `no flush` 选项。

你刚刚插入的配置选项使得整个 `.fetchmailrc` 文件看起来如下所示：

```
set daemon 600
set postmaster foobar ownset logfile ./fetchmail.log
```

```
poll mail.samenet.org
proto pop3
no dns
```

```
user foobar
pass secretword
fetchall
flush
```

此文件告诉 Fetchmail 执行哪些操作

- 每隔 600 秒检查一次 POP3 服务器 `mail.samenet.org` 是否有新邮件
- 使用用户名 `foobar` 和密码 `secretword` 登录
- 从服务器下载所有消息
- 完成下载后从服务器删除这些消息
- 将收到的任何无法投递给本地用户的邮件发送到账户 `foobar`

# 第 19 章 处理电子邮箱

> 提示：
>
> 你可以使用 X 的图形化工具 `fetchmailconf` 来配置、测试和使用你的 Fetchmail 设置，但红帽不再提供它了，因为它使用了 Tk 工具包集。高级用户可以随时从红帽 7.3 获取 RPM 包，或者从源码编译 Fetchmail。你还需要在系统中安装 Python 解释器和 Tk 工具包。如果你选择安装它，请像如下所示从 X 终端窗口的命令行启动客户端：
>
> ```
> # fetchmailconf &
> ```

如前所述，`.fetchmailrc` 文件中可以包含的选项比这里列出的要多得多。然而，这些选项足以让你通过基础配置开始运行。

为了获得额外的灵活性，你可以定义多个 `.fetchmailrc` 文件以便使用同一个 Linux 账户从不同的远程服务器检索邮件。例如，你可以为你最常用的账户定义设置并将其保存在默认的 `.fetchmailrc` 文件中。可以这样快速检索邮件：

```
$ fetchmail -a
```

1 message for bball at mail.myserver.com (1108 octets).

reading message 1 of 1 (1108 octets) . flushed

通过使用 `fetchmail` 的 `-f` 选项，你可以指定一个备资源文件，然后轻松地从另一个服务器检索邮件：

```
$ fetchmail -f .othermailrc
```

2 messages for bball at othermailer.org (5407 octets).

reading message 1 of 2 (3440 octets) ... flushed

reading message 2 of 2 (1967 octets) . flushed

You have new mail in `/var/spool/mail/bball`

通过使用 `-d` 选项配合时间间隔（秒），你可以以进程（daemon）或后台模式使用 Fetchmail。该命令将作为后台进程启动，并在指定的间隔从指定的远程服务器检索邮件。有关更高级的选项，请参阅 Fetchmail 页面，该页面非常著名并详细记录了所有选项。

> 注意
>
> 因为 `.fetchmailrc` 文件包含你的邮件服务器密码，它应该只对你可读。这意味着它属于你，且权限不应大于 600。如果 `.fetchmailrc` 文件的权限大于此，Fetchmail 将报错并拒绝启动。

针对 Yahoo! 也有一个类似的工具。可以通过 `http://web.mit.edu/ravir/fetchyahoo/index.html` 获取 Fetch。

一旦实现，你就可以使用普通的 MUA（邮件用户界面），例如接下来讨论的，来访问基于 Web 的邮箱。

## 邮件守护进程 (Mail Daemons)

Red Hat 提供了一个名为 `imam` 的包，它可以为你的系统安装 IMAP 和 POP 守护进程（服务器）。这些服务器从远程站点接收邮件。安装完成后（使用 `pm` 命令或通过 Packages 图形界面——参见第 8 章），文档可以在 `/usr/share/doc/imap-201a` 找到，README 文件非常简短；Red Hat 已经完成了配置工作：你只需要启动服务即可（参见第 7 章）。

Biff 及其 KDE Korn 是小型守护进程，用于监控你的邮件文件夹并在有消息送递时通知你。这些程序是默认安装的。通常会在 `.login` 或 `.profile` 文件中写入 `biff`，以便在用户登录时自动启动 Biff。Korn 可以通过将应用程序添加到 KDE 任务栏来启动。

> 注意
>
> 自动回复（Autoresponders）会自动对收到的邮件生成回复；它们通常用于通知收件人不在办公室。Red Hat 不包含此类功能，但你可以在 Freshmail.net 查找并安装自动回复程序。如果你订阅了邮件列表，请注意你的账户自动回复可能会给列表中的其他成员带来干扰。在激活自动回复并离开办公室之前，请先从邮件列表中取消。

## 选择邮件客户端 (MUA)

你使用邮件客户端来读取邮件。Red Hat 提供了几种控制台邮件客户端，包括高度可配置的命令行客户端和易于使用的菜单驱动型客户端。接下来的章节将讨论其中几种，最后将检查 GUI 邮件客户端程序，因为它们是新用户最常选择的 MUA。然而，许多人在尝试后都会发现文本类 MUA 很有用，所以不要亏了自己而忽略了它们。

你选择的图形 MUA 可能与 Microsoft Outlook 或 Outlook Express 邮件客户端相似。这些应用程序在许多用户中被使用。现代 Linux GUI 邮件客户端基于这种熟悉感，提供了 UNIX 环境标志性的增强、功能和可配置性。

## mail 应用程序
