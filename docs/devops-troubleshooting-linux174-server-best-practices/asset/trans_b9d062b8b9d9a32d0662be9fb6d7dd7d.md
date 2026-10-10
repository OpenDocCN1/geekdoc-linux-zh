
使用未插入网线启动的系统。你可以创建一个当网线插入时触发的 Upstart 脚本。该脚本随后可以为你重启网络服务。然后，你可以配置那些需要网络连接的服务，使其在网络服务成功启动时触发。这样，当系统启动时，你只需插入网线，Upstart 脚本就会处理其余的工作。

Upstart 目前尚未完全取代 System V init，至少在系统服务方面如此。目前，Upstart 替代了 init 和 /etc/inittab 文件的功能，并管理运行级别的变化、系统的启动和关闭，以及控制台 ttys。越来越多的核心功能正在移植到 Upstart 脚本中，但你仍会在 /etc/init.d 中找到一些标准的 init 脚本，并在 /etc/rc?.d 中找到所有的标准符号链接。不同之处在于，Upstart 现在会在运行级别变化时启动和停止服务。

Upstart 脚本位于 /etc/init，由于它们实际上不是 shell 脚本，因此语法与 init 脚本有所不同。为了说明语法，这里有一个用于在运行级别之间切换的示例 Upstart 脚本（/etc/init/rc.conf）：

```
# rc - System V runlevel compatibility
#
# This task runs the old System V-style rc script when changing
# between runlevels.

description     "System V runlevel compatibility"
author          "Scott James Remnant <scott@netsplit.com>"
start on runlevel [0123456]
stop on runlevel [!15RUNLEVEL]
export RUNLEVEL
export PREVLEVEL
task
exec /etc/init.d/rc $RUNLEVEL
```

Upstart 将 `#` 开头的行视为注释，就像大多数其他脚本和配置文件一样。前两个配置选项是 `start on` 和 `stop on`。这些行定义了脚本启动和停止所需发生的事件。在这种情况下，当进入任何运行级别时脚本将启动，当运行级别未设置时脚本将停止。

接下来的几行导出了一些环境变量，然后 `task` 选项告诉 init 此脚本不是持久性的——它将执行然后停止。

Upstart 脚本中实际运行的程序由 `script` 或 `exec` 选项定义。对于 `exec` 选项，Upstart 执行 `exec` 选项后的命令及其所有参数，并跟踪其 PID。对于 `script` 选项，Upstart 将后续行视为 shell 脚本，直到达到 `end script` 行。

尽管 Upstart 旨在是事件驱动的，但它仍然提供了检查 Upstart 作业状态以及根据需要启动和停止它们的方法。你可以使用命名适当的 `status`、`start` 和 `stop` 命令来检查、启动和停止 Upstart 脚本。Ubuntu 服务器上的一个 Upstart 作业是 `tty1` 作业，它在 tty1 上启动 `getty` 程序。这为管理员按 Alt-F1 时提供了一个控制台。然而，假设由于某种原因你认为控制台挂起了。以下是检查状态然后重启作业的方法：

```
$ sudo status tty1
tty1: start/running, process 789
$ sudo stop tty1
tty1 stop/waiting
$ sudo start tty1
tty1 start/running, process 2251
```

你还可以使用 `initctl list` 查询所有可用 Upstart 作业的状态：

```
$ sudo initctl list
mountall-net stop/waiting
rc stop/waiting
rsyslog start/running, process 640
tty4 start/running, process 708
udev start/running, process 299
upstart-udev-bridge start/running, process 297
userdata-other stop/waiting
apport start/running
hwclock-save stop/waiting
irbalance stop/waiting
plymouth-log stop/waiting
tty5 start/running, process 713
atd start/running, process 727
failsafe-x stop/waiting
plymouth stop/waiting
ssh start/running, process 1210
control-alt-delete stop/waiting
hwclock stop/waiting
module-init-tools stop/waiting
cron start/running, process 728
mountall stop/waiting
rc5 stop/waiting
ufw start/running
mounted-varrun stop/waiting
rc-sysinit stop/waiting
tty2 start/running, process 717
udevtrigger stop/waiting
mounted-dev stop/waiting
tty3 start/running, process 718
udev-finish stop/waiting
hostname stop/waiting
mountall-reboot stop/waiting
mountall-shell stop/waiting
mounted-tmp stop/waiting
network-interface (lo) start/running
network-interface (eth0) start/running
plymouth-splash stop/waiting
tty1 start/running, process 2251
udemonitor stop/waiting
dmesg stop/waiting
network-interface-security start/running
networking stop/waiting
procps stop/waiting
tty6 start/running, process 720
ureadahead stop/waiting
```

