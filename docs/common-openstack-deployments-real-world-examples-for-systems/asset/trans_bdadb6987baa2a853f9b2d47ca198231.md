
11. 现在创建你的计算节点，配备 2G 内存和 1 个网卡：

```bash
$ sudo virt-install --connect qemu:///system -n compute --vcpus=2 -r 2048 \
--network=bridge=virbr0 --f /var/lib/libvirt/images/compute.qcow2 \
-c /var/lib/libvirt/images/ubuntu-14.04.4-server-amd64.iso --vnc \
--noautostart --os-type linux --os-variant ubuntu/trusty
```

当两台服务器都已启动并运行后，你可以通过 ssh 登录到它们，或者通过虚拟机管理器（参见图 A.1）进行操作，以按照第 5 章“部署基础”及其后续章节中定义的配置设置系统。

### 建议

为了避免通过虚拟机管理器执行所有命令，你可能希望在所有系统上安装 `openssh-server` 软件包。这将允许你使用 SSH 连接到这些机器，并使向其中粘贴命令变得更加方便。

此外，你安装的 Ubuntu 桌面环境附带了 Firefox 网页浏览器。你可以使用它与 OpenStack 仪表板 Horizon 进行交互，而无需安装任何额外的软件。

![](img/8684900d708748f86bb043faa5589f9e_262_0.png)

图 A.1 虚拟机管理器。你可以使用虚拟机管理器访问你创建的 KVM 实例。

## B 其他部署机制

在本书中，我们探索了使用 Puppet 进行各种 OpenStack 部署。然而，在庞大的 OpenStack 生态系统中，Puppet 只是你的选项之一。通过拥有多种部署机制，OpenStack 可以在你的组织中部署，而无需更换工具，或者使用与环境中其他部分不同的工具运行。

可以在 OpenStack 代码仓库 https://git.openstack.org/cgit/openstack/ 中浏览找到 OpenStack 社区自身包含的所有部署机制。

这里介绍的工具是最流行和最成熟的，但这个工具列表总是在变化，对于此处未列出的你最喜欢的工具，进行搜索以查看是否有可用的 OpenStack 部署说明或正在开发中的说明，总是值得的。

### Chef

OpenStack 项目的 git 仓库中包含 OpenStack 的 Chef 食谱（cookbooks）。它们都以 `cookbook-openstack-` 为前缀，并以它们部署的具体项目结尾。例如，你可以通过此地址找到计算（Nova）项目的 Chef 食谱：https://git.openstack.org/cgit/openstack/cookbook-openstack-compute/tree/。

每个仓库中的 `README.rst` 文件为每个项目提供参考。它们都包含有关食谱用法的一些基本说明，许多还链接到一个额外的仓库，该仓库描述了如何在完整的 OpenStack 部署环境中使用它。

### Ansible

OpenStack 项目的 git 仓库中还可以找到一系列 Ansible 剧本（playbooks），可直接从此处访问浏览：https://git.openstack.org/cgit/openstack/openstack-ansible/tree/。

与 Chef 和 Puppet 不同，Ansible 提供了一个单一的部署剧本，该剧本引入其他组件。`README.rst` 文件中包含了基本设置的说明，其中包括根据你打算进行的部署类型（从引导到单独运行剧本等）对可用脚本的一些介绍。

### SaltStack 及其他

其他开源配置管理工具，例如 SaltStack，如今也在其官方仓库中发布了 OpenStack 工具。这些由 OpenStack 社区之外的维护者维护，通过搜索这些项目的代码仓库和文档可以找到下载和使用说明。

### 特定供应商

涉及 Puppet、Chef 和 Ansible 等技术的社区驱动努力，近年来已发展到可用于生产环境的速度，但 OpenStack 过去在部署方面一直很复杂。正如第 14 章“供应商与混合云”中所述，供应商提供广泛的特定供应商部署机制。其中一些机制与供应商所称的自己的 OpenStack 发行版紧密集成，该发行版在其 OpenStack 产品中打包了大量其他工具。Red Hat 和 HPE 是拥有此类产品的公司之一。其他公司则专注于使用其部署工具来聚焦于部署过程，例如 Canonical 针对 Ubuntu 生态系统的 Juju。

由 OpenStack 基金会托管的 OpenStack Marketplace 提供了提供自己的 OpenStack 发行版和设备的供应商的详尽列表，网址为 http://www.openstack.org/marketplace/distros/。

![](img/8684900d708748f86bb043faa5589f9e_265_0.png)

## C 长期运行的 Puppet

