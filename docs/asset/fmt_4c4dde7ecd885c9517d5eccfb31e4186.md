
当您选择了要添加的软件包组和软件包，并取消了要移除的选项后，点击包管理器窗口右下角的`应用`（图 13-1）。`pirut`实用程序在执行过程中会显示进度消息，并在完成软件包的安装和移除时要求您点击确定。

## BiTTorrent

下载 BiTTorrent 文件最简单的方法是在 Firefox 等网络浏览器或 Nautilus 文件浏览器中点击 torrent 文件对象。如果系统安装了 `transmission` (`transmissionbt.com`) 等图形客户端，经过确认后，浏览器将使用该客户端自动开始下载。本节介绍 BiTTorrent 的工作原理，并解释如何通过命令行下载 BiTTorrent 文件。

BiTTorrent 协议实现了一种混合的客户机/服务器和 P2P（第 1097 页）文件传输机制。BiTTorrent 高效地分发大量的静态数据，例如 Fedora 安装 ISO 镜像。它可以替代匿名 FTP 等协议，因为 BiTTorrent 不需要客户机认证。每个下载文件的 BiTTorrent 客户机都提供额外的带宽用于上传文件，从而减轻了初始源的负载。通常，BiTTorrent 下载速度比 FTP 下载更快。与 FTP 等协议不同，BiTTorrent 将多个文件组合成一个单一的包——即一个 BiTTorrent 文件。

与其他 P2P 系统一样，BiTTorrent 不使用专用服务器。相反，服务器的功能由追踪器、对等节点和种子执行。追踪器是一个允许客户机相互通信的服务器。每个客户机——在下载了 BiTTorrent 文件的一部分时称为对等节点，在下载完整个 BitTorrent 文件后称为种子——充当 BitTorrent 文件的额外来源。对等节点和种子统称为`群`。与 P2P 网络一样，群中的成员会向其他客户机上传其已下载的 BitTorrent 文件片段。种子没有什么特别之处：一旦 torrent 可以从其他种子下载，它随时可以被移除。

- 追踪器、对等节点、种子和群

### 该 torrent

下载 BitTorrent 文件的第一步是定位或获取`torrent`，即文件名扩展名为`.torrent`的文件。Torrent 包含有关待下载的 BitTorrent 文件的有用信息（元数据），如其大小和追踪器的位置。您可以通过访问其 URL 获取 torrent，也可以通过网络、电子邮件附件或其他手段获取。然后，BitTorrent 客户机可以连接到追踪器，以了解它可以从中下载 BitTorrent 文件的群的其他成员的位置。

### 礼仪

一旦您下载了 BitTorrent 文件（本地系统已成为种子），良好的礼仪是让本地的 BitTorrent 客户机继续运行，以便对等节点（尚未下载完整 BitTorrent 文件的客户机）能够上传`至少`与您下载量相当的信息。

### 先决条件

如有必要，使用`yum`（第 500 页）安装`bittorrent`软件包。安装此软件包后，`apropos bittorrent`命令将显示 BitTorrent 实用程序的列表。有关更多信息，请参见`/usr/share/doc/bittorrent*`。

由于 BitTorrent 实用程序是用 Python 编写的，并且可以在任何具有 Python 解释器的平台上运行，因此它们不依赖于系统架构。Python 安装在`/usr/bin/python`，并包含在`python`软件包中。

## 使用 BITTORRENT

`bittorrent-curses`实用程序是一个文本 BitTorrent 客户机，提供伪图形界面。一旦您拥有 torrent，请执行如下的命令，用您想要下载的 torrent 名称替换示例中的 Fedora torrent 名称：

```
$ bittorrent-curses Fedora-12-i386-DVD.torrent
```

在上面的命令中，torrent 指定 BitTorrent 文件将保存在工作目录中名为`Fedora-12-i386-DVD`的目录中。BitTorrent 文件或目录的名称并不总是与 torrent 的名称相同。图 13-3 显示了 `bittorrent-curses` 的运行状态。根据互联网连接速度和种子数量，下载大型 BitTorrent 文件可能需要从几小时到几天不等。

