
默认情况下，`NSD` 绑定到所有网络接口（包括 IPv4 和 IPv6）的 53 端口。如果你在 `ip-address` 中列出地址，`nsd` 将跳过内核路由表，并确保对一个 IP 地址的查询不会收到来自不同 IP 地址的回答；许多解析器需要这一点。如果你的机器只有一个网络接口，则此选项将没有用处。`ip4-only` 和 `ip6-only` 选项将 `nsd` 限制在特定协议，而 `port` 设置监听传入查询的网络端口。

通常你不需要这些选项中的任何一个，因为默认值已经很好。

- - `identity`: string [`hostname`]
- `hide-version`: yes | no [`no`]

这对选项控制 `nsd` 在查询 CHAOS 类名 `id.server` 和 `version.server` 时，是否对其版本号和主机名提供诚实信息。如第 598 页所示，建议不要篡改这些值。

- - `logfile` filename [`stderr` and `syslog`]
- `verbosity`: level [`u`]
- `debug-mode`: yes | no [`n0`]
- `statistics`: secs [`u`] # `statistics`

日志默认输出到标准错误（`stderr`）和 `syslog`（`daemon`），日志量由 `verbosity` 选项决定。可能值的范围是 0–5；数字越大，表示应该记录更多数据。`logfile` 允许将消息重定向到文件而不是发送到 `syslog`。

如果你指定了 `debug-mode`，`nsd` 不会派生额外的副本，而是保持在你的终端中，这样你可以看到发送到标准错误的消息。

如果你想保留统计信息，请使用 `#sec` 指定两次转储之间的秒数。统计信息将进入日志文件，或者在未指定文件时发送到 `syslog`。最好观察一下统计输出，以确保你选择了合理的转储间隔，并且没有用那些没人会看的信息填满你的磁盘。

- - `database`: filename [`/var/db/nsd.db`]
- - `diffile`: filename [`/var/db/nsd/ifr.db`]
- - `xfrfile`: filename [`/var/db/nsd/xfrd.state`]
- - `pid-file`: filename [`OS-specific`, usually `/var/run/nsd.pid`]
- - `zonesdir`: directory [`/etc`]

编译后的文件和区域数据默认存放在 `/var/db/nsd`；你可能不需要更改它。PID 文件应该遵循你的操作系统存放其他 PID 文件的位置，通常在 `/var/run`。默认情况下，可编辑文件区域位于 `/etc/nsd`，这看起来像是个糟糕的选择。考虑将它们移动到 `/var` 下，或许移动到 `/var/nsd/zones`。

- - `tcp-count`: int [`10`]
- - `server-count`: int [`1`]
- - `xfrd-reload-timeout`: #sec [`10`]

`tcp-count` 限制了服务器用于区域传输时可使用的并发 TCP 连接数。当你在日志中看到 "xfrd: max number of TCP connections (10) reached" 时，你就知道自己已经超过了限制。如果这种情况频繁发生，你应该增加此限制。

# NSD 区域特定配置选项

`server-count` 选项指定要启动的 `nsd` 实例数量。对于多 CPU 机器，你可能想增加此值。

# 第 17 章 DNS：域名系统

`incremental` 参数指定区域传输请求通过 UDP 发送而不是默认的 TCP。最好的办法是使用 TCP。`Source IP address outgoing-interface: ip-spec` 列表控制从服务器请求区域传输或主服务器发送通知的 IP 地址。地址必须匹配；主服务器配置中的访问控制子句必须使用与从服务器相同的地址。

# NSD 区域特定配置选项

`server-count` 选项指定要启动的 `nsd` 实例数量。对于多 CPU 机器，你可能想增加此值。

`unbound-host` 不像 `dig` 或 `drill` 那么详细，但在测试 DNSSEC 时，用于命令行验证非常方便。

表 17.11 显示了 Unbound 组件的位置。

# 表 17.11 Unbound 安装目录

| 项目 | 目录 |
| --- | --- |
| 二进制文件 | `/usr/local/sbin` |
| 库 | `/usr/local/lib` |
| 配置文件 | `/usr/local/etc/unbound/unbound.conf` |
| 手页页 | `/usr/local/share` |
| 安全沙箱 | `/usr/local/etc/unbound` |
| PID 文件 | `/usr/local/etc/unbound` |

`unbound` 的配置文件 `unbound.conf` 与 `nsd` 类似。基本语法如下：

```
attribute: value
```

注释以 `#` 开头，并持续到行尾。你可以运行 `unbound-checkconf` 来检查配置文件的有效性。

这里是一个 `unbound.conf` 文件的简单示例，根据帮助页进行了调整，使用了更合理的路径并增加了一些注释：

