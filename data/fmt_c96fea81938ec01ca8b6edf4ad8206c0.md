
`modprobe`相比`insmod`的巨大优势是会加载所有必要的模块，而`insmod`需要手动加载。另一个优势是你不需要指定完整的模块路径。此截图显示了`modprobe`如何在后台自动加载`isdn`模块和`slhc`。

```
[root@RHEL52 kernel]# lsmod | grep isdn
root@RHEL52 kernel]# modprobe isdn
root@RHEL52 kernel]# lsmod | grep isdn
isdn 122433 0
slhc 10561 1 isdn
[root@RHEL52 kernel]#
```

### 28.4.10. /lib/modules/<kernel>/modules.dep

模块依赖存储在`modules.dep`中。

```
[root@RHEL52 2.6.18-92.el5]# pwd
/lib/modules/2.6.18-92.el5
[root@RHEL52 2.6.18-92.el5]# head -3 modules.dep
/lib/modules/2.6.18-92.el5/kernel/drivers/net/tokenring/c359.ko
/lib/modules/2.6.18-92.el5/kernel/drivers/net/pcmcia/c574.ko
/lib/modules/2.6.18-92.el5/kernel/drivers/net/pcmcia/c359.ko
```

### 28.4.11. depmod

可以使用`depmod`命令更新（重新创建）`modules.dep`文件。在此截图中没有添加模块，所以`depmod`生成了相同的文件。

```
root@berry:/lib/modules/2.6.17-2-686$ ls -l modules.dep
-rw-r-- 1 root 310676 2008-03-01 16:32 modules.dep
root@berry:/lib/modules/2.6.17-2-686$ depmod
root@berry:/lib/modules/2.6.17-2-686$ ls -l modules.dep
-rw-r-- 1 root 310676 2008-12-07 13:54 modules.dep
```

### 28.4.12. rmod

与`insmod`类似，需要时使用`rmod`命令。

```
[root@RHEL53]# rmod isdn
[root@RHEL53]# rmod slhc
ERROR: Module slhc in use by isdn
[root@RHEL53]# rmod isdn
[root@RHEL53]# rmod slhc
[root@RHEL53]# lsmod | grep isdn
```

### 28.4.13. modprobe -r

与`rmod`相比，`modprobe`会自动移除未使用的模块。

```
[root@RHEL53]# modprobe isdn
[root@RHEL53]# lsmod | grep isdn
isdn 33537 0
slhc 72233 1 isdn
[root@RHEL53]# modprobe -r isdn
[root@RHEL53]# lsmod | grep isdn
[root@RHEL53]# lsmod | grep slhc
```

### 28.4.14. /etc/modprobe.conf

`/etc/modprobe.conf`文件和`/etc/modprobe.d`目录包含`modprobe`的别名（按名称）和选项（针对依赖模块）。

```
[root@RHEL52]# cat /etc/modprobe.conf
alias scsi_hostadapter mptbase
alias scsi_hostadapter mptspi
alias scsi_hostadapter ata_piix
alias eth0 pcnet32
alias eth2 pcnet32
alias eth1 pcnet32
```

## 28.5. 编译内核

### 28.5.1. extraversion

进入`/usr/src/redhat/BUILD/kernel-2.6.9/linux-2.6.9/`并修改`Makefile`中的`extraversion`。

```
[root@RHEL52 linux-2.6.18-i686]# pwd
/usr/src/redhat/BUILD/kernel-2.6.18/linux-2.6.18
[root@RHEL52 linux-2.6.18-i686]# vi Makefile
[root@RHEL52 linux-2.6.18-i686]# head -4 Makefile
VERSION = 2
PATCHLEVEL = 18
SUBLEVEL = 6
EXTRAVERSION = -paul2008
```

### 28.5.2. makeproper

现在使用`makeproper`清理之前的安装。如果这是你第一次下载源码，则不需要。

```
[root@RHEL52 linux-2.6.18-i686]# makeproper
CLEAN scripts/basic
CLEAN scripts/config
CLEAN include/kernel
CLEAN .config.old
```

### 28.5.3. .config

现在将`.config`复制到你的内核目录。此文件包含了当前内核使用的配置。它决定了哪些模块被编译。

```
[root@RHEL52 linux-2.6.18-i686]# cp /boot/config-2.6.18-92.el5 .config
```

### 28.5.4. make menuconfig

运行`menuconfig`（或图形化的`xconfig`）。此工具允许你选择作为模块 (m)、内核一部分 (*) 或完全不（更小的内核）。如果你删除太多，内核将无法工作。配置将存储在`.config`文件中。

```
[root@RHEL52 linux-2.6.18-i686]# make menuconfig
```

### 28.5.5. make clean

执行`make clean`准备编译。`make clean`会移除大多数生成的文件，但保留运行中的内核。在此处运行`makeproper`会破坏你通过`menuconfig`构建的`.config`文件。

```
[root@RHEL52 linux-2.6.18-i686]# make clean
```

### 28.5.6. make bzimage

然后运行`bzImage`，在内核编译时放松。你可以使用`time bzImage`了解编译需要多久，这样下次你就可以去散散步。

```
[root@RHEL52 linux-2.6.18-i686]# time make bzImage
HOSTCC scripts/basic/fixdep
HOSTCC scripts/basic/docproc
HOSTCC scripts/kconfig/conf.o
HOSTCC scripts/kconfig/kxgetext.o
```

此命令最后会告诉你`bImage`文件的位置（如果你也指定了命令，则带有时间信息）。

```
Kernel: arch/i386/boot/bzlImage is ready (#1)

real 13m59.5
user 13m22.6s
sys 11m51.0s
[root@RHEL52 linux-2.6.18-i686]#
```

## 28.5.9. /boot

我们仍然需要将内核、`System.map`和我们的配置文件拷贝到`/boot`。严格来说，`.config`文件并不是必须，但它可能对你以后编译内核有所帮助。

```
[root@RHEL52] # pwd
/usr/src/redhat/BUILD/kernel-2.6.18/linux-2.6.18.i686
[root@RHEL52] # cp System.map /System.map-2.6.18-paul2008
[root@RHEL52] # cp /boot/config/config-2.6.18-paul2008
[root@RHEL52] # cp arch/i386/boot/vmlinux-2.6.18-paul2008
```

## 28.5.10. mkinitrd

内核在启动时通常需要一个`initrd`文件。我们可以使用`mkinitrd`来生成此文件。请确保你使用了正确的内核名称！

```
[root@RHEL52] # pwd
/usr/src/redhat/BUILD/kernel-2.6.18/linux-2.6.18.i686
[root@RHEL52] # mkinitrd /boot/initrd--2.6.18-paul2008 2.6.18-paul2008
```

## 28.5.11. bootloader
