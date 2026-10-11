
# `/sbin/clock --help`

```
#/sbin/clock --help

/sbin/clock: unrecognized option '-help'

`clock` [-u] -r|w|s|a|v

r: read and print CMOS clock

w: write CMOS clock from system time

s: set system time from CMOS clock

a: get system time and adjust CMOS clock

u: CMOS clock is in universal time

v: print version (1.4) and exit
```

此命令位于 `/sbin` 目录下，不应与 OpenWindows `clock` 客户端混淆，后者在 X 会话期间显示当前时间的图形时钟。`/sbin/clock` 命令应仅由 root 操作员运行（root 应使用完整路径显式调用 `clock`）。可以使用其 `s` 选项将此命令用于显示并同步计算机的硬件时钟与 Linux 系统时钟。要将系统时间调整到硬件时钟，请使用 `s` 选项。

如果你使用基于 Red Hat 的发行版，如 Yellow Dog Linux 或 LinuxPPC 2000，你也可以使用 Red Hat 的 `timetool` 客户端来设置系统时间。此 X11 客户端可以从 X11 终端窗口的命令行启动，如下所示：

```
# timetool &
```

按回车键后，你会看到一个窗口，如图 3.1 所示。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_67_0.png)

基于 Red Hat 的 Linux 使用名为 `/etc/localtime` 的符号链接来指定你当前的时区。在 SuSE Linux 中，这是从系统时区数据库生成的二进制文件。在 SuSE Linux 中，可以通过编辑其系统-wide 配置文件 `/etc/rc.config` 来设置时区。查找以下条目：

```
TIMEZONE=EST
```

进行更改后，请确保运行 SuSE 的 `suseconfig` shell 脚本以实施你的更改。

SuSE Linux 还提供了一种基于控制台的综合系统管理工具，名为 `yast`，以及一个更新的用于 X11 的图形版本，名为 `yast2`。当你使用 `yast` 命令时，可以使用其 `--mask` 选项直接跳转到特定的管理任务，后跟诸如 backup、consolefont、gpm、help、keymap、modem、mouse、netprinter、printer、scanner、timezone、user 或 vfree 等关键字。要直接跳转到简单的时区配置，请使用 `yast`，如下所示：`yast --mask timezone`。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_67_1.png)

使用 KDE 的系统管理员可以使用 `kcmclock` 客户端来设置时间并指定时区。从 X11 终端窗口的命令行启动客户端，如下所示：

```
# kcmclock &
```

当客户端启动时，点击对话框中的时区选项卡，如图 3.2 所示。

点击下拉 GMT 菜单并选择你的时区（作为相对于 GMT 的偏移量）。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_68_0.png)

> 图 3.2 KDE 的 `kcmclock` 客户端用于设置您的时区。

你也可以通过创建或修改 `TZ` 环境变量来即时设置时区，这是一个内存设置，用于指定当前时区（详情请参阅 `tzset` 手册页）。

你也可以通过使用 `rdate` 命令及其 `-s` 或 `set` 选项，通过互联网更新系统时间。此命令只能由 root 操作员运行，并且应与互联网时间服务器的名称一起使用，例如：

```
# rdate -s tick.usno.navy.mil
```

此命令通过从指定的远程服务器获取时间来设置你的 Linux 系统时间。

> 不幸的是，SuSE Linux PPC 不包含 `rdate` 命令。但是，你可以从互联网下载、编译并安装这个小巧的工具的源代码。

## 添加用户

在 Linux 系统上管理用户是系统管理员的工作。但如果你在独立的台式机上使用 Linux，你就是系统管理员！你的首要任务之一是为自己创建一个用户名和密码，因为你不应作为 root 操作员使用 Linux（除非正在执行救援操作或系统维护）。

基于 Red Hat 的 Linux 系统包含多种图形界面和命令行工具，用于创建和管理用户。SuSE Linux 管理员可以使用图形化的 `yast` 实用程序或其他命令行工具。从命令行创建用户既轻松又简单，而且可能比使用图形工具更快。

在所有 Linux 系统中常用的 Linux 用户创建程序是 `useradd` 命令。如果你有一个名为 Fred Smith 的用户，那么使用 `useradd` 命令，如下所示：

```
# useradd fsmith
```

接下来，你应该使用 `passwd` 命令为新用户分配一个默认密码，如下所示：

```
# passwd fsmith
New password:
Re-enter new password:
Password changed
```

新用户“fsmith”现在将拥有一个名为 `/home/fsmith` 的目录，在 `/etc/passwd` 中指定的登录 Shell，以及一个新密码。

> 你拥有一个大型系统，或者需要创建数百个新用户？使用 `newusers` 命令，它使用包含新用户和密码列表的文件。有关更多信息，请参阅 `newusers` 手册页。

### 使用 userconf

许多基于 Red Hat 的 Linux 系统（如 LinuxPPC 2000 和 Yellow Dog Linux）中包含的 `linuxconf` 客户端的 `userconf` 组件可用于创建新用户。从命令行（作为 root）启动客户端，如下所示：

```
# userconf &
```

按下 Enter 键后，点击主窗口上的 **User accounts** 按钮。会出现一个新的对话框。点击 **Add** 按钮，你将看到如图 3.3 所示的对话框。

输入新用户的登录名和全名。其他设置可以留空，因为 `userconf` 将使用系统默认值。完成后，点击 **Accept** 按钮创建新用户。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_69_0.png)

### 使用 yast

SuSE Linux 的 `yast` 命令可用于创建新用户。从命令行（作为 root）启动该命令，如下所示：

```
# yast -mask user
```

按下 Enter 键后，你会看到如图 3.4 所示的对话框。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_70_1.png)

### 使用 `passwd` 命令

正如你已了解的那样，`passwd` 命令用于创建或更改用户的密码。如果你负责一个大型 Linux 安装环境，拥有众多用户，并希望实施更多安全措施，你可以采用一种称为 `密码过期` 或 `密码老化` 的技术。这对于合同员工或临时用户也是一种有效的技术。当你强制执行 `过期` 时，用户在预设时间后必须更新或更改密码。你还可以为临时账户强制执行实际的用户过期。

对于基于 Red Hat 的 Linux 系统，再次使用 `userconf` 命令（作为 root），如下所示：

```
# userconf &
```

导航到用户对话框（如图 3.3 所示），并点击 Params 选项卡。你会看到如图 3.5 所示的用户信息选项卡。

使用此选项卡设置密码必须更改的天数、用户账户的有效期限、何时发送即将过期的警告，以及警告发出后账户或密码的有效时长。

SuSE Linux 管理员可以转向 `yast` 命令的用户对话框（如图 3.4 所示）。但是，在输入用户名时，你必须按下 F6 键。你会看到如图 3.6 所示的对话框。

使用此对话框，以类似的方式操作 `userconf` 的控制。完成后，使用 Tab 键突出显示 Continue 按钮，以返回用户配置。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_71_0.png)

**图 3.5** 使用 `userconf` 设置密码过期。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_72_0.png)

图 3.6 SuSE 的 `yast` 命令功能包括一个带有密码过期的对话框，有助于确保系统获得额外的安全性。

## 网络配置

使用 Linux 创建网络接口（参见第 9 章“连接互联网”）相对容易，肯定不会像其他商业操作系统那样涉及多个机器人。就像 Mac OS 一样，一旦你的内部硬件（如网络接口）被识别，你就可以设置你的 Power Mac 运行 Linux。这允许你在 30 秒内成为 LAN 的成员。
