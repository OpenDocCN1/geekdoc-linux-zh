
查找新软件的首选位置是发行版的软件库（参见第 15 章）。使用内置的软件安装工具来安装新应用程序，你就知道自己是安全的。如果你无法在发行版的软件库中找到该应用程序，请查找由受信任来源打包的软件包。确保你和你 Linux 系统的其他用户对所使用的网站感到放心。你需要制定一个`列表`，列出那些提供你所需信息且表述不具误导性的受信任网站。作为起点，如果你的 Linux 发行版衍生自某个核心发行版（例如 Ubuntu 衍生自 Debian Linux），你可以信任父发行版的软件库。其他受信任的软件分发网站包括 GitHub 和 SourceForge——这两个网站都致力于分发开源软件。如果你或你 Linux 系统的用户不确定是否信任某个特定网站，请做一些研究，或者询问他人的意见。

第 15 章还详细介绍了如何保持你的发行版及其软件通过安全补丁保持最新。随着时间的推移，即使是最受欢迎的软件包也会被发现有安全漏洞。请务必关注安全更新并安装它们！毕竟，作为负责人，你的工作是确保这台计算机不被入侵者侵入。除了确保你在用户账户和超级用户（root）账户上执行与用户相同的所有操作之外，无论你运行的是哪个 Linux 发行版，你都必须密切关注安全问题并保持更新。

## 网络漏洞

在 Linux 服务器或工作站上——或者任何使用任何操作系统的计算机上——你不应该运行任何你并不打算使用的网络服务。把每个正在运行的网络程序想象成你房子上的玻璃窗或滑动玻璃门。每个网络服务都是一个弱点，互联网上有许多心怀不轨的人喜欢走访所有房屋，记下有多少窗户和玻璃门，它们是什么类型，以及入侵它们有多容易。

## 控制你的服务

你在系统上安装的软件越多，后台运行的服务可能就越多。Ubuntu 和 openSUSE 都提供了一种实用程序来控制系统自动启动的应用程序。

Ubuntu 和 openSUSE 都使用 `systemd` 软件来启动服务。虽然 openSUSE 提供了管理服务的图形工具，但 Ubuntu 没有。然而，在这两个系统中，你都可以使用 `systemctl` 命令行命令来

查看和管理系统服务。要查看当前在 Ubuntu 或 openSUSE 系统上运行的服务列表，只需使用以下命令：

```
$ systemctl list-units --all --state running
UNIT LOAD ACTIVE SUB DESCRIPTION
cups.path loaded active running CUPS Scheduler
init.scope loaded active running System and Service Manager
session-2.scope loaded active running Session 2 of user rich
auditd.service loaded active running Security Auditing Service
avahi-daemon.service loaded active running Avahi mDNS/DNS-SD Stack
chronyd.service loaded active running NTP client/Server
cron.service loaded active running Command Scheduler
cups.service loaded active running CUPS Scheduler
dbus.service loaded active running D-Bus System Message Bus
display-manager.service loaded active running X Display Manager
firewalld.service loaded active running firewalld - dynamic firewall daemon
getty@tty1.service loaded active running Getty on tty1
haveged.service loaded active running Entropy Daemon based on the HAVEGE algorithm
lvm2-lvmetad.service loaded active running LVM2 metadata daemon
ModeManager.service loaded active running Mode Manager
NetworkManager.service loaded active running Network Manager
nsmd.service loaded active running Name Service Cache Daemon
polkit.service loaded active running Authorization Manager
postfix.service loaded active running Postfix Mail Transport Agent
rsyslog.service loaded active running System Logging Service
rtkit-daemon.service loaded active running Realtime Scheduling Policy Service
sshd.service loaded active running OpenSSH Daemon
systemd-journald.service loaded active running Journal Service
systemd-logind.service loaded active running Login Service
systemd-udev.service loaded active running udev Kernel Device Manager
udisks2.service loaded active running Disk Manager
upower.service loaded active running Daemon for power management
user@1000.service loaded active running User Manager for UID 1000
avahi-daemon.socket loaded active running Avahi mDNS/DNS-SD Stack Activation Socket
cups.socket loaded active running CUPS Scheduler
dbus.socket loaded active running D-Bus System Message Bus Socket
lvm2-lvmetad.socket loaded active running LVM2 metadata daemon socket
syslog.socket       loaded active running Syslog Socket
systemd-journald-dev-log.socket  loaded active running Journal Socket (/dev/log)
systemd-journald.socket  loaded active running Journal Socket
systemd-udevd-control.socket  loaded active running udev Control Socket
systemd-udevd-kernel.socket  loaded active running udev Kernel Socket

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.

37 loaded units listed.
To show all installed unit files use `systemctl list-unit-files`.
lines 18-45/45 (END)
$ 
```

如您所见，Linux 系统上运行着相当多的服务！在尝试禁用任何服务之前，请确保您已经查询了它们的具体功能，并确定您的系统不需要它们。描述（Description）列可以为您提供一些线索，告诉您在哪里可以找到有关该服务的更多信息。您可能还记得第 17 章中的 CUPS 服务，或者第 9 章中的 NetworkManager 服务。请查阅您特定的 Linux 发行版的文档，查看哪些服务应当默认运行。

如果您确实发现了一些不希望其运行的服务，请使用 `systemctl` 命令来禁用它们：
