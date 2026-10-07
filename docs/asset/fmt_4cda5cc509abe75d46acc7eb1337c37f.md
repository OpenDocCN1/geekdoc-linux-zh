
这通常发生在规则意外匹配到设备时。例如，一个编写不当的规则可能会根据厂商同时匹配 SCSI 磁盘（符合预期）和相应的 SCSI 通用设备（错误匹配）。请借助 `udevadm info` 命令找到引起冲突的规则并使其更加具体。

### 7.4.3.5. `udev` 规则运行不可靠

这可能是前一个问题的另一种表现。如果不是，且你的规则使用了 sysfs 属性，则可能是内核时序问题，将在后续层中修复。目前，你可以通过创建一个等待使用的 sysfs 属性的规则，并将其附加到 `/etc/udev/rules.d/10-wait-for_sysfs.rules` 文件中（如果该文件不存在则创建它）。如果你这样做了，请通知 LFS 团队，并以此此类推。

### 7.4.3.6. `udev` 未创建设备

后续正文假设设备已静态编译到内核中，或已作为模块加载，并且你已经检查过 `udev` 没有创建不匹配的设备。

如果内核设备没有向 sysfs 导出其数据，`udev` 就没有信息来创建设备节点。这在来自外部的第三方驱动中最为常见。在 `/lib/udev/devices` 中创建一个具有适当主/次设备数的静态设备节点（参见文件详情）。内容位于内核设备内部或第三方驱动提供的文档中。静态设备节点将在 `udev` 启动时复制到 `/dev`。

### 7.4.3.7. 重启后 `udev` 设备命名发生变化

这是由于 `udev` 在设计上并行处理事件和模块，因此顺序是不可预测的。这不会被“修复”。你不应该依赖内核设备名称的稳定性。你应该创建自己的规则，根据设备的某些稳定属性（例如序列号或 `udev` 安装的 *id* 工具的输出）来创建稳定名称。示例请参见第 7.5 节“为设备创建自定义符号链接”和第 7.2 节“通用网络配置”。

## 7.4.4. 推荐阅读

在以下网站可以获得额外的帮助文档：

- devdev 的用户空间实现 http://www.koah.com/linux/tools/ols_2003_udev_paper/Reprint-Koah-Hartman-OLS2003.pdf

- 文件系统映射 http://www.kernel.org/pub/kernel/people/machel/doc/papers/ols-2005/machel.pdf

- 进一步阅读指南 http://www.kernel.org/pub/linux/utils/kernel/hotplug/udev.html

## 7.5. 为设备创建自定义符号链接

### 7.5.1. CD-ROM 符号链接

你以后可能安装的一些软件（例如各种播放器）预期 `/dev/cdrom` 和 `/dev/dvd` 设备存在并指向 CD-ROM 或 DVD-ROM 设备。此外，在 `/etc/fstab` 中引用这些符号链接可能会方便。`udev` 自带了一个脚本，可以根据设备的特性为你生成这些链接，但你需要决定希望让脚本以哪种两种模式之一运行。

首先，脚本可以以 "by-path"模式运行（USB 设备使用），通过物理路径确定 CD 或 DVD 设备。其次，它可以以 "by-id"模式运行（SCSI 设备默认值），由 `udev` 读取标识字符串。每方法都有优点；正确的方法取决于你的需求。

如果你预计物理路径会发生变化（例如你可能会插入不同的端口），那么你应该使用 "by-path" 模式。相反，如果你需要符号链接保持稳定，则应该使用 "by-id" 模式。

- **重要**

外部设备（例如 USB 连接的 CD 驱动器）不应使用 by-path 持久化，因为每次设备插入新端口时，其物理路径都会发生变化。如果你编写通过物理路径识别设备的 Udev 规则，所有连接设备都会出现这个问题。

### 7.5.2. 处理重复设备

如第 7.4 节“LFS 系统上的设备和模块处理”所解释的，具有相同功能的设备在 `/dev` 中出现的顺序本质上是随机的。例如，如果你有一个 USB 摄像头和一个电视调谐器，有时 `/dev/video0` 指向摄像头而 `/dev/video1` 指向调谐器，有时在重启后顺序会反过来。对于声卡和网卡以外的所有硬件类，这都可以通过创建 udev 规则来实现持久化符号链接来解决。网卡的情况在第 7.2 节“通用网络配置”中单独介绍，声卡配置可以在 BLFS 中找到。

