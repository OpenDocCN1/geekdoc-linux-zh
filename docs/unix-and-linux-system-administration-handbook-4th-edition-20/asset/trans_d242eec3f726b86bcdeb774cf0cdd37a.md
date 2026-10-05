

## Linux 细节

将配置信息放在 `/etc` 而将区域（zone）放在 `/var` 的逻辑在于：你作为其他站点的辅助服务器，你无法控制 `named` 写入的区域文件的大小。为了避免可能填充根分区，你可能希望将文件保留在 `/var` 中。对于你作为主服务器的区域，可以与配置文件放在一起（在 `named.conf` 文件中指定绝对路径），也可以存放在 `/var/cache/bind` 中。

如果你想运行一个纯缓存服务器，则不需要修改示例的 `named.conf` 文件。你必须添加任何由你担任权威服务器的区域，建议将它们添加到提供的 `named.conf.local` 文件中。

Ubuntu 提供的示例文件使用了一些新的 BIND 特性，以帮助你的服务器成为网络中良好的 DNS 节点。例如，将 `.com` 和 `.net` 作为仅限代理的区域，以防止用户的输入通过 Verisign 的 Site Finder 工具为其产生广告收入。如果你在内部内部不使用私有地址空间（RFC1918），那么 RFC1918 区域文件可以防止他人逃逸本地网络。Ubuntu 加油！

目录 `/usr/share/doc/bind9` 包含几个非常有用的参考。查看 `README.Debian` 文件（即使在 Ubuntu 上也是）以理解配置 BIND 的策略。

SUSE 的安装程序说明了它正在做什么，并产生了一个合理的、文档齐全的服务器安装。默认情况下，`named` 以用户和组“named”的身份运行在 `/var/lib/named` 的 chrooted 环境中。安装程序创建 chroot 监狱，并填充了运行 `named` 所需的所有文件，甚至是用于 syslog 的 UNIX 域套接字等细节文件。额外的配置文件（`named.conf` 除外）和区域文件存放在 `/etc/named.d` 中，并在 `named` 启动时被复制到监狱中。如果你不想在监狱中运行 `named`，请修改 `/etc/sysconfig/named.conf` 中的以下行：

```
NAMED_RUN_CHROOTED="yes"
```

你只需要更改这里；`/etc/init.d/` 中的启动脚本会引用此信息，并以以一种方式启动 `named`。

SUSE 提供了一个带有有用注释的示例 `/etc/named.conf` 文件，解释了许多选项。SUSE 的 `/etc/named.conf` 像其他系统上的文件一样不是对全球可读的。默认文件导入一个名为 `named.conf.include` 的文件，该文件又导入 `/etc/named.d` 中的 `rnd-access.conf` 文件，两者对所有人都是可读的。SUSE 的安全性意图非常明确。`rnd` 预配置为接受来自本地 SUSE `named.conf` 文件的控制命令，可用于运行纯缓存服务器。如果你想提供区域服务，将区域文件放在 `/etc/named.d` 目录，并在 `/etc/named.conf.include` 文件中列出你的区域名称。

ISC BIND 文档位于 `/usr/share/doc/packages/bind9`。

![](img/579efec8c67772f31ecf34844bbb71a2_731_0.png)

## 第17 章 DNS：域名系统

安装 RHEL 的 BIND 软件包会将二进制文件存放在 `/usr/sbin`，将手册页放在 `/usr/share/man`，添加名为“named”的用户和组，并为数据文件创建目录。“named”用户通过组权限访问数据文件。

与 `/etc/sysconfig/named` 中的此更改不同，`named.conf` 文件存放在 `/etc`（正如 Paul Vissie 和上帝所愿的那样），而区域文件存放在 `/var/named`。没有提供示例文件，`bindconf` 软件包应该包含这些文件。

## Solaris 规范

