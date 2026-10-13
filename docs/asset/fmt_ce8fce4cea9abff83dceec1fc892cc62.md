
即使你不知道 `/etc/inittab` 文件的语法（而且你真的不必学习语法），你大概也能猜出该行中的 `5` 表示图形登录屏幕的默认运行级别。因此，如果你希望系统在启动后以级别 `3` 运行（用于纯文本模式登录屏幕），你只需将 `5` 改为 `3` 即可。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_277_0.png)

输入 `man inittab` 以查看 `inittab` 文件中条目的详细语法。

关于 `/etc/inittab` 文件的文件格式，`/etc/inittab` 文件中的每个条目都指定 `init` 应在一个或多个指定运行级别启动的进程。你只需列出该进程应运行的所有运行级别。`inittab` 文件中的每个条目都有四个字段——以冒号分隔——格式如下：

```
id:runlevels:action:process
```

各字段含义如下：

- `id` 字段是一个唯一的、一到两个字符的标识符。`init` 进程在内部使用此字段。你可以使用任何标识符，只要不在多行中使用相同的标识符即可。例如，`si`、`x` 和 `1` 都是有效的标识符。
- `runlevels` 字段是一串零个或多个字符，每个字符表示一个运行级别。例如，标识符为 `1` 的行适用于 1 到 5 的运行级别，因此该条目的 `runlevels` 字段为 `12345`。如果 `action` 字段设置为 `sysinit`、`boot` 或 `bootwait`，则忽略此字段。
- `action` 字段告诉 `init` 进程对该特定条目执行什么操作。例如，如果此字段为 `initdefault`，`init` 将 `runlevels` 字段解释为默认运行级别。如果此字段设置为 `wait`，`init` 启动 `process` 字段指定的进程并等待该进程退出。表 22-1 总结了可在 `action` 字段中使用的有效动作值。
- `process` 字段指定 `init` 需要启动的进程。当然，`action` 字段的某些设置不需要 process 字段。（例如，当 `action` 设置为 `initdefault` 时，不需要 `process` 字段。）

### 表 22-1 /etc/inittab 中的有效动作

| 动作 | 描述 |
|---|---|
| respawn | 只要进程终止就重新启动该进程。 |
| wait | 在指定的运行级别启动进程一次；`init` 等待该进程退出。 |
| once | 在指定的运行级别执行一次进程。 |
| boot | 系统启动时执行进程，无论运行级别如何（`runlevels` 字段被忽略）。 |
| bootwait | 系统启动时执行进程；`init` 等待进程退出（`runlevels` 字段被忽略）。 |
| off | 此动作不执行任何操作。 |

### 表 22-1 继续

| 动作 | 描述 |
|---|---|
| ondemand | 在指定的运行级别执行进程，该运行级别必须是 a、b 或 c 之一。 |
| initdefault | 系统启动后在此运行级别启动系统。此动作忽略 `process` 字段。 |
| sysinit | 系统启动时执行进程，在具有 boot 或 bootwait 动作的任何条目之前（`runlevels` 字段被忽略）。 |
| powerwait | 当 `init` 接收到指示电源出现问题的 SIGPWR 信号时执行进程。然后 `init` 等待进程退出。 |
| powerfail | 与 powerwait 类似，只是 `init` 不等待进程退出。 |
| powerokwait | 当 `init` 接收到 SIGPWR 信号且 `/etc/powerstatus` 文件包含单词 OK（表示电源已恢复）时执行进程。 |
| ctrlaltdel | 当 `init` 接收到 SIGINT 信号时执行进程，该信号在按下 Ctrl+Alt+Del 时发生。通常，`process` 字段应指定带有 -r 选项的 `/sbin/shutdown` 命令以重新启动 PC。 |
| kbdrequest | 当 `init` 从键盘驱动程序接收到特殊键组合已被按下的信号时执行进程。键组合应映射到 keymap 文件中的 KeyboardSignal。 |

`process` 字段通常以 shell 脚本的形式指定，而该脚本又可以启动多个进程。例如，`15` 条目指定如下：

```
15:5:wait:/etc/rc.d/rc 5
```

