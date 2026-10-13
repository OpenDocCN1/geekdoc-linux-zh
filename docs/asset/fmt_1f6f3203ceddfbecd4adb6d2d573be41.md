
还有其他你可以尝试的免费软件引导加载程序。包括位于 http://www.gnu.org/software/grub/grub.html 的 GNU GRUB（GRand Unified Bootloader，通用引导加载程序），以及可通过大多数流行的 Linux FTP 站点或 http://www.kac.poliod.hoc/~/doochbos/ 获取的 Tuomo Valkonen 的 Choose-OS 引导加载程序。

如果你最初安装 Red Hat Linux 时没有选择安装 LILO，或者你需要帮助以特定的内核选项正确启动 Linux，或者你需要帮助排查有问题的启动故障，本章将有所帮助。你应该已经知道希望如何在该计算机上启动 Linux，但这里的信息也可以向你展示安装和启动 Linux 的其他方式。

你还可以通过在网络上启动 Linux 将计算机用作无盘工作站。对此主题的讨论超出了本章的范围，但你可以在 Robert Nemrik 的 Diskless-HOWTO 中找到相关详细信息，可通过 http://www.linuxdoc.org/HOWTO/HOWTO-INDEX/HOWTOs.html 获取。你可以尝试的一个较新的以太网引导加载程序是 EtherBoot，可通过 http://etherboot.sourceforge.net/ 获取。

## 选择和安装启动管理器

简单的启动管理器，如 PowerQuest 的 `BootMagic`，提供了一种方便的菜单或图形界面，用于引导到不同的操作系统。其他启动管理器，如 `LILO` 和 `LOADLIN`，具有更高级的功能，这些功能对于成功启动可能至关重要，并且可能是你启动策略中必要的组成部分。如果你的计算机硬件需要预启动配置，或者 Linux 内核需要在启动过程之前、期间或之后了解关于计算机硬件的关键信息，你可能需要使用这些 `引导加载程序的` 特殊功能来启动 Linux。

例如，`LOADLIN` 命令用于从 DOS 命令提示符加载 `Linux` 内核。`LOADLIN` 与 `LILO` 类似，支持传递 *视频*、*网络* 和 *磁盘几何设置*，这些被称为 *内核参数*，通常通过命令行或 *引导参数* 进行传递。一些参数需要在 Linux 启动之前传递，而其他参数，如 *内存设置*，可以放置在配置文件中。`LOADLIN` 与 `LILO` 类似，支持在引导参数中或单独的配置文件中使用单独的内核参数。

如果你需要在特定状态下（通常是为了辅助识别、配置或使用）直接引导到 `Linux`，而保持计算机硬件不变，`LOADLIN` 特别有用。`LOADLIN` 还可以用于 Windows 操作系统中的 `config.sys` 脚本以提供启动菜单，或作为直接引导到 Linux 的桌面快捷方式。如果计算机硬件的某个特定子系统（例如 IBM MWave 适配器）在用作 `Linux` 声卡之前需要 DOS 初始化，`LOADLIN` 也会很有帮助。

好消息是，随着 Linux 的成熟，在启动过程期间或之后的硬件支持现在更好了。然而，可能存在只有像 `LOADLIN` 这样的引导加载程序才能工作的情况！

## 注

与之前的版本不同，随书 Red Hat CD-ROM 中不再包含 HOWTOs。请访问 `http://www.linuxdoc.org` 搜索和阅读 HOWTOs。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_92_0.png)

## 安装和配置 LILO

在安装 LILO 之前，你应该知道你的 Linux 分区在哪里。你还应该知道其他操作系统是否安装以及安装在哪里。例如（使用 Linux 的 `df`，即磁盘文件使用情况命令），分区可能显示为：

```
$ df

Filesystem  1k-blocks  Used Available Use% Mounted on
/dev/hda5  6079464  2168440 3602200  38% /
/dev/hda1   21929   2421    18376   12% /boot
```

这个简单的示例是单硬盘系统的典型情况，表明 Linux 的 `/boot` 分区安装在 `/dev/hda1` 上，而其余的 Linux 文件系统驻留在 `/dev/hda5` 上（虽然存在其他分区，如交换分区和休眠分区，但只有被识别的分区会显示出来）。在此处，LILO 安装在 `/dev/hda` 的主引导记录（MBR）中。以下是另一个示例，使用 `fdisk` 命令的打印分区表选项的输出：

