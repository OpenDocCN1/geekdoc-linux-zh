
- Taklap Systems Ltd., The Reddings, Court, Robin Lane, llangwm, Usk, Gwent, United Kingdom NP1ET, Tel: +44 (0)291 650357, Fax:+44 (0)291 650500, info@demon.co.uk

- Trans-Ameritech Enterprises, Inc., 2342 Wals Ave, Santa Clara, CA 95051, Tel: +1 408 727-3883, roman@trans-ameritech.com

- Unifix Software GmbH, Postfach 4918, D-38039 Braunschweig, Germany, Tel: +49 (0)531 515161, Fax:+49 (0)531 515162

- Yggdrasil Computing, Incorporated, 48880 Stevens Creek Blvd., Suite 205, San Jose, CA 95129-1034, Tel: +1 800 261-6630, +1 408 261-6630, info@yggdrasil.com

## 附录 C

### FTP 教程与站点列表

FTP（文件传输协议）是用于在互联网上的系统之间传输文件的程序集。互联网上的大多数 UNIX、VMS 和 MS-DOS 系统都有一个名为 `ftp` 的程序供你用来传输这些文件，如果你有互联网接入，下载 Linux 软件的最佳方法是使用 `ftp`。本附录涵盖了 `ftp` 的基本用法——当然，其的功能和用途比这里提供的多得多。

附录末尾提供了可以 Linux 软件的 FTP 站点列表。此外，如果你没有直接访问互联网，但需要与互联网交换电子邮件，下方还包含了使用 `ftpmail` 服务的信息。

如果你使用 MS-DOS 或 VMS 系统从互联网下载内容，那么 `ftp` 是一个命令行驱动的程序。然而，还有其他 `ftp` 的实现，例如 Macintosh 版本（称为 Fetch），它拥有良好的菜单驱动界面，非常浅浅懂。即使你没有使用命令行驱动版本的 `ftp`，这里提供的信息也对你有所帮助。

`ftp` 可用于从其他互联网站点上传（发送）或下载（接收）文件。在大多数情况下，你将下载软件。互联网上有大量公开的 FTP 归档站点，它们允许任何人通过 `ftp` 访问它们并下载免费软件。其中一个站点是 `sunsite.unc.edu`，它拥有许多 Sun Microsystems 软件，是主要的 Linux 站点之一。

#### C.1 启动 ftp

注意，在下方打印的示例“屏幕”中，我只显示了最重要的信息，你看到的可能有所不同。此外，斜体命令代表你输入的命令；其他所有都是屏幕输出。

要启动 `ftp` 并连接到站点，只需使用命令

```
ftp (hostname)
```

其中 `(hostname)` 是你所连接的站点名称。例如，为了连接到虚构站点 `shoop.vpizza.com`，我们可以使用命令

```
ftp shoop.vpizza.com
```

#### C.2 登录

当 `ftp` 启动时，我们应该看到类似的内容

```
Connected to shoop.vpizza.com.
220 Shoop.vpizza.com FTPD ready at 15 Dec 1992 08:20:42 EDT
Name (shoop.vpizza.com:mdw):
```

在这里，`ftp` 询问你想要登录 `shoop.vpizia.com` 的用户名。默认值是 `mdw`，这是我正在使用的 FTP 系统上的用户名。由于我没有 `shoop.vpizia.com` 的账户，因此我无法以我的身份登录。相反，要访问 FTP 站点上公开可用的软件，你需要以匿名（`anonymous`）身份登录，并提供你的电子邮件地址（如果有的话）作为密码。因此，你会输入：

```
Name (shoop.vpizia.com:mdw) anonymous
331-Guest login ok, send e-mail address as password.
Password: mdw@sunsite.unc.edu
230- Welcome to shoop.vpizza.com.
230- Virtual Pizza Delivery[tm]: Download pizza in 30 cycles or less
230- or you get FREE!
ftp>
```

当然，你应该提供自己的电子邮件地址而不是我的，而且在你输入时，它不会回显显示在屏幕上（因为从技术上讲，它是一个“密码”）。`ftp` 应该允许我们登录，之后我们就可以准备下载软件了。

### C.3 熟悉操作

好了，我们进来了。`ftp>` 是我们的提示符，`ftp` 程序正在等待命令。有几个你需要了解的基础命令。首先，是这些命令：

- `ls` (`文件`)

- `dir` (`文件`)

命令

- `cd` (`目录`)

将移动到指定的目录（类似于 UNIX 或 MS-DOS 系统上的 `cd` 命令）。你可以使用命令

- `cd ..`

来切换到父目录。

命令

- `help` (`命令`)

将提供关于指定的 `ftp`（命令）的帮助信息，例如 `ls` 或 `cd`。如果未指定命令，`ftp` 将列出所有可用的命令。

如果我们在此时此刻输入 `dir`，我们将看到当前位置的初始目录列表。

```
ftp> dir
200 PORT command successful.
150 Opening ASCII mode data connection for /bin/ls.
total 1337
```

> 当前目录上方的目录。

### C.4 下载文件

