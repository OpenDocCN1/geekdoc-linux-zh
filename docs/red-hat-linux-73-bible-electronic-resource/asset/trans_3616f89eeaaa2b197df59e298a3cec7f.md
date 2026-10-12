

被称为 Mtools 的工具集允许你在 Linux 内部处理 DOS 文件和目录。一个名为 dosemu 的 DOS 模拟器允许你在一个实际上运行在 Linux 内部的 DOS 环境中运行 DOS 应用程序（这就像 DOS 窗口在 Windows 操作系统内部运行一样）。

## 使用 Mtools

Mtools 大多是在前面加了字母 m 的 DOS 命令，它们在 Linux 中运行（尽管有几个例外，命名不同）。使用这些命令，你可以轻松处理 DOS 文件和文件系统。表 5-5 列出了 Linux 中可用的 mtools（如果你安装了 mtools 软件包）：

### 表 5-5：Linux 中可用的 Mtools

| 命令 | 功能 |
| :--- | :--- |
| mattr | DOS 的 attrib 命令，用于更改 MS-DOS 文件属性标志。 |
| mbadblocks | DOS 的 badblocks 命令，用于测试软盘并标记软盘 FAT 中的坏块。 |
| mcd | DOS 的 cd 命令，用于将工作目录更改为另一个 DOS 目录。（其他 mtools 使用的默认目录是 A:\） |
| mcheck | DOS 的 check 命令，用于验证文件。 |
| mcopy | DOS 的 copy 命令，用于将文件从一个位置复制到另一个位置。 |
| mdel | DOS 的 del 命令，用于删除文件。 |
| mdeltree | DOS 的 delttee 命令，用于删除 MS-DOS 目录及其包含的文件和子目录。 |
| mdir | DOS 的 dir 命令，用于列出目录内容。 |
| mdu | Linux 的 du 命令，用于显示 DOS 目录占用的磁盘空间量。 |
| mformat | DOS 的 format 命令，用于格式化 DOS 软盘。 |
| minfo | 此命令用于打印有关 DOS 设备（如软盘）的信息。 |
| mkmanifest | 此命令用于创建一个 shell 脚本，以恢复被 DOS 命令截断的 Linux 文件名。 |
| mlabel | DOS 的 label 命令，用于创建 DOS 卷标。 |
| mmkd | DOS 的 md 命令，用于创建 DOS 目录。 |
| mmount | 此命令用于在 Linux 中挂载 DOS 磁盘。 |
| mmove | DOS 的 move 命令，用于将文件移动到另一个目录和/或重命名。 |
| mrd | DOS 的 rd 命令，用于删除 DOS 目录。 |
| mread | DOS 的 copy 命令，用于将 DOS 文件从一个位置复制到另一个位置。 |
| mren | DOS 的 ren 命令，用于重命名 DOS 文件。 |
| mshowfat | 此命令用于显示 DOS 文件系统中文件的 FAT 条目。 |
| mtoolstest | 此命令用于测试 mtools 配置文件。 |
| mtype | DOS 的 type 命令，用于显示 DOS 文本文件的内容。 |
| mz | 此命令用于对 Zip 磁盘执行操作，包括弹出、写保护和查询。 |

我通常使用 mtools 在我的 Linux 系统和一个不在我网络中的 Windows 系统之间复制文件。我最常使用 mcopy，它允许我使用驱动器字母而不是设备名来复制文件。换句话说，要将文件 vi.exe 从软驱 A: 复制到 Linux 中的当前目录，我会键入：

```
# mcopy a:/vi.exe
```

> **注意：** 默认情况下，软盘驱动器只能由 root 用户和 floppy 组读取或写入。为了使软驱对所有人可访问（假设是软驱 A:），请以 root 用户身份键入以下内容：`chmod 666 /dev/fd0`。

## 使用 dosemu 和 xdosemu

DOS 模拟器软件包 dosemu 和 xdosemu 不再随 Red Hat Linux 发行版提供。这些软件包以前是 Red Hat PowerTools 的一部分。现在你可以从 Red Hat Linux FTP 站点获取这些软件包，或使用 rpmfind 命令获取。

通过 **dosemu** 和 **xdosemu** 软件包提供的实用程序，你可以运行 DOS 应用程序，也可以使用你的计算机就像它正在运行 DOS 一样。这包括访问硬件、处理 DOS 配置文件以及使用 DOS 文件系统。

以下命令可用于在 Linux 中启动 dosemu：

