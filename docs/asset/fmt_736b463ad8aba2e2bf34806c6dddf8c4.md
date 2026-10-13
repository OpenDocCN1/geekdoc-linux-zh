
要获取最新版本的 DOSEMU，请访问 http://www.dosemu.org。您将找到指向最新文档和更新内容的链接。有关 FreeDOS 的更新，请访问 http://www.freedos.org。您还可以找到数百种可以添加到您的 DOSEMU 系统中的实用工具、命令和额外软件包。

## 使用 Wine 运行 Windows 客户端

由为 Wine 项目做出贡献的程序员支持的 Wine 模拟器允许您运行许多 DOS、Windows 3.1 或 Win32 程序。此模拟器可以从 http://www.winehq.com 下载，提供二进制文件或源代码归档。

> **注意**
>
> Corel 公司，即 1998 年为 Linux 提供了免费仅供个人使用的 WordPerfect 9 版本的友好公司，在 1999 年 3 月的 Linuxworld 会议上宣布，他们将为其 WordPerfect Office 2000、CorelDRAW 和 Corel PHOTO PAINT 提供 Linux 版本。一年后，Corel 发布了适用于 Linux 的 WordPerfect Office 2000 Deluxe 套件。该套件由 WordPerfect 9、Quattro Pro 9、Paradox 9 和 Corel Presentations 9 组成（连同字体、剪贴画、Corel Linux 副本和一个商业游戏），严重依赖 Wine 项目的软件库。Corel PHOTO-PAINT、适用于 Linux 的 WordPerfect 8 和最新版本的 Corel Linux 也可以免费在 http://linux.corel.com/download/ 下载。作为这一努力的一部分，Corel 还承诺积极支持和开发 Wine，“以加速将我们的办公软件应用程序移植到 Linux 的过程”。Corel 还表示，对 Wine 的开发工作结果将返回给 Wine 项目。

安装 Wine 的最简单方法是下载预构建的 `.rpm` 文件（例如来自 Red Hat PowerTools CD-ROM），然后使用此代码安装程序：

```
# rpm -ivh wine-20000725-1.1386.rpm
```

安装后，以 root 身份编辑 `/etc/wine` 目录下的 `wine.conf` 文件，告知 wine 您的 Windows 目录的位置以及软盘驱动器和 CD-ROM 的设置。首先查找软盘驱动器条目：

```
[Drive A]
Path=/mnt/fd0
...
Device=/dev/fd0
```

如果您的软盘挂载在 `/mnt/floppy` 目录下，您应该将 `Path=` 条目更改以反映这一点：

```
Path=/mnt/floppy
```

接下来，查找 Drive C 的条目：

```
[Drive C]
Path=/c
```

更改驱动器条目以反映指向您的 Windows 文件系统的路径。在 Red Hat Linux 中，相当于 Windows C: 驱动器的对应条目（在系统文件系统表 `/etc/fstab` 中）很可能指向 `/mnt/dos`。如果是这样，请将 `wine.conf` 条目更改为：

```
[Drive C]
Path=/mnt/dos
```

继续浏览 `wine.conf` 文件，编辑条目以匹配您的系统的文件系统、设备和挂载点。另一个重要的条目将指向您的系统的 CD-ROM 驱动器：

```
[Drive D]
Path=/cdrom
...
Device=/dev/cdrom
```

在此示例中，您的计算机的 CD-ROM 驱动器被分配为 D 盘。您可能需要更改此条目以反映正确的挂载点和设备，如下所示：

```
[Drive D]
Path=/mnt/cdrom
...
Device=/dev/hdc
```

### 没有 Windows 的 Wine？

早期版本的 Wine 需要在系统上安装 Windows 副本。然而，Wine 的开发已经进展到 Wine 可能能够在没有安装副本的情况下运行。但是，您需要创建以下空目录：

```
C:\windows
C:\windows\system
C:\windows\Start Menu
C:\windows\Start Menu\Programs
```

