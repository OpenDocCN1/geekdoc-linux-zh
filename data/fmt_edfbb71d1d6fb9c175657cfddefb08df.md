
相应的 getty 会被放置到线路上，直到收到第一个呼叫。当呼叫方终止连接时，getty 会退出，因为按照定义，按需生成的进程不会重新生成。

> **注意：** 前面的示例只是一个虚构的示例。对于传真和数据功能，请使用 `mgetty`。

另外两个字母 `S` 和 `Q` 比较特殊。如前所述，`S` 会将您的系统带入维护模式，这与将运行级别切换到运行级别 1 相同。`Q` 用于告诉 `init` 重新读取 `inittab`。`inittab` 文件可以根据需要随意更改，但只有在特定情况下才会被读取：

- 它的某个进程终止时。（您需要重新生成另一个吗？）
- 收到来自电源守护进程（或命令行）的 `powerfail` 信号时
- 当 `telinit` 指示它更改运行级别时

`Q` 参数告诉 `init`：“我更改了一些内容，请重新读取 `inittab`。”

## 自上而下解读 INITTAB 文件

在实际的 `inittab` 中，以 `#` 符号开头的行会被禁用，作为示例或解释性说明保留下来，或者作为将来可能使用的示例。请务必通读其中的注释。这些注释可能会给您一些关于如何有效自定义 `inittab` 的提示。大多数旨在从 `inittab` 运行的程序（如 `mgetty` 或 `fax`）都会在其文档中附带示例，说明如何实现它们。

因为您已经知道如何阅读一行（`id:runlevel:action:process`），下面来看看每一行的作用：

- `id:5:initdefault:`

  第一行值得注意的是默认运行级别行。稍后您会看到，正是这一行决定了您是启动到图形界面还是命令行终端。此值绝不能设置为 `0` 或 `6`。

- `s0::sysinit:/bin/bash -c 'C=/sbin/booterd; [ -x $C ] && $C'`  
  `s1::sysinit:/bin/bash -c 'C=/etc/rc.d/rc.modules; [ -x $C ] && $C default'`  
  `s2::sysinit:/bin/bash -c 'C=/etc/rc.d/rc.serial; [ -x $C ] && $C'`  
  `bw::bootwait:/etc/rc.d/rc.boot`

  就在默认运行级别行的下方，您会看到系统初始化脚本调用。ID 为 `s0` 的行调用 `booterd`，它是处理 Lizard 启动屏幕的两个程序之一（只要 `/etc/grub/menu.lst` 或 `/etc/lilo.conf` 中没有删除 `vga = 274`）。ID 为 `s1` 的行通过 `/etc/rc.d/rc.modules` 脚本加载 `/etc/modules/defaults` 中列出的默认模块。ID 为 `s2` 的行配置串行端口，但前提是您已启用 `/etc/rc.d/rc.serial` 脚本（默认禁用）。这三行同时执行，`s0` 行在屏幕上显示 `s1` 脚本加载模块时的状态。ID 为 `bw` 的行是您直到系统异常关闭时才会注意到的一行。这一行调用 `rc.boot`，它负责检查磁盘驱动器的状态，以确保它们被正确卸载；如果没有，则运行 `fsck` 或继续挂载磁盘。如果 `fsck` 无法在无需协助的情况下修复磁盘，此脚本会将您置于运行级别 1 的 shell 中。由于系统必须等此脚本完成后才能继续，因此 action 列为 `bootwait`。

```text
~1:S:wait:/etc/rc.d/rc 1
~~:S:wait:/sbin/sulogin
```

这两行是两个脚本，每当您进入维护（单用户）模式时都会运行。您稍后会看到 `rc` 脚本。`sulogin` 程序是一个特殊程序，它让您的系统更安全一些，防止任何可以物理接触机器的人在不知道 `root` 密码的情况下重启进入单用户模式并访问系统。如果没有这一行，启动进入单用户模式时会向用户提供一个 `root` shell，而不提示输入密码。然而，这并不能防止一个精通技术的用户在物理接触机器的情况下入侵系统。实际上，绕过 `sulogin` 的方法之一以及波浪号（`~`）作为 ID 第一个字符的意义，将在本章末尾的“紧急情况”一节中讨论。

```text
l0:0:wait:/etc/rc.d/rc 0
l1:1:wait:/etc/rc.d/rc 1
l2:2:wait:/etc/rc.d/rc 2
l3:3:wait:/etc/rc.d/rc 3
l4:4:wait:/etc/rc.d/rc 4
l5:5:wait:/etc/rc.d/rc 5
l6:6:wait:/etc/rc.d/rc 6
```

