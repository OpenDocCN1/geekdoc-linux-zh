
| :--- | :--- | :--- | :--- | :--- |
| root rwxrxr-x | root | 4月28 06:01 | K10xdm | ..xdm |
| root rwxrxr-x | root | 4月28 06:01 | K19cron | ..cron |
| root rwxrxr-x | root | 4月28 06:01 | K19ident | ..ident |
| root rwxrxr-x | root | 4月28 06:01 | K19nscd | ..nscd |
| root rwxrxr-x | root | 4月28 06:04 | K20apache | ..apache |
| root rwxrxr-x | root | 4月28 06:02 | K20apm | ..apmd |
| root rwxrxr-x | root | 4月28 06:02 | K20at | ..at |
| root rwxrxr-x | root | 4月28 06:01 | K20inet | ..inet |
| root rwxrxr-x | root | 4月28 06:01 | S01kernel | ..kernel |
| root rwxrxr-x | root | 4月28 06:01 | S02serial | ..serial |
| root rwxrxr-x | root | 4月28 06:04 | S03hardware | ..hardware |
| root rwxrxr-x | root | 4月28 06:04 | S04dummy | ..dummy |
| root rwxrxr-x | root | 4月28 06:01 | S05dhclient | ..dhclient |
| root rwxrxr-x | root | 4月28 06:01 | S05network | ..network |

# 第二章：启动和关机过程

注意来自 `/etc/rc.d/rc3.d` 的脚本以两种方式链接。

某些脚本链接为：

`K[两位数字][脚本名]`

其他脚本链接为：

`S[两位数字][脚本名]`

所有以字母 "K" 开头的脚本都带有 `stop` 参数运行，所有以字母 "S" 开头的脚本都带有 `start` 参数运行。两位数字用于设置执行顺序。因此，一个名为 `S01foo` 的脚本将在 `S10bar` 之前运行。“S”脚本和“K”脚本脚本由 `/etc/rc.d/rc` 脚本运行。

一旦 `rc` 脚本完成，它所执行的处理也随之结束。系统现在相应的运行级别可用。

## 启动你的系统

在启动过程中，`init` 将首先运行 `rc.sysinit` 脚本，然后运行默认运行级别的脚本。默认运行级别在 `/etc/inittab` 中通过如下行设置：

```
id:2:initdefault:
```

在这里，默认运行级别被设置为 2。这意味着 `init` 将运行将系统设置为多用户模式所需的脚本。

如果你再次查看列表 2-2，你会注意到以下内容指定了运行级别 2 需要运行的内容：

```
12:2:wait:/sbin/init.d/rc 2
```

`rc` 脚本带有参数 `2` 运行。如前所述，该脚本将运行 `/etc/rc.d/rc2.d` 中所有以 "S" 开头的脚本。

`rc` 脚本还将 `start` 作为参数提供给每个“S”脚本。当所有“S”脚本运行时`rc` 脚本将完成，系统将在默认运行级别可用。

你可以在 LILO 提示符处覆盖默认运行级别。如果你想以单用户模式启动系统，可以指定 `linux single`。如果你使用非 "linux" 的标签启动 Linux，你将必须指定 `yourlabel single`，其中 `yourlabel` 是相应标签的名称。

## 第一部分：安装和开始使用 SuSE Linux

现在让我们来看看系统关机期间 `init` 是如何工作的。

## 关闭你的系统

你可以手动运行 `init`，通过在命令行提供所需的运行级别来告诉 `init` 更改系统运行级别。例如：

```
init 1
```

这将停止 `init` 并将当前运行级别更改为 1。换句话说，这将停止系统。如果你正在多用户模式（运行级别 3）下运行，上述命令不如其他命令理想，因为它不会通知系统上的用户系统即将关机。

或者，你可以输入以下命令：

```
halt
```

通常情况下，`shutdown` 命令用于关闭系统。它会向所有登录的用户广播警告消息，告知系统正在更改运行级别。`shutdown` 命令还提供了一个用于调度关机事件的选项。