该条目指定 `init` 应使用 `5` 作为参数执行文件 `/etc/rc.d/rc`。如果查看文件 `/etc/rc.d/rc`，你会发现它是一个 shell 脚本文件。你可以研究文件 `/etc/rc.d/rc`，以了解它如何为 1 到 5 的运行级别启动各种进程。

回到图形登录屏幕主题，`/etc/inittab` 文件的最后一行使用以下条目启动图形登录进程：

```
x:5:respawn:/etc/X11/prefdm -nodaemon
```

该命令运行 `/etc/X11/prefdm`，它是到特定显示管理器的符号链接。对于 GNOME 图形桌面（Red Hat Linux 中的默认设置），`/etc/X11/prefdm` 是指向 `/usr/bin/gdm` 的符号链接——GNOME 显示管理器。如果你使用 KDE 桌面作为默认桌面，`/etc/X11/prefdm` 是指向 `/usr/bin/kdm` 的符号链接——KDE 显示管理器。这意味着无论你选择哪种 GUI，`init` 在运行级别 `5` 启动显示管理器。显示管理器进而显示图形登录对话框并允许你登录系统。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_280_0.png)

如果你在 Red Hat 安装期间未启用图形登录屏幕（在第 1 至 3 节中介绍），你可以通过编辑 `/etc/inittab` 文件来启用。找到包含 `initdefault` 的行并确保其如下所示（两个冒号之间的运行级别应为 `5`）：

```
id:5:initdefault:
```

在编辑 `/etc/inittab` 文件之前，你应该知道该文件中的任何错误都可能阻止 Red Hat Linux 启动到可以登录的程度。如果无法登录，你就无法使用系统。如我接下来所解释的，你可以在实际更改 `/etc/inittab` 文件中的默认运行级别之前，始终使用 `init` 命令尝试特定的运行级别。

## 使用 init 命令尝试新的运行级别

要尝试新的运行级别，你不一定需要更改 `/etc/inittab` 文件中的默认运行级别。如果你以 root 身份登录，可以使用 `init` 命令更改运行级别（从而更改 Linux 中运行的进程集）。其格式如下：

```
init runlevel
```

这里，`runlevel` 必须是一个字符，表示你想要的运行级别。例如，要将系统置于单用户模式，输入以下内容：

```
init 1
```

因此，如果你想尝试运行级别 `5`（假设你的系统尚未设置图形登录界面），而不更改 `/etc/inittab` 文件，请在 shell 提示符下输入以下命令：

```
init 5
```

系统应结束所有当前进程并进入运行级别 `5`。默认情况下，`init` 命令会在停止所有当前进程并启动运行级别 `5` 的新进程之前等待 20 秒。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_281_0.png)

要立即切换到运行级别 `5`，请键入命令 `init -t0 5`。`-t` 选项后的数字表示 `init` 在更改运行级别之前等待的秒数。

你也可以使用 `telinit` 命令，它只是指向 `init` 的符号链接。如果你对 `/etc/inittab` 文件进行了更改并希望 `init` 重新加载其配置文件，请使用命令 `telinit q`。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_281_1.png)

## 了解 Red Hat Linux 启动脚本

`init` 进程在系统启动时运行多个脚本。请注意以下出现在 `/etc/inittab` 文件开头的几行：

```
# System initialization.

si::sysinit:/etc/rc.d/rc.sysinit
```

正如第一行的注释所示，第二行会导致 `init` 运行 `/etc/rc.d/rc.sysinit` 脚本——`init` 运行的第一个 Red Hat Linux 启动脚本。`rc.sysinit` 脚本执行许多初始化任务，例如挂载文件系统、设置时钟、配置键盘布局、启动网络以及加载许多其他驱动模块。`rc.sysinit` 脚本通过调用其他多个脚本并读取位于 `/etc/sysconfig` 目录中的配置文件来执行这些初始化任务。

执行完 `/etc/rc.d/rc.sysinit` 脚本后，`init` 进程会使用运行级别作为参数运行 `/etc/rc.d/rc` 脚本。例如，对于运行级别 `5`，`/etc/inittab` 中的以下行指定了 `init` 需要执行的内容：

```
l5:5:wait:/etc/rc.d/rc 5
```
