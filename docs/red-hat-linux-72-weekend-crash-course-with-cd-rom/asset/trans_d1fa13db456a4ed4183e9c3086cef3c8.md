

![](img/5fe8f856723cde0b366f73584b9e64b8_296_0.png)

## 从源文件构建软件包

### 课程检查清单
- 1. 下载和解压软件
- 2. 从源文件构建并安装软件

![](img/5fe8f856723cde0b366f73584b9e64b8_296_1.png)

在第 23 课中，你学习了如何安装以红帽包管理器（Red Hat Package Manager，RPM）格式分发的软件包。RPM 文件打包了安装软件包所需的所有可执行二进制文件和配置文件。然而，许多开源软件包是以源代码形式分发的，不包含任何可执行二进制文件。要使用此类软件，你必须先构建可执行二进制文件，然后按照说明安装该包。本课将向你展示如何下载和解压源文件。接着，它将向你展示如何从源文件构建软件包并将其安装。

## 下载和解压软件

源文件通常以压缩 tar 归档形式分发。如你在第 26 课中学到的，`tar` 程序创建这些归档，然后 `gzip` 程序对它们进行压缩。分发形式是一个带有 `.tar.gz` 或 `.tar.Z` 扩展名的大型单个文件，通常被称为压缩或 gzip 过的 tar 球（tarball）。如果你想要该软件，你就必须下载压缩的 tar 球并解压它。

你使用匿名文件传输协议（FTP）或 Web 浏览器下载压缩的 tar 文件。通常，这个操作除了点击链接并将文件保存在系统的适当目录外，不需要你花费更多精力。

为了尝试下载和构建软件包，你可以对 X 多媒体系统（XMS）进行练习，它是一个用于播放 MP3 文件和其他多媒体文件的图形化 X 应用程序。XMS 随红帽 Linux 捆绑提供，并在你安装红帽 Linux 期间选择多媒体支持包组时安装在你的系统上。但是，再次下载并重新构建 XMS 包并无害处。

你可以从 http://www.xms.org/download.html 访问 XMMS 的源文件，其形式为压缩 tar 归档。你也可以从匿名 FTP 服务器（ftp.xms.org）的 xms1.0 目录下载这些文件。

**请尝试从匿名 FTP 服务器下载 XMMS 源文件，以便你知道如何手动访问文件。**

在尝试从 FTP 服务器下载文件之前，请确保你的 Linux 系统已连接到互联网。你还应该将目录更改为你想要存储下载文件的位置（尽管你总可以在下载后移动文件）。你可能希望以 root 身份登录并在输入 ftp 命令之前将目录更改为 `/usr/local`。如果你使用 GNOME 或 KDE 桌面，请在终端窗口中键入这些命令。

## 下载软件

下面是一个示例会话，当你从匿名 FTP 服务器下载 XMMS 的压缩 tar 文件时，可以将其作为指南。键入的行以粗体文本显示。

```
ftp ftp.xms.org
Connected to ftp.xms.org.
220 ProFTP 1.2.0r610 Server (FTP server for awpti.org) [awpti.org]
Name (ftp.xms.org:nbab): anonymous
331 Anonymous login ok, send your complete e-mail address as password.
Password: (Type your e-mail address and press Enter)
230 Anonymous access granted, restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd xms1/1.0
250 CWD command successful.
ftp> ls
200 PORT command successful.
150 Opening ASCII mode data connection for file list.
drwxr-x-x 6 xms xms 4096 Jan 30 15:20 rpm
-rw-r--r- 1 xms xms 709009 Jan 30 15:22 xms-1.0.0.tar.gz
-rw-r--r- 1 xms xms 715574 Jan 30 15:15 xms-1.0.1.tar.gz
226 Transfer complete.
ftp> binary
200 Type set to I.
ftp> get xms-1.0.1.tar.gz
200 PORT command successful.
150 Opening BINARY mode data connection for xms-1.0.1.tar.gz (715574 bytes).
226 Transfer complete.
715574 bytes received in 383 secs (1.8 Kbytes/sec)
ftp> bye
ftp ftp.xms.org
Connected to ftp.xms.org (194.236.124.44).
220 f3d2 FTP server (version 6.00<rba41.0.8) ready.
Name (ftp.xms.org:kwali): anonymous
331 Guest login ok, type your name as password.
Password: (Type your e-mail address and press Enter)
```

