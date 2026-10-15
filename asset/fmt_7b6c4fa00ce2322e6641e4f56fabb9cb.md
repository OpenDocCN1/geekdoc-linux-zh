
`x:5:respawn:/etc/init/prefdm -nodaemon`

以井号 (`#`) 开头的行是注释。`/etc/inittab` 文件中的第一行非注释行如下所示指定默认运行级别：

`id:5:initdefault:`

尽管你不知道 `/etc/inittab` 文件的语法（你真的不需要学习它），但你也可以通过查看示例来猜测它。`/etc/inittab` 文件中的每行都由冒号分隔的四个字段组成：`id:runlevel:action:process`。

第一个字段是条目的标识符。第二个字段是该条目应用的运行级别。第三个字段是动作，告诉 `init` 要做什么。第四个字段是要执行的命令或脚本。

常见动作包括：

- `initdefault`: 设置默认运行级别。
- `sysinit`: 在启动时运行一次进程。
- `wait`: 运行进程并等待其完成。
- `respawn`: 运行进程并在终止时重启。
- `ctrlaltdel`: 在按下 Ctrl-Alt-Del 时运行进程。
- `powerfail`: 在断电时运行进程。
- `powerokwait`: 在恢复电源时运行进程。
- `mingetty`: 在 TTY 上运行 getty 进程。
- `xdm`: 启动 X 显示管理器。

下表总结了 `/etc/inittab` 中可能的动作：

| 动作 | 描述 |
| :--- | :--- |
| initdefault | 设置默认运行级别 |
| sysinit | 在系统初始化期间运行一次进程 |
| wait | 运行进程并等待其完成 |
| respawn | 运行进程并在终止时重启它 |
| ctrlaltdel | 在按下 Ctrl-Alt-Del 时运行进程 |
| powerfail | 在断电时运行进程 |
| powerokwait | 在恢复电源运行时进程 |
| mingetty | 在 TTY 上运行 getty 进程 |
| xdm | 启动 X 显示管理器 |

以下是您的 Red Hat Linux 系统上 `/etc/inittab` 文件的列出，该文件配置为图形登录界面：

+ - inittab 此文件描述了 INIT 进程应如何在特定运行级别下设置系统。
- Author: Miquel van Smoorenburg, <miquel@drinking.nl.org> Marc Ewing 和 Donnie Barnes 为 RHS Linux 修改
+ # 默认运行级别。RHS 使用的运行级别为：
# 0 halt（不要将 initdefault 设置为此级别）
# 1 单用户模式
# 2 多用户模式，不带 NFS（如果没有网络，则与 3 相同）
# 3 完整多用户模式
# 4 未使用
# 5 GUI
# 6 reboot 重启（不要将 initdefault 设置为此级别）
`id:5:initdefault:`
+ # 系统初始化。
`si::sysinit:/etc/rc.d/rc.sysinit`
`10:wait:/etc/rc.d/rc 0`
`11:wait:/etc/rc.d/rc 1`
`12:wait:/etc/rc.d/rc 2`
`13:wait:/etc/rc.d/rc 3`
`14:wait:/etc/rc.d/rc 4`
`15:wait:/etc/rc.d/rc 5`
`16:wait:/etc/rc.d/rc 6`
+ # 捕捉 CLR-ALT-DELETE
`ca::ctrlaltdel:/sbin/shutdown -t3 -r now`
+ # 当我们的 UPS 我们断电时，假设我们还有几分钟电源。安排在 2 分钟后关机。
# 当然，这假设你已经安装了电源并且你的
# UPS 连接并正常工作。
`p:powerfail:/sbin/shutdown -f -h +2 "Power Failure: System Shutting Down"`
+ # 如果关机触发之前恢复了电源，则取消。
`pr:12345:powerokwait:/sbin/shutdown -c "Power Restored, Shutdown Cancelled"`
+ # 在运行级别中运行 gettys
`1:2345:respawn:/sbin/mingetty tty1`
`2:2345:respawn:/sbin/mingetty tty2`
`3:2345:respawn:/sbin/mingetty tty3`
`4:2345:respawn:/sbin/mingetty tty4`
`5:2345:respawn:/sbin/mingetty tty5`
`6:2345:respawn:/sbin/mingetty tty6`
+ # 在运行级别 5 中运行 xdm
# xdm 现在是一个独立的服务
`x:5:respawn:/etc/init/prefdm -nodaemon`

