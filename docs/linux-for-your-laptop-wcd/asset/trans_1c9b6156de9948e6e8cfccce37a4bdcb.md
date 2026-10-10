

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_210_0.png)

图 7.6 当您的笔记本电脑使用电池供电时，ksmllaptop 电池计量表会显示在桌面面板的最右侧。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_210_1.png)

图 7.7 当笔记本电脑插入电源时，ksmllaptop 电池图标会显示为一个交流电插头和一个小型计量表，指示当前充电状态。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_210_2.png)

图 7.8 ksmllaptop 弹出菜单为笔记本用户提供了客户端和 APM 控制选项。

当您选择“电池监视器”菜单项时，您会在 KDE 桌面面板的最右侧看到一个图标，如图 7.6 所示。如果您的笔记本电脑使用电池供电，此电池图标将用作电源计量表。

如果笔记本电脑已插入电源，该图标将显示为一条垂直的蓝色条，如图 7.7 所示。如果您右键单击电池或交流电插头图标，会出现一个小型弹出菜单，如图 7.8 所示。然后您可以退出 ksmllaptop 客户端，更改设置，或将笔记本电脑放入挂起或待机模式。

如果您选择“设置”菜单项，您将看到如图 7.9 所示的对话框。您可以使用此对话框更改监视器使用的图标，并更改报告 APM 状态的频率。其他标签页，如“警告”和“严重”，用于设置在电源达到警告级别（默认为剩余 15 分钟）或严重级别（默认为剩余 5 分钟）时要运行的命令。您可以使用此对话框让笔记本电脑通过系统蜂鸣声、音乐、语音录音或弹出消息窗口来通知您，例如：

```
# xmessage -display 0:0 "Warning. 5 minutes battery power remaining."
```

## 资源信息

- http://www.worldvisions.ca/~apenwarn/apmd/
  Avery Pennarun 的关于 Linux apmd（高级电源管理）信息的主页。

- http://www.microsoft.com/HWDEV/busbios/amp_12.htm
  微软网站上的一个页面，存档了有关 APM 1.2 标准的信息。

- http://www.teleport.com/~acpi/
  一个托管高级配置和电源接口（ACPI）规范的网络页面。ACPI 是由 Compaq、Intel、Microsoft、Phoenix 和 Toshiba 共同开发的开放行业标准。ACPI 在硬件和软件之间提供了一层编程信息。这包括智能电池编程、芯片设计以及操作系统内核中断规范，外加 BIOS 设置。

- apmd-list@worldvisions.ca
  Linux apmd 邮件列表。向 apmd-list-request@worldvisions.ca 发送主题为 "subscribe" 的消息以订阅。

- http://falcon.sch.bme.hu/~seasons/linux/swsusp.html
  Gabor Kuti 的 Linux 内核补丁，允许任何运行 Linux 的计算机休眠 Linux 会话。

- http://www.gw.total-web.net/~dper/dpms.htm
  DPMS 规范。

- http://www.epa.gov/energystar/
  美国环境保护署能源之星计划的官方主页。

- /usr/src/linux/arch/i386/kernel/apm.c
  用于基于 Intel 的笔记本电脑的 APM 内核驱动程序。列出了 Texas Instruments TI 4000M TravelMate、Acer 486DX4/75、Toshiba 1950S 和 Midwest Micro Soundbook Elite DX2/66 笔记本电脑的已知问题。

- http://www.time.gov
  美国国家标准与技术研究院。获取您所在时区准确时间的来源。

- http://www.taniwha.com/laptop
  Paul Campbell 关于 kmlaptop 工具的主页。请在此查找更新和改进内容。

## 第 8 章：存储问题

- 最大化磁盘空间
- 自动磁盘清理
- 压缩和压缩文件系统
- 充分利用笔记本电脑的 RAM
- 一般建议
- 资源信息

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_214_0.png)

本章介绍了一些 Linux 命令和策略，您可以利用它们来最大程度地发挥笔记本电脑硬盘、配件和 RAM 的作用。您将学习有关控制硬盘的命令、用于自动清理硬盘的工具、如何压缩文件以及如何管理笔记本电脑内存的知识。您还将了解可以采取哪些步骤在具有 16MB 或更少 RAM 的笔记本电脑上运行 Linux。

## 最大化磁盘空间

Linux 附带了许多不同的磁盘实用程序，适用于各种类型的存储介质，从软盘到硬盘再到闪存 RAM 卡。这些实用程序中的大多数都是为了让 Linux 更好地配合您的硬件而设计的，但在某些情况下，通过运行这些程序，您可以榨取额外的性能并腾出存储空间。

表 8.1 列出了一些通常包含在 Linux 发行版中的命令。在接下来的章节中，您将学习这些命令的一些常见用途。

## 使用软盘

大多数笔记本电脑（苹果 iBook 除外）都配有内置或外置的软盘驱动器。Linux 通过通用设备（如第一个驱动器的 /dev/fd0）或特定设备支持软盘 fdisk，例如：

