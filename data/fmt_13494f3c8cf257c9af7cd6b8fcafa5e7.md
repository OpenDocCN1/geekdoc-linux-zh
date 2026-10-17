
# 创建 Linux 学习空间

如果您有一台备用或旧的笔记本电脑放在那里，将其重新用作您的 Linux 学习空间可能会很适合您。如果您喜欢移动您的学习环境，这特别有用，例如，当家里变得有点吵和疯狂时，移动到家里另一个更安静的地方。旧台式电脑也可以工作，但您的移动性将降低。

无论您选择哪种系统，请确保它具备足够的容量来处理学习空间的最小硬件要求。如果您计划在单个系统上安装多个 Linux 发行版，单独启动它们，并且不使用虚拟化环境，那么表 1.1 将作为您的需求指南。

## 表 1.1 每次使用单个发行版时的硬件要求

| 资源 | 最低要求 | 建议配置 |
| :--- | :--- | :--- |
| 内存 | 2 GB | >= 4 GB |
| 可用磁盘空间 | 25 GB | >= 30 GB |
| 处理器 | 2 GHz 双核 | > 2 GHz 双核 |

虽然您可以使用这个学习空间，但它显然不是理想的。此外，您可以预期这种类型的 Linux 学习环境启动和运行速度较慢。只有在没有其他选择的情况下，才应使用此学习空间环境。

# 创建虚拟化环境

为您的 Linux 学习空间创建一个虚拟化环境是理想的。这种设置允许您同时启动多个 Linux 发行版，使您能够在它们之间快速切换，并提供对比和比较的体验。此外，在这样的环境中，您可以更彻底地探索网络实用工具。

> 如果您对虚拟化环境不熟悉，请不要绝望。不仅互联网上有许多资源可以帮助您快速上手，而且我们还在第 28 章“理解云和虚拟化概念”中涵盖了虚拟化概念。

有一些优秀且免费的虚拟化产品（称为`hypervisor`或`虚拟机管理器`）可供您安装。它们包括以下产品：

- **Oracle VirtualBox** 这款积极开发的开源软件可在`www.virtualbox.org`获取。它可以在 Linux、Windows、Macintosh 甚至 Solaris 上运行。假设您的硬件资源足够，您可以使用 VirtualBox 同时运行多个 Linux 发行版。该网站加载了有益的文档，并有社区论坛帮助您创建 Linux 学习空间。
- **VMware Workstation Player** VMware Workstation Pro 是一种专有的闭源虚拟化产品。VMware 提供名为 Workstation Player 的免费版本，可在此处获取：`www.vmware.com/products/workstation-player.html`。这个免费版本确实有一些限制。Workstation Player 一次只允许您运行一个虚拟机。此外，如果您想在公司场所安装它，必须支付费用。

![](img/c0a399aca0d18f8822d714ad0a173123_71_0.png)

如果您使用的是 Mac，VMware Workstation Player 将无法在您的系统上工作。相反，VMware 提供了另一种称为 VMware Fusion 的虚拟化产品。它可在`www.vmware.com/products/fusion.html`获取。不幸的是，Fusion 并非免费，但您可以免费试用。

- **Microsoft Hyper-V Server 2019** 这款闭源虚拟化产品可在许多当前的 64 位 Windows 版本上获取，例如 Windows 10 专业版和企业版。但是，Windows 10 家庭版不支持它。假设您的硬件资源足够，您可以使用 Hyper-V 同时运行多个 Linux 发行版。

请不要觉得受限于此列表。它仅包含一些建议您调查的`hypervisor`。如果您发现了更适合您环境的虚拟化产品，请将其用于您的学习空间。

在选择和安装特定`hypervisor`之前，确定您的笔记本电脑或选定系统是否有足够的容量来处理整个学习空间的最小硬件要求。如果您计划同时安装和运行多个 Linux 发行版，请使用表 1.2 作为您所需硬件资源的指南。但请注意，虚拟化产品的网站可能会提供更详细的信息。

## 表 1.2 使用虚拟化产品时的硬件要求

