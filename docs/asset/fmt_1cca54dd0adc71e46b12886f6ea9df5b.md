
是的，Evolution 不仅仅是一个邮件客户端。但 UCP 课程规定候选人需要知道如何“配置 Evolution 以与各种类型的服务器和过滤器配合”，这可以帮助你管理垃圾邮件和其他邮件。`evolution-exchange` 包支持从 Evolution 邮件客户端连接到 Microsoft Exchange 服务器。

### 日志文件

GNOME 显示管理器与 GNOME 桌面环境相关的图形化登录界面，如下所示。界面看起来简单，但配置选项要复杂得多。要理解 GNOME 显示管理器是如何配置的，你需要了解 `/etc/gdm` 目录中的配置文件以及 `gdmsetup` 工具提供的可用选项。通过这些工具，你可以“自定义显示管理器的欢迎界面，包括登录横幅和登录屏幕”。

### GNOME 显示管理器配置文件

主要的 GNOME 显示管理器配置文件是 `/etc/gdm/gdm.conf`。该文件顶部的第一条注释警告道：“此文件不应手动更新”。任何配置更改都应在 `/etc/gdm/gdm.conf-custom` 文件中进行。在 Gutsy Gibson 版本中，在 `/etc/gdm/factory-gdm.conf` 文件中甚至存在 `/etc/gdm/gdm.conf` 的备份。有关 `/etc/gdm` 目录中文件的更多信息，请参阅表 12-1。是的，此表中包含目录，但记住，在 Linux 中，该文件有一个特殊版本：

| 表 12-2 | 段 | 描述 |
| --- | --- | --- |
| 显示配置文件中的段 | `[daemon]` | 包含驱动显示管理器启动和响应错误的基本指令 |
| | `[security]` | 配置基础安全设置、可插身份验证模块 (PAM) |
| | `[xdcp]` | 设置远程访问显示管理器 |
| | `[gui]` | 根据 GIMP 工具包 (GTK+) 配置资源 |
| | `[greeter]` | 设置标题栏、窗口位置和浏览器，作为显示管理器操作的响应 |
| | `[chooser]` | 指定与 XDMCP 连接相关的设置 |
| | `[debug]` | 设置发送到系统日志的信息 |
| | `[servers]` | 配置显示如何运行；与之密切的是 `[server-Standard]`、`[server-Terminal]` 和 `[server-Chooser]` 段 |
| | `[customcommand]` | 留给自定义显示管理器命令 |

#### 设置显示管理器 437

有一些为普通用户和默认用户设置 `PATH` 环境变量的指令。这些指令不会覆盖任何特定用户的 `PATH` 默认值。注意，`RootPath` 变量的值可能会被截断，因为由于本书格式限制，它包含的目录比显示的更多。

`DefaultPath=/usr/local/bin:/usr/bin:/bin:/usr/bin/X11:/usr/games`

`RootPath=/usr/local/bin:/usr/local/sbin:/sbin:/usr/sbin:/bin:/usr/bin`

为了访问相关应用程序，以下指令提供了对 `gdm` 用户和组拥有脚本和文件的访问：

```
User=gdm
Group=gdm
```

以下指令运行 `/etc/gdm` 目录下的其他脚本。这些指令都指定了目录，并运行每个目录中名为 `Default` 的文件内容。

```
PostLoginScriptDir=/etc/gdm/PostLogin/
PreSessionScriptDir=/etc/gdm/PreSession/
PostSessionScriptDir=/etc/gdm/PostSession/
DisplayInitDir=/etc/gdm/Init
```

如果出现问题，`gdm` 守护进程通过以下指令引用 `BulletProofX` 文件：

```
FailsafeServer=/etc/gdm/failSafeXServer
```

即使 `BulletProofX` 文件无法工作，以下指令也会向用户提供消息：

```
XXKeepsCrashing=/etc/gdm/XXepsCrashing
```

假设硬件支持，左下角显示的 `Options` 按钮可以使用以下命令。然而，在示例中列出的 `hibernate` 命令可能只有在你在 GNOME 桌面点击 `System|Quit` 时，才在登录菜单中可用。

