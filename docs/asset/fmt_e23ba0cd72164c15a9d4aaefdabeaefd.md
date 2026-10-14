
（注：提供的 OCR 文本在第 694-697 页之间存在重复和乱码。上述文本代表了可用内容的逻辑流。）

## Juju

如果你想尝试为服务编写和创建 charm（守护符），你可以完全做到。在 https://juju.ubuntu.com/docs/write-charm.html 上有更多详细信息，帮助你学习该流程、语义以及如何将你的 charm 纳入 Juju Store。

Juju 有一个用于绑定包（bundles）的 charm 功能。一个包是一组具有特定配置和所有相应关系的服务，封装在一个方便的软件包中，可以一步到位部署这些服务。

### Juju GUI

Juju 提供可用的 GUI，如图 34.1 所示。你必须首先部署一个 Juju GUI 的 charm，然后使用本地 URL 访问它。由于该 charm 是新的并且可能会发生微变化，我们没有选择打印详情，而是让你跳转到 Charm 浏览器（Charm Browser），你可以直接从开发者那里了解它。请访问 http://jujuchcharms.com/charms/precise/juju-gui。

![](img/2a083394994f21b612810fd7c32a8def_698_0.png)

图 34.1 Juju GUI。

### Juju 快速启动

Juju 最近新增的功能是 `quickstart` 命令，它通过引导安装过程来帮助你上手，消除了手动操作过程中的大部分痛苦。Quickstart 帮助你输入设置本地云或与使用 OpenStack、Windows Azure 和 Amazon EC2 的提供商配合所需的配置信息。它会为你安装 Juju GUI。Quickstart 可以配合并部署 Juju charm 包。如果环境尚未进行引导（bootstrapped），Quickstart 将启动环境、安装 GUI，然后部署该包。

### 在 Mac OS X 和 Windows 上使用 Juju

你可以在你的 Mac 或 Windows 机器上使用 Juju 客户端来管理你的 Ubuntu 服务器。请访问 https://juju.ubuntu.com/install/ 下载客户端。

## Ubuntu 裸金属即服务 (MaaS)

Juju 的存在是为了向云端部署工作负载。Ubuntu 裸金属即服务（MaaS）被作为部署该云的第一步，当你自自己的硬件或你拥有裸金属配置控制权的硬件上创建云时使用。MaaS 是一组从 Ubuntu 服务器部署 Ubuntu 服务器的最佳实践集合。它旨在协助部署数十、数百甚至数千台云服务器。你直接将 Ubuntu Maas 安装在一台服务器的裸金属上，从那里，所有其他裸金属服务器都将被配置和设置；可以快速方便地实现整个数据中心。部署后，Maas 提供自动联邦和集成管理、监控和日志。你可以添加物理设备、删除它、在你的云中重新调整用途等。你可以动态地进行这些操作，根据需要扩展规模并管理资源。它强大且非常酷。

这些都来自标准的 Ubuntu Server 安装光盘，你可以按照第 1 章“安装 Ubuntu 和安装后配置”中描述的方式下载，只不过你需要的是服务器版本而不是普通版本的 Ubuntu。在本文编写时，Ubuntu 社区仍在为“裸金属即服务”创建文档（链接在下方的“资源”中给出），所以如果你对此感兴趣，请在此查看它们。

## Landscape

Landscape 是由 Canonical 提供的一款面向企业的系统管理和监控工具。它可以监控像本章讨论的那种 Ubuntu 云服务器。Landscape 是 Canonical 提供的名为 Ubuntu Advantage 的付费服务的一部分，并在第 35 章“管理服务器组”中有所描述。

## 参考文献

- http://cloud.ubuntu.com—Ubuntu 云计算的官方介绍。
- http://eucalyptus.com/resources/overview—Eucalyptus 的官方信息资源。
- http://aws.amazon.com/—Amazon Web Services 主页。
- http://www.linux-kvm.org/page/Main_Page—KVM（基于内核的虚拟机）的主页。
- http://open.eucalyptus.com/wiki/Euca2ooolsGuidev1.1—Euca2oools 用户指南。
- http://openstack.org—OpenStack 官方网站。
- http://www.canonical.com/enterprise-services/ubuntu-advantage/landscape/cloud-management—Canonical 的 Landscape 是用于 Ubuntu Cloud 和 Amazon EC2 实例的商业管理工具。
- http://juju.ubuntu.com—Juju 的官方 Ubuntu 文档。
- http://jujucharms.com/—官方 Ubuntu Juju Charm 浏览器。
- http://maas.ubuntu.com/—Ubuntu 和 MAAS 的官方 Ubuntu 文档。
- http://wiki.ubuntu.com/ServerTeam/MAAS—关于 Ubuntu 裸金属即服务的 Ubuntu 社区文档。

