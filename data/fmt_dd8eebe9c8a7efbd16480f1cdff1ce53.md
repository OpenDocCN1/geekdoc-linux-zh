
### 清单 24.7：使用 `ldd` 和 `grep` 发现最近升级的库

```bash
$ which ssh
/usr/bin/ssh
$
$ ldd /usr/bin/ssh > lib.txt
$
$ cat lib.txt
[...]
libk5crypto.so.3 [...]
[...]
$
$ grep -B 2 -A 2 libk5crypto /var/log/apt/history.log
Start-Date: 2019-01-22 13:37:45
CommandLine: /usr/bin/unattended-upgrade
Upgrade: libk5crypto3:amd64 (1.16-2build1, 1.16-2ubuntu0.1)
End-Date: 2019-01-22 13:37:49
$
```

本示例中使用的应用程序是 OpenSSH 的 `ssh` 程序。注意其中一个库最近被升级了。（`grep` 命令中的 `-B` 和 `-A` 选项允许你提取匹配内容上下方额外的行。）如果问题恰好在库升级后不久出现，那你就找到了一个可能的原因。请检查该库是否有新的升级版本或补丁。如果没有，你可能需要卸载该库并安装较早版本。

## 探索环境变量问题

如果你新安装的应用程序无法运行，请检查 `PATH` 环境变量。该变量决定了 `Bash` shell 直接处理之外需要搜索哪些目录以查找程序。显示该变量内容的示例见清单 24.8。

### 清单 24.8：查看 `PATH` 环境变量

```bash
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:
/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
$
```

如果需要为所有用户修改此参数，请在 `/etc/profile.d/` 目录中创建一个 `Bash` 脚本文件（`Bash` 脚本在第 25 章“部署 Bash 脚本”中有介绍）。务必使用 `.sh` 文件扩展名。该文件的所有者必须是 `root`，并且属于 `root` 组。将该文件的其他（world）权限设置为 `r`，以便所有用户都能读取该文件。该脚本会在用户登录系统或启动新 shell 时由 `/etc/profile` 或 `/etc/bashrc` 文件读取，具体取决于你的发行版。

如果只有部分用户需要此特定的 `PATH` 修改，请在他们的 `~/.profile`、`~/.bash_profile` 或 `~/.bash_login` 文件中进行修改。环境变量文件在第 10 章“管理用户和组”中已有讨论。

## 获取 GCC 兼容性

在 Linux 中用于编译程序的最常见工具是 GNU 编译器集合（`GCC`）。如果你在 Linux 上使用 `GCC` 编译应用程序时遇到问题，可能有多种潜在原因。它们如下：

- `GCC` 使用系统 C 库，该库可能不符合 ISO C 标准。

- GNU C 与 ISO 之外的 C 版本之间存在一些显著的不兼容性。

- `GCC` 使用经过修正的系统头文件版本，这也可能导致问题。

请注意，除了上述问题外，你可能正在使用较旧版本的 `gcc`，需要更新它。例如，如果你的系统发行版是 `CentOS 7`，且正在使用 `gcc v4.4.*`，则需要升级 `GCC` 包。

