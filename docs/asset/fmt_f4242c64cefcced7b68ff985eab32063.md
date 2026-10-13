
进入 `/path/to/xxx` 目录，找到 `xxx.json`。

在表达式 `cvar = avar + bvar` 中，加法运算符（`+`）将 `avar` 与 `bvar` 相加，得到它们的和 `cvar`

在 `List.of(arg0, arg1, arg2)` 中，`List` 接口的工厂方法 `of()` 接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用 `cmd` 命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

# 6. 此时，你从远程系统运行的任何 X 应用程序将出现在本地显示器上

例如，要运行远程终端窗口使其显示在本地，请输入：

```
$ xterm
```

终端窗口出现在本地显示器上。

你需要记住一些关于出现在你显示器上的远程应用程序的注意事项：

- 如果你只使用登录来运行远程应用程序，可以将导出 `DISPLAY` 变量的行添加到远程系统的用户配置文件（例如，如果你使用 `bash` shell，则使用 `.bashrc`）。之后，你运行的任何应用程序都将重定向到你的本地显示器。
- 尽管应用程序看起来像是在本地运行，但所有工作都是在远程系统上完成的。例如，如果你远程运行一个文字处理程序，它将使用远程 CPU，当你保存文件时，它会被保存到远程文件系统中。

注意：不要忘记你的桌面上打开了远程 shell 或文件编辑器。有时人们会忘记某个窗口是远程的，并会误操作编辑远程系统上的某些重要配置文件（例如 `/etc/fstab` 文件）。你可能会因此这种错误损坏远程系统。

# 使用 SSH 运行远程 X 应用程序

`ssh` 命令不仅为登录远程系统提供了安全机制，还提供了一种安全运行远程 X 应用程序的方法。在开启 X11 转发的情况下，你通过 `ssh` 会话从远程位置运行的任何 X 应用程序都将出现在你的本地桌面上。

使用 `ssh` 登录到远程计算机后，你可以使用该安全通道将 X 应用程序转发回你的本地显示器。以下是一个示例：

## 第二部分：使用 Fedora RHEL

### 1. 输入以下 `ssh` 命令登录到远程计算机（`-X` 选项启用 X11 转发）：

```
$ ssh -X jake@remotel
jake@remotel's password: ***********
```

### 2. 检查显示变量是否已设置，以便通过此 `ssh` 会话运行的任何 X 应用程序转发到你的本地显示器：

```
$ echo $DISPLAY
localhost:10.0
```

### 3. 登录后，输入与该命令相关的任何 X 命令，它将出现在本地显示器上。例如，要启动 `edit` 命令，输入：

```
$ edit &
```

对于这项工作，你不需要打开本地显示器（使用 `xhost`）。这之所以有效是因为 SSH 守护进程 (`sshd`) 为 X 应用程序建立了通到你远程系统的安全通道。为了不干扰任何实际显示，名称为 `localhost:10.0`。此转发功能在 Fedora Core 中默认关闭的，除非你在 `/etc/ssh/sshd_config` 文件中添加 `ForwardX11` 行。

# 运行 Windows、DOS 和 Macintosh 应用程序

Linux 可以运行为 X 窗口系统、许多 UNIX 系统设计的应用程序。许多最初为其他操作系统创建的应用程序已移植到 Linux。然而，仍然为其他系统的应用程序还没有 Linux 版本。

> 注意：这些模拟器中，流行的被称为 `WINE` 的并不是模拟器。`WINE` 是一种实现 Windows 应用程序接口的机制，而不是模拟 Windows，它提供了 Windows 应用程序期望的接口。事实上，有些人声称 `WINE` 的意思是“`WINE` 不是模拟器”。

在接下来的章节中，我将讨论用于以下操作系统的应用程序的模拟器：

- Windows 3.1
- Windows 95
- Windows 98
- Windows 2000
- Windows ME
- Windows NT
- Windows XP
- Macintosh (Mac OS)

至于 Mac OSX 应用程序，由于该操作系统基于名为 Darwin 的类 Unix 系统，许多为 Mac OSX 编写的开源应用程序会有 Linux 版本。如果你在 Mac OSX 上发现了喜欢的应用程序并想在 Linux 上运行，请检查 `Sourceforge.net` 站点，查看该 Mac OS X 项目是否提供了 Linux 版本（或至少提供构建应用程序所需的源码）。

可用的模拟程序包括：

