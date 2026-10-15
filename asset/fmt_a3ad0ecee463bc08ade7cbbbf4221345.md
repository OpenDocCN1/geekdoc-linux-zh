
### 表 5-4: Linux 中可用的 mtools

| 命令 | 功能 |
|---|---|
| `mattr` | DOS `attrib` 命令，用于更改 MS-DOS 文件属性标志。 |
| `mbadblocks` | DOS `badblocks` 命令，用于测试软盘并标记软盘 FAT 中包含的任何坏块。 |
| `mcd` | DOS `cd` 命令，用于将工作目录更改为其他 DOS 目录。（默认目录是 A:），供其他 `mtools` 使用。 |
| `mcheck` | DOS `check` 命令，用于验证文件。 |
| `mcopy` | DOS `copy` 命令，用于将文件从一个位置复制到另一个位置。 |
| `mdel` | DOS `del` 命令，用于删除文件。 |
| `mdeltree` | DOS `deltree` 命令，用于删除 MS-DOS 目录及其包含的文件和子目录。 |
| `mdir` | DOS `dir` 命令，用于列出目录的内容。 |
| `mdu` | Linux `du` 命令，用于显示 DOS 目录使用的磁盘空间量。 |
| `mformat` | DOS `format` 命令，用于格式化 DOS 软盘。 |
| `minfo` | 此命令用于打印有关 DOS 设备（如软盘）的信息。 |
| `mkmanifest` | 此命令用于创建恢复被 DOS 命令截断的 Linux 文件名的 shell 脚本。 |
| `mlabel` | DOS `label` 命令，用于创建 DOS 卷标。 |
| `mmd` | DOS `md` 命令，用于创建 DOS 目录。 |
| `mmount` | 此命令用于在 Linux 中挂载 DOS 磁盘。 |
| `mmv` | DOS `move` 命令，用于将文件移动到另一个目录和/或重命名它。 |
| `mrd` | DOS `rd` 命令，用于删除 DOS 目录。 |
| `mren` | DOS `ren` 命令，用于重命名 DOS 文件。 |
| `mshowfat` | 此命令用于显示 DOS 文件系统中文件的 FAT 条目。 |
| `mtoolestest` | 此命令用于测试 `mtools` 配置文件。 |
| `mtype` | DOS `type` 命令，用于显示 DOS 文本文件的内容。 |
| `mzip` | 此命令用于执行 Zip 磁盘操作，包括弹出、写保护和查询。 |

我过去使用 `mtools` 在我的 Linux 系统和网络上的一台 Windows 系统之间复制文件。我会使用 `mcopy`，它允许我使用驱动器字母而不是设备名称来复制文件。换句话说，要将文件 `vi.exe` 从软盘驱动器 A: 复制到 Linux 中的当前目录，我会输入：

```bash
# mcopy a:\vi.exe .
```

## 使用 DOSBox

要在 Fedora 中运行经典 DOS 应用程序，需要安装 `dosbox` 包。以 root 用户身份运行以下命令来安装 `dosbox`：

```
# yum install dosbox
```

安装 DOSBox 后，只需输入 `dosbox` 即可在桌面上打开一个 DOSBox 窗口。在这个窗口中，你拥有一个可以运行许多经典 DOS 应用程序的环境。假设你的 Fedora 系统中已经存储了一些你想运行的 DOS 应用程序，你可以通过挂载包含这些应用程序的目录来使它们可用。例如，要将 `/home/chris` 目录挂载到 DOSBox 的 C 盘，请输入以下命令：

```
Z:> mount c /home/chris
```

此时，你可以使用标准 DOS 命令来访问和运行刚刚挂载目录中的应用程序。例如，输入 `dir c:` 可以查看刚刚挂载目录的内容。输入 `c:` 进入该目录。然后通过输入应用程序名称来运行存储在该目录中的 DOS 应用程序。

要挂载光盘，你需要在挂载时指定文件系统类型。例如：

```
Z:> mount d /media/disk -t cdr
```

有关在 `dosbox` 中使用特殊键和功能的信息，请参阅 `dosbox` 的 README 文件（`/usr/share/doc/dosbox-*/README`）。

## 在 Linux 中运行 Microsoft Windows 应用程序

你可以采取几种有前景的方法，使 Windows 应用程序在运行的 Linux 会话中工作。以下是其中几种：

