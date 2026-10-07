

# 第 13 章 网络连接

| 208.559.243.0 | 0.0.0.0 | 255.255.255.0 | U | 0 | 0 | eth0 |
| 127.0.0.0 | 0.0.0.0 | 255.0.0.0 | U | 0 | 0 | lo |
| 0.0.0.0 | 149.112.50.65 | 0.0.0.0 | UG | 0 | 0 | eth0 |

`route` 命令可以使用 `add` 选项向表中添加条目。使用 `add` 选项时，你可以指定主机 (-host) 或网络 (-net) 作为目标。如果不使用任何选项，`route` 命令将假设你正在配置发布该命令的接口。`route` 命令最用途是为主机添加默认网关、为具有路由表的主机配置或在网关地址更改时使用。例如，要添加具有特定 IP 地址的网关，可以使用以下命令：

```
# /sbin/route add default gw 149.112.50.65
```

注意，如果需要，你可以使用主机名代替 IP 地址。另一个常见用途是在执行 `ifconfig` 命令配置接口后，立即将网络添加到路由表中。假设上一个示例中的 `208.59.243.0` 条目缺失了，请使用以下命令进行替换：

```
# /sbin/route add -net 208.59.243.0 netmask 255.255.255.0 dev eth0
```

你还可以使用 `/sbin/route` 为直连（点对点）连接配置特定主机。例如，假设你有一个由台电脑组成的网络。其中一台电脑通过调制解调器连接到你的业务网络，而你通常在另一台电脑上工作。你可以使用 `route` 命令通过特定主机建立连接：

```
# /sbin/route add -host 198.135.62 gw 149.112.50.65
```

上述示例使得带有调制解调器的电脑成为你正在使用的电脑的网关。如果你连接到互联网或防火墙，这种命令非常有用。`route` 命令还有许多额外用途，例如操作数据包大小。参见 man 页。

### /bin/netstat
`netstat` 命令用于显示网络状态。它有多个参数，可以根据喜好显示多或少的信息。服务按套接字列出（计算机之间的应用程序连接）。你可以使用 `netstat` 显示表 13.2 中的信息。

### 表 13.2 netstat 选项

| 选项 | 输出 |
| --- | --- |
| -g | 显示已配置的多播组 |
| -i | 显示由 ifconfig 配置的接口 |
| -s | 列出每个协议的活动摘要 |

### 表 13.2 netstat 输出（续）

| 选项 | 输出 |
| --- | --- |
| -v | 提供详细输出，列出活动和非活动套接字 |
| -c | 每秒更新输出（适用于故障排除） |
| -e | 仅提供活动连接的详细输出 |
| -C | 显示来自缓存的信息（适用于查看历史连接） |

该命令还有其他可用选项，但它们不那么常用。与 `/sbin/route` 命令一样，man 页可以提供所有选项和参数的细节。

## Red Hat 网络配置文件

如前所述，有七个网络配置文件可以修改以更改基本网络交互。这些文件是：

- /etc/hosts—地址、主机名和别名的列表
- /etc/services—网络服务和端口连接
- /etc/nwitch.conf—网络信息服务配置
- /etc/resolv.conf—域名服务（搜索）设置
- /etc/host.conf—网络信息搜索顺序（默认情况下是 /etc/hosts 然后是 DNS）
- /etc/HOSTNAME—主机；传统上支持但 Red Hat Linux 未使用
- /etc/sysconfig/network—主机名、IP 地址、启动控制和网关设置

当前六个文件被修改时，更改会生效。在配置文件中可以使用井号（#）添加注释。在使用最后一个文件（/etc/sysconfig/network）后需要重启网络守护进程。所有七个文件都有关于它们的 man 页。

### 将主机添加到 /etc/hosts

`/etc/hosts` 文件是 IP 到主机名的映射。如果你没有使用 DNS 或其他命名服务并且连接到大型网络，这个文件可能会变得很大，管理起来头疼。一个小的 `/etc/hosts` 文件如下：

```
127.0.0.1       localhost  localdomain
128.112.50.6    mydomain.com    yourhost
```

等等，让我们重新检查文本：“第一个条目用于环回。第二个用于机器名称。第三个是网络上的另一台机器。如果网络上使用了命名服务，唯一的识别主机将是你网络上的 IP 地址。如果你正在使用命名服务，最后一行不需要，可以删除。然而，如果 /etc/hosts 频繁连接，保留该条目可能是好的，这样主机就不需要每次咨询命名服务。这可以节省时间并减轻网络或命名服务的负担。”

### /etc/services 中的服务设置

`/etc/services` 文件将数字映射到服务。前几行所示（/etc/services 文件可能很长，超过500 行）：

```
# 每行描述一个服务，格式为：
# 服务名 端口/协议 [别名] [注释]

rpc      1/tcp          # TCP 端口复用器
rpc      1/udp          # UDP 端口复用器
rlogin   5/tcp           # 远程登录
rlogin   5/udp           # 远程登录
echo        7/tcp
echo        7/udp
discard  9/tcp          null
discard  9/udp          null
sysstat  11/tcp         users
```

通常，每个服务有两个条目，因为大多数服务可以使用 TCP 或 UDP 进行传输。通常 /etc/services 在初始化时已配置好，你不需要更改它。

### 命名服务后使用 /etc/nwitch.conf

此文件最初由 Sun Microsystems 开发，用于指定系统上访问服务的顺序。/etc/nwitch.conf 文件中列出了许多服务，但最常修改的条目是 hosts 条目。文件的部分如下：

```
passwd:  files
shadow: files
group:  files
hosts:  db nisplus dns
hosts:   files
```

### 使用 Red Hat Linux 网络配置工具

这告诉服务它们应该咨询标准的 UNIX/Linux 文件进行 passwd、shadow 和 group（分别查找 /etc/passwd、/etc/shadow、/etc/group）。对于主机查找，系统将检查 /etc/hosts，如果没有条目，它将检查 DNS。注释的 hosts 条目列出了主机的可能值。只有当你的命名服务发生变化时才编辑此文件。

### 使用 /etc/resolv.conf 设置域名服务器

/etc/resolv.conf 用于 DNS，即域名服务。（DNS 在第 14 章详细介绍。）以下是 resolv.conf 的示例：

```
nameserver 192.172.2.3
nameserver 192.172.3.9
search mydomain.com
```

这设置了 DNS 使用的名称服务器和域名顺序。如果你使用动态主机配置协议（参见后文 DHCP 部分），此文件的内容将自动设置。

### 使用 /etc/host.conf 设置 DNS 搜索顺序

/etc/host.conf 文件列出了机器查找主机名的顺序。以下是默认的 /etc/host.conf 文件：

```
order hosts, bind
```

在此示例中，文件首先检查 hosts 文件，然后执行 DNS 查询。更多选项控制命名服务的使用。nosport 选项对于系统安全可能是一个很好的选项。它将比较标准 DNS 查询和反向查询（主机到 IP 再从 IP 到主机），如果它们不匹配则失败。缺点是当使用代理服务时，查询将失败，因此你希望谨慎使用它。

### 主机名更改后使用 /etc/HOSTNAME

此文件包含一个单词，即主机名。它最初从 /etc/sysconfig/network 文件创建。如果你的主机名更改，Red Hat Linux 不再使用 /etc/HOSTNAME 文件；但为了避免混淆，更改时最好包含此文件。

### 检查 /etc/sysconfig/network 中的主机网络设置

/etc/sysconfig/network 的更改在重启网络守护进程或重启之前不会生效。如果你使用 Red Hat 的图形化网络配置工具（在下一节描述），你不应该编辑此文件。该文件如下：

