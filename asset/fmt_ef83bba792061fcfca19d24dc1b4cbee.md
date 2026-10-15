
| `ypxfrd` | 为 `ypxfr` 提供服务（在主服务器上运行） |
| `yppush` | 使从服务器更新其映射版本 |
| `makedbm` | 从平面文件构建哈希映射 |
| `ypmake*` | 从已更改的平面文件重建哈希映射 |
| `ypinits` | 将主机配置为主服务器或从服务器 |
| `ypset` | 使 `ypbind` 连接到特定服务器^b |
| `ypwhich` | 查找当前主机正在使用的服务器 |
| `yppoll` | 查找服务器正在使用的映射版本 |
| `ypcat` | 打印 NIS 映射中包含的值 |
| `ypmatch` | 打印指定键的映射条目 |
| `yppasswd` | 在 NIS 主服务器上更改密码 |
| `ypcfhn` | 在 NIS 主服务器上更改 GECOS 信息 |
| `ypchsh` | 在 NIS 主服务器上更改登录 shell |
| `yppasswdd` | 是 `yppasswd`、`ypchsh` 和 `ypcfhn` 的服务器 |
| `yppupdated*` | 是用于更新 NIS 映射的服务器（由 `inetd` 管理） |

a. 并非在所有系统上使用或支持

b. 必须通过 `ypbind -ypsetme` 或 `ypbind -ypset` 明确启用（危险）

### NIS 安全

NIS 不安全。广播模式尤其糟糕；网络上的任何主机都可以声称为特定域提供服务，然后向 NIS 客户端提供虚假的管理员数据。在 Linux 系统上，您可以通过为每个客户端明确列出允许的 NIS 服务器来缓解此特定问题。

如果您对环境中的安全性有任何担忧，就不应该使用 NIS 来提供 `passwd` 或 `shadow` 文件。为此目的使用替代的分布式身份验证机制，例如 LDAP。

在旧版本的 NIS 中发现了许多安全漏洞。确保您运行的是当前版本。

## 19.5 优先排序管理信息来源

管理信息可以通过多种方式分发。每个系统都理解平面文件并知道如何使用 DNS 来查找主机名和 Internet 地址。由于给定的信息可能来自多个潜在来源，因此您也可以指定要检查的来源以及检查的顺序。

`/etc/nsswitch.conf`（AIX 上为 `/etc/netsvc.conf`）配置文件允许为每种类型的配置信息指定显式的搜索路径。典型的 `nsswitch.conf` 文件看起来像这样：

```
passwd: files ldap
hosts: files dns
group: files
...
```

每行配置一种信息类型（通常，一个平面文件等价物）。常见的来源有 `nis`、`nisplus`、`files`、`dns`、`ldap` 和 `compat`；它们分别指 NIS、NIS+、* 纯平面文件（忽略“+”等标记）、DNS、LDAP 和 NIS 化平面文件。DNS 仅对主机和网络信息是有效的数据源。

来源按从左到右的顺序尝试，直到其中一个为查询提供答案为止。在上面的示例中，`gethostbyname` 例程首先会检查 `/etc/hosts` 文件，如果主机未在其中列出，则会检查 DNS。另一方面，关于 UNIX 组的查询只会检查 `/etc/group` 文件。

如果需要，您可以通过在其后加上带括号的表达式来更具体地定义来源的“失败”。例如，行

```
hosts: dns [NOTFOUND=return] files
```

会导致如果 DNS 可用则专门使用 DNS；名称服务器的负面响应会使查询立即返回（并带有失败代码），而不检查平面文件。但是，如果没有可用的名称服务器，则会使用平面文件。各种类型的失败在表 19.5 中显示；每个都可以设置为 `return` 或 `continue`，表示查询应被中止还是转发到下一个来源。

### 表 19.5 /etc/nsswitch.conf 中识别的失败模式

| 条件 | 含义 |
|---|---|
| `UNAVAIL` | 源不存在或已关闭。 |
| `NOTFOUND` | 源存在，但无法回答查询。 |
| `TRYAGAIN` | 源存在但忙碌。 |
| `SUCCESS` | 源能够回答查询。 |

6. 原始 NIS 的一个命运多舛的继任者，现已被 Sun 停用，但仍由一些系统出于历史原因支持。

