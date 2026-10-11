
由于大多数用户永远不会在系统软件上使用调试器，通过移除这些符号可以恢复大量的磁盘空间。下一节将展示如何从程序和库中剥离所有调试符号。

## 6.79. 剥离

本节是可选的。如果目标用户是程序员且不计划对系统软件进行任何调试，可以通过从二进制文件和库中移除调试符号，将系统体积减少约 90 MB。除了无法完全调试软件外，不会引起任何不便。

大多数使用上述命令的人都不会遇到任何困难。然而，很容易拼写错误导致新系统无法使用，因此在运行 `strip` 命令之前，最好对当前状态下的 LFS 系统进行备份。

首先，将所选库的调试符号放在单独的文件中。以后在 BLFS 中运行使用 `valgrind` 或 `gdb` 的回归测试，则需要这些调试信息。

```
save_lib="--ld-2.27.so libc-2.27.so libthread-2.27.so libthread_db-1.0.so"
```

```
cd /lib
```

```
for LIB in $save_lib; do
  objcopy --only-keep-debug $LIB $LIB.dbg
  strip --strip-unneeded $LIB
  objcopy --add-gnu-debuglink=$LIB.dbg $LIB
done
```

```
save_usrl="libquadmath.so.0.0.0 libstdc++.so.0.24
  libbmpx.so.2.0.1 libbmpxwrappers.so.2.0.1 libitm.so.1.0.0
  libcrts.so.5.0.0 libaticomic.so.1.2.0"
```

```
cd /usr/lib
```

```
for LIB in $save_usrl; do
  objcopy --only-keep-debug $LIB $LIB.dbg
  strip --strip-unneeded $LIB
  objcopy --add-gnu-debuglink=$LIB.dbg $LIB
done
```

`unset LIB save_lib save_usrl`

在执行剥离之前，要特别小心确保没有任何要剥离的二进制文件正在运行。如果不确定用户是否已通过第 6.4 节“进入 chroot 环境”中提供的命令进入 chroot，请先退出 chroot：

```
logout
```

然后使用以下命令重新进入：

```
chroot $IFS /tools/bin/env -i \
HOME=/root TERM=$TERM PS1=$(lfs chroot) \u:\w\$ \
PATH=/bin:/usr/bin:/sbin:/usr/sbin \
/tools/bin/bash --login
```

现在可以安全地剥离二进制文件和库了：

```
/tools/bin/find /usr/lib -type f -name ".*a" -exec /tools/bin/strip {} +
```

```
/tools/bin/find /usr/lib -type f -name "*.so*" -exec /tools/bin/strip {} +
```

```
/tools/bin/find /usr/lib -type f -name "*.a" -exec /tools/bin/strip {} +
```

大量文件将报告为无法识别。这些警告可以忽略。

## 6.80. 清理

最后，清理遗留的一些额外文件：

```
rm -rf /tmp
```

以下命令用于：

```
chroot $IFS /tools/bin/env -i \
HOME=/root TERM=$TERM PS1=$(lfs chroot) \u:\w\$ \
PATH=/bin:/usr/bin:/sbin:/usr/sbin \
/tools/bin/bash --login
```

## 7.2. LFS-Bootstraps-20170626

LFS-Bootstraps 软件包包含一组脚本，用于在启动/关机时启动/停止 LFS 系统。自定义启动过程所需的配置文件和步骤将在后续章节中进行描述。

**估计构建时间：** 少于 0.1 SBU

**所需的磁盘空间：** 244 KB

### 7.2.1. 安装 LFS-Bootstraps

安装该软件包：

```
make install
```

### 7.2.2. LFS-Bootstraps 的内容

**安装的脚本：** `checkfs`, `cleanfs`, `console`, `functions`, `halt`, `ifdown`, `ifup`, `localnet`, `modules`, `mountfs`, `network`, `reboot`, `signalsend`, `setclock`, `ipv4-static`, `sysctl`, `syslog`, `template`, 以及 `udev_retry`

