

双破折号是将参数直接传递给 xinit 程序所必需的。

当你首次运行 startx 时，你的主目录中很可能没有预装的 .xinitrc 文件；因此，将使用系统范围的 xinitrc 文件。要创建你自己的 .xinitrc 文件，请运行 `locate xinitrc` 命令，在 `/usr/X11R6/lib/X11/xinit` 或 `/etc/X11/xinit` 中找到一份 xinitrc 的副本。将此文件复制到你的主目录，并重命名为以句点开头，使最终文件名为 `.xinitrc`。

## 配置 .xinitrc

如前所述，`.xinitrc` 脚本用于根据用户偏好启动客户端应用程序。当在用户主目录中找到此类脚本时，startx 将运行它；当 `.xinitrc` 脚本退出时，它将终止 X Window 服务器。因此，你必须在脚本中调用一个客户端应用程序，以便控制权不会落到脚本底部（导致其退出），除非你终止该客户端应用程序。通常，这是通过在后台运行除最后一个之外的所有客户端程序来实现的。最后一个客户端程序通常是一个 X Window 管理器。清单 14-1 显示了一个示例 `.xinitrc` 文件。

### 清单 14-1 示例 .xinitrc 文件

```
#
# Example .xinitrc
#

# start xclock (in the background)
xclock -geometry 50x50-1+1 &

# start two xterms (in the background)
xterm -geometry 80x50+494+51 &
xterm -geometry 80x20+494-0 &

#

# now start a window manager in
# the foreground
#
# If my favorite GNOME is there, start it
if [ -f /usr/bin/gnome-session ]; then
    exec gnome-session
# Ok, no GNOME, try KDE
elif [ -f /usr/bin/startkde ]; then
    exec startkde
# Ok, no GNOME or KDE, try just twm
else
    exec twm
fi
```

正如你所见，xclock 和 xterm 等 X 应用程序的实例使用 `&` 运算符在后台执行。只有 X Window 管理器应用程序在前台运行。你应该从像前面那样简单的 `.xinitrc` 文件开始，并修改它以包含你需要默认启动的 X 应用程序。

你可以选择不使用窗口管理器直接运行 `xinit` 来运行 X Window；然而，大多数人会发现窗口管理器是在 X Window 下工作的必备工具。流行的 X Window 管理器包括 fvwm2、fvwm、afterstep、twm、wmaker 和 wmx 等。每个窗口管理器都有其自己的外观和风格，因此对不同用户有不同的吸引力。我建议你安装流行的窗口管理器并试用它们。

## 自定义客户端应用程序的外观和风格

当你运行一个 X 客户端应用程序，如 xterm 或计算器 (xcalc) 时，该应用程序的默认外观和风格通常来自 `/usr/X11R6/lib/X11/app-defaults` 中的一个文件。例如，xcalc（计算器）的默认外观和风格来自 `/usr/X11R6/lib/X11/app-defaults/Xcalc` 文件。你可以修改这些默认值，为你和/或你的用户提供自定义的外观和风格。请务必备份你想要修改的每个文件。

如果你只对更改少数应用程序的外观和风格以供自己使用感兴趣，可以在主目录中创建一个 `.Xresources` 文件，并使用以下语法添加行：

```
<application><resource key>: <resource value>
```

例如，我在我的 `.Xresources` 文件中放入了以下行，以更改 xcalc 程序数字显示的默认背景颜色（黑色）：

```
XCalc*bevel.Background: red
```

为了确定哪个资源负责更改这一特定颜色，我首先查看了 `/usr/X11R6/lib/X11/app-defaults/XCalc` 文件。找到该资源后，我将其复制到我的 `.Xresources` 文件中，并在该行前加上应用程序名称 (XCalc)。如果你在主目录中使用 `.xinitrc` 文件，请在加载任何客户端应用程序之前放入 `xrdb -merge $HOME/.Xresources`。每当你在 `.Xresources` 文件中添加或修改资源时，都可以从命令行运行此命令，以将资源更改集成到当前的 X 环境中。

## 使用 xdm，X 显示管理器

如果你想提供一个图形用户认证界面，X 显示管理器，即 xdm，就是答案。使用 xdm，你可以通过图形登录屏幕认证用户，并直接将他们带入他们的 X Window 环境。该程序的目的是提供类似于 getty 和 login 的服务。你可以简单地按如下方式启动显示管理器：

```
xdm &
```

xdm 配置文件位于 `/usr/X11R6/lib/X11/xdm` 目录中。文件 `xdm-config` 用于配置登录屏幕向用户显示的外观，`Xsetup_0` 用于告诉 xdm 启动 X 时应启动哪些程序。默认的 `Xsetup_0` 如下所示：

