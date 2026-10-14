
`pf::powerfail:/sbin/shutdown -h +5 "Power Failure; System Shutting Down"`

# If battery is fading fast -- we hurry...

`p1::powerfailnow:/sbin/shutdown -c 2> /dev/null`

`p2::powerfailnow:/sbin/shutdown -h now "Battery Low..."`

# If power was restored before the shutdown kicked in, cancel it.

`po:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"`

# Run gettys in standard runlevels

`1:12345:respawn:/sbin/getty tty1 VC linux`

`2:2345:respawn:/sbin/getty tty2 VC linux`

`3:2345:respawn:/sbin/getty tty3 VC linux`

`4:2345:respawn:/sbin/getty tty4 VC linux`

`5:2345:respawn:/sbin/getty tty5 VC linux`

`6:2345:respawn:/sbin/getty tty6 VC linux`

# Run kdm in runlevel 5

`gu:5:respawn:/bin/sh -c "C=/etc/rc.d/rc.gui;[ -x $C ]&&exec $C;init 3"`

> 运行级别只是使用软件将进程包分组的一种便捷方式。它们对内核没有特殊意义。所有 Linux 内核都以相同的方式启动引导过程。只有在 `init` 启动之后，你才开始使用运行级别。

### inittab 详解

> **注意**
>
> 本文以 Caldera OpenLinux 的 `inittab` 为例进行说明。你的 `inittab` 可能不同，但工作方式相同。阅读完本节后，你应该能够理解大多数 Linux 的 `inittab`。

阅读 `inittab` 时，你会跳过任何以 `#` 开头的行，因为这些行会被 `init` 当作注释忽略。其余的行可以像许多其他典型的 UNIX 类配置表一样轻松阅读；也就是说，每一列用冒号（`:`）分隔，可以按如下方式解读：
- **id**——第一列是该行的唯一标识符。它最长可以是四个字母数字字符，但通常限制为两个。较旧的系统限制为两个字母数字字符，大多数发行版没有改变这一惯例。
- **runlevel**——第二列指示该行对哪些运行级别有效。此列可以为空，也可以包含任意数量的有效运行级别。如果为空，则对所有运行级别都有效。
- **action**——可以是多种情况；最常见的是 `respawn`，但也可以是以下任何一种：`once`、`sysinit`、`boot`、`bootwait`、`wait`、`off`、`ondemand`、`initdefault`、`powerwait`、`powerfail`、`powerokwait`、`ctrlaltdel`、`kbrequest`。
- **process**——要运行的具体进程或程序。

`inittab` 中的每一行都有一个唯一标识符。通常，这个标识符很容易与所执行的特定操作关联起来。例如，在第一个串行端口上生成一个 getty 的行可能会对 `/dev/ttyS0` 使用标识符 `S0`。

默认情况下，运行级别标识为 0–6 和 A–C。运行级别 0、1 和 6 是特殊的——不要随意更改它们。它们分别对应系统停机、维护模式和系统重启。例如，更改运行级别 1 可能会产生深远影响。请注意，要进入维护模式（运行级别 1），你可以向 `init` 传递参数 1（使用 `telinit`）。或者，你也可以使用 S 或 s。如果你更改了运行级别 1 所对应的操作，那么使用 S 或 s 时也会应用相同的更改。不过，运行级别 2–5 可以根据需要自定义。（参见“故障排查”一节，了解如何引导到默认运行级别之外的运行级别。）

> **注意**
>
> 使用 `telinit` 是向 `init` 传递命令的首选方法，但直接调用 `init` 也并不少见。

大多数 Linux 发行版都包含 `runlevel` 命令（位于 `/sbin` 中），该命令可用于提供有关当前和先前运行级别的信息。执行此命令会输出先前的运行级别和当前的运行级别，例如 `N 3`。`N` 表示没有先前的运行级别，这种情况可能出现在重启之后；`3` 表示当前的运行级别。如果你将运行级别更改为 2，然后重新发出 `runlevel` 命令，你将看到 `3 2`。

## 动手实践 init

因为动手操作比仅仅阅读更能说明问题，请在您的系统上试试：以 root 身份（只有 root 才能让 `init` 切换运行级别）执行 `init` 命令。您会收到一条用法消息，提示您向 `init` 传递一个参数，该参数可以是 0–6 之间的一个数字，也可以是字母 A–C、S 或 Q。小写字母在语法上与其对应的大写字母等价。如果您向 `init` 传递了合法值以外的任何内容，您会收到相应的用法消息；因此，如果没有收到该消息，您就知道它是一个合法值（就 `init` 而言）。

> **警告**
>
> 只有在确定可以通过网络 `telnet` 到您的系统时，才尝试以下操作。

如果您正在使用的系统连接到了网络，并且您可以从另一台机器 `telnet` 到它，那么您不妨尝试向 `init` 传递参数 8，例如 `init 8`（如果您愿意，也可以 `telinit 8`）。您可能会看到一些关于向程序发送 TERM 和 KILL 信号的消息，然后您的虚拟终端将停止响应。转到另一台系统，`telnet` 到您的系统，再次输入 `runlevel`；您将看到 3 8。在您确认确实切换到了运行级别 8 之后，再切换回之前的运行级别。您的登录提示会重新出现在屏幕上。

> **注意**
>
> 根据系统脚本的具体情况，您的发行版在尝试此实验时可能会有不同的表现。您可能会保留一个登录提示，直到它第一次被使用并且您注销，届时它不会重新生成登录提示。

前面的练习表明，尽管运行级别 7–9 没有文档说明，但它们实际上在需要时是可以使用的。（当您切换到运行级别 8 时发生了什么，将在本章后面变得清晰。）这些运行级别之所以不被使用，仅仅是因为使用它们并非惯例。SysV Linux 系统可定制的运行级别（2–5）通常对任何人来说都绰绰有余；Red Hat 和 Caldera 默认都不使用运行级别 4，因此它可以供您使用。Debian 对图形和非图形登录都只使用运行级别 2，因此运行级别 3–5 可供您自定义。

## init 的冷门之处

下面来看看您可以传递给 `init` 的其他字母参数。当您想要按需生成 `inittab` 中列出的守护进程时，可以使用字母 A–C。告诉 `init` 切换到运行级别 c 本身并不会改变运行级别；它只是执行具有运行级别 c 的那一行上所列出的操作。

假设您想在一个端口上放置 `getty` 来接收呼叫，但仅限于先接到语音呼叫之后（并且不是一直如此）。再假设您想准备好接收数据呼叫或传真呼叫，并且在收到语音消息时您会知道需要哪一种。您在 `inittab` 中插入两行新行，每行都有自己的 ID，每行都有一个运行级别，例如 A 用于数据，B 用于传真。当您知道需要哪一个时，只需从以下命令行之一启动相应的进程：

```text
telinit A
telinit B
```
