
## X Server 配置段

本节用于配置 X 服务器应使用的输入设备。
- **InputDevice**
- **Modes** 本节定义 X 服务器可使用的视频模式。
- **Screen** 本节将您的显卡绑定到显示器。
- **Monitor** 本节定义连接在显示适配器上的显示器的参数。
- **ServerLayout** 本节将上述所有部分整合成一个完整的配置。

我指出你应该避免直接编辑 X 服务器配置文件。相反，你应该使用配置实用工具来避免那些可能会损坏硬件的错误。根据你所使用的发行版，你可以使用以下其中一个实用工具：

- YaST
- SaX2
- system-config-display
- system-config-keyboard
- system-config-mouse
- xorgconfig 或 xorgcfg
- Xorg -configure
- XFree-86 -configure
- xf86config 或 xf86cfg
- xvidtune

若要指定默认的窗口管理器，你需要编辑用户主目录中的一个隐藏配置文件。该文件的名称取决于你的发行版和默认的运行级别：

- .xinitrc (运行级别 3)
- .Xsession (运行级别 5)
- .Xdefaults (运行级别 5)
- .Xclients (运行级别 5)

你也可以将 WINDOWMANAGER 环境变量的值设置为你想要使用的桌面环境。

接下来我讨论了如何配置 X 字体服务器。X 字体服务器允许你从一个中心位置为整个组织配置字体。你需要做的第一件事是在 X 字体服务器上安装你要共享的字体。我讨论了位图字体和可缩放字体之间的区别。然后我讨论了字体的安装位置：

- **Type 1** /usr/share/fonts/Type1
- **TrueType** /usr/share/fonts/truetype

将字体文件复制到相应的目录后，你下一步需要运行 `mfktfonts` 和 `mkfontdir` 命令来创建字体描述文件并对字体建立索引。然后你需要在 X 服务器主机的防火墙上打开端口 7100。接下来你要做的是告诉 X 字体服务 (xfs) 字体已存在，并应通过编辑 `/etc/X11/fs/config` 文件使其可供远程 X 服务器客户端使用。在该文件中，你需要注释掉 `no-listen tcp` 行，然后验证在 `catalogue =` 下列出了适当的字体路径。

完成后，你需要启动 `xfs` 守护进程，并配置其在每次系统启动时自动启动。然后重启你的 X 服务器。

此时，我讨论了如何配置远程 X 服务器以使用 X 字体服务器提供的字体。这是通过在 `xorg.conf` 文件的 `files` 部分添加一个新的 `FontPath` 指令，并使用以下语法指向 X 字体服务器来实现的：

```
FontPath "tcp/server_address:7100"
```

然后我讨论了你如何配置显示管理器。你可以使用 `init` 脚本目录中的 `xdm` 初始化脚本来启用或禁用显示管理器。你可以使用 `chkconfig` 命令在系统启动时启用或禁用该初始化脚本。你可以通过编辑相应的配置文件来配置显示管理器：

- **xdm** /etc/X11/xdm/xdm-config
- **kdm** KDE 显示管理器实际上是基于 xdm 的，通常使用 xdm 配置文件。然而，某些发行版将 kdm 设置存储在 /etc/kde/kdm 或 /etc/X11/kdm 中。
- **gdm** /etc/X11/gdm

你还可以使用 /etc/X11/xdm 目录中的其他文件来自定义 xdm 显示管理器的行为：

- **Xresources** 自定义显示管理器在系统启动后呈现给用户的登录界面
- **Xservers** 更改显示管理器的默认颜色深度

然后我讨论了如何配置对本地显示管理器的远程访问权限。首先，你需要允许远程访问你的显示管理器。具体做法取决于你的发行版和正在使用的显示管理器。如果你的主机运行 xdm 或 kdm，请编辑 /etc/X11/xdm/Xservers 文件，找到以 :0 开头的行，并移除 –nolisten tcp 选项。如果你的系统运行 gdm，请编辑 /etc/X11/gdm/gdm.conf 文件并将 DisallowTCP= 设置为 false。如果你正在运行 openSUSE，请编辑 /etc/sysconfig/displaymanager 文件并进行以下更改：

