

此时，你的系统将加载你指定的窗口管理器或桌面环境。如果你满意当前看到的内容，可以将其设为永久配置。如果你的系统默认启动到运行级别 3，并且你使用 `startx` 命令加载 Linux GUI，那么你需要在用户主目录中找到一个名为 `.xinitrc` 的隐藏脚本文件（使用 `ls -a`）。在文本编辑器中打开此文件，找到内容为 `exec $WINDOWMANAGER` 的那一行，如下所示：

```
# finally start the window manager
#
unset WINDOW_MANAGER_STARTUP
exec $WINDOWMANAGER
# call failsafe
exit 0
```

将 `$WINDOWMANAGER` 替换为你要使用的窗口管理器或桌面环境的名称。请使用以下路径：

- KDE `/usr/bin/startkde`
- GNOME `/usr/bin/gnome`

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_292_0.png)

> 注意，$WINDOWMANAGER 引用的是 WINDOWMANAGER 环境变量。除了编辑你的 `.xinitrc` 文件，你也可以直接将 WINDOWMANAGER 变量的值设置为你想使用的窗口管理器的路径和可执行文件。

保存文件并运行 `startx`。

如果你的系统默认启动到运行级别 5，那么你需要对主目录中的 `.Xsession`、`.Xdefaults` 或 `.Xclients` 文件进行相同的更改，具体取决于你的发行版使用的是哪一个。

接下来，让我们看看如何配置显示管理器。

## 配置显示管理器

正如本章前面所讨论的，Linux 显示管理器是一种专门用于与 X 服务器协作的客户端应用程序，它提供窗口控制元素、管理虚拟桌面，并提供窗口边框功能（例如，改变窗口大小或在屏幕上移动窗口）。X 服务器不链接到任何特定的窗口管理器，因此也不链接到任何特定的外观和感觉。对于你的 LPIC-1/CompTIA Linux+ 考试，你需要知道如何使用显示管理器执行以下操作：

- 启用或禁用显示管理器
- 配置显示管理器
- 配置对显示管理器的远程访问

### 启用或禁用显示管理器

你可以使用初始化脚本来启用或禁用显示管理器。使用哪个脚本取决于你正在使用的 Linux 发行版。在许多 Linux 发行版中，例如 openSUSE，显示管理器由位于 `/etc/init.d` 目录中的 `xdm` 初始化脚本管理。其他发行版可能使用 GNOME 显示管理器（`gdm`）或 KDE 显示管理器（`kdm`）。要手动管理显示管理器，请在 shell 提示符下输入 `/etc/init.d/init_script stop` 或 `start`。

**提示** 你也可以使用 `rccxdm stop` 或 `start` 来达到同样的效果。

由于显示管理器是使用初始化脚本管理的，因此你可以使用 `chkconfig` 命令控制系统启动时是否加载显示管理器。例如，要配置 `xdm` 显示管理器不在启动时加载，请输入 `chkconfig xdm off`。你可以通过在 shell 提示符下输入 `chkconfig xdm -l` 来验证它已被禁用。以下是示例：

```
ws1: # chkconfig xdm off
ws1: # chkconfig xdm -l
xdm 0:off 1:off 2:off 3:off 4:off 5:off 6:off
ws1: #
```

或者，要配置显示管理器在系统启动时自动加载，请输入 `chkconfig xdm on`。同样，输入 `chkconfig xdm -l` 以验证显示管理器已配置为在运行级别 5 时自动启动，如下所示：

```
ws1: # chkconfig xdm on
ws1: # chkconfig xdm -l
xdm 0:off 1:off 2:off 3:off 4:off 5:on 6:off
ws1: #
```

### 配置显示管理器

你可以通过编辑相应的配置文件来配置显示管理器：

- `xdm` `/etc/X11/xdm/xdm-config`

**注意** 本章将重点介绍如何配置 `xdm` 显示管理器。

- `kdm` KDE 显示管理器实际上是基于 `xdm` 的，通常使用 `xdm` 配置文件。然而，某些发行版会将你的 `kdm` 设置存储在 `/etc/kde/kdm` 或 `/etc/X11/kdm` 中。在这种情况下，你将使用这些目录之一的 `kdmrc` 文件进行大多数配置更改。
- `gdm` `/etc/X11/gdm`

**提示** openSUSE Linux 发行版中的许多显示管理器配置设置都存储在 `/etc/sysconfig/displaymanager` 文件中。

除了 `xdm-config` 之外，你还可以使用 `/etc/X11/xdm` 目录中的其他文件来自定义 `xdm` 显示管理器的行为。示例如下：

