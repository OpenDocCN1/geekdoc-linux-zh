
- 加载和解压缩内核
- 检测和配置设备
- 交接给 init 进程

这个过程的第一部分涉及引导加载程序。LILO 或其他引导加载程序将 Linux 内核加载到内存中并启动它运行。为了开始运行，Linux 会自行解压缩并从系统 BIOS 中收集其运行所需的一些信息。一旦收集到所有必需的信息，它就会丢弃 BIOS。请记住，除了已经收集到的信息之外，BIOS 服务不再可用。

现在硬件检测过程开始。首先内核检测的是可用处理器类型、控制台设置以及系统可用的内存量。内存检测并不总是像听起来那么简单，这就是为什么引导加载程序传递的最常见信息之一是系统中安装的物理 RAM 数量。这在现代系统上不太常见，但在旧系统上几乎总是需要知道你是否有超过 64 MB 的物理内存。随着系统继续启动，会检测到你有驱动程序可用的设备（要么编译到系统中，要么作为从初始 ramdisk 加载的模块可用），并向控制台打印各种初始化消息。此信息可以在系统准备就绪后使用 dmesg 命令查看。它存储在内核的环形缓冲区中，但正如名称所示，此缓冲区不会无限增长。如果你的系统生成大量内核消息，你可能会很快丢失有关设备初始化的信息。为防止这种情况，Red Hat 在 /etc/rc.d 中的启动 rc.sysinit 脚本中添加了一行以在启动期间捕获消息：

```
dmesg > /var/log/dmesg
```

这将在 /var/log 中创建一个名为 dmesg 的文件，其中包含内核启动消息和在 rc.modules 中加载的模块生成的任何内核消息。这些信息在调试问题和确定检测到哪些设备以及检测顺序时非常有用。除了捕获启动消息外，dmesg 命令随时都可用于检查内核环形缓冲区的內容。有关此命令的完整详细信息可在 dmesg(8) 手册页中找到。

一旦所有设备都被检测到并且各种内核子系统（如 VFS）已启动，根目录将被挂载并将控制权传递给 init 程序。init 程序随后负责通过使用初始化脚本启动系统的其余部分，通常位于 /etc/rc.d 及子目录中。

## /etc/inittab 和 rc 脚本

init 进程是接管内核控制并启动系统上所有必需进程以使其准备使用的程序。在你的 Linux 系统上，init 进程始终具有进程 ID 1。init 负责跟踪当前运行级别并管理运行级别之间的转换。init 可以采用两种基本模型来实现所有这些。

其中之一是基于 BSD 发行版的大多数 UNIX 变体使用的模型。此模型使用最少的启动文件，称为 rc 脚本，通常位于 /etc 目录中，名称如 rc、rc.local 等。Red Hat 以及大多数其他 Linux 发行版不使用此模型。相反，它们选择使用 System V Release 4 风格的初始化脚本。这些脚本存储在通常称为 init.d 的目录中，对于每个定义的运行级别，都有一个名为 rcN.d 的目录，其中 N 是运行级别，其中包含指向 init.d 中脚本的系列符号链接。在 System V 基于的系统（如 HP/UX 和 Solaris）上，这些目录通常位于 /etc；然而，在你的 Red Hat Linux 系统上，这些目录存储在 /etc/rc.d 目录下更深一层。

为了了解 init 的工作，让我们来看看它所依赖的配置文件：/etc/inittab。此文件定义了 init 基于运行级别所需的操作。以下是从 Red Hat Linux 系统的 /etc/inittab 中找到的行描述。

inittab 中定义的第一件事是默认运行级别，设置为 5。在 Red Hat 系统上，5 定义为 X Windows 系统为默认接口且登录通过 gdm 接口执行的级别，该接口向用户呈现图形登录屏幕。这行看起来像这样：

```
id:5:initdefault:
```

在默认运行级别定义之后是启动脚本的定义。每个定义由一个 id 组成，后跟此操作应采取的运行级别，后跟应采取的操作，最后是应执行的进程。操作字段决定这些脚本执行的顺序。操作为 sysinit 的脚本最先运行。

