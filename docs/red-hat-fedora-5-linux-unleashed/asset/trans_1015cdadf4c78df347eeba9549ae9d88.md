
要检查版本并查看编译时选项，请使用 `mutt -v`，如下所示：

```
$ mutt -v
Mutt 1.4.2.11 (2004-02-12)
Copyright (C) 1996-2002 Michael R. Elkins and others.
Mutt comes with ABSOLUTELY NO WARRANTY; for details type `mutt -vv' .
Mutt is free software, and you are welcome to redistribute it
under certain conditions; type `mutt -vv' for details.
System: Linux 2.6.11.1177_F04 (1686) (using ncursew 5.4)
Compile options:
 -DOMAIN
 -DEBUG
 -HOMEPOOL -USE_SETGID -USE_DOTLOCK -DL_STANDALONE
 +USE_FCNTL -USE_FLOCK
 +USE_POP +USE_IMAP +USE_GSS +USE_SSL +USE_SASL
 +HAVE_REGCOMP -USE_GNU_REGEX
 +HAVE_COLOR +HAVE_START_COLOR +HAVE_TYPEHEAD +HAVE_BKGDDSET
 +HAVE_CURS_SET +HAVE_META +HAVE_RESIZETERM
 +HAVE_PGP -BUFFY_SIZE -EXACT_ADDRESS -SUN_ATTACHMENT
 +ENABLE_NLS -LOCALES_HACK +HAVE_WC_FUNCS +HAVE_LANGINFO_CODESET
 +HAVE_LANGINFO_YESEXPR
 +HAVE_ICONV -ICONV_NONTRANS +HAVE_GETSID +HAVE_GETADDRINFO
 ISPALL="/usr/bin/ispell"
 SENDMAIL="/usr/sbin/sendmail"
 MAILPATH="/var/mail"
 PKGDATADIR="/usr/share/mutt"
 SYSCONFDIR="/etc"
 EXEOSHELL="/bin/sh"
 -MIXMASTER
```

要联系开发人员，请发送电子邮件至 `<mutt-dev@mutt.org>`。要报告 bug，请使用 flea(1) 工具。

如果您想更改选项（例如任何路径），您需要从源代码重新编译 mutt。

最新的 mutt 版本以及有关它的新闻和信息，可以在 http://www.mutt.org/ 获取。mutt 自豪地被认为是一个没有 bug 的程序，但它的作者认为它可能有一些“跳蚤”——幸运的是，这些很少。

系统范围的配置文件保存在 `/etc/Muttrc`，每个用户可以拥有自己的 `~/.muttrc` 文件。mutt 的配置通常是一个不断演进的过程，因为每个用户都在尝试配置这个功能丰富的邮件客户端。

![](img/2045828cf45e5632bf056f9ca99d6755_261_0.png)

**图 8.14** mutt 结合了 elm 和 pine 的最佳特性（除了丑陋的默认屏幕颜色）。Fedora 默认将编辑器设置为 vi，但你可以选择其他任何编辑器。

在使用 mutt 之前，你需要为每个用户的主目录配置一个 muttrc 文件。示例文件位于 `/usr/share/doc/mutt-*/sample.muttrc`；只需将其（或系统范围的文件）复制到相应主目录中的 muttrc。在那里，编辑它以反映你如何配置邮件系统并设置你的偏好；你会发现 mutt 高度可定制，配置起来有点繁琐，但使用非常简单。

使用 mutt 发送和接收消息非常容易；彩色显示提供了一组常用命令的子集，F1 调出在线帮助文档。

## 其他邮件客户端

Fedora 包含的邮件客户端只是可用的客户端中的少数几种。Sylpheed-claws（未包含）非常受欢迎，因为它在输入时提供拼写检查，并且非常适合用于网络开销和 RAM 使用是重要考虑因素的大型网络环境。你可以通过搜索 http://freshmeat.net/ 找到适合与 Fedora 一起使用的其他邮件客户端和应用程序。

## 网络新闻概述

新闻组的概念彻底改变了网络上人们之间信息交换的方式。Usenet 网络新闻系统创建了一种方法，让人们可以与拥有相似兴趣的大组人进行电子通信。

以下章节描述了 Usenet 网络新闻组格式以及新闻组信息如何在主机之间传输。正如你将看到的，Usenet 新闻的许多概念体现在其他形式的协作通信中。

## 新闻组

Usenet 新闻组充当一种公共公告板系统。任何用户都可以订阅单独的新闻组并向新闻组发送（或*发布*）消息（称为*文章*），以便新闻组的所有其他订阅者可以阅读它们。一些新闻组包括一个管理员，他必须在消息发布前批准每条消息。这些被称为*受管理的*新闻组。其他新闻组是*开放的*，允许任何订阅成员发布消息。当文章发布到新闻组时，它会传输到新闻网络中的所有其他主机。

