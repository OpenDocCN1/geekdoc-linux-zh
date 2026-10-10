
64 bytes from 192.168.1.3: icmp_seq=2 ttl=64 time=0.076 ms

64 bytes from 192.168.1.3: icmp_seq=3 ttl=64 time=0.108 ms

64 bytes from 192.168.1.3: icmp_seq=4 ttl=64 time=0.076 ms

--- 192.168.1.3 ping statistics ---

5 packets transmitted, 5 packets received, 0% packet loss

round-trip min/avg/max/stddev = 0.074/0.083/0.108/0.013 ms

现在我们必须 ping 局域网上的另一台机器：

```
% ping -c 5 192.168.1.2

PING 192.168.1.2 (192.168.1.2): 56 bytes

64 bytes from 192.168.1.2: icmp_seq=0 ttl=64 time=0.726 ms

64 bytes from 192.168.1.2: icmp_seq=1 ttl=64 time=0.766 ms

64 bytes from 192.168.1.2: icmp_seq=2 ttl=64 time=0.700 ms

64 bytes from 192.168.1.2: icmp_seq=3 ttl=64 time=0.747 ms

64 bytes from 192.168.1.2: icmp_seq=4 ttl=64 time=0.704 ms

--- 192.168.1.2 ping statistics ---

5 packets transmitted, 5 packets received, 0% packet loss

round-trip min/avg/max/stddev = 0.700/0.729/0.769/0.026 ms
```

如果你已经设置了 `/etc/hosts` 文件，你也可以使用 `192.168.1.2` 的机器名。

## 11.8.32 故障排除

排除硬件和软件配置的故障总是一件痛苦的事，但通过检查简单的事情可以减轻痛苦。你的网络插好了吗？你是否正确配置了网络服务？你是否正确配置了防火墙？你使用的网卡 FreeBSD 支持吗？在提交错误报告之前，始终检查硬件说明。将你的 FreeBSD 更新到最新的 STABLE 版本。检查邮件列表存档或搜索互联网。

如果网卡正常但性能不佳，阅读 `tuning(7)` 手页是值得的。你也可以检查网络配置，错误的网络设置可能会导致连接缓慢。

某些用户会遇到一两个超时消息，这对于某些网卡是正常的。如果这些消息持续出现或令人困扰，你可能希望确保设备没有与另一个设备冲突。双检电缆连接。你可能需要另一块网卡。

有时你可能会看到看门狗超时（watchdog timeout）。首先要检查的是你的网络电缆。许多网卡需要支持总线主（Bus Mastering）的 PCI 插槽。在某些主板上，只有一个 PCI 插槽允许（通常是槽 0）。检查网卡和主板文档以确定这是否可能是问题所在。

如果系统无法路由到目标主机，就会出现“No route to host”消息。这可能发生在你尝试访问的主机没有设置默认路由，或者电缆被拔掉时。检查 `netstat -rn` 的输出并确保有有效路由。如果没有，请继续阅读第 27 章。

`ping: Permission denied` 错误消息通常由防火墙配置不当引起。如果内核启用了 `ipfw` 但没有定义规则，默认策略是拒绝所有流量，甚至是 ping 请求！更多信息请继续阅读第 26 章。

有时网卡的性能很差或低于平均水平。在这种情况下，最好将选择方法从 `autoselect` 设置为正确的网络选择。虽然这在大多数硬件上都能解决问题，但请再次检查网络设置并阅读 `tuning(7)` 手页。

## 11.9 虚拟主机

FreeBSD 的一个常见用法是虚拟主机，即一个服务器在网络中表现为多个服务器。这是通过向单个接口分配多个网络地址实现的。网络接口有一个“真实”（real）地址，并可能有任意数量的“别名”（alias）地址。这些别名通过在 `/etc/rc.conf` 中放置条目添加。接口 `fxp0` 的条目如下：

```
if fxp0_alias0=inet xxx.xxx.xxx mask xxx.xxx.xxx
```

