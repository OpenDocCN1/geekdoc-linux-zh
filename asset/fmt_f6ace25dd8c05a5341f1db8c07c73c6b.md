
- 20. 读取 `/etc/sysconfig/desktop` 文件以获取首选的 X11 显示管理器，并设置一个 `/etc/X11/prefdm` 链接文件。

这个列表很难记忆。一旦你熟悉了 `rc.sysinit` 启动序列，你可以使用下面的简要摘要备查表作为快速参考。

- 1. 运行网络脚本
- 2. 加载脚本函数
- 3. 日志级别 `Loglevel`
- 4. 键位映射 `Keymap`
- 5. 字体 `Fonts`
- 6. 交换空间 `Swap space`
- 7. 主机名/NIS 域
- 8. `fsck` 根分区
- 9. ISA 即插即用
- 10. 重新挂载根为读写
- 11. 检查根配额
- 12. 加载模块
- 13. 初始化 RAID
- 14. `fsck` 文件系统
- 15. 挂载所有文件系统
- 16. 开启配额
- 17. 设置时钟
- 18. 重新初始化交换
- 19. 串口
- 20. SCSI 磁带驱动程序
- 21. 设置 XDM
- 22. 转储 `dmesg`

## 57 认证目标 5.09

### 理解内核模块

当你编译内核时，可以选择将组件编译为模块。内核模块不是直接编译到内核中，而是作为一种可插拔的驱动程序，根据需要加载和卸载到内核中。制作模块而不是直接将其编译到内核中是一个好主意，原因如下：

- 它使内核尺寸更小。
- 这反过来增加了你的内核速度。
- 当模块不再需要时，可以动态卸载以占用更少的内存。

为了让内核根据需要动态加载和卸载内核模块，需要调用一个名为 `kereld` 的特殊守护进程。内核加载后，它将根据需要卸载模块。对于特殊参数和选项，你应该编辑 `/etc/conf.modules` 文件（注意：此文件可以与模块互换使用）。要在命令行上加载模块，你应该先执行：

```
depmod -a
```

这将扫描你的模块并找出所有模块的不同依赖关系，并映射到一个文件 `modules.dep`。该文件具有类似 Makefile 样式的结构来列出依赖关系，位于 `/lib/modules/x.x.x/`，其中 `x.x.x` 是你的内核版本。此命令通常在执行启动脚本运行时运行。此命令完成后，你就可以加载模块。如果它有依赖项，则所有需要的模块将先加载。使用 `modprobe` 加载模块。

```
modprobe 3c503
```

在此示例中，`3c503` 网卡的以太模块需要 `8390` 模块才能正常工作。如果先运行了 `depmod`，那么 `8390` 将在 `3c503` 驱动之前自动加载。如果列表中的依赖项在加载期间失败，则所有模块将自动卸载。

你可以使用 `/etc/conf.modules` 完成这些繁琐的工作。在 `/etc/conf.modules` 中有以下内容：

- `alias`（别名）
- `options`（选项）
- `install`（安装）
- `post-install`（安装后）
- `remove`（卸载）
- `post-remove`（卸载后）

这里是 `conf.modules` 的一个示例：

```
alias sound /dev/snd/*
options sound snd-pcm=1
install /dev/snd/null
post-install /dev/snd/null
remove /dev/snd/null
post-remove /dev/snd/null
```

`conf.modules` 文件的内容可能如下：

```
sound /dev/snd/*
options sound snd-
```

```
/etc/conf.modules 示例内容
alias sound /dev/snd/*
options sound snd-pcm=1
install /dev/snd/null
... (此处省略部分重复字符)
```

## 262 第5章：高级安装

请注意有一个 `modules.dep` 文件，它列出了所有目录内所有模块的依赖项。目录内部是针对每个分组的不同内核模块。你应该熟悉在需要时在哪里找到某些模块。以下是你在每个目录下可以找到的某些类型的模块：

- `block` 块设备：`ide-floppies`，`raid` 设备层级
- `cdrom` 非ATAPI 驱动程序：三菱 `Mitsubishi`，索尼 `Sony`
- `fs` 文件系统模块，`vfat`, `nfs`, `smbfs`, `minix`
- `ipv4` IP 4 模块，地址伪装模块
- `ipv6` 与上述相同，但适用于 IP 版本 6
- `misc` 杂项模块：摇杆，鼠标，`radius` 模块
- `net` 网络模块，驱动程序，`ppp`，`slip`
- `pcmia` 被 `pcmiacardmgr` 守护进程使用的驱动
- `scsi` SCSI 磁带和硬盘模块
- `video` 用于 Linux 的特殊视频模块，`MGA` 控制台

