
如果你不是为了使用互联网使用 DNS，你可以将你的主名称服务器声明为根域名的权威服务器。这种配置可能适用于未连接互联网的小型公司，或适用于在防火墙后隐藏其本地结构的组织。

在这种设置下，你的提示文件应该指向本地名称服务器，而不是互联网的根服务器。你仍然应该获得注册域名和法的 IP 地址，或者使用第 279 页描述的 RFC1918 私有地址。

# 16.16 厂商规格

本节描述了我们热心的厂商在 ISC 免费分发的 BIND 代码中提交的抽象。我们提供了配置文件的指针、每个厂商软件所基于的 BIND 版本，以及关于如何将 BIND 与其他管理数据源（如文件或 NIS）集成的信息。

关于此主题的更全面讨论请见第 18 章。特别，请参考从第 523 页开始的内容。

## Solaris 详解

Solaris 7 和 8 目前都运行着 BIND 8.1.2。Solaris 使用一个名为 `/etc/nwitch.conf` 的顺序文件来指定 BIND、NIS、NIS+ 和 `/etc/hosts` 如何相互作用。将该文件中的 hosts 行修改为

`hosts: files dns`

会导致名称解析首先查找 `/etc/hosts`，然后是 DNS。将关键服务器和路由器放在 `/etc/hosts` 文件中，可以缓解有时在启动时名称服务可用之前发生的“先有鸡还是有蛋”的问题。

Sun 手册建议你在 DNS 转发模式下运行 NIS 服务器，在该模式下，它们会将无法从本地数据库回答的查询转发到 DNS 服务器。因此，厂商推荐的配置是

```
hosts: nis [NOTFOUND=return] files
```

我们持不同意见。本地 NIS 服务器的速度并不比本地 DNS 服务器快，而且为了让外部世界访问你的站点，数据必须在 DNS 中。即使你的站点使用 NIS，最好也保持这两个系统分开。

表 16.17 总结了 Solaris 上的 BIND 文件名和位置。

### 表 16.17 Solaris 中的 BIND 文件

| 文件 | 目录 | 描述 |
|---|---|---|
| resolv.conf | /etc | 解析器库配置文件 |
| in.named | /usr/bin | 名称服务器守护进程 |
| named-xfer | /usr/bin | 区域传输代码 |
| named-conf | /etc | 名称服务器的配置文件 |
| named-pid | /etc | 运行中的 in.named 目录进程 ID |
| named-run | | 调试模式的输出 |
| named-stats | | 统计输出 |
| named-dump.db | | 整个数据库的转储 |
| named-bootconf | /usr/bin | 将 BIND 4 配置转换为 BIND 8 格式 |

- a. `/etc/named.conf` 中指定的作为 BIND 文件存放的目录

Solaris 页面说 `in.named` 包含几个谎言。它提到通过 IOT 信号转储统计信息，但 Solaris 的 `kill` 命令不支持该信号；它已被 ABRT 信号取代。然而 ABRT 并转储统计信息——它只是杀死了 `named` 进程。我们通过阅读源码发现，是 ILL 信号转储了统计文件。

主页还说数据库被转储到 `nameddumpdb`，但这也是错误的。正确的文件名是 `named_dump.db`。从 BIND 4 到 BIND 8 的切换可能没有包含对主页的仔细重写（可能甚至由 BIND 的人员编写）。

## HP-UX 详解

HP-UX 11.00* BIND 基于 BIND 4.9.7。它使用与 Solaris 相同的 `nsswitch.conf` 系统。原始系统在 `/etc` 目录下有几个示例文件，但没有一个名为 `nsswitch.conf` 的。（尝试 `ls /etc/nss*` 查看你的选项。）

要创建一个 `nsswitch.conf` 文件，请阅读主页查看你想实现的配置，并从提供的示例中窃取正确的片段。示例之一是 `/etc/nsswitch.hp_defaults`，它显示了当 `nsswitch.conf` 文件不存在或包含语法错误时你将获得的行为。

