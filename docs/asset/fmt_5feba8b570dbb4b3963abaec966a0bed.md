
Jul 19 14:37:50 nubark named[75]: lame server resolving 'w3w3.com' (in

w3w3.com?). 216.117.131.52#53

在其中一个 `.com` TLD 服务器上查询 `w3w3.com` 的名称得到如下结果：

```
$ dig @e.gtld-servers.net w3w3.com ns
:: ANSWER SECTION:
w3w3.com. 172800 IN ns0.nameserver.net.
w3w3.com. 172800 IN ns1.nameserver.net.
```

但如果我们在同一个问题中询问这些服务器中的每一个，我们得到了来自 `ns0` 的答案，而 `ns1` 则没有答案：

```
$ dig @ns0.nameserver.net w3w3.com ns
:: ANSWER SECTION:
w3w3.com. 14400 IN ns0.nameserver.net.
```

## DNS 检查工具

```
$ drill w3w3.com ns
:: ANSWER SECTION:
w3w3.com. 14400 IN ns0.nameserver.net.
w3w3.com. 14400 IN ns1.nameserver.net.
```

## DNS 检查工具

```
$ drill drill @ns0.nameserver.net w3w3.com ns
:: ANSWER SECTION:
w3w3.com. 14400 IN ns1.
$ drill @ns1.nameserver.net w3w3.com ns
:: ANSWER SECTION:
w3w3.com. 14400 IN ns0.nameserver.net.
```

## DNS 检查工具

```
$ drill @ns0.nameserver.net w3w3.com ns
:: ANSWER SECTION:
w3w3.com. 14400 IN ns1.nameserver.net.
```

## DNS 检查工具

```
$ drill @ns1.nameserver.net w3w3.com ns
:: ANSWER SECTION:
w3w3.com. 14400 IN ns0.nameserver.net.
```

## DNS 检查工具

```
$ dig w3w3.com ns
:: ANSWER SECTION:
w3w3.com. 14400 IN ns0.nameserver.net.
w3w3.com. 14400 IN ns1.nameserver.net.
```

## DNS 检查工具

```
$ dig @ns0.nameserver.net w3w3.com ns
:: ANSWER SECTION:
w3w3.com. 14400 IN ns1.nameserver.net.
```

## DNS 检查工具

```
$ dig @ns1.nameserver.net w3w3.com ns
:: ANSWER SECTION:
w3w3.com. 14400 IN ns0.nameserver.net.
```

## DNS 检查工具

```
$ host w3w3.com ns
Name:    w3w3.com
Nameserver:  ns0.nameserver.net, ns1.nameserver.net
address list:  ns0.nameserver.net,ns1.nameserver.net.
```

## DNS 检查工具

```
$ nslookup @ns0.nameserver.net w3w3.com ns
Server:  ns0.nameserver.net
Address:  ...
Non-authoritative answer:
Name:    ns1.nameserver.net
Addresses: ...
$ nslookup @ns1.nameserver.net w3w3.com ns
Server:  ns1.nameserver.net
Address:  ...
Non-authoritative answer:
Name:    ns0.nameserver.net
Addresses: ...
```

# Linux 规范

# 681

要估计 NSD 服务于你的权威数据所需的内存，请填写 `ninetlabs.net/nsd/nsd-memsize.html` 上的表单。太棒了！

使用转发器。有关转发的讨论请参见第 606 页。

在许多系统中，启动 `named` 的初始化脚本提供了额外的入口（例如 `reload`），这些是供系统管理员使用的。但使用 `rnd` 更加简单且跨平台效率更高。

关于 `inetd` 的更多信息，请参见第 1188 页。

不要使用 `inetd` 或 `xinetd` 管理名称服务器；它们在每次需要时都会重启服务器，这会极大减慢响应时间并防止形成任何有缓存。

## 17.16 厂商规范