所有模块都以 `.o` 作为扩展名（例如 `vfat.o`）。你不需要指定全名，只需指定第一部分 `vfat`。一旦你了解了目录结构，就可以使用 `modprobe` 加载特定类别的所有模块。例如，如果你在 PC 上且不知道网卡名称，可以简单地输入：

```
modprobe -t net
```

这将尝试加载 `/lib/modules/.../net` 下的所有模块。当一个模块成功加载时它会停止。要删除一个模块及其所有依赖项，你可以输入：

```
modprobe -r 3c503
```

或者

```
rmmod -r 3c503
```

这两个命令在模块未被另一个模块使用的情况下，都会移除这些模块及其所有依赖项。如果你只想删除模块而保留依赖项加载，可以省略 `rmmod` 命令的 `-r` 选项。

# 认证总结

Linux 安装非常灵活。它可以轻松地允许你使用 LILO 双启动操作系统，并将其与 NT 的 NTLDR 服务器集成。你还可以设置 RAID 层级设备来对驱动器进行镜像和条带化。RAID 层级 1 和 0 要求你有两个或更多驱动器。你可以使用 `kickstart` 自动完成整个 Red Hat Linux 安装。

`Kickstart` 安装文件可以位于引导软盘上或 DHCP/BOOT 服务器上。如果文件位于软盘上，你可以用 `linux ks=floppy` 初始化它。若要从 BOOT 服务器获取文件，你可以输入 `linux ks`。

`Kickstart` 安装只能从本地 CD-ROM 或通过 NFS 安装。当你进行升级时，必须确保定义了语言、安装方法、设备规格、键盘设置、LILO 配置并使用 `upgrade` 关键字。

启动时，`/etc/inittab` 文件决定了启动过程的其余部分，因为它是每个运行级别 `runlevel` 期间运行的所有内容。你使用默认关键字来指定你的运行级别。某些默认运行级别是 `runlevel 1` – 单用户模式，`2` – 不带 NFS 的多用户，`3` – 完整多用户和 `5` – X11。初始启动脚本由 `sysinit` 关键字调用。

`rc.sysinit` 脚本运行几乎至关重要的依赖于系统的启动操作。该脚本将检查你的 Linux 分区是否存在文件系统错误，加载内核模块并设置初始交换空间。它还将初始化 RAID 设备并设置所有 ISA 即插用设备，如果分区上启用了配额，则会在此时开启。

## 两分钟训练

- Windows NT 和 Linux 双启动之间一种非常常见的设置。实现双启动有几种不同的方法。
- 主要有两种不同类型的 RAID 设置：基于软件的和基于硬件的。基于硬件的 RAID 系统仍在开发中，来自 DPT 的 SCSI 主机适配器是唯一带有某些 Linux 文档的控制器。关于硬件和基于 DPT 的 RAID 的更多信息，你应该参考 `DPT-Hardware-RAID-HOWTO` 文档。本文将重点介绍基于软件的 RAID，尽管其原理也适用于硬件。
- RAID 0 和 1 需要两个或更多驱动器，而 RAID 5 需要三个或更多驱动器。
- 特别注意 `raid-disks` 和 `spare-disks` 从 0 开始计数。`nr-raid-disks` 和 `nr-spare-disks` 是正确的驱动器数量。示例：如果 `nr-raid-disks = 3`，那么最后一个 `raid-disk` 将是 2。
- `Kickstart` 是 Red Hat 用于自动安装 Red Hat 的解决方案。
- `Kickstart` 安装只能从 CD-ROM、HTTP、FTP 或 NFS 服务器执行。你不能使用 SMB 进行安装。硬件冲突相当容易消除。有三个可能的冲突区域：
  1. 物理硬件跳线帽与其他显卡冲突。
  2. 你有配置不当的 ISA 即插用卡。
  3. 你没有足够的中断或资源来添加新设备。
- `PCMCIA` 适用于基于 Intel 和 Alpha 的笔记本电脑。
