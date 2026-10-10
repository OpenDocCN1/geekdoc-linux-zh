
| fixed_ip | None |
| id | d8c6592-efc2-450e-9726-ccf91d1a05c2 |
| instance_id | None |
| ip | 203.0.113.10 |
| pool | ext-net |

我们可以通过运行以下命令将刚创建的地址用于此新实例，然后检查以确保 IP 已被分配。

```bash
$ openstack ip floating add 203.0.113.10 ferret
$ openstack server list
```

| ID | 名称 | 状态 | 网络 |
| :--- | :--- | :--- | :--- |
| 41887a02-1efa-4b4d-8f64-431c68da066e | ferret | ACTIVE | Network1:10.190.0.13, 203.0.113.10 |

完成了！该实例现在既有一个私有地址，又有新分配的 `203.0.113.10` 地址。可以使用该地址从该网络上的另一台系统 SSH 到该系统。

## 运行服务

无论你使用 OpenStack 仪表板（Horizon）还是 OpenStack 客户端（OSC）来启动你的第一个实例，你现在都已准备好开始登录服务器并进行更改。

## 使用 SSH 登录

我们使用的 Ubuntu 云镜像没有为默认用户 `ubuntu` 设置默认密码，因此通过 SSH 密钥访问，该密钥在之前的步骤中已导入或创建。现在你需要使用此密钥并登录。

首先，你需要与定义了 `203.0.113.1` 网关地址的系统进行交互。如果你使用的是附录 A 中的说明，这将是你运行控制节点和计算节点虚拟机的宿主机器。你可以 SSH 到这台机器，或者直接使用该机器上的 Ubuntu 桌面上的终端 SSH 到实例。为了检查实例是否可以从你所在的机器访问，我们可以先进行 ping 测试。查找你的机器在 `203.0.113.0/24` 中的地址，然后使用 `ping` 命令进行测试。例如，如果你的地址是 `203.0.113.9`，请使用以下命令，该命令应该会从服务器收到 ping 回应：

```bash
$ ping -c 5 203.0.113.9
PING 203.0.113.9 (203.0.113.9) 56(84) bytes of data.
64 bytes from 203.0.113.9: icmp_seq=1 ttl=63 time=3.56 ms
64 bytes from 203.0.113.9: icmp_seq=2 ttl=63 time=1.35 ms
64 bytes from 203.0.113.9: icmp_seq=3 ttl=63 time=1.50 ms
64 bytes from 203.0.113.9: icmp_seq=4 ttl=63 time=1.46 ms
64 bytes from 203.0.113.9: icmp_seq=5 ttl=63 time=1.58 ms
```

## 203.0.113.9 ping 统计信息

发送了 5 个数据包，接收了 5 个，丢包率 0%，耗时 4005ms

`rtt min/avg/max/mdev = 1.354/1.979/3.566/0.812 ms`

现在确认 SSH 服务器是否正常响应：

```bash
$ nc 203.0.113.9 22
SSH-2.0-OpenSSH_6.6ppl Ubuntu-2ubuntu2.6
```

如果一切正常，你可以使用 `ubuntu` 用户和你的 SSH 私钥（可能是 `id_ed25519`、`cloud.key`、`something.pem` 或者你给它起的任何名字）登录：

```bash
$ ssh -i .ssh/id_rsa ubuntu@203.0.113.9
'203.0.113.9' can't be established.
ECDSA key fingerprint is d3:b2:l3:09:35:b0:4b:01:86:0a:52:66:1a:5f:57:5d.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '203.0.113.9' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.13.0-77-generic x86_64)
ubuntu@echinchiala:~$
...
```

既然你已登录，就可以添加服务了。

## 简单的 HTTP 服务器

由于我们运行的是一个限制较多的实例，我们将放弃流行的 Apache 网络服务器，转而使用 Ubuntu 自带的一个非常基础的 `python` 命令来启动 HTTP 服务器。

