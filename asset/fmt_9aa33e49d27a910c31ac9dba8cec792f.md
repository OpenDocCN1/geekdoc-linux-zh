
系统将继续运行。如果你在系统上设置了 RAID 或逻辑卷管理（LVM），内核也将配置这些设备。在内核配置所有系统设备并挂载系统驱动器后，它会运行 `/sbin/init` 命令。

## /sbin/init 程序

`/sbin/init` 程序是内核配置完系统设备并挂载系统驱动器后运行的第一个系统进程。`/init` 程序就像系统的项目经理，因为它管理系统启动的剩余步骤，并且是所有其他自动启动的系统启动进程的父进程或祖父进程。基本上，`init` 程序负责协调并运行 `/etc/rc.sysinit` 脚本。

该脚本启动系统交换分区（swap），检查文件系统并执行其他初始化。`init` 命令引用 `/etc/init/inittab` 脚本来获取如何启动系统的信息、运行哪个系统初始化脚本以及将系统带到 `inittab` 脚本中指定的运行级别（runlevel）。在典型的系统安装后，默认运行级别是级别 5。本节的其余部分描述了系统启动到运行级别 5 所采取的步骤。

在读取 `/etc/inittab` 脚本后，`init` 将控制权移交给 `rc.sysinit` 程序，该程序读取 `/etc/rc.d/init.d/functions` 文件以确定使用默认系统路径的程序、启动/停止程序、查找运行进程的进程 ID（PID）以及如何记录程序启动的成功或失败。下一个运行脚本是 `/etc/rc.d/rc`，它负责在运行级别改变时启动和停止服务并确定运行级别。

在 `/etc/rc.d` 目录下有额外的目录 `rc0`、`rc1`、`rc2`、`rc3`、`rc4`、`rc5` 和 `rc6`。目录名对应于运行级别。这些目录中的每一个都包含对应服务的脚本。在本例中，系统将启动到运行级别 5，因此 `init` 程序在 `/etc/rc.d/rc5/` 目录下查找要启动和停止的进程。列表 6-1 显示了新安装的 Fedora Core 3 系统 `rc5.d` 目录的内容。

```
K01yum -> ../init.d/yum
K02NetworkManager -> ../init.d/NetworkManager
K05saslauth -> ../init.d/saslauth
K10psacct -> ../init.d/psacct
K20nfs -> ../init.d/nfs
K24irda -> ../init.d/irda
```

**列表 6-1** 在运行级别 5 中启动和停止服务的脚本。（继续）

```
K30spamassin -> ../init.d/spamassin
K35vncserver -> ../init.d/vncserver
K35winbind -> ../init.d/winbind
K36lisa -> ../init.d/lisa
K50netdump -> ../init.d/netdump
K73ypbind -> ../init.d/ypbind
K74nscd -> ../init.d/nscd
K74ntpd -> ../init.d/ntpd
K85mdmp -> ../init.d/mdmp
K89bluetooth -> ../init.d/netplug
K90bluetooth -> ../init.d/bluetooth
K94diskdump -> ../init.d/diskdump
K99microcode_ctl -> ../init.d/microcode_ctl
S04readahead_early -> ../init.d/readahead_early
s05kudzu -> ../init.d/kudzu
s06cpuspeed -> ../init.d/cpuspeed
s08iptables -> ../init.d/iptables
s09isidn -> ../init.d/isidn
s09pcmia -> ../init.d/pcmia
s10network -> ../init.d/network
s12syslog -> ../init.d/syslog
s13irqbalance -> ../init.d/irqbalance
s13portmap -> ../init.d/portmap
s14nfslock -> ../init.d/nfslock
s15dmonitor -> ../init.d/dmonitor
s18rpcgsssd -> ../init.d/rpcgsssd
s19rpcidmap -> ../init.d/rpcidmap
s19rpcvcgsssd -> ../init.d/rpcvcgsssd
s25nerfs -> ../init.d/nerfs
s26apmd -> ../init.d/apmd
s261_lm_sensors -> ../init.d/lm_sensors
s28autofs -> ../init.d/autofs
s33-nifd -> ../init.d/nifd
s34MDNSResponder -> ../init.d/mDNSResponder
s40smartd -> ../init.d/smartd
s44acpid -> ../init.d/acpid
s55cups -> ../init.d/cups
s55asnhd -> ../init.d/asnhd
s56xinetd -> ../init.d/xinetd
s80sendmail -> ../init.d/sendmail
s85prgm -> ../init.d/gprgm
s90crond -> ../init.d/crond
s90xfs -> ../init.d/xfs
s95anacron -> ../init.d/anacron
s95atd -> ../init.d/atd
s96readahead -> ../init.d/readahead
s97messagebus -> ../init.d/messagebus
s97rhnsd -> ../init.d/rhnsd
S98cups-config-daemon -> ../init.d/cups-config-daemon
S98haldaemon -> ../init.d/haldaemon
S99local -> /rc.local
```

