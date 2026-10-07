
## 附录

### 第九部分

**本部分包含**

- Linux FTP 站点和新闻组 1023
- Linux 商业供应商 1037
- Linux 文档项目 1043
- GNU 通用公共许可证 1045
- 版权信息 1055
- CD-ROM 上有什么？ 1061

### 附录 A

#### Linux FTP 站点和新闻组

**本附录包含**

- FTP 站点 1024
- 电子公告板 1029
- Usenet 新闻组 1034

如果你可以访问互联网，无论是直接通过 ISP（互联网服务提供商）还是通过 CompuServe、Delphi 或 America Online 等在线服务提供商，你可以访问更多的 Linux 软件和信息来源。有两个流行的 Linux 软件和帮助来源，一个是通过 FTP，另一个是通过专门的 Linux Usenet 新闻组。

如果你无法访问互联网，你仍然可能通过其他来源获取一些信息，例如由专门分发公有领域材料的公司发布的电子公告板系统（BBS）和 CD-ROM。

## FTP 站点

FTP 是一种访问远程系统并下载文件的方法。它使用起来非常简单，并为拥有互联网接入的用户提供了快速更新二进制文件列表的方法。

对于无法访问 FTP 但可以通过互联网使用电子邮件的用户，ftpmail 工具可以提供对这些 FTP 站点的访问。

### 什么是 FTP？

文件传输协议（FTP）是 TCP/IP 协议族中的一种协议。TCP/IP 被广泛用作互联网的通信协议，同时也用于许多局域网（LAN）。UNIX 系统几乎总是使用 TCP/IP 作为其协议。

FTP 用于在运行 TCP/IP 的机器之间传输文件。也有一些类似 FTP 的程序可用于其他一些协议。

要使用 FTP，连接的两端都必须运行提供 FTP 服务的程序。要从远程系统下载文件，你必须启动你的 FTP 软件，并指示它连接到运行在远程机器上的 FTP 软件。

互联网上有许多 FTP *归档站点*。这些是设置好以便任何人可以连接并下载软件的机器。在某些情况下，存在相互镜像的 FTP 归档站点。*镜像站点* 是保持与另一个站点完全相同软件的站点，因此你只需连接到对你来说更容易访问的那个站点，就可以像在另一个站点连接一样下载相同的软件。

通常，当你连接到远程系统时，必须登录。这意味着你必须是一个有效用户，拥有该远程机器的用户名和密码。由于不可能为每个想要访问公共归档的人都提供登录权限，许多系统使用匿名 FTP。匿名 FTP 允许任何人以 guest 或 anonymous 的登录名登录系统，并且要么没有密码，要么使用用户本地系统的登录名（仅用于审计目的）。

### 使用 FTP 连接和下载文件

使用 FTP 连接到远程站点非常容易。假设你可以直接或通过服务提供商访问互联网，你必须启动 FTP 并提供你想连接的远程系统的名称。如果你直接连接到互联网，过程很简单：你输入 ftp 命令并附上远程站点的名称，例如：

```
ftp sunsite.unc.edu
```

如果你使用的是 Delphi 等在线服务，你必须访问其互联网服务菜单并从中启动 FTP。一些在线服务允许你在提示符处输入任何 FTP 站点的名称，而另一些服务则有一些列出所有可用站点的菜单。你可能需要查阅你服务提供商的在线文档才能找到正确的操作步骤。

发出 FTP 命令后，你的系统将尝试连接到远程机器。当连接成功时（假设远程系统允许 FTP 登录），远程系统会提示你输入用户 ID。如果系统支持匿名 FTP，通常会有消息告知你这一点。以下是登录 Linux FTP 归档站点 sunsite.unc.edu 的示例：

```
ftp sunsite.unc.edu
331 Guest login ok, send your complete e-mail address as password.
Enter username (default: anonymous): anonymous
Enter password [tparker@tpci.com]:
[FTP] Open
230-                        WELCOME to UNC and SUN's anonymous ftp server
230-                        University of North Carolina
230-                        Office FOR Information Technology
230-                        SunSITE.unc.edu
230 Guest login ok, access restrictions apply.
FTP>
```

登录过程完成后，你会看到提示符 FTP>，表示系统准备好接受命令。登录某些系统时，你会看到一条简短的消息，其中可能包含下载文件的说明、作为匿名 FTP 用户受到的任何限制，或有用的文件位置信息。例如，你可能会看到这样的消息：