**安装的目录：** `/etc/rc.d`, `/etc/init.d` (符号链接), `/etc/sysconfig`, `/lib/services`, `/lib/lib` (符号链接)

## 简要说明

- `checkfs` 在挂载文件系统之前检查其完整性（日志和基于网络的文件系统除外）
- `cleanfs` 删除不应在重启后保留的文件，例如 `/var/run/` 和 `/var/lock/` 中的文件；它会重新创建 `/var/utmp` 并移除可能存在的 `/etc/nologin`, `/fastboot` 和 `/forceckfs`
- `console` 为所需的键盘布局加载正确的键位映射；它还会设置屏幕字体
- `functions` 包含常用函数（如错误和状态检查），这些函数被多个启动脚本使用
- `halt` 停止系统
- `ifdown` 停止网络设备
- `ifup` 初始化网络设备
- `localnet` 设置系统的主机和本地环回设备
- `modules` 加载 `/etc/sysconfig/modules` 中的内核模块，使用该文件中提供的参数
- `mountfs` 统计所有文件系统，标记为 noauto 或基于网络的文件系统除外
- `mountvirtfs` 挂载虚拟内核文件系统，如 proc
- `network` 设置网络接口（如网卡）并设置默认网关（如果适用）
- `rc` 主运行级别控制脚本；它负责按照系统链接名称确定的顺序逐一运行所有其他脚本
- `reboot` 重启系统
- `signals` 确保在系统重启或停止之前每个进程都已终止
- `setclock` 在硬件时钟未设置为 UTC 时间的情况下，将内核时钟重置为本地时间
- `ipv4-static`: 提供为网络接口分配静态 Internet协议 (IP) 地址所需的功能
- `swap`: 启用和禁用交换文件和分区
- `sysctl`: 如果存在 `/etc/sysctl.conf` 文件，则从其中加载系统配置值到运行内核中
- `syslogd`: 启动和停止系统及内核日志守护进程
- `template`: 用于为其他守护进程创建自定义脚本的模板
- `udev`: 准备 `/dev` 目录并启动 Udev
- `udev_retry`: 重试失败的 udev 事件，并在需要时将生成的规则文件从 `/run/udev` 复制到 `/etc/udev/rules.d`

## 7.3. 设备和模块处理概述

在第 6 章中，我们在构建 edev 时安装了 Udev 软件包。在详细讨论其工作原理之前，有必要简要介绍一下以前处理设备的方法。

通常 Linux 系统传统上使用静态设备创建方法，即在 `/dev` 下创建大量节点（有时是数千个节点），无论相应的硬件设备实际上是否存在。这通常通过 `MAKEDEV` 脚本实现，该脚本包含许多对 `mknod` 程序的调用，为世界上可能存在的每个设备提供相关的设备设备号和次要设备号。

使用 Udev 方法，只有被内核设备节点检测到的设备才会被创建。由于这些设备节点每次系统启动时都会创建，因此它们被存储在 dev.mem 文件系统中（一个完全驻留在内存中的虚拟文件系统）。设备节点不占用多少空间，因此我们使用的方法的影响可以忽略不计。

### 7.3.1. 历史

2000 年 2 月，一种名为 devfs 的新文件系统合并到了 2.3.4 内内核，并在 2.4 系列稳定内核中可用。尽管它存在于内核源码中，但这种动态创建设备的方法从未获得核心内核开发者的压倒性支持。

devfs 方法采用的主要问题在于它处理设备检测、创建和命名的方式。后者（设备节点命名）可能是最关键的。人们普遍认为，如果允许设备名称是配置的，那么设备命名策略应该由系统管理员决定，而不是由任何特定的开发者实施。devfs 文件系统还受到其设计固有的竞态条件的影响，如果不对内核进行重大修订将无法修复。由于缺乏维护，它长期以来被标记为弃用，并于 2006 年 6 月从内核中移除。
