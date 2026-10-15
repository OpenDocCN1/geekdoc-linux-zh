
# 使用 Wine 运行 Windows 应用程序

## 资源链接

- `http://opensuse-community.org/Package_Sources/Packman`—Packman 软件仓库的镜像列表，多媒体软件的极佳来源。
- `http://download.videolan.org`—下载 VideoLAN 播放器（以及允许你在 Linux 上播放 DVD 的 libvdcsst）。
- `http://www.softwarereview.org/cms/content/view/60/`—Jem Matzen 的“破解 openSUSE 2.0”文章，有助于在默认的 OPENSUSE 设置中添加 MP3 和其他多媒体支持。
- `http://KDE-Apps.org`—为 KDE 编写的应用程序社区目录。其中，你可以选择 KonvenientSUSE 包来为你的 openSUSE 系统添加多媒体支持。
- `http://www.cdmedia.com/audio.html`—音频格式常见问题解答，有助于学习各种音频格式。
- `http://opensuse-community.org/Package_Sources/Packman`—Packman 软件仓库的镜像列表，多媒体软件的极佳来源。
- `http://download.videolan.org`—下载 VideoLAN 播放器（以及允许你在 Linux 上播放 DVD 的 libvdcsst）。
- `http://www.softwarereview.org/cms/content/view/60/`—Jem Matzen 的“破解 openSUSE 2.0”文章，有助于在默认的 OPENSUSE 设置中添加 MP3 和其他多媒体支持。
- `http://KDE-Apps.org`—为 KDE 编写的应用程序社区目录。其中，你可以选择 KonvenientSUSE 包来为你的 openSUSE 系统添加多媒体支持。
- `http://www.cdmedia.com/audio.html`—音频格式常见问题解答，有助于学习各种音频格式。
- `http://opensuse-community.org/Package_Sources/Packman`—Packman 软件仓库的镜像列表，多媒体软件的极佳来源。
- `http://download.videolan.org`—下载 VideoLAN 播放器（以及允许你在 Linux 上播放 DVD 的 libvdcsst）。
- `http://www.softwarereview.org/cms/content/view/60/`—Jem Matzen 的“破解 openSUSE 2.0”文章，有助于在默认的 OPENSUSE 设置中添加 MP3 和其他多媒体支持。
- `http://KDE-Apps.org`—为 KDE 编写的应用程序社区目录。其中，你可以选择 KonvenientSUSE 包来为你的 openSUSE 系统添加多媒体支持。
- `http://www.cdmedia.com/audio.html`—音频格式常见问题解答，有助于学习各种音频格式。
- `http://opensuse-community.org/Package_Sources/Packman`—Packman 软件仓库的镜像列表，多媒体软件的极佳来源。
- `http://download.videolan.org`—下载 VideoLAN 播放器（以及允许你在 Linux 上播放 DVD 的 libvdcsst）。
- `http://www.softwarereview.org/cms/content/view/60/`—Jem Matzen 的“破解 openSUSE 2.0”文章，有助于在默认的 OPENSUSE 设置中添加 MP3 和其他多媒体支持。
- `http://KDE-Apps.org`—为 KDE 编写的应用程序社区目录。其中，你可以选择 KonvenientSUSE 包来为你的 openSUSE 系统添加多媒体支持。
- `http://KDE-Apps.org`—其中你可以选择 KonvenientSUSU 包来为你的 openSUSE 系统添加多媒体支持。
- `http://download.videolan.org`—下载 VideoLAN 播放器（以及允许你在 Linux 上播放 DVD 的 libvdcsst）。
- `http://www.softwarereview.org/cms/content/view/60/`—Jem Matzen 的“破解 openSUSE 2.0”文章，有助于在默认的 OPENSUSE 设置中添加 MP3 和其他多媒体支持。

## 在 Linux 中模拟其他操作系统：概述