以井号 (`#`) 开头的行是注释。`/etc/inittab` 文件中的第一行非注释行如下所示指定默认运行级别：

`id:5:initdefault:`

尽管你不知道 `/etc/inittab` 文件的语法（你真的不需要学习它），但你也可以通过查看示例来猜测它。`/etc/inittab` 文件中的每行都由冒号分隔的四个字段组成：`id:runlevel:action:process`。

第一个字段是条目的标识符。第二个字段是该条目应用的运行级别。第三个字段是动作，告诉 `init` 要做什么。第四个字段是要执行的命令或脚本。

常见动作包括：

- `initdefault`: 设置默认运行级别。
- `sysinit`: 在启动时运行一次进程。
- `wait`: 运行进程并等待其完成。
- `respawn`: 运行进程并在终止时重启。
- `ctrlaltdel`: 在按下 Ctrl-Alt-Del 时运行进程。
- `powerfail`: 在断电时运行进程。
- `powerokwait`: 在恢复电源时运行进程。
- `mingetty`: 在 TTY 上运行 getty 进程。
- `xdm`: 启动 X 显示管理器。

下表总结了 `/etc/inittab` 中可用的动作：

| 动作 | 描述 |
| :--- | :--- |
| initdefault | 设置默认运行级别 |
| sysinit | 在系统初始化期间运行一次进程 |
| wait | 运行进程并等待其完成 |
| respawn | 运行进程并在终止时重启它 |
| ctrlaltdel | 在按下 Ctrl-Alt-Del 时运行进程 |
| powerfail | 在断电时运行进程 |
| powerokwait | 在恢复电源运行时进程 |
| mingetty | 在 TTY 上运行 getty 进程 |
| xdm | 启动 X 显示管理器 |

## 第 20 章：高级系统管理

如果你在安装 Red Hat 过程中没有启用图形化登录界面（第 2 章中介绍过），可以通过编辑 `/etc/inittab` 文件来实现。找到包含 `initdefault` 的行，并确保其内容如下所示（两列之间显示的运行级别为 5）：

注意

```
id:5:initdefault:
```

在编辑 `/etc/inittab` 文件之前，你应该知道，该文件中的任何错误都可能导致 Red Hat Linux 无法启动到允许你登录的程度。如果你无法登录，就无法使用你的系统。在实际通过编辑 `/etc/inittab` 文件更改默认运行级别之前，你应该始终尝试使用 `init` 命令进入特定的特定的运行级别。如果 `/etc/inittab` 文件出现错误，你可以输入 `init 1` 进入单用户模式，然后编辑该文件以纠正错误。

### 使用 init 命令尝试新的运行级别

要尝试新的运行级别，你不需要更改 `/etc/inittab` 文件中的默认运行级别。如果你以 root 身份登录，可以使用 `init` 命令更改运行级别（随之改变的是 Red Linux 中运行的进程），其格式如下：

```
init runlevel
```

在这里，`runlevel` 必须是表示你想要运行层的单个字符。例如，要将系统置于单用户模式，请输入：

```
init 1
```

因此，如果你想在不更改 `/etc/inittab` 文件的情况下尝试运行级别 5（假设你的系统没有设置图形化登录界面），请在 shell 提示符输入以下命令：

```
init 5
```

系统应该结束所有当前进程并进入运行级别 5。默认情况下，`init` 命令会在等待 20 秒后停止所有当前进程并启动运行级别 5 的新进程。

内部见

要立即切换到运行级别 5，输入命令 `init -t 0.5`。`-t` 选项后的数字表示 init 在更改运行级别之前等待的秒数。

你也可以使用 `telinit` 命令，它是 `init` 的符号链接。如果你更改了 `/etc/inittab` 文件并希望 init 重新加载其配置文件，请使用命令 `telinit q`。

### 了解 Red Hat Linux
