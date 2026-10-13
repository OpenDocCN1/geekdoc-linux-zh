
通过 `dosemu` 软件包自带的实用程序，你可以运行 DOS 应用程序，并让你的计算机像运行 DOS 一样工作。这包括访问硬件、处理 DOS 以及使用 DOS 文件系统。

可以使用以下命令在 Linux 中启动 `dosemu`：

- `dosemu` — 在任何 shell 中启动 DOS 模拟器。
- `xdosemu` — 在自己的 X 窗口中启动 DOS 模拟器。
- `xterdos` — 在 `xterm` 窗口中启动 DOS 模拟器。
- `dosdebug` — 启动调试程序以查看有关运行中的 DOS 程序的信息和错误消息。

你的 DOS 环境的基本信息设置在 `/etc/dosemu/dosemu.conf` 文件中。以下列表描述了如何设置 DOS 环境以及如何更改：

- `CPU` — CPU 设置为模拟 80386（兼容 Intel 386）。你可以通过将 `$_cpu` 值更改为 `80486` 或 `80586` (`Pentium`)。
- `Keyboard` — 键盘设置为 `auto`，它会尝试根据当前的 Linux 控制台设置设置键盘。你可以通过将 `$_layout` 值设置为 `dosemu` 中列出的其他国家/语言组合列表来专门更改键盘类型。

## 第 5 章：访问和运行应用程序 223

### 在 Linux 中安装 Windows 应用程序

有几种很有前景的方法可以让你运行 Windows 应用程序。以下是其中一些：

- `WINE` — `WINE` 项目 (`winehq.com`) 在让为 Windows 创建在 Linux 和其他系统中运行方面取得了巨大进展。`WINE` 并不是真正的模拟器，因为它实现了 Win32 接口 (`API`)。
- `Win4Lin` — `Win4Lin` (`win4lin.com`) 是一种运行 Windows 系统的商业产品。你可以免费尝试 14 天。安装包括三个步骤：安装 `Win4Lin`、安装客操作系统（Windows 98、2000 或 ME；XP 仍在实验阶段）以及设置设置。
- `QEMU` — `QEMU` (`qemu.com`) 是一个作为处理器模拟器的开源项目。它可以模拟整个系统，也可以处于用户模式（可以用于为不同 CPU 编译的进程）。在全模拟中，`QEMU` 可以运行多种操作系统：Windows 3.1、95、98SE、ME、2000 和 XP。为了尝试其他系统的应用程序，`QEMU` 也可以 Linux 和其他类 Unix 系统运行。

本节剩余部分介绍了如何获取和使用 `WINE` 在 Linux 中运行应用程序。你可以通过以下地方获取 Windows 系统：

- 下载站点 — 你可以从不同的网站免费下载 `WINE`。访问 `winehq.com` 获取下载列表。我从 `http://sourceforge.net/projects/wine/` 下载了为 Fedora Core 3 构建的最新 RPM。（如果出现了 Fedora Core 4 版本，你应该使用该版本）。
- `Cedega` — `TransGaming, Inc.` (`transgaming.com`) 提供 `WINE` 的商业变体（称为 `WineX`）。`TransGaming` 专注于在 Linux 中运行为 Windows 创建的应用程序，并 `WINE` 为基础。有关 `Cedega` 的描述请参见第 7 章。
- `CodeWeavers` — 如果你需要 Microsoft Office 或浏览器插件，`CodeWeavers` (`codeweavers.com`) 分别提供 `CrossOver Office` 和 `CrossOver Plug-in`。尽管这些产品需要付费，但它们提供了友好的界面来安装和管理其支持的 Windows 软件和浏览器插件。

虽然确实可以使用

从 Windows 到 Linux 的桌面系统，`WINE` 的现状提供了一个机会，让你查看你需要的 Windows 应用程序是否可以在 Linux 上运行。

> 警告：我建议在将任何应用程序部署到作为工作关键部分的计算机之前，先在 `WINE` 中测试你想要使用的任何程序。虽然我没有给我的电脑造成过严重损坏，但在某些情况下 `WINE` 仍然会导致桌面冻结。请查看项目列表中列出的组织，以获取有关在 Fedora 中运行 Windows 应用程序的相关问题。

除了开发软件外，`WINE` 项目还维护了一个在 `WINE` 下运行的应用程序数据库。目前列出了 1000 多个应用程序，尽管其中许多只能部分运行。然而，关键在于应用程序列表正在不断增长，并且正特别关注让重要的 Windows 98 和 2000 应用程序运行。

