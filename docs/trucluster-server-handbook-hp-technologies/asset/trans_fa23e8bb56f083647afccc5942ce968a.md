

-   hwmgr_get(8) - 关于 get 和 set 命令选项的参考页。
-   hwmgr_show(8) - 关于 show 命令选项的参考页。
-   hwmgr_view(8) - 关于 view 命令选项的参考页。
-   hwmgr_ops(8) - 关于其他命令选项的参考页：add、delete、edit、locate、offline、online、power、redirect、refresh、reload、remove、scan、status、unconfigure、unindict、unload。

## 7.4.1 如何显示系统中的设备？

```
# hwmgr -view devices
HWID: Device Name        Mfg      Model            Location
------------------------------------------------------------
4:  /dev/kvm
30: /dev/disk/floppy0c                 3.5in floppy      fdi0-unit-0
40: /dev/disk/dsk0c     COMPAQ   BB009235B6       bus-2-targ-0-lun-0
41: /dev/disk/dsk1c     COMPAQ   BB009235B6       bus-2-targ-1-lun-0
45: /dev/disk/cdrom0c    COMPAQ   CRD-8402B        bus-0-targ-0-lun-0
```

### 注意：

hwmgr 命令选项可以缩写至唯一可识别的程度。例如：

```
# hwmgr -view devices
```

可以缩写为：

```
# hwmgr -v d
```

另外，请注意，主关键字不需要连字符（-），但后续选项需要。例如，“view”等同于“-view”，而“-dsf”选项必须包含“-”。

```
# hwmgr view device -dsf dsk3
```

你也可以只显示特定设备。例如，让我们只搜索系统上的磁带设备：

```
# hwmgr -v d -category tape
HWID: Device Name      Mfg      Model          Location
------------------------------------------------------------
75: /dev/ntape/tape0    COMPAQ   SDT-9000        bus-6-targ-0-lun-0
```

如前所述，许多命令选项可以聚焦于某个成员或整个集群。你怎么知道哪些选项可以聚焦于另一个成员或整个集群？问问 hwmgr 吧。

```
# hwmgr -help view dev
Usage: hwmgr -view devices
  [ -dsf <device-special-filename> ]
  [ -category <hardware-category> ]
  [ -member <cluster-member-name> ]
  [ -cluster ]
```

另一种使用 hwmgr 显示设备的方法是查看 SCSI 子系统。

```
# hwmgr -show scsi
HWID  SCSI   DEVICEID HOSTNAME DEVICE    DEVICE   DRIVER NUM DEVICE FIRST
      DEVICEID          TYPE      SUBTYPE OWNER   PATH   FILE   VALID PATH
------------------------------------------------------------
0:    0     sheridan  cdrom    none     0       1      (null)
40:   1     sheridan  disk     none     2       1      dsk0   [2/0/0]
41:   2     sheridan  disk     none     2       1      dsk1   [2/1/0]
45:   3     sheridan  cdrom    none     0       1      cdrom0 [0/0/0]
53:   4     sheridan  disk     none     0       1      (null)
54:   5     sheridan  disk     none     0       1      (null)
55:   6     sheridan  disk     none     0       1      (null)
56:   7     sheridan  disk     none     0       1      (null)
57:   8     sheridan  disk     none     0       1      (null)
59:   9     sheridan  disk     none     0       1      (null)
```

请注意上面输出中的“(null)”。这表示系统先前看到的一些设备没有活动路径。在这个特定实例中，存储柜未通电。让我们给存储设备通上电，然后重新运行该命令。首先，让我们扫描总线。

```
# hwmgr -scan scsi
hwmgr: Scan request successfully initiated
```

现在，让我们看看有什么变化。

```
# hwmgr -show scsi
HWID: SCSI DEVICEID HOSTNAME DEVICE TYPE DEVICE SUBTYPE OWNER DRIVER NUM PATH FILE DEVICE FIRST VALID PATH
0: 0 sheridan cdrom none 0 1 (null)
40: 1 sheridan disk none 2 1 dsk0 [2/0/0]
41: 2 sheridan disk none 2 1 dsk1 [2/1/0]
45: 3 sheridan cdrom none 0 1 cdrom0 [0/0/0]
53: 4 sheridan disk none 0 1 dsk2 [3/0/0]
54: 5 sheridan disk none 0 1 (null) [3/1/0]
55: 6 sheridan disk none 0 1 (null) [3/2/0]
56: 7 sheridan disk none 0 1 (null) [3/3/0]
57: 8 sheridan disk none 0 1 (null) [3/4/0]
59: 9 sheridan disk none 0 1 (null) [3/5/0]
```

请注意，我们现在看到了一条活动路径，但仍未看到设备名称。这时我们可以请 dsfmgr 命令帮我们一把。带有“-k”选项的 dsfmgr 命令会创建所有新检测到的设备。注意：这个额外的步骤本应是不必要的（在 V5.1A 中确实没有必要）。然而，在 V5.1（本例创建时的版本）中，它是必要的。

```
# dsfmgr -k
```

现在重新运行原始命令。

```
# hwmgr -show scsi
HWID: SCSI DEVICEID HOSTNAME DEVICE TYPE DEVICE SUBTYPE OWNER DRIVER NUM PATH FILE DEVICE FIRST VALID PATH
0: 0 sheridan cdrom none 0 1 (null)
40: 1 sheridan disk none 2 1 dsk0 [2/0/0]
41: 2 sheridan disk none 2 1 dsk1 [2/1/0]
45: 3 sheridan cdrom none 0 1 cdrom0 [0/0/0]
53: 4 sheridan disk none 0 1 dsk2 [3/0/0]
54: 5 sheridan disk none 0 1 dsk3 [3/1/0]
55: 6 sheridan disk none 0 1 dsk4 [3/2/0]
56: 7 sheridan disk none 0 1 dsk5 [3/3/0]
57: 8 sheridan disk none 0 1 dsk6 [3/4/0]
59: 9 sheridan disk none 0 1 dsk7 [3/5/0]
```

请注意，hwmgr 命令的“-view devices”选项（缩写为“-v d”）现在也能看到设备了。