```
RebootCommand=/sbin/shutdown -r now "Rebooted via gdm."
HaltCommand=/sbin/shutdown -h now "Shut Down via gdm."
SuspendCommand=/usr/sbin/pmi action suspend
HibernateCommand=/usr/sbin/pmi action hibernate
```

#### 438 第 12 章：自定义 GNOME

下一个指令将这些指令与显示管理器中的实际命令关联：

```
SystemCommandsInMenu=HALT;REBOOT;SUSPEND;CUSTOM_CMD
```

类似的指令在注销过程中与显示管理器协同工作：

```
AllowLogoutActions=HALT;REBOOT;SUSPEND;CUSTOM_CMD
```

还有其他值得关注的指令，例如在 `[security]` `[servers]` 段落中。以下指令指定了 Xsession 脚本：

```
BaseXsession=/etc/gdm/Xsession
```

接下来的指令定义了默认 `.desktop` 配置文件，该文件运行用户特定的 X 客户端脚本：

```
DefaultSession=default.desktop
```

以下指令意味着你可以通过按下 `CTRL-ALT-F` 访问第一个 GNOME 显示管理器终端：

```
FirstVT=7
```

在我看来，禁用远程 root 访问（特别是自动登录）是非常重要的，这是通过 `[security]` 段落中的以下指令实现的：

```
AllowRemoteRoot=false
AllowRemoteAutoLogin=false
```

以下指令为 GNOME 管理器支持 PAM 认证：

```
PamStack=gdm
```

进一步的安全性相关指令与 `[xdmcp]` 段落关联。自然情况下，它默认是禁用的，应该只在安全的防火墙后面才启用：

```
Enable=false
```

登录次数应该受到限制，以尽量减少通过 GNOME 显示管理器遭受远程攻击的风险。以下限制了每个系统中 GNOME 显示器的器的数量。虽然以下指令是注释的，但它是默认值。值越大，遭受拒绝服务（DoS）攻击的风险越高。

```
#DisplaysPerHost=2
```

#### 设置显示管理器 439

另一个限制 GNOME 显示管理器读取的文件大小指令是 `UserMaxFile`。较大的文件可能需要 GNOME 显示管理器读取很长时间，这也增加了 DoS 攻击的风险。以下指令是默认值，单位为字节。

```
#UserMaxFile=65536
```

最后，以下指令设置了一个标准的图形控制台，部分基于之前的 `FirstVT` 指令。换句话说，它在可以通过按下 `CTRL-ALT-F7` 访问的控制台中设置了第一个 GNOME 显示管理器。

```
0=Standard device=/dev/console
```

可以设置更多的控制台；在本章最后的实验中提供了如何操作的示例。

### GUI 登录管理器自定义工具

要自定义 GNOME 登录管理器，你需要打开“登录窗口偏好”界面。在 GUI 中可以通过两种方式打开：要么通过 `system | Administration | Login Window`，要么运行 `sudo gdmset` 命令。Gutsy Gibbon 版本如图 12-1 所示。

- 登录窗口有六个标签页，支持非常详细的配置。旧版本的 Ubuntu Linux 没有那么多选项——预期的后版本的 Ubuntu Linux 将在“登录窗口偏好”工具中包含不同的功能。相对于 Hardy Heron 发布包含的版本已经有了修改。由于本章基于 Gutsy Gibbon 版本，请不要将其视为对该工具所能操作的精确或完整的描述。

### 通用登录窗口偏好

“通用” 标签页下的配置选项与用户看到的基本的登录选项有关。选项如下：

- *视觉反馈（星号）* 在“密码输入”中，对密码文本框中的每次按键都用星号做出响应。（Hardy Heron 版本的 GDM 设置工具将其重述为“在密码输入中隐藏视觉反馈”。）

#### 440 第 12 章：自定义 GNOME

图 2-I

GNOME

登录窗口偏好

![](img/8521db60567337b3b9ca1b288c5d36b6_458_0.png)

- **在密码输入中使用圆圈代替星号** 将每次按键的星号替换为深色圆圈。
