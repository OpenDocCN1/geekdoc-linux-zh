
| `xorgconfig` | 一个基于文本的 X.org 配置工具。 |
| `xf86cfg` | XFree86 版本 4 中包含的一个图形化 XFree86 配置工具。 |
| `xorgcfg` | 一个图形化 X.org 配置工具。 |

## 章节摘要

- 引导加载程序通常由系统 BIOS 从 MBR 或活动分区的第一扇区加载。
- 引导加载程序负责加载 Linux 内核。
- LILO 引导加载程序使用 `/etc/lilo.conf` 配置文件，而 GRUB 引导加载程序使用 `/boot/grub/grub.conf` 配置文件。
- 您可以使用 LILO 或 GRUB 引导加载程序来双启动 Linux 和 Windows 操作系统。或者，可以使用 Windows NTLOADER 引导加载程序完成同样的任务。
- 可以使用 FIPS 工具来分割 FAT 或 FAT32 分区，以创建足够的空间来安装 Linux。
- 使用七个标准运行级别来根据内存中加载的守护程序的数量和类型对 Linux 系统进行分类。
- `init` 守护程序负责使用其配置文件 `/etc/inittab` 加载和卸载守护程序。
- 守护程序通常存储在 `/etc/rc.d/init.d` 目录中，并从 `/etc/rc.d` 目录中的条目在系统启动时加载。
- Linux GUI 有多个可互换的组件，包括 X 服务器、X 客户端、窗口管理器和可选的桌面环境。
- X Windows 是 Linux GUI 的核心组件，用于在终端屏幕上绘制图形。它有两种开源实现之一：X.org 和 XFree86。
- 您可以通过在命令提示符下输入 `startx` 从运行级别 3 启动 Linux GUI，或通过运行级别 5 使用 `gdm` 启动。
- 配置 X Windows 需要深入了解计算机使用的视频硬件。`system-config-mouse`、`mouseconfig`、`system-config-keyboard`、`system-config-display` 和 `xvidtune` 工具可用于配置 X Windows 使用的硬件设置。

## 关键术语

- `/boot` — 包含内核和引导相关文件的目录。
- `/boot/grub/grub.conf` — GRUB 配置文件。
- `/etc/inittab` — `init` 守护程序的配置文件。
- `/etc/lilo.conf` — LILo 配置文件。
- `/etc/rc.d/init.d` — 大多数守护程序所在的目录。
- `/etc/rc.d/rc*.d` — 用于在每个运行级别启动和终止守护程序的目录。
- `/etc/rc.d/rc.local` — 系统启动期间执行最后一个脚本。
- `/etc/rc.d/rc.sysinit` — 系统启动期间执行第一个脚本。
- `/etc/X11/XF86Config` — X Windows 的 XFree86 实现所使用的配置文件。
- `/etc/X11/xorg.conf` — X Windows 的 X.org 实现所使用的配置文件。
- `active partition`（活动分区） — 在 MBR 之后搜索操作系统的分区。
- `boot loader`（引导加载程序） — 用于加载操作系统的程序。
- `boot.ini` — 用于配置 NTLOADER 的文件。
- `chipset`（芯片组） — 外设组件（如视频适配卡）上的一组通用计算机芯片。
- `daemon`（守护程序） — 提供特定服务的 Linux 系统进程。
- `desktop environment`（桌面环境） — 与窗口管理器配合工作的软件，提供使用标准程序和开发工具的标准 GUI 环境。
- `Desktop Switching Tool`（桌面切换工具） — 允许 Red Hat Linux 用户设置默认桌面环境或窗口管理器的图形工具。
- `dual boot`（双启动） — 计算机硬盘上存在两个或更多操作系统的配置；引导加载程序允许用户在启动时选择要加载哪个操作系统。
- `ELILO` — 用于支持 Intel Extensible Firmware Interface (EFI) 技术的计算机的引导加载程序。
- `Extended Multiuser Mode`（扩展多用户模式） — 也称为运行级别 3；提供大多数守护程序和完整的网络守护程序集合的模式。
- `First nondestructive Interactive Partition Splitter (FIPS)`（首次非破坏性交互式分区分割器） — 用于在现有 FAT16 或 FAT32 分区的可用空间上创建新分区的程序。