```
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd xms-1.2.x
250 CWD command successful.
ftp> ls
227 Entering Passive mode (194,236,124,44,187,21)
150 Opening ASCII mode data connection for ‘.'
-rw-r--r-- 1 1136 xms 194572 May 11 01:16 xms-1.2.4.tar.gz
-rw-r--r-- 1 1136 xms 148604 Jun 19 21:39 xms-1.2.5.tar.bz2
-rw-r--r-- 1 1136 xms 241840 Jun 19 21:37 xms-1.2.5.tar.gz
226 Transfer complete.
ftp> binary
200 Type set to 1.
ftp> get xms-1.2.5.tar.gz
150 Opening xms-1.2.5.tar.gz Remote: xms-1.2.5.tar.gz
227 Entering Passive mode (194,236,124,44,187,51)
150 Opening BINARY mode data connection for ‘xms-1.2.5.tar.gz’ (241840 bytes).
226 Transfer complete.
241840 bytes received in 634 secs (3.7 Kbytes/sec)
ftp> bye
221 Goodbye.
```

请注意，你必须使用用户名 `anonymous` 登录，这是匿名 FTP 的标准登录名。匿名 FTP 允许没有服务器用户账户的人登录并检索文件。然而，匿名账户受到严重限制，仅用于从 FTP 服务器发送和检索文件。对于密码，你应该键入你的电子邮件地址，然后按 Enter。要更改目录，使用 `cd` 命令。要获取目录列表，使用 `ls` 命令。

你需要键入 `binary` 命令，以确保数据传输发生在二进制模式，因为 `.tar.gz` 文件是二进制文件。然后你可以使用 `get` 命令下载文件，在本例中为 `xms-1.0.1.tar.gz`。请记住，`.tar.gz` 扩展名告诉你这是一个压缩 tar 归档。下载完成后，键入 `bye` 或 `quit` 以结束匿名 FTP 会话。

下载压缩 tar 文件后，你应该首先使用以下命令检查内容（为了节省空间，并非显示所有输出）：

```
tar ztf xms.tar.gz | more
xms-1.2.5/
xms-1.2.5/Makefile.in
xms-1.2.5/README
xms-1.2.5/stamp-h1.in
xms-1.2.5/ABOUT-NLS
xms-1.2.5/AUTHORS
xms-1.2.5/COPYING
xms-1.2.5/ChangeLog
xms-1.2.5/INSTALL
xms-1.2.5/Makefile.am
xms-1.2.5/NEWS
xms-1.2.5/TODO
xms-1.2.5/accconfig.h
xms-1.2.5/aclinclude_m4
xms-1.2.5/aclonly_m4
```

```
xsms-1.2.5/config.guess
xsms-1.2.5/config.h.in
xsms-1.2.5/config.sub
xsms-1.2.5/configure
```

此命令的输出显示了归档的内容，并让你了解解压归档后将创建哪些目录。在这种情况下，当前目录（在本例中为 `/usr/local/`）中创建了一个名为 `xms-1.2.5` 的目录。从列表中，你还可以了解到编写该包使用的编程语言。如果你看到 `.c` 和 `.h` 文件，那意味着源文件是 C 编程语言，许多开源软件包都使用 C 语言编写。

## 解压软件

要提取（或解压）tar 归档的内容，键入以下 tar 命令：

```
tar zxvf xms*.gz
```

再次，你会看到从归档中提取并复制到硬盘上相应目录的文件长列表。

如果你下载的归档结尾是 `.bz2` 而不是 `.gz`，这意味着该归档是使用 `bzip2` 实用程序压缩的。为了解压这种归档，在 tar 命令中将 `z` 替换为 `j`。即，键入 `tar xjvf xms*.bz2`。

现在你准备好构建软件了。

## 从源文件构建软件并安装它

解压压缩 tar 归档后，所有源文件都位于一个目录中，其名称通常是软件包名称加上版本号后缀。例如，XMS 版本 1.2.5 的源文件提取在 `xms-1.2.5` 目录中。要开始构建软件的过程，使用以下命令更改目录：

```
cd xms*
```

你不必键入整个名称。shell 可以扩展目录名称并将其更改为 `xms-1.2.5` 目录。

几乎所有软件包都附带一个或多个 `README` 或 `INSTALL` 文件，或类似名称的文件。这些是包含有关如何构建和安装包的说明的文本文件。XMS 也不例外；它附带一个 `README` 文件，你应该通过键入 `more README` 来阅读。还有一个包含构建和安装 XMS 说明的 `INSTALL` 文件。

