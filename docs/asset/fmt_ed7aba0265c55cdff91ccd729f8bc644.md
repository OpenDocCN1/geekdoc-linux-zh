
http://www.geocities.com/epark/linux/grub-w2k-HOWTO.html

传统硬盘安装 Damn Small Linux 并不是那么困难。然而，在开始之前，你应该了解一些关于软件兼容性和硬件要求的信息。

## Some Debian Compatibility

Damn Small Linux 不是 Debian！Damn Small Linux 是使用基于 Debian 技术构建的 KNOPPIX 技术构建的。然而，我们做了很多定制以实现如此小的软件包。

这意味着如果你想使用 Damn Small Linux 作为安装 Debian 系统的手段，你注定会遇到一些问题。例如，许多核心库都基于 `old stable`，而 Debian 已不再支持该版本。因此，如果你想从 DSL 升级到完整的 Debian 系统，你需要进行大量的更新。

另一个需要注意的是，DSL 使用了一个特殊的轻量级 Xserver 构建，称为 Kdrive，它是编译好的，并且与 Debian 系统不兼容。最终，`apt-get` 会尝试用更完整的 XFree86 配置覆盖该设置。

如果你想使用前沿的 `Unstable` Debian 版本，请不要从 DSL 开始。还有其他选择。即使使用 KNOPPIX，也能让你以更少的麻烦到达那里。

由于 DSL 中移除了大部分基础 Debian 结构，我们建议你不要尝试使用 DSL 升级到更新的版本。话虽如此，许多旧版 stable Debian 应用程序可以在 DSL 中轻松安装。如果你运行的是老旧硬件，你会发现 Debian old stable 提供的软件比后期软件更适合你的机器。因此，坚持使用与 DSL 最兼容的版本可能对你最有利。

## 硬件要求

你的硬盘应至少有 200MB 的空间。如果你计划在低内存系统上进行安装，你需要为 `swap` 分区分配空间，该分区用于补充 RAM。

一个通用的经验法则是为 swap 提供相当于 RAM 两倍大小的空间。因此，如果你有 128MB 的 RAM，你应该为 swap 分区提供 256MB。如果你的系统处于低端且 RAM 为 64MB 或更少，你可能希望将 swap 增加到 RAM 大小的三倍。这有助于你在运行较大应用程序（如 Firefox）时。

另一方面，如果你拥有充足的 RAM——例如超过 1Gig——你可能根本不需要 swap 空间。我曾成功使用一台 256MB RAM 且没有 swap 分区的系统，但我必须小心我的 RAM 分配。

记住：如果你的计算机具有 IDE Flash 驱动器，请不要进行常规的硬盘安装。而是执行 Frugal 安装。

## 安装前准备

在开始安装过程之前，你需要对硬盘进行分区并设置 swap 文件。为本次演示，我们假设你将通过 DSL live CD 安装 DSL。请注意，安装过程会销毁硬盘上的所有数据，因此请务必将任何重要文件归档到除你即将格式化的计算机之外的其他位置。

## 使用 Cfdisk 进行分区

你需要设置一个 Linux 分区和一个 swap 分区。你将使用 `cfdisk` 命令作为分区编辑器。选择 `cfdisk` 作为本示例是因为它相对直观易用。`Cfdisk` 可用于检查计算机当前的分区表，以及删除和添加新分区。

在 DSL 中，你的主 IDE 硬盘应被识别为 `/dev/hda`。为了对硬盘具有可写访问权限，你需要以 root 用户权限打开一个终端；这可以通过打开一个 root 终端窗口，或在文本模式下输入 `sudo su` 来完成。

要启动 `cfdisk`，输入

```
# cfdisk /dev/hda
```

在我这个示例中，我正在修改一台之前安装了 MS Windows 98 的计算机。图 9-1 显示了 `cfdisk` 界面。

FIGURE 9-1 Cfdisk displaying data for a hard drive partitioned for Windows 98 (note, it looks much the same way as Windows 95 would look to cfdisk).

![](img/af53325d7f38f1cdafca9f44568e4ab8_200_0.png)

该图显示了硬盘最初为 MS Windows 98 安装所设置的状况。

图像顶部部分包含大量有用信息：

