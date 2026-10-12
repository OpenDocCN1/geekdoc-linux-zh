

## 表 5-4：Linux 中可用的 Mtools

| 命令 | 功能 |
|---|---|
| mattrib | DOS attrib 命令，用于更改 MS-DOS 文件属性标志。 |
| mbadblocks | DOS badblocks 命令，用于测试软盘并将软盘上包含的任何坏块在其 FAT 中标记出来。 |
| mcd | DOS cd 命令，用于将工作目录更改为另一个 DOS 目录。（默认目录是 A:\)，供其他 mtools 使用。 |
| mcheck | DOS check 命令，用于验证文件。 |
| mcopy | DOS copy 命令，用于将文件从一个位置复制到另一个位置。 |
| mdel | DOS del 命令，用于删除文件。 |
| mdeltree | DOS deltree 命令，用于删除 MS-DOS 目录及其包含的文件和子目录。 |
| mdir | DOS dir 命令，用于列出目录内容。 |
| mdu | Linux du 命令，用于显示 DOS 目录使用的磁盘空间量。 |
| mformat | DOS format 命令，用于格式化 DOS 软盘。 |
| minfo | 此命令用于打印有关 DOS 设备（如软盘）的信息。 |
| mkmanifest | 此命令用于创建一个 Shell 脚本，以恢复被 DOS 命令截断的 Linux 文件名。 |
| mlabel | DOS label 命令，用于创建 DOS 卷标。 |
| mmd | DOS md 命令，用于创建 DOS 目录。 |
| mmount | 此命令用于在 Linux 中挂载 DOS 磁盘。 |
| mmove | DOS move 命令，用于将文件移动到另一个目录和/或重命名它。 |
| mrd | DOS rd 命令，用于删除 DOS 目录。 |
| mren | DOS ren 命令，用于重命名 DOS 文件。 |
| mshowfat | 此命令用于显示 DOS 文件系统中文件的 FAT 条目。 |
| mtoolstest | 此命令用于测试 mtools 配置文件。 |
| mtype | DOS type 命令，用于显示 DOS 文本文件的内容。 |
| mzip | 此命令用于对 Zip 磁盘执行操作，包括弹出、写保护和查询。 |

我通常使用 `mtools` 在我的 Linux 系统和一个不在我的网络上的 Windows 系统之间复制文件。我最常用的是 `mcopy`，它让我可以使用驱动器盘符而不是设备名称来复制文件。换句话说，要将文件 `vi.exe` 从软盘驱动器 `A:` 复制到 Linux 中的当前目录，我会输入：

```
# mcopy a:\vi.exe
```

> **注意：** 默认情况下，软盘驱动器只能由 root 用户和 floppy 组读取或写入。要使软盘驱动器对所有人可访问（假设是软盘驱动器 A:），请以 root 用户身份输入以下命令：`chmod 666 /dev/fd0`。

### 使用 dosemu

DOS 模拟器软件包 `dosemu` 不再随 Red Hat Linux 发行版附带。要使用 `dosemu`，可以尝试从 `dosemu.sourceforge.net` 安装源代码。

借随 `dosemu` 软件包附带的实用程序，您可以运行 DOS 应用程序，并像在运行 DOS 一样使用您的计算机。这包括访问硬件、处理 DOS 配置文件以及使用 DOS 文件系统。

以下命令可用于在 Linux 中启动 `dosemu`：

- `dos` — 在任何 Shell 中启动 DOS 模拟器。
- `xdos` — 在其自己的 X 窗口中启动 DOS 模拟器。
- `xterm dos` — 在 xterm 窗口中启动 DOS 模拟器。
- `dosdebug` — 启动调试程序以查看有关正在运行的 DOS 程序的信息和错误消息。

关于您的 DOS 环境的基本信息设置在 `/etc/dosemu.conf` 文件中。以下列表描述了 DOS 环境的设置方式以及如何更改它：

- **CPU** — CPU 设置为模拟 80386（兼容 Intel 386）。您可以将 `$_cpu` 值更改为 80486 或 80586（用于 Pentium）。
- **键盘** — 键盘设置为 `auto`，这会尝试根据当前的 Linux 控制台设置来设置键盘。您可以通过将 `$_layout` 值设置为 `dosemu.conf` 文件中列出的各种其他国家/语言组合（例如 `us` 代表美式/英语，`de` 代表德语，或 `it` 代表意大利语）来专门更改键盘类型。
- **X 设置** — 有几个 X 设置（以 `$_x` 开头），可让您更改诸如 DOS 窗口中的标题、所用字体和光标闪烁率等内容。
- **软盘** — 软盘 A（`/dev/fd0`）设置为 3.5 英寸软盘（三英寸），软盘 B（`/dev/fd1`）未分配。任一磁盘均可分配为 3.5 英寸（三英寸）、5.25 英寸（五英寸）、atapi 或空。
- **硬盘镜像** — 启动 DOS 时出现的文件系统实际上是一个存储在 /var/lib/dosemu 中的磁盘镜像文件。默认情况下，dosemu 使用 hdimage.first（链接到 hdimage.freedos）。您可以将其更改为另一个 DOS 镜像或 DOS 文件系统（例如 `/dev/hda1`，如果该分区是 DOS 分区）。
- **串口** — 默认情况下未分配串口。您可以将任意串口（`_com1` 到 `_com4`）分配给设备，如调制解调器（`/dev/modem`）、鼠标（`/dev/mouse`）或终端行（`/dev/tty0`）。

