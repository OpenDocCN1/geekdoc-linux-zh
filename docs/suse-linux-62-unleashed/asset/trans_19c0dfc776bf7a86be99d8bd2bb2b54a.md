
# 模拟器
第 29 章

要为软磁盘标记，你可以使用 `mlabel` 命令：

```
# mlabel a:
卷没有标签
输入新的卷标签：LINUX
```

你也可以使用特殊的 shell 命令行引号从命令行为软磁盘标记，如下所示：

```bash
# mlabel a:'08 DISK'
```

这是一种在软磁盘标签中使用空格的方便方法。如果你想删除软磁盘上的文件，请使用 `mdel` 命令：

```bash
# mdel a*.txt
```

这会删除 a: 驱动器上所有以 .txt 结尾的文件。你还可以挂载你的软磁盘。详情，请参阅 `mmount` 手册页以及 `mount` 命令页。

# 窗口客户端

虽然软件和硬件模拟器可以简化许多计算任务，但对系统资源（如内存或存储）的需求可能是巨大的。如果你有额外的计算机或在网络化环境中工作，一种简单的方法是使用 X 窗口系统和网络协议与其他系统通信并运行其他客户端。

得益于 AT&T 剑桥实验室，Linux 用户现在可以通过虚拟网络计算相对轻松地在外国操作系统的桌面上工作。更好的消息是，该名为 `vnc` 的软件在 GNU 公共许可证下提供 Linux 源码，并可以在 SuSE Linux 下编译和安装。

vnc Linux 软件由几个主要组件组成：一个名为 `xvnc` 的 X 服务器、一个名为 `vncserver` 的服务器、一个名为 `vncpasswd` 的密码工具以及一个名为 `viewer` 的通信查看器。vnc 软件适用于其他计算机和操作系统，包括但不限于：

- DEC Alpha OSF1 3.2
- Macintosh OS
- Solaris
- Win32
- Windows CE 2

![](img/cbac72550c7126a22162e94d91a0c360_958_0.png)

# 图形、多媒体和生产力工具
第四部分

软件可以在 http://www.uk.research.att.com/vnc 获取。提供适用于 Linux 的二进制文件压缩包，或者你可以下载 2.1MB 的 UNIX 源码 tar 包。

# 编译和安装 vnc 软件

如果你下载了二进制文件，使用 `tar` 命令如下解压文件：

```bash
# tar xvzf vnc3.3_x86_linux_2.0.tgz
```

这将创建一个 `vnc` 目录。读取目录中包含的 readme 文件，或者将文件 `Xnc`、`vncserver`、`vncviewer` 和 `vncpasswd` 复制到相应的目录。

如果你下载了 vnc 源码，使用 `tar` 命令如下解压存档：

```bash
# tar xvzf vnc3.3_unixsrc.gz
```

这将创建一个 `vnc_unixsrc` 目录。进入该目录并使用 `xmkmf` 命令启动编译：

```bash
# xmkmf
# make World
```

进入 `Xnc` 目录并如下编译 vnc x 服务器：

```bash
# cd Xnc
# make World
```

最后，以 root 身份通过目标脚本安装 vnc 软件，指定安装目录：

```bash
./vncinstall /usr/local/bin
```

这完成了你的 Linux 软件安装。然而，如果你想在其他计算机的桌面上工作，你需要为目标平台下载并安装 vnc 软件。例如，如果你想在 Windows 95 或 Windows 98 桌面上工作，将 Win32 vnc 软件下载到目标计算机。

# 启用虚拟网络服务

为了在远程桌面上工作，必须在远程计算机上启动 vnc 软件。可以通过 telnet 会话或坐在控制台上启动软件。要为 Linux 启动服务器，从命令行使用 `vncserver` 脚本：

```bash
# vncserver
```

访问你的桌面需要密码。

密码：

输入允许远程访问的密码并按回车。脚本随后加载并启动 Xvnc 服务器（基于 XFree8 3.3.2）。如果你想在网络化 Win32 计算机的远程桌面工作，必须将 Win32 vnc 软件下载到远程计算机。使用存档工具（如 WinZip）提取 Win32 软件。

解压 Win32 vnc 软件并使用 VNC Setup 安装软件。要启动服务器，点击桌面 vnc 文件夹中的 `Default Registry Settings` 项。接下来，点击 WinVNC 菜单，如图 29.10 所示。

