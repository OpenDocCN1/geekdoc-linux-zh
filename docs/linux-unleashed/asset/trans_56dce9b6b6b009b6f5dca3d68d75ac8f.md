
由于许多人使用基于命令行的 FTP 来获取他们的 Linux 软件，因此本节将使用这种版本。在与你的 ISP 建立互联网连接后，即可启动 FTP。如果你使用的是 Windows 机器，DOS 窗口通常是最简单的连接方式。打开一个 DOS 窗口，并在 ftp 命令行中输入你要访问的服务器的名称。

一旦你发出 FTP 命令，你的系统将尝试连接到远程机器。当连接成功完成后，远程机器会提示你输入用户 ID。除非该系统支持匿名 FTP（所有 Linux FTP 站点都支持），否则你必须拥有该系统的有效用户 ID 和密码。当你首次连接且在登录之前，通常会显示一条消息，告知你远程系统支持匿名 FTP。例如，下面对 Linux FTP 存档站点 sunsite.unc.edu 的登录过程立即告诉你匿名登录是可以接受的：

```
ftp sunsite.unc.edu
331 Guest login ok, send your complete e-mail address as password.
Enter username (default: anonymous): anonymous
Enter password [tparker@tpci.com]:
!FTP] Open
230-            WELCOME to UNC and SUN's anonymous ftp server
230-            University of North Carolina
230-            Office FOR Information Technology
230-            SunSITE.unc.edu
230 Guest login ok, access restrictions apply.
FTP>
```

匿名 FTP 站点的登录名通常是“guest”或“anonymous”。登录消息通常会告诉你使用的是哪一个，或者你可以尝试两者。在大多数情况下，远程机器会提示你输入密码。有些系统不需要你提供密码，而有些系统则要求你输入你的用户名或电子邮件地址。这仅用于跟踪目的，并且不会带来任何安全问题（除非你在你的本地账户上没有设置密码！）。

登录过程完成后，当你提供了登录名和密码后，你会看到提示符“FTP>”。这表明系统已准备好接受 FTP 命令。有些系统在登录时会显示一条简短的消息，其中包含下载文件的说明以及作为匿名 FTP 用户所受到的任何限制。还可能显示有关有用文件位置的其他信息。例如，你可能会看到来自 FTP 站点 sunsite.unc.edu 的此类消息：

要获取二进制文件，请输入：BINARY，然后输入：GET "File.Name" newfilename
要获取文本文件，请输入：ASCII，然后输入：GET "File.Name" newfilename

名称必须完全匹配大小写。请如所示使用"引号"。要获取目录，请输入：DIR。要更改目录，请输入：CD "Dir.Name" 要读取短文本文件，请输入：GET "File.Name" TT 更多内容，请输入 HELP 或查看 gopher 中的 FAQ。要退出，请输入 EXIT 或 Control-Z。

230- 如果你向 info@sunsite.unc.edu 发送电子邮件，你会收到有关如何使用 sunsite 提供的不同服务的帮助信息
230- 我们使用 Wuarchie 实验性 ftpd。如果你"get" <directory>.tar.Z
230- 或 <file>.Z，它将即时进行压缩和/或 tar 打包。使用".gz"代替
230- ".Z" 将使用 GNU zip (/pub/gnu/gzip*)，这是一种更优越的
230- 压缩方法。

![](img/e8e6b47ac20475e23d48b4c476f5d891_66_0.png)

一旦你进入了远程系统，你可以使用 Linux（UNIX）命令来显示文件内容并在目录之间移动。要显示目录的内容，使用命令 ls 或 DOS 等效命令 dir。要切换到子目录，使用 cd <dir> 命令。要返回父目录（当前目录的上层目录），使用命令 cd ... 与 Linux 不同，FTP 没有键盘快捷键，因此你必须完整（且正确）地输入文件或目录的名称。

当你在目录中移动并找到想要转移到你的系统的文件时，使用 FTP 的 get 命令，例如：
get "file1.txt"

get（下载）和 put（上传）命令是相对于你的本地机器而言的，而不是相对于远程机器。当你发出 get 命令时，你是在告诉你的系统的 FTP 软件从远程机器获取文件。put 命令告诉 FTP 将本地机器上的文件放到远程机器上。记住哪个命令朝哪个方向移动文件非常重要，否则你可能会意外覆盖文件。