注意，`alias` 的工作方式是按顺序处理的（例如 `alias1, alias2` 等）。配置过程会在遇到缺失的名称时停止。

别名掩码的计算很重要，但非常简单。对于给定的接口，必须有一个代表该网络的地址。该网络内的其他地址必须具有全1 的掩码（表示为 `255.255.255` 或 `0ffff`）。例如，考虑以下情况：`fxp0` 接口连接到两个网络，一个是掩码为 `255.255.255.0` 的 `10.1.1.0` 网络，另一个掩码为 `255.255.255.240` 的 `202.0.75.16` 网络。我们希望系统出现在 `10.1.1.1` 到 `10.1.1.5` 以及 `202.0.75.17` 到 `202.0.75.20` 之间。如上述，给定网络中的第一个地址（在此例下为 `10.1.1.1` 和 `202.0.75.17`）应该是真实的；其余所有（`10.1.1.2` 到 `10.1.1.5` 以及 `202.0.75.18` 到 `202.0.75.20`）必须配置为 `255.255.255.255` 掩码。

以下 `/etc/rc.conf` 条目正确配置了该适配器：

```
if fxp0_alias0="inet 10.1.1.1 mask 255.255.255.0"
if fxp0_alias1="inet 10.1.1.2 mask 255.255.255.255"
if fxp0_alias2="inet 10.1.1.3 mask 255.255.255.255"
if fxp0_alias3="inet 10.1.1.4 mask 255.255.255.255"
if fxp0_alias4="inet 10.1.1.5 mask 255.255.255.255"
if fxp0_alias5="inet 202.0.75.17 mask 255.255.255.240"
if fxp0_alias6="inet 202.0.75.18 mask 255.255.255.255"
if fxp0_alias7="inet 202.0.75.19 mask 255.255.255.255"
if fxp0_alias8="inet 202.0.75.20 mask 255.255.255.255"
```

## 11.10 配置文件

有许多存放配置的目录，包括：

- `/etc`
- `/etc/defaults`
- `/etc/mail`
- `/etc/ppp`
- `/etc/namedb`
- `/usr/local/etc`
- `/usr/local/etc/rc.d`
- `/var/db`

- 通用系统信息；此处数据是特定系统的。
- 系统文件的默认版本。
- 额外的 `mail(8)` 配置和 MTA 配置。
- 用户和内核程序的配置。
- `named(8)` 的默认位置。通常 `named.conf` 和区域文件存储在这里。
- 已安装应用程序的配置。可能包含每个应用程序的目录。
- 已安装应用程序的启动/停止脚本。
- 自动生成的系统特定文件，如包数据库、locate 数据库等。

### 11.10.2 主机名

#### 11.10.2.1 /etc/resolv.conf

`/etc/resolv.conf` 规定了 FreeBSD 解析器访问互联网命名系统（DNS）。`resolv.conf` 最常见的条目有：

- `nameserver`
- `search`
- `domain`

- 应查询的服务器 IP 地址。按照列出的顺序查询服务器，最多三个。
- 搜索列表。这通常由本地主机名的域名决定。
- 本地主机名。

典型的 `resolv.conf`：

```
search example.com

nameserver 147.11.1.11

nameserver 147.11.100.30
```

注意：应使用 `search` 和 `domain` 选项中的一个。

如果你使用 DHCP，`dhclient(8)` 会根据 DHCP 服务器重写 `resolv.conf`。

#### 11.10.2.2 /etc/hosts

`/etc/hosts` 是一个类似于旧网络的简单文本数据库。它与 DNS 和 NIS 协同工作，提供名称到 IP 地址的映射。通过局域网连接的计算机可以放在这里进行简单命名，而不是设置 `named(8)` 服务器。此外，`/etc/hosts` 可用于为常用访问名称提供本地记录，减少外部查询需求。

```
# FreeBSD

# 主机数据库

# 此文件应包含本地主机的地址和别名。
