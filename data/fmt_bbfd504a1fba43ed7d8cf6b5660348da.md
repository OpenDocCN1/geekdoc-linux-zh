
| updated_at | 2016-04-13T03:06:42Z |
| virtual_size | None |
| visibility | public |

```bash
$ ironic image list
```

| ID | 名称 | 状态 |
| :--- | :--- | :--- |
| 34103a9b-b706-4ba9-a929-f755dc8f4b1e | my-initrd | active |
| ea003044-f792-408b-b6cd-46af01528c65 | my-vmlinux | active |

在此设置完成后，您接下来需要运行 `ironic node-create` 命令，其中包含裸金属服务器的详细信息，包括 IPMI 地址和登录信息，以及 CPU 数量、内存（以 MB 为单位）和磁盘（以 GB 为单位）：

```bash
$ ironic node-create -D pxe_ipmitool -i ipmi_address=10.0.0.5 -i ipmi_username=ADMIN \
  -i ipmi_password=ADMINPASS -i deploy_kernel=ea003044-f792-408b-b6cd-46af01528c65 \
  -i deploy_ramdisk=34103a9b-b706-4ba9-a929-f755dc8f4b1e -p cpus=2 \
  -p memory_mb=32000 -p local_gb=80
```

| 属性 | 值 |
| :--- | :--- |
| chassis_uuid | pxe_ipmitool |
| driver | pxe_ipmitool |
| driver_info | {'deploy_kernel': 'ea003044-f792-408b-b6cd-46af01528c65', 'ipmi_address': '10.0.0.5', 'ipmi_username': 'ADMIN', 'ipmi_password': u'******', 'deploy_ramdisk': '34103a9b-b706-4ba9-a929-f755dc8f4b1e'} |
| extra | None |
| name | |
| properties | {'memory_mb': 32000, 'local_gb': 80, 'cpus': 2} |
| uuid | 5e890ea-4f6a-4a3d-b74d-d28fdc6fc80 |

接下来，用户需要创建一个端口，以注册您打算在裸金属节点上使用的物理网络接口的所有 MAC 地址，以便 Ironic 知道应将哪个 MAC 地址与您刚刚创建的节点关联。以下操作继续使用我们的示例 UUID：

```bash
$ ironic port-create -a 5a:ba:01:02:f0:aa -n 5e890ea-4f6a-4a3d-b74d-d28fdc6fc80
```

| 属性 | 值 |
| :--- | :--- |
| address | 5a:ba:01:02:f0:aa |
| extra | () |
| node_uuid | 5e890ea-4f6a-4a3d-b74d-d28fdc6fc80 |
| uuid | 652be9f9-221b-4368-8912-b93381464f88 |

现在，您需要一个与这个物理硬件定义相关联的规格（flavor），如果您有一组相同的硬件阵列，那么其他类似硬件也需要关联。该规格应与您在 `ironic node-create` 命令中定义的硬件规格完全匹配。

```bash
$ openstack flavor create --ram 32000 --disk 80 --vcpus 2 my-baremetal
```

| 字段 | 值 |
| :--- | :--- |
| OS-FLW-DISABLED:disabled | False |
| OS-FLW-EXT-DATA:ephemeral | 0 |
| id | 80 |
| name | my-baremetal |
| os-flavor-access:is_public | True |
| ram | 32000 |
| rxtx_factor | 1.0 |
| swap | |
| vcpus | 2 |

完成此步骤后，您已准备好在硬件上启动镜像。由于这是首次使用该硬件，建议在部署镜像之前发出关闭它的命令：

```bash
$ ironic node-set-power-state 5e9809ea-4afa-4a1d-b7a4-d28fed6fc8b0 off
```

然后，您可以使用标准的 `openstack server create` 命令启动节点，请注意您需要指定硬件所在的网络，以便 Ironic 能够找到它。网络可以使用 `openstack network list` 命令找到。您希望在启动标准磁盘镜像（如 Ubuntu 服务器）时启动的规格。该镜像的 ID 可以使用 `openstack image list` 命令找到：

```bash
$ openstack server create --nic net-0d0fdc6b2-709-4050-876c-361b15f6977 \
  --image 73fc38f9-ae28-4b76-8b30-0d5f9929ad64 --flavor my-baremetal Ubuntu
```

