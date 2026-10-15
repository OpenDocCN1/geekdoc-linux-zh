

安装 RHEL 的 BIND 软件包会将二进制文件放入 /usr/sbin，将手册页放入 /usr/share/man，添加一个名为 "named" 的用户和组，并创建用于区域文件的目录。"named" 用户通过组权限可以访问数据文件。

除非你在 /etc/sysconfig/named 中更改此设置，否则 named.conf 文件位于 /etc（正如 Paul Vixie 和上帝所愿），区域文件位于 /var/named。没有提供示例文件，但 bindconf 软件包中应该有。

## Solaris 的特别说明

Solaris 10 自带 BIND 9.3.4-P1，版本可追溯到 2007 年末；你应该考虑升级。OpenSolaris 则更新一些，使用 BIND 9.6.1-P1（2009 年）。Solaris 一直以来都将其网络程序命名为 in.progname 形式，named 也不例外，所以如果你忘了它叫 in.named 而不是 named，往往会一时找不到它。幸运的是，现在情况已不再如此，Solaris 已经转而将名称服务器称为普通的 named，尽管 in.named 这个名字仍然以链接的形式存在。与 Linux 一样，Solaris 使用一个名为 /etc/nsswitch.conf 的服务顺序文件来指定 BIND、NIS、NIS+（仅限 Solaris 10）与 /etc/hosts 文件之间如何交互。将该文件中的 hosts 行修改为

```
hosts: files dns
```

会使得名称解析先尝试 /etc/hosts，然后再尝试 DNS。短路子句 NOTFOUND=return 可以修改任何条目。将关键服务器和路由器放入 /etc/hosts 文件，可以缓解在名称服务可用之前启动时偶尔出现的“先有鸡还是先有蛋”的问题。Solaris 的名称服务由 SMF 服务 svc:/network/dns/server:default 启动。SMF 选项指定命令行参数。

表 17.19 总结了 Solaris 中 BIND 的文件名和位置。

### 表 17.19 Solaris 中的 BIND 9 文件

| 文件 | 目录 | 描述 |
|---|---|---|
| resolv.conf | /etc | 解析器库配置文件 |
| named | /usr/sbin | 名称服务器守护进程 |
| named-checkconf | /usr/sbin | 检查配置文件语法 |
| named-checkzone | /usr/sbin | 检查区域文件语法 |
| named.conf | /etc | 名称服务器的配置文件 |
| nsswitch.conf | /etc | 服务切换文件 |

## HP-UX 的特别说明

HP-UX 包含 BIND 9.3.2，版本可追溯到 2005 年末；最好升级！HP-UX 提供了几个示例 nsswitch.conf 文件，用于不同的数据库和服务组合。其中一份列出了 HP 的默认设置。请将看起来适合你环境的那一份复制到 /etc/nsswitch.conf。

### HP 推荐

hosts: dns [NOTFOUND=return] nis [NOTFOUND=return] files

### 但我们更倾向于

hosts: files [NOTFOUND=continue] dns

以避免启动时出现问题。在启动过程中，必须能够在不需要查询 NIS 或 DNS 的情况下配置网络，这一点很重要，因为这些服务只有在网络就绪后才能运行。HP-UX 的名称服务启动脚本位于 /etc/rc.config.d/namesvrs_dns。

HP-UX 在 /usr/newconfig 目录中为几乎所有内容都提供了注释详尽的示例文件，但遗憾的是，没有针对名称服务的。不过，它确实有几个与名称服务相关的古老命令：hosts_to_named，用于将 hosts 文件转换为区域文件；以及 sig_named，用于向正在运行的 named 进程发送信号以控制它。如今的 /etc/hosts 文件只包含 localhost 和主机本身，因此这个转换程序毫无用处。而且从 BIND 9 开始，必须使用 rndc 来控制 named，而不是信号。

表 17.20 总结了 HP-UX 上名称服务的文件名和位置。

### 表 17.20 HP-UX 中的 BIND 文件

| 文件 | 目录 | 描述 |
|---|---|---|
| resolv.conf | /etc | 解析器库配置文件 |
| named | /usr/sbin | 名称服务器守护进程 |
| lwresd | /usr/sbin | 轻量级解析器守护进程 |
| named-checkconf | /usr/sbin | 检查配置文件语法 |
| named-checkzone | /usr/sbin | 检查区域文件语法 |
| named.conf | /etc/namedb | 名称服务器的配置文件 |
| nsswitch.conf | /etc | 服务切换文件 |

## AIX 的特别说明

AIX 同时附带 BIND 8 和 BIND 9，对应的二进制文件分别是 named8 和 named9。出厂时，named 是指向 named8 的链接，而 named8 已不再受 ISC 支持。它们提供的版本是 8.3.3+ 和 9.2.1，可追溯到 2004 年 1 月。这里的升级速度慢如树懒！AIX 不包含 named-checkconf 和 named-checkzones 命令——也许它们是在 2004 年之后才加入 BIND 发行版的。AIX 下名称服务的启动脚本位于 /etc/rc.tcpip。

我们开始觉得这些文件位置表格有些多余，因为就 BIND 而言，操作系统已经在很大程度上趋同于标准位置，但 AIX 解决了这一争论。下一页的表 17.21 显示了 AIX 的文件名和位置。

