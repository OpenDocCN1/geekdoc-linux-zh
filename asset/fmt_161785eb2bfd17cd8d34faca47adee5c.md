
Red Hat 使用大量轻量级命名的工具，而 SUSE Linux Enterprise Server 使用 YaST——无论是 TUI 版本（`/sbin/yast`）还是 GUI 版本（`/sbin/yast2-gtk`）——作为单一的管理门户。下表比较了 GUI 和 TUI 模式下 Red Hat 工具与其 YaST 模块对应项。

| **Red Hat Enterprise Linux 实用程序** | **SUSE Linux Enterprise Server YaST 模块** |
| :--- | :--- |
| `system-config-authentication` | YaST -> Security Settings |
| | `/sbin/hsystem security` |
| `system-config-boot` | YaST -> System -> Boot Loader Configuration |
| | `/sbin/yast bootloader` |
| `system-config-date` | YaST -> System -> Date and Time |
| `system-config-display` | SaX2 |
| | YaST -> Hardware -> Graphics Card and Monitor |
| `system-config-htpd` | YaST -> Network Services -> Web Server |

### 图 C-24

| Red Hat Enterprise Linux 实用程序 | SUSE Linux Enterprise Server YaST 模块 |
| :--- | :--- |
| `system-config-keyboard` | YaST :: Hardware :: Keyboard Layout |
| `system-config-kickstart` | YaST :: Software :: Installation Server |
| `system-config-language` | YaST :: System :: Language Selection |
| `system-config-lvm` | YaST :: System :: LVM |
| `system-config-mouse` | YaST :: Hardware :: Mouse Model |
| `system-config-netboot` | N/A |
| `system-config-network` | YaST :: Network Devices |
| `system-config-network-gui` | YaST :: Network Devices |
| `system-config-network-tui` | `/sbin/yast lan` |
| `system-config-nfs` | YaST :: Network Services :: NFS Server |
| | YaST :: Network Services :: NFS Client |
| `system-config-packages` | YaST :: Software :: Install and Remove Software |
| `system-config-printer` | YaST :: Hardware :: Printer |
| `system-config-printer-gui` | YaST :: Hardware :: Printer |
| `system-config-printer-tui` | `/sbin/yast printer` |
| `system-config-rootpassword` | `passwd root` |
| `system-config-samba` | YaST :: Network Services :: Samba Server |
| `system-config-securitylevel` | YaST :: Security and Users :: Firewall |
| `system-config-securitylevel-tui` | `/sbin/yast security` |
| `system-config-services` | YaST :: System :: System Services (Runlevel) |
| `system-config-soundcard` | YaST :: Hardware :: Sound |
| `system-config-time` | YaST :: System :: Date and Time |
| | （与 `system-config-date` 相同） |
| `system-config-users` | YaST :: Users and Groups |

> **SUSE 与 RED HAT 更新中的服务和支持包**
>
> Red Hat Enterprise Linux 和 SUSE Linux Enterprise Server 都使用在线更新机制，分别使用 Red Hat Network 用于内部软件分发的 YaST Online Update (`YOU`)，或用于从 Novell 获取更新的 ZENworks Linux Management。

### 图 C-25

![](img/63e88022bf135307e3eac051ad238b5b_517_0.png)

**启用 Red Hat Network 支持**

通常，系统管理员会安排从 Red Hat 获得支持订阅，通过 `rhn_register` 命令注册受支持的系统，然后使用 `up2date` 或 `rhn-applet-gui`/`rhn-applet-tui` 工具进行连接。然后一个向导将概述剩余的过程。如果注册过程不成功，通常需要访问 `rhn.redhat.com` 站点以启用支持订阅。

启用支持后，系统可以手动更新，可以使用 `up2date` 命令行工具，或者使用 GUI 桌面上的 Red Hat Network 通知工具。

**启用 SUSE Linux Enterprise Server 支持**

`YOU` (YaST Online Update) 服务器 GUI/TUI 客户端非常容易使用，root 用户只需选择 `YaST -> Software -> Online Update` 即可。系统将获取更新服务器列表，并显示一个对话框，让系统管理员配置如何执行更新。

YaST Online Update 客户端允许按计划进行自动更新；只需点击 `Configure Fully Automatic Update` 按钮，并配置在特定时间进行更新。你还可以配置它仅下载补丁，而不是其他项目。

SUSE Linux Enterprise Server 还提供 `online_update` 命令行工具来自动化系统更新。

关于内核更新的说明：Red Hat Enterprise Linux 传统上使用新内核更新系统，并在引导菜单（GRUB 或 LILO）中添加条目，而 SUSE Linux Enterprise Server 传统上是用新内核条目替换当前内核条目。在应用支持包 2 后，SUSE Linux Enterprise Server 将允许在应用后保留条目。

## 文件系统层次结构

SUSE Linux Enterprise Server 和 Red Hat Enterprise Linux 均符合 Linux 标准基础（LSB）规范，该规范现在包括文件系统层次结构标准（FHS）。Red Hat Enterprise Linux 3 符合 LSB 1.3，而 SUSE Linux Enterprise Server 9 符合 LSB 2.0。支持 LSB 最大限度地减少两个发行版文件系统布局之间的差异，系统管理员通常可以依赖配置和文件位于常见的目录位置。

你可以在 Free Standards 网站 `http://freestandards.org/` 找到 LSB 和 FHS 规范以及其他许多免费标准。

早期版本的主要差异之一是，Red Hat Enterprise Linux 使用 `/mnt` 目录来挂载所有文件系统、软盘和 CD-ROM，包括 USB 闪存盘和网络文件系统。SUSE Linux Enterprise Server 长期以来一直将 `/mnt` 目录用作基于网络的文件系统的容器，而 `/media` 目录用于任何已连接但未集成的媒体对象。例如，如果你将 USB 闪存盘连接到 SUSE Linux Enterprise Server 系统，系统会自动创建目录并将该 USB 闪存盘挂载到该目录中。

## 图 C-26

位于 `/media` 目录中的系统，例如对于 SanDisk Cruzer 1 GB USB 驱动器，该路径为 `/media/CRUZZER`。

在红帽企业版 Linux 4 中，两者同样都使用 `/mnt` 和 `/media` 目录，从而减少了可能引起混淆的一个点。
