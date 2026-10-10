

![](img/1ea833f5a3e3c1547e3dd2891f52804a_178_0.png)

*图 7.14 startx 客户端使用你的 .xintrc 文件来启动 X 桌面。*

X 服务器将判断你的系统是否能支持为你的系统定义的请求颜色深度和分辨率。不同颜色深度常用的典型值为 8、15、16、24 或 32。如果你使用的是 XFree86 版本 3.3.6，命令行看起来像这样：

```
# startx -- -bpp 8 -dpi 100
```

你甚至可以使用 *startx* 命令来启动多个 X 会话，这在测试新的窗口管理器或在不同颜色深度下运行 X 会话时非常有用。得益于 Linux 对*虚拟控制台*的支持，即可以通过键盘访问的控制台显示器，你可以快速在会话之间切换。

使用 *startx* 命令并附带一个*显示编号*来启动你的第一个 X 会话，该编号指定了一个 X 服务器实例。你可以包含一个颜色深度设置以及一个代表虚拟控制台的数字，如下所示：

```
# startx kde2 -- :0 -bpp 16 vt7
```

X 会话启动后（此处使用 KDE2），按 Ctrl+Alt+F2 返回到仅文本的登录提示符。登录并再次使用 *startx*，如下所示：

```
# startx afterstep -- :1 vt8
```

另一个 X11 会话（这次使用 AfterStep）将会出现。要跳转到 KDE2，请按 Ctrl+Alt+F7。使用 Ctrl+Alt+F8 返回运行第二个会话的 AfterStep。在每个会话中启动不同的客户端，或者注意观察使用的不同颜色深度。如果你跳转到另一个仅文本的控制台，请使用 Alt+F7 或 Alt+F8 返回任一个 X 会话。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_179_0.png)

> 使用 USB Happy Hacking 键盘吗？这款小巧的键盘（长期以来深受经验丰富的 Linux 用户喜爱）要求你按下 Ctrl+Fn+Alt+Meta+<+>FX，其中 X 是所需的 F 键。这是因为 Happy Hacking 键盘将 102 键 PC 键盘的所有按键压缩到了一个紧凑的 80 键键盘上。Mac iBook 和 TiBook 用户可能不得不采用同样的多指操作方式。

## 停止 X11 会话

要停止 X 会话，请使用窗口管理器的注销菜单。这可以通过开始菜单、根显示菜单或在 KDE 或 GNOME 的情况下通过桌面面板访问。如果你的 XFree86 配置文件 `XF86Config` 包含以下内容，你也可以使用键盘组合键来终止正在运行的 X 服务器：

```
# Uncomment this to disable the <Ctrl><Alt><B8> server abort sequence
# This allows clients to receive this key event.
#DontZap
```

为了不允许用户通过使用 Ctrl+Alt+Delete（退格键，而不是三指敬礼式 Ctrl+Alt+Del）来终止 X 会话，请去掉 `DontZap` 前面的注释符（井号）。在 XFree86 4.0 及更高版本中，此选项默认是关闭的，但可以放置在 `serverFlag` 部分中。它看起来像这样：

```
Option    "DontZap"
```

## 配置选择器

与 XFree86 和 Linux 一起常用的三个显示管理器分别是 `xdm`，属于 XFree86 发行版的一部分；KDE 的 `kdm`；以及 GNOME 的 `gdm`。

显示管理器的使用由系统的初始化表 `/etc/inittab` 控制，该表被 `/sbin/init` 命令使用。该命令用于根据运行级别（runlevel）或 Linux 启动到的系统状态来启动最初的 Linux 程序。然而，并非每个 Linux 发行版都定义了相同的运行级别。例如，Yellow Dog Linux 和 LinuxPPC 2000 发行版定义了如下运行级别：

```
# Default runlevel. The runlevels used by RHS are:
# 0 - halt (Do NOT set initdefault to this)
# 1 - Single user mode
# 2 - Multiuser, with out NFS (The same as 3, if you do not have networking)
# 3 - Full multiuser mode
# 4 - unused
# 5 - X11
# 6 - reboot (Do not set initdefault to this)
```

这里最常用的是 1（或单用户模式），用于文件系统修复或管理工作；3，用于正常的控制台登录多用户模式（用于使用 startx）；以及 5，用于带有图形 X 登录并使用显示管理器的多用户模式。

SuSE PPC Linux 定义了这些运行级别：

```
# runlevel 0 is halt
# runlevel S is single-user
# runlevel 1 is multi-user without network
# runlevel 2 is multi-user with network
# runlevel 3 is multi-user with network and xdm
# runlevel 4 is unused
# runlevel 5 is unused
# runlevel 6 is reboot
```

请注意，SuSE 的多用户、控制台模式使用运行级别 2，而带有显示管理器和 X 的图形登录是运行级别 3。默认运行级别通过 /etc/inittab 中的 initdefault 设置指定。

在 LinuxPPC 2000 下，启动到 xdm 使用：

```
id:5:initdefault:
```

对于 SuSE PPC Linux，请使用以下设置：

```
# default runlevel
id:3:initdefault:
```

默认显示管理器可以通过 /etc/inittab 中的运行级别描述来指定，如下所示：

