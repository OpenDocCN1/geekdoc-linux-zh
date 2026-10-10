
Pidgin 是 Linux 中主要的即时消息客户端。该项目最初基于 America Online (AOL) 的 Open IM 架构 (`www.aim.com`)，项目最近将其名称更改为 Pidgin GAIM。Pidgin 提供了多种即时消息协议，包括以下几种：

- Oscar — Oscar 是由 AOL 创建的原始 AOL 协议，是 Pidgin 使用的最常用的协议。为了在 Pidgin 中运行，必须对 Oscar 进行反向工程，因为它是 AOL 的私有协议。因此，在 AOL 自己的即时消息软件中可能找到某些功能并不被支持。消息通过基于 TCP 的网络（通常是互联网）进行，所有消息都通过 AOL 服务器传输，直接连接的情况除外（必须确保直接连接正常工作）。

- MSN Messenger — 该协议最初基于 MSN Messenger Service 1.0 协议 (`www.othetic.org/docs/msn/iet_draft.txt`)。自从微软首次发布该版本以来，该协议已经过大量的“增强”，导致 Pidgin 必须对其进行反向工程。要了解更多关于 MSN Messenger 的信息（通过 Pidgin 或其他），请查看 Messenger 协议资源/链接页面 (`www.hyphetic.org/docs/msn/resources/links.php`)。

- ICQ — Pidgin 使用开源 `icql` 库来实现 ICQ 协议。由于最近 ICQ 协议的更改，建议使用 Oscar 连接到 ICQ 网络，而不是 icq。

- IRC — 互联网中继聊天协议基于标准的 RFC 1459。尽管在不同的 IRC 服务器上对该标准的实现存在差异，但这种基于 TCP 的协议在大多数 IRC 服务器上都应该正常工作。

- Yahoo! Messenger — 这允许你使用 Yahoo! 服务器与其他通信。

Pidgin 还支持其他消息协议。这些包括 Jabber（GoogleTalk 使用，可从 `www.jabber.org` 获取）、Napster（即时消息和好友列表，但不支持下载）、Groupwise（Novell 的即时消息）、Sametime（来自 `한편.sourceforge.net` 的 Lotus 消息）、TOC（用于官方客户端常用的 AOL IM 服务）以及 Zephyr（MIT 的 IM 系统）。Pidgin 不仅支持多种协议，还允许你同时通过多种协议进行通信。还有可用的 Jabber 服务器可以让你运行自己的 Jabber 即时消息服务器，例如 Ejaberd (`http://ejaberd.jabber.ru`)。（输入 `yum install ejaberd` 安装该软件包。）

要从应用程序菜单启动 Pidgin，选择 Internet -> Instant Messenger。图 9-8 包含了 Pidgin 好友列表和其他窗口的示例。

![](img/6a8f767dda2519b458f97c2e7f586576_436_0.png)

如果你以前从未用过消息功能，请注册 AOL (`https://aol.com/`) 或 MSN (`https://msn.com/`)。一旦登录，Pidgin 窗口允许你输入想要加入的聊天名称。Pidgin 窗口上的滑块允许你控制允许他人上传你正在下载的文件时所需的带宽。你提供的带宽越多，下载文件的速度就越快。下载完成后，你仍然可以让其他人获取该文件。

要为你想要共享的文件或文件目录创建自己的种子（torrent），选择 File -> Make new torrent。虽然你始终可以在公共服务器上发布自己的种子，但你的防火墙可能会限制你向互联网发布自己种子的能力。

## 使用 BitTorrent 共享文件

BitTorrent 是一种向大量客户端分发软件的工具。BitTorrent 之所以独特，是因为当你从你的计算机下载文件时，其他人可能正在下载同一个文件。例如，当 Fedora 发布新版本时（现在包含超过 13GB），BitTorrent 意味着你不需要等待几天让服务器“降温”。同样，任何想与世界分享的人都可以这样做，无需工业级的服务器。

Fedora 存储库提供了基于文本和图形 (`bittrent-gui`) 的 BitTorrent 客户端。你可以以 root 身份从终端输入命令获取客户端：

```bash
# yum install bittrent-gui
```