对于可能出现此问题的每个设备（如果该问题在你当前的 Linux 发行版中不存在），请在 `/sys/class` 或 `/sys/block` 下找到相应的目录。对于视频设备，这可能是可能是 `/sys/class/video4linux/videoX`。确定能够唯一标识设备的属性（通常是视频 ID 和产品 ID 以及/或序列号）：

```
udevadm info -a -p /sys/class/video4linux/video0

cat > /etc/rules.d/83-duplicate_devs.rules << "EOF"

# 摄像头和调谐器的持久符号链接
KERNEL==="video", ATTRS{idProduct}==="1910", ATTRS{idVendor}==="0d81", \
SYMLINK+="video", ATTRS{device}==="0x036f", ATTRS{vendor}==="0x109e", \
SYMLINK="tvtuner"

EOF
```

结果是 `/dev/video0` 和 `/dev/video` 设备仍然随机指向调谐器和摄像头（且不应直接使用它们），但存在 `/dev/tvtuner` 和 `/dev/webcam` 符号链接，它们始终指向正确的设备。

## 7.6. LFS-Bootscripts-20120229

LFS-Bootscripts 包包含一组在启动/关机时启动/停止 LFS 系统的脚本。

预计编译时间：少于 0.1 SBU

所需的磁盘空间：260 KB

### 7.6.1. 安装 LFS-Bootscripts

安装软件包：

```
make install
```

### 7.6.2. LFS-Bootscripts 的内容

- 安装的脚本：checkfs, cleanfs, console, functions, halt, ifdown, ifup, localnet, modules, mountfs, mountkernfs, network, rc, reboot, reboots, setclock, static, swapt, syscall, syslog, template, udev, and udev_retry

- 安装的目录：`/etc/rc`, `/etc/init.d`（符号链接） , `/etc/sysconfig`, `/lib/services`, `/lib/bs`（符号链接）

# 描述

- checkfs：在挂载文件系统之前检查其完整性（日志文件和网络文件系统除外）

- cleanfs：移除重启之间不应保留的文件，例如 `/var/run/` 和 `/var/lock/` 中的文件；重新创建 `/var/run/utmp` 并移除可能存在的 `/etc/login,/fastboot, 和forceck`

- console：为所需的键盘布局加载正确的键位表；它还设置了屏幕字体

- functions：包含常用函数，例如错误和状态检查，供多个启动脚本使用

- halt：停止系统

- ifdown：停止网络设备

- ifup：初始化网络设备

- localnet：设置系统的主机名和本地回环设备

- modules：加载 `/etc/sysconfig/modules` 中列出的内核模块，并使用相同的参数

- mountfs：挂载所有文件系统，标记为 noauto 或基于网络的文件系统除外

- mountkernfs：挂载虚拟内核文件系统，例如 proc

- network：设置网络接口（如网卡）并设置默认网关（适用）

- rc：主级控制脚本；它负责逐个运行所有其他启动脚本，运行顺序由处理的符号链接名称决定

- reboot：重启系统

- sendsignal：确保在系统重启或停止之前每个进程都已终止

- setclock：如果硬件时钟未设置为 UTC 时间，将内核时钟重置为本地时间

- static：提供为网络接口分配静态网协议 (IP) 地址所需的功能

- swap：启用和禁用交换文件和分区

- sysctl：如果存在 `/etc/sysctl.conf` 文件，将系统配置值加载到运行的内核中

- syslogd：启动和停止系统及内核日志守护进程

- template：用于为其他守护进程创建自定义启动脚本的模板

- udev：准备 `/dev` 目录并启动 Udev

- udev_retry：重试失败的 udev 事件，并在需要时生成的规则文件复制到 `/etc/udev/rules.d`

## 7.7. 这些启动脚本是如何工作的？

Linux 使用名为 SysInit 的特殊启动机制，它基于运行级别（run-levels）的概念。它在不同系统之间可能非常不同，因此不能假设因为在某个特定的 Linux 发行版中有效，它们在 LFS 中也应该以相同的方式工作。LFS 有它自己的处理方法，但它尊重通用的标准。