**GNOME 显示管理器（`gdm`）**——提供图形登录屏幕的图形化登录程序。

**GNU 图像处理程序（`GIMP`）**——使用 `GTK+` 工具包的一个开源图形处理程序。

**GNU 对象模型环境（`GNOME`）**——Red Hat Fedora Linux 中的默认桌面环境；它创建于 1997 年。

**引导加载器（`GRUB`）**——在 Linux 系统中常用的引导加载器。

**`grub-install` 命令**——用于安装 `GRUB` 引导加载器的命令。

**`grub-md5-crypt` 命令**——用于生成加密密码，以便在 `/etc/grub/grub.conf` 文件中使用的命令。

**`GRUB` 根分区**——包含 `GRUB` 引导加载器第二阶段和 `/boot/grub/grub.conf` 文件的分区。

**`GTK+` 工具包**——用于 C 语言编程的开发工具包；它用于 `GNOME` 桌面和 GNU 图像处理程序（`GIMP`）。

**`init` 命令**——用于将操作系统从一个运行级别切换到另一个运行级别的命令。

**初始化（`init`）守护进程**——由 Linux 内核启动的第一个进程；它负责启动和停止其他守护进程。

**`initstate`**——另见运行级别。

**K 桌面环境（`KDE`）**——由 Matthias Ettrich 于 1996 年创建的桌面环境。

**`KDE` 显示管理器（`kdm`）**——一种类似于 `KDE` 桌面的用户图形登录屏幕。

**K 窗口管理器（`kwin`）**——在 `KDE` 桌面环境下工作的窗口管理器。

**`lilo` 命令**——基于 `/etc/lilo.conf` 中的配置信息重新安装 `LILO` 引导加载器的命令。

**Linux 加载器（`LILO`）**——在 Linux 系统中常用的引导加载器。

**主引导记录（`MBR`）**——通常位于第一块硬盘驱动器第一个扇区的一小块区域，用于定义分区和引导加载器。

**最大分辨率**——显示在屏幕上的图像的最佳清晰度；它由组成图像的像素数量决定（例如，640 × 480 像素）。

**`Metacity` 窗口管理器**——Red Hat Fedora Core 2 中 `GNOME` 桌面环境的默认窗口管理器。

**`mingetty`**——用于在基于字符的终端上显示登录提示的程序。

**`mouseconfig`**——用于配置鼠标以便在 X Windows 中使用的命令。

**多用户模式**——也称为运行级别 2；该模式提供大多数守护进程和一组部分网络守护进程。

**`NTLOADER`**——用于启动 Windows NT、Windows 2000 和 Windows XP 操作系统内核的引导加载器。

**`ntsysv`**——可用于更改在每个运行级别中启动的守护进程的工具。

**加电自检（`POST`）**——计算机开机时运行的一系列初始测试，以确保硬件组件功能正常。

**`Qt` 工具包**——与 K 桌面环境一起使用的软件工具包。

**运行级别**——定义 Linux 系统中特定类型和数量守护进程的术语。

**`runlevel` 命令**——用于显示当前和最近（之前）运行级别的命令。

**单用户模式**——也称为运行级别 1；该模式提供单个终端和有限的一组服务。

**`system-config-display`**——用于配置视频适配卡显示器以便在 X Windows 中使用的命令。

**`system-config-keyboard`**——用于配置键盘以便在 X Windows 中使用的命令。

**`system-config-mouse`**——另见 `mouseconfig`。

**Tab 窗口管理器（`twm`）**——在 Linux 系统中使用的最古老的窗口管理器之一。

**`telinit` 命令**——`init` 命令的别名。

**`vmlinuz-<内核版本>`**——Linux 内核文件。

**窗口管理器**——负责确定由 X Windows 在屏幕上绘制的窗口外观的 GUI 组件。

**X 客户端**——X Windows 中请求从 X 服务器绘制图形并在终端屏幕上显示它们的组件。

**X 显示管理器（`xdm`）**——图形登录屏幕。

**`Xfce` 桌面环境**——Linux 系统中常用的桌面环境。