首先，在你的控制器或存放 Ubuntu 实例 SSH 密钥的位置运行以下命令。请将 `10.190.0.8` 替换为你启动的实例的地址：

```bash
$ git clone https://github.com/DeploymentBook/http-files.git
$ scp -r http-files/nova/ ubuntu@10.190.0.8:
```

> **提示**
>
> 由于我们假设你的实例没有互联网访问权限，所以我们先克隆此仓库到控制器。如果你选择通过网络中的真实浮动 IP 赋予它们访问权限，你可以直接将此仓库克隆到实例上，或者安装 Apache 或其他你希望测试的服务。

此时，Ubuntu 系统上 `ubuntu` 用户的主目录中将会有一个 `nova` 目录。SSH 登录到 Ubuntu 系统以启动 HTTP 实例。

```bash
$ cd nova
$ python -m SimpleHTTPServer
Serving HTTP on 0.0.0.0 port 8000 ...
```

现在回到你通过 SSH 登录的服务器，打开浏览器并导航到实例地址的 `8000` 端口。地址类似于 `http://10.190.0.8:8000`。你应该会看到一个与图 6.10 类似的页面。恭喜，你正在 OpenStack 实例上运行你的第一个面向用户的应用程序！

![](img/8684900d708748f86bb043faa5589f9e_167_0.png)

当你使用完实例并准备将其删除时，你可以登录仪表盘，导航到“实例”，然后从右侧的下拉菜单中选择“关闭实例”或“终止实例”。如果你只是关闭实例，你以后可以再次启动它。终止实例将永久删除该实例。你也可以使用 `openstack server delete <server>` 命令通过 OpenStack 客户端终止实例。

## SDK 和 OpenStack API

我们已经探讨了使用 OpenStack 仪表盘（Horizon）和 OpenStack 客户端（OSC）与 OpenStack 进行交互。

但如果不在讨论软件 development 工具包（SDKs）如何与 OpenStack 应用程序接口（API）进行通信的情况下，关于与私有云交互的章节是不完整的。随着运维环境中自动化的兴起，可以说大多数部署在与其 OpenStack 云的交互中主要使用 SDK。软件使用 SDK 来管理你的 OpenStack 实例及其使用的资源。

OpenStack SDK 可用于多种语言，包括 Python、Java、Node.js、Ruby、.NET 和 PHP。如果你找不到适合你语言选择的 API，你可以通过使用 `cURL` 或 REST 客户端（许多语言都有这些的绑定）来访问 API，或者简单地从你的程序中调用我们本章前面使用的 OpenStack 客户端（OSC）。

主要 SDK 和 OpenStack API 的最新文档可以在 `http://developer.openstack.org/` 找到。

## 摘要

在组织内部运行私有计算云的能力为使用者赋予了极大的力量。无论你是一个需要学生访问服务器实例的大学，还是一个需要按需服务器资源的开发者组织，能够即时向用户提供这些资源是一件很有力量的事情。

# 7

# 公共计算云

> *没有任何房子应该建在山丘或其他任何地方。*
>
> *它应该是山丘的一部分，属于它，以便山丘和房子能*
>
> *和睦相处，彼此更加快乐。*
>
> *弗兰克·劳埃德·赖特*

世界各地的公司都在部署公共计算云，以为希望处理数据的客户提供服务。这些云的关注点涵盖了从按需计算能力到存储系统的方方面面，我们将在后续章节中对此进行探索。对于以计算为主的托管服务，OpenStack 为动态应用程序提供了一个平台，为客户提供高可用性的服务。通常，这些服务根据使用的资源（RAM、CPU、磁盘等）和实例使用的时间进行计费，通常按小时为单位。

本章将在第 6 章“私有计算云”所学内容的基础上进行构建，向你展示如何跟踪使用量并最终为组织运行的公共云服务进行计费。

## 用途