> **提示**
> 在创建服务器时遇到困难？请确保在注册后节点的状态为 available。

## Ironic Inspector

定义所有硬件可能是一项繁琐的任务，即使您拥有一个已经拥有所有硬件库存的适当 CMDB。为了填补这一空白，Ironic 创建了一个相对较新的工具，称为 Ironic Inspector。该工具严重依赖于基础设施中的硬件，旨在利用硬件驱动程序提供的有关硬件（CPU、内存、磁盘等）的信息，以启用节点属性的自动特征化。然后使用这些信息将硬件与可用规格进行匹配，从而使服务器可用。请注意，由于 Inspector 从驱动程序获取信息，您仍然需要做一些基本的节点创建工作，以提供凭据，例如，如果您使用的是 iLO，则需要用户名、密码和可以访问接口的 IP 地址。

## 管理 Ironic

除了基本的硬件注册和将镜像启动到新硬件节点之外，你还可以使用 Ironic 通过 `ironic node-list` 命令检查机器的电源状态、可用性以及是否已进入维护模式。

可以使用 `ironic node-show name` 查看特定机器的详细信息，其中 `name` 是 `ironic node-list` 命令输出中的节点名称。

> **提示**
> 在 `ironic node-show` 命令中，也可以使用物理节点的 UUID 来替代名称。我们这里建议使用名称，因为它更简单，而且与许多其他 OpenStack 服务不同，Ironic 中的节点名称是唯一的。
>
> 另外请记住，Ironic 节点名称与实例 UUID 或使用该节点的实例名称无关。

Ironic 还支持节点清理功能，通过该功能可以删除数据，以为新实例准备硬件。此功能取决于你使用的驱动程序，并非所有驱动程序都支持此功能，但目前你可以确信所有 `agent`（代理）驱动程序都支持它。

有关 Ironic 的最新服务器管理方法，请参阅 `http://docs.openstack.org` 上的 Ironic 官方文档。该项目一直在开发以添加功能并提高稳定性。随着项目的成熟，你将看到来自硬件供应商的新驱动程序以及对类似 Ironic Inspector 所执行的流程自动化的更强支持。

## 社区

Ironic 开发社区主要由来自各家硬件公司以及关注 OpenStack 自动化硬件部署的各方的代表组成。该社区以友好著称，无论是从开发人员那里获得支持，还是向项目贡献自己的更改，都是简单明了的练习。

Ironic 团队也带有幽默感，利用“bare metal”（裸机）一词的双关语，取名为 Pixie Boots 的吉祥物，这是一只金属乐队鼓手熊。

![](img/8684900d708748f86bb043faa5589f9e_221_0.png)

## 总结

Ironic 裸机配置扩展了 OpenStack 的工具集，从虚拟化领域延伸到允许以类似虚拟机的方式管理和使用物理机器。在本章中，你了解了 Ironic 安装的基本选项，并学习了硬件注册以及启动第一个基于裸机的实例的过程。还简要介绍了裸机部署的基本维护，以及对构建和支持该项目的社区的一瞥。

# 11 控制容器

> 你永远无法通过与现有现实抗争来改变事物。
>
> 要改变某事，建立一个新模型，使现有模型过时。
>
> — R. Buckminster Fuller（巴克明斯特·富勒）

在当今的系统管理中，诸如 Docker、Kubernetes 和 Linux 容器（LXC）等容器是一个热门话题。随着容器的兴起以及 OpenStack 本身走向成熟，OpenStack 一直致力于与最新技术同步，以支持容器的运行和管理。

OpenStack 最初支持对单个容器实例进行最基本的类似于虚拟机的操作，但很快就转向在 OpenStack 内生成一个完整的项目来支持容器生态系统，允许使用容器生态系统中提供的本地工具来控制各种容器技术。

## 什么是容器？

容器可以被视为用于运行单个应用程序的微型、隔离的操作系统。它为主机系统上的进程提供了一定程度的隔离，同时共享内核等主机资源，并且通常避免了虚拟机（VM）技术中常见的硬件仿真。