Solaris 10 附带了 2007 年版本的 BIND 9.3.4-P1；你应该考虑升级。Solaris 使用 BIND 9.6.1-P1 (2009年) 更好用。Solaris 始终在 `in.progname` 中调用其网络程序，`named` 也不例外，因此如果它通过 `in.named` 被调用而不是 `named`，你通常找不到它的 bug（排查信息）。幸运的是，事实并非如此，Solaris 现在调用名为简单的 `named` 的服务器，尽管 `in.named` 名称仍然作为一个链接存在。类似于 Linux，Solaris 使用服务顺序文件 `/etc/nsswitch.conf` 来指定 BIND、NIS、NIS+(仅限 Solaris 10）和 `/etc/hosts` 文件如何相互作用。修改该文件中的 `hosts` 行：

```
hosts: dns
```

会导致名称解析先尝试 `/etc/hosts` 然后是 DNS。将关键服务器放在这里可以缓解在启动时服务可用之前有时发生的“有鸡还是有蛋”的问题。Solaris 的命名服务由 SMF 服务默认启动。SMF 选项指定了命令行参数。表 17.19 Solaris 中的中的 BIND 文件总结了文件名和位置。

| 文件 | 目录 | 说明 |
| :--- | :--- | :--- |
| resolv.conf | /etc | 库配置文件 |
| named | /usr/sbin | 命名守护进程 |
| named-checkconf | /usr/sbin | 检查配置语法 |
| named-checkpoint | /usr/sbin | 检查区域语法 |
| named.conf | /etc | 服务器的配置文件 |
| nsswitch.conf | /etc | 服务切换文件 |

## HP-UX 规范

HP-UX 包含 2005 年版本的 BIND 9.3.2；更棒！HP-UX 为各种数据库组合提供了多个示例 `nsswitch.conf` 文件。将看起来适合你环境的文件拷贝到 `/etc`。类似于 Linux，HP-UX 使用服务顺序文件 `/etc/nsswitch.conf` 来指定 BIND、NIS、NIS+(仅限 Solaris 10）和 `/etc/hosts` 文件如何交互。修改该文件中的 `hosts` 行：

```
hosts: dns
```

会导致名称解析先尝试 `/etc/hosts` 然后是 DNS。将关键服务器放在这里可以缓解在启动时服务可用之前有时发生的“有鸡还是有蛋”的问题。HP-UX 的 `nsswitch.conf` 示例包含了许多解释选项的注释。表 17.20 总结了 HP-UX 的文件名和位置。

| 文件 | 目录 | 说明 |
| :--- | :--- | :--- |
| resolv.conf | /etc | 库配置文件 |
| named | /usr/sbin | 命名守护进程 |
| lwresd | /usr/sbin | 轻量级解析器守护进程 |
| named-checkconf | /usr/sbin | 检查配置语法

| named-checkzone | /usr/sbin | 检查区域语法 |
| named.conf | /etc | 服务器的配置文件 |
| nswitch.conf | /etc | 服务切换文件 |

## AIX 细节

AIX 附带 BIND 8 和 9，分别对应 `named8` 和 `named9`。在发行时，`named` 是 `named8` 的链接，但 ISC 不再支持。它们提供的版本为 8.3.3+ 和 9.2.1（2004年）。AIX 不包含 `named-checkconf` 和 `named-zones` 命令——可能是为了2004年后的 BIND 设计。AIX 下命名服务的启动脚本位于 `/etc/rc.tcpip`。下一页的表 17.21 显示了 AIX 的文件名和位置。

## 表 17.21 AIX 中的 BIND 文件

| 文件 | 目录 | 说明 |
| :--- | :--- | :--- |
| resolv.conf | /etc | 库配置文件 |
| named8 | /usr/sbin | BIND 8 命名守护进程 |
| named9 | /usr/sbin | BIND 9 命名守护进程 |
| named | /usr/sbin | 链接到 named8 [默认] 或 named9 |
| named.conf | /etc | 服务器的配置文件 |
| netsvc.conf | /etc | 服务切换文件 |
| irs.conf | /etc | 另一个服务切换文件 |
| NSORDER | 环境 | 服务切换环境变量 |