要使用种子，访问提供软件下载的网站，寻找代表你想下载的软件、视频或其他类型文件的种子链接。将种子下载到你的计算机上。接下来打开 BitTorrent 窗口（选择 Applications -> Entropy -> BitTorrent File Transfer）。通过 File -> Open torrent 打开文件（寻找 `.torrent` 扩展名）。

BitTorrent 窗口上的滑块允许你控制允许他人上传你正在下载的文件时所需的带宽。你提供的带宽越多，下载文件的速度就越快。下载完成后，你仍然可以让其他人获取该文件。

## 使用远程登录、复制和执行

本节介绍了一些允许用户跨网络使用资源的功能。它们是 `telnet`、`ssh` 和 `wget` 命令。

> 引用：Fedora 默认仅开启了 ssh 服务，因为此处描述的其他远程登录、执行和命令默认情况下不提供加密通信，因此它们可能构成重大的安全风险。有关如何在如何在 Fedora 或 RHEL 服务器上开启本章描述的服务的信息，请参考第 14 章和附录 B。

## 第 9 章：使用互联网和 Web

在本节描述的两个通常可用的命令是远程登录和文件传输程序，分别是 `telnet` 和 `ftp`。访问 FTP 服务器的其他命令是 `ncpftp` 和 `gFTP`。`ssh` 命令通常被用作安全的远程登录命令，尽管它也可以用于远程执行。

两个用于通过网络复制文件的较新命令是 `wget` 和 `rsync`。这两个工具都可高效地下载你在网络上识别的文件。

### 用于远程登录的 Telnet

Telnet 是许多不同类型的计算机系统提供的服务，允许远程用户通过 TCP/IP 网络登录到它们的机器。`telnet` 命令是您用于执行远程登录的客户端程序。使用 `telnet` 的常见方法是使用主机名。以下是一个典型的 telnet 会话：

```
$ maple
Trying 10.0.0.11 ...
Connected to maple.linustoys.net 10.0.0.11
Escape character is '^]'
Fedora release 9
Kernel 6.25-0.234.fc9 on i686
login: mike
Password: ********
Last login: Mon Jun 16 13:15:57 from pine
[maplemap mike]$
```

此示例显示了当输入 `telnet maple` 从一个名为 `pine` 的计算机登录时发生的情况。我的计算机尝试连接到 `maple` 上的 telnet 端口（IP 地址 10.0.0.11）。由于 `maple` 也是一个 Fedora 系统，一旦建立连接，我就看到了标准的登录提示符。我输入用户名（mike）和提示的密码。当登录和密码被接受后，我看到了用户名提示符。

telnet 服务在 Fedora 和 RHEL 系统上默认是禁用的（大多数网络服务也是如此）。因此，为了能够使用 `telnet` 登录，请参考附录 B 获取如何开启 telnet 服务的信息。

以下是您可以在使用 `telnet` 时使用的一些有用选项：

- `-a` 自动登录。使用此选项，您的计算机将尝试使用本地用户名登录远程计算机。因此，如果你以 `mike` 的身份登录自己的计算机，当你使用 `telnet` 登录远程计算机时，远程计算机将假设你想以 `mike` 的身份登录。它只需提示你输入密码。

- `-user` 用户名。此选项与 `-a` 选项类似，不同之处是除了当前用户名，你可以请求使用你选择的任何用户名登录。

- `-r` Rlogin 风格界面。此选项允许您使用波浪 (`~`) 选项。例如，在登录模式下断开连接可以使用 `~.`（波浪+点），或者挂起 telnet 会话可以使用 `~^z`（波浪+脱字符+z）。仅当您的远程 shell 卡住时才使用 `~`（通常情况下 `exit` 是更好的方法）。如果你使用 `~` 临时挂起 telnet 会话，将返回本地系统 shell。要回到挂起的会话，请输入 `fg` 将 telnet 回到前台。

使用 `telnet` 的另一种方法是在命令模式下。不要使用主机名，只需输入 `telnet` 单词。你会看到如下 telnet 提示符：

```
$ telnet
telnet>
```

此时，您有几个命令可以使用。您尚未连接到远程主机。要从 telnet 提示符打开到远程计算机的登录会话（例如，到名为 `maple` 的计算机），输入：

```
telnet> open maple
```
