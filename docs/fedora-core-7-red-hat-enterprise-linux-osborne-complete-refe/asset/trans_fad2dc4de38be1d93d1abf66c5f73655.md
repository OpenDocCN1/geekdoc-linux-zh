
## BitTorrent 客户端与使用方法
您需要使用 BitTorrent 客户端。您可以选择多种 BitTorrent 客户端，例如 **azureus、rtorrent、ctorrent、ktorrent**，以及原始的 BitTorrent。这些软件包均可在 Fedora 仓库中获取。对于原始 BitTorrent，有两个软件包：**bittorrent** 和 **bittorrent-gui**，后者提供 GNOME 界面。原始 BitTorrent 网站现在是一个商业网站，用于下载需要 Windows Media Player 和数字版权管理（DRM）的电影。

要开始一个 torrent，只需在 Web 浏览器中点击该文件对应的 torrent 条目即可。Firefox 会提示您是直接启动应用程序还是下载文件。您可以运行该应用程序，BitTorrent 客户端将随之启动，下载随即开始。您可以随时暂停，并稍后重新启动 torrent。它将从您上次中断的地方自动恢复，保留已下载的内容。例如，若要开始 Fedora DVD torrent 以下载 DVD 镜像，请点击 **torrent.fedoraproject.org** 网页上的 DVD torrent 条目。BitTorrent 客户端会自动调整到合适的下载/上传速率，但您也可以根据需求自行调整。界面上有用于暂停和停止下载的按钮，以及查看 torrent 详细信息的选项。状态栏显示进度和预计剩余时间，不过随着下载进行，预计时间可能会缩短。客户端将显示所有正在进行中的 torrent，标出每个 torrent 已下载的比例，并允许您选择希望激活哪个。配置项允许您调整行为，例如使用哪个端口、默认下载目录，以及是否允许并行运行多个 torrent。

从 **torrent.fedoraproject.org** 下载的文件并不是 ISO 或 DVD 镜像文件。BitTorrent 将负责下载实际文件。相反，这是一个简单、小巧的 BitTorrent 文件，其中包含访问和启动该特定 torrent 的信息。您可以下载 torrent 文件，稍后通过启动它来开始 torrent 下载。您可以维护一组 torrent 文件，并按需启动或停止。您的磁盘上将会有一个类型为 **.torrent** 的小型 torrent 文件。双击它以启动 BitTorrent 客户端并开始下载 Fedora 二进制 ISO 镜像。

您可以使用 BitTorrent 下载任何能找到对应 torrent 文件的资源。但下载速度具有时间敏感性，这取决于参与该 torrent 的用户数量。Linux 发行版的 torrent 通常维护良好，有多名用户提供持续的上传支持，这些用户被称为种子（seeds）。而其他 torrent 可能会消亡，如果没有其他用户参与的话。下载速度直接取决于参与该 torrent 的用户数量。因此，torrent 更适合时间敏感性强的场景，例如当某个 Linux 发行版发布新版本时。

> **注意：** BitTorrent 软件包还提供了创建自己的 torrent 以分发文件的工具。目前有两种分发方式：基于 tracker 和基于 trackerless。Trackerless 方式无需服务器支持。

## 使用 yum 和 PUP 进行更新
您可以使用包含 Fedora 软件的 Yum（Yellowdog Update, Modified）仓库来更新软件。Yum 使用 RPM 头信息来确定哪些软件包需要更新。您可以访问 **linux.duke.edu/projects/yum** 获取有关 Yum 的更多信息。

### PUP
在 Fedora 上更新软件包时，您可以使用软件包更新程序（PUP）。之前使用的 RHN 更新工具已不再随 Fedora 提供（该工具曾用于 Red Hat Enterprise Linux）。PUP 是 Yum 的图形化更新界面，现在负责执行所有更新。

PUP 具有更新通知小工具，它会自动检测是否有可用更新，并在您登录时通知您。通知将显示在面板上，标示更新的数量（打开的软件包图标）。点击该通知将启动 PUP。您也可以选择不理会该通知，甚至退出小工具。您还可以通过手动运行 PUP 来进行更新。在“应用程序 | 系统工具”菜单中，您可以找到带有软件包（打开的盒子）图标的“软件更新器”（Software Updater）条目。