对于书中的每个部署示例，我们都运行了一个设置脚本，然后运行 `puppet apply` 来应用清单（manifests）。这种方法对于逐个场景摸索以了解 OpenStack 在各种部署中的工作原理非常有用，但这并不是运行 OpenStack 的可维护方式。为了将书中的 Puppet 部署模块和 Hiera 转化为真正的 Puppet OpenStack 部署，有一些事项需要考量，并且需要进行一些更改。

### Puppet Master 还是无 Master？

从 Puppet 方面来看，你需要更改的第一个主要事项是，你可能不希望像在这里那样使用 `puppet apply` 来运行 Puppet。尽管一些 OpenStack 部署使用无 Master 的 Puppet，但它有一些缺点。首先，所有 Puppet 代码和 Hiera 数据都需要复制到每个节点并保持最新。你也不能在使用无 Master 的 Puppet 时使用诸如导出资源（https://docs.puppet.com/puppet/latest/reference/lang_exported.html）等功能。与无 Master 模式相比，使用 Puppet Master 运行 Puppet 也有一些优势。首先，它提供了一个单一位置进行更改，然后自动部署到每个节点。默认情况下，所有客户端每 30 分钟请求一次目录（catalog）并执行一次 Puppet 运行。这意味着在 30 分钟内，可以应用的更新和手动更改将被自动还原（只要被更改的资源由 Puppet 管理）。尽管无 Master 的 Puppet 也有一些优势，例如没有目录编译瓶颈，但在将本书提供的解决方案产品化之前，你需要至少确认你希望使用无 Master 模式，并权衡其利弊。

### Hiera

在本书中，我们使用 Puppet 中的一个键值工具 Hiera 来存储每个部署示例的偏好设置。出于简单性的考虑，本书中使用的 Hiera 几乎无法满足 Hiera 本应达到的定义。Hiera 本应允许基于层次结构暴露重叠的值。在本书中，我们使用的是一个简单的扁平文件。在任何实际部署中，你都需要一个真正的层次结构，该层次结构暴露诸如区域、节点类型以及节点是开发、预发布还是生产环境等层。想象一下，你可能希望开发环境的计算节点具有与生产节点不同版本的软件包的场景。这正是 Hiera 的用途。它甚至可用于在地理上分隔节点。欧洲的节点与美洲的节点将拥有不同的 NTP 和 DNS 服务器。关于 Hiera 的强大功能，请阅读 https://docs.puppet.com/hiera/1/。

### Hiera 中的密码

你需要解决的另一个问题是在 Hiera 中存储密码。未加密地将密码提交到 git 并不是个好主意，也是不安全的。使用 `hiera-eyaml` 后端是解决此问题的一种方案。密码在磁盘上将被加密，并在目录编译时解密（参见：https://puppet.com/blog/encrypt-your-data-using-hiera-eyaml）。其缺点是 Puppet Master 需要一个解密密钥，但这比明文有很大改进。还有其他解决方案需要考虑。请记住，管理持有你整个部署“钥匙”的密码应该是首要考量事项。Hiera 包含 OpenStack 管理员用户、RabbitMQ 和 MySQL 的密码，其中任何一个如果泄露，都将极其危险。

### 节点分类

如前所述，在本书中，你通过手动在给定机器上运行 `puppet apply` 来选择节点类型。这种方法扩展性不佳且容易出错。如果有人误将 `foundations_public_cloud.pp` 目录应用到计算主机上，你的 OpenStack 集群会发生什么？为了在生产环境中运行，你需要首先思考如何对 Puppet 进行节点分类（https://docs.puppet.com/pe/latest/puppet_assign_configurations.html）。这可以使用随 Puppet Enterprise（付费版）附带的 Puppet 控制台来完成，也可以使用 Hiera 和 `site.pp` 文件来完成。这是你在将此代码产品化时需要考虑的事项。

### 模块管理

主要考量之一是你如何管理 Puppet 模块并与上游保持同步。模块的版本由 Puppetfile 管理，然后由 Puppet 部署工具集 r10k 拉取。总体而言，随附本书的 Puppetfile 让你处于良好的状态。非 OpenStack 模块的版本锁定在特定的标签（tag）上，这意味着除非你主动移动它们，否则它们的代码不会“移动”。但每天都有新的模块被标记和发布。事实上，该 Puppetfile 中的许多标签可能已经过时。你将采用什么系统来更新这些标签并跟踪新发布？你将如何测试新模块？这些是你需要做出的关键考量。我建议，落后太多然后试图一次性对所有模块进行大规模更新并不是一个好计划。计划至少每隔几个月审查一次模块标签，看看是否可以升级。以下是一个固定在特定标签的模块示例：

```ruby
mod 'stdlib'
  :git => 'https://github.com/puppetlabs/puppetlabs-stdlib.git'
  :ref => '4.6.0'
```