| 资源 | 最低要求 | 建议配置 |
| :--- | :--- | :--- |
| 内存 | 8 GB | >= 8 GB |
| 可用磁盘空间 | 70 GB | >= 100 GB |
| 处理器 | `x86_64` 2 GHz 双核 | `x86_64` > 2 GHz 双核 |

使用虚拟化学习空间非常灵活。图 1.1 展示了这种弹性学习环境的一个示例。

![](img/c0a399aca0d18f8822d714ad0a173123_72_0.png)

请注意图 1.1 中描绘的学习空间，其中包含两个 Ubuntu 和 Rocky Linux 发行版的安装实例。这些发行版提供了安装面向服务器的环境或面向图形的桌面环境的能力。使用 VirtualBox，您可以轻松安装这两种环境并对它们进行比较！

希望您已经开始构思如何配置您的私人学习空间。在此之前，我们还需要探索另一个平台类别。

# 转向云端

如果您没有拥有足够资源以提供多 Linux 发行版学习空间的笔记本电脑或台式机，请考虑云端。虽然云服务器在大型环境中变得越来越流行，但它们也可以提供一种运行单个 Linux 系统的方式。

有许多云服务提供商可以让您启动各种 Linux 发行版虚拟机，例如亚马逊网络服务（AWS）、微软 Azure 和 DigitalOcean。云服务变化迅速，您可能无法找到所需的 Linux 发行版版本。但是，花些时间查看云服务提供商的各种服务是值得的。对于您的学习空间来说，云端可能比新电脑更便宜。

如果您选择使用云服务，该服务可能不会提供探索某些 CompTIA Linux+ 目标的方式，例如通过 BIOS 与 UEFI 修改 Linux 服务器启动方式。在探索您的学习空间场所时请记住这一点。

在您确定学习空间的位置之前，请考虑各种推荐的 Linux 发行版及其版本。这些是您成功的学习空间环境的额外组成部分。

# 探索 Linux 发行版

CompTIA Linux+ 认证是中立的。从实际意义上来讲，这意味着考试的重点不是特定的 Linux 发行版。如果您有红帽企业 Linux（RHEL）的经验，您需要更多地了解 Ubuntu 和 openSUSE 发行版上的实用工具或功能，反之亦然。

人们很容易认为 Linux 发行版都是一样的，它们之间的差异很少。不幸的是，这是一个谬误。我们喜欢将 Linux 内核比作汽车的发动机，将发行版比作汽车的功能。如果您曾经租过车，汽车的功能通常与您通常驾驶的汽车的功能大相径庭。当您进入租来的汽车时，您需要花几分钟时间调整座椅，查看各种汽车控制，并在驶上路面前弄清楚如何使用它们。学习新发行版也是如此。好消息是，如果您拥有丰富的 Linux 经验，学习新发行版并不那么困难。

Linux 发行版通常基于其他发行版或发行版分支。两个流行的发行版组，包含有助于通过 Linux+ 考试的发行版，是基于 Red Hat 的和基于 Debian 的。这两个组之间的差异包括软件包、名称及其管理工具；配置文件名和/或位置；软件发布计划；防火墙配置实用工具；等等。Red Hat Inc. 倾向于关注企业和企业计算，而 Debian 项目关注自由软件。由于这些各种差异，有必要在学习空间中使用两个组的发行版。

了解哪些 Linux 发行版将有助于您成功通过 CompTIA Linux+ 认证考试非常重要。此外，您还应该知道哪些特定的发行版版本是有用的。

## 了解红帽企业 Linux

早期的 Red Hat Linux 始于 1995 年，最初是一个开源项目。它广受欢迎，一度成为最流行的 Linux 发行版，被用于教育环境、企业环境，甚至也被普通的 Linux 爱好者使用。然而，2003 年 Red Hat 停止了 Red Hat Linux 项目，转而支持红帽企业 Linux（RHEL）项目。RHEL 项目主要专注于企业级 Linux 环境。RHEL 是一个商业软件包；因此，在大多数情况下，你必须购买许可证才能使用它。作为回报，Red Hat 提供全面的客户支持，协助设置 Linux 系统并排查故障，这与大多数其他 Linux 发行版不同。

