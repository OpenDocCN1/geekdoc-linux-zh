
对于这项工作，你不需要打开本地显示器（使用 `xhost`）。这之所以有效是因为远程系统上的 SSH 守护进程 (`sshd`) 为你的计算机建立了一个用于 X 应用程序的安全通道。为了不干扰任何真实的显示器编号，SSH 守护进程（默认）使用 `localhost:10.0` 作为显示名称。

此转发功能在最新版本的 Fedora 中是默认开启的（查看 `/etc/ssh/sshd_config` 文件中的 `X11Forwarding yes` 值）。但在其他系统中它是关闭的，因此你可能需要更改其他系统上的 `X11Forwarding` 值。

## 运行 Microsoft Windows、DOS 和 Macintosh 应用程序

Linux 准备好运行大多数专为 Linux、X Window 系统和许多 UNIX 系统创建的应用程序。许多最初为其他操作系统创建的应用程序也被移植到了 Linux 上。然而，仍然有许多为其他操作系统创建的应用程序没有 Linux 版本。

Linux 可以使用模拟器程序运行针对其他操作系统的应用程序。正如其名所示，模拟器试图表现得像它本身不是的东西。在操作系统体系的情况下，模拟器试图呈现一个看起来像目标操作系统的环境。

> 注意：在这些模拟器中最流行的是名为 `WINE`，它实际上不是一个模拟器。`WINE` 是一种实现 Windows 应用程序编程接口的机制，而不是模拟 Microsoft Windows，它提供了 Windows 应用程序所预期的接口。事实上，有些人声称 `WINE` 的意思是 "WINE is Not an Emulator（WINE 不是一个模拟器）"。

在接下来的章节中，我将讨论你可以运行针对以下操作系统应用程序的模拟器：

- Microsoft Windows 3.1
- Microsoft Windows 95
- Microsoft Windows 98
- Microsoft Windows 2000
- Microsoft Windows ME
- Microsoft Windows NT
- Microsoft Windows XP
- Macintosh (Mac OS)

对于 Mac OS X 应用程序，由于该操作系统基于一个名为 Darwin 的类 Unix 操作系统，许多为 Mac OS X 编写的开源应用程序都有可在 Linux 下运行的版本。如果你在 Mac OS X 中发现了一个你喜欢的应用程序并想在 Linux 中运行，请检查 `Sourceforge.net` 网站，查看创建该 Mac OS X 应用程序的项目是否也提供了 Linux 版本（或至少提供了供你尝试自行构建该应用程序的源码）。

> 注意：在理论上，任何兼容 Win32 的应用程序都应该可以使用如 `WINE`（后文将描述）之类的软件运行。Microsoft Windows 应用程序是否会在 Linux 模拟器中运行，必须根据具体情况进行检查。

可用的模拟程序包括：

- `DOSBOX`，用于运行在现代计算机上无法运行的经典 DOS 应用程序。（以 root 身份通过 Fedora `yum install dosbox` 安装它）
- `WINE`，它可以让你运行 Windows 3.1、Windows 95、Windows 98、Windows 2000、Windows NT 和 XP 的二进制文件。Windows NT 和 XP 程序的支持并不好。然而，由于许多 Windows 应用程序设计为在早期的 Windows 系统中运行（这限制了它们仅使用几个 XP 特有的调用？），它们在 `WINE` 中也能良好运行。检查该 Windows 应用程序的文档。如果它只需要 Windows 95 或 Windows 98，它通常可以在 `WINE` 中运行。
- `ARJI` 让你运行针对 Macintosh 操作系统（MAC OS）的应用程序。

通常情况下，程序越旧越不复杂，在模拟器中运行的机会越高。基于字符的应用程序通常比基于图形的应用程序运行得。此外，程序在模拟中运行速度往往较慢，有时是因为模拟器中加入了额外的调试代码。然而，由于 `WINE` “不是模拟器”，任何不进行系统调用的应用程序在 `WINE` 中的运行速度都应该像在 Windows 中原生运行一样快。

在 Linux 上运行其他操作系统应用程序的另一种方法是使用虚拟化产品。一个流行的虚拟产品是 `VMware Player` (`www.vmware.com/products/player`)。然而，Fedora 本身包含了 Xen 虚拟化软件。另一种虚拟化方法 `KVM` 被添加到 Fedora 7 中。（Xen 和 KVM 都将在本章稍后介绍。）