在此示例中，第一个要运行的脚本是名为 booterd 的脚本。此脚本绘制 Red Hat 使用的花哨启动屏幕。接下来，以 default 参数运行模块初始化脚本 rc.modules。随后，rc.serial 脚本运行以初始化我们系统上的串行端口。一旦所有操作为 sysinit 的脚本运行完毕，init 就会运行操作为 boot 或 bootwait 的脚本。这两种操作的区别在于，对于 bootwait，init 会等待指定进程完成后再继续，而对于 boot 则不会。我们的示例 inittab 文件包含一个具有 sysinit 操作的单行，该行执行 rc.boot 脚本。以下是执行启动过程中的这些步骤的行：

```
s1::sysinit:/etc/rc.d/rc.sysinit
```

为了实现期望的 System V 风格启动，我们需要为每个运行级别提供一行来定义如何进入该运行级别。inittab 中接下来的九行正是这样做的。在每个级别，rc 脚本都以运行级别作为参数运行。

```
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```

这些行中有两个值得注意的地方是被调用的 rc 脚本，以及作为故障安全机制提供的最后一行，以防更改到运行级别 6（重新启动系统）失败。rc 脚本背后的基本思想是执行以下操作：

- 更改目录到 /etc/rc.d/rcN.d，其中 N 是指定的运行级别。
- 运行所有以字母 K 开头的脚本，并带上 stop 参数。顺序由文件名决定。
- 运行所有以字母 S 开头的脚本，并带上 start 参数。

当然，实际情况比这更复杂，但大致就是这样。

在这些行之后是一行指定在每个运行级别运行的进程。此行在每次运行级别转换时运行一次 update 实用程序。

```
ud::once:/sbin/update
```

我们 inittab 文件中的下一行定义了用户按下 Ctrl+Alt+Del 时运行的进程。此行说明在任何运行级别，按下此键序列将导致系统使用 shutdown 命令重新启动。

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now
```

init 包的一个相对较新的功能是能够定义一个特殊的键序列，触发 init 进程的操作。Red Hat 的默认 inittab 文件不包含此示例，但通过添加以下行，该行除了向控制台回显一条消息外什么也不做，你可以自行实现此功能。如果你想利用此功能，请参阅 inittab 的手册页。

```
kb::kbrequest:/bin/echo "Keyboard Request--edit /etc/inittab to let this work."
```

init 程序还能够解释来自智能 UPS 的信号。这通常通过有一个监控 UPS 状态的守护进程来实现，并基于该状态向 init 进程发送信号。可以为这些类型的事件指定的有三种操作：

- powerfail — 发生了电源故障，我们正在使用电池供电。
- powerfailnow — 电源已故障且电池电量低。
- powerokwait — 电源已恢复。

我们的示例 inittab 文件显示了可以采取的处理这些事件的操作类型：

```
pf::powerfail:/sbin/shutdown -h +5 "Power Failure; System Shutting Down"
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"
```

我们示例 inittab 中的下一组行负责管理虚拟控制台上的 getty 进程。类似的条目将用于在串行设备上运行 getty，但我们的示例不包含此类行。

```
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```

这些 getty 行的语法高度依赖于你在系统上选择的可用 getty 版本。因此，始终有必要参考你运行的 getty 版本的手册页以确定正确的语法。如果你决定更改 getty 版本，最好在确定新版本工作正常之前至少保留一个虚拟控制台在旧版本下运行。

我们示例 inittab 文件中的最后一行用于启动 X Windows 系统的图形登录程序。有几种可供选择。随 XFree86 发行版一起提供的传统程序是 xdm。此外，KDE 桌面环境有自己的版本称为 kdm，GNOME 也有一个称为 gdm。由于 KDE 和 GNOME 都是 Red Hat 安装的标准部分，我们的示例包含对 prefdm 的调用，它是符号链接到 kdm 或 gdm，具体取决于系统管理员的偏好。

```
x:5:respawn:/etc/X11/prefdm -nodaemon
```

现在，让我们把所有内容放在一起并添加注释以提高清晰度。以下是我们 Red Hat Linux 系统的 /etc/inittab 文件。

