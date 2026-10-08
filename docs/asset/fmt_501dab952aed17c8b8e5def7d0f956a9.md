
```
# ls
kernel-2.2.16-31686.rpm
# rpm -Uvh kernel-2.2.16-31686.rpm
```

在升级内核头文件时，由于无法移除旧的 `/lib/modules`，您可能会遇到错误。这种情况是可以接受的。请记下稍后清理。替换的 RPM 软件包如下：

```
# ls
kernel-2.2.16-31686.rpm
# rpm -Uvh kernel-2.2.16-31686.rpm
```

- 8. 在升级内核头文件时，由于无法移除旧的 `/lib/modules`，您可能会遇到错误。这种情况是可以接受的。请记下稍后清理。替换的 RPM 软件包如下：

```
# ls
kernel-2.2.16-31686.rpm
# rpm -Uvh kernel-2.2.16-31686.rpm
```

- 7. 继续升级或安装新的 RPM 软件包。在升级内核头文件时，由于无法移除旧的 `/lib/modules`，您可能会遇到错误。这种情况是可以接受的。请记下稍后清理。替换的 RPM 软件包如下：

```
# ls
kernel-2.2.16-31686.rpm
# rpm -Uvh kernel-2.2.16-31686.rpm
```

## Linux 的定制与升级

`rpm --rebuilddb` 命令将解决任何存在的 RPM 差异。

我们建议您查询 RPM 数据库，检查系统的磁盘空间，创建另一个启动盘等。

```
[root@HostA /root]# rpm --rebuilddb
```

# 第 11 步。重启并测试新内核

```
[root@HostA /root]# reboot
Red Hat Linux release 7.1 (Seawolf)
Kernel 2.4.3-12 on i686
login:
```

# RedHat V6.X 升级快速指南

此练习非常简单直观。这些指令可以适用于所有版本的 Red Hat Linux V6，只要您确保 RPM 软件包版本与现有的发行版版本和内核级别一致即可。

- 1. 检查并确保 `/boot` 中的内核有足够的磁盘空间，`/usr` 中的源文件有足够的磁盘空间。

之前：

```
# df
Filesystem 1k-blocks Available Use% Mounted on
/dev/hda1 806368 55140 710264 7% /
/dev/hda5 272226 1551 256620 1% /home
/dev/hda7 964500 667672 247832 73% /usr
```

之后：

```
# df
Filesystem 1k-blocks Available Use% Mounted on
/dev/hda1 806368 55140 710264 7% /
/dev/hda5 272226 1551 256620 1% /home
/dev/hda7 964500 667672 247832 73% /usr
```

- 2. 识别系统中已安装的 RPM 软件包并将其记录下来。将它们与升级内核所需的 RPM 软件包进行对比。

# 使用 RPM 软件包升级内核