随着 OpenStack 社区在过去几年的发展，我们看到多家公司应运而生，提供与市场上现有专有云解决方案竞争的服务。OpenStack 基金会市场有一个专门部分致力于提供公共云的公司（`http://www.openstack.org/marketplace/public-clouds/`）。

作为该市场的参与者，公司可以利用 OpenStack 开源平台的开发，并在其上为客户构建优势，例如地理多样性、速度、高网络速度甚至应用程序集成，以加快客户构建产品的速度。

## 传统科技公司

传统科技公司拥有悠久的历史和良好的创新声誉，并为客户提供稳固的产品。在当今云驱动的世界中，一些传统科技公司开始构建公共云。这些通常与其其他产品一起提供，或与其私有云产品协同提供。

在一次 OpenStack 峰会主题演讲中，一家公司谈到其客户现在正在使用混合云，即将部署的一系列私有云与公共云相结合。该公司将进行现场支持以协助部署私有云，然后为基础设施中面向公众的部分提供公共云。

## 网络托管公司

专注于网络托管的公司也开始提供公共计算选项。许多公司最初通过向客户提供虚拟专用服务器（VPS）购买开始，并提供特定的托管服务，如博客或论坛安装。随着向云的转变，这些托管公司使用类似于许多传统网络托管服务所使用的框架，赋予用户构建自己的应用程序的能力。

此外，一些公司正在利用 OpenStack 的部分功能为客户服务，提供用于单个文件的对象存储，你将在第 9 章“对象存储云”中了解相关内容。

## 需求

在此部署场景中，你将使用你在第 5 章“部署基础”中创建的控制器和计算节点。对于此安装，你可以使用你在第 6 章中使用的相同系统，因为我们在该基础部署上没有做任何添加。

你可能还希望留出一些时间让此部署运行一段时间。由于 OpenStack 收集计量是随时间跟踪的，让两个实例整夜运行将收集数据，以便你第二天或下一周进行探索。

## 选择组件

除了基础工具之外，我们将在此场景中向你的部署添加 Ceilometer 遥测服务。这将扩展基本安装，以包含以下服务，其部署位置如图 7.1 所示：

- 计算（Nova）
- 身份（Keystone）
- 网络（Neutron）
- 镜像服务（Glance）
- 仪表盘（Horizon）
- Ceilometer（遥测）

![](img/8684900d708748f86bb043faa5589f9e_172_0.png)

图 7.1 包含 Ceilometer 遥测服务的双节点 OpenStack 部署的组成部分

## 架构概览

在最基本的层面上，Ceilometer 轮询你正在运行的 OpenStack 服务。在我们的演示中，我们将使用 Nova 计算服务和 Glance 镜像存储。它还可以从通知总线收集通知。收集器会收集这些信息并将其放入数据库中。在我们的部署中，为了保持简单，使用 MySQL 作为数据库，但 MongoDB 是原始的也是目前仍推荐的数据库。

从这个数据存储中，你通过与 API 交互来查询数据。这可以通过在 Horizon 仪表板中查看输出、使用 OpenStack 客户端或 Ceilometer 命令行界面，或者通过稍后本章将简要介绍的外部计费系统来实现。这一基本概述如图 7.2 所示。

收集器收集的数据以度量的形式进行跟踪。度量是实际被测量的对象，例如 CPU 负载、磁盘 I/O 或 Glance 镜像占用的空间量。这些度量的每一种都作为类型被跟踪。Ceilometer 理解以下度量类型：

- 累计型（Cumulative）——随时间增加，例如实例运行了多久
- 仪表型（Gauge）——离散项目，如镜像上传数量或使用的浮动 IP 数量，以及像磁盘 I/O 这样波动的值
- 差值型（Delta）——随时间范围的变化，如带宽

