
## Alpha Miniloader 使用教程

### E.1 引言

本文介绍了用于 Alpha AXP 上 Linux 的 Miniloader (`MILO`)。此固件用于初始化 Alpha AXP 系统、加载并启动 Linux，并为 Linux 提供 `PALCode`。

### E.1.1 版权

Alpha Miniloader (`MILO`) HOWTO 版权所有 (C) 1995, 1996, 1997 David A Rusling。

**版权。** 与所有的 HOWTO 文档一样，可以在任何媒介（物理或电子）上全部或部分复制和分发，只要在所有副本上都保留此版权声明。允许并鼓励商业分发；然而，作者希望收到此类分发的通知。你可以将此 HOWTO 翻译成任何语言，前提是你保持此版权声明和免责声明完整，并附上说明翻译文档是谁的通知。

免责声明。尽管我尝试包含我所能找到的最准确、最新的信息，但我无法保证使用本文中的信息不会导致数据或设备的丢失。我对本 HOWTO 中的信息**不提供任何保证**，对于使用本 HOWTO 信息所导致的任何后果，我不承担责任。

### E.1.2 本档的新版本

本文的最新版本可以在 `ftpp://gatekeeper.com/pub/Digital/Linux-Alpha/Miniloader/docs` 找到，David Mosberger-Tang 慷慨地将其一些有趣的 HTML 格式包含在他出色的 Linux FAQ 网站 `http://www.azstarnet.com/axplinux` 中。

### E.2 什么是 MILO？

在基于 Intel 的系统上，BIOS 固件设置系统，然后加载镜像以从 DOS 文件系统的启动块运行。这在很大程度上是 `MILO` 在 Alpha 系统上做的事情，但 BIOS 固件与 `MILO` 之间存在一些有趣的区别，其中之一是 `MILO` 包含并使用了未修改的标准 Linux 设备驱动。`MILO` 是固件，不像 BIOS 依赖 BIOS 固件来加载自身。`MILO` 的主要功能部分包括：

- 1. `PALCode`，
- 2. 内存设置代码（构建页表并开启虚拟地址），
- 3. 视频代码（BIOS 仿真代码和 TGA (21030)），
- 4. Linux 内核代码。这包括真实的 Linux 内核代码（例如中断处理）以及替代或模拟的 Linux 内核，
- 5. Linux 块设备驱动（例如软盘驱动器），
- 6. 文件系统支持（`ext2`, `MS-DOS` 和 `ISO9660`），
- 7. 用户界面代码（`MILO`），
- 8. 内核接口代码（为 Linux 设置 `HWRPB` 和内存映射

- 9. 输入“no”表示你不想在启动时初始化调试器。
- 10. 在启动选择菜单中，选择“Change a boot selection option”。选择你创建的启动项。
- 11. 使用方向键选择“`OSLOADFILENAME`”，并输入“`\milo.`”。按回车。
- 12. 使用方向键选择“`OSLOADADOPTIONS`”，并删除其中可能存在的任何信息。或者，如果你让 `MILO` 自动启动你的 Red Hat Linux/Alpha 系统，可以输入以前从 `MILO` 软盘启动 Red Hat Linux/Alpha 的启动命令。在任何情况下，完成后按回车。
- 13. 按 `Esc` 退出“Change a boot selection option”菜单。
- 14. 选择“Setup Menu”。选择“Supplementary menu, and save changes”。
- 15. 返回启动菜单。

- 1. 在启动菜单中，选择“Supplementary menu”（补充菜单）。
- 2. 在补充菜单中，选择“Set up the system”（设置系统）。
- 3. 在启动选择菜单中，选择“Add a boot selection”（添加启动项）。
- 4. 如果显示，选择描述你的 `MILO` 分区的行。如果没有显示，选择“New System Partition”（新建系统分区）。
- 5. 输入描述你的 `MILO` 分区的设备属性（例如 SCSI/IDE、总线号等）。
- 6. 在擦除任何默认信息后，输入“`linload.exe`”作为操作系统加载器的目录和文件名。
- 7. 输入“yes”表示操作系统与加载器位于同一分区中。
- 8. 在擦除任何信息后，输入“/”作为操作系统根目录。
- 9. 给启动项取一个有意义的名字。“Linux”是一个不错的名字。
- 10. 输入“no”表示你不想在启动时初始化调试器。
- 11. 在启动选择菜单中，选择“Change a boot selection option”（更改启动项选项）。选择你创建的启动项。
- 12. 使用方向键选择“`OSLOADFILENAME`”，并输入“`\milo.`”。按回车。
- 13. 使用方向键选择“`OSLOADADOPTIONS`”，并删除其中可能存在的任何信息。或者，如果你让 `MILO` 自动启动你的 Red Hat Linux/Alpha 系统，可以输入以前从 `MILO` 软盘启动 Red Hat Linux/Alpha 的启动命令。在任何情况下，完成后按回车。
- 14. 按 `Esc` 退出“Change a boot selection option”菜单。
- 15. 选择“Setup Menu”（设置菜单）。选择“Supplementary menu, and save changes”（补充菜单并保存更改）。
- 16. 返回启动菜单。

这是一个启动项示例：

```
LOADIDENTIFIER =Linux
SYSTEMSPARTITION=scsi(0)disk(0)rdisk(0)partition(1)
OSLOADADER=scsi(0)disk(0)rdisk(0)partition(1)\linload.exe
OSLOADADERPARTITION=scsi(0)disk(0)rdisk(0)partition(1)
OSLOADFILENAME=milo
OSLOADADOPTIONS=-boot sda2:vmlin.gz root=/dev/sda2
sda2
```

注意，在这种情况下，我们使用 `OSLOADOPTIONS` 行来自动引导 `MILO` 启动我们的内核。

此时，重启你的系统到你刚刚创建的启动项。一旦出现 `login:` 提示，以 `root` 身份登录，并继续完成第89页第6章中的安装后任务。

- 13. 使用方向键选择“`OSLOADADOPTIONS`”，并删除其中可能存在的任何信息。或者，如果你让 `MILO` 自动启动你的 Red Hat Linux/Alpha 系统，可以输入以前从 `MILO` 软盘启动 Red Hat Linux/Alpha 的启动命令。在任何情况下，完成后按回车。
- 14. 按 `Esc` 键退出“Change a boot selection option”菜单。
- 15. 选择“Setup Menu”（设置菜单）。选择“Supplementary menu, and save changes”（补充菜单并保存更改）。
- 16. 返回启动菜单。

这是一个启动项示例：

```
LOADIDENTIFIER =Linux
SYSTEMSPARTITION=scsi(0)disk(0)rdisk(0)partition(1)
OSLOADADER=scsi(0)disk(0)rdisk(0)partition(1)\linload.exe
OSLOADADERPARTITION=scsi(0)disk(0)rdisk(0)partition(1)
OSLOADFILENAME=milo
OSLOADADOPTIONS=-boot sda2:vmlin.gz root=/dev/sda2
sda2
```

注意，在这种情况下，我们使用 `OSLOADOPTIONS` 行来自动引导 `MILO` 启动我们的内核。

此时，重启你的系统到你刚刚创建的启动项。一旦出现 `login:` 提示，以 `root` 身份登录，并继续完成第89页第6章中的安装后任务。
