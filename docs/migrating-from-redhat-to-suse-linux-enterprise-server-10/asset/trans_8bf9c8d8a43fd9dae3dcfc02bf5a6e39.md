
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

如果未安装 iscsitarget 软件包，YaST 将提示您安装：

![](img/63e88022bf135307e3eac051ad238b5b_414_0.png)

在 iSCSI 目标配置的主菜单中，有 3 个标签页可用。**服务** 是第一个；在这里您可以配置 iSCSI 的启动方式。对于大多数用户而言，**在启动时** 是正确的选择。

![](img/63e88022bf135307e3eac051ad238b5b_415_0.png)

如果启用了 SuSE 防火墙，您应选择 **在防火墙中开放端口** 以便访问 iSCSI 所需的端口。如果未启用防火墙，则无法选择该选项，如上图中所示。

在 **全局** 标签页上，您可以配置 iSCSI 目标与发起端在发现过程中的身份验证。

![](img/63e88022bf135307e3eac051ad238b5b_416_0.png)

默认情况下选中 **无身份验证**。这意味着任何 iSCSI 客户端都可以发现此目标。

**传入身份验证** 和 **传出身份验证** 之间的区别如下：

传入身份验证意味着 iSCSI 发起端负责身份验证。如果使用 **传出身份验证**，则 iSCSI 目标负责。使用挑战-握手身份验证协议（CHAP）进行身份验证。

在此定义的密码将以明文形式存储在配置文件中。

您也可以设置不使用身份验证（默认）的 iSCSI 环境。

在第三个标签页上，您可以配置您的 iSCSI 目标：

![](img/63e88022bf135307e3eac051ad238b5b_417_0.png)

默认情况下已定义了一个 iSCSI 目标，但由于未配置后端，因此无法直接使用。您可以编辑此目标，也可以将其删除并创建一个新目标。

在添加 iSCSI 目标之前，您应当决定要使用的后端设备。您可以使用常规磁盘、逻辑卷或文件作为后端设备。为了演示配置，我们将使用一个大小为 1 GB 的文件，可以使用以下命令创建：

```bash
mkdir /srv/iscsi
dd if=/dev/zero of=/srv/iscsi/first-device bs=1M count=1024
```

选择 **添加** 按钮将打开以下对话框：

![](img/63e88022bf135307e3eac051ad238b5b_418_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_418_1.png)

在此对话框中，您可以定义 iSCSI 设备的名称和要使用的后端。若要在一台 iSCSI 目标上使用多个 LUN（逻辑单元号），您必须手动编辑文件 `/etc/ietd.conf`。

目标名称应在全球范围内具有唯一性。默认情况下，使用以下语法：

`iqn.YYYY-MM.reverse-domain-name:identifier`

`iqn`（iSCSI 限定名称）通常后跟设备创建日期和公司域名的反转顺序。标识符是可选的，可用于基于名称的识别，例如 “iscsi-database-target”。

在 **路径** 框中，您定义后端设备；在我们的案例中，这将 是 `/srv/iscsi/first-device`。

选择 **下一步** 将打开下一个对话框，您可以在此配置此目标的身份验证。

![](img/63e88022bf135307e3eac051ad238b5b_419_0.png)

默认情况下不使用身份验证。如果您为 **传入身份验证** 添加用户名和密码，则必须在 iSCSI 发起端设置中记住该用户名和密码。

选择 **下一步** 后，您可以查看新的 iSCSI 目标：

![](img/63e88022bf135307e3eac051ad238b5b_420_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_420_1.png)

选择 **完成** 后，设置将写入系统。

命令 `iscsitarget status`（或 `/etc/init.d/iscsitarget status`）显示 iSCSI 目标守护进程是否正在运行。如果正在运行，`cat /proc/net/iet/volume` 将显示您配置的 iSCSI 目标。

iSCSI 目标配置存储在 `/etc/ietd.conf` 中，并由 iscsitarget-daemon（IETd：iSCSI Enterprise Target Daemon）服务管理。

以下列表展示了一个包含两个目标的 `/etc/ietd.conf` 文件；其中一个使用设备 `/dev/sda6` 作为物理存储，另一个使用文件。注释解释了您可能希望为每个目标定义的进一步参数：

```
Target iqn.2006-10.com.digitalairlines:87813d1d-d58f ...
Lun 0 Path=/dev/sda6,Type=fileio
Target iqn.2006-10.com.digitalairlines:14736b2d-f00e ...
Lun 1 Path=/srv/iscsi/second-device,Type=fileio
# 可以访问此目标的用户。此处适用与发现用户相同的规则。
# 如果不想使用身份验证，请保持原样。
#IncomingUser joe secret
#OutgoingUser jim 12charpawswd
# 逻辑单元定义
# 至少必须定义一个逻辑单元。
# 块设备、常规文件、LVM 和 RAID 可以作为块设备
# 提供给发起端。
#Lun 0 Path=/dev/sdc,Type=fileio
# 此目标的别名
# Alias Test
# 各种 iSCSI 参数
# （目前并非所有参数都使用中，详情请参见 iSCSI 规范）
#MaxConnections	1
#InitialR2T		Yes
#ImmediateData	No
#MaxRecvDataSegmentLength 8192
#MaxXmitDataSegmentLength 8192
#MaxBurstLength	262144
#FirstBurstLength	65536
#DefaultTime2Wait	2
#DefaultTime2Retain	20
#MaxOutstandingR2T	8
#DataPDUInOrder	Yes
#DataSequenceInOrder Yes
#errorRecoveryLevel	0
#HeaderDigest	CRCS32,None
#DataDigest	CRCS32,None
# 各种目标参数
#WThreads	8
```

#### 设置 iSCSI 发起端

您可以启动 YaST 并选择 **网络服务 > iSCSI 发起端**，或者在控制台中以 root 身份输入 `yast2 iscsi-client` 直接启动 iSCSI 发起端模块。

如果未安装 open-iscsi 软件包，YaST 将提示您安装。

![](img/63e88022bf135307e3eac051ad238b5b_422_0.png)

安装完成后，将打开以下对话框：

![](img/63e88022bf135307e3eac051ad238b5b_423_0.png)

在 **服务** 标签页中，您可以配置 iSCSI 客户端是在启动时自动启动还是手动启动。

**已连接的目标** 标签页显示活动连接。但首先，您需要发现并配置一个 iSCSI 目标设备。为此，请选择 **已发现的目标** 标签页：

![](img/63e88022bf135307e3eac051ad238b5b_424_0.png)

目前未发现任何目标设备。使用 **发现** 按钮，您可以开始在特定 IP 地址上进行搜索。

![](img/63e88022bf135307e3eac051ad238b5b_425_0.png)

输入要扫描 iSCSI 目标设备的 IP 地址。如果发现过程需要用户名和密码，请在此处输入。默认情况下，无需使用任何身份验证。