你可以在 `GCC` 编译器的官方网站——[https://gcc.gnu.org](https://gcc.gnu.org) 上找到详细文档。该网站包含常见问题解答（FAQs）和其他有用信息。

## 追踪软件仓库问题

当你收到有关找不到、无法更新或无法安装包的奇怪错误消息时，首先要检查的是网络连接。通常，未连接网络是导致此问题的原因。然而，各种软件包仓库（也称为 `repos`）也可能变得损坏。

在使用 `Debian` 包管理器的系统上，如 `Ubuntu`，如果收到无法下载仓库信息或类似消息，请使用 `apt-get clean` 命令。该命令清理数据库和任何临时下载文件。之后，尝试使用 `apt-get update` 更新本地仓库，该命令会尝试获取仓库中软件包的最新信息。

> 在使用 `Debian` 包管理系统的系统中，建议使用 `apt-get dist-upgrade` 命令代替 `apt-get upgrade` 来更新系统的所有软件包。`dist-upgrade` 会防止任何软件升级导致依赖包损坏。

在使用 `Red Hat` 包管理器的系统上，如 `Rocky Linux`，根据你的发行版，你可以使用 `yum` 的 `clean all` 或 `zypper clean -a` 命令。接下来，使用 `yum check-update` 或 `zypper refresh` 命令更新本地仓库。

如果你正在尝试从非标准仓库安装或更新软件包，你可能需要在你的系统上启用该仓库。要查看系统上已启用的仓库列表，在 `Red Hat` 包系统上使用 `yum repolist` 或 `zypper repos` 命令。对于 `Debian` 包系统，你需要执行 `grep -v "#" /etc/apt/sources.list` 命令来查看已启用的仓库。

在添加任何额外的非标准仓库之前，请备份仓库文件，例如以下这些：

- `/etc/apt/sources.list`

- `/etc/yum.repos.d/*.*`

- `/etc/zypp/repos.d/*.*`

你需要手动编辑 `sources.list` 文件来添加并启用新仓库。要使用 `YUM` 添加并启用新仓库，请使用 `yum-config-manager --add-repo repository-url` 命令。`zypper` 命令类似，但还需要仓库名称别名——`zypper addrepo repository-url aliases`。

请记住，我们只触及了程序和它们的各类依赖关系中更常见的几个问题。请务必使用你发行版的 `man` 页面获取更多帮助。

## 检查 SELinux 上下文违规

应用程序问题可能由你系统的 Linux 内核安全模块引起，例如 `SELinux`（在第 15 章中有介绍）。不正确的策略配置会触发违规，从而阻止应用程序发挥其作用。首先使用 `sealert` 命令检查审计日志文件。如果该工具不可用，你可以通过安装 `setroubleshoot` 包来获取它。

错误标记的文件可能会导致问题，例如应用程序被拒绝访问。使用 `ls -Z` 命令查看文件的 `SELinux` 上下文。如果它或其父目录需要更改上下文，请使用 `chcon` 实用工具进行临时修改，使用 `semanage` 命令使其永久生效，并使用 `restorecon` 修复标签。别忘了使用这三个命令，否则问题无法解决。

![](img/c0a399aca0d18f8822d714ad0a173123_747_0.png)

你可以使用超级用户权限通过 `setenforce permissive` 命令将 `SELinux` 的模式从强制（`enforcing`）暂时更改为宽容（`permissive`）。这允许你进行上下文更改，并查看是否触发任何违规，而实际不会阻止访问。一旦你配置了正确的 `SELinux` 策略，使用 `setenforce enforcing` 命令将其恢复为强制模式。

受 `SELinux` 限制的应用程序需要设置适当的布尔值（Booleans）以允许适当的访问。`getsebool` 命令允许你查看应用程序的布尔值。如果需要更改它们，请使用超级用户权限和 `setsebool` 命令。

![](img/c0a399aca0d18f8822d714ad0a173123_747_1.png)

如果你在日志或日志文件中发现大量 `SELinux` 上下文违规，而过去并未出现应用程序问题，则有可能你的系统存在入侵者。请使用入侵检测工具进行确认。

## 探索防火墙阻挡

如果应用程序在网络中出现问题，且没有网络故障，你可能需要检查本地和远程系统的防火墙。任何应用程序更新或防火墙修改都可能触发此问题。防火墙在第 18 章“监管 Linux 防火墙”中已有介绍。

### 解除 ACL 限制

防火墙 `ACL` 通过审查其控制信息以及其他网络数据来识别网络数据包。因此，在排查与防火墙相关的应用程序问题时，你需要收集往返的应用程序数据包的以下信息：

- 源地址或主机名

- 目标地址或主机名

- 使用的网络协议

- 使用的入站端口

- 使用的出站端口

你还必须知道你的源系统和目标系统所使用的防火墙应用。收集到这些信息后，你可以审查两侧的防火墙设置，以确定 `ACL` 是否过于严格。

例如，如果你的应用程序主机系统使用 `firewalld`，你可以快速检查当前默认区域，如清单 24.9 所示。

### 清单 24.9：使用 `firewall-cmd` 命令查看默认区域

```bash
$ firewall-cmd --get-default-zone
drop
$
```

注意该系统将 `firewalld` 默认设置为 `drop` 区域。这意味着所有入站网络数据包都会被丢弃，只允许出站网络连接。如果应用程序接收来自其他系统的数据或连接，则此防火墙 `ACL` 设置过于严格。

### 解除端口封锁

如果应用程序依赖于另一个系统服务（守护进程），您就需要检查与该服务端口相关的规则。封锁外部服务所需的端口会对应用程序产生不利影响。如果您的应用程序设计使用未分配给知名服务的端口，也请进行检查。

例如，如果您在系统上提供公共 `Web` 服务，您需要允许与 `HTTPS` 协议 `443` 端口相关的入站和出站数据包。如果系统使用的是 `iptables` 防火墙软件，可以通过 `iptables -L` 命令查看当前的 `ACL` 规则。如果包过滤器通过特定规则或策略封锁了 `443` 端口，您可以使用类似清单 24.10 中的命令修改链，以开放 `443` 端口。

### 清单 24.10：使用 `iptables` 命令修改防火墙

```bash
$ iptables -A INPUT -p tcp --dport 443 -j ACCEPT
$
```

请记住，您还需要修改 `OUTPUT` 链规则，以便 `Web` 服务器能够建立连接。此外，如果应用程序允许 `HTTP` 流量，还必须修改 `80` 端口的规则。

![](img/c0a399aca0d18f8822d714ad0a173123_748_0.png)

在调查应用程序问题时，请查看防火墙日志文件条目。如有必要，通常可以增加记录的信息量。例如，`UFW` 防火墙有一个 `full` 设置，可以记录所有内容。

### 解除协议封锁

除了端口，还要了解应用程序使用的各种协议，如 `UDP`、`TCP` 和 `ICMP`。如果使用其他系统服务，还必须知道其使用的协议。`/etc/services` 文件可以提供帮助。

例如，假设应用程序正在与本地网络上的 `DNS` 缓存服务器协作。`DNS` 协议使用 `53` 端口。检查 `/etc/services`（知名端口）文件以找到其使用的传输协议，如清单 24.11 中的摘录所示。

### 清单 24.11：在 `/etc/services` 文件中检查 `DNS` 的协议

```bash
$ grep 53 /etc/services

domain        53/tcp # Domain Name Server
domain        53/udp
$
```

在 `DNS` 服务器系统上同时通过 `TCP` 和 `UDP` 解除 `53` 端口的封锁，因为 `DNS` 使用这两种传输协议监听请求。此外，对于入站和出站数据包，也请解除封锁。

## 排查其他硬件问题

Linux 需要硬件才能运行。当硬件停止正常工作时，Linux 无法正常运行。因此，了解如何排查所有硬件故障是 Linux 系统管理员的一项基本技能。

### 查看有用的硬件命令

在排查硬件问题时，有许多 Linux 命令行工具可以提供帮助。`lspci`、`lsusb` 和 `lsdev` 命令就是其中几个，这些命令在第 23 章“处理 Linux 设备”中介绍过。这里我们将介绍另外两个很好的实用工具：`dmidecode` 和 `lshw`。

### 理解 `dmidecode` 实用工具

在查看 `dmidecode` 命令之前，您需要了解分布式管理任务工作组（`DMTF`）及其标准。`DMTF` 是一个非营利组织，其目标是通过标准简化对可联网技术（如服务器）的管理。从本质上讲，它有助于简化系统管理。

`DMTF` 创建了桌面管理接口（`DMI`）和系统管理 BIOS（`SMBIOS`）标准。`DMI` 规范由四个组件组成，提供关于计算机所使用的硬件的信息以及一些其他有用的数据。`SMBIOS` 标准由用于读取计算机 BIOS 生成的管理信息的数据结构等项组成。这两个标准相互作用，并被硬件制造商广泛采用。

要使用这些标准，您需要两样东西：一台符合 `DMI/SMBIOS` 标准的计算机和一个软件界面来访问其数据结构。Linux 系统中的软件界面是 `dmidecode` 实用工具。

`dmidecode` 实用工具默认从 `sysfs` 文件系统获取信息，特别是从 `/sys/firmware/dmi/tables/` 目录中的表格。您可以使用清单 24.12 中的命令检查这些表格是否存在于您的系统中。请注意，在该系统上，这些表格是存在的。

### 清单 24.12：检查 `sysfs` 文件系统中的表格

```bash
# ls /sys/firmware/dmi/tables
DMI     smbios_entry_point
#
```

`dmidecode` 命令的 `-h` 选项描述了在硬件故障排除过程中可用于揭示信息的各种选项。虽然提取表格信息时必须使用超级用户权限，但获取帮助时无需这样做。示例显示在清单 24.13 中。

### 清单 24.13：查看 `dmidecode` 的帮助功能

```bash
$ dmidecode -h
Usage: dmidecode [OPTIONS]
Options are:
   -d, --dev-mem FILE        Read memory from device FILE (default: /dev/mem)
   -h, --help                Display this help text and exit
   -q, --quiet               Less verbose output
   -s, --string KEYWORD      Only display the value of the given DMI string
   -t, --type TYPE           Only display the entries of given type
   -u, --dump                Do not decode the entries
       --dump-bin FILE       Dump the DMI data to a binary file
       --from-dump FILE      Read the DMI data from a binary file
   --no-sysfs                Do not attempt to read DMI data from sysfs files
   -V, --version             Display the version and exit
$
```

在各种选项中，对故障排除最有用的是 `-t` 或 `--type` 开关。它允许通过提供参数（数字或关键字）从 `DMI/SMBIOS` 表中拉取指定信息。关键字参数可以是以下之一：

- `baseboard`

- `bios`

- `cache`

- `chassis`

- `connector`

- `memory`

- `processor`

- `slots`

- `system`

如果表中不包含所需信息，您将只会收到一条关于该实用工具尝试提取数据的位置以及可能支持的 `DMI` 和/或 `SMBIOS` 标准版本的消息。清单 24.14 显示了两个示例。请注意，表中没有可用的内存信息，但显示了一些系统数据。

### 清单 24.14：查看 `dmidecode` 表格数据

```bash
# dmidecode -t memory
# dmidecode 3.0
Getting SMBIOS data from sysfs.
SMBIOS 2.5 present.
```

```bash
# dmidecode -t system
# dmidecode 3.0
Getting SMBIOS data from sysfs.
SMBIOS 2.5 present.

Handle 0x0001, DMI type 1, 27 bytes
System Information
  Manufacturer: innoteK GmbH
  Product Name: VirtualBox
  Version: 1.2
  Serial Number: 0
  UUID: 3909BE96-5CA6-4801-8236-D6113BB5D2CF
  Wake-up Type: Power Switch
  SKU Number: Not Specified
  Family: Virtual Machine
```

> **注意** 如果您正在使用虚拟化 Linux 系统，则 `dmidecode` 实用工具的信息值得怀疑。此外，不要仅依赖此实用工具获取硬件信息。其 `man` 页甚至指出：“通常情况下，`DMI` 表中包含的信息是不准确、不完整或完全错误的。”

### 理解 `lshw` 实用工具

硬件信息存储在您系统的各个 `/proc/` 目录文件中。虽然您可以四处查找并自行挖掘出来，但 `lshw` 实用工具可以为您代劳。它提供关于系统处理器、内存、网卡（`NIC`）、`USB` 控制器、磁盘等的信息。它通常在大多数发行版中默认安装，或在标准软件仓库中可用（第 13 章介绍了软件包的安装）。

两个有用的选项是 `-short`，它生成格式良好的表格形式硬件数据显示；以及 `-businfo`，它显示与 `SCSI`、`USB`、`IDE` 和 `PCI` 设备相关的信息。使用 `-short` 选项的示例摘录显示在清单 24.15 中。

### 清单 24.15：使用 `lshw` 命令的 `-short` 选项

```bash
# lshw -short
```

| H/W 路径 | 设备 | 类别 | 描述 |
| :--- | :--- | :--- | :--- |
| /0 | | system | VirtualBox |