```
DISPLAYMANAGER_REMOTE_ACCESS="yes"
DISPLAYMANAGER_XSERVER_TCP_PORT_6000_OPEN="yes"
```

然后在 xdm 主机的防火墙上打开端口 177。完成后，你接下来在文本编辑器中打开 xdm 主机上的 /etc/X11/xdm/Xaccess 文件，并为每个将访问主机上 xdm 服务的远程系统添加一条条目。

我通过讨论如何在 Linux 系统上配置辅助功能设置结束了本章。为此，你需要启用辅助技术 (Assistive Technologies)。你可以使用的工具之一是 AccessX，它允许你配置多种键盘辅助功能设置，使行动不便的用户也能使用传统键盘：

- StickyKeys
- MouseKeys
- SlowKeys
- ToggleKeys
- RepeatKeys
- BounceKeys
- Delay Keys

对于无法使用传统键盘的行动不便用户，Linux 提供了使用屏幕键盘的选项，该选项允许用户使用任何指点设备（如鼠标）在虚拟键盘上选择按键。

除了键盘辅助功能外，辅助技术还为行动不便的用户提供了鼠标辅助功能选项。你可以配置以下功能：

- 模拟次要点击
- 停留点击
- 鼠标手势

接下来我们查看了使用屏幕阅读器来协助视障用户。屏幕阅读器“读取”屏幕上显示的文本，并以音频形式播放给用户听。Orca 应用程序可能是最常用的 Linux 屏幕阅读器。Orca 还提供屏幕放大镜。屏幕放大镜允许视障用户放大屏幕区域，仿佛他们正在使用真正的放大镜。

然后我们查看了使用 Linux 上的盲文设备来支持视障用户。支持多种类型的盲文显示器和压印机。要与这些类型的设备接口，Linux 系统必须运行 brltty 守护进程。Orca 应用程序也可以用于与盲文设备进行接口。

为了协助视障用户，你还可以实施高对比度、大文本的桌面主题。

## 加速复习

- Linux 图形环境由以下组件组成：
  - X 服务器
  - 窗口管理器
  - 桌面环境
- Linux 系统上实现了两种不同的 X 服务器软件包：
  - X.org-X11
  - XFree86
- 一些更受欢迎的窗口管理器包括以下：
  - enlightenment
  - fvwm
  - kwin
  - sawfish
  - twm
  - wmaker
- 如今，两种桌面环境在 Linux 系统上占主导地位：
  - KDE
  - GNOME
- 在 Linux 上实现显卡/显示器组合之前，你需要检查你发行版的硬件兼容性列表 (HCL)，并确保你的显卡和显示器受到支持。
- 你的 X 配置存储在 `/etc` 目录中的一个文本文件中：
  - XFree86 `/etc/X11/XF86Config`
  - X.org `/etc/X11/xorg.conf`
- `xorg.conf` 文件分为以 `Section` 指令开头并以 `EndSection` 结尾的部分。
- 典型的 `xorg.conf` 中最常用的部分包括：
  - `Files` 告诉 X 服务器在哪里找到它完成工作所需的文件
  - `ServerFlags` 指定全局 X 服务器选项
  - `Module` 告诉 X 服务器在启动时加载某些服务器扩展和字体光栅化模块
  - `InputDevice` 配置 X 服务器应使用的输入设备
  - `Modes` 定义 X 服务器可使用的视频模式
  - `Screen` 将你的显卡绑定到你的显示器
  - `Monitor` 定义连接在你的显示适配器上的显示器的参数
  - `ServerLayout` 将上述所有部分整合成一个完整的配置
- 你应该使用配置实用工具来配置你的 X 服务器软件，以避免那些可能会损坏硬件的错误。
- 你可以使用以下其中一个实用工具来配置你的 X 服务器软件：
  - YaST
  - SaX2
  - system-config-display

