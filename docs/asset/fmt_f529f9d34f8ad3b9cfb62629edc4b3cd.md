
命令 `get`（下载）和 `put`（上传）是相对于你的主机器而言的。你是告诉你的系统从远程位置获取文件并将其放到本地机器上，或者将本地机器上的文件放到远程机器上。这与另一种常用的 TCP/IP 协议 `Telnet` 相反，`Telnet` 中一切都是相对于远程机器而言的。记住哪个命令朝哪个方向移动很重要，否则你可能会意外覆盖文件。

在大多数 `FTP` 版本中，文件名周围的引号是可选的，但它们向远程版本提供了特定字符（防止 shell 扩展），因此建议使用引号以避免错误。`FTP` 提供两种文件传输模式：`ASCII` 和二进制。一些系统会自动在这两者之间切换，但手动设置模式是一个好主意，以确保你不浪费时间。要将 `FTP` 设置为二进制传输模式（用于任何可执行文件），输入命令 `binary`。

你可以使用命令 `ASCII` 切换回 `ASCII` 模式。由于你很可能正在检查远程站点是否有新的二进制文件或源代码库，对于大多数传输使用二进制模式是一个好主意。如果你以 `ASCII` 模式传输二进制文件，它在你的系统上不可执行（或不可理解）。`ASCII` 模式仅包含有效的 `ASCII` 字符，而不包含二进制文件内部使用的 `Ctrl+` 键序列。以二进制模式传输 `ASCII` 文件不会影响其内容，尽管杂波噪声在极少情况下可能会引起问题。

当你发出 `get` 命令时，远程系统会将数据传输到你的本地机器，并在完成后显示状态消息。在传输大文件时没有进度指示，所以要耐心一点。

```
FTP> get "file1.txt"
200 PORT command successful.
150 BINARY data connection for FILE1.TXT (27534 bytes)
226 BINARY Transfer complete.
27534 bytes received in 2.35 seconds (12 Kbytes/s).
```

要退出 `FTP`，输入命令 `quit` 或 `exit`。其中任何一个都会关闭你在远程机器上的会话，然后终止你本地机器上的 `FTP`。

### 使用 `ftpmail`

如果你无法通过 `FTP` 访问远程站点，情况并未完全糟糕。如果你有电子邮件，你仍然可以接收文件传输。一些在线系统允许发送和接收互联网邮件，但不允许直接访问 `FTP`。类似地，一些互联网服务提供商提供 `UUCP` 账户，不允许直接连接但提供电子邮件。要访问 `FTP` 站点并传输文件，你可以使用 `ftpmail` 工具。

前文提到的站点 `sunsite.unc.edu` 是一个主要的 Linux 归档站点，支持 `ftpmail`。（本附录中列出的所有 Linux `FTP` 站点也支持 `ftpmail`。）要了解如何使用 `ftpmail`，向其中一个站点的登录名 `ftpmail` 发送电子邮件消息，例如 `ftpmail@sunsite.unc.edu`，并且消息正文只包含一个单词：`help`。

通过回信，`ftpmail` 工具将发送使用该服务的说明。基本上，你在邮件消息中发送你想要执行的 `FTP` 命令的正文，因此你可以通过以下文本在邮件消息中获取 Linux 目录的目录列表：

```
open sunsite.unc.edu
cd /pub/Linux
ls
quit
```

你可以使用类似的邮件消息通过电子邮件传输文件回来：

```
open sunsite.unc.edu
cd /pub/Linux
binary
get README
quit
```

`FTP` 邮件系统相对缓慢，因为您需要等待电子邮件到达目标机器并经过远程处理，然后再等待回复邮件返回给您。尽管如此，它为没有 `FTP` 连接的提供了一个有用的访问方法，并且是检查几台机器上 Linux 目录内容相对简单的方式。

## Linux `FTP` 存档站点

Linux `FTP` 存档站点的列表变化缓慢，但本书付印时表 A.1 中列出的站点均有效且可访问。其中许多站点是镜像站点，提供完全相同的内容。

要找到离您最近的站点，请使用站点名称末尾的国家标识符（`uk`=英国，`fr`=法国，以此类推）。大多数 `FTP` 版本允许使用机器名称或 `IP` 地址，但如果本地互联网网关无法解析该名称，`IP` 地址是最好的寻址方式。