本节描述了我们各个厂商平台上的名称服务软件的状况。大家都会安装 BIND，尽管你可能需要在分发操作系统时指定安装它，或者作为软件包层进行安装。

大多数 Linux 发行版在升级到 BIND 最新版本方面比 UNIX 同类产品灵活得多。尽管如此，名称服务仍然至关重要。你可能希望制定一种策略：获取最新的源发行版并进行构建，而不是等待软件包发布。

Ubuntu 和 Red Hat 拥有以软件包形式提供的自己的 NSD/Unbound 套件；SUSE 的官方存储库中只有 Unbound。目前，所有软件包版本都略显落，所以与 BIND 一样，你可能想从 `ninetlabs.net` 获取最新的源代码并进行构建。

在本节中，我们包含了指向配置文件的指针、每个厂商软件中构建的 BIND 版本信息，以及关于如何将 BIND 与其他管理数据源（如平面文件或 NIS）集成的信息。关于此主题的更完整讨论在第 19 章中给出。特别是请参阅从第 739 页开始的内容。

有关系统启动脚本的更多信息，请参见第 87 页。

我们还包含了应在启动时执行以启动名称服务器的启动脚本指针。如果没有名称服务，你的网络、邮件——一切都会受到影响。某些站点使用持续运行的脚本，例如 BIND 分发版中的 `nanny` 脚本。

# Linux 规范

Linux 的 BIND 软件包为 `named` 运行安装了启动脚本，Ubuntu 通过 `/etc/init.d/bind9`，RHEL 和 SUSE 通过 `/etc/init.d/named`。

Linux 的 `named` 软件包将内容安装在所有常规位置。表 17.18 显示了细节。Red Hat 有一些通过 `named` 的 `-D` 命令行标志与你的 Network Manager 工具交互的额外细节。可以在 Red Hat BIND 软件包中的 `doc/README-DBUS` 文件。

表 17.18 Linux 中的 BIND 文件
| 文件 | 目录 | 描述 |
|---|---|---|
| resolv.conf | /etc | 解析器库配置构文件 |
| named, lwres | /usr/sbin | 名称服务器守护进程 |
| lwres | /usr/sbin | 轻量级解析器 |
| named.conf | /etc | named 配置文件 (RHEL 和 SUSE) |
| | /etc/bind | named 配置文件 (Ubuntu) |
| named-checkconf | /usr/sbin | 检查配置文件的语法 |
| named-checkzone | /usr/sbin | 检查区域文件的语法 |
| namedGetForwards | /usr/sbin | Red Hot, 用于 Network Manager 工具 |
| namedSetForwards | /usr/sbin | Red Hat, 用于 Network Manager 工具 |
| nsswitch.conf | /etc | 服务切换文件 |

Linux 使用切换文件 `/etc/nsswitch.conf` 来指定如何执行主机名到 IP 地址的转换，以及应该先尝试、后尝试还是完全不尝试 DNS。如果不存在切换文件，默认行为是：

- hosts: dns [UNAVAIL|return] 文件

`!UNAVAIL` 子句意味着如果 DNS 可用但未找到名称，则查找尝试应该失败，而不是在这种情况下继续处理下一个条目（在这种情况下是 `/etc/hosts` 文件）。如果没有服务器在运行（在启动过程中可能会出现这种情况），查找过程将咨询 `hosts` 文件。

我们的示例发行版提供了以下默认的 `nsswitch.conf` 条目：

hosts: dns

配置查找没有所谓的“最佳”方法——这取决于你的站点是如何维护的。通常情况下，我们倾向于将尽可能多的信息保存在 DNS 中，而不是 NIS 或平面文件中，但我们也尝试在必要时启动过程中回退到 `hosts` 文件以保持稳定性。

Ubuntu 是我们 Linux 发行版中更新最新的，其发行软件包仅是几个月前的。程序和文件的所有者为 `root`，组所有者为 `bind`，当以用户 `bind` 而不是 `root` 调用时，具有访问权限。

