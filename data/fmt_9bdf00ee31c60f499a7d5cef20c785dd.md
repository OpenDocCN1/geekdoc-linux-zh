
- 主机名（Hostname）。您的机器在网络上的名称。
- IP 地址。您的机器在网络上的地址。
- 广播地址。向网络上的所有节点发送消息时使用的地址。
- 域名。您的机器所属的域名称。
- 子掩码（Netmask）。用于您网络的网络掩码。
- 名称服务器地址。为您服务的名称服务器地址。
- 网关地址。如果适用，网关机器的地址。

如果您拨号到 ISP 以访问互联网，您的 ISP 可以为您提供详细说明这些信息的文档。

虽然网络配置相当简单，但它需要一定的远见。您必须访问并修改许多配置文件。IP 地址必须完全准确，别名必须逐字准确。

大多数 Linux 发行版提供了一个网络配置应用程序（文本或图形模式）来简化配置文件的维护。这可能是安装或设置程序。对于 Slackware，对于 SuSE Linux，您使用 `YaST`。以下列出了发行版及其相关的配置程序：

| 发行版 | 工具 |
|---|---|
| CalderaLinux 2.2 | Lisa |
| Red Hat 6.0 | Linuxconf |
| Slackware 4.0 | Setup 或手动编辑文件 |
| SuSE Linux 6.1 | YaST |

## 配置文件

本节提供了网络配置文件的概述。我们提供了每个文件的概述及其职责。并提供并讨论了示例。

我们假设网络软件已安装在您的 Linux 系统上。如果没有，在继续之前，您必须先安装它。

大多数 Linux 发行版将网络配置文件存储在 `/etc` 目录下。您的发行版可能在其他地方存储其 TCP/IP 配置。至少，您可以在那里找到它们。

### `/etc/hostname` 文件

> 注意：由于有关于网卡的大量信息可用，正如提到的，您应参考 Ethernet 和 Hardware HOWTO。

至少，Linux 可以配置为网络硬件进行设置。这可以通过使用环回模式轻松实现。简单来说，这是一个连接到自身的连接。许多程序需要环回支持。

### `/etc/hosts` 文件

此文件指定了主机名的解析方式。此文件必须包含两行，如下所示：

```
# /etc/hosts
# 自动生成于 Fri Jul 9 13:46:19
# /etc/locale-1999
# 请勿编辑此文件！
# 请在 /etc/rc.config 中更改变量 (NAME SERVER + Y SERVER)。
#
order hosts bind
multi on
```

`*order*` 条目指定了必须执行搜索的顺序。在本例中，解析器将首先检查 `/etc/hosts` 以进行名称查找；如果查找失败，解析器将转到机器的名称服务器。

`*multi*` 条目，设置为 `on` 时，决定了在 `/etc/hosts` 中列出的机器是否可以具有多个 IP 地址。`multi` 的参数可以是 `on` 或 `off`。

### `/etc/resolv.conf` 文件

`/etc/resolv.conf` 文件仅包含两个项。其中一个项指定了名称服务器的 IP 地址（未标识名称），其前面是域名。可以可以指定第三个项 `search`，并识别要搜索的域名。此文件由解析库使用。

```
domain cartoon.com
search cartoon.com
name server 216.168.74.2
name server 216.168.64.2
```

如示例所示，你可以指定多个名称服务器。每个名称服务器条目必须单独占一行。可以使用任何一个名称服务器来解析名称。

## `rc` 文件

`rc` 文件，又称为运行命令（run commands），位于 `/etc/rc.d` 目录。随着系统启动，在启动时，`init` 程序会读取如 `cron` 和 `sendmail` 等文件。这些进程在 `/etc/rc.d` 中被标识。除了启动之外，TCP/IP 网络是使用 `/etc/rc.d` 中的文件以及可能在子目录中的文件进行配置的。

使用 System V Init 进程的 Linux 发行版使用 `/etc/rc.d` 目录。BSD 将启动文件存储在 `/etc/init` 目录中。System V 正在被采用 Linux 启动的标准方法。新的 Linux 发行版反映了 System V 的功能。

`/etc/rc.d` 的目录结构由各种子目录组成，如 `/etc/rc.d/init.d`、`/etc/rc.d/rc.d`、`/etc/rc.d/S.d` 等。每个目录都包含启动或关闭运行服务的脚本。

