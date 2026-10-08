
对于 GNOME 图形用户界面（或 GNOME GUI，Red Hat Linux 的默认设置），`/etc/X11/prefdm` 运行 `/usr/bin/gdm` —— GNOME 显示管理器。“从 GNOME 切换到 KDE”章节将向你展示 `/etc/X11/prefdm` 运行 `/usr/bin/kdm` —— KDE 管理器。这意味着无论你选择什么 GUI，在级别 5 都会启动一个显示管理器。显示管理器反过来显示图形登录对话框，使你能够登录系统。

如果你在 Red Hat 安装期间没有启用图形登录界面，可以通过编辑 `/etc/inittab` 文件来实现。找到包含 `initdefault` 的行行，并确保其内容如下：

`id5:initdefault:`

在编辑 `/etc/inittab` 文件之前，你应该知道该文件中的任何错误都可能导致 Linux 无法启动到可以登录的状态。如果你无法登录，就无法使用你的系统。

## GNOME 显示管理器 (gdm)

`gdm` 程序被编写为 `xdm`（X 显示管理器）的替代品。与 `xdm` 类似，`gdm` 为每个本地显示启动 X 服务器，显示登录对话框并允许用户登录系统。

当 `gdm` 运行时，它会读取配置文件 `/etc/X11/gdm/gdm.conf` 的各种配置参数，该结构类似于 Windows 的 ini 文件。例如，这里是一个典型的 `gdm.conf` 文件：

```
[daemon]
AutomaticLoginEnable=false
AutomaticLogin=
AlwaysRestartServer=false
Configurator=/usr/bin/gdm/configurator --disable-sound --disable-crash-dialog
GnomeDefaultSession=/usr/share/gnome/default.session
Chooser=/usr/bin/gdmchooser --disable-sound --disable-crash-dialog
DisplayPath=/usr/bin:/usr/bin:X11:/usr/local/bin;/usr/bin
DisplayInitDir=/etc/X11/gdm/Init
Greeter=/usr/bin/gdmlogin --disable-sound --disable-crash-dialog
Group=gdm
HaltCommand=/usr/bin
KillInitClients=true
LogDir=/var/log/gdm
PidFile=/var/run/gdm.pid
PostSessionDir=/etc/X11/gdm/PostSession/
PreSessionScriptDir=/etc/X11/gdm/PreSession/
FailsAfterServer=
XKeepsCrashing=/etc/X11/gdm/XKeepsCrashing
KeepsCrashingConfigurator=/usr/bin/X11/config
RebootCommand=/usr/bin/shutdown -r
RootPath=/bin:/usr/bin:/bin:X11:/usr/local/bin
root/gdm
SessionDir=/etc/X11/gdm/Sessions/
SuspendCommand=
User=gdm
UserAuthDir=/tmp
UserAuthFile=.authority
TimedLoginEnable=false
TimedLoginDelay=30
[security]
AllowRoot=true
AllowRemoteRoot=true
AllowRemoteLogin=false
Permissions=0
RetryDelay=1
UserMaxFile=65536
SessionFile=VerboseAuth=true
[xdm]
Enable=false
HonorIndirect=true
MaxPending=4
MaxPendingIndirect=4
```

```
MaxSessions=16
MaxWait=30
MaxWaitIndirect=30
Port=7

[gui]
Gtk=false
Wait,no,false
MaxWidth=128
MaxHeight=128

[greeter]
TitleBar=false
Available=false
DefaultFace=/usr/share/themes/gtk
Defaultlocale=en_US
DefaultFont=helvetica-bold
Defaultmark=
Quit=true
SystemMenu=true
LockPosition=true
SetPosition=0
PositionY=0
XineramaScreen=0
Color=0
BackgroundColor=
BackgroundScaleFit=true
BackgroundRemoteOnly=true
BackgroundProgram=/usr/bin/redhat-login
ShowChooser=false
ShowFailsafeSession=false
ShowXtermFailsSession=false

[chooser]
CurrentImage=/usr/share/pixmaps/host.png
HostImageDir=/usr/share/hosts/
ScanTime=3
```

```
Hosts=
Broadcast=true

[debug]
Enable=false

[servers]
0=/usr/bin/X11
#1=/usr/bin/X11
#Note: 如果你想确保 X 运行在特定的控制台上，#0 你可以使用以下内容（针对控制台 7）：
#0=/usr/bin/X11 vt7
```

`[servers]` 部分指定了 gdm 显示登录对话框的显示。该部分的每一行都以显示数字开头，并显示启动 X 服务器所需的命令。表 9-1 描述了所有的 gdm 选项。

编辑 `Welcome=` 行可以更改图形登录界面上的欢迎信息。默认消息显示主机名，这可能有些晦懂。你可以使用 `Welcome=Welcome to XYZ Corp.` 语法将该行更改为更有意义的内容。

