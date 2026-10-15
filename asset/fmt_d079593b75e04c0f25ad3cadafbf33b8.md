
`x:5:resp /etc/init` 是

`xdm` 现在会在你启动系统时运行。

## Tip 4.2.1：自定义 `xdm` 提示符

你可以使用通常位于 `/etc/X11/xdm/Resources` 的 `Xresources` 文件来自定义 `xdm` 提示符，该文件包含了定义 `xdm` 外观和行为的项。你可以按照以下方式自定义 `xdm` 提示符：

1. 使用你喜好的文本编辑器打开 `Xresources` 文件。例如，使用 `Emacs` 打开文件，可以使用：

```
emacs /etc/X11/xdm/Resources
```

找到以 `login*greeting=` 开头的行，并修改其值以反映你希望显示在 `xdm` 窗口顶部的文本。典型的 `Xresources` 文件如下：

```
login*greeting: Welcome to CLIENTHOST

login*namePrompt: Login:

login*fail: Login incorrect if WIDTH > 800

login*greetFont: -adobe-helvetica-bold-o-normal-24-240-75-75-p-138-iso859-1
```

如果你使用的是颜色支持的系统，可以自定义 `xdm` 提示符。在 `RedHat` 6 系统上的 `Xresources` 所示：

```
login*translations: #override

<Key>R: abort-display()

<Key>F1: set-session-argument(failsafe) finish-field()

<Key>Return: set-session-argument(failsafe) finish-field()

<Key>Return: set-session-argument() finish-field()
```

如果你使用的是 `RedHat` 7 系统，`Xresources` 所示：

```
login*borderWidth: 1

login*frameWidth: 5

login*innerFramesWidth: 2

login*shdColor: grey30

login*hiColor: grey90

login*background: grey

!login*foreground: darkgreen

login*greetColor: Blue3
```

# 让 Linux 运行起来：核心技巧与技术

```
xlogin*failColor: red

*Foreground: black

*Background: #ffffff

#else

xlogin*borderWidth: 3

xlogin*frameWidth: 0

xlogin*innerFramesWidth: 1

xlogin*shdColor: black

xlogin*hiColor: black

#endif

#if PLANES >= 8

xlogin*logoFileName: /etc/X11/xdm/pixmaps/XFree86.xpm

#else

xlogin*logoFileName: /etc/X11/xdm/pixmaps/XFree86bw.xpm

#endif

xlogin*useShape: true

xlogin*logoPadding: 10

XConsole.text.geometry: 480x130

XConsole.verbose: true
```

# 4：配置 `X` 窗口

| `XConsole*iconic:` | `true` |
| --- | --- |
| `XConsole*font:` | `fixed` |
| `Chooser*geometry:` | `700x500+300+200` |
| `Chooser*allowShellResize:` | `false` |
| `Chooser*viewport.forceBars:` | `true` |
| `Chooser*label.font:` | `*-new century schoolbook-bold-normal-*-240-*` |
| `Chooser*label.label:` | `来自 CLIENTHOST 的 XDMCP 菜单` |
| `Chooser*list.font:` | `*-medium-r-normal-*-230-*-c*-iso8859-1` |
| `Chooser*Command.font:` | `*-new century schoolbook-bold-r-normal-*-180-*` |

找到以 `login*namePrompt` 开头的行，并修改其值以反映你希望显示的用户名提示文本。通常情况下，你会在字符串前加上八进制的 `0040`，以便在提示符和用户输入的用户名之间留出一个空格。

- 3. 找到以 `login*greetColor` 开头的行，并将值更改为任何有效的 `X Windows` 颜色，以更改 `xdm` 顶部主信息的颜色。
4. 保存文件并关闭文本编辑器。

# 技巧 4.2.2：自定义 `xdm` 窗口颜色

你可以使用 `Xresources` 文件自定义 `xdm` 窗口的背景颜色，在 `RedHat Linux` 7 系统上，该文件通常位于 `/etc/X11/xdm/Xresources`。此文件包含一系列 `X` 资源样式，定义了 `xdm` 提示符的视觉外观和行为。你可以按照以下步骤自定义 `xdm` 提示符文本：

- 1. 使用你偏好的文本编辑器打开 `Xresources` 文件。例如，使用以下命令用 `Emacs` 打开文件：

```
# emacs /etc/X11/xdm/Xresources<ENTER>
```

- 2. 找到以 `xlogin*background` 开头的行，并将值更改为任何有效的窗口颜色，以更改 `xdm` 窗口的背景颜色。
3. 保存文件并关闭文本编辑器。

## 技巧 4.2.3：配置 `xdm` 为 `X` 终端和其他 `Linux` PC 提供登录服务

`Linux` 系统上的 `xdm` 进程可以作为运行在其他 `X Windows` 系统上的客户端的登录服务器。要配置 `xdm` 以以这种方式运行，请执行以下步骤：

- 1. 使用你偏好的文本编辑器打开 `Access` 文件进行编辑。例如，使用以下命令用 `Emacs` 打开文件：

```
# emacs /etc/X11/xdm/Xaccess<ENTER>
```

- 2. 在文件中添加以下行：

`CHOOSER BROADCAST`

- 3. 保存文件并关闭文本编辑器。

当你重启 `xdm` 时，你的系统将作为网络上其他运行 `xdm` 终端的登录服务器工作。

# 技巧 4.2.4：通过向 `xdm` 服务器请求登录提示，将 `Linux` 系统作为 `X` 终端

如果你想通过向 `xdm` 服务器请求登录提示，将 `Linux` 系统作为 `X` 终端，并在该机器上登录并运行桌面环境或应用程序，你需要以特殊方式启动 `Windows`。不是使用运行本地设置并启动本地管理器或桌面环境的启动脚本，而是通过直接调用 `X` 服务器并让其查询远程登录符来启动 `Windows`：

```
X -query xdm服务器
```

例如，如果你在主机 `xserv` 上运行 `xdm`，可以通过以下命令在客户端上启动 `Windows`：

```
# X -query xserv<ENTER>
```