```
To get a binary file, type: BINARY and then: GET "File.Name" newfilename
To get a text file, type: ASCII and then: GET "File.Name" newfilename
Names MUST match upper, lower case exactly. Use the "quotes" as shown. To get a directory, type: DIR. To change directory, type: CD "Dir.Name" To read a short text file, type: GET "File.Name" TT For more, type HELP or see FAQ in gopher. To quit, type EXIT or Control-Z.
```

230- 如果你给 info@sunsite.unc.edu 发邮件，你会收到有关如何使用 sunsite 提供的不同服务的帮助信息
230- 我们使用 Wuar chive 实验性 fpfd。如果你 “获取” `<directory>.tar.Z`
230- 或 `<file>.Z`，它将即时压缩和/或打包。使用 “ .gz ” 代替
230- “.Z” 将使用 GNU zip (/pub/gnu/gzip*)，这是一种更高级的压缩方法。

连接到远程系统后，你可以使用熟悉的 Linux 命令来显示文件内容并在目录中移动。例如，要显示目录内容，使用命令 `ls` 或 DOS 等效命令 `dir`。要切换到子目录，使用 `cd` 命令。要返回父目录（当前目录的上一级），使用命令 `cd ..` 或 `cd`。FTP 没有键盘快捷键，因此你必须完整输入文件或目录的名称。

当你在目录中浏览并找到想要传输到主系统的文件时，使用 get 命令：

```
get "file1.txt"
```

命令 `get`（下载）和 `put`（上传）是相对于你的主机器而言的。你是告诉你的系统从远程位置获取文件并将其放到本地机器上，或者将本地机器上的文件放到远程机器上。这与另一种常用的 TCP/IP 协议 Telnet 相反，Telnet 中一切都是相对于远程机器而言的。记住哪个命令朝哪个方向移动很重要，否则你可能会意外覆盖文件。

在大多数 FTP 版本中，文件名周围的引号是可选的，但它们向远程版本提供了特定字符（防止 shell 扩展），因此建议使用引号以避免错误。FTP 提供两种文件传输模式：ASCII 和二进制。一些系统会自动在这两者之间切换，但手动设置模式是一个好主意，以确保你不浪费时间。要将 FTP 设置为二进制传输模式（用于任何可执行文件），输入命令 `binary`。

你可以使用命令 `ASCII` 切换回 ASCII 模式。由于你很可能正在检查远程站点是否有新的二进制文件或源代码库，对于大多数传输使用二进制模式是一个好主意。如果你以 ASCII 模式传输二进制文件，它在你的系统上不可执行（或不可理解）。ASCII 模式仅包含有效的 ASCII 字符，而不包含二进制文件内部使用的 Ctrl+键序列。以二进制模式传输 ASCII 文件不会影响其内容，尽管杂波噪声在极少情况下可能会引起问题。

当你发出 get 命令时，远程系统会将数据传输到你的本地机器，并在完成后显示状态消息。在传输大文件时没有进度指示，所以要耐心一点。

```
FTP> get "file1.txt"
200 PORT command successful.
150 BINARY data connection for FILE1.TXT (27534 bytes)
226 BINARY Transfer complete.
27534 bytes received in 2.35 seconds (12 Kbytes/s).
```

要退出 FTP，输入命令 `quit` 或 `exit`。其中任何一个都会关闭你在远程机器上的会话，然后终止你本地机器上的 FTP。

### 使用 ftpmail

如果你无法通过 FTP 访问远程站点，情况并未完全糟糕。如果你有电子邮件，你仍然可以接收文件传输。一些在线系统允许发送和接收互联网邮件，但不允许直接访问 FTP。类似地，一些互联网服务提供商提供 UUCP 账户，不允许直接连接但提供电子邮件。要访问 FTP 站点并传输文件，你可以使用 ftpmail 工具。

前文提到的站点 sunsite.unc.edu 是一个主要的 Linux 归档站点，支持 ftpmail。（本附录中列出的所有 Linux FTP 站点也支持 ftpmail。）要了解如何使用 ftpmail，向其中一个站点的登录名 ftpmail 发送电子邮件消息，例如 ftpmail@sunsite.unc.edu，并且消息正文只包含一个单词：help。

通过回信，ftpmail 工具将发送使用该服务的说明。基本上，你在邮件消息中发送你想要执行的 FTP 命令的正文，因此你可以通过以下文本在邮件消息中获取 Linux 目录的目录列表：

```
open sunsite.unc.edu
cd /pub/Linux
ls
quit
```

你可以使用类似的邮件消息通过电子邮件传输文件回来：

```
open sunsite.unc.edu
```