![](img/32dd492a14c1741062582e3caae7f04b_282_0.png)

# 表 9-1 gdm 配置选项

| 配置选项 | 说明 |

| --- | --- |

| [daemon] 部分 | 如果设置为 true，gdm 总是杀死现有的 X 服务器并启动一个新的。 |

| AlwaysRestartServer=true or false | gdm 总是杀死现有的 X 服务器并启动一个新的。 |

| AutomaticLoginEnable=true or false | 设置为 true 则自动登录 `AutomaticLogin` 选项中指定的用户而无需密码。 |

| AutomaticLogin=username | 如果指定了用户名且 `AutomaticLoginEnable` 为 true，则无需密码登录该用户。 |

| Chooser=chooserprogram | `gdmchooser` 执行文件的完整路径和名称（通常应为 `/usr/bin/gdmchooser`）。 |

| Configurator=chooserprogram | `gdmconfig` 执行文件的完整路径和名称（通常应为 `/usr/bin/gdmconfig`）。 |

## 第二部分：探索红帽 Linux

| 配置选项 | 描述 |

| :--- | :--- |

| DefaultPath=pathname | 用于用户会话的路径（冒号分隔的目录名称） |

| DisplayInitDir=pathname | 包含初始化脚本的目录（默认是 /etc/X11/gdm/Init） |

| GnomeDefaultSession=sessionfile | 当没有用户 GNOME 会话文件时，gdm 读取的完整文件名（默认是 /usr/share/gnome/default.session） |

| Greeter=greeterprogram | 引导程序（greeter）可执行文件的完整路径和名称，后面后跟参数（通常，这应该是 /usr/bin/gdmlogin） |

| Group=groupname | 运行 gdmchooser 的用户组名（默认是 gdm） |

| HaltCommand=haltprogram | 当用户从系统菜单选择“停机”时执行的命令的完整路径和参数（通常，这应该是 /sbin/shutdown -h now） |

| KillInitClients=true or false | 设置为 true 时，用户登录后，gdm 会杀死由初始化脚本启动的 X 客户端（默认是 true） |

| LogDir=pathname | 包含显示日志文件的目录（默认情况下，此选项的值与 ServAuthOption 相同） |

| PidFile=pidfile | 存储 gdm 进程 ID（pid）的文件名（默认是 /var/run/gdm.pid） |

| PostSessionScriptDir=pathname | 包含 PostSession 脚本的目录——在用户注销后运行的脚本（默认是 /etc/X11/gdm/PostSession/） |

## 第9 章：GUI 桌面

| 配置选项 | 描述 |

|---|---|

| PreSessionDir=pathname | 包含 PreSession 脚本的目录——在用户登录后立即运行的脚本（默认是 /etc/X11/gdm/PreSession/） |

| RebootCommand=rebootprogram | 当用户从系统菜单选择“重启”时执行的命令的完整路径和参数（通常，这应该是 /sbin/shutdown -r now） |

| RootPath=pathname | 用于 root 用户会话的路径（冒号分隔的目录名称） |

| ServAuthDir=pathname | 包含显示器 X 认证文件的目录（/var/gdm）（此目录应由用户 gdm、组 gdm 拥有，权限为 750） |

| SessionDir=pathname | 包含系统上所有可用会话类型脚本的目录（默认是 /etc/X11/gdm/Sessions） |

| TimedLoginEnable=true or false | 如果设置为 true，则自动登录 TimedLogin 选项中指定的用户，无需询问任何密码 |

| TimedLogin=username | 如果指定了用户名且 TimedLoginEnable 为 true，则在登录界面非活动状态持续 TimedLoginDelay 选项指定的秒数后，该用户将在无需询问密码的情况下登录 |

| TimedLoginDelay=N | 在 TimedLogin 中指定的用户自动登录之前等待的秒数 |

| User=username | 运行 gdmchooser 和 gdmlogin 的用户名（默认是 gdm） |

| 表 9-1（续） | |

| 配置选项 | 描述 |

| UserAuthDir=pathname | 应当保存用户的 .Xauthority 文件路径的目录（如果此字段为空，则使用用户主目录，这是默认值） |

| UserAuthFBDir=pathname | 如果 gdm 无法更新用户的 .Xauthority 文件，则创建回退 cookie（它仅指向少量的认证信息）的目录（默认是 /tmp） |

| UserAuthFile=filename | 存储用户认证 cookie 文件名（默认是 .Xauthority） |

| XKeepsCrashing=sessionfile | 如果 X 持续崩溃时应运行的脚本完整名称（默认脚本是 /etc/X11/gdm/XKeepsCrashing） |

| XKeepsCrashingConfigurators=config1 config2 | 如果 X 持续崩溃，gdm 可以运行以配置 X 的一个或程序的完整名称（默认程序是 /usr/bin/X11/XF8Setup /usr/bin/X11/Xconfig） |

