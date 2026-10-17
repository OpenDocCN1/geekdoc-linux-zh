
2. 输入目标分区的设备名称。例如，如果你使用的是计算机上的第一块 IDE 硬盘（`hda`），第一个分区（`hda1`）分配给交换分区，第二个分区（`hda2`）分配为 Linux 文件系统，你可以输入 `hda2` 并按 Enter。

接下来，系统会提示你输入正在安装的 DSL 软件的来源，如下所示：

```
Install from:
[L]iveCD or Frugal Install
[P]endrive
Local [I]so File
Fetching latest iso from [W]eb
From Poorman's via [B]ootfloppy
Choose (l/p/i/w/b):
```

3. 如果你是从 CD-ROM 启动的，选择显然是 L 代表 Live CD-ROM。

> **NOTE**
>
> 请注意，Frugal Grub 可以在从 pen drive 运行 DSL、从下载的 ISO 文件安装时进行安装，无论是 Isolinux 还是 Syslinux 版本，甚至可以从 Poorman's 通过 DSL 启动软盘进行安装。我将在本章“Poorman's—An Easy Way to Try DSL”部分中稍后谈论 Poorman's。

以下提示出现，询问是否格式化目标分区：

```
For INSTALL answer y to format, for UPGRADE answer n.
Format the target partition (y/..)? y
```

```
Last chance to exit before destroying all data on
Formatting target partition.
Setting up system image on target partition.
Setting up grub
```

4. 进行安装时，你需要格式化（`y`）。之后，当你想升级到 DSL 的新版本时，就不要格式化分区（`n`）。

> **NOTE**
>
> 升级 Frugal 安装就像再次运行安装脚本一样简单。因为 Frugal 意味着从未修改过的压缩映像运行，所以在升级期间，你的所有扩展和配置备份都不会受到影响。只有三个系统文件会被复制到目标介质。

Frugal Grub 安装的最后一个提示是为了兼容现有的 Windows 安装。因为 Frugal Grub 安装到主引导记录，所以你必须通知脚本为 Windows 添加一个条目。这包括所有版本的 Windows 直到 Windows XP。

> **NOTE**
>
> 稍后，在“Poorman's—An Easy Way to Try DSL”部分，我将讨论 Poorman's 安装，它允许 DSL 安装在现有的 Windows 分区内。

```
Do you have Windows installed on the first partition (y/..)?
Grub Installation Completed.
```

5. 如果你的第一个分区安装了 Windows，并且你希望能够从 Grub 引导提示中选择启动 Windows 或 DSL，请输入 `y`。如果没有 Windows 分区，则输入 `n`。

> **NOTE**
>
> 尽管我们尚未正式测试 Windows Vista 与 DSL 双启动，但 Windows Vista 的某些“功能”使得与 Linux 双启动变得困难。

一个问题是，安装 Windows Vista 时会擦除主引导记录（在我们的例子中是 Grub 或 Lilo）。因此，你应该先安装 Windows Vista 再安装 Linux，以免丢失 Grub 引导加载程序。第二个问题是 Windows Vista 使用了 Linux 或旧版 Windows 调整大小工具无法调整大小的不同版本的 NTFS。如果你能克服这些问题，使用 DSL 和 Windows Vista 双启动应该是可行的。

Poorman's 安装现已完成。然而，如果你的硬盘配置与上面描述的不同（即全部为 DSL 或 DSL 加上第一个分区上的单个 Windows 系统），你可能需要手动编辑你的 Grub 配置文件。

“如何在 Frugal Grub 安装中编辑启动选项？”是安装后最常被问到的问题之一。

所有 Frugal 类型安装都模拟从 CD-ROM 运行；对运行系统而言，这意味着系统挂载在 `/cdrom`。因此，作为超级用户 `root`，你可以编辑 Grub 的配置文件 `/cdrom/boot/grub/menu.lst`。然而，如果你使用 `toram` 启动选项启动系统，在你先挂载分区之前是找不到此文件的。例如，假设你安装到 `hda2` 并使用 `toram` 启动；作为超级用户，挂载 `/mnt/hda2`，如有必要，然后编辑 `/mnt/hda2/boot/grub/menu.lst`。

## Frugal Lilo CompactFlash Install

为什么此选项指的是 CompactFlash？我选择用 CompactFlash 命名此选项有两个原因：

- 对大多数用户来说，Lilo 引导加载程序更难编辑。
- 通常，使用 CompactFlash 意味着你正在构建一个设备，因此不希望出现易于访问的或甚至引导菜单选项。

Frugal Lilo 与 Frugal Grub 的不同之处在于它不会安装到主引导记录（MBR）。它将引导加载程序安装到目标分区。你需要将分区标记为活动分区。

使用 Frugal Lilo，你无需担心是否安装了其他操作系统，或谁将拥有 MBR。Frugal Lilo 在安装更改后有更多提示，以消除或减少你需要编辑 Lilo 配置文件的需求。

> **NOTE**
>
> 在安装 Frugal Lilo 之前，最好先从 DSL CD-ROM 启动并学习可能对你的特定机器或用途所需或期望的额外启动选项。

使用以下步骤进行 CompactFlash Lilo 安装：

1. 从 DSL Install Options 屏幕选择菜单选项 5（参见图 8-1）。你会看到以下免责声明和目标分区的提示：

```
DSL Compressed Image Install/Upgrade.

No responsibility for data loss or hardware damage!

A Linux partition large enough to hold the image file must be created prior to installation.

This version uses Lilo Boot Loader in the specified partition. You must therefore make that partition the active/boot one.

For Grub Boot Loader version, use frugal_grub.sh

Enter the target partition to hold DSL image & Lilo (EXAMPLE: hda1):
```

再次，如果你没有 Linux 分区，脚本会以错误退出。

2. 输入目标分区的设备名称。例如，如果你使用的是计算机上的第一块 IDE 硬盘（`hda`），第一个分区（`hda1`）分配给 swap，第二个分区（`hda2`）分配为 Linux 文件系统，你可以输入 `hda2` 然后按 Enter。

与 Frugal Grub 一样，你会被提示选择源位置，如下所示：

```
Install from:
[L]iveCD or Frugal Install
[P]endrive
Local [I]so File
Fetching latest iso from [W]eb
From Poorman's via [B]ootfloppy
Choose (l/p/i/w/b):
```

3. 如果你是从 CD-ROM 启动的，则应选择 L 来运行 live CD-ROM。

## 注意

与 Frugal Grub 一样，Frugal Lilo 可以在从 U 盘运行 DSL、从下载的 ISO 文件（Isolinix 或 Syslinux 版本）运行 DSL，甚至通过 DSL 启动软盘从 Poorman's 运行时安装。Poorman's 将在本章后面的“Poorman's——轻松尝试 DSL 的方法”一节中讨论。

因为我发现编辑 Lilo 配置对新用户来说并不容易，所以 Frugal Lilo 会预先提示许多用户可能需要使用的启动选项。