从根本上说有两种方法可以实现跨平台运行应用程序。在种方法中，模拟器将应用程序对一个操作系统（如 Windows）的调用转换为另一个操作系统（Linux）。在第二种方法中，应用程序构建一个虚拟机，在你的计算机内部创建第二台计算机。该虚拟机随后像任何物理计算机一样托管文件系统和操作系统。

在本节中，你将学习三款模拟器（`Wine`、`DOSBox` 和 `Basilik II`）和两款虚拟机（`VMWare` 和 `Win4Lin`）。

## 关于跨平台工具的常见误解

没有什么是是完美的，要达到无缝的跨平台计算境界是非常困难的。在仔细研究这些工具之前，你应该了解几点可能会降低你对新功能热情的事：

- 无论你从 Linux 运行什么工具，你都无法在计算机的 Windows 端运行现有的应用程序。你将安装应用程序的新实例，并且可能需要从头重新创建你的设置。
- 你无法在 Windows 端和 Linux 端之间自动使用相同的数据（例如你的 Eudora 队列）。在许多应用程序中，你可以将数据从一端导入到另一端，但在一端所做的更改不会反映在另一个副本中。
- 不要为了运行一个你没有的应用程序而安装模拟器或虚拟机。这些产品会让你“在 Linux 上运行 Word”，但你需要自己的 Word 副本才能进行安装和运行。如果你需要一个可以打开和编辑 Word 文档的 Linux 应用程序，请使用 OpenOffice 或其他 Linux 套件。

## 使用 Wine 运行 Windows 应用程序

该项目遵循经典的 GNU 递归缩写传统：`Wine Is Not an Emulator` `Wine` 不是模拟器），它是这样说的。尽管如此，这个开源项目长期以来帮助 Linux 用户运行 Windows 应用程序。

概述提到，`Wine` 的工作原理尝试将 Windows 系统调用转换为 Linux 内核，或者让 Windows 应用程序认为它正舒适地位于 Windows 目录中。

`Wine` 环境针对 Windows 98，因此应用程序的行为就像运行在 Windows 98 下。

到目前为止这不是问题，但由于微软已经停止了对该操作系统的支持，其他公司可能会效仿。尽管如此，在购买想要在 `Wine` 下运行的新应用程序时要小心。确认它们可以在 Windows 98 下运行，然后检查 `Wine` 应用程序数据库。

### 安装和配置 Wine

让 `Wine` 运行起来分两步。首先，你必须从 `YaST` 安装 `Wine` 软件包。这使得 `Wine` 命令可用，但不会创建环境或安装任何软件。

启动工作的一种简单方法是安装 `WineTools` 软件包。它包含在你的 openSUSE DVD 中，也可以从 `http://www.vonthadden.de/joachim/WineTools` 获取。这为你提供了一个简单的 GUI 工具来配置 `Wine` 并安装一些基本应用程序。它以 `RPM` 和 `tarball` 包的形式提供。通过 `YaST` 或命令行安装此包。

> 注意
>
> 根据你的系统和 `Wine` 版本，你可能会遇到 `xdialog` 的依赖错误。你可以安全地忽略它并继续安装。

当你安装了 `WineTools` 后，进入提示符（用户用户）并输入 `winetools`。会出现 `WineTools` 菜单（见图 11.1）。

![](img/c9db7a0f830c3bc4a085bc553b89ff25_254_0.png)

图 11.1 `WineTools` 简化了你的 `Wine` 安装。

`WineTools` 菜单的组织方式让你按顺序运行每个工具，并在最后获得一个功能齐全的基础安装。从 `Base Setup` 开始，它将创建你的 `fake_windows` 目录并处理基础 `Wine` 配置（见图 11.2）。

![](img/c9db7a0f830c3bc4a085bc553b89ff25_255_0.png)

图 11.2 使用此菜单创建你的基础 `Wine` 配置。

除了创建你的 `Wine` 驱动器外，使用此菜单安装 `DCOM98`（微软组件对象模型 `COM` 应用程序的关键组件）和 `Internet Explorer`。当你完成此菜单的操作后，点击 `Main Menu` 返回。