对于 Linux 爱好者来说，幸运的是，还有另一种运行 RHEL 的方式。由于 Linux 是一个开源软件包，Red Hat 被要求发布 RHEL 的源代码。随后，一些其他的 Linux 发行版利用 RHEL 的源代码应运而生。其中最受欢迎的是社区企业操作系统（CentOS）。它几乎是 RHEL 的完全副本，是准备 CompTIA Linux+ 认证考试的绝佳免费学习资源。

然而，正如在快速变化的 Linux 世界中常见的那样，情况已经改变。2014 年，CentOS 加入了 Red Hat 的开源与标准团队；2020 年，Red Hat 用一个名为 CentOS Stream 的新开发版本取代了原始的 CentOS 项目。虽然你仍然可以免费获取 CentOS Stream，但它不再是当前 RHEL 版本的完全副本，而是新概念的试验场，这使得它作为学习资源的好处减少了。

但别担心，CentOS 的原始开发者又启动了一个新的发行版，名为 Rocky Linux。Rocky Linux 回归了 CentOS 的初衷——它是最新 RHEL 版本的完全副本。你可以从 Rocky 网站`www.rockylinux.org`获取 Rocky Linux 发行版的 ISO。请注意，该发行版与许多其他发行版一样，提供多种版本。我们建议你获取 Rocky BaseOS 下载包，选择`8.x`版本系列（撰写本文时为`8.5`版本）。

![](img/c0a399aca0d18f8822d714ad0a173123_74_0.png)

> 随着时间的推移，新的 Rocky 发行版版本将会发布。虽然总是让人受诱惑去获取最新和最棒的版本，但在你的学习环境中使用它并不是有益的。请记住，CompTIA Linux+ 的目标在认证考试下一次更新之前是静态的。因此，使用认证考试创建时可用的发行版版本是明智的。

当你安装 Rocky Linux 时，系统会提示你选择想要安装的环境。对于学习 Linux 而言，通常最好安装图形桌面环境，因为它提供了访问所有你需要了解的 Linux 功能的最简便方式。

安装你的 Rocky Linux `8.x` BaseOS 发行版后，你应该更新软件包。为此，请使用你在安装期间设置的密码登录`root`账户，并发出清单 1.1 中显示的命令。

### 清单 1.1：在 Rocky Linux 上更新软件

```bash
# sudo dnf update
Loaded plugins: fastestmirror
[...]
Upgrade  3 Packages

Total download size: 1.3 M
Is this ok [y/d/N]: y
[...]
Complete!
# 
```

虽然 RHEL（及其衍生版本）是一个流行的发行版，但你还需要一个属于 Debian 阵营的发行版。接下来，我们将探讨 Ubuntu 发行版。

## 了解 Ubuntu

Ubuntu Linux 发行版由 Canonical LTD 管理，自 2004 年起就已存在。这款免费且流行的 Linux 发行版基于 Debian 发行版，是你个人 Linux 学习空间中必备的工具。

你可以从`www.ubuntu.com`获取 Ubuntu 发行版的 ISO。Ubuntu 有好几个版本，如果你想确保能够跟随本书中的示例，我们建议你下载 Ubuntu 桌面版`20.04 LTS`。

![](img/c0a399aca0d18f8822d714ad0a173123_75_0.png)

> Ubuntu 版本名称中的`LTS`代表`Long-Term Support`（长期支持）。这是 Canonical 用来表示将在延长的时间段内提供维护和安全更新的指标。对于`20.04 LTS`而言，你可以指望这些更新持续到 2025 年 4 月。

如果你不熟悉 Ubuntu，你需要了解几个重要的事项。默认情况下，你无法登录到`root`账户。相反，当你需要使用超级用户权限时，请登录你在安装期间设置的账户，并在你的命令行命令前加上`sudo`。清单 1.2 中展示了一个示例。

### 清单 1.2：在 Ubuntu 上使用 sudo

```bash
$ sudo grep root /etc/shadow
root:::17737:0:99999:7:::
$
```

