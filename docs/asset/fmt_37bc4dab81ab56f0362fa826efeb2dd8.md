
`/bin/` 目录包含可执行文件，`dict/` 包含不符合 FHS 标准的文档页，`etc/` 包含系统级配置文件，`games` 用于游戏，`include/` 包含头文件，`kerberos/` 包含用于 Kerberos 的二进制文件及更多内容，`lib/` 包含并非供用户或 shell 脚本直接使用的对象文件和库。`libexec/` 目录包含其他程序调用的小型辅助程序，`sbin/` 用于系统管理二进制文件（即那些不属于 `/sbin/` 目录的文件），`share/` 包含不特定架构的文件，`src/` 用于源码，`X11R/` 用于 X Window 系统（Red Hat Linux 上的 XFree86）。

### 3.2.1.9. `/usr/local/` 目录

FHS 规定：

> “`/usr/local` 层次结构由系统管理员在本地安装软件时使用。在安装软件时，它是安全的不会被覆盖。”

`/usr/local/` 目录与 `/usr/` 目录类似。它具有以下类似的子目录：

- `/usr/local`
- `bin/`
- `dict/`
- `doc/`
- `etc/`
- `games/`
- `include/`
- `lib/`
- `libexec/`
- `local/`
- `sbin/`
- `share/`
- `src/`

### 3.2.1.10. `/var/` 目录

FHS 规定 `/var/` 用于变动数据。以下是应该是 `/var/` 子目录的某些目录：

- `/var`
- `account/`
- `arpwatch/`
- `cache/`
- `crash/`
- `db/`
- `empty/`
- `ftp/`
- `gdm/`
- `kerberos/`
- `lib/`
- `local/`
- `lock/`
- `log/`
- `mail/`
- `mailman/`
- `nis/`
- `preserve/`
- `run/`
- `spool/`
- `anacron/`
- `at/`
- `cron/`
- `fax/`
- `lpd/`
- `mail/`
- `mqueue/`
- `news/`
- `pcmcia/`
- `radvd/`
- `slr/`
- `squid/`
- `update/`
- `uucp/`
- `us/`
- `vbox/`
- `voice/`
- `tmp/`
- `tux/`
- `www/`
- `yp/`

# 第 4 章

# sysconfig 目录

`/etc/sysconfig/` 目录存储了 Red Hat Linux 的各种系统配置文件。

本章概述了 `/etc/sysconfig/` 目录中的某些文件及其功能和内容。本章的信息并不完全，因为这些文件中有许多仅在非常特定或罕见的情况下使用的选项。

### 4.1. `/etc/sysconfig/` 目录下的文件

以下文件通常位于 `/etc/sysconfig/` 目录中：

- `amd`
- `apmd`
- `arpwatch`
- `authconfig`
- `cii pe`
- `clock`
- `desktop`
- `dhcpd`
- `firstboot`
- `gpm`
- `harddisks`
- `hwconf`
- `il8n`
- `identd`
- `init`
- `ipchains`
- `iptables`
- `irda`
- `keyboard`
- `kudzu`
- `mouse`
- `named`
- `netdump`
- `network`
- `npd`
- `pcmcia`
- `radvd`
- `samba`

# 第 4 章. sysconfig 目录

- `rawdevices`
- `redhat-config-securitylevel`
- `redhat-config-users`
- `redhat-logviewer`
- `samba`
- `sendmail`
- `soundcard`
- `spamassassin`
- `squid`
- `tux`
- `ups`
- `vncservers`
- `xinetd`

> 注意
> 如果列出的某些文件在 `/etc/sysconfig/` 目录中不存在，则说明相应的程序可能未安装。

### 4.1.1. `/etc/sysconfig/amd`

`/etc/sysconfig/amd` 文件包含了 `amd` 使用的各种参数，这些参数允许文件系统的自动挂载和卸载。

### 4.1.2. `/etc/sysconfig/apmd`

`/etc/sysconfig/apmd` 文件被 `apmd` 用作配置，用于设置在挂起或恢复时启动/停止的电源开关设置。它被配置为在启动时开启 `apmd`，具体取决于硬件是否支持高级电源管理 (APM) 或用户是否配置了系统使用它。`apmd` 守护进程是一个监控程序，与 Linux 内核中的电源管理代码协同工作，能够向笔记本电脑用户发出电量低的警告以及其他电源相关的设置。

### 4.1.3. `/etc/sysconfig/arpwatch`

`/etc/sysconfig/arpwatch` 文件用于在启动时向 `arpwatch` 守护进程传递参数。`arpwatch` 守护进程维护着一个以太网 MAC 地址及其 IP 地址配对的表。有关此文件可用参数的更多信息，请参阅 `arpwatch` 手页。默认情况下，此文件将 `arpwatch` 进程的所有者设置为用户 `pcap`。

### 4.1.4. `/etc/sysconfig/authconfig`

