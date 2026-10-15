
### DNS sanity checking tools

有几种工具可检查 DNS 环境的各个方面。`named-checkconf` 和 `named-checkzone` 与 BIND 9 一起提供；它们检查 `named.conf` 文件和区域文件的基本语法（而非语义）。NSD 和 Unbound 包含类似的工具，称为 `nsd-checkconf` 和 `unbound-checkconf`。

原始的 DNS 检查工具是 `nsint`，由 Craig Leres 在劳伦斯伯克利实验室时编写。`doc`，即域名粗俗控制程序，用于检查委派并查找部署 DNS 中的不一致和错误，下面会更详细地讨论。该工具 `lamers`（与 `doc` 相同网站）会翻阅日志文件并向违规站点的 DNS 管理员发送电子邮件，告知他们存在跛脚委派并说明如何修复问题。`DDT` 由 Jorge Frazao 和 Artur Romao 编写，用于调试缓存数据。

`dnswalk` 遍历你的委派树并识别父子之间或正向与反向记录之间的不一致。它还会查找缺失的点、不必要的胶水记录等。它是一种通用的 DNS 卫生提醒。`dnswalk` 需要能够执行区域传输才能发挥其魔力。

第 663 页描述了几种 DNSSEC 调试和管理工具。

`doc` 是一个 C shell 脚本。它目前由 Brad Knowles 维护，可从其网站下载：`shub-internet.org/brad/dns`（注意是“shub”，不是“shrub”）。如果你计划将 `doc` 放入路径或从 cron 运行它，必须编辑脚本并将 `auxd` 变量设置为指向安装目录。

`doc` 通过反复调用 `dig` 来检查委派。它报告与特定域名相关的不一致、错误和其他问题。其屏幕输出总结了发现的问题。它还在当前目录中生成一个详细日志文件，其中包含详细信息。

`doc` 使用本地名称服务器进行查询。如果你的域名使用了 BIND 的 `view` 语句，并且在内部视图中包含了 RFC9186 私有地址，在内部视图上运行 `doc` 会让 `doc` 感到困惑，并使其报告虚假错误。如果使用视图，请从域外运行 `doc`，使其看到外部用户所看到的内容。

以下是 `doc` 对上述 lame 域名 `w3w3.com` 的说法：

```
$ doc w3w3.com

Doc-2.2.3: doc w3w3.com

Doc-2.2.3: Starting test of w3w3.com.   parent is com.

Doc-2.2.3: Test date - Tue Jul 21 21:15:11 MDT 2009

Summary:

        ERRORS found for w3w3.com. (count 1)

        WARNINGS issued for w3w3.com. (count: 1)

Done testing w3w3.com. Tue Jul 21 21:15:21 MDT 2009
```

`doc` 将测试的详细信息和发现的错误（共 600 多行）放在其日志文件中，在本例中为 `log.w3w3.com`:

```
ERROR: no SOA record for w3w3.com. from ns1.nameservices.net.
```

`doc` 并没有将 `w3w3.com` 明确标记为“lame delegation”，但这就是它识别出的根本问题。沿着父区域的 NS 记录进行跟踪，它检查了 `ns1.nameservices.net` 是否确实作为 `w3w3.com` 的权威名称服务器运行；事实并非如此。

如果你管理一个包含子域的域名（或不信任父域的管理者），请考虑每周通过 cron 运行一次 `doc`，以验证与你的域名相关的所有委派是否正确。

### Performance issues

BIND 9 在多处理器架构上的性能不如其开发者所希望的那样快，但多个根服务器使用 BIND 9 并愉快地处理每秒数万次查询。性能对于大多数站点来说可能已经足够了。但 NSD 和 Unbound 的性能甚至更好，尤其是在 DNSSEC 签名的区域。

我们已经多次说过这一点，但仍需重申：请将你的 TTL 设置为合理的值——以周或天为单位，而不是分钟或秒。短 TTL 的使用会惩罚你（因为你必须不断重新提供相同的记录）也会惩罚你的网络客户端（因为它们必须不断获取这些记录）。它还为潜在攻击者提供了缓存投毒的机会。一些名称服务器会选择性地忽略它们不喜欢的 TTL（看起来不合理地长或不合理地短）。