```
#!/bin/sh

# Xsetup for Red Hat Linux
# Copyright (c) 1999, 2000 Red Hat, Inc.

pidof -s kdm > /dev/null 2>&1
if [ $? -eq 0 -a -x /usr/bin/kdesktop ]; then
    /usr/bin/kdesktop
else
    /usr/X11R6/bin/xsetroot -solid "#356390"
fi

# only set the background if the xsri program is installed
if [ -x /usr/bin/xsri ]; then
    /usr/bin/xsri -geometry +5+5 -avoid 300x250 -keep-aspect \
    /usr/share/pixmaps/redhat/redhat-transparent.png
fi
```

当用户通过认证时，此文件启动 xconsole 和 xbanner 程序。这些对大多数用户实际上毫无用处。因此，你应该将其修改为适合你的内容。例如，你可以使用 xv 程序将 X 环境的背景设置为适合你组织的内容。或者，你可以启动一些通常由大多数用户运行的应用程序，如 xmailbox。

可以通过将默认运行级别更改为 5，使 xdm 在引导后自动运行。要将系统的运行级别更改为 5，请修改 `/etc/inittab` 文件中的以下行：

```
id:3:initdefault:
```

将 3 替换为 5。并确保同一文件中包含以下行：

```
# Run xdm in runlevel 5
# xdm is now a separate service
x:5:respawn:/etc/X11/prefdm -nodaemon
```

## 在 MS Windows 9x/2000 上使用 XFree86

要在 MS Windows 9x/2000 上运行 X Window 应用程序，你需要在这类平台上运行一个 X Window 服务器。有许多适用于 MS Windows 9x/2000 的商业 X Window 服务器软件包，如 Metro X-Win32、Reflection/X、Exceed 和 NTCracker。本节使用 Micro X-Win32，我已使用一年多，发现它非常易于安装和支持。

### 获取 Micro X-Win32

你可以从 StarNet Communications Corporation 的 http://www.starnet.com/ 下载 X-Win32 的评估副本。该产品的评估版运行方式与产品版完全相同；唯一的限制是每个会话只能使用评估版两小时；每过两小时，你就必须在 MS Windows 端重新启动 X Window 服务器。由于评估版中没有任何功能被阉割，因此这一限制并不是大问题。毕竟，如果你使用它，你应该付费！

下载评估副本后，它通常以自解压可执行文件的形式出现，双击该可执行文件即可解压文件；安装程序将自动开始。系统会要求你选择安装的目标目录。安装完成后，你就可以在 MS Windows 上使用 X Window 服务器了，你的 Red Hat Linux 服务器的 X 客户端应用程序可以在运行本地 X Window 服务器的 MS Windows 系统上运行。

在你能从 Red Hat Linux 安装运行 X 客户端之前，需要使用随发行版提供的 X-Util32 程序配置 Micro X-Win32。执行以下操作：

- 在 Windows 9x 或 Windows NT/2000 系统上运行 X-Util32 程序。
- 从其菜单中选择 **Sessions > Edit sessions**。从此菜单中选择一个现有的会话条目，如 sun。这将显示一个包含当前会话信息的对话框。
- 通过在 **Session name** 字段中键入新名称来重命名会话条目。这可以是任何名称。接下来，选择连接方式：rsh（远程 shell）、rexec（远程执行）或 XDMCP（用于 xdm）。为你的 Red Hat Linux X Window 环境选择最合适的一种。例如，如果你在 Linux 端运行 xdm，请选择 XDMCP。

如果你选择使用远程 shell 选项，则必须在 Linux 用户的主目录中有一个 `.rhosts` 文件。该文件必须包含 MS Windows 系统的主机名或 IP 地址。

此外，请确保你没有在 `/etc/xinetd.d` 中相应的服务文件里禁用 rsh 或 rexec 服务。出于安全考虑，你可能希望通过 `/etc/hosts.deny` 文件禁止任何人使用 rsh 或 rexec，并仅在 `/etc/hosts.allow` 文件中允许特定主机使用这些服务。

- 如果你想每次启动 Micro X-Win32 时自动启动此会话，请勾选 **Auto startup** 选项。此外，确保 **Window setting** 设置为 **Switch to multiple windows** 选项。
- 在 **Host** 字段中输入将驻留 X 应用程序的 Red Hat Linux 服务器的主机名。
- 在 **Login** 字段中输入用户名。如果你选择远程执行 (rexec) 选项，每次想要连接会话时都会被要求输入密码。如果你倾向于只输入一次密码（不推荐，因为这可能是一个安全问题），请在 **Password** 字段中输入，该字段仅在你选择 rexec 选项时出现。
- 在 **Command** 字段中，输入你想要运行的命令。通常，你会想在这里运行一个 xterm。因此，将此字段设置为以下值：

```
/usr/bin/X11/xterm -ls -display $DISPLAY
```

- 保存修改后的会话并退出 Micro X-Win32 应用程序。

现在，你已准备好运行新会话。单击任务栏上的 Micro X-Win32 图标，选择 **Sessions** 菜单，然后选择修改后的会话名称。如果你通过 rexec 连接，系统会要求你输入密码。

