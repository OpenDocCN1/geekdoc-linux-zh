
tool 通过 -D 命令行标志传递给 named。详细信息可在 Red Hat BIND 包中的 doc/README-DBUS 文件中找到。

## Table 17.18 BIND files in Linux

| File | Directory | Description |
|---|---|---|
| resolv.conf | /etc | 解析库配置文件 |
| named, lwres | /usr/sbin | 名称服务器守护进程 |
| lwresd | /usr/sbin | 轻量级解析器 |
| named.conf | /etc | named 配置文件（RHEL 和 SUSE） |
|  | /etc/bind | named 配置文件（Ubuntu） |
| named-checkconf | /usr/sbin | 检查配置文件语法 |
| named-checkzone | /usr/sbin | 检查区域文件语法 |
| namedGetForwarders | /usr/sbin | 仅 Red Hat，用于 Network Manager 工具 |
| namedSetForwarders | /usr/sbin | 仅 Red Hat，用于 Network Manager 工具 |
| nsswitch.conf | /etc | 服务切换文件 |

Linux 使用一个切换文件 /etc/nsswitch.conf 来指定应如何执行主机名到 IP 地址的映射，以及是否应首先、最后或根本不尝试 DNS。如果没有切换文件，则默认行为为

```
hosts: dns [!UNAVAIL=return] files
```

!UNAVAIL 子句意味着如果 DNS 可用但其中未找到名称，则查找尝试应失败而不是继续到下一个条目（本例中为 /etc/hosts 文件）。如果没有运行名称服务器（例如在启动过程中可能出现的情况），查找过程将咨询 hosts 文件。

我们的示例发行版都提供了以下默认 nsswitch.conf 条目：

```
hosts: files dns
```

实际上并没有“最佳”的查找配置方式——这取决于你的站点如何管理。一般来说，我们更喜欢尽可能将尽可能多的主机信息保存在 DNS 中，而不是保存在 NIS 或平面文件中，但我们也试图在启动过程中如果必要时保留回退到静态 hosts 文件的能力。

![](img/14d78e3cecac4581d37024baf1e94cca_730_0.png)

Ubuntu 是我们 Linux 发行版中最为最新的，其分发包仅有几个月旧。程序和文件的所有者为 root，组所有者为 "bind"，权限设置为允许在 named 以用户 "bind" 而非 root 身份调用时访问。

一些有用的示例文件存放在 /etc/bind 中。其中包括一个 named.conf 文件和用于根提示、localhost、广播地址以及私有地址空间的区域文件。提供的 named.conf 包含文件 named.conf.options 和 named.conf.local。它将 BIND 的默认目录设置为 /var/cache/bind；按原样提供时，该目录存在但为空。

配置信息放在 /etc 中而区域信息放在 /var 中的逻辑在于，如果你是其他站点的辅助服务器，你无法控制 named 将写入的区域文件的大小。为了避免可能填满根分区，你可能希望将文件保存在 /var 中。对于你作为主服务器的区域，可以与配置文件一起存放（在 named.conf 文件中使用绝对路径），也可以放在 /var/cache/bind 中。

示例 named.conf 文件无需修改即可运行仅缓存服务器。你必须添加你有权威的任何区域，最好添加到提供的 named.conf.local 文件中。

Ubuntu 提供的示例文件利用了一些新的 BIND 功能来帮助你的服务器在网络上成为良好的 DNS 公民。例如，它们将 .com 和 .net 配置为仅委派区域，以防止你的用户因拼写错误而通过 VeriSign 的 Site Finder 工具为其产生广告收入。如果你在内部不使用私有地址空间（RFC1918），那么空的 RFC1918 区域文件可防止这些地址逃离本地网络。Go, Ubuntu！

目录 /usr/share/doc/bind9 包含几个有用的参考资料。查看 README.Debian 文件（即使在 Ubuntu 上）以了解配置 BIND 的策略。

![](img/14d78e3cecac4581d37024baf1e94cca_731_0.png)

SUSE 安装会说明其正在执行的操作并生成一个合理且文档完善的名称服务器安装。默认情况下，named 在 /var/lib/named 下的 chroot 环境中以用户和组 "named" 运行。安装程序创建 chroot jail 目录并用运行 named 所需的所有文件填充它，甚至包括 syslog 的 UNIX 域套接字等细节。额外的配置文件（非 named.conf）和区域文件存放在 /etc/named.d 中，并在 named 启动时复制到 jail 中。如果不想在 jail 中运行 named，请修改 /etc/sysconfig/named 中

```
NAMED_RUN_CHROOTED="yes"
```

这一行。这就是你需要更改的全部内容；/etc/init.d 中的启动脚本会引用此信息，能够以任一方式启动 named。

SUSE 提供了一个带有有帮助注释的示例 /etc/named.conf 文件，解释了许多选项。SUSE 的 /etc/named.conf 文件不像其他系统上通常那样对所有用户可读。默认文件导入名为 named.conf.include 的文件，该文件随后导入 /etc/named.d 中的 rndc-access.conf 文件，两者都对所有用户可读。SUSE 在这里关于安全性的意图并不完全清楚。rndc 预先配置为仅接受来自本地主机的控制命令。

SUSE 的 named.conf 文件可直接用于运行仅缓存服务器。如果你想提供自己的区域，请将区域文件放在 /etc/named.d 目录中，并在 /etc/named.conf.include 文件中列出区域名称。

ISC BIND 文档位于 /usr/share/doc/packages/bind9。