默认情况下，大多数系统都附带了适用于独立机器的 `nsswitch.conf` 文件。所有条目都指向平面文件，除了主机查找，先查询平面文件然后查询 DNS。少数系统对 `passwd` 和 `group` 默认使用 `compat` 模式，这可能值得更改。如果你确实使用 NIS，就明确将其写入 `nsswitch.conf` 文件。

### nscd：缓存查找结果

在某些 Linux 发行版中，另一个参与系统文件处理的组件是 `nscd`，即名称服务缓存守护进程，其名称有些误导。

`nscd` 与 C 库协同工作，缓存 `getpwent` 等库调用的结果。`nscd` 只是这些库例程的包装器；它对实际查询的数据源一无所知。理论上 `nscd` 应该能提升查找性能，但从用户角度来看，任何提升都几乎无法察觉。

我们说“名称服务缓存守护进程”具有误导性，因为“名称服务”一词通常指的是 DNS，即在主机名和 Internet 地址之间进行映射的分布式数据库系统。`nscd` 确实会缓存 DNS 查找结果（因为它包装了 `gethostname` 等），但它也会包装访问 `passwd` 和 `group` 文件及其网络数据库等价物的库例程。 （出于安全考虑，对 `/etc/shadow` 的查找不会被缓存。）

从概念上讲，`nscd` 除了加快重复查找之外，不应对系统的运行产生任何影响。实际上，它可能导致意外行为，因为它维护着查找结果的自己的副本。查找结果会在缓存中保留固定时间（在 `nscd` 的配置文件 `/etc/nscd.conf` 中设置），并且总有可能最近的更改在旧数据超时之前不会反映在 `nscd` 的缓存中。`nscd` 足够智能，能够监控本地数据源（例如 `/etc/passwd`）的更改，因此本地更新应在 15 秒内传播。对于通过 NIS 等检索的远程条目，你可能必须等待完整的超时时间后更改才会生效。

在我们的示例发行版中，只有 SUSE 默认运行 `nscd`。Red Hat 安装了 `nscd`，但默认在启动时不启动它；要启用 `nscd` 的使用，请运行 `chkconfig nscd on`。Ubuntu 与 `nscd` 兼容，但默认安装中不包含 `nscd`；运行 `apt-get install nscd` 即可下载它。

`nscd` 在启动时启动并持续运行。默认的 `/etc/nscd.conf` 对 `passwd` 数据指定 10 分钟超时，对 `hosts` 和 `group` 指定一小时超时，负向超时为 20 秒（即在重新尝试不成功查找之前的等待时间）。实际上，这些值很少需要更改。如果你最近做的更改似乎没有显示出来，`nscd` 很可能是原因。

请参阅第 17 章了解有关 DNS 的更多信息。

## 19.6 推荐阅读

- Carter, Gerald. *LDAP System Administration*. Sebastopol, CA: O’Reilly Media, 2003.
- Malère, Luiz Ernesto Pinheiro. *LDAP Linux HOWTO*. tldp.org
- Voglmaier, Reinhard. *The ABCs of LDAP: How to Install, Run, and Administer LDAP Services*. Boca Raton, FL: Auerbach Publications, 2004.
- *LDAP for Rocket Scientists*. zytrax.com/books/ldap

## 19.7 练习

- E19.1 为什么“拉取”方法更新本地机器文件比“推送”方法更安全？
- E19.2 解释 `rdist` `distfile` 中的以下摘录：

```
LINUX_PASSWD = ( redhatbox unbox susbox )
passwd:
    ( /etc/passwd ) -> ( ${LINUX_PASSWD} )
    install /etc/passwd:dist;
    cmds special /etc/passwd rdist "-u/local/bin/mkpasswd";
```

- ★ E19.3 解释 `rdist` 与 `rsync` 之间的区别。在什么情况下使用其中一个会比另一个更好？
- ★ E19.4 你使用什么方法共享系统文件？该方法有哪些安全问题？建议一种在你站点共享系统文件的替代方法，并详细说明它解决的问题。有什么缺点吗？
- ★★★★★ E19.5 设计一个 LDAP 模式，用于存储用户信息，如登录名、密码、shell、授权机器等。构建一个工具，可交互地或从包含用户列表的文件中将新用户输入数据库。构建一个工具，可从 LDAP 数据库为实验室中的机器生成 `passwd`、`group` 和 `shadow` 文件。允许用户在每台机器上使用不同的密码（如果他们愿意）。 （并非所有用户都一定有权使用每台计算机。）你的 `adduser` 系统应能够打印现有用户登录名列表，并为新用户打印登录名/密码对。
