
# 471

还有一个可以从 Ubuntu 仓库安装的图形界面来管理 GUFW。如果您安装了它，可以在“系统”、“管理”、“防火墙配置”中打开 GUFW。细节相同，界面更简单且不需要记忆过多内容，如图 19.1 所示，我们有一条规则允许 22 端口（SSH 服务）的入站流量，以及使用 TCP 的 5900 端口（VNC 服务）。

![](img/2a083394994f21b612810fd7c32a8def_471_0.png)

图 19.1 GUFW 图形界面

点击 `Add` 可以为预配置的服务添加规则，如图 19.2 所示，或者您可以在“简单”和“高级”选项卡中配置您自己的规则。

UFW 基于 `iptables`，后者是用于配置 Linux 内核内置防火墙的表。UFW 简化了用户任务和语法，它只是在使用 `iptables`。您可能在 Ubuntu 机器上不需要了解这些，但为了完整性以及在您以后使用不同的 Linux 发行版时提供帮助，表 19.2 列出了简单的基础命令，作为 `iptables` 的简要介绍。

在表格中，您将看到全大写的 `ACCEPT` 和 `DROP`，这些是针对所谓的“链”（Chains）的策略。链是对特定类型网络访问的描述，如下所示的 `INPUT`、`FORWARD`、`OUTPUT` 以及网络中的其他交互。例如，您可以将默认策略定义为 `DROP`（即拒绝），然后允许特定类型的流量通过防火墙。`iptables` 非常复杂且极其强大。

## 配置你的防火墙

![](img/2a083394994f21b612810fd7c32a8def_472_0.png)

表 19.2 `iptables` 命令基础示例集

| 命令 | 执行的操作 |
| --- | --- |
| Usage: COMMAND | |
| `sudo iptables -L` | 列出当前设置的防火墙规则 |
| `sudo iptables -L -vn` | 列出当前设置的防火墙规则，但更详细 |
| `sudo iptables -F` | 删除所有设置的防火墙规则 |
| `sudo iptables -P INPUT DROP` | 丢弃所有入流量 |
| `sudo iptables -P FORWARD ACCEPT` | 接受所有转发流量 |
| `sudo iptables -P OUTPUT DROP` | 丢弃所有出流量 |
| `sudo iptables -A INPUT -s 8.8.8.8 -j DROP` | 丢弃来自特定 IP 的流量（示例为 Google DNS；你可能不想拦截它……） |

你可以根据 IP 地址、网卡（NIC）、端口、网络等阻止或允许流量。你可以设置 `iptables` 记录所有操作或仅特定操作。你甚至可以使用它来配置 NAT 路由器。更多信息，请参考 `iptables` 及其 IPv6 兄弟 `ip6tables` 的 man pages。

## AppArmor

`AppArmor` 是一种强制访问控制（MAC）系统。它比众闻名的 `SELinux`（//www.nasa.gov/research/selinux/）简单得多，后者是由美国国家安全局（NSA）创建的 MAC。`AppArmor` 设计用于通过将特定程序限制在预定义的资源范围内限制其功能，并通过配置（profiles）来实现，这些配置在启动时加载到内核。它可以在抱怨模式（`complain mode`）下运行，记录不安全操作的信息但不采取行动；也可以在强制模式（`enforce mode`）下运行，激活策略和限制。

这是 `AppArmor` 的简要介绍。如需完整介绍，请查看本章最后“参考文献”中链接的列表。

默认情况下，`AppArmor` 的作用有限。你可以通过安装 `apparmor-profiles` 软件包从 Ubuntu 仓库安装一些额外的配置文件。它们运行在抱怨模式，并在 `/var/log/messages` 中记录问题。

要释放 `AppArmor` 的威力，你需要编辑或在 `/etc/apparmor.d` 中创建文件。配置文件以其限制的应用程序命名，包括应用程序在文件系统中的完整路径。例如，此处显示的 `sbin.syslogd` 文件限制了系统日志守护进程：

```
Sun Sep 25 08:58:35 2011

#include <tunables/global>
```

# 如果无法写入写入内核记录拒绝信息的文件，调试 syslog 将很困难。在这种情况下，你可以执行以下操作：

```
# watch -n 1 'dmesg | tail -5'

/usr/sbin/syslogd {

#include <abstractions/base>

#include <abstractions/nameservice>

capability sys_tty_config,

capability dac_override,

capability dac_read_search,

capability setuid,

capability setgid,

capability sys_nice,

capability syslog,

}
```

```
/etc/rsyslog.conf r

/etc/rsyslog.d/ r

/etc/rsyslog.d/** r

/{,{var/}/run/syslogd.pid rwk,
```

```
/var/spool/rsyslog/ r,
/var/spool/rsyslog/** rwk,

/usr/lib/{32,64}/rsyslog/**.so mr,
```

```
/dev/tty* rw
/dev/xconsole rw,

@{PROC}/kmsg

r,
```

```
/dev/log wl
/var/lib/*/dev/log wl
/var/spool/postfix/dev/log wl,
```

```
# 当使用 infile 时需要 'r'

/var/log/** rw,
```

```
# 这里的 为 mysql 支持添加这些

#/etc/mysql/my.cnf r

#/{var}/run/mysqld/mysqld.sock rw,
```

```
# 为 postgresql 支持添加这些
#include <abstractions>/openssl
#include <abstractions>/ssl_certs
/#{var}/postgresql/*.s.PGSQL.*[0-9] rw,
```

```
# 站点特定的添加和覆盖。详情请见 local/README。

#include <local/usr.sbin.rsyslogd

}
```