# 第 35 章 管理服务器组

本章对一些实用的工具进行了简要介绍，特别是对于管理大量服务器的人来说。这些工具是为系统管理员和开发者设计的——这些人负责维护两台及以上服务器的运行、管理它们的配置等。系统的增长已经到了通过单独管理每台服务器有时变得力不从心的程度，因此创建了一些工具，通过将工作简化为管理软件（由该软件反过来管理所有服务器），来减轻一些压力和复杂性。好吧，任何系统管理员或开发者都会告诉你这有点过于简化了，但已经很接近。

由于情况非常复杂，拥有正确的工具至关重要。本章概述了一些可以帮助你管理服务器组的工具。每种工具将根据其功能和使用方法进行讨论。

- Juju
- Puppet
- Chef
- Ansible

## Juju

一个非常适合本章的条目在第 34 章“云中的 Ubuntu”中有所介绍，因为它与 Ubuntu 紧密结合。它免费提供了管理服务器组所需的功能。如果你需要管理服务器组，它值得一看。

本章内容
- Juju
- Puppet
- Chef
- CFEngine
- 参考文献

## Puppet

Puppet 是一种用 Ruby 编写的配置管理工具。它旨在通过自定义声明式语言更容易部署服务器和扩展应用程序。它有开源和商业（闭源）版本。

Puppet 执行四项基本工作：第一，它提供了一个定义基础设施所需状态的地方；第二，Puppet 在执行之前模拟更改；第三，Puppet 自动强制执行状态，纠正配置漂；最后，Puppet 提供实际状态与所需状态之间差异的报告。

名为 Puppet Forge 的网站提供了可下载的模块，这些是用于自动化特定任务的 Puppet 代码。也可以创建和分享你自己的模块。

Puppet 的大部分功能在其付费版本中可用，该版本还包含一个良好的 GUI。开源版本可以配合 Amazon EC2 进行配置，管理操作系统和应用程序配置，让你使用 Puppet Forge 中的模块，并通过网络获得社区支持。如果你需要此更多的任何功能，请寻找其他产品，或付费使用 Puppet 的企业版本 Puppet Labs，它的成熟性和实用性享有盛誉。