```
x:5:respawn:/usr/bin/xdm -nodaedmon
```

然而，SuSE 和基于 Red Hat Linux 的 PowerPC 发行版使用更复杂的方式来确定默认启动管理器。在 SuSE Linux 中，确定默认启动管理器的逻辑位于：

```
13:3:wait:/sbin/init.d/rc 3
```

在基于 Red Hat Linux 的系统中，名为 *prefdm* 的 shell 脚本，位于 */etc/X11* 目录下，被用来确定使用的显示管理器：

```
x:5:respawn:/etc/X11/prefdm -nodaemon
```

该脚本包含逻辑，基于 /etc/sysconfig 目录下名为 *desktop* 的文件内容来选择显示管理器：

```
...
# Run preferred X display manager
preferred=
if [ -f /etc/sysconfig/desktop ]; then
    if grep -q GNOME /etc/sysconfig/desktop 2>/dev/null; then
        preferred=xdm
    elif grep -q KDE /etc/sysconfig/desktop 2> /dev/null; then
        preferred=kdm
    elif grep -q AnotherLevel /etc/sysconfig/desktop 2> /dev/null; then
        preferred=xdm
    fi
fi
...
```

*desktop* 文件会被解析，查找关键字 **GNOME**、**KDE** 或 **AnotherLevel**，以确定要使用的显示管理器：*gdm*、*kdm* 或 *xdm*。

### 配置 xdm

*xdm* 客户端由 */etc/X11/xdm* 目录下的一系列文件控制。这些文件确定了要使用的 X 服务器、访问权限、你登录的主机、选择器对话框的默认外观以及用于 fail-safe 或终端使用的安全设置。你可以使用其 *-nodaemon* 选项从命令行启动 *xdm* 客户端（作为 *root*），如下所示：

```
# xdm -nodaemon
```

按下回车键后，屏幕将清除，你将看到一个 *xdm* 登录屏幕。输入你的用户名和密码进行登录。

用于你的 *X* 会话的窗口管理器可以在你的 ~/.Xinitrc 文件中指定。

> 如果你使用的是基于 Red Hat Linux 的 PowerPC 发行版，并使用 **xdm** 显示管理器登录，请在登录后使用 *switchdesk* 客户端来选择你的默认窗口管理器。

### 配置 kdm

与 *xdm* 不同，*kdm* 客户端和登录对话框为你的 *X* 会话提供了窗口管理器的选择，其中包括一个用于启动会话的 **Go!** 按钮、一个取消登录的 **Cancel** 按钮，以及一个用于关机、重启系统或重启你的 *X* 服务器的 **Shutdown** 按钮。

要登录，请输入你的用户名，然后是密码。在按下回车键或点击 **Go!** 按钮之前，点击下拉菜单以选择要在你的会话中使用的窗口管理器。*kdm* 可以由 root 操作员在活动的 KDE 会话期间使用 *kdmconfig* 客户端进行配置。该客户端可以通过 KDE 控制中心访问，或者从 X11 终端窗口使用如下命令访问：

```bash
# kdmconfig
```

按下回车键后，你将看到一个对话框，如图 7.15 所示。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_182_0.png)

使用不同的选项卡和对话框来浏览 `kdmconfig` 的配置。你可以更改问候语，选择不同的壁纸，控制用户访问权限，或者为每个用户分配一个图形（或扫描的照片）。

## 配置 gdm

gdm 客户端，就像 `xdm` 一样，为 Linux 和 X 提供图形化登录。可以通过编辑 `/etc/inittab` 并添加如下的 gdm 运行级别 5 条目来使用此客户端：

```
x:5:respawn:/usr/bin/gdm -nodadaemon
```

请注意，在 SuSE PPC Linux 7.0 下，该条目看起来像这样：

```
x:5:respawn:/opt/gnome/bin/gdm -nodadaemon
```

你可以通过编辑 `/etc/X11/gdm` 目录下的 `gdm.conf` 文件来配置 gdm（作为 root）。该文件组织成不同的部分，例如 daemon、security、xdmcp、gui、greeter、debug 和 servers。例如，你可以通过编辑 "greeter" 部分来更改登录对话框的外观：

```
...
Icon=/usr/share/pixmaps/gdm.xpm
LocaleFile=/etc/X11/gdm/locale.alias
Logo=/usr/share/pixmaps/gnome-logo-large.png
QuitVer=0
SystemMenu=
Welcome=Welcome to &\n
...
```

在这个例子中，可以更改对话框的图标、徽标和欢迎消息。自定义 gdm 登录桌面的另一种方式是编辑 `/etc/X11/gdm/init` 目录下名为 `default` 的文件。例如，你可以添加以下内容：

```
/usr/bin/play /usr/share/sounds/retina.wav &
/usr/bin/xclock -bg '#363047' -fg yellow -update 1 -geometry 256x256+20+250 &
```

当屏幕第一次出现时，用户会被要求准备进行视网膜扫描以便登录（好吧，这是个玩笑！）。一个带有黄色指针的大型浮动时钟将出现在登录对话框旁边。（这是利用空闲终端的一个好方法！）

## 资源

http://www.xfree86.org. XFree86 Project, Inc. 的主页。你将在这个站点找到 X 的二进制发行版、源代码和文档。