在 `/etc/rc.init.d` 目录中有许多脚本。每个脚本负责启动一项服务，例如 `cron` 或 `sendmail`。此外，脚本文件可能被用于关闭服务。

系统在启动时完成自身初始化。当内核启动时，它初始化 `init` 进程。`init` 进程是一个通常运行在 `/sbin` 目录中的进程，但在其他地方也可以找到。内核会在已知的地方查找并运行找到的一个。shell 脚本 `rc.sysinit`（位于 `/etc/rc/sysinit`）由它执行。如果 `rc.serial` 脚本存在，它将执行该脚本。

`init` 做的下一件事是运行适用于当前运行级别（runlevel）的所有脚本。如前所述，`/etc/rc.d` 包含如 `/etc/rc.d/init.d`、`/etc/rc.d/rc0.d`、`/etc/rc.d/rc1.d`、`/etc/rc.d/rc5.d` 和 `/etc/rc.d/rc3.d`，包含启动（或关闭）Windows 系统的脚本，最后，它运行位于 `/etc/rc.d` 目录中的 `rc.local` 脚本。

## Linux 内部

### `/etc/initab` 文件

`/etc/initab` 文件包含了大量关于启动和关机的信息。如果你想查看 Linux 启动的细节，请检查此文件。以下是一份来自红帽（Red Hat）的 `/etc/initab` 示例：

```
# 这描述了 INIT 进程应该如何在特定的运行级别
# 设置系统。
# initab
# 运行级别被 CUDA 使用
# 0 停止（不要将默认值设置为此项）
# 1 单用户模式（包括网络接口的初始化，
# 2 多用户模式
# 3 多用户模式（不带 NFS-Server 和某些类似服务）
#（如果你没有网络，则基本与 3 相同）
# 4 完整多用户模式
# 5 未使用
# 6 现在应该等于 3
# 7 xiii
# 8 重启（不要将 initdefault 设置为此项）
# 默认运行级别。
id:3:initdefault:
# 系统初始化，
sis:sysinit/etc/rc.d/modules default
bs:bstart/etc/rc.d/boot
# 在单用户模式下执行什么。
-1:sysinit/etc/rc.d/1
-2:sysinit/sbin/inolog

10:wait/etc/rc.d/0
11:wait/etc/rc.d/1
12:wait/etc/rc.d/2
13:wait/etc/rc.d/3
14:wait/etc/rc.d/4
15:wait/etc/rc.d/5
16:wait/etc/rc.d/6
# 正常不会到达，但在紧急情况下会备选。
z6:reboot:sbin/inolog
# 捕获 TR-ALT
ca:1:initab/sbin
```

# 如果电源在关机前恢复，则取消正在运行的关机操作。

```
pg:0123456:powerorkait:/sbin/shutdown -c "电源已恢复。"
```

# 如果在单用户模式下电源恢复，则返回多用户模式。

```
ps:powerorkait:/sbin/init
```

# 控制台和串口线上的多用户模式的 getty。

# 注意：再次强调，必须有 getty，否则你将无法登录！

# 注意：对于 "getty_ps" 你使用 lineless，而 "getty_ps" 使用 line。

```
c121:/sbin/bin/getty 3800 tty1
c122:/sbin/bin/getty 3800 tty2
c123:/sbin/bin/getty 3800 tty3
c124:/sbin/bin/getty 3800 tty4
c125:/sbin/bin/getty 3800 tty5
c126:/sbin/bin/getty 3800 tty6
```

# 串口线

```
#01123456:resp:/sbin/getty 19200 tty0 syt100
#01123456:resp:/sbin/getty 19200 tty1 syt100
```

# 拨号

```
#01123456:resp:/sbin/getty -m 6800 38400,19200,9600,2400,1200 tty0 syt100
#01123456:resp:/sbin/getty -m 6800 38400,19200,2400,1200 tty1 syt100
```

# 级别 4 仅用于 X-Windows 系统，直到我们发现它根本没有加载图形登录界面！因此级别 1 是

# 时间，然后有一个开启的 getty tty6。希望没有人

# 再次拥有一个文本控制台可能不是坏事，以防你发生意外情况。
