
menu (Select and Exit Install in Figure 2-5). The `Page Up` and `Page Down` keys can be used to scroll through very long lists of options that fill more than one screen. The `space bar` may toggle an option on or off. No such options are shown in Figure 2-5, but such an option has a box formed from square braces ([ ]) to the left of the option, and this box is filled with an `X` if it's selected. Press `ENTER` to select the currently active action button. In some menus this action does the same thing as the space bar. In most menus, some options have differently colored leading letters, such as *Standard* and *Express* in Figure 2-5. You can skip directly to these options by typing the appropriate letter along with the `ALT` key, such as `ALT+E` to begin an Express installation in Figure 2-5. This procedure isn't perfectly reliable, though, particularly in menus with many options, so if it doesn't work, use the arrow keys to locate the appropriate option.

FreeBSD supports three types of installation: *standard*, *express*, and *custom*. Standard is the best choice for most new installations. Express skips some menus and checks, and so can install a system somewhat quicker if you're in a hurry; but you may need to spend more time later setting it up correctly. Custom can be useful if you're experienced with FreeBSD because it gives you somewhat greater control over certain options. The rest of this chapter assumes that you select the standard installation.

### 系统分区

Once you select the Standard option from the main *sysinstall* menu, the system tells you that you must partition your computer. As described in Chapter 1, this is actually a two-step process. First, you must create an x86 partition (aka a FreeBSD slice). Second, you create BSD-style partitions within the FreeBSD slice. A message appears immediately after you select the Standard option telling you that you’ll be creating a DOS-style partition; this is the FreeBSD slice. When you select `OK` to this message, `sysinstall` displays the FDISK Partition Editor screen shown in Figure 2-6.

#### 创建 FreeBSD 切片

Depending upon how you set aside space for FreeBSD, you may need to do one of two things:

- **使用整个磁盘** 如果你希望将整个磁盘用于 FreeBSD（这将销毁现有分区和数据），你可以输入 `A` 来执行此操作。这将创建一个单一的主 x86 分区（即 BSD 切片），FreeBSD 将驻留于此。

- **创建新分区** 如果你有空闲空间（通过 Desc 列中未使用的条目标识），你可以选中它并输入 `C` 来创建 FreeBSD 切片。随后系统会询问大小。在大多数情况下，你希望将所有空间分配给 FreeBSD，因此只需按 `ENTER` 接受默认值。否则，请按照 512 字节块或兆字节（末尾加 M，例如 `500M` 创建 500MB 切片）输入大小。如果你已经为 FreeBSD 创建了分区（例如使用 FDISK），你需要选中该分区并输入 `D` 将其删除，然后使用由此产生的空闲空间来创建 FreeBSD 切片。

![](img/f34d37e3abe9f4517128e54f80ab2616_83_0.png)

**图 2-6.** FreeBSD FDISK 分区编辑器在原理上与 DOS 或 Windows 的 FDISK 相似，但用户界面略有不同。

#### 设置引导加载器选项

一旦你对 x86 分区表进行了修改以添加一个或多个 FreeBSD 切片，请键入 `q`。此操作会将你的更改写入磁盘，并进入关于引导加载器放置位置的问题。本章稍后将在第 4 章中详细讨论此主题。目前，FreeBSD 提供三个选项：

- **BootMgr** 此选项将 x86 引导管理器安装到硬盘的*主引导记录 (MBR)*上，这是计算机启动时运行的第一段基于磁盘的代码。当 FreeBSD 是计算机上唯一的操作系统，或者你有简单的双启动配置（例如 FreeBSD 和 Windows）时，这是一个很好的选择。如果你的系统多启动了多个操作系统并且已经有一个引导加载器，你可能希望使用其他选项。

- **Standard** 此选项用标准 MBR 覆盖现有的 MBR，该 MBR 直接启动只有活动分区。如果你计划随后安装另一个引导加载器，可能会使用此选项，但即使在那种情况下，下一个选项也应该适用。

- **None** 此选项不触碰 MBR。如果你已经安装了其他引导加载器（如 System Commander 或 Linux 的 LILO），这是最佳选项。你需要重新配置该引导加载器，以便除了其他操作系统外还能引导 FreeBSD。

#### 创建 FreeBSD 分区

选择 MBR 选项后，FreeBSD 进入分区创建的第二阶段。在此阶段，你将使用一个称为 *FreeBSD Disklabel Editor*（如图 2-7 所示）的工具在 FreeBSD 切片内创建分区。每个 FreeBSD 系统至少需要两个分区：根 (/) 分区和交换 (`swap`) 分区。如果你的系统还有 DOS 或 Windows，FreeBSD Disklabel Editor 也会显示其分区，如图 2-7 所示。在全新安装中，FreeBSD Disklabel Editor 的初始状态仅显示现有的 DOS 或 Windows 分区（如果存在）。

你可以通过确保屏幕顶部的 Disk 行被高亮显示，然后按下 `c` 键来创建新分区。该实用程序将依次询问几项信息：

1. 分区大小（以块、兆字节或柱面为单位）。
2. 你正在创建文件系统还是交换分区。文件系统用于存放文件，但 FreeBSD 至少需要一个交换分区。最好将其设置得至少与计算机内存一样大，因为如果未这样做，理论上某些类型的系统崩溃可能会清除交换分区之后分区中的数据。
3. 分区的挂载点（即可访问该分区的目录名称）。稍后将更详细地描述挂载点。你至少需要一个根 (/) 分区，但可以创建更多分区。交换分区没有挂载点，因此系统不会询问交换分区的挂载点。

如果你有几百兆字节的空闲空间，可以输入 `A`，FreeBSD 将使用一些常见的分区规则设置空闲空间。这种方法可以节省一些时间，在某些情况下可能是一个有用的快捷方式，特别是如果你对 FreeBSD 不熟悉时。然而，如果你更有经验，你可能希望自行设置分区。以下是 FreeBSD 使用 `A` 选项创建的一些常见分区：

- **root (/)**
