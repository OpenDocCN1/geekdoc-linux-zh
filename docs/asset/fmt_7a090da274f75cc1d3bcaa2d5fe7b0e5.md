
当你开启计算机系统时，它从主板上的存储器加载启动监控器或基本输入输出系统 (`BIOS`)。该存储器通常是一个可编程的只读芯片 (`PROM`) 或闪存内存区域。`BIOS` 或启动监控器是一个面向硬件的应用程序，它执行某些硬件初始化，为控制台输入提供接口，然后指定内存地址处。

在资源有限的系统中，`BIOS` 加载的程序是 `Linux` 内核，将在后续小节中描述。桌面和服务器系统的启动过程要复杂一些。在这些类型的系统中，中间程序由 `MBR` 加载到内存中。现代 `x86` 系统（包括 64 位系统）最常用的程序是统一引导加载器 (`GRUB`)，尽管某些 `Linux` 发行版使用较旧、更简单的加载器，即 `Linux Loader` (`LILO`)。

# 加载器

加载器通常由两个阶段组成：第一阶段加载器和更优雅的第二阶段加载器。第一阶段加载器的阶段受存储存储设备上的 `MBR` 限制，这是一个单扇区（512 字节）。因此，第一阶段加载器主要包含足够定位和加载第二阶段加载器的信息，而那才是操作的核心。

如所述，`Linux` 提供了两种加载器：`LILO` 和 `GRUB`。在 `GRUB` 之前开发的加载器不理解 `Linux` 格式——它通过直接存储这些文件的设备偏移量来识别第二阶段加载器和其他启动相关信息。`Ubuntu` 使用的 `GRUB` 加载器遵循这种方法，但在启动过程中使用了一个中间步骤，为此 `GRUB` 提供了一个理解特定类型文件系统的阶段 1.5 加载器，因此它可以从机器的根文件系统中加载 `GRUB` 的文本格式配置文件。`GRUB` 提供了许多不同的阶段 1.5 加载器，例如：

- `c2fs_stage_1_5`，从包含 `ext2` 或 `ext3` 文件系统的分区启动
- `fat_stage_1_5`，从包含 `DOS` 或 `Windows VFAT` 文件系统的分区启动
- `ffs_stage_1_5`，从包含 `Berkeley Fast` 文件系统的分区启动
- `iso9660_stage_1_5`，从包含 `iso9660` 文件系统的分区启动（例如 `CD-ROM`）
- `jfs_stage_1_5`，从包含 `JFS` 文件系统的分区启动
- `minix_stage_1`，从包含 `Minix` 文件系统的分区启动

## 理解系统启动与关闭过程

- `ufs2_stage1_5`，用于启动包含传统 `UNIX` 文件系统的分区
- `vstafs_stage1_5`，用于启动包含 `Plan 9 VSTA` 文件系统的分区
- `xfs_stage1_5`，用于启动包含 `XFS` 文件系统的分区

默认情况下，`Ubuntu` 和 `Ubuntu` 衍生系统使用第 1 阶段引导加载程序来引导 `ext2`/`ext3`、`JFS`、`Minix`、`ReiserFS`、`VFAT` 和 `XFS` 系统。

第 1 阶段引导加载程序直接从其所在的文件系统类型中加载 `GRUB` 的第 2 阶段引导加载程序及相关配置文件。

> `LILO` 和 `GRUB` 之间的根本区别在于，它们是从文件系统加载引导加载配置和菜单数据，还是需要将这些信息的位置构建到引导加载程序中。两种引导加载程序都使用配置文件，你必须运行 `LILO` 命令（`sbin/lilo`）来编辑每个 `lilo` 配置文件（`/etc/lilo.conf`），或者让 `LILO` 重新加载通过直接文件系统偏移读取的菜单选项信息，并更新该文件在 `MBR` 中的位置。`GRUB` 第 1 阶段引导加载程序的工作原理是允许 `GRUB` 在文件系统中定位其配置和相关文件。

第 2 阶段引导加载程序通常提供一个菜单访问，允许你在计算机上加载操作系统的不同方式之间进行选择。`GRUB` 和 `LILO` 都可以配置为短时间显示此菜单、仅响应键盘输入（通过按 `Escape` 键）时显示，或者通过修改引导加载程序的配置文件让引导加载程序自动显示菜单（`LILO` 的配置文件位于 `/etc/lilo.conf`，`GRUB` 的位于 `/boot/grub/menu.lst`）。

> `Ubuntu` 和 `Ubuntu Linux` 系统使用 `GRUB` 引导加载程序，因此我们的重点是它。有关有关 `LILO`（其他 `Linux` 发行版如 `Xandros Linux` 仍在使用）的信息，请参见 `www.freshmeat.net/projects/lilo`，这是针对 `LILO` 的 `FreshMeat` 项目。

默认情况下，`Ubuntu` 和 `Ubuntu` 系统上的 `GRUB` 加载程序被配置为不显示菜单直接启动默认，但你可以在 `GRUB` 首次启动时快速按下 `Escape` 键（你有五秒钟时间）来显示所有可用 `GRUB` 启动选项的菜单。图 22-1 显示了我其中一个 `Ubuntu` 系统上 `GRUB` 引导加载器的示例菜单。如果你在启动过程中没有按键，`GRUB` 将自动启动。

某些发行版（如 `Fedora`）提供了比图 22-1 更好的 `GRUB` 菜单：如果你在启动过程中没有按键，`GRUB` 将自动启动。

图 22-1 示例菜单。

图 22-1 显示了我其中一个 `Ubuntu` 系统上 `GRUB` 引导加载器的示例菜单：

```
- Ubuntu
- Ubuntu (recovery mode)
- Ubuntu (advanced options)
```

其中一个 `Ubuntu` 系统上 `GRUB` 引导加载器的示例菜单：

```
- Ubuntu (advanced options)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (advanced options)
```

图 22-1 `Ubuntu` 和 `Ubuntu Linux` 系统使用 `GRUB` 引导加载器

图 22-1 `Ubuntu` 和 `Ubuntu Linux` 系统使用 `GRUB` 引导加载器：

```
- Ubuntu (advanced options)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (advanced options)
```

图 22-1 `Ubuntu` 和 `Ubuntu Linux` 系统使用 `GRUB` 引导加载器示例菜单：

```
- Ubuntu (advanced options)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (advanced options)
```

图 22-1 `Ubuntu` 和 `Ubuntu Linux` 系统使用 `GRUB` 引导加载器示例菜单：

```
- Ubuntu (advanced options)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (advanced options)
```

图 22-1 `Ubuntu` 和 `Ubuntu Linux` 系统使用 `GRUB` 引导加载器：

```
- Ubuntu (advanced options)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (advanced options)
```

图 22-1 `Ubuntu` 和 `Ubuntu Linux` 系统使用 `GRUB` 引导加载器：

```
- Ubuntu (advanced options)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (recovery mode)
- Ubuntu (advanced options)
```

图 22-1：