![](img/c0a399aca0d18f8822d714ad0a173123_75_1.png)

> 如果你从未在终端中发出过命令行命令，建议你在尝试之前读完这一整章。你会在本章后面阅读更多关于终端的内容。

另一个重要的事项涉及安装 Ubuntu。如果你连接到网络，可以在安装发行版时自动更新其软件。你会在安装过程中看到一个列为 Download updates（下载更新）的选项，旁边有一个复选框。如果你选择在安装期间不安装更新，你可以稍后通过命令行手动发出清单 1.3 中显示的命令，使用超级用户权限在终端中更新软件。

### 清单 1.3：在 Ubuntu 上更新软件

```bash
$ sudo apt-get update
[sudo] password for Christine:
Hit:1 http://us.archive.ubuntu.com/ubuntu bionic InRelease
Get:2 http://us.archive.ubuntu.com/ubuntu bionic-updates InRelease
[88.7 kB]
[...]
Fetched 1,053 kB in 2s (631 kB/s)
Reading package lists... Done
$
$ sudo apt-get dist-upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages will be upgraded:
[...]
Do you want to continue? [Y/n] Y
[...]
$
```

如果你只能容纳两个 Linux 发行版，Rocky Linux 和 Ubuntu 是不错的选择。如果你有额外的资源，值得再添加一个发行版，openSUSE。

## 了解 openSUSE

openSUSE 发行版于 1994 年首次发布，当时使用的是不同的名称 SUSE Linux。有许多公司参与了对其的支持，其中总部位于德国的 SUSE 公司是原始支持者。

这个发行版拥有非常忠诚且稳固的追随者群体。不仅 openSUSE 发行版得到了社区开发者的强力支持，openSUSE 用户也喜爱它。它的一个独特且流行的实用工具是 Yet another Setup Tool（YaST）。YaST 可以被视为一个命令中心实用工具，它允许你从一个界面控制许多系统服务。

你可以从`https://software.opensuse.org`获取 openSUSE 发行版的 ISO。这个发行版主要有两种版本：Leap 和 Tumbleweed。我们建议你选择 openSUSE Leap 的`15.x`版本系列。

![](img/c0a399aca0d18f8822d714ad0a173123_77_0.png)

openSUSE 社区在 2017 年更改了其发行版的版本号命名方案。`15.0`之前的版本是`42.3`。在你获取 openSUSE Leap 时，请注意这一巨大变化。

一旦你成功安装了 openSUSE，在探索这个发行版之前更新所有软件是一个好主意。要通过命令行更新软件，请手动在终端中发出清单 1.4 中显示的命令，并使用超级用户权限。

### 清单 1.4：在 openSUSE 上更新软件

```bash
$ sudo zypper patch
[sudo] password for root:
Loading repository data...
Reading installed packages...
Resolving package dependencies...
[...]

Note: System reboot required.
Continue? [y/n/.../? shows all options] (y): y
[...]
Warning: One of the installed patches requires a
reboot of your machine. Reboot as soon as possible.
There are some running programs that might use files
deleted by recent upgrade. You may wish to check and
restart some of them. Run 'zypper ps -s' to list these programs.
$
```

你可能已经注意到，最近三个发行版使用不同的命令来更新软件。这是你需要在学习空间中拥有多个发行版的另一个原因。接下来我们将看看另一个重要的发行版。

## 了解 Fedora

Fedora 由 Fedora Project 维护，该项目由 Red Hat 赞助。创新且有时处于最前沿的软件是此发行版的一个优秀特性。如果你想尝试新事物，Fedora 适合你。与其他发行版一样，这个发行版也有多种版本，Fedora Project 将其称为版本（editions）。我们建议你使用 Fedora 34 Workstation 版本。你可以在`https://getfedora.org`获取此 Fedora ISO 的副本。

请注意，这个特定的发行版每六个月更新一次版本。因此，你可能需要从以下位置检索 Fedora 34 Workstation：`https://dl.fedoraproject.org/pub/fedora/linux/releases/34/Workstation`。

![](img/c0a399aca0d18f8822d714ad0a173123_78_0.png)
