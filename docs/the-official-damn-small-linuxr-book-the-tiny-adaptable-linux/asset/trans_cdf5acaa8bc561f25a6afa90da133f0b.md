

第二个分区用于交换。创建新分区的第一步是按下键盘上的向下箭头键，以突出显示驱动器上剩余的空闲空间。接下来，使用右箭头键导航到 New 按钮。再次选择 Primary，然后按 Enter。

由于第一个分区的计算已经完成，这个分区的大小应该与你为交换文件想要的大小相符——你应该可以直接按 Enter 来设置大小。不要将此分区标记为可启动！导航到 Type 按钮并选择 #82，即 Linux swap。图 9-2 显示了 cfdisk 界面的示例，其中包含刚刚描述的分区。

## FIGURE 9-2 An example of a hard drive partitioned for Linux.

![](img/af53325d7f38f1cdafca9f44568e4ab8_202_0.png)

这就是现在同时映射出 Linux 启动分区和 Linux 交换分区的同一块硬盘。

现在，你应该已经为硬盘分配了所有空间。数字可能与你选择的值略有出入，但差别不大——可能只有几 MB。这是由硬盘内部几何结构的物理限制造成的。

接下来，导航到 Write 按钮并按 Enter。你会被提示输入 yes 或 no。如果一切看起来都很好，输入 yes 并按 q 退出程序。

## Creating the Swap File

现在是格式化交换分区的好时机。这是一个简单的过程；在具有 root 权限的终端中，输入 mkswap 然后输入你在 Cfdisk 中分配给交换分区的分区。

因此，如果交换分区分配给 hda2，你将输入：

```
# mkswap /dev/hda2
```

图 9-3 显示了在格式化 /dev/hda2 分区后 mkswap 命令输出的示例。

![](img/af53325d7f38f1cdafca9f44568e4ab8_203_0.png)

**FIGURE 9-3** The mkswap command sets up a Linux swap area.

## THE HARD DRIVE INSTALL SCRIPT

使用 Damn Small Linux 进行传统硬盘安装时，有很多选项。你可以不安装引导加载程序，也可以选择安装 Grub 或 Lilo。除非你要在多操作系统启动的计算机上安装 DSL，否则你可能希望脚本为你设置引导加载程序。

你可以以 *单用户模式* 安装 DSL，这会在启动时直接进入桌面。或者，你也可以选择多用户设置，这要求你在访问桌面或命令行之前先登录。你还有安装 DSL 使用 ext3，即日志文件系统，或较旧的 ext2 文件系统的选项。

在我们的演示中，我们将选择 Lilo，因为它简单（提供较少的启动选项），并且这是一台老旧的计算机，只会启动 DSL。此外，我们将安装 DSL 以设置为多用户，因为在用户被授予系统访问权限之前需要登录，这使其安全性稍高。

如果你不确定该做出什么选择，可以尝试几种不同的安装配置，看看哪种最符合你的需求且最舒适。对于本示例，我还选择了 ext2，即非日志文件系统，因为它具有更快的读写访问速度并使用更少的磁盘空间。其他人可能会发现 ext3 文件系统带来的可靠性提升值得付出性能损失。

如果你的系统性能不足（或你赶时间），你可能希望从 DSL CD 以“安装模式”进行安装。在启动提示符下输入 **install**：

```
boot: install
```

这会引导你进入以下 DSL Install Options：

```
┌──[ DSL Install Options ]──────────────────────────────┐
│                                                        Net Access Req’d │
│  1. Make Standard Boot Floppy                         yes              │
│  2. Make USB Boot Floppy                              yes              │
│                                                        │
│  3. **Install to Hard Drive**                         **no**            │
│  4. Frugal Grub Hard Drive Install                    no               │
│  5. Frugal Lilo Compact Flash Install                 no               │
│                                                        │
│  6. USB Pendrive ZIP boot Install                     no               │
│  7. USB Pendrive HDD boot Install                     no               │
│                                                        │
│  8. Split KNOPPIX into floppy sized chunks            no               │
└────────────────────────────────────────────────────────┘
```
