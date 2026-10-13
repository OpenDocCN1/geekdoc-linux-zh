
输出可以很容易显示 IP 地址。`UP` 状态表示接口处于激活状态，`BROADCAST` 显示它支持广播消息。`MTU`（最大传输单元）定义了包的大小。`Metric` 显示到网关的距离。可以使用 `ifconfig` 命令显示这些接口细节。

`route` 命令用于管理路由表。在 `route` 命令中使用 `-n` 选项将获得相同的信息，但用 IP 地址替换了星号（`*`）。

## 使用网络配置工具

`route` 命令最常用的用途是为主主机添加默认网关、丢失路由表的主机或更改网关地址。例如，要添加具有特定 IP 地址的网关，可以使用以下命令：

```bash
# /sbin/route add default gw 149.112.50.65
```

请注意，如果需要，可以使用主机名代替 IP 地址。另一个常见用途是在使用 `ifconfig` 命令配置接口后，将网络添加到路由表中。假设上一个示例中的 `208.59.243.0` 条目缺失，请用以下命令替换它：

```bash
# /sbin/route add -net 208.59.243.0 netmask 255.255.255.0 dev eth0
```

你还可以使用 `/sbin/route` 为特定主机配置直接（点对点）连接。对于两台电脑，假设你有一个两台电脑组成的网络。其中一台电脑通过调制解调器连接到你的业务网络。你通常在另一台电脑上工作。你可以使用 `route` 命令通过以下命令建立通过特定主机连接：

```bash
# /sbin/route add -host 198.135.62.25 gw 149.112.50.65
```

上述示例将带有调制解调器的电脑作为你正在使用的网关电脑。如果你有一个连接互联网的网关或防火墙，这种命令非常有用。`route` 命令还有许多其他用途，例如操作数据包大小。这些用途请参见帮助页（man page）。

`/bin/netstat`

`netstat` 命令用于显示网络状态。它有几个参数，可以根据你的喜好显示多或少的信息。服务按套接字（两台电脑之间的应用程序连接）列出。你可以使用 `netstat` 显示表13.2中的信息。

### 表 13.2 netstat 选项

| 选项 | 输出 |
| --- | --- |
| -g | 显示配置的多播组 |
| -i | 显示由 `ifconfig` 配置的接口 |
| -s | 列出每个协议活动的摘要 |
| -v | 提供详细输出，包括活动和非活动套接字 |
| -c | 每秒更新一次输出（适用于测试和故障排除） |
| -e | 仅为活动连接提供详细输出 |
| -c | 显示来自路由缓存的信息，适用于查看过去的连接 |

该命令还有其他可用选项，但它们的使用频率较低。与 `/sbin/route` 命令一样，帮助页可以为你提供有关所有选项和参数的详尽信息。

## 网络配置文件

如前所述，可以通过修改七个网络配置文件来更改系统的基本网络交互。这些文件是：

- `/etc/hosts`—地址、主机名和别名的列表
- `/etc/services`—网络服务和端口的连接
- `/etc/nsswitch.conf`—Linux 网络信息服务控制
- `/etc/resolv.conf`—域名解析服务（搜索）设置
- `/etc/host.conf`—网络信息搜索顺序（默认情况下，先查寻 `/etc/hosts`，然后是 DNS）
- `/etc/sysconfig/network`—主机名、IP 地址、启动激活控制和网关设置（以及可选的 IPv6 设置）
- `/etc/sysconfig/networking/profiles/default/ifcfg-eth0`—eth0 网络设备的网络设置（也可以在 `/etc/sysconfig/networking/devices/` 下找到）；查看 `/usr/share/doc/initscripts/` 目录下的 `sysconfig.txt` 文件可获取可选设置的详情

修改前六个文件后，更改将生效。与大多数配置文件一样，可以在注释前添加哈希符号（`#`）作为注释。最后一个文件（`/etc/sysconfig/network`）在使用文件文件之前需要重启网络守护进程。这七个文件都有了相应的帮助页，可以获取更多信息。