SysInit（从现在起称为 "init"）使用运行级别方案工作。共有 0 到 6 7 个运行级别（实际上有更多运行级别，但它们用于特殊情况且通常不使用，详情请见 `init (8)`），每一个级别都对应于计算机启动时应该执行的操作。默认运行级别是 3。以下是不同运行级别的描述：

- 0：停止计算机

- 1：单用户模式

- 2：无网络的多用户模式

- 3：带网络的多用户模式

- 4：留作自定义，否则与 3 相同

- 5：与 4 相同，通常用于 GUI（如 X 的 xdm 或 KDE 的 kdm）

- 6：重启计算机

### 7.7.1. 配置 Sysinit

在内核初始化期间，运行的第一个程序要么在命令行指定，要么是默认的。程序读取初始化文件 `/etc/inittab`。通过以下命令创建此文件：

```
cat >/etc/inittab << "EOF"
# Begin inittab
id:3::sysinit/rc.d/init.rc
10:0:wait/rc.d/init.rc S
11:S:wait/rc.d/init.rc
12:2:wait/rc.d/init.rc
13:3:wait/rc.d/init.rc
14:4:wait/rc.d/init.rc
15:5:wait/rc.d/init.rc
16:6:wait/rc.d/init.rc
ca:12345:ctrlalt:/bin/shutdown -r now
su:0:once:/sbin/getin
1:2345:respawn:/sbin/agetty t1
2:2345:respawn:/sbin/agetty t2
3:2345:respawn:/sbin/agetty t3
4:2345:respawn:/sbin/agetty t4
5:2345:respawn:/sbin/agetty t5
6:2345:respawn:/sbin/agetty t6
# End inittab
EOF
```

对于 LFS，该初始化文件的说明在 `inittab` 手。上述初始化文件将指示 `rc` 运行 `/etc/rc.d` 目录中所有以 S 开头的脚本，然后是 `rc?.d/` 目录（其中问号替换为默认值）。为了方便起见，`rc` 脚本读取 `/lib/init` 中的函数库。该库还读取可选配置文件 `/etc/sysconfig/`。后续章节中描述的任何系统参数都可以放在此文件中，以便汇总所有系统参数。

为了调试方便，`functions` 脚本还将所有输出记录到 `/run/log`。由于 `/run` 目录是 tmpfs，此文件在启动后是不持久的。

### 7.7.2. 更改运行级别

更改运行级别通过 `init <runlevel>` 完成，其中 `<runlevel>` 是目标运行级别。例如，用户重启计算机可以使用 `init 6`，它是 `reboot` 命令的别名。同样，`init 0` 是 `halt` 命令的别名。

`/etc/rc.d` 下有许多 `rc?.d`（其中 `?` 是运行级别数字）和 `rc.d` 目录，它们包含许多符号链接。以 K 开头，其余以 S 开头，后面跟着两个数字。K 表示停止（杀死）服务，S 表示启动服务。数字决定了脚本运行的顺序，从 00 到 99——数字越小运行越早。当 `init` 切换到另一个运行级别时，根据级别启动或停止相应的服务。

真正的脚本位于 `/etc/rc.d/init.d`。它们执行实际工作，符号链接都指向它们。K 和 S 链接指向 `/etc/rcinit.d`。这是因为脚本可以使用不同的参数（如 *start, restart, reload, status*）调用。当遇到 K 链接时，相应的脚本带有 *start* 参数运行。当遇到 S 链接时，相应的脚本也带有 *start* 参数运行。

此说明有一个例外。`rc0.d` 和 `rc6.d` 目录中以 S 开头的链接不会启动任何内容。它们将使用 stop 参数调用以停止某些内容。背后的逻辑是，当用户要重启或停止系统时，不需要启动任何东西。系统只需要停止。

这些是参数脚本执行的操作描述：

- start：启动服务。

- stop：停止服务。

- restart：停止服务然后重新启动。

- reload：更新服务的配置。这在服务的配置文件被修改后使用，此时不需要重启服务。

- status：告知服务是否正在运行以及 PID 是什么。

可以随意修改启动过程（毕竟这是你自己的 LFS 系统）。这里提供的文件是如何操作的示例。

