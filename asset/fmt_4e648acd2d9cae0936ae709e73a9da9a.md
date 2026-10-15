
输入以下内容（假设你正在使用 bash 或 sh shell）：
```
# export DISPLAY=:0
```

此时，你可以运行任何管理命令（例如 `neat system-config-packages`）并让它显示在你的 X 桌面面上。如果你从远程计算机运行管理命令，并希望它显示在你的本地桌面上，你可以将 `DISPLAY` 设置为 `:host:0`，其中 `host` 被替换为计算机的名称。

完成后，请务必退出你正在运行的应用程序。然后通过输入以下命令来恢复你 X 桌面的安全性：
```
$ xhost -
```

了解 GUI 管理工具、命令和文件的所在位置以及如何使用它们，将帮助你有效地维护 Linux 系统。虽然大多数管理功能是为 root 用户引入的，但其他管理用户（在本节稍后描述）具有有限的管理能力。

## 使用图形化管理工具

过去几个版本 Fedora 和 Red Hat Enterprise Linux 的趋势是避开庞大的管理界面（如 linuxconf 和 Webmin），转而提供执行单个管理任务的图形化窗口。它们不再共享一个单体界面，而是共享通用菜单。可以从菜单启动配置网络、添加用户或设置打印机的单个图形化窗口。

若要通过 GNOME 或 KDE 桌面管理你的 Fedora 或 RHEL 系统，Red Hat, Inc 拥有一套常用的管理工具，可以通过面板上的按钮访问。启动图形化管理窗口的选择可以在以下菜单中找到：

- 管理（Administration）——从 GNOME 桌面面板选择 System -> Administration（在 KDE 菜单中为 Administration），以选择用于配置配置的工具。这些工具包括添加用户、设置日期和时间、配置网络、设置打印机以及让声卡和打印机正常工作。
- 系统工具（System Tools）——从 GNOME 桌面面板（或 KDE 菜单）选择 Applications -> System Tools，以选择监控和处理系统的工具。这些工具包括更新软件、监控系统和检查网络活动的工具。

由于这些管理任务需要 root 权限，如果你以普通用户身份登录，在 GUI 应用程序打开之前必须输入 root 密码。例如，如果你以普通用户从桌面面板启动显示设置窗口（System -> Administration -> Display），你会看到图 10-1 所示的弹出窗口。

![](img/74f214fbb2938b570bec5f957507ac66_445_0.png)

**图 10-1：** 从普通用户的 GUI 输入 root 密码以打开系统管理窗口。

输入 root 密码后，大多数系统配置工具将打开，无需在本次登录会话期间重新输入密码。寻找面板右下角的黄色“徽章”，它表示你拥有 root 授权。点击徽章可以打开一个弹出窗口，允许你移除授权。否则，将在五分钟后消失。

当你在 Fedora 或 Red Hat Linux 系统上配置不同的功能时，系统会要求你启动不同的单个图形化窗口。通常情况下，如果你有配置服务器或添加功能的工具供选择，我建议你使用发行版自带的工具。因为 Red Hat 的 GUI 工具更紧密地集成到 Fedora 和 RHEL 系统存储和管理其配置信息的方式中。

以下列表描述了你可以从管理菜单（System -> Administration）启动的管理工具。括号中显示了获取该功能所需的安装包名称：

- 服务器设置（Server Settings）——此子菜单访问以下服务器配置窗口：
  - 域名系统 (`system-config-bind`)——如果你的计算机作为 DNS 服务器运行，则创建并配置区域。
  - HTTP (`system-config-httpd`)——将你的计算机配置为 Apache Web 服务器。
  - NFS (`system-config-nfs`)——设置你的系统目录，通过 NFS 服务与网络上的其他计算机共享。
  - `Samba` (`system-config-samba`)——配置 Windows (SMB) 文件共享。（若要配置其他 Samba 功能，你可以使用 SWAT 窗口。SWAT 在第 18 章中描述。）
  - `服务` (`system-config-services`)——显示并更改在你的 Fedora 或 RHEL 系统上以不同运行级别运行的服务。
  - `身份验证` (`auth-config-gtk`)——更改用户在系统上进行身份验证的方式。通常选择 Shadow 密码和 MD5 密码。如果你的网络支持 LDAP、Kerberos、SMB、NIS 或 Hesiod 身份验证，可以使用其中任何身份验证类型。
  - `日期与时间` (`system-config-date`)——设置日期和时间，或选择让 NTP 服务器系统同步。图 10-2 显示日期/时间属性窗口。

