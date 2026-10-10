
本节提供了解决 Linux 启动问题的可用选项概述。`dmesg` 用于将内核消息发送到标准输出（例如控制台）。内核可以向计算机显示器发送消息，代表启动期间检测和配置的硬件设备。`dmesg` 通过能够打印或控制内核环缓冲区来实现这一点，并协助故障排除或获取有关系统硬件的信息。`dmesg` 的语法如下：

```
dmesg [-c] [-n level] [-s bufsize]
```

# 第 3 章 启动 Linux

```
LinuxExpert1@linux-0vc /etc/initstab cat instab
#
# /etc/initstab
#
# Copyright (c) 1996-2002 SuSE Linux AG., Nuremberg, Germany. 保留所有权利。
# 作者 Florian La Roche, 1996
# 请向 http://www.suse.de/feedback 反馈。
#
# 这是 /sbin/init 的配置文件，
# 它由内核在启动时执行。它描述了
# 用于不同运行级别的脚本
#
# 所有用于运行级别变化的脚本都在 /etc/init.d/ 中

# 此文件可能被 SuSEconfig 修改，除非 /etc/sysconfig/suseconfig 中的
# CHECK_INITTAB 被设置为 "no"
#
# 默认运行级别在此定义
id:5 default

# 如果不是以紧急模式 (-b) 启动，第一个执行的脚本
# shell:bootroot=/etc/init/dboot

# /etc/init/drc 处理运行级别
# 运行级别 0 系统停止 (不要将其用于 initdefault!)
# 运行级别 1 单用户模式
# 运行级别 2 无远程网络本地多用户 (例如 NFS)
# 运行级别 3 带网络的全多用户
# 运行级别 4 未使用
# 运行级别 5 带网络和 xdm的全多用户
# 运行级别 6 系统重启 (不要将其用于 init!)

10.0 wait /etc/init/drc 0
11.1 wait /etc/init/drc 1
12.2 wait /etc/init/drc 2
13.3 wait /etc/init/drc 3
14.4 wait /etc/init/drc 4
15.5 wait /etc/init/drc 5
16.6 wait /etc/init/drc 6
```

图 3.4

Init 脚本文件。

- "`c`" 清除内核环缓冲区。
- "`sbuf`" 确定从内核环缓冲区查询的缓冲区大小。默认大小为 16392。
- "`n level`" 发送到计算机显示器的消息类型。当使用 "`-n 1`" 时，只有 panic 消息出现在计算机显示器上。所有其他消息都会显示。使用 "`-n`" 选项时，`dmesg` 命令不会打印或清除内核环缓冲区。

在不带任何参数输入 `dmesg`（或 `dmesg | more`）将显示发送到标准输出的内核消息完整列表。

## 关键时刻

在解决启动时间问题时使用 `dmesg` 非常有用，考试中记住这一点很重要。该命令将向你显示内核检测到的硬件设备以及它是否可以配置它们。

## 考试目标总结

下一个选项是内核选项（kernel options），允许你输入在 Linux 系统启动期间由内核执行的信息。可以通过编辑 `/boot/menu.lst` 或在启动提示符处输入信息来添加内核参数。`/boot/menu.lst` 提供了默认内核参数，如前文 3.2 所示。此外，可以预定义故障安全内核参数，以便 Linux 在出现问题的情况下启动。要使用 GRUB 动态修改启动过程，你可以输入运行级别参数。

# 第 3 章 启动 Linux

运行级别（Runlevels）使用一组脚本，通过执行各种服务或进程，来定义计算机系统的启动或停止，以及 root 管理权限和用户访问的级别。运行级别编号从 0 到 6，系统的默认运行级别设置位于 `/etc/initstab` 文件中。

最后一个章节“故障排除启动问题”介绍了解决启动问题的方法。`dmesg` 命令可以协助故障排除或获取有关系统硬件的信息，它通过能够打印或控制内核环形缓冲区（ring buffer），将 Linux 内核消息发送到标准输出。

内核选项的动态修改允许你输入在系统启动期间由 Linux 内核执行的信息。可以通过编辑 `/boot/grub/grubmenu.lst`、在启动提示符（prompt）处输入信息，或在启动过程中使用 GRUB 动态修改内核来添加内核参数。