容器的概念可能听起来很熟悉。容器化的新晋流行源自于一个包含 BSD 监狱（jails）、Solaris 区域（zones）、Linux-VServer 以及更近的迭代版本如 cgroups 和 Linux 容器（LXC）的系统历史。

近年来，几项变化增强了其流行度。首先是围绕容器创建的用户友好工具的开发，这主要得益于 Docker 的引入。此外，包含启动特定服务所需的所有软件依赖项的容器镜像也越来越受欢迎，这些服务在容器中运行。最后，有了 Kubernetes、Docker Swarm 和 Apache Mesos，现在有编排工具可用于管理这些容器，在某些环境中，其数量已达数千个。如今，单个容器可以轻松被视为完全可丢弃的，具备按需拆除和替换容器的能力。

能够交付小型、功能完整的容器镜像对开发人员和系统管理员来说也是一大利好。团队现在可以轻松地在容器中的这些隔离应用程序之间进行测试、部署和从主机到主机的迁移。鉴于 OpenStack 构建和扩展大型平台的现有能力，对容器的支持是一个自然的选择。

## 用途

公司希望在基础设施中使用容器有很多原因，从隔离到服务整合，再到更小的镜像和更快的启动时间。如果一个组织已经使用 OpenStack 来管理其基础设施的其他组件，那么将其用于容器通常也是很有价值的。

## 公有云公司

一家已经在基础设施中利用虚拟机的公有云公司可能选择同时提供 Docker 或 Kubernetes。通过使用 Magnum（在本章后面讨论），他们可以利用现有的 OpenStack 框架，并轻松引入其各自的编排引擎，例如 Docker Swarm。通过建立此框架，客户可以配置和部署自己的容器组，并通过 OpenStack 和本地工具进行控制。向客户提供资源选项也可以在其他方面使云公司受益——因为它们是共享资源，一台服务器上容纳的容器将比虚拟机更多。

## 在线游戏公司

一家已经使用 OpenStack 运行虚拟机并通过 Web 交付内容的游戏公司，可能对使用容器感兴趣，以便快速开发、测试、部署和迭代他们制作的游戏。在容器中部署变更所带来的灵活性，使开发人员能够在不一定要在生产环境中的情况下处理规模和高可用性问题。使用更小、针对进程且具有可移植性的容器，可以在本地帮助复制生产环境。开发速度的增加将帮助更快地向玩家提供更多功能。能够运行比虚拟机更多的容器也改变了部署的方式。除了确保维持高可用性之外，如果你只想向用户子集推出游戏变更该怎么办？如果你运行的实例更多，你对百分比的控制就精细得多。

> **注意**
> 在研究容器和 OpenStack 时，你可能会了解到既有非正式的也有官方的努力，试图在容器中运行 OpenStack 本身。然而，本章仅关注为支持容器管理所做的工作，以处理你的基础设施向用户提供的进程。

![](img/8684900d708748f86bb043faa5589f9e_226_0.png)

*图 11.1 带有容器的控制器和计算节点。一个控制器节点，运行着多个计算节点：标准的带有 KVM 的 libvirt 虚拟机，以及专注于容器的带有 LXC 和 Docker-Nova 驱动程序的 libvirt。*

## Nova 的容器驱动程序

OpenStack 与容器的故事始于早期，一系列直接与特定容器技术交互的计算驱动程序。首先，是使用 libvirt（OpenStack 已支持）与 LXC 的能力。然后是 Nova-Docker 驱动程序，它允许用户像使用其他虚拟化技术一样使用 Docker，并通过 Nova 计算启动 Docker 实例。在这种模型中，你还需要为这些中的每一个设置计算节点。因此，你可能有一个运行由 libvirt 驱动的 KVM 标准虚拟机的节点，另一个使用 libvirt 和 LXC 的节点，以及第三个使用 Nova-Docker 驱动程序的节点（参见图 11.1）。

不幸的是，这些有一些非常明确的局限性。既然你把容器当作虚拟机，你的工具反映的是你会对完整虚拟机运行的命令——你失去了容器特定的工具。由于容器是面向进程而非面向服务器的，这意味着需要一种非常不同的方法才能获得使用容器的全部价值。

这就是 Magnum 项目发挥作用的地方。

