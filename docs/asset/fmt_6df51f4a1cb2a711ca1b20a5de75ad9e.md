
| `mbadblocks` | DOS 的 badblocks 命令，用于测试软盘并标记软盘上包含的坏块在其 FAT 中。 |
| `mcd` | DOS 的 cd 命令，用于将工作目录更改为另一个 DOS 目录。（其他 mtools 使用的默认目录是 A:\） |
| `mcheck` | DOS 的 check 命令，用于验证文件。 |
| `mcopy` | DOS 的 copy 命令，用于将文件从一个位置复制到另一个位置。 |
| `mdel` | DOS 的 del 命令，用于删除文件。 |
| `mdeltree` | DOS 的 deltree 命令，用于删除 MS-DOS 目录及其包含的文件和子目录。 |
| `mdir` | DOS 的 dir 命令，用于列出目录内容。 |
| `mdu` | Linux 的 du 命令，用于显示 DOS 目录使用的磁盘空间量。 |
| `mformat` | DOS 的 format 命令，用于格式化 DOS 软盘。 |
| `minfo` | 此命令用于打印有关 DOS 设备（如软盘）的信息。 |
| `mkmanifest` | 此命令用于创建一个 shell 脚本，以恢复被 DOS 命令截断的 Linux 文件名。 |
| `mlabel` | DOS 的 label 命令，用于创建 DOS 卷标。 |
| `mmkdir` | DOS 的 md 命令，用于创建 DOS 目录。 |
| `mmount` | 此命令用于在 Linux 中挂载 DOS 磁盘。 |
| `mmove` | DOS 的 move 命令，用于将文件移动到另一个目录和/或重命名它。 |
| `mrmdir` | DOS 的 rmdir 命令，用于删除 DOS 目录。 |
| `mren` | DOS 的 ren 命令，用于重命名 DOS 文件。 |
| `mshowfat` | 此命令用于显示 DOS 文件系统中文件的 FAT 项。 |
| `mtooltest` | 此命令用于测试 mtools 配置文件。 |
| `mtype` | DOS 的 type 命令，用于显示 DOS 文本文件的内容。 |
| `mzip` | 此命令用于对 Zip 磁盘执行操作，包括弹出、写保护和查询。 |

我通常使用 `mtools` 在我的 Linux 系统和未连接在我网络中的 Windows 系统之间复制文件。我最常用的是 `mcopy`，它允许我使用驱动器字母而不是设备名称来复制文件。换句话说，要将文件 `vi.exe` 从软盘驱动器 `A:` 复制到 Linux 中的当前目录，我会输入：

```bash
# mcopy a:\vi.exe .
```

> 注意：默认情况下，软盘驱动器只能由 root 用户和 floppy 组读取或写入。若要使软盘驱动器对所有人可访问（假设它是软盘驱动器 A:），请以 root 用户身份输入以下命令：`chmod 666 /dev/fd0`。

### 使用 dosemu

DOS 模拟器软件包 `dosemu` 未随 Fedora Core 发行版提供。若要使用 `dosemu`，请从 `dosemu.sourceforge.net` 下载 `dosemu` RPM 文件。

借助 `dosemu` 软件包附带的实用程序，您可以运行 DOS 应用程序，并像计算机正在运行 DOS 一样使用它。这包括访问硬件、处理 DOS 配置文件以及使用 DOS 文件系统。

以下命令可用于在 Linux 中启动 `dosemu`：

- `dosemu` — 在任何 shell 中启动 DOS 模拟器。
- `xdosemu` — 在独立的 X 窗口中启动 DOS 模拟器。
- `xtermdos` — 在 xterm 窗口中启动 DOS 模拟器。
- `dosedbg` — 启动一个调试程序，以查看有关正在运行的 DOS 程序的信息和错误消息。

您的 DOS 环境的基本信息在 `/etc/dosemu/dosemu.conf` 文件中设置。以下列表描述了 DOS 环境的设置方法以及如何更改它：