# 图 29.10
Win32 vnc 软件提供了 Windows 桌面菜单上易于使用的项目。

![](img/cbac72550c7126a22162e94d91a0c360_960_0.png)

这就是全部操作！如果你需要自定义访问 Win32 桌面的设置，点击 WinVNC 设置项。你会看到如图 29.11 所示的对话框，你可以用它更改网络或密码设置。

从 Linux 查看远程 Win32 桌面，使用 `vncviewer`，后跟 Win32 计算机的主机或 IP 地址，以及 vnc 号（根据 vnc readme 始终为 0）。在 X11 终端窗口中输入命令：

# 图形、多媒体和生产力工具
第四部分

图 29.11
使用 WinVNC 设置对话框为你的 Windows32 桌面配置 WinVNC。

![](img/cbac72550c7126a22162e94d91a0c360_961_0.png)

# vncviewer ascentia.home.org:
你会被提示输入远程 vnc 服务器的密码，直到显示：

vncviewer: VNC server supports protocol version 3.3 (viewer 3.3)
Password：

输入密码并按回车后会出现带有远程桌面的 X11 窗口（如图 29.12 所示）。你可以启动远程应用程序并像操作自己的计算机一样操作它。

# 图 29.12
Linux vncviewer 客户端用于启动远程会话。

![](img/cbac72550c7126a22162e94d91a0c360_961_1.png)

Windows 打印机或依赖于操作系统特定驱动程序的打印机（例如 HP LaserJet 700 和 1000 系列打印机的 USB 专用驱动程序）由本书 CD-ROM 包含的软件支持。你可以通过此处的软件找到这些打印机的支持：

其他打印机（例如对 Epson 彩色打印机的打印支持）需要特定的打印机驱动程序。你可以在以下网站 Calendisp.com 找到更多答案：

Windows（PC 和笔记本电脑通用打印机声音访问的最新趋势）是操作系统特定的，可能永远不受 Linux 支持。这些驱动程序使用免费的通用驱动程序，允许使用无驱动程序设备（选择它是为了避免……）

从 Linux 查看远程 Win32 桌面，使用 `vncviewer`，后跟 Win32 计算机的主机或 IP 地址，以及 vnc 号（根据 vnc readme 始终为 0）。在 X11 终端窗口中输入命令：

```bash
#!/bin/sh
xrdb $HOME/.Resources
xsetroot grey
xterm geometry 80x24
twm &
```

图 29.13
三个远程会话的链可能会有点困惑，但得益于 vnc 软件，运行良好。

![](img/cbac72550c7126a22162e94d91a0c360_962_png)

# 使用 Executor 模拟 Apple Macintosh

由 ARDI 开发的 Executor 是一种商业软件模拟器，你可以在 Linux 下运行它（尽管也有 Windows 版本）。根据 ARDI 的说法，在 90MHz 的 Pentium 上运行大多数应用程序的速度“接近 50MHz 的 6840”。Executor 软件以 .rpm 存档的形式分发，可以在 http://www.ardi.com 获取演示版。

# 图形、多媒体和生产力工具
第四部分

虽然该软件可以帮助你运行近 340 个遗留 Macintosh 应用程序，但 Apple Macintosh 的软件模拟并不完美且具有局限性。默认的 MacOS 是 System 6.0.7，尽管某些 System 7.0 应用程序可以运行。重要的是，其他排除项包括：

- 串口访问
- AppleTalk (LocalTalk)
- CVs
- INITs
- 国际化
- 调制器使用

声音支持有限，且软件可以读写 1.44MB  格式的软磁盘。根据 ARDI 的说法，“桌面配件支持非常弱；大多数无法运行。”

使用 rpm 命令以 root 身份安装。安装后，主执行文件位于 /opt/executor/bin，但在 /usr/local/bin 下会创建符号链接。虽然包含了 SVGA 版本，但运行 executor 命令最简单的方法是在 X11 会话期间。启动 X，然后在终端命令行输入以下命令启动程序：

```bash
# executor &
```

会出现启动屏幕，然后出现主窗口，如图 29.14 所示。
模拟窗口的默认屏幕大小为 640 x 480，但你可以通过使用 Executor 的命令行开关更改它，如表 29.2 所示。

