

### 5. 请**不要**尝试在其他 Linux 发行版上配置这些实验。
我们选择 Ubuntu (18.04 LTS) 作为实验环境，是因为它是全球前 1000 个网站中最流行的 Linux 发行版，每天约有 500 个网站进入全球前 1000 万网站名单。

### 6. 你**必须**正在阅读或已经阅读过 Linux 学习指南，或观看过理论视频课程。
除了某些配置技巧和建议外，本书不会深入讲解大量理论知识；所有内容均为动手实验。

### 7. 我们不可能为本书成千上万的读者提供个别支持（抱歉！），因此请勿联系我们寻求技术支持。
每个实验都由从初学者到专家的多位技术编辑进行过测试。

## 现实出版社（REALITY PRESS LTD.）的其他著作

- Cisco CCNA 简化指南
- 60 天掌握 Cisco CCNA
- IP 子网划分——从零到高手
- 101 个实验——CompTIA A+（预计 2019 年出版）
- 101 个实验——CompTIA Network+
- 101 个实验——IP 子网划分
- 101 个实验——Cisco CCNP
- 101 个实验——Cisco CCNA
- 101 个实验——Wireshark WCNA（预计 2019 年出版）

## 技术编辑

感谢所有奉献时间检查所有实验并提供反馈的技术编辑。

- Charles L. Burkholder
- Carol Wood
- Dante J. Alarcón
- Timothy A Clark
- Tim Peel
- Elbert L Freeman
- John DeGennaro
- Steve Quan

## LPI-Linux Essentials

# 实验 1

## Linux 的发展与流行操作系统

**实验目标：**
了解什么是 Linux，各种 Linux 发行版是如何演变的，以及这些发行版的用例和目标受众。在虚拟机中安装 Ubuntu 18.04，或您选择的其他发行版。

**实验目的：**
与专有操作系统不同，Linux 的特性意味着用户在决定要在电脑上安装（或不安装）什么软件时拥有无限的选择权。如今有数百种 Linux 发行版或“distros”可供选择，但 Linux 并非一开始就是这样的。Debian、Slackware 和 Red Hat 自 20 世纪 90 年代初就存在，是仍在使用最古老的三个发行版。目前许多最受欢迎的发行版都是衍生或分叉自这三个版本之一。

**实验工具：**
一台连接互联网且支持 VirtualBox 或其他 hypervisor 软件的计算机。

**实验拓扑：**
无

## 实验详解：

### 任务 1：
查看这棵 Linux 发行版树（参见注释中的 URL）。尝试找出一些最常用的发行版：

- Debian
- Ubuntu
- CentOS
- SUSE
- Red Hat
- Linux Mint
- Scientific Linux
- Raspbian
- Android

这些发行版之间有什么关系？

### 任务 2：
如果你还没有这样做，请考虑你即将第一次安装一个 Linux 发行版。思考你在桌面、服务器或两者方面有什么需求。然后参加这个测验：https://distrochooser.de/en

### 任务 3：
记录你在任务 2 中的结果。访问任何看起来有趣的发行版的网站。它们的用例和开发理念（如果有的话）是什么？

### 任务 4：
现在是时候安装一个 Linux 发行版，用于后续的实验了。为了简单起见，我们将假设使用 **Ubuntu 18.04 LTS**。然而，如果你是高级用户，鼓励你尝试在其他自选的发行版上进行这些实验。

这里有一个很好的指南，教你如何在 VirtualBox 中安装 Ubuntu 18.04：

https://linuxhint.com/install_ubuntu_18-04_virtualbox/

**注释：**
许多发行版都有“Live USB”，你可以测试它而无需擦除计算机的硬盘。你还可以使用 VirtualBox 或其他 hypervisor 来测试任意数量的 Linux 发行版。几乎每个发行版都应该能在虚拟机中无故障运行。

在后续实验中，我们将假设使用在 VirtualBox 上运行的 Ubuntu 18.04 LTS 虚拟机。这绝非唯一的可能性，一旦你练习了几次实验，我们鼓励你尝试其他发行版！

https://upload.wikimedia.org/wikipedia/commons/1/1b/Linux_Distribution_Timeline.svg

# 实验 2

## 主要开源应用：桌面

**实验目标：**
了解常见的 Linux 桌面应用程序以及如何使用包管理器安装新应用程序。