- `Disk Drive:` 你正在查看/编辑的磁盘驱动器，此处显示为 `/dev/hda`。
- `Size:` 驱动器的大小，此例中约为 3200MB。
- `Heads/Sectors per Track/Cylinders:` 驱动器的几何结构显示了硬盘上的磁头数、每磁道扇区数和柱面数。

在设置分区时，你需要参考驱动器的大小。你将把驱动器分割为一个 Linux 分区，用于存放 DSL，以及一个较小的 Linux swap 分区，Linux 使用它类似于 MS Windows 使用 swap 文件的方式。

在本示例中，你将把引导分区放在最前面。然而，你需要为 swap 分区预留空间，因此你需要从驱动器的总大小中减去 swap 分区的大小。演示计算机有 256MB 的 RAM，你希望为该计算机提供一个 swap 分区，其大小是 RAM 的两倍。

你需要做一些计算：

```
3,200MB    Total Drive Space
- 512MB    The desired swap partition size
------
2,688MB    The size of the boot partition
```

现在你得到了数字：引导分区为 2688MB。在创建它之前，你需要删除现有的表。

`Cfdisk` 使用起来相当简单；要移动焦点，只需使用键盘上的方向键即可。第一步是导航到 Delete 选项卡并按 Enter。这会删除现有分区。如果你有多个预先存在的分区，请全部删除。

在只剩下空闲空间后，导航到 New 按钮并按 Enter。接下来，它会询问这应为 Primary 还是 Logical 分区；选择 Primary 并按 Enter。

第二个分区用于交换。创建新分区的第一步是按下键盘上的向下箭头键，以突出显示驱动器上剩余的空闲空间。接下来，使用右箭头键导航到 New 按钮。再次选择 Primary，然后按 Enter。

由于第一个分区的计算已经完成，这个分区的大小应该与你为交换文件想要的大小相符——你应该可以直接按 Enter 来设置大小。不要将此分区标记为可启动！导航到 Type 按钮并选择 #82，即 Linux swap。图 9-2 显示了 `cfdisk` 界面的示例，其中包含刚刚描述的分区。

## FIGURE 9-2 An example of a hard drive partitioned for Linux.

![](img/af53325d7f38f1cdafca9f44568e4ab8_202_0.png)

这就是现在同时映射出 Linux 启动分区和 Linux 交换分区的同一块硬盘。

现在，你应该已经为硬盘分配了所有空间。数字可能与你选择的值略有出入，但差别不大——可能只有几 MB。这是由硬盘内部几何结构的物理限制造成的。

接下来，导航到 Write 按钮并按 Enter。你会被提示输入 yes 或 no。如果一切看起来都很好，输入 yes 并按 q 退出程序。

## Creating the Swap File

现在是格式化交换分区的好时机。这是一个简单的过程；在具有 root 权限的终端中，输入 `mkswap` 然后输入你在 `Cfdisk` 中分配给交换分区的分区。

因此，如果交换分区分配给 `hda2`，你将输入：

```
# mkswap /dev/hda2
```

图 9-3 显示了在格式化 `/dev/hda2` 分区后 `mkswap` 命令输出的示例。

![](img/af53325d7f38f1cdafca9f44568e4ab8_203_0.png)

`FIGURE 9-3` The `mkswap` command sets up a Linux swap area.

## THE HARD DRIVE INSTALL SCRIPT

使用 Damn Small Linux 进行传统硬盘安装时，有很多选项。你可以不安装引导加载程序，也可以选择安装 Grub 或 Lilo。除非你要在多操作系统启动的计算机上安装 DSL，否则你可能希望脚本为你设置引导加载程序。

你可以以 `单用户模式` 安装 DSL，这会在启动时直接进入桌面。或者，你也可以选择多用户设置，这要求你在访问桌面或命令行之前先登录。你还有安装 DSL 使用 ext3，即日志文件系统，或较旧的 ext2 文件系统的选项。

在我们的演示中，我们将选择 Lilo，因为它简单（提供较少的启动选项），并且这是一台老旧的计算机，只会启动 DSL。此外，我们将安装 DSL 以设置为多用户，因为在用户被授予系统访问权限之前需要登录，这使其安全性稍高。
