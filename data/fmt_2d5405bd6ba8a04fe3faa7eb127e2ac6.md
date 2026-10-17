
$ mail paul@hudzilla.org

随后 `mail` 会提示你输入邮件主题。光标会向下移动到下一行空行。现在你可以开始输入邮件正文了。完成后，在空行上按 `Ctrl+D` 退出 `mail` 程序并发送消息。（如果你不想向任何人发送抄送，系统可能会提示你输入 `Cc:`）消息会被处理完毕——你的 shell 提示符就会返回。如果想放弃正在写的邮件，请按 `Ctrl+C`。

如果你想使用 `mail` 程序检索邮件，只需在 shell 提示符下输入 `mail`。系统会返回类似下面的内容：

```
Mail Type ? 获取帮助。
```

```
/var/mail/andrew: 1 message 1 unread

>U 1 paul@hudzilla.org    Sun Mar 20 07:15 18/551 "Birthday"

>N 2 spam@ebay.com         Sun Mar 20 08:25 18/542
```

### 第 8 章 接入互联网：浏览网页、编写邮件和阅读新闻

“一条巨大且令人讨厌的垃圾邮件”
> 3 paul@hudzilla.org Sun Mar 20 09:21 17/524 "Ubuntu 4 Update"
> 4 nick@veitch.org Sun Mar 20 09:24 17/528 "Issues"

`mail` 提示方式中的第一列是提示你输入的。

第一列中，`U` 表示该消息未读。`N` 表示该消息是新消息。其他列均自言易懂。

要阅读其中一条消息，只需输入消息编号并按回车。

例如，

```
& 4
Message 4

From nick@veitch.org Sun Mar 20 09:24:35 0023
Date: Sun, 29 Mar 2006 09:24:34 -0500
From: andrew@andbhubson.co.uk
To: nick@veitch.org
Subject: Issues

Hey Nick,

新一期看起来棒极了！你从哪里得到的封面灵感？

Seeya
```

如果你想回复这条消息，可以输入 `respond` 并按回车。你也可以简单地输入 `r` 并按回车。默认情况下，该命令应用于当前激活的消息，在消息列表中由 `a` 标出（并且这将是你阅读的最后一条消息）。如果你想让命令应用于不同的消息，只需在命令后指定消息编号即可。例如，输入 `r 2` 将回复编号为 `2` 的消息。

在 `mail` 中通过在提示符处输入 `?` 可以查看完整的命令列表。注意，你可以将所有命令缩写为不产生歧义的最短缩写。

#### 使用 mail Shell 脚本

如前所述，`mail` 最有用的应用是在 shell 脚本中使用。创建和发送消息的完整指令可以在命令行完成。例如，假设我们有一个生成报告并将其存储为文本文件的 shell 脚本。现在我们想在脚本结束时向用户发送该文件。通过 `mail`，我们可以使用如下命令：

```
$ mail andrew@andbhudson.co.uk -s "Report from shell script" < report.txt
```

`-s` 指定命令行上的主题行，然后我们使用 shell 重定向将 `file.txt` 作为消息正文（第 15 章，“自动化任务”）。这种方法简单、简洁，且发送消息不需要用户交互。
有关 `mail` 命令行可其他选项，请参阅 `man page`（帮助手册）。

#### mutt

`mutt` 是一个相对新的命令行邮件客户端，正迅速受到用户的欢迎。该客户端被称为 `mutt`，是因为它被称为“邮件客户端中的杂杂”，因为它尝试结合 `elm` 和 `pine` 等客户端的最佳功能。`Mutt` 是一个功能极其邮件客户端，尽管它没有 `pine` 那么易用。图 8.14 显示了 `mutt` 界面。

要检查版本并查看编译选项，请如下使用 `mutt -v`：