Usenet 新闻组被划分为一个层次结构，以便更容易找到单独的新闻组。层次级别基于主题，如计算机、科学、娱乐和社会问题。每个新闻组都命名为更高级别主题的一个子集。例如，新闻组 `comp` 与所有计算机主题相关。新闻组 `comp.laptops` 与笔记本电脑问题相关。通常，层次结构有几层深。例如，新闻组 `comp.databases.oracle.server` 与 Oracle 服务器数据库问题相关。

> **注意**
> 新闻组文章的格式遵循 Internet 标准文档请求注释（RFC）1036 中定义的严格指南。每篇文章必须包含两个不同的部分：头行和消息正文。
>
> 头行标识文章发布的来源和时间。消息正文应仅包含标准 ASCII 文本字符。新闻文章中不应发布任何二进制字符或文件。为了绕过此限制，二进制文件通过标准 UNIX uuencode 程序或较新的多用途 Internet 邮件扩展（MIME）协议转换为文本数据。然后，生成的文本文件发布到新闻组。新闻组阅读器随后可以将发布的文本文件解码回其原始二进制形式。

针对共同主题发布的文章集合被称为*线程*。当用户根据其他已发布的消息发布消息时，线程可以包含许多文章。一些新闻阅读器程序允许用户根据所属线程跟踪文章。这有助于简化新闻组中文章的组织。

> **提示**
> 免费新闻服务器 `news.gmane.org` 通过新闻组提供 Red Hat 和 Fedora 邮件列表。测试列表可用为 `gmane.linux.redhat.rhl.beta`。这是一种阅读线程讨论的便捷方式，比使用 Fedora 邮件列表存档更容易。

用于将新闻组文章从一个主机传输到另一个主机的协议是网络新闻传输协议（NNTP），在 RFC 977 中定义。（你可以在 `ftp://metalab.unc.edu/pub/docs/rfc/` 搜索 RFC；查看文件 `rfc-index.txt`。）NNTP 被设计为一种简单的客户端/服务器协议，使两个主机能够高效地交换新闻组文章。

### 选择新闻阅读器

无论你的 Fedora 服务器是否设置为新闻服务器，你都可以使用新闻阅读器程序阅读新闻组文章。新闻阅读器程序只需要连接到新闻服务器。新闻服务器是在同一台机器上还是世界另一端的远程新闻服务器并不重要。

有几种程序可用于 UNIX 系统连接到新闻服务器以阅读和发布新闻组中的文章。以下章节描述了随 Fedora 发行版提供的新闻阅读器。

#### slrn 新闻客户端

`slrn` 程序是一个基于文本的新闻阅读器程序，包含在 Fedora Core 发行版中。它使用 ncurses 包在终端屏幕上绘制基于文本的窗口。`slrn` 可用于阅读和发布到已配置新闻服务器上新闻组的文章。如果你想在不同的平台上使用相同的新闻阅读器，`slrn` 运行在 Linux、Mac、OS2、BeOS、Windows 和 VMS 上。它现在提供了真正的离线阅读功能。

`slrn` 程序包含在 `slrn` RPM 软件包中。你可以使用 `yum` 或 `rpm` 命令安装它。安装 `slrn` 后，你需要创建一个本地配置文件。首先设置一个环境变量：

```
$ export NNTPSERVER=news.andhudson.co.uk
```

当然，你将使用自己的新闻服务器的域名。

然后使用以下内容创建你的本地配置文件

```
$ slrn -f .jnewsrc -- create
```

并启动 `slrn`。位于 `/etc/slrn.rc` 的配置文件是一个注释良好、易于修改和自定义的文件。

当 `slrn` 启动时，它显示新闻服务器上可用组的列表。你选择要阅读文章的组，然后选择单个文章。图 8.15 显示了一个 `slrn` 屏幕示例。

#### Pan 新闻客户端

Pan 是一个图形新闻阅读器客户端，适用于 GNOME，并且是 Fedora 的默认新闻阅读器。如果你安装了 GNOME 库（通常默认安装），你也可以在 K 桌面环境（KDE）中使用 Pan。Pan 具有下载和显示所有命令 pan & 的功能。Pan 支持组合多部分消息和 yenc 编码/解码协议。图 8.16 显示了一个示例 Pan 显示。与 `slrn` 程序不同，Pan 不需要系统范围默认或用户定义的 NNTPSERVER 环境变量来定义新闻服务器地址，但你确实需要配置 Pan。