```
drxr-xr-x 2 root wheel 512 Aug 13 13:55 bin
drxr-xr-x 2 root wheel 512 Aug 13 13:58 dev
drxr-xr-x 2 root wheel 512 Jan 25 17:35 etc
drxr-xr-x 19 root wheel 1024 Jan 27 21:39 pub
drwrwx-wx 4 root ftp-admi 1024 Feb 6 22:10 uploads
drxr-xr-x 3 root wheel 512 Mar 11 1992 usr
```

226 Transfer complete.

921 bytes received in 0.24 seconds (3.7 Kbytes/s)

ftp>

这些条目中的每一个都是一个目录或一个我们可以下载的单个文件（通过列表第一列的 `d` 来）。在大多数 FTP 存档站点上，公开的软件都在 `/pub` 目录下，所以让我们去那里吧。

```
ftp> cd pub
ftp> dir
200 PORT command successful.
1550 ASCII data for /bin (128.181.1.4525) (0 bytes).
total 846
```

```
-r--r--r-- 1 root staff 1433 Jul 12 1998 README
-r--r--r-- 1387 staff 15586 May 13 1991 US-DOMAIN.TXT
-r--r--r-- 1539 staff 52664 Feb 20 1991 altenergy.avail
-r--r--r-- 16534 65534 56456 Dec 27 1990 ataxx.tar.z
-r--r--r-- 1 root other 2013041 Jul 3 1991 gesysp.tar.z
-r--r--r-- 1432 staff 41831 Jan 3 1980 gneqe.arc
-rwx-rw- 1615 staff 50315 Apr 16 1992 linpack.tar.z
-r--r--r-- 1 root wheel 12168 Dec 25 1990 localtime.o
-r--r--r-- 1 root staff 7035 Aug 27 1996 manualslist.tbl
drxr-xr-x 2195 staff 512 Mar 10 00:48 mdw
-r--r--r-- 1 root staff 5593 Jul 19 1988 t.out.h
```

226 ASCII Transfer complete.

2443 bytes received in 0.35 seconds (6.8 Kbytes/s)

ftp>

在这里我们可以看到许多（可能有趣的？）文件，其中一个名为 `README`，我们应该下载它（大多数 FTP 站点在 `/pub` 目录下都有一个 `README`）。

#### C.4 下载文件

在下载文件之前，有几点你需要注意：

- 开启哈标记（hash marking）。哈标记会在文件传输时打印在屏幕上；它们能让你知道传输了多少进度，以及你的连接没有挂断（这样你就不用坐在那里等 20 分钟以为还在下载）。通常情况下，哈标记显示为美元符号（`$`），每传输 1024 或 8192 字节打印一次，取决于你的系统。要开启哈标记，请输入命令：

```
ftp> hash on
```

- 确定你下载的文件类型。对于 FTP 来说，文件有两种类型：二进制（`binary`）和文本（`text`）。你下载大部分文件是程序、压缩文件、存档文件等。然而许多是文本文件。为什么文件类型很重要？只有某些系统（如 MS-DOS 系统）文本文件中的回车符需要转换后才可读。在二进制模式下传输时，不进行转换——文件直接按字节传输。`bin` 和 `ascii` 命令分别将传输模式设置为二进制和文本。如果不确定，始终使用二进制模式传输文件。如果你尝试用文本模式传输二进制文件，文件将会损坏且无法使用。对于我们的例子，读取 `README` 可能是一个文本文件，所以我们使用命令：

```
ftp> ascii
```

- 设置你的本地目录。你的本地目录是你希望下载的文件存放的系统目录。`cd` 命令更改的是远程目录（你正在 FTP 的远程机器），而另一个更改的是本地目录。例如，将本地目录设置为 `/home/db/mdw/tmp`，使用命令：

```
ftp> cd /home/db/mdw/tmp
Local directory now /home/db/mdw/tmp
```

现在你准备好下载文件了。`get remote-name [local-name]` 命令中 `remote-name` 是远程机器上的文件名，`local-name` 是你想给本地机器的名字。`local-name` 参数是可选的；默认与远程文件名相同。然而，如果你正在下载的文件在本地目录下已经有一个 `README`，你会想要一个不同的 `local-filename` 以免覆盖。对于我们的例子，下载 `README`，我们只需使用：

```
ftp> get README
200 PORT command successful.
150 ASCII data connection for README (128.84.1.4527) (1433 bytes).
226 ASCII Transfer complete.
local: README remote: README
1493 bytes received in 0.03 seconds (49 Kbytes/s)
ftp>
```

### C.5 退出 FTP

要结束 FTP 会话，只需使用命令：

```
quit
```

命令

```
close
```

用于关闭当前 FTP 站点的连接；可以使用 `open` 命令启动另一个站点的会话（而不退出 FTP 程序）。

```
ftp> close
221 Goodbye.
ftp> quit
```

### C.6 使用 ftpmail