`shutdown` 命令的工作原理是告诉 `init` 将系统的当前运行级别更改为停止（0）或重启（6）。例如：

```
shutdown -h now
```

此命令将信号 `init` 立即将运行级别改为 0。

## 取消关机

`shutdown` 命令还允许你调度在稍后时间执行关机事件。例如：

```
shutdown 10
```

将在 shell 提示符输入该命令恰好 10 分钟后执行关机。你还可以按照如下方式向所有登录系统的用户发送消息：

```
shutdown 10 "chivas is being shutdown for system maintenance"
```

## 第二章：启动和关机过程

如果需要取消关机事件，可以执行带有 `-c` 选项的另一个 `shutdown` 命令。例如：

```
shutdown -c
```

这将取消任何已调度的关机事件。

## 重启服务器

你也可以手动运行 `init` 来重启服务器。例如，你可以输入以下命令：

```
init 6
```

当你在多用户模式（运行级别 2 或以上）运行时，此命令不是最佳方法，因为它不会通知系统上的用户系统即将重启。相反，你可以使用 `shutdown` 命令重启服务器，如：

```
shutdown -r +10
```

这将在 10 分钟后重启服务器。所有用户将收到一条消息，告知系统即将重启，这将让他们能够完成并保存工作。如果用户正在运行重要进程并需要时间注销，它还允许你取消关机。

![](img/1d90939eac39ca761233542e5471_74.png)

当你使用上述的延迟 `shutdown` 命令时，登录的用户将看到广播消息，告知系统即将重启。为了阻止新登录，你可以创建一个 `/etc/nologin` 文件，并说明关机已调度，人们应稍后尝试登录。重启后不要忘记。如果你正在远程重启服务器，请确保在实际关机之前删除或重命名此文件。当此文件存在时，不允许普通用户登录。事实上，你可能想在 `/etc/rc.local` 脚本末尾添加 `rm -f /etc/nologin`，确保在运行级别 2 结束时由 `init` 执行。要立即重启，可以运行以下命令：

```
shutdown -r now
```

## Ctrl+Alt+Del 重启

如果你在系统控制台上，可以使用传统的 Ctrl+Alt+Del 组合键重启系统。这是由于 `/etc/inittab` 中的以下行实现的：

```
ca::altdel:/sbin/shutdown -r 4 now
```

此行允许 `init` 捕获 Ctrl+Alt+Del 组合键并立即调用 `shutdown` 脚本。

![](img/1d90939eac39ca761233542e5471_75.png)

任何物理访问系统控制台的人都可以通过 Ctrl+Alt+Del 键关闭系统。为了防止此类关机，你可以创建一个名为 `/etc/shutdown.allow` 的文件，其中包含允许关闭系统的用户列表（每行一个用户名）。root 账户不需要列在该文件中。

## 断电时的自动关机

如果你使用 UPS 为系统提供备份电源，当 UPS 电量耗尽时，可以使用 `init` 安全地关闭系统。`/etc/inittab` 包含以下行：

```
pf::powerwait:/sbin/init.d/powerfail
np::powerfail:/sbin/init.d/powerfail now
#pn::powerfail:/sbin/init.d/powerfail now
```

这些行告诉 `init` 在断电情况下运行 `powerfail` 脚本。当 UPS 向 `init` 发送 SIGPWR 信号时，会激活 `powerfail` 操作。默认设置 `--powerfail start` 防止用户在系统关机时登录。`powerfail` 选项立即关机。

由于在 UPS 电量耗尽之前电力恢复是可能的，可以调用 `init` 取消之前调度的关机事件。这是通过以下行实现的：`po::powerwait:/sbin/init.d/powerfail`

当 UPS 向 `init` 发送 SIGPWR 信号时，会激活 `powerfail` 操作。默认设置 `--powerfail start` 防止用户在系统关机时登录。`powerfail` 选项立即关机。

## 第二章：启动和关机过程

## 管理文件
