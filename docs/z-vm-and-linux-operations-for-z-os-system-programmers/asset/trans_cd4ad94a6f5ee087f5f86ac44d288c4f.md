

有关两者的更多信息，请参考 *Devices Drivers, Features, and Commands, SC33-8289*。最新版本可在 Developerworks 网站上找到，网址为：
http://www.ibm.com/developerworks/linux/linux390/october2005_documentation.html

## Devices nodes and udev

Linux 内核将它所知的字符设备和块设备表示为一对数字，<major>:<minor>。某些主设备号为特定设备驱动程序保留，其他则在 Linux 启动时动态分配给设备驱动程序。例如，主设备号 94 始终是 DASD 设备驱动程序的主设备号，但通道连接磁带设备驱动程序没有固定的主设备号。一个主设备号也可以由多个设备驱动程序共享。

设备驱动程序使用 <minor> 号来区分各个物理或逻辑设备。例如，DASD 设备驱动程序为每个 DASD 分配四个次设备号：一个用于整个 DASD，另外三个用于最多三个分区。设备驱动程序根据设备驱动程序特定的命名方案为其设备分配设备名称。每个设备名称都与一个次设备号相关联。

历史上，Linux 在 /dev 目录中提供了一大套预定义的设备节点。大多数情况下，只使用了其中一小部分。从 Linux 2.6 开始，情况发生了变化：/dev 目录中只有少数预定义的设备节点；并且有一个用户空间守护进程 udev，负责在内核通知有新设备插入时动态在 /dev 中创建所需的设备节点。Udev 还可用于调整设备节点名称以适应组织的需要，或设置节点权限等。

有关 udev 功能的信息，请参阅 udev 手册页（man 7 udev）。

## /sys filesystem

在 Linux 中将设备上线后，设备驱动程序通过一个称为 /sys 的内存文件系统向用户空间公开其参数。

> **Note:** /sys 文件系统不存在于磁盘上。每次 Linux 客户机 IPL 时都会重新创建。
> 
> /sys 是 /proc 文件系统的继任者，后者仍存在以保持向下兼容。

/sys 文件系统允许初始化脚本或用户与驱动程序参数交互以查询或修改配置。

## 6.4.2 Disk management

### Enabling a disk in Linux

在新磁盘已定义、在目录中，并且已动态附加到客户机后（请参阅第 5.3.9 节“管理 DASD”，第 258 页所述），即可在 Linux 中启用它。

使用 lscss 命令，即 List Channel Subsystem，用于显示连接到系统的所有设备。示例 6-1 显示了在将磁盘作为设备 0200 附加之前和之后的 lscss 命令输出。

### Example 6-1 The lscss command output, before and after attaching new DASD to guest

```
lnxguill:~ # lscss
Device   Subchan. DevType CU Type Use  PIM PAM POM CHPID
------------------------------------------------------------
0.0.0191 0.0.0000 3390/0A 3990/E9     F0 F0 FF 52565A5E 00000000
0.0.0100 0.0.0001 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
0.0.0101 0.0.0002 9336/10 6310/80 yes 80 80 FF 00000000 00000000
0.0.0150 0.0.0003 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
[...]
lnxguill:~ # lscss
Device   Subchan. DevType CU Type Use  PIM PAM POM CHPID
------------------------------------------------------------
0.0.0191 0.0.0000 3390/0A 3990/E9     F0 F0 FF 52565A5E 00000000
0.0.0100 0.0.0001 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
0.0.0101 0.0.0002 9336/10 6310/80 yes 80 80 FF 00000000 00000000
0.0.0150 0.0.0003 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
[...]
0.0.0200 0.0.0012 3390/0C 3990/E9     F0 F0 FF 5054585C 00000000
lnxguill:~ #
```

此时，磁盘已被 Linux 看到，但必须启用它，操作系统才能使用它。磁盘使用 chccwdev 命令启用，如示例 6-2 所示，该命令由 IBM 提供，并在 s390-tools 软件包中提供。

### Example 6-2 Enabling a disk for Linux

```
lnxguill:~ # chccwdev -e 0.0.0200
Setting device 0.0.0200 online
Done
lnxguill:~ #
```

要启用设备，请使用 -e 开关；要禁用设备，请使用 -d 开关。当磁盘上线时，Linux 内核会为磁盘分配一个设备节点