- `WINE` — `WINE` 项目（www.winehq.org）在让为 Microsoft Windows 创建的应用程序在 Linux 及其他操作系统上运行方面取得了巨大进展。`WINE` 实际上并不是一个模拟器，因为它并不模拟整个 Windows 操作系统。相反，由于它实现了 Win32 应用程序编程接口（API）和 Windows 3.x 接口，`WINE` 项目更像是一个“Windows 兼容层”。`WINE` 不需要安装 Windows。不过，如果你有，它可以利用 Windows dll 文件。

- `Win4Lin` — `Win4Lin`（www.win4lin.com）是一款用于在 Linux 中运行 Windows 系统的商业产品。你可以免费试用该软件 14 天。安装过程包括三个步骤：安装 `Win4Lin`（提供 RPM 格式），安装客户操作系统（Windows 98、2000 或 ME；XP 仍处于实验阶段），以及设置客户会话。当你从 Linux 桌面运行完整的 Windows 系统时，你可以安装和运行任何你选择的 Windows 应用程序。

- `QEMU` — `QEMU`（www.qemu.org）是一个开源项目，充当处理器模拟器。它可以模拟完整系统，或者工作在用户模式模拟下（在那里它可以用来测试为不同 CPU 编译的过程）。在完整系统模拟中，`QEMU` 可以运行多种操作系统，包括 Windows 3.11、95、98SE、ME、2000，以及可能支持 XP。

为了尝试为其他操作系统设计的应用程序，`QEMU` 还可以运行几种 Linux（Fedora、KNOPIX、Mandrake、Morphix、Debian 以及其他）和其他 UNIX 类系统（NetBSD、Solaris 以及其他）。`QEMU` 可以利用最近添加到 Linux 内核（本章后面会有描述）的 KVM 虚拟化功能。

本节其余部分描述如何获取和使用 `WINE` 在 Linux 中运行 Windows 应用程序。要在 Fedora 系统中获取 `WINE`，你可以前往以下地点：

- **Fedora 中的 WINE** — 从 Fedora 7 开始，`WINE` 成为主要 Fedora 软件仓库的一部分。使用 `WINE` 需要 `wine` 和 `wine-core` 包。额外的 `WINE` 支持来自以下软件包：`wine-capi`（ISDN 支持）、`wine-cms`（颜色管理）、`wine-esd`（ESD 声音支持）、`wine-jack`（JACK 声音支持）、`wine-ldap`（LDAP 支持）、`wine-nas`（NAS 声音支持）、`wine-tools`（有用的 Windows 实用工具），以及 `wine-twain`（扫描仪支持）。添加 `wine-docs` 可获得更多文档，或添加 `wine-devel` 获取 `WINE` 开发组件。

- **Cedega** — 一种名为 `Cedega`（以前称为 WineX）的商业版 `WINE` 由 TransGaming, Inc.（www.transgaming.com）提供。TransGaming 专注于使用 `WINE` 作为基础在 Linux 中运行 Windows 游戏。有关 `Cedega` 的描述，请参见第 7 章。

- **CodeWeavers** — 如果你需要 Microsoft Office 或 Web 浏览器插件，CodeWeavers（www.codeweavers.com）提供 CrossOver Linux。虽然 CrossOver Linux 需要付费，但它提供了安装和管理 Windows 软件的友好界面。提供 30 天免费试用。

虽然确实可以使用 `WINE` 运行许多 Windows 应用程序，但为了让许多 Windows 应用程序正常工作，仍然需要一些调整。如果你正考虑将桌面系统从 Windows 迁移到 Linux，`WINE` 的当前状态提供了一个机会，让你看看你需要的某些 Windows 应用程序是否可以在 Linux 上运行。

除了开发软件外，`WINE` 项目还维护了一个在 `WINE` 下运行的应用程序数据库（http://appdb.winehq.org）。列出了 1000 多个应用程序，尽管其中许多只是部分可操作。然而，重点是应用程序列表正在增长，并且特别关注让重要的 Windows 2000 和 XP 应用程序运行起来。

尽管 `Win4Lin` 不是开源产品，但它也是运行 Windows 应用程序的好方法之一，可以在同一台运行中的计算机上与 Linux 系统一起运行。利用开源 `QEMU` 项目，你可以同时在同一台 PC 上运行 Microsoft Windows 和 Linux 操作系统。（有关支持操作系统的完整列表，请参见 http://qemu.org/ossupport.html。）
