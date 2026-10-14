
```
[0] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1420-0755(ev:wwid)
[1] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1425-0755b(ev:none)
[2] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1425-0746(ev:none)
[3] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1425-004b(ev:none)
[4] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1425-0049(ev:none)
[5] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1425-0747(ev:none)
[6] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-9216-0029(ev:none)
[7] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-0926-0055f(ev:none)
[8] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-9216-0028(ev:none)
[9] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-9210-0827(ev:none)
```

```
P00>> init
```

```
P00>>> show ww*
wwid0 1 WWID:0100010:6000-1fe0-0001-6950-089-142005755048
wwid1
wwid2
wwid3
```

在此示例中，我们通过 "`show ww*`" 命令看到 `wwid0` 控制台变量设置为集群成员的启动磁盘。

```
P00>>> show n*
N1 5000fe100016952
N2
N3
N4
```

让我们快速查看 HSG80 控制器：

```
HSG* show this
Controller:
HSG80 ZG14100634 Software V8F-8, Hardware E16
  NODE_ID = 5000-1FE1-0001-6950
  ALLOCATION_CLASS = 0
  SCSI_VERSION = SCSI-3
  Configured for dual-redundancy with ZG21420755
  In dual-redundant configuration
  Device Port SCSI address 7
  Time: 29-JUL-2002 08:54:46
  Command Console lun is lun 0 (NOIDENTITY)
Host PORT_1:
  Reported PORT_ID = 5000-1FE1-0001-6951
  PORT_1_TOPOLOGY = FABRIC (fabric up)
  Address = 011100
Host PORT_2:
  Reported PORT_ID = 5000-1FE1-0001-6952
  PORT_2_TOPOLOGY = FABRIC (standby)
  Address = 011100
REMOTE_COPY
Cache:
  256 megabyte write cache, version 0012
  Cache is GOOD
  Unflushed data in cache
  CACHE_FLUSH_TIMER = 300 (seconds)
Mirrored Cache:
  Not enabled
Battery:
  NOUPS
  FULLY CHARGED
Expires: 15-FEB-2004
```

我们可以从 SRM 控制台的 "`show n*`" 命令与 HSG80 控制台的 "`show this`" 命令对比看出，`N1` SRM 控制台变量包含了提供集群成员启动服务的服务的 `PORT_ID`。这通过 HSG80 端口指示。

# 第 4 章

```
P00>> show dev
dga1.1001.0.7.1      $1$DGA1 HSG80 V8EF
dkc0.0.0.0.7               DKCO            RZ2DD-LS 0306
dqa0.0.0.105.0   DQAO            CD-224E 9.5B
dva0.0.0.0.0     DVAO            00-50-SB-AE-F3-23
eia0.0.0.9.1     EIAO            WWN 2000-0000-c924-7c58
pga0.0.0.7.1     PGAO
pka0.0.0.6.6       PKA0            SCSI Bus 7
pkb0.7.0.106.0   PKBO            SCSI Bus 7
pck0.7.0.7       PKCO            SCSI Bus 7
```

Bootfile:

| 功能描述 |

| :--- | :--- |

| Display | 显示系统配置表。 |

| Exit | 退出 LFU（重置）。 |

| List | 列出设备、版本、固件名称、更新版本。 |

| Update | 用可加载的数据镜像替换当前固件。 |

| Verify | 比较可加载镜像与硬件镜像。 |

| ? | 或帮助。滚动显示此功能表。 |

- 更新固件。

`UPD> update`

确认更新以下设备：

fb

t

pga0

srm

`[Y/(N) ] y`

> 警告：每个设备的更新可能需要几分钟才能完成。

不要取消！

fsb 正在更新到 3.2... 正在验证 3.2... 通过。

nt 正在更新到 5.71... 正在验证 5.71... 通过。

pga0 正在更新到 DS3.81A4... 正在验证 DS3.81A4... 通过。

srm 正在更新到 6.1-2... 正在验证 6.1-2... 通过。

`UPD> exit`

其实就是这些。

## 4.3.2 ECU 固件

对于某些带有扩展行业标准架构 (EISA) 总线的 AlphaServer，如果您添加了设备或该系统是双启动系统（带有 OpenVMS），则应运行 EISA 配置程序 (`ECU`)。

以下概述了如何更新 ECU 固件：

- 将 ECU 磁盘插入软磁盘驱动器。

- 从软磁盘驱动器启动系统。

- 按照屏幕上的指示显示主菜单。

- 从主菜单中选择以下菜单项：

  * CMOS 设置

  * 高级 CMOS 设置

  * 控制台选择：Digital Unix 控制台 (`SRM`)

- 按 `F10` 键保存您的选择。

- 关闭电源然后重新启动系统。

## 4.3.3 主机总线适配器固件

从 Alpha 固件更新版本 6.1 开始，主机总线适配器固件和 Alpha 固件同时更新。更新设备列表包含 KGPSA 主机适配器——即 `pga0` 设备。只需确保该设备的固件已更新即可。

## 4.3.4 HSZ/HSG RAID 阵列控制器固件

更新 HSZ/HSG RAID 阵列控制器固件应由 HP 现场工程师负责。只有真正清楚自己在做什么的客户才应尝试此更新，并且在对存储系统中可能存在的任何数据进行完整备份后进行。

支持 TruCluster Server 的最小 HSZ/HSG 固件版本如表 4-3 所示。

要确定您的 HSZ/HSG 控制器级别，请使用以下命令：

```
HSG> show this
Controller:
HSG80 ZG14100634 Software V86F-8 Hardware E16
...
```

在此示例中，`HSG80` 控制器处于 ACS 固件版本 `V86F-8`。`"-8"` 通常表示固件的补丁级别。适用于 HS ACS 固件的相同惯例和注意事项也适用于 HSG 系列控制器的 HSO 固件。

## 4.3.5 光纤通道交换机固件

同样，与 HSZ/HSG RAID 阵列控制器固件一样，只有 HP 现场工程师应对光纤通道交换机固件进行更新。

## 4.4 配置和验证集群互连硬件

实现集群需要一个专用的集群互连（Cluster Interconnect），所有集群成员都连接在其中。集群互连为虚拟私有网络提供了基础，允许所有成员之间进行通信。该集群互连在集群节点和成员之间提供了节点间通信（通过 `ICS¹²`）。TruClusterServer 软件在集群内部创建了此虚拟私有网络，该虚拟私有网络与集群互连提供的物理通信通道并存存在。

它是如何工作的？对于每个成员，集群软件会为集群互连创建一个虚拟网络设备。在 V5.1A 中，该设备命名为 `ic0`。在 V5.0a 和 V5.1 中，该设备命名为 `mc0`，因为当时仅支持内存通道（Memory Channel）适配器作为集群互连。无论何种，该设备都有自己的 IP 名称和 IP 地址，在建立系统在集群中的身份时会使用。