- `DOSEMU`，用于运行 DOS 程序。（`DOSEMU` 从 `http://dosemu.sourceforge.net` 获取）。
- `WINE`，让你运行 Windows 3.1、Windows 95、Windows 98、Windows 2000、Windows NT；Windows XP 二进制的支持并不良好。然而，由于许多 Windows 应用程序是为早期 Windows 系统编写的（这限制了它们使用某些特定的 XP 调用）。
- `ARDI Executor`，允许你运行针对 Macintosh 操作系统（MAC OS）设计的应用程序。

通常情况下，程序越旧、越简单，在模拟器中运行的机会越大。基于字符的应用程序通常比图形应用程序运行得更好。此外，程序在模拟中运行速度通常较慢，有时是因为额外的调试代码。

放入模拟器中。然而，由于 `WINE` “并不是模拟器”，任何不产生系统调用的应用程序在 `WINE` 中的运行速度都不会像在 Windows 原生环境下快。

## 运行 DOS 应用程序

由于 Linux 最初是在 PC 上开发的，因此开发了多种工具帮助用户并弥合 Linux 与 DOS 系统之间的差距。一组名为 `mtools` 的 Linux 实用程序允许你在 Linux 内部处理 DOS 文件和目录。一个名为 `dosemu` 的 DOS 模拟器允许你能够在实际上运行在 Linux 中的 DOS 环境中运行 DOS 应用程序（就像 DOS 窗口在 Microsoft Windows 操作系统中运行一样）。

> 注意：你可以从 `dosemu.sourceforge.net/stable` 获取 `dosemu` 的 RPM 包。

## 使用 mtools

`mtools` 大多数是在前面带有字母 `m` 的 DOS 命令，并且它们在 Linux 中运行（尽管有少数几个命名不同的例外）。使用这些命令，你可以轻松地处理 DOS 文件和文件系统。表 5-4 列出了 Linux 中可用的 `mtools`（前提是你安装了 `mt` 软件包）。

### 表 5-4：Linux 可用的 mtools

| 命令 | 功能 |
| :--- | :--- |
| `mattrib` | `attr` 命令，用于更改 MS-DOS 文件属性标记。 |
| `mbadblocks` | `badblocks` 命令，用于测试软盘并在其 FAT 中标记软盘包含的任何坏块。 |
| `mcd` | `cd` 命令，用于将工作目录更改到另一个 DOS 目录。（默认目录为 A:\），其他 `mtools` 会使用该目录。 |
| `mcheck` | `check` 命令，用于验证文件。 |
| `mcopy` | `copy` 命令，用于将文件从一个位置复制到另一个位置。 |
| `mdel` | `del` 命令，用于删除文件。 |
| `mdeltree` | `deltree` 命令，用于删除 MS-DOS 目录及其包含的所有文件和子目录。 |
| `mdir` | `dir` 命令，用于列出目录内容。 |
| `mdu` | `du` 命令，用于显示 DOS 目录占用的磁盘空间。 |
| `mformat` | `format` 命令，用于格式化 DOS 软盘。 |
| `minfo` | 此命令用于打印有关 DOS 设备（如软盘）的信息。 |
| `mkmanifest` | 此命令用于创建一个 shell 脚本，以恢复被 DOS 命令截断的 Linux 文件名。 |
| `mlabel` | DOS 标签命令，用于创建 DOS 卷标。 |
| `mmd` | DOS `md` 命令，用于创建 DOS 目录。 |
| `move` | DOS `move` 命令，用于将文件移动到另一个目录并/或对其重命名。 |
| `mrd` | DOS `rd` 命令，用于删除 DOS 目录。 |
| `mren` | DOS `ren` 命令，用于重命名 DOS 文件。 |
| `mshowfat` | 此命令用于显示 DOS 文件系统中文件的 FAT 条目。 |
| `mtoolstest` | 此命令用于测试 `mtools` 配置文件。 |
| `mtype` | DOS `type` 命令，用于显示 DOS 文本文件的内容。 |
| `mzip` | 此命令用于对 Zip 磁盘进行操作，包括弹出、写保护和查询。 |

我使用 `mtools` 在我的 Linux 系统和不在网络中的 Windows 系统之间复制文件。我经常使用 `mcopy`，它允许我使用驱动器器而不是设备名称来复制文件。换句话说，要把软盘驱动器 A: 中的文件 `vi.exe` 复制到 Linux 的当前目录，我会输入：

```bash
# mcopy a:\vi.exe
```

> 注意：默认情况下，软盘驱动器可以被 root 用户和 floppy 组读写。要让所有人都能访问软盘驱动器（假设是 A 盘），请以 root 用户身份输入命令：`chmod 666 /dev/fd0`。

## 使用 dosemu

`dosemu` 模拟器包未包含 Fedora Core 发行版中。要使用 `dosemu`，请从 `dosemu.sourceforge.net` 下载 `dosemu` RPM 文件。