```
wsl:/etc/X11/xdm # ls
GiveDevices         README.SuSE       README.security   wsl:/etc/X11/xdm #
RunChooser          TakeDevices       Xaccess           Xresources        Xservers            Xsetroot            Xservers        Xsetup
Xreset              Xservers          Xsession          Xwilling          sys.xsession
Xstartup            pixmaps           xdmrc             authdir         xdm-config
```

例如，你可以使用 `Xresources` 文件来自定义系统启动后由 `xdm` 管理器向用户呈现的登录界面。每次 `xdm` 显示管理器启动时都会读取 `Xresources` 文件。可以在该文件中配置的一些指令列在 **表 7-1** 中。

`Xresources` 文件是一个简单的文本文件，因此你可以使用 `vi` 等文本编辑器修改这些指令。进行任何更改后，你必须使用 `/etc/init.d/xdm` 脚本重启显示管理器才能使更改生效。

你还可以使用 `/etc/X11/xdm` 目录中的 `Xservers` 文件来更改显示管理器的默认颜色深度。在文本编辑器中打开该文件，找到以下行：

```
: 0 local /usr/bin/X -nolisten tcp -br vt7
```

**提示** 你需要 root 权限才能修改此文件。

| 指令 | 描述 |
| :--- | :--- |
| **xlogin*Foreground** | 指定登录框的默认前景颜色。 |
| **xlogin*Background** | 指定登录框的默认背景颜色。 |
| **xlogin*greetColor** | 指定登录框中问候语的颜色。 |
| **xlogin*failColor** | 指定当输入的用户名或密码无效时使用的颜色。 |
| **xlogin*login.Font** | 指定用于用户名的字体。 |
| **xlogin*login.greetFont** | 指定用于问候语的字体。 |
| **xlogin*login.promptFont** | 配置用于用户名和密码提示的字体。 |
| **xlogin*login.failFont** | 指定登录失败时使用的字体。 |
| **xlogin*greeting** | 在登录框中显示欢迎问候语。你可以在问候语中包含 CLIENTHOST 变量，这将显示系统的主机名作为问候语的一部分。 |
| **xlogin*namePrompt** | 指定显示的用户名提示。 |
| **xlogin*fail** | 指定登录不成功时显示的文本。 |

**表 7-1** Xresources 指令

要手动设置 `xdm` 显示管理器的默认颜色深度，请在该行末尾添加 `--bpp color_depth`。你可以指定 8、16 或 24 的值。例如，要将默认颜色深度设置为 16 位，请使用以下指令：

```
:	local /usr/bin/X -nolisten tcp -br vt7 :bpp 16
```

与 `Xresources` 文件一样，你必须使用 `/etc/init.d/xdm` 初始化脚本重启显示管理器，以应用你对文件的更改。

接下来，让我们讨论如何配置显示管理器以支持远程 X 终端。

### 配置对显示管理器的远程访问

许多组织为其最终用户使用瘦客户端系统。瘦客户端是一种最小的计算机系统，它使用 X 服务器软件通过网络连接连接到远程 X 服务器并运行显示管理器。这使得显示管理器呈现的远程 X 服务器输出可以在瘦客户端的本地显示器上显示。这种实现方式允许这些组织使用少量高端 `xdm` 系统和大量廉价的瘦客户端，向所有用户提供完整的图形桌面。

> **注意** 某些瘦客户端系统极其简陋。它们甚至可能没有硬盘驱动器。连接到 `xdm` 主机所需的最小 Linux 操作系统和 X 服务器软件嵌入在瘦客户端系统的固件中。

要在你的 `xdm` 主机上配置对显示管理器的远程访问，你需要配置它以监听来自网络中瘦客户端上的 X 服务器软件的传入连接请求。这些请求使用端口 177 上的 Xdm Control Protocol (XDMCP)。请执行以下操作：

1. 如果你的主机正在运行 `xdm` 或 `kdm`，请编辑 `/etc/X11/xdm/Xservers` 文件，并找到以 `: 0` 开头的行，如下所示：

```
:	local /usr/X11R6/bin/X -nolisten tcp -br vt7
```

移除 `-nolisten tcp` 选项；然后保存你对文件的更改并重启系统。

2. 如果你的系统正在运行 `gdm`，请编辑 `/etc/X11/gdm/gdm.conf` 文件并将 `DisallowTCP=` 设置为 `false`。

3. 如果你正在运行 openSUSE，你需要编辑 `/etc/sysconfig/displaymanager` 文件并进行以下更改：

```
DISPLAYMANAGER_REMOTE_ACCESS="yes"
DISPLAYMANAGER_XSERVER_TCP_PORT_6000_OPEN="yes"
```

4. 在 `xdm` 主机的防火墙中打开端口 177。

5. 在 `xdm` 主机上用文本编辑器打开 `/etc/X11/xdm/Xaccess` 文件。此文件用于配置 XDMCP 连接的访问控制。