![](img/74f214fbb2938b570bec5f957507ac66_446_0.png)

图 10-2：选择 NTP 服务器或设置日期和时间。
- `显示` (`system-config-display`)——更改你的 X 桌面的设置，包括色彩深度和分辨率。你还可以选择显卡和显示器的设置。
- `防火墙和 SELinux` (`system-config-securitylevel`)——配置防火墙以允许或拒绝网络服务。还可以启用或禁用由 SELinux 支持的各种服务。
- `硬件` (`hwbrowser`)——查看硬盘、网络设备、声卡和其他硬件的信息。（安装 `hwbrowser` 包以查看此项。）
- `键盘` (`system-config-keyboard`)——根据语言选择你使用的键盘类型。
- `语言` (`system-config-language`)——选择系统的默认语言。
- 逻辑卷管理 (`system-config-lvm`)—显示并管理逻辑卷及相关的分区。
- 登录界面 (`gdm`)——控制你登录界面的外观和行为。
- 网络 (`system-config-network`)——管理你当前的网络接口。
- 打印 (`system-config-printer`)——配置本地和网络打印机。
- Root 密码 (`system-config-rootpassword`)—更改 root 密码。
- SELinux 管理 (`system-config-selinux`)—设置 SELinux 强制模式和默认策略。
- SELinux 故障排除 (`setrouhoot-server`)—监控并诊断 SELinux AVC 拒绝。
- 声卡检测 (`system-config-soundcard`)—尝试检测并配置你的音频。
- 系统日志 (`gnome-utils`)——按日期显示存储在 `/var/log` 目录下的日志文件。
- 用户与组 (`system-config-users`)——允许你添加或修改 Fedora 或 RHEL 系统的用户和组帐户（见图 10-3）。

![](img/74f214fbb2938b570bec5f957507ac66_447_0.png)

图 10-3：使用用户管理器更改用户和组帐户。

以下与系统管理相关的工具可以在系统工具菜单（Applications -> System Tools）启动：

- 软件更新 (`puret`)—从 Fedora 或 RHEL 发行版或第三方源更新软件包。
- 配置编辑器 (`gconf-editor`)—更改与你的 GNOME 桌面系统相关的设置。
- 磁盘使用分析器 (`gnome-utils`)—显示并分析计算机硬盘使用情况的数据。

## 第 10 章：理解系统管理

- `Kickstart` (`system-config-kickstart`) — 创建一个 Kickstart 配置文件，可用于在无人干预安装 Fedora 或 RHEL 系统。
- 系统监视器 (`frysk-gnome`) — 显示运行进程和资源使用情况的信息。

另一个从“系统工具”(System Tools) 菜单直接移动到“应用程序”(Applications) 菜单的系统管理应用是“添加/删除软件”(pirut) 应用程序。书中将介绍各种系统图形化管理工具的操作步骤。

## 管理命令

许多命令仅供 root 使用。当你以 root 身份登录时，你的 `$PATH` 变量会被设置为包含一些含有 root 用户命令的目录。这些包括以下目录：

- `/sbin` — 包含修改磁盘分区（如 `fdisk`）、更改启动程序（`grub`）以及更改系统状态（`init`）的命令。
- `/usr/sbin` — 包含管理用户账户（如 `useradd`）和检查网络流量（`wireshark`）的命令。作为守护进程运行的命令也在此目录中。（寻找以“d”开头的命令，如 `sshd`、`pppd` 和 `crond`。）

一些管理命令包含在普通用户目录（如 `/bin` 和 `/usr/bin`）中。对于所有人都可某些选项的命令尤为如此。例如 `/bin/mount` 命令，任何人都可以用它列出文件系统，但只有 root 可以用它挂载文件系统。

要查找主要为系统管理员设计的命令，请查看第 8 节 man 页面（通常在 `/usr/share/man/man8`）。它们包含了更多 Linux 管理命令的描述和选项。例如，要查看 `fdisk` 命令的 man 页面（`/usr/share/man/man8/fdisk.8.gz`），输入：
```
