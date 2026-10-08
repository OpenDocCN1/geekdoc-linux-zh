
多媒体内容创建是 Ubuntu Studio 的重点，它使用相同的 GNOME 桌面。Ubuntu Studio 专注于获取基础桌面镜像并对其进行配置，以为创意人员提供最佳性能。它包含了一个用于音频、图形、视频和出版的软件套。

# Ubuntu 18.04 LTS

## 快速指南

如果你正在安装新版本，可能会发现一些细微的变化。虽然仍使用默认设置，但还有其他需要注意的选项。第一个是 `minimal`（最小），它在不安装大部分预设软件的情况下安装 Ubuntu（约 500MB），但剩余的安装并不特别轻量，特别是安装应用程序时。

对于 Ubuntu 上的 Web 用户，需要注意的是 Ubuntu 18 已于 2020 年寿命并从主仓库中移除。

> 切换到 GNOME 的副作用之一是登录界面现在由 `GDM` 驱动。

在分区时，你将不再被提示创建交换分区（`swap partition`）。现在它是基于文件的，所以你不需要担心空间。默认选择 Ubuntu 变体、位置、硬件等。

### 安装 32 位版本

Ubuntu 18.04 是第一个仅提供 64 位完整 ISO 下载的发行版本。如果你需要在 32 位硬件或 ARM 等其他架构上运行，你有几个选择。首先，你可以安装上一个 LTS (`16.04`) 并升级到最新版本。或者，你可以使用网络镜像和 USB 闪盘获取创建 `PXE` 启动服务器所需的文件，并通过对发行版的安装，从启动到网络构建所需的文件。在在机器上安装所需包之前，对于包括 HTTP 代理、网关和 apt 仓库密钥、镜像选择和其他工具在内的基础网络配置，最简单的方法是制作你自己的自定义 ISO：

上图：`Subiquity` 安装程序为服务器安装的易用性和速度带来了许多急需的的改进。

## Ubuntu Server

服务器安装对 Ubuntu 至关重要。桌面用户可能热于更新到“最新”和“最强”，但这并不适用于 Ubuntu。在服务器环境中，稳定性至关重要，用户更倾向于留在 LTS 版本，仅升级到点版本，然后再升级。Ubuntu Server 现在使用 `Subiquity`（又称 '`ubiquity`'）来处理为服务器环境定制的服务器设置。安装程序仍然如你预期的那样基于文本，但更好用得多。

> 服务器的首次更改来自于一个长期更新，该更新改进了网络延迟和吞吐量。虚拟化 API `Libvirt` 已更新到第 4 版本，为其主机的自动化管理带来了最新的改进。

如果你处理云业务，18.04 中增加了一套易于操作的 Python 工具，其中还包括 `DPK`（一组数据库和对其他修复的支持）。自 2022 年起，新版本开箱即用包含了 `Meltdown` 和 `Spectre` 问题，内核需要相应的缓解措施。

上图：在第一个 LTS 点发布版本之前，你需要使用 `-d` 选项进行升级。

LTS 的发布非常直接——`ifdown/network/interfaces`。网络设备使用 `netplan` 配置。默认选择 Ubuntu 变体、位置、硬件等。

长期更改来自于长期更新，该更新改进了网络延迟和吞吐量。虚拟化 API `Libvirt` 已更新到第 4 版本，为其主机的自动化管理带来了最新的改进。

如果你处理云业务，18.04 中增加了一套易于操作的 Python 工具，其中还包括 `DPK`（一组数据库和对其他修复的支持）。自 2022 年起，新版本开箱即用包含了 `Meltdown` 和 `Spectre` 问题，内核需要相应的缓解措施。

上图：在第一个 LTS 点发布版本之前，你需要使用 `-d` 选项进行升级。

LTS 的发布非常直接——`ifdown/network/interfaces.`网络设备使用 `netplan` 配置。默认选择 Ubuntu 变体、位置、硬件等。

长期更改来自于长期更新，该更新改进了网络延迟和吞吐量。虚拟化 API `Libvirt` 已更新到第 4 版本，为其主机的自动化管理带来了最新的改进。

