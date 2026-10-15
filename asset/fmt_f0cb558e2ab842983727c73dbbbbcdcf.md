
此条目表示 `init` 应以 `5` 作为参数执行文件 `/etc/rc.d/rc`。如果你查看文件 `/etc/rc.d/rc`，你会发现它是一个 shell 脚本文件。你可以研究文件 `/etc/rc.d/rc`，查看它如何为运行级别 1 到 5 启动各种进程。

回到图形登录界面的主题，`/etc/inittab` 文件的最后一行通过以下条目启动图形登录进程：

```
x:5:respawn:/etc/X11/prefdm -nodaeom
```

此命令运行 `/etc/X11/prefdm`，它是一个指向特定显示管理器的符号链接。对于 GNOME 图形桌面（Red Hat Linux 的默认选项），`/etc/X11/prefdm` 是 `/usr/bin/gdm`（GNOME 显示管理器）的符号链接。如果你使用 KDE 桌面作为默认选项，`/etc/X11/prefdm` 是 `/usr/bin/kdm`（KDE 显示管理器）的符号链接。这意味着无论你的 GUI 选择如何，`init` 都会在运行级别 5 启动显示管理器。显示管理器反过来显示图形登录对话框并使你能够登录到系统。

**如果你未在 Red Hat 安装过程中启用图形登录界面（见第 1 节），你现在可以通过编辑 `/etc/inittab` 文件来启用。找到包含 `in`default 的行，并确保其内容如下（两个冒号之间出现的运行级别应为 5）：**

```
id:5:initdefault:
```

在编辑 `/etc/inittab` 文件之前，你应该知道该文件中的任何错误都可能阻止 Red Hat Linux 启动到可以登录的阶段。如果你无法登录，你就无法使用你的系统。如下节所述，在你实际更改 `/etc/inittab` 文件中的默认运行级别之前，你始终可以使用 `init` 命令尝试特定的运行级别。

**切勿将 `in`default 设置为 0 或 6！如果你将 `default` 运行级别设置为 0，你的 Red Hat Linux 系统将启动，然后关机并停机。同样，将 `in`default 设置为 6 将导致系统每次启动时都重启。**

## 使用 init 命令试用新的运行级别

若要试用新的运行级别，您不一定非要更改 `/etc/inittab` 文件中的默认运行级别。如果您以 root 用户登录，可以使用 `init` 命令更改运行级别（从而更改 Linux 中运行的进程集合）。其格式如下：

```
init runlevel
```

在这里，`runlevel` 必须是单个字符，表示您想要达到的运行级别。例如，若要将系统置于单用户模式，请输入以下命令：

```
init 1
```

假设您的系统尚未设置为图形登录界面，如果您想在更改 `/etc/inittab` 文件的情况下试用运行级别 5，请在 shell 提示符下输入以下命令：

```
init 5
```

系统应该会终止所有当前进程并进入运行级别 5。默认情况下，`init` 命令在停止所有当前进程并启动运行级别 5 的新进程之前，会等待 20 秒。

![](img/5fe8f856723cde0b366f73584b9e64b8_249_0.png)

若要立即切换到运行级别 5，请输入命令 `init -t 5`。`-t` 选项后的数字表示 `init` 在更改运行级别前等待的秒数。

您还可以使用 `telinit` 命令，它只是 `init` 的一个符号链接。如果您对 `/etc/inittab` 文件进行了修改并希望 `init` 重新加载其配置文件，请使用命令 `telinit q`。

## 理解 Red Hat Linux 启动脚本

`init` 进程在系统启动时运行许多脚本。请注意 `/etc/inittab` 文件开头附近的以下行：

```
# System initialization.
si::sysinit:/etc/rc.d/rc.sysinit
```

如第一行注释所示，第二行使 `init` 运行 `/etc/rc.d/rc.sysinit` 脚本，这是 `init` 运行的第一个 Red Hat Linux 启动脚本。`rc.sysinit` 脚本执行许多初始化任务，例如挂载文件系统、设置时钟、配置键盘布局、启动网络以及加载许多其他驱动模块。`rc.sysinit` 脚本通过调用许多其他脚本并读取位于 `/etc/sysconfig` 目录中的配置文件来执行这些初始化任务。