```
$ ls /dev/fd*
/dev/fd0        /dev/fd0360     /dev/fd0u3200   /dev/fd1h1440   /dev/fd1h720
/dev/fd0360     /dev/fd0h1200   /dev/fd0u3520   /dev/fd1h360    /dev/fd1u1440
/dev/fd0720     /dev/fd0u360    /dev/fd0u3840   /dev/fd1h720    /dev/fd1u2880
/dev/fd0h1440   /dev/fd0h720    /dev/fd1        /dev/fd1360     /dev/fd1u3200
/dev/fd0h360    /dev/fd0u1440   /dev/fd1360     /dev/fd1h1200   /dev/fd1u3520
/dev/fd0h720    /dev/fd0u2880   /dev/fd1h720    /dev/fd1h360    /dev/fd1u3840
```

启动后，您可以使用 dmesg 命令来查看 Linux 识别了哪些软盘设备：

```
$ dmesg
...
Floppy drive(s): fd0 is 1.44M
```

FDC 0 是 1991 年后生产的 82077
...

在这个例子中，识别到一个单槽 1.44MB 软盘驱动器（FDC 0）。您可以使用常规的 Linux 磁盘和卷管理器来操作插入的软盘。大多数 Linux 发行版默认安装一个 /mnt/floppy 目录，但您也可以（作为 root）自己创建一个，如下所示：

```
# mkdir /mnt/floppy
```

如果您插入一张 DOS 格式的软盘，则可以挂载软盘使其在 Linux 下可用，如下所示：

```
# mount -t vfat /dev/fd0 /mnt/floppy
```

此命令使软盘的内容（使用 vfat，即长文件名支持）出现在 /mnt/floppy 目录下。然后您可以使用常规的 Linux 命令——如 ls、cp、mv 和 rm——来列出、复制、重命名或删除该目录下的软盘文件。处理完软盘后，您应该使用以下命令卸载软盘：

```
# umount /mnt/floppy
```

大多数 Linux 发行版还包含文件系统表 /etc/fstab 中的一个软盘条目，可能如下所示：

```
/dev/fd0       /mnt/floppy           auto    sync,user,noauto   0 0
```

此条目显示第一个软盘驱动器通常挂载在 /mnt/floppy 目录下。Linux 会尝试自动确定正确的文件系统，并且任何用户都可以读写软盘。

然而，通过使用其他实用程序，例如包含在 mtools 包中的那些，您可以避免挂载然后卸载软盘驱动器——这方便得多！例如，在笔记本电脑中插入一张 DOS 启动软盘，然后使用 mdir 命令，如下所示：

```
# mdir a:
Volume in drive A has no label
Volume Serial Number is 15FA-2C24
Directory for A::
COMMAND   COM    93880  05-11-1998  19:01
AUTOEXEC  BAT      438  01-03-2000  15:44
CHOST     COM     5239  05-11-1998  20:01
CONFIG    SYS     1020  01-03-2000  15:02
DELTRH3   EXE    19083  05-11-1998  20:01
```

## 表 8.1 Linux 磁盘实用程序

| 名称 | 描述 |
| :------------- | :----------------------------------------- |
| badblocks | 在磁盘分区中搜索坏扇区（块） |
| cfdisk | 图形化 Linux 分区信息编辑器 |
| df | 显示已挂载文件系统的使用情况 |
| du | 显示磁盘使用情况（文件或目录） |
| e2label | 修改 Linux 文件系统的标签 |
| edquota | 编辑用户磁盘配额 |
| fdformat | 格式化 Linux 软盘 |
| fdisk | 编辑驱动器分区表 |
| fdrawcmd | 直接向软盘控制器发送命令 |
| find | Linux 搜索文件系统实用程序 |
| floppycontrol | 软盘驱动器配置实用程序 |
| floppymeter | 软盘性能监视器 |
| fsck | 检查和修复 Linux 文件系统 |
| gnorpm | GNOME 包管理器 |
| hattrib | 更改 HFS 文件或目录属性 |
| hcd | 更改 HFS 工作目录 |
| hcopy | 将文件复制或从 HFS 卷复制文件 |
| hdel | 删除 HFS 卷上的文件 |
| hdir | 列出 HFS 卷或目录中的文件目录 |
| hdparm | 显示和更改 IDE 硬盘设置 |
| hls | 列出 HFS 目录中的文件 |
| hmkdir | 在 HFS 卷上创建目录 |
| hmount | 挂载 HFS 卷 |
| hpwd | 打印 HFS 工作目录 |
| hrename | 重命名 HFS 文件或目录 |
| hrmdir | 删除 HFS 目录 |
| humount | 卸载 HFS 卷 |
| kfloppy | 格式化 Linux 或 DOS 软盘的 KDE 客户端 |
| kfsstastus | KDE 客户端；显示已挂载文件系统的使用情况 |
| kpackage | KDE 软件包管理客户端 |
| limit | Tcsh  shell 核心转储大小控制 |
| ln | 创建硬链接或软链接（符号链接） |
| lsdev | 显示已安装的设备 |

