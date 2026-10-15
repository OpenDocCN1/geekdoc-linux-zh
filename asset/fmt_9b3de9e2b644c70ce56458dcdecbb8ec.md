
KDE 对我来说显然很好用，尽管在旧硬件上或高负载下它感觉很重。这里列出了`RedHat`/`Mandrake`光盘中可用的窗口管理器列表，供你决定是否要安装它们。我几乎全部使用`KDE`，尽管其他管理器可能更小、运行更快。`Gnome`是一个著名的`X-windows`项目，据说比`KDE`更先进、更漂亮，但它仍然存在很多Bug，所以除非你不介意偶尔出现问题，否则不推荐。`RH6.x`包含了两个主要的`X-windows`系统：`Gnome`和`KDE`。

## 5.3.5 我可以同时运行多个 X 会话吗？

可以。当你在系统上使用 `startx` 命令时，第一个 X 会话默认显示为 0。第二个 X 会话将在不同的显示上打开。例如，这将在显示 1 上打开另一个 X 会话：

```
start 1
```

你最多有 6 个并发 X 会话。使用 `<ctrl><Alt=F7>` 切换到显示 0，`<ctrl><Alt=F8>` 切换到第二个屏幕，最多到 `<ctrl><Alt=F12>`。如果需要更多信息，请尝试 `man switch`。

同样，你可以打开另一个没有窗口管理器的裸会话。这将在显示器 2 上打开：

```
xinit :2
```

在这个裸显示器上，我可以通过在终端输入运行不同的窗口管理器（以便同时运行两个），详情请见上一个回答：

```
startde gnome-session
xfce
afterstep
AnotherLevel
fvwm
```

## 5.3.6 我姐姐可以拥有第二个 GUI 提示，这样她不需要杀死我的 X 会话吗？

为了在不同的终端上启用多个 GUI 登录（`RedHat`使用`gdm`进行图形登录），我必须编辑 `/etc/X11/gdm.conf` 文件。在该文件的末尾 `<Ctrl><Alt-F7>` 有以下条目：

```
[servers]
3=/usr/bin/X11/10
2=/usr/bin/X11/9
1=/usr/bin/X11/8
0=/usr/bin/X11/7
```

为了在两个终端上运行 `KDE` 和 `GNOME` 的四个 GUI 列表，以便我姐姐可以不杀死我的屏幕，在 `Mandrake` 下启用并发登录（`Mandrake` 使用 `kdm` 进行图形登录），我必须修改两个文件：`/etc/X11/xdm/Xservers` 包含：

```
:0 local/X11/bin/X
:1 local/X11/bin/X
:2 local/X11/bin/X
```

以及 `/etc/X11/xdm/config` 包含显示 0 和 1 的设置，如下：

```
DisplayManager_0.true /etc/X11/xdm/Xsetup
DisplayManager_1.true /etc/X11/xdm/GiveConsole
DisplayManager_2.true /etc/X11/xdm/TakeConsole
DisplayManager_0.reset /etc/X11/xdm/Xsetup
DisplayManager_1.reset /etc/X11/xdm/GiveConsole
DisplayManager_2.reset /etc/X11/xdm/TakeConsole
DisplayManager_0.start /etc/X11/xdm/Xsetup
DisplayManager_1.start /etc/X11/xdm/GiveConsole
DisplayManager_2.start /etc/X11/xdm/TakeConsole
```

这允许我在带有第三终端的电脑上同时运行 `gnome` 和 `kde`。

## 5.3.7 如何远程访问 X-window？

- 在本地机器上运行 X-server，例如 `xinit`
- 从 x-终端允许远程机器显示在你的本地屏幕上：`xhost [远程服务器名称]`
- 在我家里非常安全的环境下，可以使用 `xhost +` 允许所有服务器在我的屏幕上显示（连接互联网时不要这样做）
- telnet 到远程服务器。在远程服务器上运行 x 程序显示在你的本地屏幕，例如你可以启动一个窗口管理器：“&”符号让命令在后台运行，这样你的 telnet 窗口仍然可用。

0.0 意味着“display zero，screen zero”，它是你第一个显示器的第一个屏幕，因为你可以在 Linux 上运行许多并发 X 会话。如果你的环境指定了当前终端正确的位置，你不需要指定“display”选项，我的系统默认就是如此，但今天其他人并非如此。你可以检查你的 `DISPLAY` 设置：

```
echo DISPLAY
```

- 在镜像远程会话后，我恢复 X-server 的访问控制：`xhost [远程服务器名称]`
- 示例。此系列命令将在名为 `marie` 的远程机器上运行 `Netscape`，将显示重定向到运行在本地机器 `hacker` 上的 `X-windows` 管理器：

```
startx
xhost marie
telnet marie
[login]
netscape -display hacker:0.0 &
[do my stuff]
logout
xhost marie
```

原则上，你可以在网络上的任何电脑上运行程序，并将输出显示在任何其他电脑上（不一定是你正坐在那台电脑上）。

我使用 X-window 在一台机器（48-33，8 MB 内存）上运行许多大型程序（`kde`、`Word 8` 和 `Netscape`），这些程序本身无法运行。这也是在没有设置 `mfs` 的远程系统上工作的一种方便快速的方法。X-window 设计之是为了通过网络远程运行。远程 X-window 是一个强大的工具，而且体验非常愉快。尝试一下。

如果你为 Windows 安装了 X-window 程序，你可以在 Linux（或任何 Unix）上运行程序并将显示重定向到本地 Windows 机器。查看选项概述：`http://www.linuxworld.com/linuxworld/jw-2000-09/jw-09-legacy_1.html`

## 5.3.8 我如何从 Windows 分区安装 TrueType 字体？

某些发行版拥有 `TrueType` 字体服务器但没有（或可选有限）`TrueType` 字体。不过你可以安装自己的 `TrueType` 字体。以下是我手动操作的方法。`Mandrake` 包含一个将 Windows 字体传输到 Linux 的 GUI 工具，所以你不需要担心下面的步骤。

- 0. 从 K-菜单（`KDE`）选择“Font Manager”（或类似工具）并记录已安装的字体。
- 1. 在命令行上，检查是否安装了“free”字体服务器：

```
rmp -q freetype
```

这会查询软件包管理器 `freetype` 包。如果包已安装，请继续。如果没有安装 `freetype`，请从你的发行版光盘安装。我的系统在完整安装 `RH` 后安装了 `freetype`。

- 2. 以 root 身份创建一个存放 `TrueType` 字体的目录：

```
mkdir TrueType
cd /usr/lib
```

该目录在配置文件 `/etc/X11/xF86Config` 中引用，以确保名称完全一致。如果你想编辑，请打开 `/etc/X11/xF86Config` 并进行相应调整。我的 `RedHat` 默认路径包含这样一行：`FontPath "/usr/X1RR6/lib/fonts/TrueType"`

- 3. 以 root 身份，从你的 `TrueType` 字体目录拷贝你的 `.ttf` 文件到刚创建。我从 MS Windows 位置提取了 `TrueType`，你可能需要使用不同的源位置：

```
$ /usr/X11/lib/X11/fonts/TrueType
cp /mnt/dos/idal/fonts/my_private_fonts/*.ttf
```
