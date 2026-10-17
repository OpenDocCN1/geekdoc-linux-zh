
此选项启用 `xend` 中的迁移功能。

`(xend-relocation-hosts-allow '^(localhost)$')`

此选项控制哪些主机被允许连接到 `xend` 以进行域迁移。默认情况下，只允许 `localhost` 连接。该选项以正则表达式作为参数。请查看配置文件以获取示例。

> 请注意，域迁移涉及两个 `xend`（当前主机和新主机）。你可能需要在两个系统上调整 `xend-config.sxp` 文件。

### 摘要

| 目标 | 摘要 |
| :--- | :--- |
| 1. 理解虚拟化概念 | 虚拟化技术将操作系统的运行实例与物理硬件分离。操作系统不再运行在物理机器上，而是运行在所谓的虚拟机中。多个虚拟机共享底层硬件的资源。<br>虚拟化允许你在单台物理机器上运行多个虚拟系统。 |
| 2. 理解 Xen 的工作方式 | 有两种不同类型的虚拟化：<br>- 完全虚拟化 (`Full-Virtualization`)<br>- 半虚拟化 (`Para-Virtualization`)<br>`Xen` 使用半虚拟化。它通过 API 提供对物理硬件的访问。 |
| 3. 安装 Xen | 在初始 SUSE Linux Enterprise Server 10 安装中，必须安装以下软件包：<br>- `xen`。此软件包包含 Xen 虚拟机监视器（Hypervisor）。<br>- `xen-tools`。包含 `xend` 和一组用于管理 Xen 系统的命令行工具。<br>- `kernel-xen`。此软件包包含一个修改后的 Linux 内核，该内核在 Xen 域中运行。<br>- `xen-doc-*`（可选）。各种格式的 Xen 文档。<br>安装 `xen` 会在 `grub` 配置文件中添加一个条目。 |
| 4. 使用 YaST 管理 Xen 域 | YaST 提供了一个模块，可用于创建和管理 Xen 域。该模块名为：`虚拟机管理 (Xen)`。<br>此模块提供了一种便捷的方式来创建和控制你系统上的 Xen 域。该模块可以从 YaST 控制中心的 `System` 部分启动，并且必须在运行于域 0 的 Linux 系统上运行。 |
| 5. 在命令行管理 Xen 域 | 每个 Xen 域都需要一个配置文件。通常位于 `/etc/xen/vm/`。<br>`xm` 是 Xen 域的核心管理工具。<br>要启动虚拟机，使用 `create` 命令。例如：<br>`xm create -c f SLES10.conf`<br>某些服务在 Xen 环境中不是必需的，可以删除。<br>- `insserv -r earlykbd`<br>- `insserv -r kbd`<br>- `insserv -r irq_balancer`<br>在 Xen 下，所有域都通过域 0 连接到物理网络。 |
| 6. 理解 Xen 网络 | 域 0 是在 Xen 系统上配置网络连接的中心点。<br>域 0 中的网络网桥用作虚拟交换机。<br>此网桥由 `xend` 设置和控制。 |
| 7. 迁移来宾域 | 虚拟化的一个优势是域可以轻松地从一个物理系统移动到另一个物理系统。在 Xen 中，此过程称为`域迁移`。可以使用 `xm` 的 `save` 和 `restore` 命令或 `migrate` 命令来迁移域。 |

## 第 9 节 iSCSI

Internet 小型计算机系统接口（iSCSI）是常规 SCSI 命令在 IP 上的实现。SUSE Linux Enterprise Server 10 允许作为 iSCSI 发起者（initiator）连接到 iSCSI 目标（target），或者作为 iSCSI 目标向其他 iSCSI 发起者提供存储空间。

### 目标

1. iSCSI 背景
2. iSCSI 配置

### 目标 1

### iSCSI 背景

SCSI 命令用于使系统与 I/O 设备（特别是存储设备）进行通信。Internet 小型计算机系统接口在 IP 上实现了常规 SCSI 命令。

使用 iSCSI 时，操作系统（iSCSI 发起者）不直接将 SCSI 命令发送到设备，而是发送到通过网络连接的另一个系统（iSCSI 目标）；然后该系统将 SCSI 命令重定向到实际的存储设备——例如分区、逻辑卷或文件。

