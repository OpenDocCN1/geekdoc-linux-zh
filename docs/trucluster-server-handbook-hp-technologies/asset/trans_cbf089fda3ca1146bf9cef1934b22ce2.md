

## 22.6 更换失败的仲裁磁盘

如果集群处于运行状态时仲裁磁盘发生故障，只要磁盘丢失不会导致集群失去仲裁，就可以在线更换它。

由于我们没有一个即将损坏的仲裁磁盘，我们将物理移除仲裁磁盘以说明如何更换它。如果您对集群在检测到仲裁磁盘出现问题时将看到的错误感兴趣，我们将使用 evmwatch(8) 命令监控此操作。此外，为节省空间我们将按一个成员进行过滤——两个成员都会记录事件，因此您会为每个成员看到相同的事件。并且一些重复的事件已被删减。

```
# export EVM_SHOW_TEMPLATES='@host) @name\n'
# evmwatch -f "host molari" -c evmshow -f "[\"%T\"]"

[08:44:53] (molari) sys.unix.binlog.hw.scsi._hwid.106
SCSI event

[08:44:59] (molari) sys.unix.hw.state_change.unavailable.disk._hwcomponent.SCSI$WID0c0000080000e100189f1f._hwid.106
Component SCSI$WID0c0000080000e100189f1f._hwid.106
is in the unavailable state (HWID=106)

[08:44:59] (molari) sys.unix.hw.no_connections.disk._hwid.106
Connectivity has been lost for device (HWID=106 lid=5 b1=3/3/0)

[08:45:09] (molari) sys.unix.binlog.hw.scsi._hwid.106
SCSI event

[08:45:14] (molari) sys.unix.clu.cnx.qdisk.loss
CNX MGR: Cluster quorum disk 19,240 has become unavailable due to a read error (status 5)

[08:45:14] (molari) sys.unix.clu.drd.server_leave._hwid.106
DRD: Removed (unmapped) DRD server molari

[08:45:14] (molari) sys.unix.syslog.kern
vmunix: CNX QDISK: Cluster quorum disk 19,240 has become unavailable due to a read error (status 5).

[08:45:15] (molari) sys.unix.clu.drd.server_add._hwid.106
DRD: Added (mapped) DRD server molari

[08:45:15] (molari) sys.unix.clu.drd.new_accessnode._hwid.106
DRD: Server sheridan selected for device 106

[08:45:15] (molari) sys.unix.clu.drd.new_accessnode._hwid.106
DRD: Server sheridan selected for device 106

[08:45:15] (molari) sys.unix.binlog.hw.scsi._hwid.106
SCSI event

[08:45:15] (molari) sys.unix.syslog.kern
vmunix: CNX QDISK: Quorum disk lost, removing 1 vote.

[08:45:15] (molari) sys.unix.clu.drd.no_accessnode._hwid.106
DRD: No server found for device 106
```

# 1. 移除仲裁磁盘。

```
# clu_quorum -d remove
Collecting quorum data for Member(s): 1 2

Quorum disk successfully removed.
```

EVM 应会记录此操作的发生。

```
[08:46:10] (molari) sys.unix.syslog.kern
vmunix: CNX QDISK: Bad close status (6) on device 19, 240.

[08:46:10] (molari) sys.unix.syslog.kern
vmunix: CNX MGR: Delete quorum disk operation completed with quorum.
```

# 2. 验证仲裁磁盘是否已移除。

```
# clu_quorum | grep "Quorum disk"
Quorum disk: Not Configured
```

# 3. 查找失败设备的 HWID。

EVM 事件会记录出现故障的组件，但也可以使用 hwmgr(8) 命令找到它。

```
# hwmgr view device -dsk dsk4
HWID  Device Name     Mfg      Model          Location
------------------------------------------------------------
106:  /dev/disk/dsk4c  COMPAQ   8D009635C3     bus-3-targ-3-lun-0
```

# 4. 移除失败的组件。

```
# hwmgr del -id 106
hwmgr: Delete operation was successful
```

EVM 将会看到如下内容：

```
[08:46:59] (molari) sys.unix.hw.deregistered.undefined._hwid.106
A hardware component has been de-registered (HWID=106)
[08:46:59] (sheridan) sys.unix.hw.deregistered.undefined._hwid.106
A hardware component has been de-registered (HWID=106)
[08:46:59] (molari) sys.unix.syslog.kern
vmunix: drd_delete_device; received status 16 when attempting to delete hwid 106.
```

```
[08:47:01] (molari) sys.unix.syslog.daemon
syslog: hotswapd: subsystem hwc may have successfully run the command '/sbin/dsfmgr -Z rm_cluster_hwid 106 461197741623797587'
[08:47:02] (molari) sys.unix.syslog.daemon
syslog: hotswapd: subsystem hwc may have successfully run the command '/sbin/dsfmgr -Z rm_local_hwid 106 4612247179486683987'
```

# 5. 更换磁盘。

此时您可以物理更换磁盘，或识别另一块可作为仲裁磁盘使用的磁盘。在本示例中，我们将把磁盘重新插回。

# 6. 扫描新组件。

使用 hwmgr 命令识别新设备。

```
# hwmgr scan component -category disk -cluster
hwmgr: Scan request successfully initiated
hwmgr: Scan request successfully initiated
```

EVM 将会看到类似于下面的事件。

```
[08:48:29] (sheridan) sys.unix.hw.scan_completed.platform_hwid.56
A hardware scan has just completed
[08:48:30] (molari) sys.unix.hw.scan_completed.platform_hwid.1
A hardware scan has just completed
[08:48:46] (molari) sys.unix.binlog.hw.scsi
SCSI event
[08:48:46] (molari) sys.unix.hw.registered.disk_hwid.107
A hardware component has been registered (HWID=107)
[08:48:46] (molari) sys.unix.sysman.station_update.MEMBER
SysMan Station: daemon on host molari.fafrak.com has written new serialization files. These files allow the daemons to communicate state and topology changes.
[08:48:47] (sheridan) sys.unix.hw.registered.disk_hwid.107
A hardware component has been registered (HWID=107)
[08:48:49] (molari) sys.unix.hw.cluster_attribute_change.disk_hwid.107
A change has occurred in a cluster attribute for device (HWID=107 lid=5)
[08:48:50] (sheridan) sys.unix.hw.cluster_attribute_change.disk_hwid.107
A change has occurred in a cluster attribute for device (HWID=107 lid=6)
[08:48:51] (molari) sys.unix.hw.dev_base_name_changed.disk_hwid.107
Device base name changed from "unknown" to "dsk12" (HWID=107)
[08:48:51] (sheridan) sys.unix.hw.dev_base_name_changed.disk_hwid.107
Device base name changed from "unknown" to "dsk12" (HWID=107)
[08:48:54] (molari) sys.unix.syslog.daemon
syslog: hotswapd: subsystem hwc may have successfully run the command '/sbin/dsfmgr -Z cr_new 4612491815432330179'
```

