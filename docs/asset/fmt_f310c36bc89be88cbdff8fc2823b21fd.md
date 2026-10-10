
请记住，使用硬盘运行 Fedora Live 与在硬盘上安装 Fedora 是不同的。使用硬盘运行 Fedora 是标准的 Fedora Live 操作，它使用部分硬盘空间来运行 Live DVD/CD 磁盘镜像。`Install Hard Drive`（桌面上的图标）实际上运行的是标准的 Fedora 安装过程，将 Fedora 放入你的系统中，就像进行普通安装一样（见第 2 章）。

## 在 KDE 上使用 USB 驱动器

KDE Live CD 使用新的 Plasma 桌面和面板。USB 盘不再以图标形式显示在桌面上。USB 盘图标将同时出现在 Kickoff 菜单和文件管理器侧边栏中。要挂载驱动器，只需点击其图标。驱动器上将出现挂载标志（见图 1-3）。在文件管理器窗口中，点击侧边栏中的 USB 盘项以打开 USB 盘的文件列表。然后你可以将文件保存到驱动器。

![](img/9a8872dc6f2acaed163529fd9d421e05_42_0.png)

### 图 1-2：Fedora KDE CD

![](img/9a8872dc6f2acaed163529fd9d421e05_42_1.png)

### 图 1-3：Fedora KDE CD

![](img/9a8872dc6f2acaed163529fd9d421e05_43_0.png)

### 图 1-4：Fedora KDE CD

要挂载驱动器，只需点击其图标。驱动器上将出现挂载标志（见图 1-3）。在文件管理器窗口中，点击侧边栏中的 USB 盘项以打开 USB 盘的文件列表。然后你可以将文件保存到驱动器。

## 从 USB 安装 Fedora

在配置文件中，你可以设置如语言、防火墙、启动的 `xconfig` 以及用于网络的 `NetworkManager` 和 `DHCP` 等特定服务。所使用的存储库在 `repo` 条目中指定。你可以使用桌面 `desktop`、最小化 `minimal` 和 `KDE` 配置文件作为基础。软件包列在 `%packages` 条目之后。对于单个软件包，只需指定软件包的唯一名称。软件包组的 Kickstart 语法符合“添加/删除软件”面板（`PackageKit`）中相同的类别和子标题。当你需要选择如 GNOME 或 KDE 桌面所需的大量软件包时，这些非常有用。确保在组名前加上 `@` 符号，例如基础软件包使用 `@Base`。

## Fedora 9 桌面视觉效果：

Fedora 9 具有桌面视觉效果，包含 Fedora 图标以及新的默认无限背景。图标描绘了一个封装在蓝色圆圈内的 F。在主面板上，你现在将看到蓝色 Fedora 图标作为应用程序菜单的图标。默认背景是气泡中的蓝色 F 图标，周围还有其他气泡。图标有自己的包 `fedora-logos`。

该图标的设计旨在代表 Linux 社区和开发的三个特征：自由、交流和无限可能——代表自由的 f 融入无限符号，两者都封装在通过全球交流（声音）发展的对话框中。通过全球交流实现无限可能的自由开源软件。其理念是唤起 Linux 开发的精神和目的，即给予无限自由。该图标整合了 Fedora 的四个基本理念：开放、自由、创新和前瞻性（见图 1-5）。更多详情请参考 `fedoraproject.org/wiki/Logo`。网站上显示的图标描述如下

![](img/9a8872dc6f2acaed163529fd9d421e05_44_0.png)

### 图 1-5：Fedora 图标

默认主题现在是 `Nodoka`，这是一个为 Fedora 设计的 GNOME 主题。按钮和窗口更加易用，且视觉上更令人悦目。在 Gnome 主题管理器中还有许多其他主题可供选择。Gnome 桌面的功能与 Fedora 7 相同，包含“应用程序”、“位置”和“系统”菜单（见图 1-6）。

![](img/9a8872dc6f2acaed163529fd9d421e05_45_0.png)

图 1-6：带有 Fedora 标志的 Fedora 9 桌面

## 开源软件