- `dos` — 在任何 shell 中启动 DOS 模拟器。
- `xdos` — 在其自己的 X 窗口中启动 DOS 模拟器。
- `xtermdos` — 在 xterm 窗口中启动 DOS 模拟器。
- `dosdebug` — 启动调试程序以查看关于正在运行的 DOS 程序的信息和错误消息。

有关 DOS 环境的基本信息在 `/etc/dosemu.conf` 文件中设置。以下列表包含有关如何设置 DOS 环境以及如何更改它的信息：

- **CPU** — CPU 设置为模拟 80386（Intel 386 兼容）。你可以将 `$_cpu` 值更改为 80486 或 80586（用于 Pentium）。
- **键盘** — 键盘设置为 `auto`，它尝试根据当前的 Linux 控制台设置来设置键盘。你可以通过将 `$_layout` 值设置为 `dosemu.conf` 文件中列出的各种其他国家/语言组合（例如美国的 `us`、德国的 `de` 或意大利的 `it`）来专门更改键盘类型。
- **X 设置** — 有几个 X 设置（以 `$_x` 开头），允许你更改诸如 DOS 窗口标题、使用的字体以及光标闪烁率等事项。
- **软盘** — 软盘 A（`/dev/fd0`）被设置为 3.5 英寸软盘（`threeinch`），软盘 B（`/dev/fd1`）未被分配。任一磁盘都可以被分配为 3.5 英寸（`threeinch`）、5.25 英寸（`fiveinch`）、`atapi` 或 `empty`。
- **硬盘映像** — 当你启动 DOS 时出现的文件系统实际上是存储在 `/var/lib/dosemu` 中的磁盘映像文件。默认情况下，dosemu 使用 `hdimage.first`（它链接到 `hdimage.freedos`）。你可以将其更改为另一个 DOS 映像或 DOS 文件系统（例如 `/dev/hda1`，如果该分区是 DOS 分区）。
- **串行端口** — 默认情况下未分配任何串行端口。你可以将任何串行端口（`$_com1` 到 `$_com4`）分配给设备，如调制解调器（`/dev/modem`）、鼠标（`/dev/mouse`）或终端行（`/dev/tty0`）。

Dosemu 是为 root 用户设置的。允许多个用户访问 DOS 并不安全，因为 DOS 没有像 Linux 那样对文件和设备进行相同的安全保护。但是，如果你希望 Linux 系统上的其他用户使用 DOS，请编辑 `/etc/dosemu.users` 文件，使其包含以下行：

```
root c_all
all c_all
```

有关 dosemu 的更多信息，请访问 dosemu 主页 www.dosemu.org。

## 使用 WINE 运行 Windows 应用程序

WINE 项目（www.winehq.com）在让为 Microsoft Windows 创建的应用程序在 Linux 和其他操作系统上运行方面取得了巨大进展。WINE 实际上并不是一个模拟器，因为它并不模拟整个 Windows 操作系统。相反，由于它实现了 Win32 应用程序编程接口（APIs）和 Windows 3.x 接口，WINE 项目更像是一个“Windows 兼容层”。

WINE 仍在开发中，尽管 Red Hat Linux 附带的光盘上提供了一个初步版本。虽然使用 WINE 可以运行许多 Windows 应用程序，但要让大多数 Windows 应用程序正常工作仍需要一些调整。如果你正在考虑将桌面系统从 Windows 迁移到 Linux，WINE 的现状提供了一个机会，让你看看你需要的某些 Windows 应用程序是否可以在 Linux 中运行。

> **警告：** 我建议你不要在作为你工作关键部分的计算机上使用 WINE。虽然我没有对计算机造成任何严重损害，但 WINE 在某些条件下仍会冻结你的桌面。

除了开发软件外，WINE 项目还维护了一个在 WINE 下运行的应用程序数据库。列出了超过 1000 个应用程序，尽管其中许多只是部分可操作。然而，重点是应用程序列表正在增长，并且正特别注意让重要的 Windows 3.1、95 和 98 应用程序运行起来。

> **提示：** 虽然 VMware 不是开源产品，但它是另一种在同一个运行计算机上同时运行 Windows 应用程序和 Linux 系统的好方法。使用 VMware，你可以在同一台 PC 上同时运行 Windows 98、Windows NT、Windows 2000 和 Linux 操作系统。你可以从 www.vmware.com 获取有关 VMware 的更多信息。

以下部分描述了如何设置你的 Linux 系统以使用 WINE 运行 Windows 应用程序。

> **注：** 一个名为 WineX 的独立项目，由 Transgaming, Inc.（www.transgaming.com）开发，专注于使用 WINE 作为底层技术将 Windows 游戏带到 Linux。关于 WineX 的描述请参阅第 7 章。