开发 Puppet 的公司最近收购了 Cloudsmith (http://www.cloudsmith.com/)，这是一家制作基于 Puppet 的开发者工具的公司。这一发展将确保 Puppet 在市场上成为更有具竞争力的对手。

## Chef

Chef 同样是用 Ruby 编写的配置管理工具。它使用面向服务的架构来帮助自动化任务。对于 Chef，你编写配方（recipes）来定义你如何配置服务器或特定的服务器软件，例如 HTTP 服务器或数据库服务器。配方描述每个资源，例如应该运行的服务或应该安装的包，以及它们应该处于的状态。它确保了在所有服务器上维护或更新配置。

Chef 是开源的。然而，要真正使用它，你必须购买托管版本（Hosted）或可以在公司防火墙内安装的独立版本（Private），并签有服务合同。下载源代码并使其运行并非易事，而且在没有服务合同的情况下，对开源版本（Open Source）的支持是的。像 Puppet 一样，Chef 是成熟且受推的，如果你需要它提供的内容，它值得你花时间。

## CFengine

CFengine 可能是自动化基础设施最古老的选项了。它用 C 语言编写，因此可能比其他选项快一点。它管理服务器的构建、部署和管理，并执行一些非常有用的审计和报告。众所 way许多知名公司使用 CFengine，例如 AT&T、IBM、Pixar 和高通。

CFengine 有开源版和企业版。它们之间的差异不像某些其他选项那么极端，但同样，企业版拥有华丽的外观和一些非常实用的功能，对于大多数需要或想要获得这些额外益处的用户来说，这笔支出是值得的。

## Ansible

Ansible 是一个编排引擎。它负责配置管理、应用部署等。它是一个运行在 Linux 上的专用产品，最近获得了一定的关注。它声称易于使用，并且无需在这些设备上安装特殊软件即可管理设备。

## Landscape

Landscape 是由 Canonical 提供的面向企业级系统管理和监控工具。它是 Ubuntu Advantage 计划（www.canonical.com/enterprise-services/ubuntu-advantage）的一部分，这是一项付费服务。你可以作为 Canonical Ubuntu Advantage 的托管服务来运行 Landscape，也可以在本地安装。它可以监控本地服务器以及云服务器，例如第 34 章“云端 Ubuntu”中讨论的。

## 参考

- www.puppetlabs.com—Puppet 的官方网站。
- http://forge.puppetlabs.com/—Puppet Forge 的官方网站。
- www.opscode.com/chef/—Chef 的官方网站。
- //cfengine.com/—CFngine 的官方网站。
- http://www.ansibleworks.com/—Ansible 的官方网站。
- www.canonical.com/enterprise-services/ubuntu-advantage/landscape—Landscape 的官方网站。
- http://help.ubuntu.com/14.04/serverguide/index.html—Ubuntu 服务器指南。

# 第 36 章 使用域名命名系统 (DNS) 进行域名解析

人类喜欢给事物命名。我们给孩子、给宠物命名，也给无生命物体命名。汽车、船只和计算机也不例外。这对于网络化计算机来说尤其是如此。对我们大多数人来说，记住名字比记住数字更容易。当我们必须记住数字时，我们可以做到；我仍然记得我小时候住过的房子的电话号码。然而，当我们可以使用名字代替时，我们倾向于这样做；今天我忘了我女儿的手机号，因为号码被程序化在了我的手机里，我只需要在通讯录中选择她的照片就可以给她打电话。

像这样的助记设备是有用的，但它们必须将我们给的名字映射到它们实际使用的数字上。映射只是匹配，将单词与数字连接起来，使用户能够请求 http://google.com 并获取存储在 http://74.125.224.72/ 上的信息。

域名命名系统 (DNS) 将赋予网络化机器的人类可读名称转换为机器使用的 IP 地址。更多信息请参见第 17 章“网络”。

## 本章内容概要

- 理解域名
- 使用 BIND 设置 DNS 服务器
- 参考

在 IP 地址。DNS 双向工作。

当你使用在本章中讨论的 Bind 9 DNS 服务器软件设置 DNS 服务器时，你获得了为你所拥有的域名设置名称/IP 详情的能力，无论是你网络上的域名，还是通过 Namecheap.com 或 GoDaddy 等注册商购买的互联网域名。但是，这些注册商运行 DNS 服务器，并允许通过他们精美的 Web GUI 执行此设置。为什么有人有人自己做这些呢？有几个可能的原因：

- 你有一个内部网络，一个从网络外部无法访问的局域网，也称为 LAN。你的内部网络分配并使用私有 IP 地址，但你想通过为各种系统分配名称来让你的 LAN 用户更方便。这些域名不会由域名注册商分配，因为它们仅限内部使用；它们末尾不会包含 .com 或 .net 等顶级域名，且只能在网络内部使用。

- 你想通过缓存提高性能。大多数 DNS 查询由大量计算机共享。如果每台计算机不需要都连接到互联网并由你的互联网提供商的 DNS 服务器（或其他公共 DNS 服务器）解析其域名，而是可以从本地服务器获取这些信息，这可能会提高速度。对于我们大多数人来说这不是问题，但对于大型网络来说，这是一个巨大的收益。

- 你想禁止一个有害域名。也许有一封邮件发给了你公司的员工，其中包含一个传播病毒的特定网站链接，你想防止天真的内部网络用户访问该网站。你可以更改该域名所提供的 IP，将用户重定向到你编写的描述该问题的 HTML 页面。你的更改只会影响你内部网络上的计算机，所以这不会让你公司外的人生气，他们也永远不知道正在发生这种情况。

- 你在家里有一个本地网络。你想在登录每台计算机和执行更新时让生活更轻松一点，所以你想给每台计算机命名，并允许使用宠物名称而不是网络上的 IP 地址来访问每台计算机。

毫无疑问我们还可以想出其他例子。老实说，我们大多数人不需要设置或运行 DNS 服务器，但你是那种会读《Ubuntu Unleashed》之类的书籍并喜欢折腾新事物的人。本章将带你

## 理解域名

简单来说，域名是用于表示 IP 地址的字符字符串。域名旨在比数字字符串更容易记忆。通常，它们被设置成由点分隔的标签集。这些字母集中的每一个被称为一个标签。最右侧的标签表示最广泛的组，即顶级域名 (TLD)。右侧的每个标签都是子域。这里有一个例子：