`ftpmail` 是一种通过互联网电子邮件从 FTP 存档站点获取文件的服务。如果你无法直接上网，但可以向互联网发送邮件（例如通过 CompuServe 等服务），`ftpmail` 是从 FTP 存档站点获取文件的好方法。遗憾的是，在发送大量负载时速度可能会慢。在使用 `ftpmail` 下载大量软件之前，请确保你的邮件邮箱能够处理这些流量。许多系统对传入邮件有配额，如果你的邮件超过此配额，可能会删除你的账户。请在使用常识。

`sunsite.unc.edu` 主要 Linux FTP 存档站点之一，拥有 `ftpmail` 服务器。要使用此服务，请向以下地址发送电子邮件：

`ftpmail@sunsite.unc.edu`

```
ftpmail@sunsite.unc.edu
```

正文仅包含单词：

`help`

这将向你发送一份 `ftpmail` 命令列表以及使用系统的简要教程。例如，要获取 `sunsite.unc.edu` 上的 Linux 文件列表，向上述地址发送以下文本：

```
open sunsite.unc.edu
cd /pub/Linux
dir
quit
```

你可以使用 `ftpmail` 服务连接到任何 FTP 存档站点；你不限于 `sunsite.unc.edu`。后续章节列出了若干 Linux FTP 存档。

### C.7 Linux FTP 站点列表

表 C.1 是携带 Linux 软件的最知名 FTP 存档站点列表。请记住，许多其他站点都是镜像，你可能在列表之外的站点遇到 Linux。

| 站点名称 | IP 地址 | 目录 |
| :--- | :--- | :--- |
| tsx-11.mit.edu | 18.172.1.2 | /pub/linux |
| sunsite.unc.edu | 152.22.281 | /pub/linux |
| nic.funet.fi | 128.214.600 | /pub/OS/Linux |
| fpc.mcc.ac.edu | 130.88.200.7 | /pub/linux |
| fgbl.fgb.mw-tu-muenchen.de | 129.187.200.1 | /pub/linux |
| ftp.informatik.tu-muenchen.de | 131.159.0110 | /pub/linux |
| ftp.dfv.rwht-aachen.de | 137.226.4105 | /pub/linux |
| ftp.informatik.rwht-aachen.de | 137.226.122.172 | /pub/linux |
| ftp.hfr | 132.227.602 | /pub/linux |
| kit.box.au.edu | 131.244.1.1 | /pub/OS/Linux |
| ftp.uu.net | 137.39.1 | /systems/unix/linux |
| woarchive.wustl.edu | 128.252.135.4 | /systems/linux |
| ftp.wie.tu.net | 131.155.70.100 | /pub/linux |
| ftp.ibr.cs.tu-bs.de | 134.169.34.15 | /pub/os/linux |
| ftp.denet.dk | 129.142.6.74 | /pub/OS/linux |

表 C.1：Linux 站点

`tsx-11.mit.edu`、`sunsite.unc.edu` 和 `nic.funet.fi` 是 Linux 软件的“主站点”，大部分新软件都安装在这里。列表中大多数其他站点都是这三个者的组合。为了减少网络流量，请选择地理位置离你最近的站点。

## 附录 D

## Linux BBS 列表

此处列出了提供 Linux 软件的公告板系统（BBS）。此列表由 Zane Healy (`healyzh@holonet.net`) 维护。如果你知道或运行着某个提供 Linux 软件但未列在此列表中的 BBS，请与我们联系。

Linux 社区不再是一个仅限互联网的社会。事实上，我们估计大多数 Linux 用户没有接入互联网。因此，BBS 持续为全球用户提供并支持 Linux 显得尤为重要。

### D.1 美国

- Citrus Grove Public Access, 916-381-5822. ZyXEL 16.8/14.4 萨克拉门，加利福尼亚州。Internet: citrus.cas.ca.us

- Higher Power BBS, 408-737-7040. RIME: ->HIGHER

- hip-hop. 408-773-0768. 19.2k 桑尼维尔，加利福尼亚州。USENET 接入

- hip-hop. 408-773-0768. 38.4k 桑尼维尔，加利福尼亚州。

- Unix Online, 707-4631. 9600 佩塔卢马，加利福尼亚州。USENET 接入

- The Outer Rim, 805-252-6342. 圣克拉拉，加利福尼亚州。

- Programmer's Exchange, 818-444-3507. 埃尔蒙特，加利福尼亚州。Fidonet

- Programmer's Exchange, 818-579-9711. 埃尔蒙特，加利福尼亚州。

- Micro Oasis, 510-505-5985. 14.4k 圣莱昂德，加利福尼亚州。

- Test Engineering, 916-928-0504. 萨克拉门，加利福尼亚州。

- Club Shit, 813-925-2603. US/DS 18/14.4k 坦帕，佛罗里达州。Fidonet: 1/377

- Lost City Atlanta, 904-727-9334. 14.4k 杰克斯维尔，佛罗里达州。Fidonet

- Acquired Knowledge, 305-720-3690. 14.4k v32bis. 罗代代堡，佛罗里达州。Fidonet, UUCP

- The Computer Connection, 754-544-3545. 14.4k v32bis. 彼得堡，佛罗里达州。Fidonet, Sailor, MXBSnets

- AV, 404-420-6202. 亚特兰大，乔治亚州
