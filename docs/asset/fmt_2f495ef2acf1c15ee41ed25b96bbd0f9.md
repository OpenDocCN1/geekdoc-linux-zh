
您已配置并定制了内核模块。`initrd` 映像，或称初始 RAM 磁盘映像，由在引导过程中加载的所有内核模块组成。额外安装的模块也需要添加到 `initrd` 映像中，以便在启动时自动加载。在本主题中，您将创建 `initrd` 映像以更新内核。

您系统中现有的内核可能已经包含了所有必要的模块，但在后续阶段，当需要支持一组新设备时，您可能需要更新模块。了解如何通过创建 `initrd` 映像来更新现有模块，将使您能够为新设备提供支持。

### `initrd`

![](img/477ccb2f05b6ba1b2d563ea74f18c197_327_0.png)

`initrd` 指的是初始 RAM 磁盘，它被临时挂载为根文件系统，用于加载启动程序和模块。`ramdisk` 与内核一起加载，其功能由内核控制。`initrd` 使系统能够分两个阶段启动。在第一阶段，系统使用加载主根文件系统或永久根文件系统所需的最小模块集进行引导。在第二阶段，当主根文件系统被挂载时，之前挂载的 `initrd` 文件系统将被移除，`ramdisk` 将被释放，以便根据需要安装额外的模块。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_327_1.png)

图 8-6：`initrd` 分两个阶段启动系统。

## `initrd` 映像

`initrd 映像` 是一个归档文件，包含引导操作系统所需的所有基本文件。可以构建或定制它以包含额外的模块、删除不必要的模块或更新现有模块。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_328_0.png)

### `mkinird` 命令

`mkinird 命令` 用于创建初始 RAM 磁盘映像，以预加载内核模块。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_328_1.png)

```
The mkinird command

[root@localhost ~]# mkinird
usage: mkinird [--version] [--help] [-v] [-f] [--preload <module>]
       [--force-id=probe] [--force-scsi-probe] [--omit-scsi-modules]
       [--image-version] [--force-raid-probe] [--omit-raid-modules]
       [--with=<module>] [--force-lvm-probe] [--omit-lvm-modules]
       [--builtin=<module>] [--net-dev=<interface>]
       [--without-usb] [--without-multipath] [--without-draid]
       [--fstab=<fstab>] [--nocompress] <initrd-image> <kernel-version>

       (ex: mkinird /boot/initrd-2.2.5-15.img 2.2.5-15)

[root@localhost ~]#
```

*图 8-7：`mkinird` 命令的选项。*

`mkinird` 命令的各种选项列在下表中。

| 命令选项 | 用途 |
| :--- | :--- |
| `--preload=(module name)` | 在加载 SCSI 模块之前，在 `initrd` 映像中加载一个模块。 |
| `--with=(module name)` | 在加载 SCSI 模块之后，在 `initrd` 映像中加载一个模块。 |
| `--builtin=(module name)` | 指定该模块已构建在当前加载的内核中，以便 `mkinird` 命令在创建 `initrd` 映像时将其省略。 |
| `--fstab=(fstab)` | 自动确定根设备所在文件系统的类型。 |
| `--omit-lvm-modules` | 在创建 `initrd` 映像时避免加载 LVM 模块。 |
| `--omit-raid-modules` | 在创建 `initrd` 映像时避免加载 RAID 模块。 |
| `--omit-scsi-modules` | 在创建 `initrd` 映像时避免加载 SCSI 模块。 |
| `-f` | 覆盖现有的 `initrd` 映像文件。 |

## 如何创建 `initrd` 映像

**操作参考：创建具有更新信息的 `initrd` 映像**

要创建具有更新信息的 `initrd` 映像：

1. 在 CLI 中以 `root` 身份登录。
2. 输入 `mkinird [command options] /boot/initrd-(kernel version number).img (kernel version number)` 以创建 `initrd` 映像。
3. 使用更新后的 `initrd` 信息更新 `/boot/grub/grub.conf` 文件。

### 活动 8-3

**创建 `initrd` 映像以更新内核**

- **开始之前：**
    1. 重新启动 `srvB` 并启动系统上的 Red Hat Linux。
    2. 切换到 CLI。

**场景：**

您需要排查一个存在引导问题的 Linux 系统。该系统包含一个装有 Linux 安装文件的 SCSI 磁盘。然而，内核没有内置的 SCSI 模块。尽管内核可以加载并执行其他模块，但如果先不加载 SCSI 模块，它将无法挂载其根文件系统。由于该模块位于 `/lib/modules/` 中的根文件系统中，您无法预先启用 SCSI 支持。您已更新内核并需要引导新内核。

| 您需要做什么 | 怎么做 |
| :--- | :--- |
| 1. 创建一个新的 `initrd` 映像。 | a. 在 CLI 中以 **`root`** 身份登录。<br>b. 输入 `mkinitrd /boot/new-initrd-image.img 'uname -r'` 以创建一个新的 `initrd` 映像。 |
| 2. 使用新的 `initrd` 映像更新 GRUB 配置。 | a. 输入 `cd /boot/grub` 以访问 GRUB 所在的目录。<br>b. 输入 `vi grub.conf` 以编辑 GRUB 配置文件。<br>c. 输入 `:17` 以导航到文件的第十七行。<br>d. 按 `I` 切换到插入模式。<br>e. 确认光标位于以 "initrd /initrd-2.6.***.img" 或 "module /initrd-2.6.***.img" 开头的文本附近<br>f. 输入 `#` 将该行显示为注释。<br>g. 在新的一行中，输入 `module /new-initrd-image.img`<br>h. 按 `Esc` 切换到命令模式。<br>i. 保存并关闭文件。<br>j. 输入 `reboot` 以加载新的 `initrd` 映像。 |
| 3. 查看新的 `initrd` 映像并使用它引导系统。 | a. 当系统重新启动且 GRUB 启动画面显示消息 **Booting Red Hat Enterprise Linux (2.6.\*\*\*) in 3 seconds, press A to enter the bootloader menu** 时。<br>b. 如果提示输入密码，按 `P` 查看 **Password** 提示。在提示符下，输入您的密码。<br>c. 在引导加载器菜单上，确认当前安装的 Linux 版本已被选中，并按 `E` 查看其组件。<br>d. 观察引导顺序列表中显示的 newly created initrd 映像 **module /new-initrd-image.img**。<br>e. 按 `B` 从新的 `initrd` 映像引导。 |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_330_0.png)

# 主题 D

## 管理设备驱动程序

在整个课程中，您一直在执行各种内核服务管理任务。设备管理是内核提供的另一项重要服务。在本主题中，您将管理 Linux 基于内核的设备驱动程序。

当需要添加硬件或升级现有硬件时，系统管理员必须频繁地读写驱动程序文件中的详细信息。了解如何通过 `/dev` 访问驱动器将使您能够有效地处理此任务。

### `udev`

`udev` 是一个设备管理器，负责硬件设备的自动检测和配置。`udev` 是内核的组成部分，在启动时初始化。`udev` 实用程序处理冷插和热插设备的模块加载。它在系统启动时加载冷插设备（如监视器或声卡）的模块，并在系统运行时动态加载热插设备（如 USB 驱动器或摄像机）所需的模块。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_332_0.png)

### `/dev` 目录

`/dev` 目录包括硬件和软件设备驱动程序。

### 冷插与热插