使用 `MAAS` 或云配置时，Open Ubuntu 提供了许多方便的。。 Ubuntu Ubuntu Ubuntu  Ubuntu Ubuntu Ubuntu Ubuntu Ubuntu  Ubuntu  Ubuntu  Ubuntu Ubuntu Ubuntu  Ubuntu  Ubuntu  Ubuntu  Ubuntu Ubuntu 在 Ubuntu 18 Ubuntu  Ubuntu  Ubuntu  Ubuntu  Ubuntu  Ubuntu  Ubuntu  Ubuntu 。

## 提示 使用 Livepatch 补丁无需重启

Canonical `Livepatch` 环境允许在无需重启的情况下提供安全补丁。它适用于少少数设备，并在 Bonionic 中增强了 `MOTD` 状态更新。

| Finished install! |

| :--- |

| configuring mount: mount- |

| running 'curtin-net-auto' |

| running 'curtin-install' |

| installing sources to disk |

| running 'curtin hook' |

| copying archive image from //root |

| running 'curtin hooks' |

| configuring apt config |

| installing packages |

| installing kernel |

| writing /etc/fstab |

| updating packages on target system |

| running user-agent on target system |

| finalization |

| running curtin hook |

| executing-services |

### 特性

# Ubuntu 18.04 LTS

### Ubuntu 云

Ubuntu 向云端的迈进正在加速，并提供了广泛的产品选择。

Canonical 已经强调了 Ubuntu 云对于**其作为快速增长的收入流的修订战略**重要性。Ubuntu 正在成为云计算的操作系统，50% 的公有云工作负载和 54% 的 OpenStack 云正在使用该操作系统。

自 2011 年初以来Canonical 一直支持 **Ubuntu 上的 OpenStack**，但它究竟是什么呢？OpenStack 是一种“云”操作系统，用于控制整个数据中心的计算、存储和网络资源池，所有内容通过一个仪表板进行管理，为管理员提供控制权，同时允许用户通过 Web 界面配置资源。

要为自己开始使用 Ubuntu 非常简单，这得益于一种理想的工具，它可以在几分钟内单机机器上快速构建 OpenStack 云；此外，它还可以轻松扩展到四台或更多物理服务器，使用 **MAAS（金属即服务 - 一种物理硬件、配置和管理的云方法）、Juju、LXD、PaaS 和 HCI。**

对于本地使用，在 Ubuntu 3.0 之后你可以使用 `LXD`，它是一个轻量级虚拟机化程序，运行 Linux 内核操作系统并具有前所未有的速度虚拟机状态操作。`LXD` 可以以虚拟机化器的安全性管理虚拟机，但运行速度更快。对于裸机，`LXD` 容器与原生操作系统一样快，这意味着在云端中，

> Ubuntu 'conjecture' 工具包含了几个用于云部署和容器部署的预包“咒语”

`Conjecture-juju` 以软件包的形式安装，从 18.04 版本开始，它将日益成为 Ubuntu 的标准方式。

首先安装 `sudo snap install lxd`，然后执行 `sudo apt install juju` 和 nextcloud。使用 `sudo snap install --classic conjecture-juju` 构建工具本身。这个基于的实用程序——毕竟它是为服务器构建的——提供了推荐命令列表以及软件应如何部署的描述，并由 YAML 文件组成。咒语 conjure-spells 存储在 https://github.com/ubuntu/spells 的 GitHub 注册表中，在那里，可以在不通过 git 配置的情况下继承咒语，该配置将直接传递给工具，并从该处加载咒语。带有 Nova-LXD 的 OpenStack。

#### Snap 咒语从 18.04 开始将日益成为 Ubuntu 的标准方式

- 快速指南：使用 Juju 部署服务

Juju “charms”是简化部署和管理复杂服务的简单方法。在 https://juju.com 可以找到，涵盖了 openstack、分析、apache 监控、OpenStack 等许多不同场景。使用 ElasticSearch 作为 charm 像往常一样简单：`juju deploy cs:elasticsearch`。当命令启动时，ElasticSearch 默认将应用端口 (`9200`) 设置为仅实例自身可用，但更改只需运行命令 `elastic-search-juju status` 来确认哪些端口是打开的。要打开所有端口，请使用命令 `juju deploy elasticsearch firewall_enabled=false`。