```
Disk /dev/hda: 240 heads, 63 sectors, 1559 cylinders
Units = cylinders of 15120 * 512 bytes

Device Boot    Start   End  Blocks   Id System
/dev/hda1 *      1     218 1648048+ c  Win95 FAT32 (LBA)
/dev/hda2          219   1559 10137960 5 Extended
/dev/hda5          219   221 22648+ 83 Linux
/dev/hda6          222   499 210148+ 83 Linux
/dev/hda7          500   534 264568+ 82 Linux swap
/dev/hda8          535   881 2623288+ 83 Linux
/dev/hda9          882   1559 5125648+ 83 Linux
```

在这个示例中，Linux 文件系统安装在多个分区上，例如 `/dev/hda5`、`/dev/hda6`、`/dev/hda8` 和 `/dev/hda9`。虽然不明显，但这些分区分别对应 `/boot`、根目录（`/`）和两个附加卷，而 Windows 安装在 `/dev/hda1` 上。同样，LILO 安装在 `/dev/hda` 的 MBR 中，尽管它也可以安装在 `/dev/hda9` 上。

如果 Linux 是你计算机上唯一的操作系统，或者你已经安装了 Windows，请将 LILO 作为启动驱动器的主引导记录（MBR）进行安装。如果你还安装了 OS/2，你将希望将 LILO 安装在硬盘的根分区上，并使用 OS/2 的引导加载器位于 MBR 来启动不同的操作系统。

### 注意

某些操作系统，如 Windows，会在安装期间覆盖 MBR。这意味着如果你打算将机器用作双启动系统，你需要先安装微软的产品，然后用 LILO 覆盖 MBR，或者使用执行相同类型任务的其他类型软件，如 Partition Magic。

### 注意

Red Hat Linux 在初始 Linux 安装或升级过程中安装 LILO。在 LILO 安装过程中，你将有机会创建一张启动盘——请这样做！即使你不使用该磁盘，拥有一点“保险”以应对意外情况也是有益的。如果你不安装 LILO，你肯定需要这张磁盘来启动 Linux。如果你在安装过程中忘记制作启动盘，请在你的 Linux 会话中使用 Red Hat 的 `mkbootdisk` 命令创建一张。

LILO 是在你分区硬盘并安装了 Linux 或其他操作系统之后安装的。LILO 具备与商业解决方案相当甚至在某些情况下超越的功能，并且它是免费的。LILO 用于通过以下三种传统方式之一启动 Linux：

- 从硬盘的主引导记录（MBR）

- 从硬盘上根 Linux 分区（主分区或扩展分区）的超级块

- 从软盘（或 CD-ROM）

LILO 有许多配置参数和命令行参数，展示了其特殊功能。

虽然使用 `lilo` 命令（位于 `/sbin` 目录下）安装 LILO 很容易，但你应首先花时间阅读其文档，你可以在 `/usr/share/doc/lilo-21.4.4` 目录下找到这些文档。与文档一起，你会发现一个名为 `quickinst` 的 shell 脚本，可用于首次安装。LILO 的文档详细说明了其功能，并提供了针对特殊问题（如在容量非常大的硬盘上安装引导加载器或从其他操作系统启动）的重要提示和解决方案。

## 安装或重新配置 LILO

如果你没有在 Red Hat 安装过程中安装 LILO，或者决定不使用 *QuickInst* 脚本，你可以分两个基本步骤安装 LILO：

- 1. 创建并配置 `/etc/lilo.conf`。

- 2. 运行 `/sbin/lilo` 以安装 LILO 并使其激活。

本讨论描述了修改现有的 `lilo.conf` 文件。在进行任何更改之前，请为自己做一个备份，将文件备份到同一目录或单独的磁盘上。有几个文件对 LILO 很重要，并在初始安装时创建：

- `/sbin/lilo`—映射安装程序；更多信息请参阅 `man lilo`。

- `/boot/boot.b`—引导加载器。

- `/boot/map`—包含内核位置的引导映射。

- `/etc/lilo.conf`—LILO 的配置文件。

## 配置 LILO
