
终端窗口将出现在本地显示器上，标题栏中带有 Remotel 字样。

通常情况下，我在运行远程应用程序时使用 `-title` 选项。在标题中，我会尝试指示远程计算机名称。这样可以提醒我该应用程序并不是在本地运行的。

## 第二部分 + 使用 Red Hat Linux

你需要记住关于现在出现在显示器上的远程应用程序的一些事项：

- 如果你只使用登录来运行远程应用程序，可以将导出 `DISPLAY` 变量的内容添加到远程系统的用户文件中（如果你使用 `bash` shell，可以使用 `.bashrc`）。之后，你运行的任何应用程序都将重定向到本地显示器。
- 尽管应用程序看起来像是在本地运行，但所有工作都在远程系统上完成。例如，如果你远程远程运行文字处理程序，它将使用远程 CPU，当你保存文件时，它会被保存到远程文件系统中。

> 注意：当远程 shell 或文件编辑器位于桌面上时要小心。有时人们会忘记窗口是远程的，从而编辑了文件。

### 安全 X 应用程序

有几种方法可以防止 X 应用程序。每种方法提供不同的安全级别。支持的主要方法包括：

- `Hot Access` — 此前描述的方法让你决定哪些主机具有访问权限。使用 `xhost` 命令指定允许的 host (`+hostname`) 和不允许的 (`-hostname`)。这种方法在小型网络中效果最好。
- `Magic Cookie` — 这种方法称为 `MIT-COOKIE`，允许授权访问。远程客户端在访问之前必须提供有效的 cookie。

还有其他基于在 `.authority` 中存储随机生成的密钥的安全方法。`XDM-AUTH` 使用 `DES` (56位) 和一些随机数据 (64位) 来启用访问。当系统支持 `RPC` 时，`MIT-KERBEROS` 方法允许客户端和服务端相互验证（使用第三方）。

有关 Kerberos 的更多信息，请访问 Kerberos 主页：http://web.mit.edu/kerberos/www/index.html。关于 Linux 安全的通用信息，你可以参考 Hungry Minds（原 IDG Books）出版的 David A. Bandel 编写的 Linux Security Toolkit。