**列表 6-1**（继续）

`rc.d` 目录中的所有脚本都是 `/etc/rc.d/` 目录下实际脚本的符号链接。使用符号链接意味着可以通过添加或删除链接或更改 `rc0` 到 `rc6` 中的脚本顺序来修改运行级别，而不影响它们指向的脚本。符号链接是指向另一个文件的类型。如你所示，每个链接以 K 加数字或 S 加数字开头。以 K 开头的进程在运行级别上被停止，而以 S 开头的进程被启动。进程按数字顺序停止或启动：由 `/etc/rc.d/init.d/stop` 命令停止，由 `/etc/rc.d/init.d/start` 命令启动。如果你需要，可以通过运行命令更改你系统的启动顺序。例如，`/etc/rc.d/init.d/vsftp` 会停止 vsftp 服务。

`init` 程序在完成之前还有几个任务要执行。其中一个任务是运行 `/etc/inittab` 文件中指定的 `getty`。这提供了你可以用于登录服务器的终端。这些终端是级别 5 提供的标准登录界面之外的。`init` 程序最后执行的操作是运行 `/etc/rc.d/rc.local` 脚本。如果你想运行自己的脚本，可以在此文件中放入调用。更多信息请参见本章后面的“系统启动时启动程序”部分。由于系统在运行级别 5 ，你会看到图形登录提示。

## 探索运行级别

“运行级别”一词在本章中已经使用了几次，现在是了解更多运行级别以及为什么要使用它们的好机了。Linux 系统通常有八个运行级别，但我们对 Fedora Core 或 Enterprise Linux 系统使用的七个。每个运行级别都有组与该级别相关的进程，会在进入运行级别时启动。Fedora Core 或 Enterprise Linux 系统上的运行级别及其用途如下：

`/etc/inittab` 文件控制系统启动时使用的默认运行级别。你可以通过进行以下更改来轻松更改系统的运行级别：

### 修改系统运行级别

在 `/etc/inittab` 文件中查找以下行。它位于可用运行级别的列表下方。

```
id:5:initdefault:
```

行中的数字 5 表示系统将启动到运行级别 5。如果你想启动到运行级别 3，只需将数字 5 改为 3，现在行变为：

```
id:3:initdefault:
```

Fedora Core 和 Enterprise Linux 系统的默认运行级别是级别 5，它提供完整的多用户环境并启动 X Window 系统为用户提供图形环境。运行级别 3 提供与级别 5 完全相同的多用户系统，例外是不为用户提供图形环境。运行级别 3 通常用于不需要 GUI 的系统，因为运行 GUI 会消耗大量的系统资源。

运行级别 2 和 4 在 Fedora Core 或 Enterprise Linux 系统中没有使用。设置运行级别是为了用户可以根据需要配置它们。通过这样做，你可以为测试或任何用途创建自己的运行级别。运行级别 1 进入单用户模式进行故障排除或运行诊断，但它通常不会设置为 `/etc/inittab` 文件中的默认运行级别。如果你的系统出现问题，你通常会在系统启动期间输入命令进入运行级别 1，如下：

- 当启动屏幕出现时，使用方向键选中你想更改的内核。
- 按字母 `e`。
- 滚动到第二行并再次按 `e`。
- 在行尾输入 `init 1` 并按回车。
- 按字母 `b` 将系统启动到单用户模式。

