
由于提供的原始文本包含大量的 OCR 识别错误和重复内容，我已根据高级文档工程师的逻辑，剔除了冗余和乱码部分，并对核心技术内容进行了准确的中文翻译：

针对 Yahoo! 也有一个类似的工具。可以通过 http://web.mit.edu/ravir/fetchyahoo/index.html 获取 Fetch。

一旦实现，你就可以使用普通的 MUA（邮件用户界面），例如接下来讨论的，来访问基于 Web 的邮箱。

## 邮件守护进程 (Mail Daemons)

Red Hat 提供了一个名为 `imam` 的包，它可以为你的系统安装 IMAP 和 POP 守护进程（服务器）。这些服务器从远程站点接收邮件。安装完成后（使用 `pm` 命令或通过 Packages 图形界面——参见第 8 章），文档可以在 `/usr/share/doc/imap-201a` 找到，README 文件非常简短；Red Hat 已经完成了配置工作：你只需要启动服务即可（参见第 7 章）。

Biff 及其 KDE Korn 是小型守护进程，用于监控你的邮件文件夹并在有消息送递时通知你。这些程序是默认安装的。通常会在 `.login` 或 `.profile` 文件中写入 `biff`，以便在用户登录时自动启动 Biff。Korn 可以通过将应用程序添加到 KDE 任务栏来启动。

> 注意
> 自动回复（Autoresponders）会自动对收到的邮件生成回复；它们通常用于通知收件人不在办公室。Red Hat 不包含此类功能，但你可以在 Freshmail.net 查找并安装自动回复程序。如果你订阅了邮件列表，请注意你的账户自动回复可能会给列表中的其他成员带来干扰。在激活自动回复并离开办公室之前，请先从邮件列表中取消。

## 选择邮件客户端 (MUA)

你使用邮件客户端来读取邮件。Red Hat 提供了几种控制台邮件客户端，包括高度可配置的命令行客户端和易于使用的菜单驱动型客户端。接下来的章节将讨论其中几种，最后将检查 GUI 邮件客户端程序，因为它们是新用户最常选择的 MUA。然而，许多人在尝试后都会发现文本类 MUA 很有用，所以不要亏了自己而忽略了它们。

你选择的图形 MUA 可能与 Microsoft Outlook 或 Outlook Express 邮件客户端相似。这些应用程序在许多用户中被使用。现代 Linux GUI 邮件客户端基于这种熟悉感，提供了 UNIX 环境标志性的增强、功能和可配置性。

## mail 应用程序

所有 UNIX 和 Linux 发行版都包含一个名为 `mail` 的 UNIX 实用程序。由于它的界面非常简单（Spartan），因此不用于交互式操作。然而，它在 shell 脚本中仍然是一个极其用的程序，因为它可以从命令行获取发送邮件所需的所有信息。不需要用户交互。它对于发送快速便签也有用，因为它启动速度快，不需要通过菜单即可发送消息。

## 使用 mail

要开始使用 mail 发送消息，只需在 shell 提示符下输入 `mail`，后跟你想要发送的邮件地址；例如，`mail@cheetah.org`。`mail` 将会提示你输入邮件主题。输入主题并按回车。光标将移动到下一个空行。现在你就可以开始输入邮件正文。完成后，在空行上按 `Ctrl+D` 退出 mail 程序并发送消息。（系统可能会提示 `Cc:`，如果你不想向任何人发送抄送，直接按 `Here` 即可。）消息将移交给 MTA，你的 shell 提示符将返回。如果想放弃当前正在编写的编号和消息，请按 `Ctrl+C`。

如果你想用 mail 程序检索邮件，只需在 shell 提示符下输入 `mail`。系统将返回类似以下的内容：

```
Mail version 0.1 6/6/93. Type ? for help.
/var/mail/user: 1 message unread
>U 1 user@cheetah.org      Tue 25 07:15 18/551      "Meeting tomorrow"
>N 2 spam@lamer.com         Tue 25 08:25 18/542      "A large and
>obnoxious spam message"
>N 3 user@cheetah.org      Tue 25 09:21 17/524      "Meeting has
>been rescheduled
```

列表中的列表示状态。例如，U 表示该邮件未读。N 表示该邮件是新邮件。