救援（Rescue）方法会启动一个没有图形界面的特殊 Linux 内核。所加载的 Linux 内核可以从可启动设备（例如 LiveCD）获取。一旦内核加载到内存（RAM），你就可以配置文件、检查文件系统缺陷、验证和/或修改引导程序配置、调整分区大小，以及其他可能必要的系统修改。

## 五大最难级问题

1. 你是部门 Linux 系统的 IT 系统管理员。你需要更改默认运行级别设置。哪一个文件包含默认运行级别设置？

   A. `/etc/initstab`

   B. `/etc/grub/boot/initab`

   C. `/boot/grub/device.map`

   D. `/etc/init.d`

2. 你的 IT 部门进行了若干次严重的硬件设备更改。这些包括对硬盘驱动器的修改。你需要修改 GRUB 引导加载程序。你应该编辑哪个文件来配置 GRUB 2 阶段镜像？

   A. `/etc/menu.lst`

   B. `/boot/grub/menu.lst`

   C. `/etc/grub.conf`

   D. `/boot/grub/grub.conf`

3. 你是部门 Linux 系统的 IT 系统管理员。你需要更改 GRUB 设备命名规范。哪个文件包含默认运行级别设置？

   A. `/etc/device.map`

   B. `/etc/grub.boot/device.map`

   C. `/boot/grub/device.map`

   D. `/etc/init.d`

4. Linux 内核是 Linux 启动过程中的关键组件。它位于系统的哪个位置？

   A. `/kernel` 目录

   B. `/grub/boot/kernel` 目录

   C. `/boot` 目录

   D. `/boot/kernel` 目录

5. Linux 引导加载程序是 Linux 启动过程中的关键组件。它位于系统的哪个位置？

   A. 它位于主引导记录（MBR）中

   B. 它位于 Linux 内核内部

   C. `/etc` 目录

   D. 在系统 BIOS 内部

## 答案

- 1. 正确答案及解释：A。答案 A 是正确的，因为 `/etc/initstab` 包含默认运行级别设置。运行级别 5 的默认设置如下：

```
5:initdefault
```

错误答案及解释：B、C 和 D。答案 B 是错误的，因为路径 `/etc/grub` 不存在。答案 C 是错误的，因为 `/boot/grub/device.name` 用于将 Linux 设备名称映射到 GRUB 命名规范。答案 D 是错误的，因为 `/etc/init.d` 是包含运行级别脚本的目录。

- 2. 正确答案及解释：C。答案 C 是正确的，因为 `/etc/grub.conf` 包含了用于查找和加载 GRUB stage2 镜像的磁盘分区信息。

错误答案及解释：A、B 和 D。答案 A 是错误的，因为 `menu.list` 不位于 `/etc` 目录中，且该文件用于确定在选定的菜单项上加载并启动哪个操作系统。答案 B 是错误的，因为该文件用于确定在选定的菜单项上加载并启动哪个操作系统。答案 D 是错误的，因为 `grub.conf` 不位于 `/boot/grub` 目录。

- 3. 正确答案及解释：C。答案 C 是正确的，因为 `/boot/grub/device.name` 用于将 Linux 设备名称映射到 GRUB 命名规范。

例如：

```
(hd0)->~/dev/sda
```

错误答案及解释：A、B 和 D。答案 A 是错误的，因为路径 `/etc` 不包含 `device.map`。答案 B 是错误的，因为目录 `/boot/grub` 不存在。答案 D 是错误的，因为 `/etc/init.d` 是包含运行级别脚本的目录。

- 4. 正确答案及解释：C。答案 C 是正确的，因为 Linux 内核位于 `/boot` 目录。

错误答案及解释：A、B 和 D。答案 A、B 和 D 是错误的，因为这些目录不存在。

- 5. 正确答案及解释：A。答案 A 是正确的，因为 Linux 引导加载程序位于主引导记录（MBR）中。MBR 是引导扇区。系统 BIOS 读取启动设备的第一个扇区。该扇区的大小为 512 字节。对于硬盘驱动，这个特殊扇区被称为 MBR。

错误答案及解释：B、C 和 D。答案 B 是错误的，因为 Linux 引导加载程序用于检索 Linux 内核。答案 C 是错误的，因为 `/etc` 是 Linux 内核获取控制权后挂载的文件夹。

## 第3章 启动 Linux