## 系统启动时启动程序

`/etc/rc.d/rc.local` 文件是系统启动时 `init` 命令运行的最后一个文件。如果你想运行额外的脚本来配置设备，可以将命令放入此脚本中。列表 6-2 显示了一个典型的 `/etc/rc.d/rc.local` 文件，调用了另一个名为 `/usr/bin/novellconfig` 的脚本。`novellconfig` 脚本用于加载模块并在服务器上配置 IPX。你也可以在调用脚本后通过输入参数为脚本传递选项。

> 注意：novellconfig 仅作为示例，在默认安装中并不存在。你可以创建自己的脚本并调用你想要的任何内容。

```
#!/bin/sh
# 此将在所有其他 init 脚本*之后*执行。
# 如果你不想执行完整的 Sys 风格初始化工作，
# 可以在这里放入自己的初始化内容。

touch /var/lock/subsystems/local
/usr/bin/novellconfig
```

**列表 6-2** 调用另一个程序的 /etc/rc.d/rc.local 文件。

## 关闭系统

如果你在系统上运行图形用户界面（GUI），关闭系统只需点击几次鼠标一样简单。GNOME 桌面面的关机程序如下：

1. 在顶部面板菜单中选择“操作”（Actions）->“注销”（Logout）。屏幕会显示一个界面，询问你是想注销、重启还是关机。
2. 点击“关闭”（shutdown）单选按钮。
3. 点击“确定”（OK），系统将开始关闭。

如果你在系统上没有运行图形界面，关机命令是 `shutdown`，并使用以下语法：

```
/sbin/shutdown -t sec [-c time [warning message]]
```

你可以参考 `shutdown` 的 man 页来获取关机命令的所有细节。要访问 `shutdown` 的 man 页，请输入以下命令：

```
man shutdown
```

无论使用何种方法启动关闭命令，随后的过程都是相同的。任何登录到系统的用户将收到通知，告知已发出关闭命令，且将不再允许继续操作。系统上运行的进程将收到 `SIGTERM` 信号，这将尝试干净停止运行的进程。关闭程序会向 `init` 程序发送信号，根据关闭命令切换到不同的级别。级别 0 用于关闭系统，而级别 6 用于重启系统。以下是一些常用关机命令的示例及其含义解释：

> 注意：在大多数情况下，只有 root 用户可以使用 `shutdown` 命令来关闭系统。

`/sbin/shutdown -h now` 命令会立即开始关机过程并停止系统。`/sbin/shutdown -r now` 命令会立即开始关机过程并重启系统。

# 系统启动与关闭

## GRUB 配置文件

当系统启动时，GRUB 会呈现一个图形界面，显示你可以启动的各个操作系统。`/boot/grub/grub.conf` 文件控制在图形界面上显示的信息。这决定了你是否能看到图形界面。列表 6-3 显示了一个典型的 GRUB 配置文件。文件中各个项的解释如下：

```
## grub.conf 由 anaconda 生成
# 请注意，在修改此文件后，你不需要重新运行 grub
# 注意：你有一个 /boot 分区。这意味着
# 所有内核和 initrd 路径都是相对于 /boot/ 的；例如：
# root (hd0,0)
# kernel /vmlinuz-version root=/dev/VolGroup00/LogVol00
# initrd/initrd-version.img
# boot=/dev/hda
default=0
timeout=5
splashimage=(hd0,0)/grub/splash.xpm.gz
hiddenmenu
title Fedora Core (2.6.9-1.667)
root (hd0,0)
kernel /vmlin-2.6.9-1.667 root=/dev/VolGroup00/LogVol00 rhgb
initrd-2.6.9-1.667.img
```

**列表 6-3** /boot/grub/grub.conf GRUB 配置文件。

所有以 `#`（井号字符）开头的行都是注释，会被忽略。GRUB 也会忽略空行。

紧随 `#` 开头的行之后、`title` 开头的行之前的行，是 GRUB 用于显示菜单的菜单界面命令。这些行的含义如下：