如果没有 `nsswitch.conf` 文件，红帽（Red Hat）默认 如下方案：

`hosts: dns [UNAVAIL=return] files`

- db files nisplus dns

我们推荐推广 DNS 并使用该配置。Red Hat 有一些示例配置文件，但它们直接在 `/etc` 中，而不是专门的目录。示例非常棒。`named.conf` 没有手册页。

## FreeBSD 详解

FreeBSD 3.4 和 4.0 包含 BIND 8.2.2-P5。一个名为 `/etc/host.conf` 的服务顺序文件控制主机查找的服务顺序。可能主机信息源列在不同的行上，按你希望查询的顺序排列：

```
# 首先尝试 /etc/hosts 文件
hosts
# 现在下一步尝试名称服务器
bind
# 如果你配置了 Y/NIS，取消下一行的注释
# nis
```

# 第 16 章 域名系统 485

如果 `host.conf` 文件不存在，则首先查询 DNS。如果失败，则查询 `/etc/hosts`。FreeBSD 已将 `named.conf` 从 `/etc` 目录移动到 `/etc/namedb`。表 16.20 总结了相关的文件名和位置。

### 表 16.20 FreeBSD 中的 BIND 文件

| 文件 | 目录 | 描述 |
| --- | --- | --- |
| resolv.conf | /etc | 解析器库配置文件 |
| named | /usr/sbin | 命名服务器守护进程 |
| named-xfer | /usr/libexec | 区域传输代码 |
| named.conf | /etc/namedb | 命名服务器配置文件 |
| named.pid | /var/run | 运行中 named 的进程 ID |
| named.run | 目录* | 调试模式输出 |
| named.stats | 目录* | 统计输出 |
| named.memstats | 目录* | 内存使用统计 |
| named_dump.db | /etc/namedb | 整个数据库转储 |

a. `/etc/namedb/named.conf` 中指定的目录作为 BIND 文件的家目录。

`/etc/namedb` 包含几个文件：用于 `named.root` 的根缓存文件、本地主机反向区域文件的原型（PROTO.localhost.rev），以及一个名为 `make-localhost` 的 shell 脚本，它会提示你的域名，然后从原型创建正确的反向区域文件。

`/usr/sbin` 中的 `named-bootconf` Perl 脚本将 BIND 4 的 `named.boot` 转换为 BIND 8 的 `named.conf` 启动文件。

在我们看来，位于 `/etc` 的 `named.conf` 应该是一个可惩罚的行为；我们建议你对其建立链接，以便两个名称都能工作。查看示例 `named.conf` 文件底部的注释，我们推测 FreeBSD 原意是指在 chroot 环境（chrooted environment）中运行 named。然而，默认配置并没有实际这样做。更多信息请参阅 `/etc/defaults/rc.conf` 中的 `named_*` 变量。

FreeBSD 的 `named` 手页涉及某些路径，例如统计文件和转储数据库。它在来自 isc.org 的发行版中可能是错误的，因为 Solaris 和 FreeBSD 均存在相同的错误。

## 16.17 推荐阅读

DNS 和 BIND 由多种来源描述，包括随发行版附的文档、几本关于互联网主题书籍的章节、O'Reilly Nutshell 系列中的整本书，以及各种在线资源。

### 邮件列表和新闻组

以下邮件列表与 BIND 联：

- bind-users – 邮件至 `bind-users-request@isc.org` 加入
- bind-announce – 邮件至 `bind-announce-request@isc.org`
- nameddroppers – 邮件至 `nameddroppers-request@internet.net`
- bind-workers – 邮件至 `bind-workers-request@isc.org`（代码战士）

将错误报告发送至 `bind-bugs@isc.org` 或 `bind9-bugs@isc.org`。

### 书籍和其他文档

NOMIN BIND 开发团队。《BINDv9 管理员参考手册》。可在 www.isc.org 的 BIND 发行版 (doc/arm) 中获取。