## 运行 DOS 应用程序

由于 DOS 最初在 PC 上开发，因此开发了各种工具来帮助开发者并桥接 Linux 和 DOS 系统之间的差距。一组名为 `mtools` 的 Linux 实用程序允许你在 Linux 内处理 DOS 文件和目录。DOS 模拟器 `DOSbox` 让你能够在在 Linux 中的 DOS 环境中运行 DOS 应用程序（就像 DOS 窗口在 Microsoft Windows 操作系统中运行一样）。

## 使用 mtools

`mtools` 大多数是在前面带有字母 `m` 的、且在 Linux 中运行的 DOS 命令（尽管有少数命名不同的例外）。使用这些命令，你可以轻松地处理 DOS 文件和文件系统。列出 Linux 中可用的 5-4 个 `mtools`。

### 表 5-4：Linux 中可用的 mtools

| 命令 | 功能 |
| --- | --- |
| `mattrib` | DOS `attrib` 命令，用于更改 MSDOS 文件属性标记。 |
| `mbblocks` | DOS `badblocks` 命令，测试软磁盘并标记其中包含的任何坏块。 |
| `mcd` | DOS `cd` 命令，用于切换到任何 DOS 目录。（默认目录是 `A:\`，供 `mtools` 使用。） |
| `mcheck` | DOS `check` 命令，用于验证文件。 |
| `mcopy` | DOS `copy` 命令，用于从一个位置复制文件到另一个位置。 |
| `mdel` | DOS `del` 命令，用于删除文件。 |
| `mdeltree` | DOS `deletetree` 命令，删除目录及其包含的文件和子目录。 |
| `mdir` | DOS `dir` 命令，列出目录内容。 |
| `mdu` | Linux `du` 命令，用于显示目录占用的磁盘空间。 |
| `mformat` | DOS `format` 命令，用于格式化 DOS 软磁盘。 |
| `minfo` | 该命令用于打印有关 DOS 设备（如软磁盘）的信息。 |
| `mkmanifest` | 该命令用于创建一个恢复被 DOS 命令截断的 Linux 文件名的 脚本。 |
| `mlabel` | DOS `label` 命令，用于创建 DOS 卷标。 |
| `mmount` | 该命令用于在 Linux 中挂载 DOS Disk。 |
| `mm` | DOS `move` 命令，用于将文件移动到另一个目录并或重命名。 |
| `mrd` | DOS `rd` 命令，用于删除 DOS 目录。 |
| `mren` | DOS `ren` 命令，用于重命名 DOS 文件。 |
| `mshowfat` | 该命令用于显示 DOS 文件系统中文件的 FAT 条目。 |

| 命令 | 功能 |
|---|---|
| `mtoolstest` | 该命令用于测试 `mtools` 配置文件。 |
| `mtype` | DOS `类型` 命令，用于显示 DOS 文本文件的内容。 |
| `mzip` | 该命令用于对 Zip 磁盘进行操作，包括弹出、写保护和查询。 |

我经常使用 `mtools` 从我的 Linux 系统和未连接到网络的 Windows 系统之间复制文件。我经常使用 `mcopy`，它允许我使用驱动器号而不是设备名称来复制文件。换句话说，要从软磁盘 `A:` 将文件 `vi.exe` 复制到 Linux 的当前目录，我将输入：

```
# mcopy a:\vi.exe
```

> 注意：默认情况下，软磁盘驱动器可以被 root 用户和 `floppy` 组（floppy group）读写。要让所有人都能访问软驱（假设是软驱 `A:`），请以 root 用户身份输入命令：`chmod 666 /dev/fd0`。

# 第 5 章：访问与运行应用程序 231

## 使用 DosBox

为了运行你的经典 DOS 应用程序，Fedora 包含了 `dosbox` 软件包。要安装 `dosbox`，请以 root 用户身份输入以下：

```
# yum install dosbox
```

安装好 `DosBox` 后，只需输入 `dosbox` 即可在桌面上打开一个 `DosBox` 窗口。通过该窗口，你将拥有一个可以运行许多经典 DOS 应用程序的环境。假设你已经将某些想要运行的 DOS 应用程序存储在 Fedora 系统上，你可以通过挂载包含这些程序的目录来使这些应用程序可用。例如，要将 `/home/chris` 目录挂载到 `DosBox` 中的 `C` 盘，请输入：

```
Z:\> mount c /home/chris
```