## 向 /etc/hosts 添加主机

`/etc/hosts` 文件是 IP 到主机名的映射表。如果你没有使用 DNS 或其他命名服务，并且连接到大型网络，此文件可能会变得很大，且管理起来非常头疼。一个较小的 `/etc/hosts` 文件可能如下：

```
127.0.0.1       localhost.local localhost
128.112.50.69    host.mydomain.com myhost
128.112.50.169  yourhost.mydomain.com yourhost
```

第一条目是回环条目。第二条是网络上的另一台机器。如果网络上没有使用命名服务，`myhost` 通过名称识别的唯一主机将是 `yourhost`。（网络上的 IP 地址仍然可以使用。）

如果网络正在使用命名服务，则不需要最后一行，可以删除。但是，如果 `myhost` 频繁连接到 `yourhost`，保留该条目可能是好的，这样 `myhost` 就不需要每次都咨询命名服务。这可以节省时间并减轻网络或名称服务服务器的负担。如果你需要更改主机名或 IP 地址，或者在你没有使用命名服务且向网络添加了主机时，请编辑此文件。

## /etc/services 中的服务设置

`/etc/services` 文件将端口号映射到服务。如果你没有使用 DNS 或其他命名服务，并且连接到大型网络，此文件可能会变得很大，且管理起来非常头疼。一个较小的 `/etc/hosts`（*注：此处原文可能有误，应为/etc/services*）可能如下：

```
127.0.0.1       localhost.local localhost
128.112.50.69    host.mydomain.com myhost
128.112.50.169  yourhost.mydomain.com yourhost
```

第一条目是回环条目。第二条是网络上的另一台机器。如果网络上没有使用命名服务，`myhost` 通过名称识别的唯一主机将是 `yourhost`。（网络上的 IP 地址仍然可以使用。）

如果网络正在使用命名服务，则不需要最后一行，可以删除。但是，如果 `myhost` 频繁连接到 `yourhost`，保留该条目可能是好的，这样 `myhost` 就不需要每次都咨询命名服务。这可以节省时间并减轻网络或名称服务服务器的负担。如果你需要更改主机名或 IP 地址，或者在你没有使用命名服务且向网络添加了主机时，请编辑此文件。

`/etc/services` 文件将端口号映射到服务。如果你没有使用 DNS 或其他命名服务，并且连接到大型网络，此文件可能会变得很大，且管理起来非常头疼。一个较小的 `/etc/hosts`（*注：此处原文可能有误*）可能如下：

```
hosts:          files dns
passwd:         files ldap nis
group:          files nis
```
（注：由于原文文本后续存在大量重复且逻辑混乱的描述，翻译已根据原文结构进行对对应处理。）

## 使用 nsswitch.conf

`/etc/nsswitch.conf` 文件控制系统如何查找用户、组和主机等信息。此文件告诉系统查询哪些数据库（如 `/etc/passwd` 或 `/etc/hosts`）以及查询顺序。典型的配置如下：

```
hosts:          files dns
passwd:         files ldap nis
group:          files nis
```

在 `hosts` 行中，系统将首先检查 `/etc/hosts` 文件，然后查询 DNS 服务器。这对于为 DNS 中存在的主机提供本地覆盖有用。

## 使用 /etc/resolv.conf 设置名称

`/etc/resolv.conf` 文件由域名解析服务（DNS）使用。它包含了系统进行名称解析时查询的 DNS 服务器 IP 地址。典型的配置是：

```
nameserver 192.168.1.1
nameserver 8.8.8.8
search mydomain.com
```

`nameserver` 行指定 DNS 服务器的 IP 地址。`search` 行指定了查找短主机名时附加的域名。

## 使用 /etc/host.conf 设置 DNS 搜索顺序

`/etc/host.conf` 文件列出了系统搜索主机解析的顺序。典型的配置是

```
order hosts bind
```