- **CPU** — CPU 设置为模拟 80386（与 Intel 386 兼容）。您可以将 `$cpu` 值更改为 80486 或 80586（用于 Pentium）。
- **键盘** — 键盘设置为 auto，它尝试根据当前的 Linux 控制台设置来设置键盘。您可以通过将 `$layout` 值设置为 `dosemu.conf` 文件中列出的各种其他国家/语言组合（例如美国/英语的 *us*、德语的 *de* 或意大利语的 *it*）来具体更改键盘类型。
- **X 设置** — 有几个 X 设置（以 `$X` 开头），允许您更改诸如 DOS 窗口标题、使用的字体和光标闪烁率等内容。
- **软盘** — 软盘 A（`/dev/fd0`）设置为 3.5 英寸软盘（*threeminch*），软盘 B（`/dev/fd1`）未分配。两个磁盘均可设置为 3.5 英寸（*threeminch*）、5.25 英寸（*fiveminch*）、*atapi* 或 *empty*。
- **硬盘镜像** — 启动 DOS 时显示的文件系统实际上是存储在 `/var/lib/dosemu` 中的磁盘镜像文件。默认情况下，`dosemu` 使用 `hdimage.first`（该文件链接到 `hdimage.freedos`）。您可以将其更改为另一个 DOS 镜像或 DOS 文件系统（例如 `/dev/hda1`，如果该分区是 DOS 分区）。
- **串行端口** — 默认情况下未分配任何串行端口。您可以将任何串行端口（`$com1` 到 `$com4`）分配给设备，例如调制解调器（`/dev/modem`）、鼠标（`/dev/mouse`）或终端线路（`/dev/tty0`）。

`dosemu` 软件包是为 root 用户设置的。允许多个用户访问 DOS 并不是非常安全的，因为 DOS 没有像 Linux 那样对文件和设备进行相同的安全保护。但是，如果您希望 Linux 系统上的其他用户使用 DOS，请编辑 `/etc/dosemu.users` 文件，使其包含以下行：

```text
root c_all
all c_all
```

有关 `dosemu` 的更多信息，请访问 `www.dosemu.org` 上的 `dosemu` 主页。

#### 在 WINE 中运行 Microsoft Windows 应用程序

`WINE` 项目（`www.winehq.com`）在使为 Microsoft Windows 创建的应用程序能在 Linux 及其他操作系统上运行方面取得了巨大进展。`WINE` 实际上并不是一个模拟器，因为它并不模拟整个 Windows 操作系统。相反，由于它实现了 Win32 软件编程接口（API）和 Windows 3.x 接口，`WINE` 项目更像是一个“Windows 兼容层”。

要在 Fedora 系统中获取 `WINE`，你可以前往以下位置：

- **下载站点** 你可以从几个不同的网站免费下载 `WINE`。请访问 `winehq.com` 查看下载站点列表。我从 `http://sourceforge.net/projects/wine/` 下载了为 Fedora Core 2 构建的最新 RPM。（如果 Fedora Core 3 版本可用，你应该最好使用那个版本。）
- **Cedega** `TransGaming, Inc.`（`www.transgaming.com`）提供名为 `Cedega`（原名 `WineFX`）的 `WINE` 商业版本。`TransGaming` 专注于使用 `WINE` 作为基础在 Linux 中运行 Windows 游戏。有关 `Cedega` 的说明，请参见第 7 章。
- **CodeWeavers** 如果你需要 Microsoft Office 或 Web 浏览器插件，`CodeWeavers`（`www.codeweavers.com`）分别提供 `CrossOver Office` 和 `CrossOver` 插件。虽然这些产品需要付费，但它们提供了友好的界面来安装和管理其所支持的 Windows 软件和浏览器插件。

虽然确实可以使用 `WINE` 运行许多 Windows 应用程序，但仍需进行一些调试才能使许多 Windows 应用程序正常工作。如果你正在考虑将桌面系统从 Windows 迁移到 Linux，`WINE` 的现状提供了一个机会，让你看看你所需的一些 Windows 应用程序是否能在 Linux 中运行。

> **注意：** 我建议在将任何你想在 `WINE` 中使用的应用程序部署到作为你工作关键部分计算机之前，先对其进行测试。虽然我没有对计算机造成严重损坏，但 `WINE` 在某些情况下仍会冻结桌面。请咨询项目符号列表中列出的组织，了解与在 Fedora 中运行 Windows 应用程序相关的特定问题。

除了开发软件外，`WINE` 项目还维护了一个在 `WINE` 下运行的应用程序数据库。列出了 1000 多个应用程序，尽管其中许多只是部分可用。然而，其意义在于，应用程序列表正在增长，并且特别关注让重要的 Windows 98 和 2000 应用程序得以运行。
