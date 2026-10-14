
你可以从 Ubuntu 存储库安装一个名为 GUFW 的图形化界面来管理 UFW。如果你安装了它，可以在“系统 - 管理 - 防墙配置”中打开 GUFW。细节是相同的，但界面更简单，不需要你记住那么多内容，正如图 19.1 所示，我们有一条规则允许端口 22（用于 SSH 服务）的入站流量，以及如果使用 TCP 则端口 5900（用于 VNC 服务）的入站流量。

![](img/d9236e4682dfcf03b759a19829a318ef_467_0.png)

图 19.1 GUFW 图形界面。

如果你点击“添加”，可以轻松地为预配置的服务添加规则（如图 19.2 所示），或者从“简单”和“高级”选项卡中配置自己的规则。

## 配置你的防火墙

![](img/d9236e4682dfcf03b759a19829a318ef_468_0.png)

图 19.2 GUFW 预配置服务选项。

UFW 基于 `iptables`，`iptables` 是用于配置 Linux 内核内置防火墙的表。UFW 简化了用户任务和语法，但实际上只是在使用 `iptables`。在你的 Ubuntu 机器上可能不需要了解这些，但为了完整性以及帮助你以后使用不同的 Linux 发行版，表 19.2 列出了一些简单的基础命令作为 `iptables` 的简要介绍，以引起你的兴趣。

在表中，你会看到全大写的单词，如 `ACCEPT` 和 `DROP`，这些是为名为“链”（chains）的项目设置的策略。链是对特定类型网络访问的描述，如下所示的 `INPUT`、`FORWARD` 和 `OUTPUT`，以及网络中的其他交互。例如，你可以将默认策略定义为 `DROP`（即拒绝），然后允许特定类型的流量通过防火墙。`iptables` 非常复杂且极其强大。

### TABLE 19.2 UFW 有用命令

| Command | 执行的操作 |
| --- | --- |
| Usage: COMMAND | |
| `sudo iptables -L` | 列出当前设置的防火墙规则 |
| `sudo iptables -L -vn` | 列出当前设置的防火墙规则，但提供更详细的信息 |
| `sudo iptables -F` | 删除所有当前设置的防火墙规则 |

## AppArmor

| Command | 执行的操作 |
| --- | --- |
| `sudo iptables -P INPUT DROP` | 丢弃所有入站流量 |
| `sudo iptables -P FORWARD ACCEPT` | 接受所有转发流量 |
| `sudo iptables -P OUTPUT DROP` | 丢弃所有出站流量 |
| `-A INPUT -s` | 丢弃来自特定 IP 的流量（示例是 Google DNS 服务器；你可能不想屏蔽它……） `8.8.8.8 -j DROP` |

你可以根据 IP 地址、网卡（NIC）、端口、网络等阻止或允许流量。你可以设置 `iptables` 记录所有操作或仅记录特定操作。欲更多信息，请参阅 `iptables` 及其 IPv6 兄弟 `ip6tables` 的 man 页。

AppArmor 是一个强制访问控制（MAC）系统。它比由美国国家安全局（NSA）创建的著名的 SELinux (`www.nsa.gov/research/selinux/`) 更简单。AppArmor 旨在通过限制特定程序使用预定义的资源且仅使用这些资源来限制它们的行为。这是通过配置文件（profiles）实现的，这些在启动时加载到内核中。它可以在“投诉模式”（complain mode）下运行，在该模式下会记录不确定操作的信息但不采取行动；也可以在“强制模式”（enforce mode）下运行，此时策略和限制将生效。

这是对 AppArmor 的简要介绍。如需更完整的介绍，请查看本章最后“引用”部分列出的链接。

默认情况下，AppArmor 作用很小。你可以通过安装 `apparmor-profiles` 包从 Ubuntu 存储库安装一些额外的配置文件。这些运行在投诉模式下，并在 `/var/log/messages` 中记录问题。

要释放 AppArmor 的威力，你需要在 `/etc/apparmor.d/` 中编辑或创建文本文件。配置文件以其限制的程序命名，包括该程序在文件系统中的完整路径。例如，此处显示的 `sbin.risyslog` 文件限制了系统日志守护进程

```
# Last Modified: Sep 25 08:58:35 2011

#include <tunables>/global>

# 如果无法写入内核记录拒绝访问的文件中，那么调试 syslog 将变得困难。在这些情况下，你可以执行以下操作：# watch -n 1

'dmesg | tail -5'

#include <abstractions/base> #include <abstractions/

nameservice>

  capability sys_tty_config, capability dac_override, capability dac_read_search,

capability setuid, capability setgid, capability sys_nice, capability syslog,

```

```
# rsyslog 配置 /etc/rsyslog.conf, /etc/rsyslog.d/**, /etc/
rsyslog.d/**, /var/run/rsyslog.pid rwk, /var/pool/rsyslog/
rsyslog/** rwk,
/usr/lib(32,64)/rsyslog*/so.mr,
/dev/tty* rw, /dev/xconsole rw, @{PROC}/xmsg r,
/dev/log wl, /var/lib*//dev wl, /var/pool/postfix/
devlog wl,
# 使用 /var/log/ rw 时需要 'r'，
# 为 mysql 支持添加此此行 #/etc/mysql/my.cnf r, #/(var)/run/mysqld.
sock rw,
# 为 postgresql 添加此此行 ##include <abstractions/openssl> ##include
<abstractions/ssl_certs> #/(var/run/postgresql/s.PGSQL.*[0-9] rw
# 站点特定的属性和覆盖。详情请见 local/README。#include
<local/usr.sbin.rsyslog>
```

即使不使用该语法，你也可以从此文件中看到，配置（profiles）是简单的类型，支持使用注释、绝对路径和通配符（文件名的模式匹配），支持允许或禁止特定功能，并规定文件系统中的哪些位置和程序可以被访问或使用。

每个访问规则都指定了列表中的特定权限：

- `r` - 读
- `w` - 写
- `ux` - 无限制执行
- `Ux` - 无限制执行 - 清理环境
- `px` - 离散配置执行
- `Px` - 离散配置执行 - 清理环境
- `ix` - 继承执行
- `m` - 允许在 `mmap(2)` 调用中使用 `PROT_EXEC`
- `l` - 链接

这些权限列在每行的末尾。

Genprof 是一个由你生成或更新配置的程序。你可以提供可执行文件的名称（如果它不在路径中，则提供路径），并可能可选地提供配置文件的路径，如下：

```
matthew@seymour-r:$ sudo genprof google-chrome
```

系统将要求你启动程序并使用一段时间。完成后，你将有机会选择允许还是拒绝每个函数。程序随后会在 `/etc/apparmor.d` 中写入一个文件，使用程序名称和其路径（在此情况下为 `opt.google.chrome.google-chrome`，因此没有直接从 Google 安装 [`www.google.com/chrome?platform=linux`]，所以你的系统中不存在预装的 AppArmor 配置）。然后你可以根据需要编辑该文本文件，如果你想从投诉模式（complain mode）切换到强制模式（enforce mode），则必须这样做。

当你拥有一组涵盖了你所需的配置后，以下这些命令将是最经常使用的：

```
start:
```

```
matthew@seymour:-$ sudo service apparmor start
```

```
stop:
```

```
matthew@seymour:-$ sudo service apparmor stop
```

```
reload:
```

```
matthew@seymour:-$ sudo service apparmor reload (or restart)
```

```
show status:
```

```
matthew@seymour:-$ sudo service apparmor status
```