**实验目的：**
Linux 拥有各种开源桌面软件，其功能与其他操作系统上常见的专有软件相同。在本实验中，你将了解一些流行的开源软件，以及如何使用称为包管理器的工具安装和更新这些软件。

**实验工具：**
Ubuntu 18.04（或你选择的其他发行版）

**实验拓扑：**
一台 Linux 计算机或虚拟机

**实验详解：**

### 任务 1：
默认的 Ubuntu 桌面已经安装了一些常用软件。看看你是否能找到并熟悉以下应用程序：

- LibreOffice——办公套件
- Thunderbird——邮件客户端
- Firefox——Web 浏览器

找不到这些吗？点击左下角的“显示应用程序”，然后你可以在搜索框中搜索应用程序：

![](img/64f3c5d0defa97e8b856b229f9322b97_19_0.png)

### 任务 2：
仅举一例，你现在的任务是配置 Thunderbird 以连接到电子邮件账户。首次打开 Thunderbird 时，你应该会看到如下的对话框：

![](img/64f3c5d0defa97e8b856b229f9322b97_19_1.png)

输入你的电子邮件账户详细信息，然后单击继续。许多常见的邮件提供商都包含在 Mozilla 自己的数据库中，无需进一步配置。例如，如果你有一个 Gmail 账户，一旦你提供了凭据，Thunderbird 会自动为你设置好。

如果你的邮件服务没有自动配置，你将不得不点击“手动配置”（在下一个屏幕上）以输入你的服务器详细信息。请咨询你的邮件提供商以获取正确的输入值。

### 任务 3：
如果你想使用一个尚未安装的应用程序怎么办？你需要安装它！幸运的是，使用 Linux 包管理器，这很容易做到。搜索“GIMP”并使用 Ubuntu Software 安装它。然后，也熟悉一下 GIMP。GIMP 是一个图像编辑应用程序。

### 任务 4：
在底层，Ubuntu Software 使用一个名为 *apt* 的包管理器。不同的 Linux 发行版使用不同的包管理器，但它们的主要目的相同——提供一个集中位置，用于安装和更新数千个常用软件包。

你能将以下发行版与其默认的包管理器匹配吗？

| 发行版 | 包管理器 |
| :--- | :--- |
| Arch | pacman |
| CentOS | yum / dnf |
| Debian | apt |
| Fedora | dnf |
| Gentoo | Portage |
| SUSE | Zypper |

**注释：**
有时，你可能需要安装一个在发行版的包管理仓库（repos）中不可用的包。在这种情况下，你需要添加额外的仓库，或者使用像 *dpkg* 这样的工具手动安装包。

# 实验 3

## 主要开源应用：服务器

**实验目标：**
了解一些通常部署在 Linux 服务器上的软件和开发工具。

**实验目的：**
在本实验中，你将调研几种常见的 Linux 服务器软件工具。虽然详细配置这些工具超出了本实验的范围，但熟悉它们的应用场景非常重要。

**实验工具：**
Ubuntu 18.04（或你选择的其他发行版）

**实验拓扑：**
一台 Linux 计算机或虚拟机

**实验详解：**

### 任务 1：
使用你 Linux 虚拟机上的 Web 浏览器研究以下一些常见的 Linux 服务器应用程序：

- Web 服务器：Apache httpd, nginx
- 数据库：MariaDB, MySQL
- 文件服务器：NFS, Samba
- 私有“云”：Nextcloud, ownCloud

在什么情况下你会部署每个应用程序？

### 任务 2：
你熟悉任何编程语言吗，例如……

- C？
- Java？
- JavaScript？
- Perl？
- Python？
- PHP？
- 其他？

如果你有软件开发经验，你可能喜欢搜索 Ubuntu Software 或其他包管理器中你最喜欢的语言工具。所有这些语言以及更多其他语言都受 Linux 支持。

### 任务 3：
现在，你将连接到一台远程 Linux 服务器。首先，使用 Ubuntu Software 安装一个名为 PuTTY 的应用程序。PuTTY 是 SSH/Telnet 客户端的图形界面版本，通常用于连接远程 Linux 服务器，尤其是从 Windows 机器连接。

运行 PuTTY 后，你将看到连接屏幕。输入“towel.blinkenlights.nl”，选择 Telnet，然后单击 Open：

![](img/64f3c5d0defa97e8b856b229f9322b97_23_0.png)