PUP 启动后，将列出所有需要更新的软件包。默认情况下，所有软件包均会被自动选中。每个条目旁边的复选框允许您取消选择那些不想更新的特定软件包。点击“应用”按钮开始更新。系统会先检查依赖关系。然后，软件包将从其对应的仓库下载。下载完成后，软件包将得到更新。系统中配置的所有与 Yum 兼容的仓库都会被检查。现在，软件被视为分布在不同在线仓库上的集合，而非特定的磁盘介质。

### 使用 yum 命令更新
作为替代方案，您可以使用带有 **update** 选项的 **yum** 命令进行更新。以下命令用于更新已安装的 **gnumeric** 软件包：

```
yum update gnumeric
```

您可以使用 `check-update` 选项来查看哪些软件包需要更新。

```
yum check-update
```

要执行对所有已安装软件包的全量更新，只需使用 **update** 选项即可。这与通过 PUP 进行更新的效果相同。

```
yum update
```

### 自动 Yum 更新
Yum 还会在 `/etc/cron.daily` 目录中安装一个 `yum.cron` 文件，它将自动更新您的系统。该 cron 条目会先根据需要在必要时更新 Yum 软件本身，然后继续下载并安装已安装软件包的更新。它运行带有 **update** 选项的 **yum**。

只有当系统在 `/var/lock/subsys` 目录中检测到 Yum 锁定文件时，自动更新才会运行。默认情况下，该文件是不存在的。您可以使用 **yum** 服务脚本添加该文件。**start** 选项创建锁定文件，从而启用由 cron 支持的更新；而 **stop** 选项则删除该文件，从而禁用自动更新。

```
service yum start
```

## 使用 yum 命令安装 Fedora 软件包
您可以使用 **yum** 命令直接访问 Yum 仓库以下载新软件。Fedora 仓库已配置好供 Yum 使用。要下载任何 Fedora 软件包，您可以使用 Pirut 软件包管理器，或使用带有 **install** 选项的 **yum** 命令行。Pirut 软件包管理器（在应用程序菜单中作为“添加/移除软件”访问）是 Yum 的 GNOME 前端。该软件包管理器基于互联网，仅从在线仓库安装，使用 Yum 进行下载和安装。作为 Pirut 的替代方案，您可以使用 **yumex**（Yum 扩展器），它也提供桌面界面。Pirut 软件包管理器和 **yumex** 在第四章中有详细描述。

> **提示：** 要使用 Pirut 移除软件包，只需取消勾选该条目，然后点击“应用”。所有已安装的软件包默认都是被勾选的。

要使用 **yum** 命令，请在命令行上输入带有 **install** 选项的 **yum** 命令（在桌面上，请先右键点击并打开一个终端窗口）。系统将检测到该软件包及其所有依赖软件，并提示您确认安装。下载和安装将是自动进行的。您可以在线检查下载仓库，以及 repodata 目录，以在网页上显示可用软件包。该页面将包含基于软件包名称首字母的易用功能，如软件包组和索引链接。

以下示例安装了 Xine 视频播放器：

```
yum install xine
```

您还可以移除软件包，以及根据不同的标准搜索和列出软件包，例如需要更新的软件包、仓库中尚未安装的软件包，以及已安装的软件包。以下示例列出所有已安装的软件包：

```
yum list installed
```

available 选项显示未安装的软件包。

```
yum list available
```

要搜索特定的软件包，您可以使用 search 选项。

```
yum search xine
```

> **提示：** 您可以像使用 freshrpms.net 和 rpm.livna.org 这样的 Fedora Yum 软件仓库来下载额外的软件。它们的配置文件将位于 /etc/yum.repos.d。freshrpms.repo 和 livna.repo 文件将被安装在 /etc/yum.repos.d。

## Yum 配置
Yum 选项在 /etc/yum.conf 文件中配置，而 /etc/yum.repos.d 目录则存放列出可访问 Yum 仓库的仓库（repo）文件。仓库文件的扩展名为 .repo。请查阅 **yum.conf** 的 Man 页以获取不同 Yum 选项的列表。

