

# 表 3-2 来自图 3-1 的 LILO 指令。

| 指令 | 说明 |
| :--- | :--- |
| boot=/dev/sda | 从第一个可用的硬盘启动 |
| prompt | 在启动加载器菜单中添加提示符 |
| install=menu | 安装标准的 LILO 菜单 |
| map=/boot/map | 指定映射文件的位置；在 1998 年之前的系统上，必须位于硬盘的前 1,024 个磁道内 |
| vga=normal | 为菜单配置低级视频图形卡阵列 (VGA) 模式 |
| password= | 为菜单选择或特定菜单选项设置密码，取决于所在位置 |
| default=Linux | 根据每个分区（stanza）中的 label 指令指定默认分区 |
| delay=100 | 设置以十分之一秒为单位的延迟；delay=100 表示在启动默认分区前延迟 10 秒 |
| image=/vmlinuz | 指定 Linux 内核的位置；它可以是指向实际内核文件的软链接 |
| root=/dev/sda | 注明第一个硬盘的分分区为顶层根目录的位置 |
| initrd=/initrd.img | 指定初始 RAM 磁盘的位置 |
| read-only | 以只读模式启动内核，在文件系统挂载之前这是标准做法 |
| other=/dev/db1 | 指定非 Linux 操作系统的位置 |
| table=/dev/sdb | 指定另一个所注操作系统的位置；功能上等同于 GRUB 链加载命令 |

# 安全与传统的 GRUB

本节定义了安装在 Red Hat Enterprise Linux 0.97 版本上的标准 GRUB 启动加载器。最新的 OpenSUSE Linux 也安装了相同版本的 GRUB。GRUB 启动加载器的细节在更多入门 Linux 教书中已有介绍。在本节中，你将查看如何使此 GRUB 配置安全。

# 第 3 章 | 基础安全：通过启动过程实现

```
# 由 anaconda 生成的 grub.conf
```

```
# 注意，修改文件后不需要重新运行 grub
```

```
# 注意：你有一个 /boot 分区。这意味着
# 所有内核和 initrd 路径都是相对于 /boot/ 的，例如：
root (hd0,0)
```

```
# kernel /mlinuz-version root=/dev/VolGroup00/LogVol00
initrd /initrd-version.img
```

```
#boot=dev/hda
default=0
timeout=5
splashimage=(hd0,0)/grub/splash.pmz
hiddenmenu
title Red Hat Enterprise Linux (2.6.18-164.el5)
root (hd0,0)
kernel /mlinuz-2.6.18-164.el5 root=/dev/VolGroup00/LogVol00
initrd /initrd-2.6.18-164.el5
```

```
//grub.conf" 17L 69C
```

# 图 3-2

一个传统的 GRUB 配置文件。

![](img/c0608a8c8a0777903dfec4ff61fdffa1_94_0.png)

首先，检查图 3-2 所示的标准版本 GRUB 配置文件。如注释所示，/dev/hda 是要启动的硬盘。

你可以对此配置文件进行一些更改以确保安全。首先，`timeout=5` 指令为黑客提供了五秒时间打开本地 GRUB 菜单。在此期间，屏幕上显示的信息是一个开放的邀请：

“按任意键进入菜单”

如果你将 `timeout=5` 改为 `timeout=0`，黑客将很难知道配置了什么种启动加载器，更不用说访问 GRUB 菜单了。但由于仍然有可能，你需要考虑显示中的以下选项：“按回车启动所选操作系统，'e' 在启动前编辑命令，'a' 在启动前修改内核参数，或按 'c' 进入命令行”。

任何可以修改内核参数的人都可以轻松进入单用户模式，并获得 root 管理员访问权限。是的，某些发行版让无密码管理访问变得稍微困难。然而，任何能进入内核命令行的人都可以绕过 root 密码限制。

黑客只需要在内核命令行末尾添加 `init=/bin/sh` 或 `init=/bin/bash` 指令。图 3-3 包含了为了安全系统而做的更改。为了管理目的，增加了一个受保护的分区。

# 通过启动过程实现的基础安全设施

# 图 3-3

```
# 由 anaconda 生成的 grub-conf
# 注意，修改此文件后不需要重新运行 grub
# 注意：你有一个 /boot 分区。这意味着
# 所有内核和 initrd 路径都是相对于 /boot/ 的，例如：
# root (hd0,0)
# kernel /mlinuz-version root=/dev/VolGroup00/LogVol00
# initrd /initrd-version.img
#boot=dev/sda
default=0
timeout=5
splashimage=(hd0,0)/grub/splash.pmz
hiddenmenu
title Red Hat Enterprise Linux (2.6.18-164.el5)
root (hd0,0)
kernel /mlinuz-2.6.18-164.el5 root=/dev/VolGroup00/LogVol00
initrd /initrd-2.6.18-164.el5
```

