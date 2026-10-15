
```
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

此时，磁盘已被 Linux 看到，但必须启用它，操作系统才能使用它。磁盘使用 `chccwdev` 命令启用，如示例 6-2 所示，该命令由 IBM 提供，并在 s390-tools 软件包中提供。

### Example 6-2 Enabling a disk for Linux

```
lnxguill:~ # chccwdev -e 0.0.0200

Setting device 0.0.0200 online

Done

lnxguill:~ #
```

要启用设备，请使用 -e 开关；要禁用设备，请使用 -d 开关。当磁盘上线时，Linux 内核会为磁盘分配一个设备节点

```
Initrd 映像：/boot/initrd-2.6.16.21-0.8-default
共享库：lib64/ld-2.4.so lib64/libacl.so.1.1.0
lib64/libattr.so.1.1.0 lib64/libblkid.so.1.0 lib64/libc-2.4.so
lib64/libcom_err.so.2.1 lib64/libc-2.4.so lib64/libext2fs.so.2.4
lib64/libhistory.so.5.1 lib64/libncurses.so.5.5 lib64/libpthread-2.4.so
lib64/libreadline.so.5.1 lib64/librt-2.4.so lib64/libuuid.so.1.2
驱动程序模块：dasd_mod dasd_eckd_mod dasd_fba_mod
DASD：0.0.0100(ECKD) 0.0.0101(FBA) 0.0.0150(ECKD) 0.0.0200(ECKD)
文件系统模块：jbd ext3
包含：initramfs fsck.ext3
17062 个块
```

initrd 已更新，在 IPL 之前 `zipl` 需要更新 IPL 记录！

```
lnxquill:/etc/sysconfig/hardware # zipl
使用配置文件 '/etc/zipl.conf'
在 '/boot/zipl' 中构建启动
构建菜单 'menu'
添加 #1: IPL 部分 'ipl' (默认)
添加 #2: IPL 部分 'failsafe'
准备启动设备：dasda (0100)。
完成。
lnxquill:/etc/sysconfig/hardware #
```

> 注意：对于某些设备驱动程序，次设备号和名称的分配在内核启动之间可能会发生变化，在虚拟机环境中添加或移除设备时也可能变化，甚至设备被设置离线和重新上线时也会变化。因此，相同的文件名可能会导致完全不同的设备。

我们重建初始 ramdisk，以确保所有磁盘在 IPL 时按您激活它们的顺序上线。

要在 RHEL5 中使更改永久生效：

1. 更新 `/etc/modprobe.conf` 文件，在 `options` 行 `dasd_mod=` 的末尾添加新的 DASD，如示例 6-5 所示：

### 示例 6-5 更新 modprobe.conf

```
[root@mbase40 etc]# cat /etc/modprobe.conf

options dasd_mod dasd=0100,0150,0101,200

alias eth0 qeth

alias hsi0 qeth
```

2. 重建初始 ramdisk 并更新启动记录，如第 306 页的示例 6-6 所示。

### 示例 6-6 在 RHEL5 中重新创建初始 ramdisk 并更新启动记录

```
[root@mbase40 etc]# mkinitrd -v /boot/initrd-2.6.18-8.1.3.el5.img

2.6.18-8.1.3.el5

Creating initramfs

Looking for deps of module uhci-hcd

Looking for deps of module ohci-hcd

Looking for deps of module ehci-hcd

Looking for deps of module ext3: jbd

Looking for deps of module jbd: dasd_mod

Looking for driver for device dasd

Looking for deps of module ccw:t3990Me9dt3390dm0C: dasd_mod dasd_eckd_mod

Looking for deps of module dasd_mod

Looking for deps of module dasd_eckd_mod: dasd_mod

Looking for driver for device dasd1

Looking for deps of module ccw:t6310m80dt9336dm10: dasd_mod dasd_fba_mod

Looking for deps of module dasd_fba_mod: dasd_mod

Looking for deps of module ide-disk

Using modules: /lib/modules/2.6.18-8.1.3.el5/kernel/fs/jbd/jbd.ko

/lib/modules/2.6.18-8.1.3.el5/kernel/fs/ext3/ext3.ko

/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_mod.ko

/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_eckd_mod.ko

/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_fba_mod.ko

/sbin/nash -> /tmp/initrd.sl4762/bin/nash

/sbin/insmod_static -> /tmp/initrd.sl4762/bin/insmod

copy from '/lib/modules/2.6.18-8.1.3.el5/kernel/fs/jbd/jbd.ko' [elf64-s390]

to '/tmp/initrd.sl4762/lib/jbd.ko' [elf64-s390]

copy from '/lib/modules/2.6.18-8.1.3.el5/kernel/fs/ext3/ext3.ko'

[elf64-s390] to '/tmp/initrd.sl4762/lib/ext3.ko' [elf64-s390]

copy from

'/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_mod.ko'

[elf64-s390] to '/tmp/initrd.sl4762/lib/dasd_mod.ko' [elf64-s390]

copy from

'/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_eckd_mod.ko'

[elf64-s390] to '/tmp/initrd.sl4762/lib/dasd_eckd_mod.ko' [elf64-s390]

copy from

'/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_fba_mod.ko'

[elf64-s390] to '/tmp/initrd.sl4762/lib/dasd_fba_mod.ko' [elf64-s390]

Adding module jbd
```