分页会非线性地降低服务器性能，因此不要在运行名称服务器的主机上吝啬内存。对于递归服务器，你需要等待大约一周的时间让内存占用稳定下来；参见第 571 页。

要估算 `nsd` 为提供你的权威数据所需的内存，请填写 `nlnetlabs.net/nsd/nsd-memsize.html` 上的网络表单。很棒！

使用转发器。有关转发的讨论请参见第 606 页。

许多系统上启动 `named` 的 init 脚本提供了额外的入口点（例如 `reload`），这些入口点 intended for use by system administrators。但使用 `rndc` 更简单且跨平台效率更高。

不要使用 `inetd` 或 `xinetd` 来管理名称服务器；它每次需要时都会重启服务器，极大地减慢响应时间并阻止任何有用的缓存的形成。

有关 `inetd` 的更多信息请参见第 1188 页。

## 17.16 VENDOR SPECIFICS

本节描述了我们在各个厂商平台上名称服务软件的状态。每个人都提供 BIND，尽管在安装操作系统时你可能需要指定要安装它，或稍后作为软件包安装。

就升级到 BIND 最新版本而言，Linux 发行版在很大程度上比其 UNIX 同类产品更灵活。即使如此，名称服务至关重要。你可能希望制定获取最新源代码分发版并自行构建的策略，而不是等待软件包可用。

Ubuntu 和 Red Hat 均以软件包的形式提供完整的 NSD/Unbound 套件；SUSE 在其官方存储库中仅提供 Unbound。目前，所有打包版本都有些过时，因此对于 BIND，你可能只想从 `nlnetlabs.nl` 获取最新源代码并自行构建。

在本节中，我们包括指向配置文件、每个厂商软件所基于的 BIND 版本的指针，以及如何将 BIND 与其他管理数据源（如平面文件或 NIS）集成的相关信息。关于最后一个主题的更完整讨论在第 19 章中提出。特别是，请参考第 739 页开始的内容。

我们还包括指向应在启动时执行的启动脚本的指针，以启动名称服务器。如果名称服务停止，你的网络、电子邮件、网站——一切都将停止。一些站点使用诸如 BIND 分发版中的 `nanny` 脚本之类的保持运行脚本。

有关系统启动脚本的更多信息请参见第 87 页。

### Specifics for Linux

![](img/14d78e3cecac4581d37024baf1e94cca_729_0.png)

Linux 的 BIND 软件包安装了一个通过 init 运行的 `named` 启动脚本：Ubuntu 为 `/etc/init.d/bind9`，RHEL 和 SUSE 为 `/etc/init.d/named`。

Linux 的 `named` 软件包将事物安装在所有常规位置。表 17.18 显示了详细信息。Red Hat 有一些与他们的 Network Manager 交互的额外组件

tool 通过 `-D` 命令行标志传递给 `named`。详细信息可在 Red Hat BIND 包中的 `doc/README-DBUS` 文件中找到。

### Table 17.18 BIND files in Linux

| File | Directory | Description |

|---|---|---|

| `resolv.conf` | `/etc` | 解析库配置文件 |

| `named`, `lwres` | `/usr/sbin` | 名称服务器守护进程 |

| `lwresd` | `/usr/sbin` | 轻量级解析器 |

| `named.conf` | `/etc` | `named` 配置文件（RHEL 和 SUSE） |

|  | `/etc/bind` | `named` 配置文件（Ubuntu） |

| `named-checkconf` | `/usr/sbin` | 检查配置文件语法 |

| `named-checkzone` | `/usr/sbin` | 检查区域文件语法 |

| `namedGetForwarders` | `/usr/sbin` | 仅 Red Hat，用于 Network Manager 工具 |

| `namedSetForwarders` | `/usr/sbin` | 仅 Red Hat，用于 Network Manager 工具 |

| `nsswitch.conf` | `/etc` | 服务切换文件 |

Linux 使用一个切换文件 `/etc/nsswitch.conf` 来指定应如何执行主机名到 IP 地址的映射，以及是否应首先、最后或根本不尝试 DNS。如果没有切换文件，则默认行为为

```
hosts: dns [!UNAVAIL=return] files
```
