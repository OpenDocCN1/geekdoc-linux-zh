
```
Sep 26 03:12:34 skapet sshd[5279]: Failed password for root from 200.72.41.31 port 40992
ssh2
Sep 26 03:12:35 skapet ssh[5279]: Received disconnect from 200.72.41.31:
11: Bye Bye
Sep 26 03:12:44 skapet ssh[29635]: Invalid user admin from 200.72.41.31
Sep 26 03:12:44 skapet ssh[24703]: input_userauth_request: invalid user admin
Sep 26 03:12:44 skapet ssh[24703]: Failed password for invalid user admin from 200.72.41.31 port 41484 ssh2
```

这表明存在暴力破解攻击，有人或某些程序正尝试发现用户名和密码以进入系统。

如果合法用户需要外部 SSH 访问，更改 SSH 使用的默认端口可以提供一些保护。然而，PF 提供了一个更优雅的解决方案。通过规则（Pass rules）可以对连接主机可执行的操作进行限制，并将违规者被逐逐到一个地址表中，该表将拒绝其部分或全部访问。甚至可以丢弃来自超出限制的机器的所有现有连接。

要配置此项，请在规则集的 `tables` 部分创建此表：

```bash
table <bruteforce> persist
```

然后，在规则集的较早位置添加规则来阻止暴力访问，同时允许合法访问：

```bash
block quick from <bruteforce>
```

```bash
pass inet proto tcp from any to $localnet port $tcp_services \
flags S/A keep state \
(max-src-conn 100, max-src-conn-rate 15/5, \
overload <bruteforce> flush global)
```

括号中的部分定义了限制条件，应根据本地需求更改数字。可以将其理解为：

`max-src-conn` 是允许来自单个主机的并发连接数。

`max-src-conn-rate` 是允许任何单个主机在指定秒数（5秒）内允许的新连接速率（15）。

`overload <bruteforce>` 意味着任何超过这些限制的主机，其地址将被添加到 `bruteforce` 表中。规则将阻止来自 `bruteforce` 表中地址的所有流量。

最后，`flush global` 表示当一个主机达到限制时，该主机的所有（全局）连接都将被终止（flush）。

注意

