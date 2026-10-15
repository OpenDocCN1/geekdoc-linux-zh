
HP-UX 将启动脚本的输出保存在 `/etc/rc.config`。如果某个启动脚本失败，请检查 `/etc/rc.log` 查看是否包含任何相关的错误消息或问题来源的提示。这种保存启动脚本输出的功能是非常有用且优秀的，而且实现也很简单。惊讶的是其他供应商还没有注意到这一点。

`/etc/rc.config.d` 中的配置文件可能会令人困惑，尽管它们有良好的注释。表 2.4 对一些常用的文件进行了简要说明。

### 表 2.4 `/etc/rc.config` 中常见的修改的 HP-UX 配置文件

| 文件 | 用途 |
| --- | --- |
| `snmp` | 开启或关闭所有 SNMP 支持的主开关 |
| `snmp*` | 其他 SNMP 相关的选项 |
| `acct` | 开启或关闭进程。参见 `acct(1)` |
| `auditing` | 配置系统环境。参见 `audsys(1)` 和 `audevent(1)` |
| `cde` | 存储 CDE（公共桌面环境）设置 |
| `clean*` | 控制各种引导清理操作 |
| `desktop` | 配置桌面环境为默认 |
| `hpbase100conf` | 配置 100 MB 接口 |
| `hpetherconf` | 配置以太网接口。参见 `lanadmin(1)` |
| `list_mode` | 配置启动显示选项 |
| `lp` | 开启或关闭打印溢字 |
| `mailserv` | 启动 `startmail` 或指定邮件服务器 |
| `nameserv` | 配置/启动名称服务器守护进程 |
| `nddconf` | 在启动时使用 `ndd` 设置可调内核参数 |
| `netconf` | 指定网络设备配置（IP 地址等） |
| `netdaemons` | 告诉启动哪些网络守护进程 |
| `nettl` | 配置网络跟踪和日志 |
| `nfsconf` | 设置 NFS 配置选项 |
| `pd` | 配置 HP 分布式打印服务 |
| `vt` | 启动 `vtdaemon`。依赖于 `ptdaemon` |
| `xfs` | 开启或关闭 X Windows 字体服务器 |

- a. 更多信息请 `nettl(1)`、`netconf(1)` 和 `netlig.config(4)`。

对于这些大多数文件，默认值通常是可以的。最常用的需要修改的文件是 `netconf`、`netdaemons` 以及 `nddconf`。

...并询问你如何处理这些更改。你可能希望在生产系统中禁用此服务，因为每当检测到硬件配置更改时，它都会延迟启动过程，导致每次硬件更改产生额外的 30 秒停机时间。

- `network-scripts` 目录包含与网络配置相关的额外材料。你唯一需要更改的是名为 `ifcfg-interface` 的文件。例如，`network-scripts/ifcfg-eth0` 包含了接口 `eth0` 的配置参数。它设置了接口IP地址和网络选项。有关配置网络接口的更多信息，请参阅第300页。

- `sendail` 文件包含两个变量：`DAEMON` 和 `QUEUE`。`DAEMON` 变量设置为 `yes` 时，系统在启动时将启动 `sendmail`。`QUEUE` 告诉在发生错误后 `sendmail` 应该队列多长时间的邮件再重新发送。

## FreeBSD 启动脚本

本节专门针对 FreeBSD，但启动策略的总体概述适用于其他 BSD 系统。

`FreeBSD-init` 仅运行单个启动脚本，系统的其他 `rc` 脚本都位于 `/etc` 中并命名为 `rc.something`。脚本按照预定义的顺序运行，没有级别运行（level runs）的概念。

`/etc/rc` 开始读取（准确地说是执行）三个指定配置信息的文件：

- `/etc/defaults/rc.conf`
- `/etc/rc.conf`
- `/etc/rc.conf.local`

`rc.conf` 文件还可以指定用于查找启动文件的其他目录。你通过设置 `local_startup` 变量的值来指定其他目录。

这些配置文件通过定义 shell 变量的值来发挥作用。`rc` 脚本随后使用这些变量通过 `source` 命令（更准确地说，是使用其并不直观的别名 `~`）将配置文件和附属脚本插值到其自身的执行流中；实际上，这一过程将所有配置文件和启动脚本合并成一个巨大的脚本。

`/etc/defaults/rc.conf` 是一个巨大的文件，列出了所有配置参数及其默认设置。此文件绝不应编辑；否则启动脚本的“怪兽”会找你。要更改变量的内容，请通过在 `/etc/rc.conf` 或 `/etc/rc.conf.local` 中设置它来覆盖其默认值。`rc.conf` 手页列出了你可以指定的变量详细列表。

通过查看 `/etc` 可以看到，有很多 `rc` 脚本。

## 第2章 启动与关机

```
% ls /etc/rc*

rc rc.diskless1 rc.isdn rc.pccard

rc.atm rc.diskless2 rc.local rc.resume

rc.conf rc.firewall rc.serial rc.devfs

rc.1386 rc.network rc.shutdown rc.suspend

```

如果内核被配置为无盘客户端，`/etc/rc` 将开始调用 `rc.diskless1`。它接着调用 `rc.sysctl`、`rc.serial`、`rc.pccard` 和 `rc.network`，后者将继续执行一些管理职功能。作为最后的操作之一，它运行 `rc.local` 脚本。如果脚本不存在，它将跳过它。（在上面的列表中，`rc.sysctl` 不存在。）

默认的 `rc.serial` 脚本什么都不做，但它定义了一组函数，可以在启动时初始化串口端口和设备。

如果在其中一个 `rc.conf` 文件中指定了 PCMCIA/CardBus 支持，`rc.pard` 将加载与 PCMCIA 控制器相关的内核模块，并启动 `pccard`——该守护进程用于控制 PCMCIA 卡在插入和拔出时的配置和取消配置。

`rc.network` 是一个很长且复杂的脚本，用于设置机器网络环境。它使用在 `rc.conf` 中指定的变量来配置接口并处理 DHCP、PPP、路由和防火墙。除非所有配置都在 `rc.conf` 中完成，否则你不需要碰该脚本。`rc.network` 脚本会调用其他与其他相关的 `rc` 脚本：`rc.atm`、`rc.isdn` 和 `rc.firewall`。

在 FreeBSD 下配置网络接口，使用 `hostname`、`defaultrouter` 和 `ifconfig_if` 变量（其中 `if` 是接口名称)。`ifconfig_if` 变量应包含一组传递给该接口 `ifconfig` 的选项字符串。

例如，这些行：

```
hostname=my.fullyqualified.name

ifconfig_de="inet 192.168.1.2 netmask 0xffffff00"

defaultrouter="192.168.1.1"

```

将主机配置为地址 192.168.1.2，默认路由为 192.168.1.1。要使用 DHCP 配置接口，请使用如下行：

```
ifconfig_de0="DHCP"
```
