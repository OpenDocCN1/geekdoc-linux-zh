
# 图 13.1 至 13.4：xman 窗口操作

这将显示类似于图 13.1 的初始 `xman` 窗口。

**13.1: the initial xman window** (`img/96f44a58bee05a0863d1e0.png`)。从这里，你可以按 `Manual Page` 按钮显示图 13.2 所示的主 `xman` 窗口。

**13.2: The main xman window**

| Options | Sections | Help |
| :--- | :--- | :--- |
| XMAN 是一个 X Window 系统手册浏览工具。 | | |
| GETTING STARTED | | |

默认情况下，`xman` 会创建一个包含三个“按钮”的小窗口。这些按钮中的 `Help` 和 `Quit` 是自而易见的。第三个 `Manual Page` 在 `xman` 运行时都会创建一个新页面。手册页显示此信息。在右上角有两个菜单。当你点击这些章节中的任何一个时，会弹出一个菜单。这些菜单的内容在下文中描述。

通常显示正在显示的手册名称。

1. `User Commands`
2. `System Calls`
3. `Subroutines`
4. `File Formats`
5. `Games`
6. `Miscellaneous`
7. `Sys Administration`
8. `New`

如你所见，`man pages` 被分为八大类，包括 `User Commands`、`System Calls` 等。选择其中任何一个章节将列出类似图 13.5 所示的目录列表。

**13.5: A directory listing**

| Options | Sections | |
| :--- | :--- | :--- |
| `Manual Page` | `Xman Help` | |
| `ImageMagick` | `Magick--config` | `Magick--config` |
| `SuperProbe(n)` | `Win32` | `XF6_SVGA(n)` |
| `XConfiguration(n)` | `Xview(n)` | `afmlodit` |
| `addtrinfo` | `animale` | `asend` |
| `anypress` | `apacheconf` | `ann` |
| `alias` | `ash` | `asp` |
| `ascriptbg` | `altton(n)` | `arch` |
| `atktopm` | `audiocompose` | `atq` |
| `autotect` | `autorun` | |
| `balsa` | `basename` | `autobox` |
| `baub` | `bioradoptgm` | `bash` |
| `bind` | `bmtoa(n)` | `bitmap(n)` |
| `bnptopm` | `brushtpm(n)` | `bouuble` |
| `break` | `burnit` | `burniz` |
| `bustle` | `bczat` | `bizp2` |
| `burst` | `cs` | `cal` |
| `zip2recover` | `card` | `case` |
| `Captionb(m)` | `cda2wav` | `cdp` |
| `cat` | `cdge` | `charset` |
| `cdparanoia` | `ctm` | `chrshp` |
| `chage` | `chrool(n)` | `cksum` |
| `chmod` | `ciphers` | `cpeg` | `col` |
| `chvt` | `cmwumbbpm` | `column` |
| `clear` | `colm` | `combine` |
| `colrt` | `comp` | `consolety` |
| `comm` | `cp` | `cpio` |
| `continua` | `cr12acx7` | `crutab` |
| `critical` | `cut` | `date` |
| `csplit` | `cxpm(n)` | `deallocvt` |
| `dbmanager` | `dd` | |

**13.4: The Sections menu**

| Options | Display Directory | Display Manual Page | Help | Search | Show Both Screens | Remove | Open New Manage | Show Version | Quit |

窗口的主区域用于显示当前选定 `man page` 的文本。初始显示 `man` 的帮助文件。窗口有两个菜单：`Options` 和 `Sections`。图 13.3 所示的 `Options` 菜单允许你在 `man pages` 列表（`Display Directory`）和当前 `man page` 的内容（`Display Manual Page`）之间切换，还可以搜索页面内容。`Help` 选项显示 `man` 的完整帮助文件，提供了有关使用 `man` 的详细说明。如果你想查看特定的 `man page`，选择 `Search` 选项，然后在出现的文本框中输入命令名称。

# 第十四章

## 文件操作

- 复制和删除文件
- 移动和重命名文件
- 创建文件
- 创建符号链接
- 文件名扩展简述

在第 14 章“文件操作”中，你将学习 Linux 提供的用于处理文件和目录的强大命令。你将在本章讨论的命令（如 `ls`）的基础上，探索创建目录和其他高级任务。

### 复制和删除文件

在上一章中，你已经略了解了使用 Linux 所涉及的内容。你看到所有命令实际上都是存储在不同文件中的独立程序。你甚至开始通过观察使用 `ls` 命令显示文件列表的各种方式，来学习如何操作文件。

在本章中，你将详细查看用于进一步操作文件和目录的命令，包括复制、删除、移动、重命名和创建。本章将通过快速回顾文件名扩展来结束——即像在 DOS 和 Windows 中常用的常用的星号之类的通配符。

可能最常见的两种文件操作任务是复制文件和移动文件。你会经常发现自己需要在磁盘驱动器上复制文件，或者将文件复制到软磁盘中（后者是为了备份，或者使用最廉价的网络方法：你的脚来“传输”文件）。同样，普通 PC 用户在某个时刻会遇到磁盘空间不足的问题，并寻找要删除的文件以释放宝贵的磁盘空间，从而避免购买新硬盘。

#### 复制文件

任何简要使用过 DOS 或任何版本 Windows 中的 DOS 提示符的人可能都意识到，点击、拖动和释放并不是复制文件的唯一方法。事实上，DOS 的 `copy` 命令提供了额外的功能（例如通配符），这使得它比文件管理器或 Windows 资源管理器更快速、更简单、更强大。

同样，在 Linux 世界中，`cp` 命令（通常位于 `/bin/cp`）用于复制，并为复制操作提供了强大的工具。

##### 基础复制

显然，`cp` 命令最基础的用法是将文件从一个地方复制到另一个地方，以及在同一目录下创建副本文件。例如，

你想将当前目录下的文件（`ThisFile`）复制到同一目录下的第二个文件（命名为 `ThisFile-Acopy`），请输入以下命令：

```
$ cp ThisFile ThisFile-Acopy
```

使用 `ls -l` 查看目录下的文件列表，你会发现两个大小相同但日期不同的文件。新文件有一个指示复制操作发生时间的时间戳。它是一个新的、独立的文件。对 `ThisFile-Acopy` 的更改不会影响原始的 `ThisFile`。

同样，要在 `/tmp` 目录中创建 `ThisFile` 的副本（也许为了与其他用户共享该文件），请使用以下命令：

```
$ cp ThisFile /tmp
```

如果你想将 `ThisFile` 复制到 `/tmp` 但给新文件起一个不同的名字，请输入：

```
$ cp ThisFile /tmp/NewFileName
```

#### 不要覆盖该文件

Linux 发行版中可怕的一点是，很容易通过覆盖现有文件来意外覆盖文件。考虑 `ThisFile` 和 `NewFile` 都存在且你执行以下命令的情况：

```
$ cp ThisFile NewFile
```

使用此命令后，`NewFile` 的内容将被 `ThisFile` 的副本覆盖并永久丢失（除非你有自律地备份系统的良好习惯）。

为了避免这种困难，请使用 `cp` 命令的 `-i` 标志，它会强制系统在复制时确认它将覆盖的任何文件。然后，当你尝试复制时，你会看到这样的提示：

```
$ cp -i ThisFile NewFile

cp: overwrite 'ThisFile'?
```

如果你想防止这种情况，可以为 `cp` 命令创建一个别名。通过执行命令：

```
$ alias cp='cp -i'
```