虽然不是源码产品，但 `QEMU` 和 `WinLin` 是运行 Windows 应用程序的其他良好方法，配合同一台运行计算机上的 Linux 系统使用。通过 `QEMU`，你可以在同一台 PC 上同时运行 Windows 98/NT/2000 和 Linux 操作系统。通常情况下，Windows 应用程序在 `QEMU` 中崩溃的概率比在 `WINE` 中低（因为你实际上运行了整个 Windows 操作系统），但性能会更差（因为你在操作系统内部运行操作系统）。

下一节将介绍如何设置 Linux 使用 `WINE` 运行 Microsoft Windows 应用程序。

# 理解 WINE

为了让 `WINE` 能够运行 Microsoft Windows 应用程序，它需要一个类似于 Microsoft Windows 系统的环境。本节将带你完成从 `source.net/projects/wine` 为 Fedora Core（位于 Red Hat Packages）安装并配置最新 `wine` RPM 的步骤。

当你在 Fedora Core 中安装 `wine` 包时，该包会创建 `/etc/wine/config` 文件，Windows 注册表通过该文件识别应用程序在 Microsoft Windows 操作系统所需的组件位置。

`WINE` 基础 Windows 操作系统目录的位置是 `$HOME/.wine/drive` 目录，它在 `wine` 看来就像 `C:` 盘。`$HOME/.wine` 目录在用户第一次运行 `wine` 命令时自动创建。驱动器号在 `$HOME/.wine/dosdevices` 目录中分配。

> 注意：如果你在 `WINE` 中访问光驱或其他驱动器时遇到困难扰，请检查 `dosdevices` 目录。如果 CD 没在 `dosdevices` 目录中显示为 `d:`，你可以通过输入类似下面的内容自己创建一个链接：

```
# ln -s /media/recorder $HOME/.wine/dosdevices/d:
```

表 5-5 显示了 `C:` 和其他 Windows 驱动器号映射到 Linux 目录和设备。

# 表 5-5：WINE 中的 Microsoft Windows 驱动器号

| 描述 | 驱动器号或 | Linux 目录输出 | 设备名称（如适用） |
|---|---|---|---|---|
| 软盘 | `A:` | `/mnt/floppy` | `/dev/fd0` | |
| 硬盘 #1 | `C:` | `$HOME/.wine/drive_c` | | |
| 光驱 | `D:` | `/mnt/cdrom` | `/dev/cdrom` | |
| 临时目录 | `E:` | `/tmp` | | |
| 用户主目录 | `F:` | `$HOME` (用户主目录) | | |
| 根目录 | `Z:` | `/` | | |
| 串口 | `COM1` | | `/dev/tty0` | |
| | `COM2` | | `/dev/tty1` | |
| | `COM3` | | `/dev/tty2` | |
| | `COM4` | | `/dev/modem` | |
| 并口 | `LPT1` | | `/dev/lp0` | |
| 打印后台程序 | `LPT1` | 将打印作业通过管道交给 `lpr` 命令 (`| lpr`) | | |
| WineLook | `Win95` (系统显示应用程序的形式: `Win31`, `Win98` 或默认的 `Win95`) | | | |

在 `$HOME/.wine/drive_c` 目录（即你的 `C:` 盘）中，如果你来自旧版本的 Windows 环境，你应该能看到一些你熟悉的内容：`Program Files` 和 `windows` 目录。

假设基础目录结构对你没有问题，你可能仍然想更改一些东西。例如，你可能想将 `/etc/wine/wine/config` 文件中的命令更改为 `| lpr|` 以外的内容，以便使用特定的打印机或添加某些 Linux 打印选项。

> 注意：有关配置 `wine.conf` 文件的详情，请参 `Wine` 用户指南。当你安装 Fedora Core 的 `wine` RPM 时，该指南 (`wineuser.pdf`) 位于 `/usr/share/doc/wine*` 目录下。

对于包含在 CD 或 DVD 上的 Windows 应用程序，你可以尝试通过简单使用 `wine` 命令运行该介质上的设置程序来安装它们。因此，在插入并挂载包含你想安装的应用程序的 CD 后，你可以运行如下的命令：

```
# wine d:\setup.exe
```

该应用程序将像在 Windows 中一样运行，并将应用程序安装到你的硬盘上。

# 设置 Microsoft Windows 应用程序