这基本上就是 iSCSI 发起者（客户端）和 iSCSI 目标（服务器）之间的客户端/服务器连接。然而，与通常的客户端/服务器连接不同，通常只允许一个客户端连接到服务器。iSCSI 协议在 RFC3720 中进行了标准化。

使用 iSCSI 可以连接到远程存储，它可以是磁盘、逻辑卷或文件，它对于系统而言表现为一个本地磁盘。这也称为 SAN（存储区域网络）。与其他 SAN 解决方案相比，iSCSI 的优势主要在于成本方面。常见的 SAN 解决方案使用相对昂贵的 FC（光纤通道）硬件，而 iSCSI 可以利用现有的以太网网络。此外，许多 SAN 解决方案也提供 iSCSI 接口。

考虑到通过网络传输的数据量，确保有足够的带宽很重要，例如千兆以太网。通常为 iSCSI 连接设置专用网络是有意义的。

远程设备在 Linux 中作为常规 SCSI (`/dev/sdX`) 设备可用，并且应该使用 `ntdev` 选项进行挂载。你可以配置 iSCSI 目标，要求 iSCSI 发起者在连接时提供用户名和密码。

Linux 上拥有多种 iSCSI 解决方案，但它们默认均使用 3260 端口进行 iSCSI 连接。

## 目标 2：iSCSI 配置

RHEL4 和 SUSE Linux Enterprise Server 10 的 iSCSI 配置与维护在某些方面有所不同。

- Red Hat Enterprise Linux 4
- SUSE Linux Enterprise Server 10

### Red Hat Enterprise Linux 4

在 RHEL 中，从 Service Pack 2 开始支持 iSCSI。它由两个模块 `iscsi` 和 `scsi_transport_iscsi` 以及软件包 `iscsi-initiator-utils` 实现。

若要查看当前是否正在使用任何 iSCSI 设备，请使用命令 `iscsiadm -m session -I` 或类似的列表命令。

如果列出了任何设备，您应当分析并保存用于 iSCSI 连接的配置文件：`/etc/ietd.conf`、`/etc/icsi.conf` 和 `/etc/initiatorname.iscsi`。本节稍后将会详细描述这些文件的作用。

在迁移到 SUSE Linux Enterprise Server 10 之前，您应当使用命令 `service iscsi stop` 停止 iSCSI 守护进程。

您还应检查 `/etc/fstab` 中是否配置了任何 iSCSI 设备。

### SUSE Linux Enterprise Server 10

SUSE Linux Enterprise Server 10 可以配置为 iSCSI 目标（Target）和 iSCSI 发起端（Initiator）。您可以通过配置工具 YaST 或手动操作来完成此设置。

- 设置 iSCSI 目标
- 设置 iSCSI 发起端
- 在启动时自动挂载 iSCSI 目标

#### 设置 iSCSI 目标

您可以启动 YaST 并选择 **网络服务 > iSCSI 目标**，或者在控制台中以 root 身份输入 `yast2 iscsi-server` 直接启动 iSCSI 目标模块。

如果未安装 `iscsitarget` 软件包，YaST 将提示您安装：

![](img/63e88022bf135307e3eac051ad238b5b_414_0.png)

在 iSCSI 目标配置的主菜单中，有 3 个标签页可用。`服务` 是第一个；在这里您可以配置 iSCSI 的启动方式。对于大多数用户而言，`在启动时` 是正确的选择。

![](img/63e88022bf135307e3eac051ad238b5b_415_0.png)

如果启用了 SuSE 防火墙，您应选择 `在防火墙中开放端口` 以便访问 iSCSI 所需的端口。如果未启用防火墙，则无法选择该选项，如上图中所示。

在 `全局` 标签页上，您可以配置 iSCSI 目标与发起端在发现过程中的身份验证。

![](img/63e88022bf135307e3eac051ad238b5b_416_0.png)

默认情况下选中 `无身份验证`。这意味着任何 iSCSI 客户端都可以发现此目标。

`传入身份验证` 和 `传出身份验证` 之间的区别如下：

传入身份验证意味着 iSCSI 发起端负责身份验证。如果使用 `传出身份验证`，则 iSCSI 目标负责。使用挑战-握手身份验证协议（CHAP）进行身份验证。

在此定义的密码将以明文形式存储在配置文件中。

您也可以设置不使用身份验证（默认）的 iSCSI 环境。

在第三个标签页上，您可以配置您的 iSCSI 目标：