| [security] 节 | |

| AllowRoot=true or false | 设置为 true 时，root 用户在控制台登录（默认是 true） |

| AllowRemoteRoot=true or false | 设置为 true 时，root 用户远程登录（默认是 true） |

| RelaxPermissions=0, 1, 或 2 | 0 = gdm 仅接受由用户拥有的文件和目录；1 = gdm 允许组写入的文件和目录；2 = gdm 允许可写的文件和目录（默认是 1） |

| RetryDelay=N | 登录失败后 gdm 再次显示登录窗口之前的等待秒数（默认是 3 秒） |

| UserMaxFile=N | gdm 读取或写入的文件的最大大小（字节）（默认是 64KB，或 65536 字节） |

| VerboseAuth=true or false | 设置为 true 时，gdm 在消息中打印认证错误 |

| Enable=true or false | 设置为 true 时，gdm 支持登录窗口（默认是 true） |

| HonorIndirect=true or false | 设置为 true 时，gdm 允许间接连接（默认是 true） |

| Pending=N | 最大等待数（默认是 4） |

| MaxSessions=N | gdm 允许的最大会话数（默认是 16） |

| MaxWait=N | gdm 等待响应的最大秒数（默认是 30） |

| Port=177 | gdm 监听的端口号（默认是 177） |

| 表 9-1（续） | |

| 配置选项 | 描述 |

| --- | --- |

| [gui] 节 | |

| GtkRC=pathname | gdm 使用的主题（默认为空） |

| MaxIconWidth=N | 图标的最大宽度（默认是 128 像素） |

| MaxIconHeight=N | 图标的最大高度（默认是 128 像素） |

| PingInterval=N | ping X 服务器并检查其仍然运行的分钟数 |

| [greeter] 节 | |

| Browser=true or false | 设置为 true 时，显示名为“脸部浏览器”的浏览器，其中显示所有用户的脸（默认是 false） |

| DefaultFace=imagefile | gdm 用户可读的文件，当用户在 ~/.gnome 目录中没有图片时显示的图像。默认值是 /usr/share/pixmaps/nobody.png |

| DefaultLocale=localename | 如果 ~/.gnome 中未指定且用户未在引导程序中选择语言，则会话使用的语言。（默认是 english。） |

# 第二部分：探索 Red Hat Linux

| 表 9-1 (续) | |

| 配置选项 | 描述 |

| --- | --- |

| [chooser] 节 | |

| DefaultHostImg=filename | 对于那些没有唯一图标文件的主机，包含要显示的图像的文件（默认为 /usr/share/pixmaps/nohost.png） |

| ImageDir=pathname | 目录（默认为 /usr/share/hosts/），其中包含的主机图标文件名与主机系统的完全限定域名匹配（例如 yourhost.yourdomain.com）。 |

| ScanTime=N | 选择器等待其 XDMCP 广播查询答复的秒数（默认为 3 秒） |

| [debug] 节 | |

| Enable=true or false | 设置为 true 时，gdm 会保存信息，这有助于隔离 gdm 中的任何错误（默认为 false） |

| [servers] 节 | |

| N=/usr/bin/X11/X | 启动用于本地显示器编号的 X 服务的命令（如果你的系统只有一个显示器，N 为 0） |

对于默认配置（在安装了 Red Hat Linux 和随附 CD-ROM 中的 X 后），gdm 以如下方式管理登录会话：

- 1. gdm 程序启动 X 服务，并对以本地显示器命名的脚本进行响应（对于第一个显示器，文件名为 :0），该脚本位于 `/etc/X11/gdm/Init` 目录。如果找不到该文件，则执行该目录下名为 Default 的文件。Red Hat Linux 中的 `/etc/X11/gdm/Init/` 脚本包含以下命令：

```sh
#!/bin/sh
# Xsetup for Red Hat Linux
# Copyright (c) 1999, 2000, 2001 Red Hat, Inc.
```

## 第 9 章：GUI 桌面

```sh
/usr/X11R6/bin/xsetroot -solid #5477A0

if [ -z$RUNNING_UNDER_GDM ]; then
  /sbin/pidof -s kdm & /dev/null && $? -eq 0 -a -x
  /usr/bin/kdmesktop j && /usr/bin/kdmesktop && sleep 1

# 只有在安装了 xsri 程序时才设置背景
if [ -x /usr/bin/xsri -a -f /etc/X11/xsirirc ]; then
  /usr/bin/xsri --redhat-login --set
fi
fi
```

在这种情况下，脚本将背景设置为纯色并显示 Red Hat Logo。gdm 程序以 root 身份运行此脚本并等待命令完成。

- 2. gdm 程序运行 `/usr/bin/gdmlogin` 程序，该程序会显示一个对话框，其中包含用户可以输入用户名和密码的字段。