```
$ mutt -v

Mutt 1.4.2.1i (2004-02-12) Michael R. Elkins and others.

Copyright (C) 1996-2002 Michael R. ABSOLUTELY NO WARRANTY; for details `mutt -vv`.

Mutt 是 free软件，你可以在特定条件下重新分发它；详情见 `mutt -vv`.

System: Linux 2.6.11.177_FC4 (i686) [using ncurses 5.4]

Compile options:

-DOMAIN

-DEBUG

-HEMSPOOL -USE_GETGID -USE_DOTLOCK -LD_STANDALONE

+USE_FCNTL +USE_IMAP -USE_GSS +USE_SSL +USE_SASL

+HAVE_RECOMP +USE_GENU_REGEXP

+HAVE_COLOR +HAVE_START_COLOR +HAVE_TYPEHEAD +HAVE_BKDGSET

+HAVE_CURS_SET +HAVE_META +HAVE_RESIZETERM

+HAVE_PGP -BUFFY_SIZE -EXACT_ADDRESS -SUN_ATTACHMENT

+ENABLE_NBLS -LOCALES_HACK +HAVE_WC_FUNCS +HAVE_LANGINFO_CODESET

?+HAVE_ICONV -ICON_NONTRANTS +HAVE_GETIDS +HAVE_GETADDRINFO

ISPELL="/usr/bin/ispell"

SENDMAIL="/usr/bin/sendmail"

MAILPATH="/var/mail"

PGDATDIR="/usr/share/mutt"

CONFIGDIR="/etc"

EXCSHELL="/bin/sh"

-MIXMASTER
```

*(注：由于提供的文本中存在大量重复段落，译文已根据“不要重复输出原文”的原则进行了去重处理，保留了核心内容的翻译)*

# 第8章 在互联网上：浏览网页、编写电子邮件和阅读新闻

某些新闻阅读器程序允许你根据文章所属的线程（`threads`）来跟踪文章。这有助于简化新闻组中文章的组织。

用于将新闻文章从一个主机传输到另一个主协议是网络新闻传输协议（`NNTP`），定义在 `RFC 977` 中。（你可以在 `ftp://metalab.unc.edu/pub/docs/rfc/` 搜索 `RFC`；请查看 `rfc-index.txt` 文件）。`NNTP` 被设计为一种简单的客户端/服务器协议，允许两个主机以高效的方式交换新闻组文章。

## 选择新闻阅读器

无论你的 Ubuntu 服务器是否已配置为新闻服务器，你都可以使用新闻阅读器程序阅读新闻组文章。新闻阅读器需要连接到新闻服务器。无论新闻服务器是在同一台机器上，还是在世界另一端的远程服务器上都没有关系。

`UNIX` 系统有多种程序可以连接到新闻服务器，并在新闻组中读取和发布文章。以下章节介绍了 Ubuntu 发行版提供的新闻阅读器。

## slnr 新闻客户端

`slnr` 程序是 Ubuntu Core 发行版自带的基于文本的新闻阅读器。它使用 `ncurses` 包在终端屏幕上绘制基于文本的窗口。`slnr` 可用于在配置好的新闻服务器上读取和发布新闻组文章。如果你想在不同平台上使用相同的新闻阅读器，`slnr` 可运行在 Linux、Mac、OS2、Windows 和 VMX 上。它现在提供了真正的离线阅读能力。

`slnr` 程序包含在 `slnr RPM` 包中；你通过使用 `yum` 或 `rpm` 命令进行安装。安装完 `slnr` 后，你需要创建一个本地配置文件。通过设置环境变量：

```
$ export NNTSERVER=news.andbhudson.co.uk
```

当然，你将使用你自己的服务器的域名。

然后，使用以下命令创建你的本地配置文件：

```
$ slnr -f .jnewsrc --create
```

并启动 `slnr`。配置文件位于 `/etc/slnr.rc`，这是一个注释详细的文件，易于修改和自定义。

当 `slnr` 启动时，它会显示新闻服务器上可用的组列表。选择你想要阅读文章的组，然后选择特定的文章。图 8.15 显示了 `slnr` 屏幕示例。

```
news@optima:~~

File Edit View Terminal Press help

slrn 9.0.8. Press '?' for help, to quit.. Server: usenet.plus.net

D 10:[Berry(islam)] Accessing the Internet by E-mail FQ

D 1401:10:[15] Time to talk - Affiliate's Magic Words - PRELAUNCH!! +1/108 (Top)

[169] unreal group:alt.internet.server

newsgroups: internet.services,alt.online-service,alt.bbs,internet.answer

Subject: Accessing the Internet by E-mail FQ
```