Linux 是通过互联网作为一项合作性的开源努力开发的，因此没有哪个公司或机构控制 Linux。为 Linux 开发的软件反映了这一背景。开发通常发生在 Linux 用户决定共同开展某个项目时。软件被发布在互联网网站上，任何 Linux 用户都可以访问它并下载该软件。Linux 软件开发一直在互联网环境中运行，并具有全球范围，招募了来自世界地的程序员。你启动一个基于 Linux 的软件项目唯一需要的是一个网站。

大多数 Linux 软件都是作为开源软件开发的。这意味着应用程序的源代码随应用程序免费分发。互联网上的程序员可以对软件包的开发做出自己的贡献，修改并纠正源代码。Linux 是一个开源操作系统。它的源代码包含在所有的发行版中，并在互联网上免费提供。许多主要的软件开发工作也是开源项目，`KDE` 和 `GNOME` 桌面以及大部分应用程序也是如此。`Netscape Communicator` 网页浏览器包也已开放，其源代码免费可用。由 Sun 支持的 `OpenOffice` 办公套件是一个基于 Star Office 套件的开源项目（StarOffice 本质上是 Sun 的 OpenOffice 商业版本）。许多运行在 Linux 上的开源应用程序已将它们的网站定在 `SourceForge` (`sourceforge.net`)，这是一个专门设计用于支持开源项目的托管站地。你可以在 `www.opensource.org` 找到更多关于开源运动的信息。

开源软件受公共许可的保护。这些许可防止商业公司通过添加少量自有的修改、对这些更改申请版权并将软件作为自己的产品出售来获取对开源软件的控制权。最流行的公共许可是由自由软件基金提供的 GNU 通用公共许可证（`GPL`）。这是 Linux 分发时遵循的许可。GNU 通用公共许可证保留了版权，免费许可软件，并要求软件及其任何修改版本始终免费可用。还创建了其他公共许可以支持不同类型开源项目的需求。GNU 简化公共许可证 (`LGPL`) 允许应用程序使用 GNU 许可软件库。Qt 公共许可证 (`QPL`) 允许开源开发者使用 Qt KDE 桌面。你可以在 `www.opensource.org` 找到完整列表。

Linux 目前受自由软件基金提供的 GNU 公共许可证保护，它通常被称为 GNU 软件（见 `www.gnu.org`）。只要免费分发给他人，GNU 软件就是免费分发的。许多流行的 Linux 工具，如 C 编译器、shell 和编辑器，都是 GNU 软件应用程序。随你的 Linux 发行版一起安装的 GNU `C++`、`Vi` 和 `Emacs` 编辑器，`BASH` 和 `TSHSH` shell，以及 `TeX` 和 `Ghostscript` 文档格式化器。此外，还有许多根据 GNU 通用公共许可证 (`GPL`) 许可的开源项目。这些许多软件应用程序可以在不同的网站上获得，并列在表 1-2 中。第 4 章详细描述了从互联网网站下载软件应用程序并将其安装到系统中的过程。

根据 GNU 通用公共许可证的条款，原作者保留版权，尽管任何人都可以修改并重新分发软件，前提是包含、公开并免费提供源代码。此外，对于出售软件或免费赠送软件没有限制。一个发行商可以对软件收费，而另一个发行商可以免费提供。主要的软件公司也提供它们最受欢迎应用程序的 Linux 版本。

由于 Fedora 的的 。 | | | | | | | | | | | | | | | | |

 | | |ora | | | | | | | | | | | | | | | | |

..... |..ora |ora |ora |.....ora..... |. | |. |

......... |

..orafedora.org | Fedora 镜像 |

| mirrors.fedora.org | Fedora 镜像 |

| download.fedora.org |

### 表 1-2: Fedora 软件仓库

| URL | 互联网站点 |
| :--- | :--- |
| mirrors.fedora.org | Fedora 镜像 |
| download.fedora.org | Fedora 镜像 |
| mirrors.fedoraproject.org | Fedora 镜像 |
| .ora.fedoraproject.org | Fedora 镜像 |
| rpm.livna.org | Fedora |
| atrpms.org | Fedora |
| .ora.fedora.org | Fedora |
| .ora | |
| download.redhat.com | 红帽提供的 Fedora 镜像源 |
| sources.redhat.com | 红帽开源软件 |
| torrent.fedoraproject.org | Fedora 镜像下载 |