一些实用的示例文件存储在 `/etc/bind` 中。包括一个 `named.conf` 文件以及用于根提示（root hints）、本地主机、广播地址和私有地址的区域文件。提供的 `named.conf` 包含了 `named.conf.options` 和 `named.conf.local` 文件。它将 BIND 的默认目录设置为 `/var/cache/bind`；出厂时，该目录存在但是空的。

# Linux 特有

配置信息位于 `/etc` 而区域信息位于 `/var` 背后的逻辑是：你是其他站点的辅助服务器，你无法控制 `named` 写入的区域文件的大小。为了避免可能填满根分区，你可能希望将文件保留在 `/var` 中。作为主服务器的区域可以存在于 `/etc`（在 `named.conf` 文件中使用使用绝对路径），也可以存在于 `/var/cache/bind`。如果你想运行一个纯缓存服务器，则不需要修改示例 `named.conf` 文件。Ubuntu 提供的示例文件使用了一些 BIND 功能来帮助你的服务器成为良好的公民。例如，为你的用户配置 .com 和 .net 仅有区域。如果你不使用私有地址空间（RFC1918），空的 RFC1918 区域文件可以防止这些地址逃逸本地网络。此外，目录 `/usr/share/doc/bind9` 包含了几个实用的引用。Ubuntu 说明了它在做什么并产生了一个合理的、文档良好的名称服务器。默认情况下， `named` 以用户和组 `named` 在 chroot 环境下运行。安装程序创建一个 jail 并用填充运行 named 所需的所有文件，如用于 syslog 的 UNIX 套接字。额外的配置文件（不是 `named.conf`）和区域文件位于 `/etc/named.d` 中，并在 `named` 启动时复制到 jail 中。如果你不想在 jail 中运行 `named`，请修改 `/etc/sysconfig/named` 中显示 `NAM_RUN_CHROOT="yes"` 的行。这就是你需要更改的所有；`/etc/init.d/` 中的启动脚本引用了这些信息并能够以任何方式启动 `named`。SUSE 提供了一个带有有用注释的示例 `/etc/named.conf` 文件，解释了许多选项。SUSE 的 `/etc/named.conf` 文件不像其他系统那样是全局可读的。默认文件导入了一个名为 `named.conf.include` 的文件，该文件又导入了 `rndc-access.conf`，两者对全球可见。目前还不完全清楚 SUSE 在安全方面的考虑。`rndc` 预配置为接受来自 localhost 的命令。SUSE 的 `/etc/named.conf` 文件可以原样用于纯缓存服务器。如果你要提供自己的区域，将区域文件放在 `/etc/named.d` 并在 `named` 启动时复制到 jail 中。BIND 的文档位于 `/usr/share/doc/bind9`。

第 17 章 DNS：域名系统

安装 RHEL BIND 软件包将二进制文件放在 `/usr/sbin`，将帮助页放在 `/usr/share/man`，创建一个名为 `named` 的用户和组，并创建数据目录。配置文件位于 `/etc`（如 Paul Vixie 意所示），区域文件位于 `/var/named`。没有提供示例文件，但 bind 软件包应该有。除非你更改 `/etc/sysconfig/named`，否则 `named.conf` 文件位于 `/etc/var/named`。

# Solaris 特有

Solaris 10 带有 BIND 9.3.4-P1，发布于2007 年；你应该考虑升级。OpenSolaris 使用 BIND 9.6.1-P1（2009年）。Solaris 一直将它们的网络程序命名为 `ingrade`，`named` 也不例外，以至于你找不到它。现在 Solaris 已经将其命名为普通的 `named`，尽管链接仍然存在。像 Linux 一样，Solaris 使用服务顺序文件 `/etc/nsswitch.conf` 来指定 BIND、NIS、NIS+（仅限 Solaris 10）以及 `/etc/hosts` 文件如何交互。修改文件中的 hosts 行使得：

```
hosts: dns
```