`LXD` 是最好的起点——你会注意到，还提供了使用 Apache Hadoop 和 Spark 进行大数据分析的咒语，以及用于 Kubernetes 的。

选择咒语后，系统将提示你编辑设置位置 (`localhost`)，配置网络和存储，然后提供公钥以启用对新部署内容的访问。接受默认值并点击“部署”。Juju 控制器——Juju 的一部分，打开应用程序服务和建模配置。设置完成后，你将能够在 http://openstack-ip/horizon 打开 OpenStack 仪表板并使用用户名登录查看正在运行的内容。

## 快速指南

免费在云端尝试 Ubuntu

Ubuntu 提供了云端部署的精彩机会，但由于定价模型，成本可能会迅速增加！幸运的是，如果你想在不花任何钱的情况下尝试云部署，我们提供了免费优惠。亚马逊 AWS 提供了一项优惠，包含期一年的免费层级。Google Cloud 提供 300 美元的免费额度。DigitalOcean 提供 100 美元的免费额度。Azure 提供了 12 个月的免费用期。Heroku 提供了免费额度。Linode 提供了免费额度。Vultr 提供了免费额度。Oracle Cloud 提供了免费额度。Alibaba Cloud 提供了免费套餐。腾讯云 提供了免费额度。华为云 提供了免费额度。

### 详情

| AWS EC2 | 1 GB |

| :--- | :--- |

| 750 小 | Free |

| AWS RDS | 5 GB |

| :--- | :--- |

| 750 Hours | Free |

| AWS Lambda | 1 Million |

| :--- | :--- |

| Monthly requests | Free |

| AWS QuickStart | 1 Million |

| | Free |

已被 Ubuntu 支持 12 个月的免费产品。

Ubuntu 上的 Docker Engine

Canonical 认为没有这两个重量级——Docker 和 Kubernetes 将是不完整的。Docker 是一个轻量级容器运行时，带有功能齐全的工具包，可以构建并运行你的容器。超过 65% 的基于 Docker 的扩展

在 Ubuntu 上运行的操作。

Docker Inc. 在 Ubuntu 上发布并更新 Docker 的稳定版本，让所有 Ubuntu 用户都能直接访问官方 Docker Engine。

Canalytics 确保了 Docker Hub 上安全 Ubuntu 镜像的可用性，它为 Docker Enterprise 提供第一级支持和技术支持，并由 Docker 公司本身提供支持。

如果你正处于选择尝试何种技术的阶段，在 Docker 和 LXD 之间做出决定并不容易。LXD 为你的所有管理进程提供了类似虚拟机的体验，感觉像一个普通的系统，但它通常每个容器只运行单个进程或应用程序。

LXD 允许你将基础设施作为“服务”——使 OS 实例部署变得快得多，而 Docker 则被开发者用于使“平台即服务”变得更具可移植性。但请记住，这些选项并不是互斥的——你可以同时运行 Docker 和 LXD。

在 Ubuntu 上，Kubernetes 得到了良好的支持。在云端也是如此。

![](img/adbb964c9bace8f3e3949547041f6ef9_66_0.png)

更多：如果部署 Kubernetes，支持多个云提供商，包括 AWS（如图所示）、Azure、Cloud、Google、Oracle 和 Rackspace。

通过 Ranchera 交付原生 Kubernetes，Canonical 有一个纯正的 Kubernetes 产品，有一个响亮的名字：“Kubernetes 发行版”（The Distribution of Kubernetes）。这是 Kubernetes，在各种基础设施上经过测试，具有现代化的指标和监控，并与 Ubuntu 工作节点以及 Canonical 的 Google Kubernetes Engine (GKE) 服务合作开发。该技术栈是

> 快速提示

> 配合 Juju 使用 Kubernetes

> 可以 Juju 快速部署带有附加服务的 Kubernetes Core（Kubernetes 的一部分）集群或 Canonical Kubernetes 发行版。执行 `juju deploy be-starter:3.2` 或 `juju deploy bundle/canonical-kubernetes-179`。

完全托管的。最重要的是，Canonical 在对比参考实现的标准合规方面处于领先地位。

我们使用这个过程是因为清理，只是这次你在选项中选择了 Canonical Kubernetes 发行版。值得获取一个免费账户来设置独立的集群环境。