在大多数版本的 FTP 中，文件名周围的引号是可选的，但它们确实为远程版本提供了特定字符（防止 shell 扩展）。这可以防止来自 FTP 的错误消息或意外传输许多文件而不是仅传输一个文件，因此使用引号是一个有用的惯例。

当你发出 get 命令时，远程系统会将数据转移到你的本地机器，并在完成后显示状态消息。在传输大文件期间没有进度指示，因此要有耐心。这是一个 get 命令的示例记录：

```
FTP> get "file1.txt"
200 PORT command successful.
150 BINARY data connection for FILE1.TXT (27534 bytes)
226 BINARY Transfer complete.
27534 bytes received in 2.35 seconds (12 Kbytes/s).
```

FTP 提供两种文件传输模式：ASCII（7 位字符）和 Binary（8 位字符）。有些系统会自动在这两种模式之间切换，但手动设置模式以确保不浪费时间是个好主意。你必须以 Binary 模式下载所有 Linux 发行版文件。要将 FTP 设置为二进制传输模式（对于任何可执行文件），输入命令

```
binary
```

你可以使用命令 ASCII 切换回 ASCII 模式。如果你在 ASCII 模式下传输二进制文件，它将无法执行。以 Binary 模式传输 ASCII 文件不会影响文件的内容，因此 Binary 是一个良好的默认传输模式。

![](img/e8e6b47ac20475e23d48b4c476f5d891_68_0.png)

要退出 FTP，输入命令 quit 或 exit。这两个命令都会关闭你在远程机器上的会话，然后终止你本地机器上的 FTP。

请记住，Linux 存档非常大，使用异步调制解调器传输即使是小的发行版也需要一段时间。如果你使用慢速调制解调器（9,600 波特或更低），你可能需要考虑替代方法，因为你的连接必须保持长达数小时。一些远程站点限制你可以保持连接的时间。

## Linux FTP 存档站点

Linux FTP 存档站点的列表变化缓慢，但以下列出的站点在本书付印时都是有效且可访问的。其中许多站点是镜像站点，提供与主站点完全相同的内容。Linux FTP 存档的主站点（也称为 home 站点）是 tsx-11.mit.edu、sunsite.unc.edu 和 nic.funet.fi。大多数新软件的加载始于 home 站点。上一列表中大多数站点都是这三个站点之一的镜像。

你可以通过使用站点名称末尾的国家/地区标识符（uk=英国，fr=法国等）找到离你最近的站点。大多数版本的 FTP 允许使用机器名称或 IP 地址，但如果名称无法被本地互联网网关解释，IP 地址是最佳的寻址方法。确保你正确输入了 IP 地址的四个组件。表 2.1 显示了在本书付印时是 Linux 材料良好来源的站点。

### 表 2.1 Linux FTP 站点及其 IP 地址。

| 站点名称 | IP 地址 | 目录 |
|---|---|---|
| tsx-11.mit.edu | 18.172.1.2 | /pub/linux |
| sunsite.unc.edu | 152.2.22.81 | /pub/linux |
| nic.funet.fi | 128.214.6.100 | /pub/OS/Linux |
| ftp.mcc.ac.uk | 130.88.200.7 | /pub/linux |
| fgb1.fgb.mw.tu-muenchen.de | 129.187.200.1 | /pub/linux |
| ftp.informatik.twmuemchen.de | 131.159.0.110 | /pub/Linux |
| ftp.dfv.rwth-aachen.de | 137.226.4.105 | /pub/linux |
| ftp.informatik.rwth-aachen.de | 137.226.112.172 | /pub/linux |
| ftp.ibp.fr | 132.227.60.2 | /pub/linux |
| kirk.bu.oz.au | 131.244.1.1 | /pub/OS/Linux |
| ftp.uu.net | 137.39.1.9 | /systems/unix/linux |
| warchive.wustl.edu | 128.252.135.4 | /systems/linux |
| ftp.win.tue.nl | 131.155.70.100 | /pub/linux |
| ftp.stack.urc.tue.nl | 131.155.2.71 | /pub/linux |
| ftp.ibr.cs.tu-bs.de | 134.169.34.15 | /pub/os/linux |
| ftp.denet.dk | 129.142.6.74 | /pub/OS/linux |

如果你在连接到一个站点时遇到困难，请尝试连接另一个站点。如果困难持续存在，你的互联网访问可能存在问题。