除了这个基本概述之外，Ceilometer 还有变换器（transformers）和发布者（publishers）的概念。变换器允许你操作原始数据并对其进行扩展，以形成新的测量值或改变维度，使不同类型的数据能够呈现给客户端或其他外部系统。发布者允许你将指定数据重定向到一个或多个目标，而不是要求这些目标主动请求数据。

## 场景

如前所述，我们将把 Ceilometer 添加到我们在第 5 章中定义并再次用于第 6 章的基本 OpenStack 安装中。由于我们要添加另一个服务，因此需要使用 Puppet 拉取额外的组件。

在此场景中，你将对控制节点和计算节点都进行修改。

## 控制节点设置

在控制节点上，你将使用另一个 `puppet apply` 命令，它将处理我们在 Puppet 中的基础公有云角色：

```bash
$ sudo puppet apply /etc/puppet/modules/deployments/manifests/role/foundations_public_cloud.pp
```

当此命令正在运行时，让我们看看我们在运行什么。

```puppet
class deployments::role::foundations_public_cloud {
  include deployments::role::foundations
  include deployments::profile::ceilometer
}
include deployments::role::foundations_public_cloud
```

如图所示，这拉取了我们的基础清单（manifest），如果你是从之前设置的节点开始，它应该已经运行过了。然后它拉取我们在部署组合模块中定义的 Ceilometer 配置文件。Ceilometer 配置文件是有趣的地方所在。在你的文件系统中，它位于 `/etc/puppet/modules/deployments/manifests/profile/ceilometer.pp`，包含以下内容：

```puppet
class deployments::profile::ceilometer
{
  include ::ceilometer
  include ::ceilometer::client
  include ::ceilometer::collector
  include ::ceilometer::agent::auth
  include ::ceilometer::agent::central
  include ::ceilometer::agent::notification
  include ::ceilometer::agent::polling
  include ::ceilometer::api
  include ::ceilometer::config
  include ::ceilometer::db
  include ::ceilometer::db::mysql
  include ::ceilometer::keystone::auth
}
```

我们要安装 Ceilometer 客户端，以便在本章后面可以查询数据。除此之外，你还有组件遵循图 7.2 中的流程：

1. 轮询代理收集测量值并将其放入队列。
2. OpenStack 服务在标准通知总线上发送通知。
3. 通知代理处理来自轮询代理和通知总线的数据，并将其发送到目标，在我们的情况下就是收集器。
4. 收集器或其他报告器将数据存储在持久存储中，如数据库、文件或 Gnocchi（一个在 OpenStack 遥测项目下开发的时间序列数据库存储系统）。同样，我们使用 MySQL 作为数据存储。

认证由 Keystone 处理，因此我们拉取设置认证所需的组件。

## 计算节点设置

与控制节点一样，我们将使用 `puppet apply` 命令为计算节点添加另一个基础角色，以便可以从运行在其上的节点收集数据。

```bash
$ sudo puppet apply /etc/puppet/modules/deployments/manifests/role/foundations_compute_public_cloud.pp
```

这将运行几分钟，因为它安装和配置所需的组件，我们可以看看拉取的是什么：

```puppet
class deployments::role::foundations_compute_public_cloud {
  include deployments::profile::base
  compute
  include deployments::profile::compute
  include ::ceilometer::agent::polling
  include ::ceilometer::agent::auth
}

include deployments::role::foundations_compute_public_cloud
```

这个类与我们之前应用的基础计算角色几乎完全相同，但它现在包含了轮询和认证代理，以便可以从虚拟化管理程序（hypervisor）收集有关 CPU 和网络使用率等统计信息。

## 轮询虚拟化管理程序

用于轮询虚拟化管理程序的代理需要对系统正在做什么有相当大的可见性。这意味着它还需要支持查询这些虚拟化管理程序的方式。在 Mitaka 中，支持以下虚拟化管理程序：

- KVM 和 QEMU，用于我们的参考部署（通过 libvirt）
- LXC（通过 libvirt）
- UML（通过 libvirt）
- Hyper-V
- Xen