部署容器变得简单而容易。

Ubuntu 18.04 缓解了痛苦。Docker 最小 Ubuntu 镜像与包含超过 10 万个文件的官方镜像相比，体积缩小了 53%。当然，这些镜像非常基础——只有运行和下载额外包所需的内容，但压缩后仅为 31mb，解压后为 818mb，这些就是全部。

简而言之，较小的镜像改进了安装容器工具集的过程，最新的 LTS 发行版提升了部署容器后的体验，而在主流平台的帮助下满足了 Ubuntu 的生态需求。

## 快速指南：迁移到容器

Ubuntu 18.04 `LXD 3.0` 包含一个名为 `lxd-p` 的新工具。它使得通过 `LXD` API 将系统转换为 `LXD` 容器变得更加容易。安装后，结果可以通过将其到 `LXD` 服务器传输到任何系统，系统文件将传输到新容器中。此工具可以用于

另一个集成是与物理机或虚拟机 OpenStack 的集成。这是可能的，但更复杂。首先，需要通过编辑 `/etc/selinux/` 禁用inux。

# Ubuntu 18.04 LTS 特性

# Ubuntu Core、IoT 与机器人

Ubuntu Core 是一个精简、事务化的 Ubuntu 版本，专为 IoT 设备、机器人和容器部署设计。它基于超安全的、远程可升级的 Linux 应用程序平台，该平台被从芯片供应商到设备制造商和集成系统的一系列领先 IoT 厂商所使用。

当设备在现场运行时，安全问题会被解决。当然，Ubuntu Core 是免费的；它可以带有自定义内核、BSP（板级支持）并根据你的套件选择免费发布。它具有无与伦比的可靠性，包括完整的回滚功能，以降低现场管理设备的成本。

Ubuntu Core 中的所有内容都基于数字签名的 snaps。内核驱动程序、设备驱动程序被封装为 snap。最小操作系统也是一个 snap。最后，所有应用本身都是 snaps，使其易于管理。整个发行版仅 350MB，比许多都要小。

Core 使用与经典 Ubuntu 相同的内核、库和系统软件。IoT 的 snaps 可以在 Ubuntu 或任何其他发行版上开发。Core 的区别在于它是为了物联网而构建的。它默认是安全的——自动更新确保了任何关键

当前版本的 ROS（非常适合在 Ubuntu 上使用，是第 11 版本“月亮记录头”（Lunar Loggerhead）

![](img/adbb964c9bace8f3e3949547041f6ef9_67_0.png)

> Joshua Elsdon

![](img/adbb964c9bace8f3e3949547041f6ef9_67_1.png)

## 为树莓派 3 构建新的 Ubuntu Core 镜像

![](img/adbb964c9bace8f3e3949547041f6ef9_67_2.png)

```
sudo snap install --classic celery
snapcraft create --name my-snap .
```

- 创建用于签名上传的密钥

  在开始构建镜像之前，你需要创建一个密钥来签署未来的上传。生成一个与你的 Ubuntu Store 账户关联的密钥，并使用 `snapcraft list-keys` 密钥确认 snaps。

- 在 Ubuntu Store 注册

  接下来，你必须将密钥注册到 Ubuntu Store，将其关联到你的账户。你将能够使用商店账户登录。

- 创建模型断言 (model assertion)

  为了构建镜像，你需要创建一个模型断言。这是一个包含设备描述的 JSON 文件，根据你的现有设备对其进行调整。

# UBUNTU CORE 18.04

尽管拥有丰富的特性集，它仍然是强大的。最重要的是，Ubuntu Core 支持大量的设备，从 32 位 ARM 树莓派 1 和 2 到 64 位 Qualcomm 龙板 410 以及 Intel 最新 i7 核心。对于开发板，需要创建 gadget 和模型断言。构建 Core 镜像的过程是非常简单的。内核是 snap

内核驱动、设备驱动程序在 Ubuntu Core 中被封装为 snap。

![](img/adbb964c9bace8f3e3949547041f6ef9_68_0.png)

封装的应用是 snap

![](img/adbb964c9bace8f3e3949547041f6ef9_68_1.png)

最小操作系统封装为 snap