## 7.8. 配置系统主机名

`local` 脚本的工作部分是设置系统主机名。这需要在 `/etc/sysconfig/network` 文件中配置。

创建 `/etc/sysconfig/network` 文件并运行以下命令输入主机名：

```
echo "HOSTNAME=lfs" > /etc/sysconfig/network
```

Linux From Scratch - 版本 7.1

`<hostname>` 需要替换为给该计算机指定的名称。不要输入完全限定域名 (FQDN)。该信息存放在 /etc/hosts 文件中。

## 7.9. 配置 setclock 脚本

`setclock` 脚本从硬件时钟读取时间，硬件时钟称为 BIOS 或互补金属氧化半导体 (CMOS) 时钟。如果硬件时钟设置为 UTC，它将使用 `/etc/localtime` 文件将硬件时钟时间转换为本地时间（该文件告诉 `hwclock` 程序用户所在的时区）。目前无法检测硬件时钟是否设置为 UTC，因此这需要手动配置。

当内核检测到硬件能力时，会通过 `udev` 运行 `setclock`。它也可以带有 `stop` 参数手动运行，将系统时间存储到 CMOS 时钟中。

如果你不记得硬件时钟是否设置为 UTC，可以通过运行 `hwclock --localtime --show` 来查看。这将显示根据硬件时钟当前的时刻。如果时间与你的手表显示一致，则时钟被设置为本地时间。如果 `hwclock` 的输出不是本地时间，那么你目前可能处于 UTC 时间。通过为 `hwclock` 显示的时区增加或减少相应的小时来验证这一点。例如，在 MST 时区（也称为 GMT-0700）中，在本地时间的基础上增加七小时。

如果硬件时钟未设置为 UTC，将 `UTC` 变量的值改为 0（零）。

运行以下命令创建一个新文件 `/etc/sysconfig/clock`：

```
cat > /etc/sysconfig/clock << "EOF"
# Begin /etc/sysconfig/clock
UTC=1

# 设置你可能需要提供给 hwclock 的任何选项，
# 例如针对 Alpha 的机器硬件时钟类型。
CLOCKPARAMS=

# End /etc/sysconfig/clock
EOF
```

关于如何在 LFS 中处理时间的良好提示，可以在 http://linuxfromscratch.org/hints/downloads/files/time.txt 找到。它解释了时区、UTC 和 TZ 环境变量等问题。

> 注意

> `CLOCKPARAMS` 和 `UTC` 参数也可以在 `/etc/sysconfig/rc.site` 文件中进行设置。

### 7.10. 配置 Linux 控制台

本节讨论了如何配置控制台启动脚本，该脚本设置键盘映射、控制台字体和控制台内核日志级别。如果不使用非 ASCII 字符（例如：版权符号、英镑符号和欧元符号）且键盘是美式的，则本节的大部分内容可以跳过。如果没有该配置文件（或 `rc.site` 中的等效设置），控制台启动脚本将无所作为。

Linux From Scratch - 7.1

**console** 脚本读取 `/etc/sysconfig/console` 文件以获取配置信息。各种特定语言的 HOWTO 也可以提供帮助，请参阅 http://www.tldp.org/HOWTO/HOWTO-INDEX/other-lang.html。如果仍有疑问，请查看 `/lib/kbd` 目录下的有效键映射和屏幕字体。阅读 `loadkeys(1)` 和 `setfont(8)` 页面以确定这些程序的正确参数。

`/etc/sysconfig/console` 文件应包含形如 `VARIABLE="value"` 格式的行。这些变量是可以识别的：

- LOGLEVEL

此变量设置由 **dmesg** 指定输出到控制台的内核消息日志级别。有效级别从 "0"（无消息）到 "8"。

- KEYMAP

此变量指定 **loadkeys** 程序的参数，通常是需要加载的键映射名称，例如 "us104"。如果未设置此变量，启动脚本将不会运行 **loadkeys** 程序，并将使用默认的内核键映射。

- KEYMAP_CORRECTIONS

此（未使用）变量指定第二次调用 **loadkeys** 程序的参数。如果默认键映射不完全满意并需要进行微调，可以使用此变量。

- FONT
