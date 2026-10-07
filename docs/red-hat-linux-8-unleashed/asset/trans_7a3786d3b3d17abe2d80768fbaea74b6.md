
如果你收到一个 uencoded 文件，而你的电子邮件程序无法识别它，起初你会看到看起来是几百行甚至上千行的垃圾信息。然而，该文本块将以一个特殊行开头。以下是一个 uencoded 文件前几行的可能示例：

```
begin 64 lion_in_tree.jpg
M_C_X`$0$(D29)$$0'2'(($#[1I&4&A0&[S]:)P(#,N,$X0DE-`T'
M!H`'$!"2'$$0!(`01.))30/S------------------------------------------------$X0DE-_
M!H`'$#A*2DGT$$`0*!8`$(X0DE-_4$se
M+V9F'$;$F&8'$+$V9F$H9F:8'$,0$60'
```

文本块的第一行给出了文件解码后应拥有的权限（644）以及解码时应创建的文件名称。你如何解码这个文件？只需将邮件消息保存为文本文件（例如 `lion_in_tree.txt`）。接下来，使用 `uencode` 程序对其进行解码：

```
$ uucode lion_in_tree.txt
```

这将创建一个新文件，在这种情况下它被称为 `lion_in_tree.jpg`。
如果你有一个想要编码的二进制文件以便通过电子邮件发送给他人，可以使用 `uencode` 程序来实现。`uencode` 使用以下语法：

```
uencode local_file remote_file
```

`local_file` 是存储在你本地硬盘上的二进制文件名称。`remote_file` 是你或他人以后使用 `uencode` 处理它时想要解码的名称。通常情况下，你可能想对 `local_file` 和 `remote_file` 使用相同的名称。

默认情况下，输出将发送到 STDOUT（通常是屏幕）。但这并没有太大用，所以通常你会在使用 `uencode` 命令时配合重定向。这里是一个示例：

```
$ uencode lion_in_tree.jpg lion_in_tree.jpg > lion_in_tree.txt
```

此命令将文件 `lion_in_tree.jpg` 编码为一个纯文本文件，你可以用相同名称（`lion_in_tree.jpg`）对其解码，并将编码后的文件存储在 `lion_in_tree.txt` 中。该文本适用于电子邮件发送。

当然，你也可以使用管道（pipes）将 `uencode` 的输出传递给另一个应用程序。例如，你可以将结果传给标准邮件程序，并直接发送给另一个用户。例如：

```
$ uencode lion_in_tree.jpg lion_in_tree.jpg | mail -s "Lion photograph" user@example.org
```

# 注意

编码二进制数据的一个副作用是，由于行始终是固定长度，如果数据无法填满，则需要将每行填充到特定的字符数。通常这些额外的字符是随机的，并且在解码时总是被忽略，但你可以故意放置信息而不是随机的 ASCII 文本。在其他数据文件的“空”中放置信息被称为隐写术（steganography）。现在有程序可以用这种方式编码和解码信息（通常在图片中），还可以扫描图像中隐藏的隐写信息。访问 http://freshheat.net/steg/ 获取感兴趣的应用列表。隐写术不仅限于 `uencode`。

# 相关 Red Hat 和 Linux 命令

你将使用以下命令在 Red Hat Linux 中管理电子邮件：

- balsa—一个用于 X 的 GNOME 邮件代理
- biff—一个基于控制台的邮件通知实用程序
- evolution—一个功能强大的 X Xian GNOME 邮件 PIM
- fetchmail—一个用于 Linux 的控制台和守护模式邮件检索命令
- fetchmailconf—一个用于 X 的图形 fetchmail 配置客户端
- kmail—用于 KDE 和 X 的图形邮件用户客户端
- korn—一个用于 KDE 和 X 的应用程序
- mail—一个基于控制台的邮件代理
- mutt—一个基于控制台的邮件（及新闻阅读）代理
- Sendmail—一个用于 UNIX 和 Linux 的全面邮件传输代理
- xbf—一个邮件通知 X 

# 参考

以下参考文献是电子邮件配置的推荐阅读材料。当然，所有参考文献都适用于你。根据你使用的电子邮件服务器选择相关的。

# 网络资源

http://www.instinct.org/elm/—关于 elm 邮件程序的综合信息网站。

http://www.washington.edu/pine/—Internet News & Email (pine) 邮件程序主页。

http://www.sendmail.org—这是 Sendmail 主页。在这里你将找到关于 Sendmail MTA 的配置信息和常见问题解答。

http://www.postfix.org—这是 Postfix 主页。如果你在使用 Postfix MTA，可以在此站点找到文档和示例配置。

http://www.qmail.org—这是 Qmail MTA 的主页。它包含了 Qmail 的文档以及指向其他资源的链接。

ftp://ftp.isi.edu/in-notes/—RFC（意见征求）库，它们定义了现代计算机使用的技术“规则”。

http://www.procmail.org—Procmail 主页。
http://www.moongroup.com/docs/procmail/—Procmail 常见问题解答，包含故障排除建议。该页面还引用了一个链接页面，该页面又引用了其他链接集以及 Procmail 邮件列表提示。

# 书籍

O’Reilly 出版的《Sendmail》。这是所有 Sendmail 的事实标准指南。它超过 1000 页，让你了解 Sendmail 到底有多复杂。

Sams Publishing 出版的《Postfix》。这是 Sams 出版的一本新书，涵盖了 Postfix MTA。

Sams Publishing 出版的《Running Qmail》。这本书与 Sams 出版的 Postfix 书类似，只是它涵盖了 Qmail MTA。

# 第 20 章

# 新闻与其他协作

# 本章内容

- 网络新闻概述
- 配置本地新闻服务器
- 新闻阅读器
- TWiki
- 互联网聊天 (IRC)
- 在 Red Hat Linux 中带有 KIT 和 GAIM 的 IM
- Gnome 视频会议
- 邮件列表管理
- 参考
