
# inittab This file describes how the INIT process should set up
# the system in a certain run level.
.
.
.
id:5:initdefault:

# System initialization.
si:sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

# Trap CTRL-ALT-DELETE
ca:2:ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have a few minutes
# of power left.  Schedule a shutdown for 2 minutes from now.
# This does, of course, assume you have powerd installed and your
# UPS connected and working correctly.
pf:powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"

# If power was restored before the shutdown kicked in, cancel it.
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

# Run getty in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# Run xdm in runlevel 5
x:5:once:/etc/X11/prefdm -nodemand

纯文本的 `init tab` 文件由几个以冒号分隔的字段组成，格式如下：

```text
id:runlevels:action:command
```

`id` 字段是一个唯一的标识符，长度为一到四个字母数字字符，代表系统启动期间要采取的一个特定操作。`runlevels` 字段包含将在其中运行命令的运行级别列表。常见的运行级别是 0、1、2、3、4、5 和 6（s 和 S 代表单用户模式，等同于 1）。运行级别 7、8 和 9 也可以用作与 on-demand 操作关联的特殊运行级别（a、b 和 c，分别等同于 A、B 和 C）。下一个字段代表 `init` 要采取的操作类型（有效的操作及其结果列于表 11-3 中），最后一个字段是要执行的实际命令。

### 表 11-3：有效的 init 操作

| 操作 | 命令运行方式 |
| :--- | :--- |
| once | 进入指定运行级别时执行一次命令。 |
| wait | 与 `once` 相同，但 `init` 会等待命令完成，然后再继续处理其他 inittab 条目。 |
| respawn | 监控该进程，如果原始进程终止，则启动一个新实例。 |
| powerfail | 在接收到来自通用电源（UPS）单元关联软件的 SIGPWR 信号时执行命令。这假设还有几分钟的电力，因此默认情况下，系统可以在两分钟内关闭系统。 |
| powerwait | 与 powerfail 相同，但 init 会等待命令完成。 |
| powerokwait | 如果 `/etc/powerstatus` 文件包含单词 OK，则在接收到 SIGKRW 信号时执行命令。这通常由 UPS 软件完成，表示正常电力水平已恢复。 |
| powerfailnow | 本地系统可能能够检测到外部 UPS 电量耗尽，并即将立即发生故障。 |
| ondemand | 当手动指示 init 进入特殊运行级别 a、b 或 c（分别等同于 A、B 和 C）时执行命令。实际上不会发生运行级别的变更。如果原始进程终止，程序将重新启动。 |
| sysinit | 在系统引导阶段执行命令；忽略 runlevels 字段。 |
| boot | 在系统引导阶段，处理完所有 sysinit 条目后执行命令；忽略 runlevels 字段。 |
| bootwait | 与 boot 相同，但 init 会等待命令完成，然后再继续处理其他 inittab 条目；同样忽略 runlevels 字段。 |
| initdefault | 完成 boot 和 sysinit 操作后要进入的运行级别。 |
| off | 不执行任何操作（可能对测试和调试有用）。 |
| ctrlaltdel | 拦截 Ctrl+Alt+Del 按键序列，通常用于优雅地关闭系统。 |
| kbsrequest | 用于拦截由键盘处理程序解释的特殊按键序列。 |

由于 inittab 文件是一个配置文件，而不是顺序执行的 shell 脚本，因此行的顺序并不重要。以井号（`#`）字符开头的行是注释，不会被处理。

前面示例 inittab 文件中的第一个非注释行将默认运行级别设置为 5。Fedora 的默认值 5（这是桌面系统常见的运行级别）意味着，在完成与 sysinit、boot 和 bootwait 操作，进入运行级别 5（引导至基于文本的登录界面）。另一个常见的 `initdefault` 级别是运行级别 3（通常用于以文本模式启动且通常没有图形用户界面的服务器）。表 11-4 描述了每个运行级别，并帮助你选择最适合作为环境中默认值的运行级别。

#### 表 11-4：可能的运行级别

| 运行级别 | 该运行级别中发生的情况 |
|---|---|
| 0 | 所有进程终止，机器有序停止。正如 init 标签中的注释所指出的，这不是 `initdefault` 的好选择，因为一旦内核、模块和驱动程序加载完毕，机器就会停止。 |
| 1, s, S | 这是单用户模式，通常用于系统维护，并且在某些情况下，保持较少进程运行且不激活任何服务可能是更可取的选择。在单用户模式下，网络不存在，X 服务器未运行，并且某些文件系统可能未挂载。 |
| 2 | 多用户模式。允许多个用户登录，所有配置的文件系统都已挂载，除了 X、`at` 守护进程、`xinetd` 守护进程和 NIS/NFS 之外的所有进程均已启动。如果你的机器没有（或者也许不需要）永久网络连接，这是 `initdefault` 的一个好选择。 |
| 3 | 带有网络服务的多用户模式。运行级别 3 是 Fedora 服务器上 `initdefault` 的典型值。 |
| 4 | 运行级别 4 作为用户定义的运行级别可用。在默认的 Fedora 配置中，它与运行级别 3 几乎相同。 |
| 5 | 带有网络服务和 X 的多用户模式。此运行级别启动 X 服务器并显示图形登录窗口，外观类似于更昂贵的基于 UNIX 的工作站。这是 Fedora 工作站或桌面系统常见的 `initdefault` 值。 |
| 6 | 所有进程终止，机器优雅地重启。同样，`init tab` 文件中的注释提到，这不是 `initdefault` 的好选择，甚至可能比运行级别 0 更糟。其效果可能是引导后重启的无限循环。 |
| 7, 8, 9 | 通常未使用且未定义，这些运行级别有潜力满足默认选项未涵盖的任何需求。 |
| a, b, c, A, B, C | 与 `ondemand` 操作配合使用。这些实际上并不指定运行级别，但可以根据指示在“按需”启动程序或守护进程。 |

> **注意：** 如果 `init tab` 文件中未指定 `initdefault`，引导过程将被中断，系统将提示你指定机器将进入的默认运行级别。

`init tab` 文件中的下一行指示 `init` 在进入默认运行级别之前执行 `/etc/rc.d/rc.sysinit` 脚本。此脚本执行许多初始化例程，例如选择*键位映射*文件，检查和挂载*根*和*proc*文件系统，设置时钟和主机名，配置*交换*空间，清理*临时*文件，并加载模块。接下来的七行控制在每个主要运行级别内执行的命令。在每一行中，调用 `/etc/rc.d/rc` 脚本，并使用所需的运行级别作为参数。反过来，它下降到*相应的*目录树（例如，对于运行级别 3，进入 `/etc/rc3.d` 目录）。
