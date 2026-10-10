
![](img/f36419c0b225d12fa66de83fa271829b_444_0.png)

这是一个强大的工具。现在你的 Linux 电脑可以拥有你所需的各种能力，而无需让所有程序都 100% 运行（这只会减慢系统）。通过为特定目的手工剪裁运行级别，你可以轻松地在系统的不同用途之间切换。

# 特殊运行级别

Debian 的 `init` 在几个运行级别中配置了某些特定（且不可更改）的行为。这些都对应于重要的任务。在可能的情况下，Debian 遵循既定惯例。因此，大部分将与其他发行版保持一致。

## 运行级别 0

运行级别 0 有一个非常简单的任务：关闭所有程序并停止计算机。如果你的电脑中编译了 APM（高级电源管理）支持，且硬件较新，系统会自动关闭。

### 关闭你的电脑

是的，你只需要在 root shell 中输入 `0` 并看着你的系统关闭。然而，`shutdown` 命令有几个别名；如果你想让系统在三个三个小时后停止，你可以输入：

```
shutdown -h +3
```

或者直接输入

```
halt
```

这等同于

```
shutdown -h now
```

## 运行级别 1

运行级别 1 留给单用户模式。在这个运行级别下，除了 root shell 之外，没有任何程序在运行。除了根目录外没有挂载任何文件系统，而根目录恰好是只读的。此运行级别通常用于恢复。

## 运行级别 3

运行级别 3 是可配置的，没有保留用途，但它是 Debian 使用的默认运行级别。

## 运行级别 6

运行级别 6 与运行级别 0 非常相似，但运行级别 6 不是停止系统，而是重启。这也可以通过 `shutdown` 命令调用：

## 运行级别 2、4 和 5

Debian 对运行级别 2、4 和 5 的配置没有特定策略。它们大部分是开放供你自定义的。

# init 的配置文件，`/etc/inittab`

除了所有使用 `init` 的脚本外，它只有一个控制其最基本行为的配置文件；`inittab` 指定了在 `init` 进入任何运行级别之前应该运行的脚本，以及在该脚本完成后将启动哪个运行级别。它指定了应该运行的命令。

Debian 组织 `inittab` 的方式将大部分运行级别的定义移出了 `inittab`，从 `inittab` 直接启动的程序只有 `getty`，用于在虚拟终端设备上启动登录提示。之所以这样做是因为它们需要特殊的处理，这在 `inittab` 之外完成要困难得多。

列举 12.2 `/etc/inittab` 示例

```
# /etc/inittab: init(8) 配置文件。
# $Id: inittab,v 1.8 1998/05/10 10:37:50 miquels Exp

# 默认运行级别。
id:2:default:

# 启动时的系统配置/初始化脚本。
# 除了在以紧急模式 (-b) 启动外，它最先运行。
```

# Debian 系统管理
第二部分

# 列表 12.2 续

```
si:sysinit:/etc/init.d/rcS
```

# 在单用户模式下执行的操作。

--S:wait:/sbin/login

# `/etc/init.d` 在运行级别（run level）改变时

# 执行 S 和 K 脚本。

# 运行级别 0 是停机。

# 运行级别 1 是单用户模式。

# 运行级别 2-5 是多用户模式。

# 运行级别 6 是重启。

10:wait:/etc/init.d/rc 0

11:wait:/etc/init.d/rc 1

12:wait:/etc/init.d/rc 2

13:wait:/etc/init.d/rc 3

14:wait:/etc/init.d/rc 4

15:wait:/etc/init.d/rc 5

16:wait:/etc/init.d/rc 6

# 通常不会到达，但在紧急情况下会发生穿透。

26:respawn:/sbin/login
```

# 当按下 CTRL-ALT-DEL 时执行的操作。

ca:12345:ctrlaltdel:/sbin/shutdown -t1 -a -r now

# 特殊按键（Alt-上方向键）的动作。

kb:kbreakpoint:echo "键盘请求--编辑 /etc/inittab 以使此生效。

```

# 当断电/恢复电源时执行的操作。

pf:powerwait:/etc/init.d/powerfail start

np:powerfailnow:/etc/init.d/powerfail now

po:powerok:/etc/init.d/powerfail stop

# 用于运行级别的 `/sbin/getty` 调用。

# "id" 字段必须与设备的最后

# 字符（"tty" 之后）相同。

# 格式：

# id:<runlevels>:<action>:<process>

1:234S:respawn:/sbin/getty 38400 tty1

2:23:respawn:/sbin/getty 38400 tty2

3:23:respawn:/sbin/getty 38400 tty3

4:23:respawn:/sbin/getty 38400 tty4

5:23:respawn:/sbin/getty 38400 tty5

6:23:respawn:/sbin/getty 38400 tty6
```

# 在串口线上（用于终端）放置 `getty` 的示例

#
T0:23:respawn:/sbin/getty -L ttyS0 9600 vt100
```

# 自定义启动过程
第 12 章

```
 #T1:23:respawn:/sbin/getty -L ttyS1 9600 vti0

# 在调制解调器线上放置 `getty` 的示例

#
#T3:23:respawn:/sbin/mgetty -x0 -s 57600 ttyS3
```

# `/etc/inittab` 的格式

仔细查看列表 12.2。你的系统的 `inittab` 看起来（至少在某种程度上）是这样的。此文件包含一种基本类型的指令，它指定了一个命令行、对其采取的某些动作，以及在哪些运行级别下应当激活。这些行的格式基本上如下：

```
id:runlevels:action:command
```

其中 `id` 是某个任意名称（这并不重要），`runlevels` 是一个数字字符串（用于运行级别），`action` 描述了应该执行什么命令，而 `command` 指定了要执行的实际命令行。

例如，启动 `getty` 的这些行之一：

```
1:2345:respawn:/sbin/getty 38400 tty1
```

基本上，这告诉系统在启动后、在运行级别 2–5 中，应该运行命令 `/sbin/getty 38400 tty1`（有关此操作具体作用的更多信息，请参阅 `getty(8)`）。在这里使用的 `action` 标志是 `respawn`，它会导致命令在每次退出时重新运行（在这种情况下，当用户在 shell 中输入 `exit` 时）。

正如你在列表 12.2 中所所示，在运行级别 2 和 3 中有六个活跃的 `getty`，但在 4 和 5 中只有一个。假设你想在虚拟控制台上有三个可用的 shell。你需要在 ID 为 2 和 3 的行的 `runlevels` 字段中添加数字 4。也就是说，你替换这二行：

```
2:23:respawn:/sbin/getty 38400 tty2

3:23:respawn:/sbin/getty 38400 tty3
```

替换为这些行：

```
2:234:respawn:/sbin/getty 38400 tty2

3:234:respawn:/sbin/getty 38400 tty3
```

你只能通过重启或执行命令来使 `inittab` 的更改生效：

```
telinit q
```