```
server:
directory: "/var/unbound/etc"
username: unbound
chroot: "/var/run"
pidfile: "/var/run/unbound.pid"
root-hints: "root.cache"
interface: 0.0.0.0
# 监听所有 IPv4 接口
interface: 0
# 以及所有 IPv6 接口
控制access-control: 10.0.0.0/8
# 本地私有网络
access-control: 2001:db8::/64
# 本地 IPv6 网络
```

此示例在所有接口上列表，并允许来自本地 IPv6 网络和未路由私有网络 10 的查询。它以守护进程模式（默认）记录日志到 `syslog`，并以 `unbound` 身份运行在 `chroot` 沙箱中。

递归查询带有许多选项；`unbound` 的选项列表几乎是 BIND (150+) 规模的一半 (70+)。我们的涵盖是选择性的。完整内容请参阅 `unbound.net` 上的帮助页和文档。

`unbound` 的配置语言有四个顶级语句：`server`、`remote-control`、`stub-zone` 和 `forward-zone`。全局选项出现在 `server` 语句下方。以下是一些重要的选项。

## 第 17 章 DNS：域名系统

### 位置

| `directory`: directory | `/usr/local/etc/unbound` |
| `pidfile`: filename | `/usr/local/etc/unbound.pid` |
| `root-hints`: filename | [none] |

`directory` 选项设置工作目录，`unbound` 默认位于 `/usr/local/etc` 下的目录，但许多站点更倾向于 `/var`。PID 文件默认位于 `unbound` 工作目录，但它更传统的位置（如 `/var/run`）也可以正常工作。

根提示（Root hints）内置在 `unbound` 代码中，不需要提示文件。然而，如果你愿意，可以提供一个文件，因为代码中的地址可能会过。偶尔使用 `dig .ns` 获取最新副本，如果你非常疑虑，可以尝试 `dig@root-servers.net` 获取权威副本。

### 日志

| `use-syslog`: yes | no | [yes] |
| `logfile`: filename | [none] |
| `log-ascii`: yes | no | [no] |
| `verbosity`: level | [1] |

日志信息可以进入 `syslog` 或文件。通过 `use-syslog` 和 `logfile` 选项在它们之间进行选择。如果你想在日志消息中使用普通时间而不是 UNIX 时间（自 1970/1/1 以来的秒数），请开启 `log-ascii` 选项。`verbosity` 决定日志量；详情见第 673 页。

### 统计信息

| `statistics-interval`: seconds | [0, i.e., 已禁用] |
| `statistics-cumulative`: yes | no | [no] |
| `extended-statistics`: yes | no | [no] |

统计信息默认关闭，因为它们会减慢服务器。如果你通过将 `statistics-interval` 选项设置为非零秒数来开启它们，统计信息将按照指定的间隔写入日志文件（或 `syslog`）。默认情况下，计数器在每次写入时都会重置为 0；使用 `statistics-cumulative` 选项让它们随时间累积。

关于 Cacti 和 RRDtool 的信息请参阅第 886 页。

发行版的 `contrib` `extended-statistics` 生成更多数据，你可以使用 `unbound-control` 导出它们。

### 查询访问

| `access-control`: netblock action | [仅允许 localhost] |

`access-control` 选项是配置 `unbound` 为自己的用户提供递归服务器而非世界其他部分的关键。使用多个 `access-control` 行来允许多个网络。`access` 参数可以取四个值：

- blocks - 阻塞来自指定网络或主机的所有查询
- refuse - 阻塞查询并返回 REFUSED 消息
- allow - 响应请求递归的客户端查询
- allow-snoop - 响应递归和迭代查询

## 安装和配置 Unbound

`refuse` 动作比 `deny` 更符合 DNS 规范，因为客户端会假设未响应的查询是在网络上丢失的，而不是由于策略原因被管理性地丢弃了。`allow` 动作是普通 DNS 客户端使用的。

`allow-snoop` 响应迭代查询和递归查询。你可以用它调查服务器缓存的内容，因为迭代查询只有在答案已在缓存中才会成功。`allow-snoop` 也可以用于良性目的，因此将此操作限制在你的系统管理员主机上。

`unbound` 的配置文件 `unbound.conf` 与 `nsd` 类似。基本语法如下：

```
attribute: value
```

注释以 `#` 开头并持续到行尾。你可以运行 `unbound-checkconf` 来检查配置文件的有效性。

这里是一个 `unbound.conf` 文件的简单示例，根据帮助页进行了调整，使用了更合理的路径并增加了一些注释：

```
server:
directory: "/var/unbound/etc"
username: unbound
chroot: "/var/run"
pidfile: "/var/run/unbound.pid"
root-hints: "root.cache"
interface: 0.0.0.0
# 监听所有 IPv4 接口
interface: 0
# 以及所有 IPv6 接口
access-control: 10.0.0.0/8
# 本地私有网络
access-control: 2001:db8::/64
# 本地 IPv6 网络
```