### 表 A.1. LINUX `FTP` 存档站点。

| **站点名称** | **IP 地址** | **目录** |
| :--- | :--- | :--- |
| `tsx-11.mit.edu` | 18.172.1.2 | `/pub/linux` |
| `sunsite.unc.edu` | 152.2.22.81 | `/pub/linux` |
| `nic.funet.fi` | 128.214.6.100 | `/pub/OS/linux` |
| `ftp.mcc.ac.uk` | 130.88.200.7 | `/pub/linux` |
| `ftp.df.v.rwth-aachen.de` | 137.226.4.111 | `/pub/linux` |
| `ftp.informatik.rwth-aachen.de` | 137.226.255.3 | `/pub/linux` |
| `ftp.ibp.fr` | 132.227.60.2 | `/pub/linux` |
| `ftp.uu.net` | 192.48.96.9 | `/systems/unix/linux` |
| `wuarchive.wustl.edu` | 128.252.135.4 | `/systems/linux` |
| `ftp.win.tue.nl` | 131.155.70.19 | `/pub/linux` |
| `ftp.stack.urc.tue.nl` | 131.155.140.128 | `/pub/linux` |
| `ftp.ibr.cs.tu-bs.de` | 134.169.34.15 | `/pub/linux` |
| `ftp.denet.dk` | 129.142.6.74 | `/pub/OS/linux` |

Linux 存档的主要主站点是 `tsx-11.mit.edu`、`sunsite.unc.edu` 和 `nic.funet.fi`。主站点是大多数新软件加载开始的地方。表 A.1 中的大多数站点都是这三个站点之一的镜像。

# 公告板

全世界有数百个提供 Linux 软件的电子公告板系统（`BBS`）。一些定期从 `FTP` 主站点下载新版本，而另一些则依赖 `BBS` 用户来更新软件。

一份完整的提供 Linux 软件的 `BBS` 列表过于冗长（而且几乎会立即过时），无法在此收录。Zane Healy 维护着一份完整的提供 Linux 材料的 `BBS` 列表。要获取该列表，请发送电子邮件至 `healyzh@holonet.net` 请求 Linux 列表。

如果您无法访问电子邮件，请尝试在几个本地公告板系统上发布信息，询问提供 Linux 软件的本地站点，或者请有互联网访问的人为您发送电子邮件。

# 与 Linux 相关的 `BBS`

Zane Healy（`healyzh@holonet.net`）维护此列表。如果您知道或运营一个提供 Linux 软件但未在此列出的 `BBS`，您应与 lui（他）取得联系。

您还可以从 `tsx-11.mit.edu` 的 `/pub/linux/docs/bbs.list` 文件中获取最新的 `BBS` 列表。下面显示的列表在付印时是最新的。

# 美国 `BBS`

以下是美国提供一些包含 Linux 或 Linux 信息的 `BBS` 列表：

- 1 Zero Cybernet `BBS`，(301) 589-4064。MD（马里兰州）。
- AVSync，404-320-6202。Atlanta, GA（佐治亚州亚特兰大）。
- Allentown Technical，(215) 432-5699。9600 v.32/v.42bis Allentown, PA（宾夕法尼亚州艾伦镇）。`WWIVNet` 2578
- Acquired Knowledge，(305) 720-3669。14.4k v.32bis Ft. Lauderdale, FL（佛罗里达州劳德代尔堡）。Internet, `UUCP`
- Atlanta Radio Club，(404) 850-0546。9600 Atlanta, GA（佐治亚州亚特兰大）。
- Broadmann's Place，(301) 843-5732。14.4k Waldorf, MD（马里兰州沃尔多夫）。`RIME` ->BROMANN, `Fidonet`
- Centre Programmers Unit，(814) 353-0566。14.4k V.32bis/HST Bellefonte, PA（宾夕法尼亚州贝尔丰特）。
- Channel One，(617) 354-8873。Boston, MA（马萨诸塞州波士顿）。`RIME` ->CHANNEL
- Citrus Grove Public Access，(916) 381-5822。ZyXEL 16.8/14.4 Sacramento, CA（加利福尼亚州萨克拉门托）。
- CyberVille，(817) 249-6261。9600 TX（德克萨斯州）。`Fidonet` 1:130/78