## Magnum

OpenStack Liberty 版本是 Magnum 的第一个生产就绪版本。Magnum 提供了对容器的更完整支持。该项目还寻求在部署 OpenStack 中的容器时提供一致性，同时保留使用每个受支持容器技术特定功能的能力。这意味着使用 Heat（在第 1 章“什么是 OpenStack？”中简要介绍）进行编排的通用机制，使用 Keystone 进行身份管理的单独集群的多租户，以及使用 Neutron 进行多主机网络。这也意味着每个服务都由 Magnum 以相同的方式处理，通过使用 Magnum API 创建栈（在下一节定义并在图 11.2 中显示），每个容器编排引擎（COE）在其中运行。通过允许 OpenStack 管理网络和在 OpenStack 本身之外超出你所做的事情的基础设施，容器管理变得 considerably 简单得多。

![](img/8684900d708748f86bb043faa5589f9e_227_0.png)

为了对每个容器编排引擎（COE）进行控制，可以使用针对每个引擎的本地 API 和工具，因此，如果你希望使用 Docker API，或者使用 Kubernetes 的原生命令行客户端 `kubectl` 来管理你的容器，这些都是完全可以做到的。Mitaka 版本包含对 Docker Swarm、Kubernetes 和 Apache Mesos 等 COE 的支持。

## Magnum 概念

正如你在图 11.2 中看到的，Magnum 拥有一个“Bays（港湾）”的概念，特定的 COE 将在此运行。除了 Bays 之外，Magnum 还具有容器和节点的概念（适用于所有容器），而对于 Kubernetes 还有额外的概念。宽泛地说，你拥有以下概念：

- **Container（容器）**：运行你的进程的容器。
- **Node（节点）**：港湾的成员，这是实际执行工作的裸金属服务器或虚拟机。
- **Bay（港湾）**：一组调度工作的节点对象的集合，这是你的 COE 所在的地方。

图 11.3 展示了这三个概念之间的关系。

更多的支持正在定期添加中。例如，如果你使用的是 Kubernetes，你还会有 Pod（豆荚/容器组）的概念，它是一组运行在一台物理机或虚拟机上的容器，作为一个层位于你的容器和节点之间，并且也可以支持复制控制器。

![](img/8684900d708748f86bb043faa5589f9e_228_0.png)

图 11.3 容器、节点和港湾

## 安装 Magnum

在撰写本文时，Mitaka 的 Magnum Puppet 模块仍在开发和测试中，因此很快就会有一种通过 Puppet 驱动的方式为你的基础架构配置 Magnum。截至撰写之时，尝试 Magnum 的最佳方式是部署我们在第 5 章“部署基础（Foundations for Deployments）”中讨论的 Foundations 框架，并配合一个使用 Magnum 的自定义计算节点。

## 总结

容器是一个热门话题，OpenStack 已正面应对了这一挑战。它很早就开始支持容器特定的 Nova 计算驱动。我们简单介绍的 Magnum 项目，则为当今常见的容器技术（包括 Docker、Kubernetes 和 Apache Mesos）提供了更全面的支持。

# 扩展与故障排除

熟悉 OpenStack 的各种部署类型只能让你走那么远。一旦你有了用例并建立了一个基本的云，你可能希望扩展该云，并将有扩展你的架构的需求，无论这意味着是添加更多存储节点还是增强计算集群的性能。故障排除也是任何 OpenStack 操作员工具包中至关重要的一部分。部署方案差异很大，每个环境都可能有一些细微差别，你必须知道如何处理。最后，OpenStack 生态系统中的各种供应商存在以支持你的更大规模部署，并用公有云服务增强它。

# 12

## 完整的云

> Two drifters
> Off to see the world,
> There's such a lot of world
> To see.
> Johnny Mercer, Moon River

这本书中的最后一个场景将我们在前面独立场景中呈现的所有部分组合在一起。你将能够看到 Cinder 块存储和 Swift 对象存储如何也输入到 Ceilometer 遥测中，并且能够在你的实例中同时使用 Cinder 块存储和 Swift 对象存储。当我们把这些部分组合在一起时，我们也会谈谈在这些场景之外的扩展。

## 用途