- **default=0** — 该命令告诉 GRUB 启动第一个以 `title` 开头的项。如果你有两个以 `title` 开头的项，你可以将此数字设置为 1 来启动第二个项。
- **timeout=5** — 该命令告诉 GRUB 在五秒后启动默认项。要更改时间，请根据需要增加或减少该数字。
- **splashimage=(hd0,0)/grub/splash.xpm.gz** — 该命令告诉 GRUB 在哪里查找它在菜单时显示的启动图像（splash image）。如果你需要，可以创建自己的图像。只需遵循此处所示的格式。
- **hiddenmenu** — 该命令告诉 GRUB 不要显示菜单，并在超时过期后启动默认项。你仍然可以通过按任何键看到菜单。
- **title** — 该命令告诉 GRUB 使用 `title` 命令后的名称在菜单上列出启动名称。在本例中，该标题为 `Fedora Core (2.6.9-1.667)`，这是操作系统的名称和内核版本号。

`title` 之后的行解释如下：

- **root (hd0,0)** — 此行告诉 GRUB 从第一块硬盘的分区启动系统。
- **kernel...** — 此行告诉 GRUB 内核的位置，并将内核参数传递给内核。所有位置都相对于 `boot` 分区，因此此列表表示内核在 `boot` 分区的根目录下。如果你想在内核加载之前传递内核参数，这就是要添加参数的行。这里已经有两个选项了：`kernel` 行上的 `rhgb` 告诉系统使用图形启动。最后，`quiet` 告诉系统不要显示有关系统启动的详细信息。
- **initrd...** — 此行告诉 GRUB 初始内存磁盘（initial ramdisk）镜像的位置，该镜像用于加载系统的特殊驱动程序。所有位置都相对于 `boot` 分区，因此此列表表示初始内存磁盘镜像在 `boot` 分区的根目录下。

## 总结

在本章中，你学习了 Fedora Core 和 Red Hat Enterprise Linux 启动和停止系统的程序。启动过程的每一步都按照其发生的顺序进行了解释，并列出了每一步运行的程序。此外，你还学习了引导加载程序（boot loaders）。在本章中，你学习了关于引导加载程序的知识，以及 GRUB 在启动过程中的至关重要性。最后，你学习了如何使用 `shutdown` 命令来关闭系统。

第 7 章：文件系统

本章从描述文件系统的结构开始，介绍文件系统。

图 7-1 显示了典型的 Fedora 和 Red Hat Linux 系统的文件系统结构。

# 文件系统详解 143

这种技巧在 Windows 上无法运行，因为 Windows 将其文件位置映射到静态磁盘设备定义。你必须将程序的文件引用从 `c:\` 更改为 `d:\` 等。Linux 的文件系统管理是你在生产环境服务器上使用 Linux 而不是 Windows 的另一个良好理由。

## 目录 (The Directory)

目录是根目录，位于文件系统结构的顶端。在许多系统中，`/` 目录是系统上的唯一分区，所有其他目录都挂载在其下方。图 7-1 显示了一个将 `/` 目录挂载为唯一分区的文件系统，所有其他目录都包含其中。`/` 目录的主要目的是启动系统并纠正可能阻止系统启动的任何问题。根据 FHS（文件层次结构标准），`/` 目录必须包含或链接以下目录：

- bin — 该目录包含供系统管理员或其他用户使用的命令文件。`bin` 不能包含子目录。
- boot — 在 Red Hat 系统上，这是包含内核（操作系统的核心）的目录。该目录下还包含与系统启动相关的文件，如引导加载程序和初始内存磁盘（ramdisk）。
- dev — 该目录包含设备节点，操作系统通过这些设备节点访问系统上的硬件和软件设备。
- etc — 该目录及其子目录包含大多数系统配置文件。如果你在系统上安装了 X Windows 系统，则 `X11` 子目录位于此处。网络和系统相关文件在 `sysconfig` 子目录中。`etc` 的另一个子目录是 `skel` 目录，它保存作为模板的文件，在创建用户时在用户的家目录下创建文件。
- home — 该目录包含系统中用户的目录。`home` 的子目录将以其所属的用户命名。