您可以通过按`q`或`CONTROL-C`中止下载。当您再次将相同的 torrent 下载到相同位置时，下载将从中断处自动恢复。

![](img/f28adb66a7398a382f0505e0ba74a872_549_0.png)

图 13-3 `bittorrent-curses` 正在处理 Fedora DVD torrent

## 确保您有足够的空间来下载 torrent

某些 torrent 体积巨大。请确保您正在工作的分区有足够的空间来容纳您要下载的 BitTorrent 文件。

`bittorrent-curses` 最有用的选项之一是 `-max_upload_rate`，它限制了群在从您这里下载 torrent 时可以使用的带宽量。默认值为 0，意味着上传带宽没有限制。以下命令可以防止 BitTorrent 使用超过每秒 10 千字节的上行带宽：

```
$ bittorrent-curses --max_upload_rate 10 Fedora-12-i386-DVD.torrent
```

BitTorrent 通常允许上传更多数据的群成员拥有更高的下载速度，因此如果您有闲置带宽，增加此值对您是有利的。然而，您需要留出足够的空闲上行带宽，以确保您的下载的确认数据包能够通过，否则下载速度会非常慢。默认情况下，`bittorrent-curses` 一次最多向七个其他客户机上传。您可以使用 `-max_uploads` 参数更改此数字，后面跟随您希望允许的同时上传数量。如果您通过调制解调器下载，请尝试将 `-max_upload_rate` 设置为 3，将 `-max_uploads` 设置为 2。

BitTorrent 保存文件或文件的文件名或目录名由 torrent 指定。您可以使用 `-saves` 选项指定不同的文件名或目录名。`torrentinfo-console` 实用程序显示 BitTorrent 文件的保存名称、文件大小、torrent（元信息文件）名称及其他信息：

```
$ torrentinfo-console Fedora-12-i386-DVD.torrent
torrentinfo-console 4.4.0 - decode BitTorrent metaInfo files

metaInfo file..... : Fedora-12-i386-DVD.torrent
info hash......... : 9aae97762980179119dbbdfefc1f8de0356f675f3
directory name.... : Fedora-12-i386-DVD
files........... :
				Fedora-12-i386-CHECKSUM (1511)
				Fedora-12-i386-DVD.iso (3204427776)
archive size....... : 3204429287 (12223 × 262144 + 243175)
tracker announce url: http://torrent.fedoraproject.org:6969/announce
comment......... :
```

## RPM：红帽软件包管理器

`rpm`（Red Hat Package Manager，红帽软件包管理器）实用程序仅适用于为 `rpm` 处理而构建的软件包；它用于安装、卸载、升级、查询和验证 `rpm` 软件包。由于红帽将 `rpm` 以 GPL 许可发布（第 4 页），许多不同的发行版都使用 `rpm`。此实用程序会跟踪软件包的安装位置、已安装软件包的版本以及软件包之间的依赖关系。

`rpm` 源软件包通常位于名为 `SRPMS`（source rpms，源 rpm 软件包）的目录中，而二进制 `rpm` 软件包通常位于 `Packages` 中。下载二进制软件包时，请确保它们适用于本地操作系统（包括发行版和版本——例如 Fedora 12）。$^1$ 它们还应针对相应的体系结构进行编译：

- `i386` 涵盖所有基于 Intel 的大多数 AMD 系统。
- `i586` 涵盖 Pentium 级或更高处理器。
- `i686` 指 Pentium II 或更好的处理器，并包含 MMX 扩展。
- `S390x` 用于 IBM System/390。
- `ia64` 用于 Intel 64 位 Intel Itanium（与 x86_64 不兼容）。
- `alpha` 用于 DEC/Compaq Alpha 芯片。
- `ppc` 和 `ppc64` 分别指代 Power PC 32 位和 64 位处理器。
- `x86_64` 用于 Intel 和 AMD 64 位处理器（非 Itanium）。
