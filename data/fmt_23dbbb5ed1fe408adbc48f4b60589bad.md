
| Java 运行时环境, OpenJRE | 开源 Java 运行时环境，包括 Java 虚拟机。作为 Red Hat Enterprise Linux 6 发行版的一部分包含 `java-1.6.0-openjdk-dev` 中。 |

| Java 兼容层 | 不含 Java 的开放环境，由 GNU Java 运行时 (`libgcj`)、Eclipse Java 编译器 (`ecj`) 以及支持的包装器和链接 (`java-gc-compat`) 组成。随 RHEL6 包含。 |

| GNU Java 编译器 | GNU 公共许可 Java 编译器 (`GJC`)，用于编译 Java 程序，`http://gcc.gnu.org/`。随 RHEL6 和 `libgcj` 包含。 |

| Jakarta 项目 | 用于开源 Java 应用的 Apache 软件基金会，`http://jakarta.apache.org` |

| Classpath | GNU 许可证 Java 开库，`www.gnu.org/software/classpath` |

## 表 7-3：Java 包与 Java Web 应用

`Jakarta` 项目 (`http://jakarta.apache.org`) 是 Apache 软件基金会的一部分，提供开源 Java 工具和应用程序，包括库、服务器应用和引擎。`Jakarta` 与其他软件包一起包含在 `RHEL6` 中。

## BitTorrent (transmission)

`GNOME` 和 `KDE` 提供了非常有效的 BitTorrent 客户端。通过 BitTorrent，你可以在共享分布式操作中快速下载大文件，其中多个用户参与下载文件的不同部分，并将这些部分发送给其他下载的用户，这些用户被称为节点（peers）。与其让每个人尝试访问几个中央服务器，所有参与 BitTorrent 操作的节点都成为所下载文件的源。某些节点作为种子者（seeders），即那些已经下载了文件但继续向需要它的人发送分部分的用户。

`Red Hat Enterprise Linux` 不安装 BitTorrent 客户端。你必须手动安装一个。首先从 `EPEL` 或 `RPMforge` 存储库安装支持的库，`torrent` 包提供了两个命令行 BitTorrent 应用：`ctorrent` 和 `rtorrent`。

`RHEL6` 没有桌面版 BitTorrent 应用，尽管你可以安装 Fedora 12 版本的 `GNOME` BitTorrent `Transmission`。Fedora 12 使用兼容 `x86_64` 和 `RHEL 6` 的 `GNOME` 版本。以下链接可以访问 32 位版本的 Fedora 12 包（使用 `i386` 代替 `i64` 位）。

`http://download.redhat.com/pub/fedora/linux/releases/12/Fedora/i386/os/Pkgs/`

然后你可以下载并安装 `transmission` 包。

# 第二部分：应用程序

`transmission-1.76-1.fc12.i686.rpm`

你可以通过 `Transmission` 应用 | `Internet` | `Transmission BitTorrent` 客户端 访问 `transmission`。对于 `KDE`，你可以使用 `KTorrent BitTorrent` 客户端。要执行 BitTorrent 下载，你需要下载文件对应的 BitTorrent 客户端。例如，Fedora ISO 镜像的 BitTorrent 客户端是 `Fedora-i686-DVD.torrent`（见图 7-7）。

![](img/99301381a0d2790a6cdc2798147cbdad_217_0.png)

图 7-7：Transmission BitTorrent 客户端

`Transmission` 可以同时处理多个 `torrent`。工具栏有启动、暂停和删除下载的按钮。`Add`（添加）按钮可加载 BitTorrent 文件 (`.torrent`) 并设置下载。你也可以将 `torrent` 文件拖入 `Transmission` 窗口。当你打开一个 `torrent` 文件时，会打开 `Torrent Options`（选项）窗口，可以在其中指定目标文件夹和优先级。默认选中自动启动下载的选项。

你可以设置 `Transmission` 来管理多个 BitTorrent 操作，其中只有少数可能是激活状态，其他以及已完成但继续作为种子者运行的操作。从第一个下拉菜单中，你可以选择所有（`All`）、激活（`Active`）、下载中（`Downloading`）、种子中（`Seeding`）、暂停（`Paused`）、完成（`Finished`）和队列中（`Queued`）的 `torrent`。你还可以选择正在验证的和错误的 `torrent`。从第二个菜单中，你可以选择跟踪器（`Trackers`）、公共或私有 `torrent`（隐私），并按优先级（高、中、低）进行选择。