有关使用 Windows 设置 Wine 的更多详细信息，请参见 `/usr/doc/wine*/documentation` 目录下的 `no-windows` 文件。您还将找到有关让棘手的程序运行的额外提示。

如果您已挂载 Windows 分区，则可以通过输入以下内容尝试运行 Windows WordPad 客户端：

```
# wine /mnt/dos/Prog*/Accessories/wordpad.exe
```

编辑器窗口出现，如图 28.2 所示。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_942_0.png)

如果你想了解更多有关 Wine 的信息，或其他用户或开发者的技巧与提示，请阅读 Usenet 新闻组 `comp.emulators.ms-windows.wine`。如果在 http://www.deja.com 进行搜索，你还将找到近 30 个专注于模拟器讨论的新闻组。

## 使用 Executor 模拟 Apple Macintosh

Executor 是由 ARDI 开发的商业软件模拟器，可用于在 Linux 下运行 MacOS 应用程序。据 ARDI 称，在 90MHz Pentium 处理器上运行 Executor，其速度几乎与 50 MHz 68040 处理器相当，可以运行大多数应用程序。Executor 软件以一系列 `.rpm` 归档文件分发，演示版可通过 http://www.ardi.com 获取。

该软件或许能帮你运行近 340 个遗留的 Macintosh 应用程序之一，但对 Apple Macintosh 的软件模拟并不完美，存在一些限制。默认模拟的 MacOS 版本为 System 6.0.7，尽管某些 System 7.0 应用程序可能可以运行。但更重要的是，其他排除项包括：

- 对串行端口的访问
- AppleTalk（LocalTalk）
- CVEs
- INITs
- 国际化
- 调制解调器使用

该软件对声音的支持有限，并且可以读写 1.44MB 的 Macintosh 格式软盘。据 ARDI 称：“Desk Accessory 支持非常薄弱，大多数无法运行。”另一方面，你会发现对一些主要 Macintosh 客户端有很好的支持，如表 28.1 所列。

**表 28.1 支持 Executor 的 Macintosh 客户端**

| 名称 | 支持的版本 |
| :--- | :--- |
| Adobe Dimensions | 2.0 |
| Adobe Illustrator | 1.9.5, 5.5 |
| Adobe Photoshop | 4.0 |
| Aldus Freehand | 2.2 |
| Aldus Persuasion | 2.1, 3.0 |
| Claris Draw | 1.0v1 |
| Claris Works | 2.01, 2.1, 3.0 |
| File Maker Pro | 2.0, 2.1, 3.0, 4.0 |
| HyperCard | 2.1, 2.2, 2.3 |
| Microsoft Excel | 3.0a, 4.0 |
| Microsoft Word | 5.1 |
| Microsoft Works | 2.00a |
| QuarkXPress | 3.32 |
| Quicken | 4.0, 5.0, 6.0 |
| WordPerfect | 3.1 |
| WriteNow | 4.0 |

### 安装 Executor

使用 `rpm` 命令（以 root 身份）安装该软件。安装完成后，主可执行文件位于 `/opt/executor/bin` 目录下，但会在 `/usr/local/bin` 目录下创建符号链接。尽管包含 SVGA 版本，但在 X11 会话中运行 `executor` 命令是最简单的方法。启动 X，然后在终端的命令提示符下输入以下内容以启动程序：

```
# executor &
```

会出现启动画面，随后主窗口将出现，如图 28.3 所示。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_944_0.png)

模拟窗口的默认屏幕尺寸为 640×480，但你可以通过使用 Executor 的命令行开关之一来更改，如表 28.2 所示。

**表 28.2 Executor 命令行开关**

| 选项 | 操作 |
| :--- | :--- |
| appizone n[k] | 为应用程序使用 n 千字节内存 |
| appizone n[MB] | 为应用程序使用 n 兆字节内存 |
| bpp n | 使用每像素 n 位（1 或 8） |
| desparate | 极简模式（仅适用于 DOS） |
