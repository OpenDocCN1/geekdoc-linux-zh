
现在，我们已为集群的系统磁盘配置了所有存储集，但有时我们需要从系统控制台查看和访问每个集群成员引导分区或引导磁盘。遗憾的是，这并非自动发生的事情。何时需要执行此操作？在 Tru64 UNIX 完全安装和配置之后、但在安装 TruCluster Server 之前。在 TruCluster Server 的安装和操作期间，需要从每个集群成员的系统控制台查看和访问每个集群成员的引导磁盘。

我们将使用系统控制台上的 `wwidmgr` 命令来查看并使每个集群成员的引导磁盘可见。如何操作？我们究竟在寻找什么？我们要查找的是我们在 RAID 存储阵列上创建的集群成员引导分区磁盘的标识符或 `wwid`。

在开始使用 `wwidmgr` 命令之前，请注意，如果集群成员是 AS1200、AS4x00、AS8x00、GS60、GS60E 或 GS140，控制台必须设置为诊断模式。

> 9 这仅适用于使用基于光纤通道的存储（HSG60 或 HSG80 控制器）。如果使用基于 SCSI 的存储，则可跳过此步骤。

```
P00>>> set mode diag
```

Console is in diagnostic mode

After using the `wwidmgr` commands, the system must be reinitialized to return to the SRM console. This is done using the `init` command at the console.

The following example shows how we discover and make viewable a cluster member's boot disk. This example assumes that a cluster has not been previously installed.

Moreover, for the purposes of this example, the cluster member's boot disk that we are interested in has an identifier of 1 and this maps to storage unit D1.

### Display existing devices at the system console.

```
P00>>> show dev
dkc0.0.0.7.0        DKCO            R2ZDD-LS  0306
dqa0.0.0.105.0     DQA0            CD-224E  9.5B
dva0.0.0.0.0       DVA0
eia0.0.0.9.1       EIA0            00-50-8B-AE-P3-23
pga0.0.0.7.1       PGA0            WWN 2000-0000-c924-7c58
pkb0.7.0.6.0       PKB0            SCSI Bus ID 7
pkb0.7.0.106.0     PKB0            SCSI Bus ID 7
pkc0.7.0.7.0       PKC0            SCSI Bus ID 7
--
```

### Use `wwidmgr` to clear any `wwid` entries and check for the reachability of devices.

```
P00>>> wwidmgr -clear all
```

```
P00>>> init
```

```
P00>>> show ww*
wwid0
wwid1
wwid2
wwid3
```

```
P00>>> show n*
N1
N2
N3
N4
```

The `wwidmgr -clear all` command cleared the stored Fibre Channel `wwid1`, `wwid2`, `wwid3`, `wwid4`, `N1`, `N2`, `N3`, and `N4` console variables.

```
P00>>> show wwid*
wwid0 1 1 WWID:01000010:6000-1fe1-0001-6950-0009-1420-0755-0048
wwid1
wwid2
wwid3
```

In this example, we see by the `show wwid*` command that the `wwid0` console variable is set to the cluster member's boot disk.

```
P00>>> show n*
N1 50001fe100016952
N2
N3
N4
```

Let's also take a quick look at the HSG80 controller:

```
HSG> show this
Controller:
HSG80 2G14100634 Software V8F-8, Hardware E16
NODE_ID = 5000-1FE1-0001-6950
ALLOCATION_CLASS = 0
SCSI_VERSION = SCSI-3
Configured for dual-redundancy with 2G14200755
    In dual-redundant configuration
Device Port SCSI address 7
Time: 29-JUL-2002 08:54:46
Command Console LUN is lun 0 (NOIDENTIFIER)
Host PORT_1:
    Reported PORT_ID = 5000-1FE1-0001-6951
    PORT_1_TOPOLOGY = FABRIC (fabric up)
    Address = 011000
Host PORT_2:
    Reported PORT_ID = 5000-1FE1-0001-6952
    PORT_2_TOPOLOGY = FABRIC (standby)
    Address = 011100
    NOREMOTE_COPY
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

As we can see from the `show n*` command at the SRM console vs. the `show this` command at the HSG80's console, the `N1` SRM console variable contains the `PORT_ID` of the controller that is serving out the cluster member's boot disk. This indicates accessibility through the HSG80 ports.

```
p00>>> show dev

dga1.1001.0.7.1          $1$DGA1          HSG80  V6F

dkc0.0.0.0.7.0          DKC0            R22DD-LS 0306
dqa0.0.0.0.105.0        DQA0            CD-224E 9.5B
dva0.0.0.0.0            DVA0
eia0.0.0.0.0            EIA0            00-50-8B-AE-F3-23
eia0.0.0.0.7.1          PGA0            WWN 2000-0000-c934-7c58
pka0.7.0.6.0            PKA0            SCSI Bus ID 7
pkb0.7.0.106.0          PKB0            SCSI Bus ID 7
pkc0.7.0.7.0            PKC0            SCSI Bus ID 7
...
```

A new device also shows up when we enter the `show dev` command. This will be the device that we use to boot the cluster node after the TruCluster Server software is properly installed and configured.
