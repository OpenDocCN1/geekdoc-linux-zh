
iSCSI 在 `RFC3720` 中进行了正式规定。与大多数 RFC 不同，该规范长达数百页，主要原因在于底层 SCSI 协议十分复杂。在大多数情况下，iSCSI 管理都很简单，除非你使用可选的 Internet 存储名称服务（`iSNS`）来对存储资源进行结构化管理和发现。`iSNS` 在 `RFC4171` 中定义，是将光纤通道的管理和发现协议改编到 IP 上，因此它主要适用于希望同时使用光纤通道和 iSCSI 的站点。

iSCSI 可以在 `IPsec` 上运行，尽管这不是必需的。如果不使用 IPsec 隧道，数据块本身不会被加密。根据 `RFC3720`，未使用 IPsec 的连接必须至少使用 12 个字符长的 CHAP 密钥。

目标和发起方都具有 iSCSI 名称，并且定义了几种命名方案。常见使用的名称是 iSCSI 限定名称（`IQN`），其格式如下所示的奇怪格式：

```
iqn.yyyy-mm.reversed_DNS_domain: arbitrary_name
```

在大多数情况下，冒号之前的部分都是固定的（即本质上无关紧要）前缀，其特征在于你的站点。你在 IQN 的 `arbitrary_name` 部分实现自己的命名方案。月份和年份（`mm` 和 `yyyy`）限定 DNS 域，以防止域所有权变更的可能性。使用原始 DNS 注册日期。实际名称看起来像这样：

```
iqn.1995-08.com.example.disk54.db.engr
```

尽管 IQN 名称格式很具体，但前缀反映你的实际 DNS 域或开始日期并不重要。大多数 iSCSI 实现默认使用厂商的域作为 IQN，这工作得很好。参与服务关系的 IQN 甚至不需要具有匹配的前缀。

### 从 iSCSI 卷启动

如果你打算将重要数据放在 SAN 上，是否会希望完全消除本地硬盘？不仅可以消除管理本地磁盘所需的大多数特殊程序，而且还可以允许管理员通过简单重启“交换”启动驱动器，使即时升级和多种启动配置即使对于 Windows 系统也触手可及。

不幸的是，将 iSCSI 卷用作启动设备并不得到广泛支持。至少，不是很直接，也不是主流功能。各种 Linux 项目都尝试过，但实现必然与特定硬件和特定 iSCSI 发起程序软件绑定，而且没有当前的 iSCSI 启动项目与现在占主导地位的发起程序软件 `Open-iSCSI` 配合。同样，Solaris 和 OpenSolaris 的 iSCSI 启动支持正在开发中，但目前还没有可投入生产的解决方案。

在我们的示例系统中唯一的例外是 AIX，它有着良好的 iSCSI 支持历史。运行在 POWER 硬件上的 AIX 5.3 及更高版本完全支持通过 IPv4 进行 iSCSI 启动。

### iSCSI 发起程序的厂商特定信息

Linux 至少有四种不同的 iSCSI 发起程序实现。其中一些已经停止，其他则合并了。到目前为止，似乎唯一的幸存者是 `Open-iSCSI`，它是我们示例 Linux 发行版中打包的标准发起程序。要使其运行，在 Ubuntu 和 SUSE 上安装 `open-iscsi` 包，在 Red Hat 上安装 `iscsi-initiator-utils` 包。

该项目的网站是 `open-iscsi.org`，但不要去那里寻找文档。除了 `iscsiadm` 和 `iscsid` 的手册页之外，似乎没有其他文档，它们分别代表系统的实现和管理接口。不幸的是，Open-iSCSI 的管理模型最好被描述为“富有创造性”。

在 Open-iSCSI 的世界中，“节点”是一个 iSCSI 目标，即用 IQN 命名的对象。Open-iSCSI 在 `/etc/iscsi/nodes` 目录下的层次结构中维护其所知的节点数据库。单个节点的配置参数存储在此树中。默认值设置在 `/etc/iscsi/iscsid.conf` 中，但它们有时会被复制到新定义的节点中，因此其功能并不完全可预测。设置每个目标参数的过程很痛苦；`iscsiadm` 通过让你一次只更改一个参数并要求你在每条命令行上列出 IQN 和服务器来折磨你。

该系统的救赎之处在于 `iscsid.conf` 和所有数据库文件只是可编辑的文本文件。因此，明智的做法是使用 `iscsiadm` 来完成它擅长的少数事情，并绕过它来完成其他事情。

要将系统设置为使用单个用户名和密码对所有 iSCSI 目标进行简单、静态操作，首先编辑 `iscsid.conf` 文件并确保以下行按所示配置：

```
node.startup = automatic
node.session.auth.authmethod = CHAP
node.session.auth.username = chap_name
node.session.auth.password = chap_password
```

我们将这些行一起显示，但在实际文件中它们会被分隔。文件实际上注释得相当不错，并且包含各种被注释掉的配置选项。确保不要引入重复项。

接下来，将 `iscsiadm` 指向你的目标服务器，让它通过读取该服务器的目录来为每个发现的目标创建节点条目。在这里，我们将配置名为 `test` 的目标，该目标来自名为 `iserver` 的服务器。

```
ubuntu$ sudo iscsiadm -m discovery -t st -p iserver
192.168.0.75:3260,1 iqn.1994-11.com.admin:test
```

`iscsiadm` 为每个目标在 `/etc/iscsi/nodes` 中创建一个子目录。如果有你不想处理的 target，完全可以 `rm -rf` 它们的配置目录。如果服务器提供许多目标，而你宁愿只指定想要的那个的详细信息，也可以这样做：

```
ubuntu$ sudo iscsiadm -m node -o new -p iserver
    -T iqn.1994-11.com.admin:test
New iSCSI node [tcp:hw=default,ip=,net_if=default,iscsi_if=default]
iserver,3260,-1 iqn.1994-11.com.admin:test added
```

奇怪的是，这两种方法实现了类似的结果，但在 `/etc/iscsi/nodes` 下创建了不同的层次结构。无论你使用哪个版本，请检查生成的文本文件

是层次结构的叶子节点，以确保配置参数设置得当。如果你手动输入了目标，可能需要手动将属性 `node.startup` 设置为 `automatic`。

然后你可以使用 `iscsiadm -m node -l` 连接到远程目标：

```
ubuntu$ sudo iscsiadm -m node -l
Logging in to [iface: default, target: iqn.1994-11.com.admin:test, portal:
192.168.0.75,3260]
Login to [iface: default, target: iqn.1994-11.com.admin:test, portal:
192.168.0.75,3260]: successful
```

你可以通过运行 `fdisk -l` 验证系统现在是否看到了额外的磁盘。（iSCSI 磁盘的设备文件命名方式与任何其他 SCSI 磁盘相同。）如果你按照上述描述设置了配置文件，连接应该会在启动时自动恢复。

对于 Linux 系统上的 iSCSI 目标服务，首选实现是托管在 `iscsitarget.sourceforge.net` 的 iSCSI Enterprise Target 包。它通常作为名为 `iscsitarget` 的包提供。

Solaris 包含目标和发起程序包；两者都是可选的。所有与 iSCSI 相关的包名称中都有“iscsi”。对于发起程序端，安装包 `SUNWiscsi`；之后你必须重新启动。

没有配置文件；所有配置都通过 `iscsiadm` 命令进行，该命令的语法相当奇怪。四个顶级动词（`add`、`modify`、`list` 和 `remove`）可以应用于发起程序配置的各种不同方面。以下步骤执行发起程序整体的基本配置并连接到服务器 `iserver` 上的目标。