ID 为 `l0`–`l6` 的行会在您切换到特定运行级别时运行。每次切换运行级别都会以要进入的特定运行级别作为参数来运行 `rc` 脚本。请记住，运行级别 `7`–`9` 是合法的运行级别，必要时可以使用。如果您想使用这些非标准运行级别中的任何一个，您需要添加一些行来定制这些运行级别，因为如果您要使用其中任何一个运行级别，您几乎肯定希望运行 `rc` 脚本。

```text
z6:6:respawn:/sbin/sulogin
```

ID 为 `z6` 的行旨在机器进入运行级别 6 时无法正常重启的情况下显示 `root` 密码提示。这仅仅是预防措施。在撰写本文时，我还没有听说有哪台机器不能正确响应重启命令。

```text
ca:12345:ctrlaltdel:/sbin/shutdown -t3 -r now
```

ID 为 `ca` 的行捕获键盘组合键 `Ctrl+Alt+Delete` 并执行关机并重启。如果需要，可以修改这一行，将 `-r` 改为 `-h` 来停止系统，或者

你可以直接删除 `-r`，让系统进入带有 `root` 提示符的单用户模式。

> **注意**
>
> 在使用 `X` 服务器时，你无法使用这个按键序列。`X` 服务器会捕获 `Ctrl-Alt-Delete`。你需要切换到虚拟终端才能使用此按键序列。

```text
kb::kbrequest:/bin/echo "Keyboard Request--edit /etc/inittab to let this work."
```

行 ID `kb` 捕获键盘序列 `Alt+Up` 箭头。目前，它会回显提示信息，说明这需要先配置才能使用。在大多数使用 `bash` 的默认设置中，这一特定命令序列会被忽略。首先，需要更改键映射，使 `bash` 能够传递该序列。完成之后，只需更改该行的进程部分，将 `echo` 命令替换为你想要运行的命令即可。

```text
pf::powerfail:/sbin/shutdown -h +5 "Power Failure; System Shutting Down"
p1::powerfailnow:/sbin/shutdown -c 2> /dev/null
p2::powerfailnow:/sbin/shutdown -h now "Battery Low..."
po:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"
```

如果你拥有与 `powerd` 守护进程兼容的 `UPS`，那么行 ID `pf`、`p1`、`p2` 和 `po` 将值得关注。`powerd` 守护进程可以监视串行端口，并执行 `inittab` 中记录的操作。`inittab` 已经足够清晰，这里不再赘述。

```text
1:12345:respawn:/sbin/getty tty1 VC linux
2:2345:respawn:/sbin/getty tty2 VC linux
3:2345:respawn:/sbin/getty tty3 VC linux
4:2345:respawn:/sbin/getty tty4 VC linux
5:2345:respawn:/sbin/getty tty5 VC linux
6:2345:respawn:/sbin/getty tty6 VC linux
```

行 ID `1`–`6` 在虚拟终端（VT）上重新生成 `getty`。请注意，在单用户模式下，只有一个 VT 可用。如果你想节省一些内存，可以在运行级别 5 中运行更少的 VT（但至少必须运行一个）。如果你决定使用未列出的运行级别，则需要将这些级别添加到已列出的级别中。你可以通过添加更多行（当然，需使用唯一的 ID）来增加 VT 的数量。查看之前的条目，你会看到行中的 `VC` 作为 `gettytab` 条目类型。`VC` 代表虚拟控制台（Virtual Console），在本文上下文中它与 VT 基本等价。如果你更希望使用 VT，则需要在 `/etc/gettytab` 中适当更改 `VC` 行。

> **提示**
>
> 如果在 `X` 服务器运行时使用 VT，并且更改了启动时生成的 VT 数量，你将会发现 `X` 服务器会位于不同的 VT 上。默认情况下，第一个可用终端是 8（除非你取消了图形启动——那么就是 7）。如果你减少了 VT 的数量，`X` 服务器会相应地降到编号更低的终端上。

请注意，无论运行级别如何，`kb`、`pf`、`p1` 和 `p2` 都会运行。当运行级别列为空时，该进程会在每个运行级别中运行。

```text
gu:5:respawn:/bin/sh -c 'X=/etc/rc.d/rc.gui;[ -x $X ]&&$X;[ -x $X ]||init 3'
```