## BIOS 启动顺序

如果你的系统甚至无法到达 GRUB 提示符（但之前可以），那么要么 GRUB 已从 MBR 中完全移除，要么你的硬盘已崩溃无法识别，或者 BIOS 中的启动顺序已更改。由于这是最简单和最快的修复方法，我们将首先从如何修复启动顺序开始。这种情况通常发生在有人调整 BIOS 启动顺序以便从其他媒体（如 USB 密钥、CD-ROM 或通过网络）启动，完成后忘记恢复原状时。

BIOS 提供了一种在系统开机时更改其设置的方法——通过按下键盘上的特殊键。许多 BIOS 还允许你按不同的键并选择从哪个设备启动。不幸的是，制造商似乎无法就按下哪个键来进入任一选项达成一致，但幸运的是，大多数 BIOS 会在系统开机时在显示器上显示它们使用的按键。当然，重点在于快速启动时间，因此许多 BIOS 会快速闪过此屏幕。如果你运气好，你的 BIOS 会在屏幕上显示一个简短的通知（通常在你的显示器开始显示内容的时机），提示你按一个键（通常是 Del、F1、F2 或 Esc）来配置 BIOS。你可能还会看到一个提示，让你按另一个键（通常是 F11 或 F12）来更改 BIOS 启动顺序或仅为本次启动选择启动设备。

由于我们要排除 BIOS 启动顺序是否是我们问题的原因，如果你的 BIOS 允许你在运行中实时选择启动顺序，请首先选择该选项。否则，按下配置 BIOS 的键，前往允许你编辑启动顺序的屏幕（通常标记为 Boot，如果没有，你可以在 Advanced 中找到）。每个制造商的 BIOS 都略有不同，因此你可能需要四处查看以找到正确的选项。

无论你选择的是临时启动设备还是处于 BIOS 配置中，你应该看到一个你可以从中启动的可能设备列表。在大多数服务器上，这将是某种类型的硬盘，因此找到第一个硬盘选项并选择它。如果该驱动器正常启动，你就找到了正确的驱动器；否则，重置系统并尝试每个启动设备，直到找到可用的那个。如果你能够找到一个可以启动的驱动器，不要忘记返回 BIOS 配置屏幕，确认启动顺序将该驱动器置于其他驱动器之前。

如果没有任何驱动器能让你看到 GRUB 提示符，那么要么 GRUB 已被完全擦除，要么你的主磁盘或磁盘控制器已故障。首先，按照下一节的步骤尝试修复 GRUB，因为这些步骤将帮助你使用救援磁盘来确定磁盘是否可用。如果磁盘完全不可用，你可能需要参考第 10 章，该章讨论了如何硬件故障。

## 修复 GRUB

识别和修复 GRUB 问题的难点在于，如果没有一个功能正常的引导加载器，你就无法启动系统并使用修复 GRUB 所需的工具。GRUB 在系统中可能出现几种不同的损坏方式，但在讨论这些之前，你应该理解，为了快速启动，某些系统设置 GRUB 具有仅几秒钟的短超时，然后启动默认操作系统，即使在服务器上也是如此。更糟糕的是，某些系统甚至隐藏了初始 GRUB 提示符，因此你需要在 BIOS 将控制权交给 GRUB 后的一两秒内按下一个特殊键（GRUB 1 版本按 Esc，也称为 GRUB legacy；GRUB 2 版本按 Shift，也称为 GRUB）。

如果你不知道自己安装的是哪个版本的 GRUB，你可能需要启动系统几次并尝试 Esc 和 Shift，看看能否显示某种 GRUB 窗口。在那之后，你可能仍需要处理 GRUB 启动默认操作系统之前的短超时，因此你需要按下一个键（方向键通常很安全）来禁用超时。以下部分讨论了 GRUB 损坏的几种方式，然后随后介绍了一些通用的修复方法。

### 没有 GRUB 提示符

GRUB 在你的系统中损坏的第一种可能是它已从你的 MBR 中完全移除。不幸的是，由于 GRUB 即使在正常工作时也常对用户隐藏，你可能无法判断 GRUB 是配置错误还是根本没有安装。通过按 Esc 或 Shift 键来测试，确认在启动过程中没有 GRUB 提示符出现。