Dosemu 是为 root 用户设置的。允许多个用户访问 DOS 不是很安全，因为 DOS 没有 Linux 那样对文件和设备的安全保护。但是，如果您希望 Linux 系统上的其他用户使用 DOS，请编辑 /etc/dosemu.users 文件，使其包含以下行：

```
root c_all
all c_all
```

有关 dosemu 的更多信息，请访问位于 www.dosemu.org 的 dosemu 主页。

### 使用 WINE 运行 Windows 应用程序

WINE 项目（www.winehq.com）在使为 Microsoft Windows 创建的应用程序能够在 Linux 和其他操作系统中运行方面取得了长足进步。WINE 其实并非模拟器，因为它不模拟整个 Windows 操作系统。相反，因为它实现了 Win32 应用程序编程接口（API）和 Windows 3.x 接口，WINE 项目更像是一个“Windows 兼容层”。

要为您的 Red Hat Linux 系统获取 WINE，有几个地方可以去：

- **下载站点** — 您可以从几个不同的网站免费下载 WINE。请查看 winehq.com 以获取下载站点列表。我从这个站点下载了为 Red Hat Linux 构建的最新 RPM：http://sourceforge.net/projects/wine/。WINE 每日构建版（RPM 格式）可从 http://wine.dataparty.no 获取。
- **WineX** — WINE 的商业版本，称为 WineX，可从 TransGaming, Inc.（www.transgaming.com）获得。TransGaming 专注于使用 WINE 作为基础在 Linux 中运行 Windows 游戏。请参见第 7 章了解 WineX 的说明。
- **Codeweavers** — 如果您需要 Microsoft Office 或 Web 浏览器插件，Codeweavers（www.codeweavers.com）分别提供 CrossOver Office 和 CrossOver Plug-in。虽然这些产品需要花费一些费用，但它们为安装和管理其支持的 Windows 软件和浏览器插件提供了友好的界面。

虽然确实可以使用 WINE 运行许多 Windows 应用程序，但要让许多 Windows 应用程序正常工作仍需要一些调试。如果您正考虑将桌面系统从 Windows 迁移到 Linux，WINE 的当前状态提供了一个机会，可以查看您需要的一些 Windows 应用程序是否可能在 Linux 中运行。

> **注意：** 我建议您在将任何想要在 WINE 中使用的应用程序部署到作为您工作关键部分的任何计算机之前，先对其进行测试。虽然我没有对我的计算机造成严重损坏，但在某些条件下 WINE 仍会冻结桌面。

除了开发软件，WINE 项目还维护一个在 WINE 下运行的应用程序数据库。列出了 1000 多个应用程序，尽管其中许多仅能部分运行。关键在于，应用程序列表正在增长，并特别关注使重要的 Windows 98 和 2000 应用程序能够运行。

虽然 VMware 和 Win4Lin 不是开源产品，但它们是在同一台正在运行的计算机上同时运行 Windows 应用程序和 Linux 系统的其他好方法。使用 VMware，您可以在同一台 PC 上同时运行 Windows 98、Windows NT、Windows 2000、Windows XP 和 Linux 操作系统。您可以从 www.vmware.com 获取有关 VMware 的更多信息。Win4Lin（www.netraverse.com）允许您在正在运行的 Linux 系统中运行 Windows 应用程序。

下一节介绍如何设置 Linux 以使用 WINE 运行 Windows 应用程序。

### 理解 WINE

为了让您运行 Windows 应用程序，WINE 需要建立一个看起来像 Windows 系统的环境。当您在 Red Hat Linux 中安装 wine 软件包时，该软件包会创建 /etc/wine/wine.conf 和 /etc/wine/system.reg 文件，类似于 Windows 注册表，标识应用程序在 Windows 操作系统中所需组件的位置。

WINE 的基本 Windows 操作系统目录的位置默认为 /usr/share/wine-c 目录（换句话说，即驱动器 C:）。表 5-5 显示了 C: 和其他 Windows 驱动器盘符如何映射到 Linux 目录和设备。

## 表 5-5：WINE 中的 Windows 驱动器盘符

| 说明 | 驱动器盘符或名称 | Linux 目录或输出位置 | Linux 设备名称（如适用） |
|---|---|---|---|
| 软盘驱动器 | A: | /mnt/floppy | /dev/fd0 |

