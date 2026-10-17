
c. Solaris 配置文件位于 `/etc/saf`，应使用 `sacadm` 进行管理。

d. 为了确保一致性，请在 AIX 上使用 `SMIT` 修改 TTY 参数。

### `/etc/ttytype` 文件

在许多系统上，终端类型信息保存在名为 `/etc/ttytype` 的文件中。`ttytype` 中条目的格式为

```
termtype device
```

其中 `device` 是表示端口的设备文件的短名称，`termtype` 指定 `termcap` 或 `terminfo` 数据库中的一个条目。当您登录时，`TERM` 环境变量将设置为此字段的值。

以下是一个 `ttytype` 示例文件：

```
wyse      console
dialup     ttyi0
dialup     ttyi1
vt320      ttyi2
h19        ttyi3
dialout    ttyi4
```

`sh` 和 `ksh` 使用 `.profile`；`bash` 使用 `.bash_profile` 和 `.bashrc`；`csh`/`tcsh` 使用 `.cshrc` 和 `.login`。

## `/etc/gettytab` 文件

`gettytab` 文件将 `std.9600` 等符号名称与端口配置配置文件关联，后者包括速度、奇偶校验和登录提示等参数。以下是一个示例：

```
# The default entry, used to set defaults for other entries, and in cases
# where getty is called with no specific entry name.
default:\
:ap:lm=\r\n\r\n hlogin\72 :sp#9600:
# Fixed-speed entries
2|std.9600|9600-baud:\
:sp#9600:
h|std.38400|38400-baud:\
:sp#38400:
```

格式与 `printcap` 或 `termcap` 相同。用竖线 (`|`) 分隔名称的行列出了每个配置所知的名称。条目中的其他字段设置与串行端口一起使用的选项。

## `/etc/gettydefs` 文件

与 `gettytab` 类似，`gettydefs` 定义了 `getty` 使用的端口配置。给定的系统通常只有一个或另一个，从不会同时存在两者。`gettydefs` 文件如下所示：

```
console# B9600 HUPCL # B9600 SANE IXANY #login: #console
19200# B19200 HUPCL # B19200 SANE IXANY #login: #9600
9600# B9600 HUPCL # B9600 SANE IXANY HUPCL #login: #4800
4800# B4800 HUPCL # B4800 SANE IXANY HUPCL #login: #2400
2400# B2400 HUPCL # B2400 SANE IXANY HUPCL #login: #1200
1200# B1200 HUPCL # B1200 SANE IXANY HUPCL #login: #300
300# B300 HUPCL # B300 SANE IXANY TAB3 HUPCL #login: #9600
```

### 条目的格式为

```
label# initflags # finalflags # prompt #next
```

`getty` 尝试将其第二个参数与标签条目匹配。如果在没有第二个参数的情况下调用它，则使用文件中的第一个条目。`initflags` 字段列出了在执行 `login` 之前应设置在端口上的 `ioctl(2)` 标志。`finalflags` 字段设置此后应使用的标志。

`initflags` 和 `finalflags` 中都必须有一个条目来设置连接的速度。可用标志因系统而异；请查阅 `gettydefs` 或 `mgettydefs` 手册页以获取权威信息。

`prompt` 字段定义登录提示，其中可能包含反斜杠表示法的制表符和换行符。`next` 字段给出应替换当前条目的 `initab` 条目的标签，如果收到中断信号。这在几十年前很有用，当时调制解调器不会自动协商速度，你必须通过一系列中断手动匹配速度。如今，它已过时。对于硬连线终端，`next` 应引用当前条目的标签。

每次更改 `gettydefs` 文件时，都应运行 `getty -c gettydefs`，它会检查文件的语法，以确保所有条目都有效。

## `/etc/inittab` 文件

`init` 支持各种“运行级别”，用于确定启用哪些系统资源。有七个运行级别，编号为 0 到 6，其中 “s” 被识别为级别 1 的同义词（单用户操作）。当你离开单用户模式时，除非 `/etc/inittab` 中存在如下面所述的 `initdefault` 字段，否则 `init` 会提示你输入运行级别。然后 `init` 会扫描 `inittab` 文件，查找与指定运行级别匹配的所有行。

运行级别通常设置成一个级别仅启用控制台，另一个级别启用所有 `getty`。你可以根据系统需要定义运行级别；不过，我们建议你不要偏离默认值太远。

`inittab` 中的条目形式为

```
id:run-levels:action:process
```

以下是 `inittab` 条目的一些简单示例：

```
# Trap CTRL-ALT-DELETE
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

# Run gettys in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
```

在此格式中，*id* 是一个一到两个字符的字符串，用于标识条目；可以为空。对于终端条目，通常使用终端编号作为 *id*。

*run-levels* 列出条目适用的运行级别。如果未指定任何级别（如第一行），则该条目对所有运行级别都有效。*action* 说明如何处理 *process* 字段；表 31.5 列出了一些常用的值。

如果 *run-levels* 中的一个与当前运行级别匹配，并且 *action* 字段表明该条目相关，则 `init` 使用 `sh` 执行（或终止）*process* 字段中指定的命令。表 31.5 中的 Wait? 列说明 `init` 是否在继续之前等待命令完成。

在上面的示例 `inittab` 行中，最后两行在前两个虚拟控制台上生成 `mingetty` 进程（使用 <Alt-F1> 和 <Alt-F2> 访问）。如果你添加硬连线终端或拨入调制解调器，适当的 `inittab` 行看起来与这些类似。然而，对于此类设备，你必须使用 `mgetty` 或 `getty`（而不是 `SUSE`），因为 `mingetty` 不够智能，无法正确处理它们。一般来说，`respawn` 是正确的操作，`2345` 是一个合适的级别集合。

> 请参阅第 88 页，了解有关 `init` 作用的更多信息。

*speed* 是波特率（例如 38400），而 *device* 是串行端口的设备文件（使用完整路径名）。

如果你想在使用 `mgetty` 时为某个端口指定默认终端类型，你必须在单独的文件 `/etc/ttype` 中指定它，而不能在 `mgetty` 命令行上指定。`ttype` 中条目的格式在第 1172 页有描述。

## Ubuntu Upstart

Ubuntu 已用一个重新架构的版本取代了其 `init`，该版本称为 Upstart，可根据事件启动和停止服务。Upstart 的可执行文件仍称为 `/sbin/init`。

Upstart 为 `/etc/event.d` 中的每个活动终端使用一个文件。例如，如果我们想让 `getty` 在 `ttyS0` 上运行，`/etc/event.d/ttyS0` 可能如下所示：

```
# ttyS0 — getty

# This service maintains a getty on ttyS0 from the point when
# the system is started until it is shut down again.

start on runlevel 2
start on runlevel 3
start on runlevel 4
start on runlevel 5

stop on runlevel 0
stop on runlevel 1
stop on runlevel 6 respawn
exec /sbin/getty 38400 ttyS0
```

有关 Upstart 的更多评论，请参阅第 94 页。

## Solaris and sacadm

与传统的 UNIX `gettys` 不同，传统的 UNIX `gettys` 监视每个端口的活动并提供登录提示，Solaris 有一个复杂的层次结构，称为服务访问设施，它控制 TTY 监视器、端口监视器以及提供大量复杂性但功能很少的其他许多东西。