`/etc/sysconfig/authconfig` 文件设置了主机上将使用的授权类型。它包含以下一行或多行：

- `USEMD5=<value>`，其中 `<value>` 是以下值之一：
  - `yes` — 不使用 MD5 进行认证。
  - `no` — 不使用 MD5 进行认证。

- `USERKERBOS=<value>`，其中 `<value>` 是以下值之一：
  - `yes` — 使用 Kerberos 进行认证。
  - `no` — 不使用 Kerberos 进行认证。

- `USELDAPUTH=<value>`，其中 `<value>` 是以下值之一：
  - `yes` — 使用 LDAP 进行认证。
  - `no` — 不使用 LDAP 进行认证。

### 4.1.5. `/etc/sysconfig/clock`

`/etc/sysconfig/clock` 文件控制对从系统硬件时钟读取的值的解释。

正确的值为：

- `UTC=<value>`，其中 `<value>` 是以下布尔值之一：
  - `true` or `yes` — 硬件时钟设置为通用时间 (UTC)。
  - `false` or `no` — 硬件时钟设置为本地时间。

- `ARC=<value>`，其中 `<value>` 为以下内容：
  - `true` or `yes` — ARC 控制台的 42 年时间偏移生效。此设置仅适用于基于 ARC 或 AlphaBIOS 的系统。任何其他值均表示使用标准的 UNIX 纪（epoch）。

- `SRM=<value>`，其中 `<value>` 为以下内容：
  - `true` or `yes` — SRM 控制台的 1900 纪生效。此设置仅适用于基于 SRM 的系统。任何其他值均表示使用标准的 UNIX 纪。

- `ZONE=<filename>` — `/usr/share/zoneinfo` 下的时区文件，`/etc/localtime` 是它的副本。该文件包含如下信息：
  `ZONE="America/New York"`

较早版本的 Red Linux 使用以下值（已废弃）：

- `CLOCKMODE=<value>`，其中 `<value>` 是以下值之一：
  - `GMT` — 时钟设置为通用时间（格林威治标准时间）。
  - `ARC` — ARC 控制台的 42 年时间偏移生效（仅用于基于 Alpha 的系统）。

### 4.1.6. `/etc/sysconfig/desktop`

`/etc/sysconfig/desktop` 文件指定了要运行的桌面管理器，例如：

`DESKTOP="GNOME"`

`/etc/sysconfig/dhcpd` 文件用于在启动时向 `dhcpd` 守护进程传递参数。`dhcpd` 守护进程实现了动态主机配置协议 (DHCP) 和互联网引导协议 (BOOT)。DHCP 和 BOOT 为网络上的机器分配主机名。有关此此文件中可用参数的更多信息，请参阅 `dhcpd` 手页。

在 Red Hat Linux 8.0 中，系统首次启动时，`/sbin/init` 程序会调用 `/etc/rc.d/init.d/firstboot` 脚本，该脚本会启动 Setup Agent。此应用程序允许用户安装最新的更新以及额外的应用程序和文档。`/etc/sysconfig/firstboot` 文件告诉 Setup Agent 在随后的启动时不运行。若要仅在系统启动时运行，请删除 `/etc/sysconfig/firstboot` 并执行 `chconfig --level=5 firstboot on`。

`/etc/sysconfig/gpm` 文件用于在启动时向 `gpm` 守护进程传递参数。`gpm` 守护进程是鼠标服务器，允许鼠标加速和中键点击粘贴。有关此文件中可用参数的更多信息，请参阅 `gpm` 手页。默认情况下，它将鼠标设备设置为 `/dev/mouse`。

`/etc/sysconfig/harddisks` 用于调整硬盘。管理员还可以使用 `/etc/sysconfig/harddisks` 为特定驱动器配置参数。在没有仔细考虑的情况下不要修改此文件。通过更改默认值，可能会损坏硬盘上的所有数据。`/etc/sysconfig/harddisks` 文件可能包含内容：

- `USE_DMA=1`，将此值设置为 1 可启用 DMA。然而，在某些芯片组和硬盘的组合下，DMA 可能会导致损坏。
- `Multiple_IO=16`，设置为 16 允许每次 I/O 多个扇。启用此功能后，系统开销将减少 50%。
- `EIDE_32BIT=3` 启用 (EIDE) 32 位支持。
- `LOOKHEAD=1` 启用预读。
- `EXTRA_PARAMS=` 指定可以添加的额外参数。

### 4.1.11. `/etc/sysconfig/hwconf`

`/etc/sysconfig/hwconf` 文件列出了系统上检测的所有硬件，以及使用的驱动程序、供应商 ID 和设备信息。该程序检测并配置系统上新增或更改的硬件。`/etc/sysconfig/hwconf` 文件不用于手动编辑。如果进行编辑，设备可能会显示为已添加或删除。

### 4.1.12. `/etc/sysconfig/i18n`

`/etc/sysconfig/i18n` 文件设置语言。