要创建加密传输信息的安全连接，请使用 `ssh` shell。你可以像之前的示例描述的那样，使用 `ssh` 登录远程系统。`ssh` 工具最近在 Red Hat Linux 中可用，因为美国政府更改了与加密技术相关的出口限制。有关 `ssh` 的更多信息，请访问 Secure Shell 社区 (http://www.ssh.org)。

### 使用模拟器运行其他操作系统的应用程序

Linux 准备好运行专为 Linux、X Window 系统和许多 UNIX 系统创建的应用程序。许多为其他操作系统创建的应用程序也已移植到 Linux。然而，仍然有成千上万为其他操作系统创建的应用程序没有 Linux 版本。

Linux 可以通过模拟器运行某些为其他操作系统设计的应用程序。模拟器正如其名，模拟器试图表现得像它本身不是的东西。在操作系统的情况下，模拟器试图提供一个在应用程序看来是目标操作系统的环境。在接下来的章节中，我将讨论允许你运行针对以下系统的应用程序的模拟器：

- DOS
- Windows 3.1
- Windows 95
- Windows 98
- Windows NT
- Macintosh

Red Hat Linux 提供了运行 DOS 程序的仿真程序。你需要安装 `dosemu` 和/或 `xdosemu` 包（这些包包含 Red Hat Linux PowerTools CD 中）。这些包提供的 DOS 仿真命令包括：`dos`、`xtermdos`、`dosebug`、`xdos` 和 `dosex`。还可以添加其他的操作系统仿真程序：

- `WINE`，它可以让你运行 Windows 3.1、Windows 95、Windows 98 和 Windows NT 二进制文件。（对 Windows NT 程序的支持并不良好。）
- `Bochs`，它是一个 PC 仿真软件软件包，通过仿真 x86 CPU 来运行 DOS、Windows 95、Minix 2.0 以及其他操作系统。
- `ARDI Emulator`，它允许你运行为 Macintosh 操作系统设计的应用程序。

通常情况下，程序越旧、复杂程度越低，在仿真器中运行的机会越高。基于字符的应用程序通常比基于图形的应用程序运行更好。此外，由于仿真器中可能会加入额外的调试代码，程序在仿真环境中的运行速度往往较慢。

#### 运行 DOS 应用程序

由于 Linux 最初是在 PC 上开发的，因此开发了多种工具来帮助开发者并弥合 Linux 与 DOS 节点之间的差距。一组名为 `mtools` 的 Linux 实用程序你在 Linux 中处理 DOS 文件和目录。一个名为 `dosemu` 的 DOS 仿真器让你能够在运行在 Linux 中的 DOS 环境中运行 DOS 应用程序（就像 DOS 窗口运行在 Windows 95/98/2000 中一样）。

#### 使用 mtools

`mtools` 大多数是在 DOS 命令前加上字母 "m" 的命令，并在 Linux 中运行（尽管有少数几个命名不同的例外）。使用这些命令，你可以轻松地处理 DOS 文件和文件系统。表 5-5 列出了 Linux 中可用的 `mtools`（如果你安装了 `mtools` 包）：

表 5-5
Linux 可用的 mtools

| 命令 | 功能 |
| --- | --- |
| `mattrib` | DOS `attrib` 命令，用于更改 MS-DOS 文件属性标志位。 |
| `mbadblocks` | DOS `badblocks` 命令，用于测试软磁盘并将软磁盘包含的任何坏块标记在 FAT 中。 |
| `mcd` | DOS `cd` 命令，用于更改其他 mtools 使用的工作目录。 |
| `mcheck` | DOS `check` 命令，用于验证文件。 |
| `mcopy` | DOS `copy` 命令，用于将文件从一个位置复制到另一个位置。 |
| `mdel` | DOS `del` 命令，用于删除文件。 |
| `mdeltree` | DOS `deltree` 命令，用于删除 MS-DOS 目录及其包含的文件和子目录。 |
| `mdir` | DOS `dir` 命令，用于列出目录内容。 |
| `mdu` | Linux `du` 命令，用于显示 DOS 目录占用的磁盘空间。 |
| `mformat` | DOS `format` 命令，用于格式化 DOS 软磁盘。 |
| `minfo` | 该命令用于打印关于软磁盘的 DOS 设备的信息。 |
| `mkmanifest` | 该命令用于创建一个 shell 脚本，恢复被 DOS 命令截断的 Linux 文件名。 |
| `mlflow` | DOS `label` 命令，用于创建 DOS 卷标签。 |
| `mmd` | DOS `md` 命令，用于创建 DOS 目录。 |
| `mmount` | 该命令用于在 Linux 中挂载 DOS 磁盘。 |
| `mmove` | DOS `move` 命令，用于将文件移动到另一个目录并/或重命名。 |
| `mrd` | DOS `rd` 命令，用于删除 DOS 目录。 |
| `mread` | DOS `copy` 命令，用于将 DOS 文件从一个位置复制到另一个位置。 |
| `mren` | DOS `ren` 命令，用于重命名文件。 |
| `mshowfat` | 该命令用于显示 DOS 文件系统的 FAT 条目。 |
| `mtoolstest` | 该命令用于测试 mtools 配置文件。 |
| `mtype` | DOS `type` 命令，用于显示 DOS 文本文件的内容。 |
| `mzip` | 该命令用于对 Zip 磁盘执行操作，包括弹出、写保护和查询。 |

我通常使用 `mtools` 在我的 Linux 系统和未连接到网络的 Windows 95/98 系统之间复制文件。我经常使用 `mcopy`，它允许我使用驱动器代替设备名称来复制文件。换句话说，要从软磁盘器 A: 将文件 `vi.exe`复制到 Linux 的当前目录，我会输入：

```
mcopy a:\vi.exe
```