这些规则不会阻止慢速的暴力破解者，正如 [http://home.nuug.no/~pe-ter/hailmary2013/] 中描述的。

此示例规则集主要用于说明。例如，如果通常情况下允许较数量的连接，但在 ssh 方面希望更具限制性，可以在规则集的早期使用类似下面的内容的规则来补充上述规则：

## 第 31 章 防火墙

```bash
pass quick proto { tcp, udp } from any to any port ssh \
flags S/A keep state \
(max-src-conn 15, max-src-conn-rate 5/3, \
overload <bruteforce> flush global)
```

### 不一定需要阻塞所有重载者

值得注意的是，重载（overload）机制是一种通用技术，并不仅适用于 SSH，而且完全阻止来自违规者的所有流量并不总是最优的。例如，可以使用重载规则来保护邮件服务或 Web 服务，并可以在规则中使用重载表将违规者分配到一个具有最小带宽的队列中。

有时表会增长并占用内存。对于此类情况，PF 提供了过期条目的功能。例如，超过指定时间的 `<bruteforce>` 表条目：

```bash
# pfctl -t bruteforce -T expire 86400
```

类似的功能，`expirable` 可以删除旧于指定时间的条目。

```bash
# pfctl -t expirable -T expire 24h
```

### 31.3.2.6 防止垃圾邮件 (SPAM)

垃圾邮件发送者倾向于发送大量消息，且垃圾邮件主要从被劫持的机器发送。当来自黑列表地址的 SMTP 连接时时，垃圾邮件呈现显示并立即切换到逐字节回答的模式。这种技术通常被称为 *tarpitting*（拦截）。

此示例演示了使用自动更新的黑列表设置垃圾邮件的基本步骤。

步骤 31.1 配置垃圾邮件

1. 安装 `mail/spam` 包或端口。为了使用 `spamd` 的灰名单功能，必须将 `fdescs(5)` 挂载到 `/dev/fd`。在 `/etc/fstab` 中添加以下行：

```
fdescs /dev/fd rw 0 0
```

然后，挂载文件：

```bash
# mount fdescs
```

2. 接下来，编辑 PF 规则集包含：

```bash
table <spamd> persist
table <spamd-white> persist

rdr pass on $Ext_if proto tcp from <spamd> to { $ext_if, $localnet } port smtp -> 127.0.0.1 port 8025

rdr pass on $Ext_if proto tcp from !<spamd-white> to { $ext_if, $localnet } port smtp -> 127.0.0.1 port 8025
```

这两个表 `<spamd>` 和 `<spamd-white>` 是必须的。来自 `<spamd>` 但不在 `<spamd-white>` 中的地址的 SMTP 流量将重定向到监听端口 8025 的 `spamd` 守护进程。

3. 下一步是在 `/usr/local/etc/spamd.conf` 中配置 `spamd` 并添加一些 `rc.conf` 参数。

`mail/spam` 包含了示例配置文件 `/usr/local/etc/spamd.conf.sample` 和 `spamd.conf` 的手册页。参考这些内容可以获得示例所示之外的其他配置选项。配置文件中不以 `#` 注释开头的行之一包含定义 `all` 列表的块，指定了要使用的列表：

```
all:
:traplist:whitelist:
```

此条目通过冒号 (:) 添加了所需的黑列表。要使用白名单从黑列表中剔除地址，将白名单名称紧接在相应黑列表名称之后。例如：`:blacklist:whitelist:`。

随后是指定黑列表的定义：

```
traplist:
:black:
:msg="SPAM. Your address %A 在过去的 24 小时内发送了垃圾邮件":
```

```
:method=http\
:file=www.openbsd.org/spamd/traplist.gz
```

其中，第一行是黑名单的名称，第二行指定列表类型。`msg` 字段包含

在 SMTP 对话期间向黑名单中的发送者显示的消息。`method` 字段指定了 `spamd-setup` 如何获取列表数据；支持的方法包括 http、ftp、从挂载的 `eld` 系统中的文件，以及通过 `exec` 执行外部程序。最后，`file` 字段指定了 `spamd` 期望接收的文件名。

指定的白名单定义类似，但省略了 `msg` 字段，因为不需要显示消息：

```
whitelist:\
:method=file:\
:file=/var/mail/whitelist.txt
```

### 谨慎选择数据源

使用示例 `spamd.conf` 中的所有黑名单将导致互联网的大部分区域被封锁。管理员需要编辑该文件以创建一个优化配置，使用适用的数据源并在必要时使用自定义列表。

接下来，将此条目添加到 `/etc/rc.conf`。额外的参数在注释中指定的 man 手页中有所描述：

614

# 第31章 防火墙

`spamd_flags="-v"` # 使用 "" 并查看 `spamd-setup(8)` 获取标志

完成后，重加载规则集，通过输入 `service spamd-start` 启动 `spamd`，并使用 `spamd-setup` 完成配置。最后，创建一个 `cron(8)` 任务，以合理的间隔调用 `spamd-setup` 来更新表。

在邮件服务器前面的典型网关上，主机将很快在几秒到几分钟内开始被捕获。

PF 还支持灰列表机制（greylisting），它通过 45n 错误代码临时拒绝来自未知主机的消息。那些在合理时间内重试的灰列表主机消息将被允许通过。设置为在 RFC 1123 和 RFC 2821 限制内行为的发送者流量将立即允许通过。

关于灰列表作为一种技术的更多信息，可以在 `greylisting.org` 网站上找到。除了简单之外，灰列表最令人惊讶的地方在于它仍然有效。垃圾邮件发送者和恶意软件编写者在适应并绕过这一技术方面非常缓慢。

配置灰列表的基本步骤如下：

# 过程 31.2 配置灰列表

1. 确保 `fdescfs(s)` 已按照上一个过程步骤 1 中的描述进行挂载。

2. 要以灰列表模式运行垃圾，将此行添加到 `/etc/rc.conf`：

```
spam_grey="YES" # 如果为 YES 则使用垃圾灰列表
```

参考 `spam` man 手页以获取其他相关参数的描述。

3. 完成灰列表设置：

```bash
# service spamd restart
```

```bash
# service spamlogd start
```

在后台，`spamdb` 数据库工具和 `spamlogd` 白名单更新器为灰列表功能执行了核心功能。`spamdb` 是管理员通过 `/var/db/spamdb` 数据库的内容来管理黑、灰、白列表的主要接口。

### 31.3.2.7. 网络卫生

本节描述了如何使用 `block-policy`、`scrub`（清洗）和 `antispoof`（反欺骗）来使规则集的行为正常。

`block-policy` 是一个可以在规则集 options 部分设置的选项，该部分位于重定向和过滤规则之前。此选项决定了 PF 向被规则拦截的主机发送哪些反馈（如果有的话）。该选项有两个可能的值：`drop` 丢弃被拦截的封包且不提供反馈，`return` 返回状态代码（如连接被拒绝）。

如果未设置，默认策略为 `drop`。要更改 `block-policy`，请指定所需的值：

```
set block-policy return
```

在 PF 中，`scrub` 是一个启用网络数据包归一化的关键字。此过程会重组分片数据包，并丢弃具有无效组合的 TCP 包。启用 `scrub` 可以针对基于错误处理数据包分片的某些类型的攻击提供一种保护措施。有许多可用选项，但最简单的形式适用于大多数配置：

```
scrub in all
```

某些服务（如 NFS）需要特定的分片处理选项。更多信息请参阅 https://home.nnug.org/~-peter/pf/en/scrub.html。

615

# 启用 ALTQ

此示例重组了分片，清除了“不要分片”位，并将最大段大小设置为 1440 字节：

```
scrub in all fragment reassemble no-df max-mss 1440
```

`antispoof` 机制防止来自伪造或仿冒 IP 地址的活动，主要通过拦截出现在逻辑上不可能的接口和方向上的封包。

这些规则过滤掉了来自世界其他地区的欺骗流量，以及任何源自本地网络的欺骗封包：

```
antispoof for $ext_if
```

```
antispoof for $int_if
```

### 31.3.2.8. 处理不可路由地址

即使有了正确配置的网关来处理网络地址转换，可能仍需要补偿他人的配置错误。常见的配置错误是让带有不可路由地址的流量流互联网。由于来自不可路由地址的流量可能参与多种 DoS 攻击技术，请考虑显式阻止流量从外部接口进入网络。

在此示例中，定义了一个包含不可路由地址的宏，然后将其用于拦截规则。访问这些地址的流量在网关的外部接口上被静默丢弃。

```
martians = "{ 127.0.0.0/8, 192.168.0.0/16, 172.16.0.0/12, \
10.0.0.0/8, 169.254.0.0/16, 192.0.2.0/24, \
0.0.0.0/8, 240.0.0.0/4 }"
```

```
block drop in quick on $ext_if from $martians to any
```

```
block drop out quick on $ext_if from any to any $martians
```

### 31.3.3. 启用 ALTQ

在 FreeBSD 上，ALTQ 可以配合 PF 使用以提供服务质量 (QOS)。一旦启用 ALTQ，可以在规则集中定义队列，这些队列决定了输出数据包的处理优先级。

在启用 ALTQ 之前，请参考 `altq(4)` 确定安装在系统上的网卡驱动是否支持它。

ALTQ 不作为加载内核模块可用。如果系统接口支持 ALTQ，请使用第 8 章“配置 FreeBSD 内核”中的说明创建自定义内核。可以使用以下内核选项。需要 `rst` 来启用 ALTQ。至少需要其他选项之一来指定队列调度算法：

```
options ALTQ
```

```
options ALTQ_CBQ # 基于类的队列 (CBQ)
```

```
options ALTQ_RED # 早期检测 (RED)
```

```
options ALTQ_RIO # 早期检测入出 (RIO)
```

```
options ALTQ_HFSC # 分级公平服务调度器 (HFSC)
```

```
options ALTQ_PRIQ # 优先级队列 (PRIQ)
```

可用以下调度算法：

CBQ 基于类的队列 (CBQ) 用于将带宽分为不同的类或队列，根据过滤规则划分流量。

RED 早期检测 (RED) 通过测量队列长度并与阈值比较来避免网络拥塞。当队列超过最大值时，随机丢弃新包。

616

# 第31章 防火墙

RIO 早期检测入出 (RIO) 模式维护队列长度并为每个 QoS 级设置多个阈值。

HFS级公平服务调度器 (HFSC) 的描述见 http://www-2.cs.cmu.edu/~zhang/HFSC/main.html。

PRI 优先级队列 (PRIQ) 总是通过高队列的流量。关于调度算法和示例规则集的更多信息可以在 OpenBSD 的存档中找到。

### 31.4. IPFW

`IPFW` 是为 FreeBSD 编写的状态防火墙，同时支持 IPv4 和 IPv6。它由多个部分组成：内核过滤器及其集成的数据包计数设施、日志设施、NAT、`dummynet(4)` 流量整形、转发设施、桥接设施以及隐形设施。

FreeBSD 在 `/etc/rc.firewall` 提供了一个示例规则集，定义了常见场景的防火墙类型，以帮助新手用户生成合适的规则集。`IPFW` 提供了强大的语法，高级用户可以创建满足环境安全需求的自定义规则集。

本节介绍了如何启用 `IPFW`，提供了其规则语法概述，并演示了常见配置场景的规则集。

### 31.4.1. 启用 IPFW

`IPFW` 作为内核加载模块包含基础 FreeBSD 安装中，因此不需要自定义内核。对于希望将 `IPFW` 静态编译到自定义内核的用户，请参见第 31.4.6 节“IPFW 内核选项”。要要配置系统在启动时启用 `IPFW`，请在 `/etc/rc.conf` 中添加 `firewall_enable="YES"`：

```
# sysrc firewall_enable="YES"
```

要使用 FreeBSD 提供的默认防火墙类型之一，请添加行指定类型：

```
# sysrc firewall_type="open"
```

可用类型有：

- open: 允许所有流量。

- client: 仅保护此机器。

- simple: 保护整个网络。

- closed: 除了环回接口（loopback interface）外，完全禁用 IP 流量。

- workstation: 使用状态检测规则仅保护此机器。

- filename: 包含规则集的文件的完整路径。

617

# IPFW 规则语法

如果 `firewall_type` 设置为 `client` 或 `simple`，请修改 `/etc/rc.firewall` 中的默认规则以设置系统配置。

请注意，`filename` 类型用于加载自定义规则集。

加载自定义规则集的另一种方法是将 `firewall_script` 变量设置为包含 IPFW 命令的可执行脚本的绝对路径。本节中使用的示例假设假设 `firewall_script` 已设置为 `/etc/ipfw.rules`：

```
# sysrc firewall_script="/etc/ipfw.rules"
```

要通过 `syslogd(8)` 启用日志，请包含此行：

```
# sysrc firewall_logging="YES"
```

# 警告

只有带有 `log` 选项的防火墙规则会被记录。默认规则不包含此选项，必须手动添加。因此，建议对默认规则集进行日志编辑。此外，如果日志存储在单独的文件中，可能需要日志轮转。

没有 `/etc/rc.conf` 变量来设置日志限制。要限制规则在每次连接尝试中被记录的次数，请在 `/etc/sysctl.conf` 中通过此行指定数量：

```
# echo "net.inet.ip.fw.verbose_limit= 5" >> /etc/sysctl.conf
```

要通过名为 `ipfw0` 的专用接口启用日志，请在 `/etc/rc.conf` 中添加此行而不是：

```
# sysrc firewall_logif="YES"
```

然后使用 `tcpdump` 查看记录的内容：

```
# tcpdump -t -n -i ipfw0
```

提示

除非挂载了 `tcpdump`，否则日志记录不会产生开销。
