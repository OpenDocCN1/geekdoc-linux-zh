
http://fedoraproject.org/get-fedora

你可以通过输入以下 URL 直接访问 Fedora 镜像站点。然后你需要通过 `releases` 和 `8` 目录找到存放 Fedora 安装和 Live 镜像的目录。

`download.fedoraproject.org`

你也可以通过以下 URL 访问镜像。这里将列出当前的 Fedora 镜像及其地址。

`mirrors.fedoraproject.org`

在以下 URL 可以找到所有 Fedora 下载选项的详细说明，包括你需要的所有 ISO 光盘镜像以及镜像站链接。请访问此网站以获取最新的下载步骤。
`http://fedoraproject.org/wiki/Distribution/Download`

或者，你仍然可以使用 `download.fedora.redhat.com` 上的链接直接从 Fedora 网站下载。该网站不包含 DVD 版本，只有 CD 和软件包文件。
`down.fedora.redhat.com/pub/fedora/linux/releases/`

使用宽带 DSL 或电缆，直接下载可以非常快，可以使用像 `gFTP`（应用程序 | 互联网菜单）这样的 FTP 客户端。使用 `Firefox` 等浏览器进行网页客户端下载速度会较慢。

## 安装 DVD 和 Live 镜像

要从 DVD/CD-ROM 驱动器下载 Fedora 9，你需要下载安装 DVD 镜像或 Fedora Live 镜像。Fedora 安装和 Live 镜像是扩展名为 `.iso` 的大文件。Fedora 安装 DVD 位于 Fedora 子目录下的相应版本（i386, x86, 64 或 PPC）目录中（`Fedora/i386/iso`）。Live 镜像位于 Live 子目录下的相应版本（i686, x86, 64 和 i64）。下载完成后，你可以使用 CD 或 DVD 刻录机和刻录软件（如 Fedora `Nautilus` 浏览器或 `K3b`）将其刻录到光盘上。

提供了支持 64 位系统和标准 x86 (32 位) 支持的 ISO 镜像。请下载对应的一个。你不能在 x86 (32 位) 系统上运行 64 位版本。

你不需要将镜像下载到 Linux 系统。你同样可以在 Windows 系统上下载它们，并使用 Windows CD/DVD 刻录机制作光盘。

## 使用 Jigdo

你可以使用任何 FTP 或 Web 客户端（例如 `gFTP` 或 `Firefox`）下载 CD 镜像文件。然而，DVD 镜像是一个大文件，可能需要很长时间下载，特别是 FTP 站点非常繁忙或你的互联网连接缓慢时。此类超大文件的替代方案是使用 BitTorrent。BitTorrent 是一种安全的分布式下载操作，非常适合大文件，允许许多参与者下载和上传同一个文件，构建一个对所有参与者都能运行非常快的 torrent。Fedora 9 的 BitTorrent 文件同时位于 `fedoraproject.org` 和

## 使用 BitTorrent

你可以使用任何 FTP 或 Web 客户端（例如 `gFTP` 或 `Firefox`）下载 CD 镜像文件。然而，DVD 文件是一个大文件，可能需要很长时间下载，特别是 FTP 站点非常繁忙或你的互联网连接缓慢时。此类超大文件的替代方案是使用 BitTorrent。BitTorrent 是一种安全的分布式下载操作，非常适合大文件，允许许多参与者下载和上传同一个文件，构建一个对所有参与者都能运行非常快的 torrent。Fedora 9 的 BitTorrent 文件同时位于 `fedoraproject.org` 和

`http://torrent.fedoraproject.org/`

你首先需要安装 BitTorrent 客户端。对于 Fedora，有多个 BitTorrent 客户端可用，包括 `azureus`、`rttorrent`、`ktorrent` 和原始的 `bittorrent`。在“添加/删除软件”中搜索“bittorrent”将显示它们（注意 `bittorrent` 的拼写中有两个‘t’ 和两个‘r’）。只需安装你需要的即可。

## Fedora Live 镜像

Fedora 提供了 Live CD，你可以通过 CD-ROM 驱动器运行 Fedora。Fedora 提供了官方和自定义的版本（spins）。Live CD 镜像可以在 `fedoraproject.org/get-fedora` 页面的 LiveCD 部分获取。Fedora 提供了 GNOME 和 KDE 桌面官方 Live CD 版本。

- `Fedora Live:` 适用于 i686、`x86_64` 和 i64。包含 Gnome 桌面和生产应用程序。i686 是 Live CD，`x86_64` 和 i64 是 DVD。
- `Fedora KDE Live:` 适用于 i686 和 `x86_64`。包含 KDE 桌面。i686 版本是 CD，`x86_64` 是 DVD。

## Fedora Spins

特殊兴趣小组还提供自定义版本，请见 `fedoraproject.org/wiki/Spins`。这些可以从 Fedora Project Tracker 页面下载，该页面列出了内容：

- `Fedora Developer Spin (开发者版):` 仅限 i686。包含带有 Eclipse 等应用程序的 GNOME 桌面，以及调试、分析工具和文档。
- `Fedora Electronic Lab (电子实验室版):` i386 为 CD。为设计设计和真的工程师设计。
- `Fedora Games Spin (游戏版):` 目前为 Live DVD。为游戏玩家配置的 Fedora，包含游戏集。
- `Fedora Xfce Spin:` 使用 Xfce 桌面。

## USB 磁盘

你可以将 Live 镜像安装到 USB 磁盘。磁盘上的原始数据将被保留。下载 `livecd-tools` 软件包，然后使用 `livecd-to-disk` 命令安装镜像。使用 Live 镜像和设备名称作为 USB 磁盘参数。如果你希望能够在 USB Live 版本上保存对 Fedora 系统的更改，请以兆字节为单位设置覆盖内存（overlay memory）。确保你的 USB 驱动足够大，能够容纳覆盖层和 CD 镜像。以下允许 512 MB 的持久数据：

```
livecd-iso-to-disk --overlay-size 512 /dev/sdX i686.iso
```
