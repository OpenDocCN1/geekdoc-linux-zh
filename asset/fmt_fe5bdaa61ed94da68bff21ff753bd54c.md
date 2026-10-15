
```
/dev/fd0        /mnt/floppy    auto  noauto,user           0      0

proc             /proc            proc  defaults               0      0

/dev/sda2                       ext2  defaults               1      1

/dev/sda1       none            swap  defaults               0      0

homeserver:/home/michael /mnt  nfs   rw                    0      0
```

## 使用 `linuxconf` 挂载文件系统

如果你正在按照第 6 章“配置你的环境”所述使用 `linuxconf` 程序，你可以视觉化地对 `/etc/fstab` 进行调整或挂载文件系统。在“文件系统”（File Systems）部分，你会看到“访问本地驱动”（Access Local Drive）或“访问 NFS 卷”（Access NFS Volume）的独立模块。选择其中任意都会弹出“卷规格”（Volume Specification）选项卡（如图 7.1 所示），你可以在其中输入想要挂载的文件系统的详情。新文件系统现在出现在你的 `fstab` 中，并在你在 `linuxconf` 中激活更改时被挂载。

![](img/b916e6553833e904f268fdbef0cc11e9_146_0.png)

### 图 7.1
`linuxconf` 工具还允许你更改已存在于 `/etc/fstab` 中的文件系统的选项。

另参

- 有关关于 `linuxconf` 的更多信息，请参第 109 页。

# 第8章

## 添加磁带和 Zip 驱动器

- 添加磁带驱动
- 添加 Zip 驱动器

# 第二部分 配置你的系统

# 第8章 添加磁带和 Zip 驱动器

本章介绍了如何在 Linux 下安装和使用磁带和 Iomega Zip 驱动器。磁带驱动和可移动驱动通常用于系统备份和重要软件的存档。可移动驱动也可用于存储 Linux 文件系统。

另参

- 要学习如何备份你的系统，请参第 476 页。

## 添加磁带驱动

Linux 通过 `ftape` 和 `st` 带模块支持许多磁带驱动。`ftape` 模块是一个用于支持软驱控制器磁带驱动或可移动备份驱动的设备驱动程序，而 `st` 模块支持 SCSI 磁带设备。这两个模块都由 `kmod` 守护进程在磁带操作需要时自动加载和卸载。

通常情况下，几乎所有的 SCSI 和软驱控制器磁带驱动都应该可以在现代 Linux 内核（2.0 及以上版本）上运行，但许多高速或并行端口磁带可能不行。检查 `Hardware-HOWTO` 或 `Ftape-HOWTO` 页面以查看你的磁带驱动和接口是否受支持。Linux HOWTO 页面通常安装在 `/usr/doc` 或 `/usr/share/doc` 下。检查你的发行版以验证 HOWTO 文档可用，或获取有关安装位置的更多信息。

## 安装磁带驱动

SCSI 磁带驱动器直接连接到已安装的 SCSI 适配器上，或添加到当前的 SCSI 设备链中。确保使用空闲的设备号并正确终止 SCSI 链。支持 SCSI 驱动器的设备位于 `/dev` 目录下，并以 `st` 或 `nst` 字母开头：

```bash
/dev/st0 /dev/st2 /dev/st3
/dev/st4 /dev/st5 /dev/st6 /dev/st7
/dev/nst0 /dev/nst1 /dev/nst2 /dev/nst3
/dev/nst4 /dev/nst5 /dev/nst6 /dev/nst7
```

磁带设备有两种类型：

- 回卷（Rewinding）：回卷设备在磁带操作后会自动回卷。
- 非回卷（Nonrewinding）：名称以 `n` 开头的设备是非回卷设备，在磁带操作后不会回卷。

有关这些 SCSI 磁带设备的更多信息，请参阅 `st` 手册页。

软驱控制器磁带驱动连接到空闲的软驱控制器端口。使用软驱磁带驱动时，你无法使用软驱。支持磁带驱动器的设备位于 `/dev` 目录下，文件名包含 `ft` 字母：

```bash
/dev/nfrtf0 /dev/nfrtf2 /dev/rft0 /dev/rft2
/dev/nfrtf1 /dev/nfrtf3 /dev/rft1 /dev/rft3
```

## 创建磁带驱动设备符号链接

1. 选择与你的 SCSI 软驱磁带驱动匹配的设备名称，例如 `/dev/st0` 或 `/dev/rft0`。
2. 作为 root 操作员，使用 `ln` 命令为你的设备创建符号链接，如下：

```bash
# ln -s /dev/nfrtf0 /dev/nftape
# ln -s /dev/rft0 /dev/nftape
```

该命令创建了磁带驱动器。

## 使用 `mt` 命令

`mt`（磁带）命令用于控制磁带驱动器。磁带驱动器的操作包括：

- 回卷磁带
- 张紧磁带
- 擦除磁带
- 磁带操作

`mt` 命令也可以用于备份脚本（如 `tar` 或 `cpio` 命令）来存档目录和文件。`mt` 有许多不同的选项，通常配合 `-f` 选项指定磁带设备：

```bash
# mt -f /dev/nftape
```

磁带驱动与其他文件系统不同不需要挂载或卸载。

另参

- 要了解更多关于挂载文件系统和使用 `mount` 命令的信息，请参阅第 124 页。
- 要学习如何使用 `tar` 和 `cpio` 命令，请参阅第 505 页。

# 第二部分 配置你的系统

# 第8章 添加磁带和 Zip 驱动器

## 张紧磁带

当磁带闲置一段时间后，张力（磁带绕卷轴的松紧程度）会发生变化。磁带用户的共识是，在使用磁带前进行张紧是一个好主意。磁带在使用前应张紧以消除现有的松弛，并确保符合驱动器的张力要求。这有助于减少备份期间的错误。要张紧磁带，请将磁带插入驱动器，并使用非回卷磁带设备执行 `mt` 命令的张紧操作：

```bash
# mt -f /dev/nftape tension
```

`mt` 命令也接受 `reten` 作为 `tension` 的缩写。

虽然某些磁带驱动器会自动回卷插入的磁带，但你可能需要回卷磁带，特别是当备份操作被软件或人工干预停止时。要回卷磁带，请使用非回卷磁带设备执行 `mt` 命令的回卷操作：

```bash
# mt -f /dev/nftape rewind
```

## 为 Linux 备份准备磁带

在为格式化磁带进行备份之前，通常需要使用 `mt` 命令擦除磁带并为 Linux 做好准备。要擦除磁带，请使用非回卷磁带设备执行 `mt` 命令的擦除操作：

```bash
# mt -f /dev/nftape erase
```