在执行完 `/etc/rc.d/rc.sysinit` 脚本后，`init` 进程将使用运行级别作为参数运行 `/etc/rc.d/rc` 脚本。例如，对于运行级别 5，`/etc/inittab` 中的以下行指定了 `init` 必须执行的内容：

```
::5:wait:/etc/rc.d/rc 5
```

这意味着 `init` 应该执行命令 `/etc/rc.d/rc 5`，并等待该命令完成。

`/etc/rc.d/rc` 脚本有点复杂。它是这样工作的：

- 它更改到与运行级别对应的目录。例如，要切换到运行级别 5，脚本会更改到 `/etc/rc.d/rc5.d` 目录。
- 在与运行级别对应的目录中，它查找所有以 K 开头的文件，并使用 `stop` 参数执行每一个文件。这会终止当前正在运行的进程。然后它查找所有以 S 开头的文件，并使用 `start` 参数执行每个文件。这将启动指定运行级别所需的进程。

若要查看在运行级别 5 下执行了哪些内容，请输入命令 `ls -l /etc/rc.d/rc5.d`。输出如下所示，由于具有重复性，此处进行了截断：

```
ls -l /etc/rc.d/rc5.d
total 0
lrwxwxwxwx    1 root     root    15 Aug 14 16:24 K01pppoe -> ../init.d/pppoe
lrwxwxwxwx    1 root     root    14 Aug 14 16:08 K05snd -> ../init.d/sound
lrwxwxwxwx    1 root     root    13 Aug 19 22:18 K20nfs -> ../init.d/nfs
lrwxwxwxwx    1 root     root    16 Aug 14 16:24 K20rstatd -> ../init.d/rstatd
lrwxwxwxwx    1 root     root    17 Aug 14 16:24 K20ruserd -> ../init.d/ruserd
lrwxwxwxwx    1 root     root    16 Aug 14 16:24 K20rwalld -> ../init.d/rwalld
lrwxwxwxwx    1 root     root    16 Aug 14 16:24 K20rwhod -> ../init.d/rwhod
...part of listing deleted...
...
.
.
.
lrwxwxwxwx    1 root     root    14 Aug 14 16:24 S80sendmail -> ../init.d/sendmail
lrwxwxwxwx    1 root     root    13 Aug 14 16:07 S85gpm -> ../init.d/gpm
lrwxwxwxwx    1 root     root    15 Aug 14 15:58 S85httpd -> ../init.d/httpd
lrwxwxwxwx    1 root     root    13 Aug 14 15:58 S90x -> ../init.d/xfs
lrwxwxwxwx    1 root     root    17 Aug 14 15:55 S95anacron -> ../init.d/anacron
lrwxwxwxwx    1 root     root    19 Aug 14 16:16 S99initscripts -> ../init.d/initscripts
lrwxwxwxwx    1 root     root    11 Aug 14 15:56 S99local -> ../rc.local
```

输出显示，所有以 K 和 S 开头的文件都是指向位于 `/etc/rc.d` 和 `/etc/init.d` 目录中的脚本的符号链接。实际上，`/etc/rc.d/rc` 脚本严格按照目录列表中出现的顺序执行这些文件。

> 请注意，目录列表中的最后一个文件是指向 `../rc.local` 脚本的符号链接。这意味着 `/etc/rc.d/rc.local` 在所有其他脚本之后执行。因此，您可以在此脚本中放置任何希望在 Linux 系统每次启动时执行的命令。

大多数启动脚本位于 `/etc/rc.d/init.d` 目录中。您可以手动调用此目录中的脚本来启动、停止或重启特定进程——通常是服务器。例如，若要停止 Web 服务器，请输入以下命令：

```
/etc/rc.d/init.d/httpd stop
Shutting down httpd: [  OK  ]
```

您可以通过熟悉 `/etc/rc.d/init.d` 目录中的脚本来提高系统管理技能。若要查看列表，请输入以下命令：