要移除 `torrent`，右键点击它并选择 `Remove`（移除）。选择 `Delete Files and Remove`（删除文件并移除）以移除你目前为止下载的内容。

要查看有关 `torrent` 的更多信息，选择它并点击 `Properties`（属性）按钮（见图 7-8）。这将打开一个属性窗口，带有 `Information`（信息）、`Peers`（节点）、`Tracker`（跟踪器）、`Files`（文件）和 `Options`（选项）标签。在 `Information` 标签中，`Activity` 部分显示进度、时间和错误等统计，`Details` 部分显示下载文件夹的来源、内容和位置。`Peers` 显示所有参与下载的节点。`Tracker` 显示跟踪器的位置，即管理 `torrent` 操作的服务器。`Files` 显示文件下载进度（一个 `torrent` 可以下载多个文件）。`Options` 标签允许设置带宽和连接参数，限制下载或上传以及节点数量。

![](img/99301381a0d2790a6cdc2798147cbdad_218_0.png)

图 7-8：Transmission BitTorrent 客户端

### BitTorrent 客户端

BitTorrent 客户端是用于使用 BitTorrent 协议下载文件的程序。在该协议中，文件被分成许多小块，并从多个节点同时下载。这允许加快下载并减轻中央服务器的负载。

针对不同的操作系统，有许多 BitTorrent 客户端可用。最流行的包括：

- `transmission`：一个适用于多个平台的轻量级快速的 BitTorrent 客户端。
- `qBittorrent`：一个开源 BitTorrent 客户端。
- `uTorrent`：适用于 Windows 的流行 BitTorrent 客户端。
- `BitTorrent`：适用于 Windows、Linux 和 macOS 的原始 BitTorrent 客户端。

要使用 BitTorrent 客户端，你需要一个 `.torrent` 文件，它包含了要下载的文件的信息。这些文件可以在各种网站上找到或通过磁力链接共享。一旦有了 `.torrent` 文件，用你的 BitTorrent 客户端打开它，它将开始下载文件。

# 第 7 章：互联网应用程序 219

![](img/99301381a0d2790a6cdc2798147cbdad_220_0.png)

# 图 7-9：使用“连接服务器”和文件管理器访问 GNOME FTP

远程 FTP 站点的根文件夹将显示在文件管理器。使用文件管理器浏览远程 FTP 站点的目录树，直到找到你想要的文件。然后，打开另一个窗口，显示你想要将远程文件复制到的本地文件夹。在显示 FTP 文件的窗口中，选择你想要下载的文件。然后点击并拖动这些文件到本地文件夹的窗口中。在文件下载时，会弹出一个对话框显示进度。

文件管理器的“位置”（Places）侧边栏将列出已访问的 FTP 站点项目。FTP 名称右侧会显示一个弹出按钮。要断开站点连接，点击此按钮。FTP 条目将随着 FTP 站点的图标和列表一起消失。

# KDE 文件管理器：Conqueror 和 Dolphin

在 `KDE` 桌面，桌面文件管理器（`Conqueror` 和 `Dolphin`）内置了 FTP 功能。FTP 操作已无缝集成到标准的桌面操作中。从 FTP 站点下载文件就像将文件从一个文件夹拖动到另一个文件夹一样简单，其中一个文件夹位于远程站点。在 `KDE` 上，你可以使用文件管理器窗口访问远程 FTP 站点。远程文件夹中的文件列出方式与你的本地文件完全相同。要从 FTP 站点下载文件，你只需打开一个窗口来访问该站点，在窗口的位置地址框中输入 FTP 站点的地址。使用 `ftp://` 协议进行 FTP 访问。连接后，打开文件夹，然后打开另一个窗口显示你想要将远程文件复制到的本地文件夹。在显示 FTP 文件的窗口中，选择你想要下载的文件。点击并拖动文件到本地文件夹窗口。会弹出菜单，提供“复制”、“链接”或“移动”选项。选择“复制”。选中的文件将被下载。随后会打开另一个窗口，显示下载进度并依次显示每个文件名，并有一个进度条指示到目前下载的百分比。

### Filezilla
