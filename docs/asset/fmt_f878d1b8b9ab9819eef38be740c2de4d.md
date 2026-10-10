
5. 一旦规则文件到位，启动 `iptables`：

```
# /etc/init.d/iptables
```

6. 此时，`iptables` 已安装为您的防火墙。您可以使用 `lsmod` 命令检查 `iptables` 使用的模块是否已加载，如下：

```
lsmod |grep ip
ipt REJECT 4736 1
ipt state 1536 7
ip_count 24368 1
iptable_filter 2176 1
iptables 13568 3 ipt REJECT,ipt_state,iptables_filter
```

7. 如果您想允许来自局域网计算机的 FTP 或 IRC 连接，您可能需要通过将它们添加到 `/etc/modprobe.conf` 文件来加载这些模块。基础连接跟踪模块 `ip_count` 默认情况下应该是加载的。（参见防火墙示例章节之后关于被动 FTP 和 IRC 的描述。）

- 您在启动服务时拥有 `root` 权限。

- `/etc/sysconfig/iptables` 文件存在。（如果在安装 Fedora 时没有为您创建，您需要手动创建一个。）

如果您的 `/etc/sysconfig/iptables` 文件中有错误，可以制作该文件的副本，然后通过运行 `system-config-securitylevel` 并设置基本防火墙来尝试创建一个有效的配置。然后您可以对防火墙进行更改以添加您需要的功能。

> 提示：随着您添加 `iptables` 规则，将更多的模块需要加载。当输入新规则时，相应的模块应该会自动加载。在添加几条规则后运行 `lsmod | grep ip` 查看添加了哪些模块。注意，如果您决定停止 `iptables`，这些模块将不会被卸载。

## 创建 iptables 规则

以下步骤描述了如何在 Fedora 或 RHEL 系统上运行 `iptables`。（等等，OCR 文本在这里重复了某些逻辑，我将遵循逻辑流）。

为了开始使用 `iptables`，我提供了一组示例规则以及关于您如何修改它们的描述。以下是您可以使用此示例的方法：

1. 停止 `iptables` 并清除所有现有规则：

```
# /etc/init.d/iptables stop
```

2. 使用任何文本编辑器将示例所示的规则添加到文件中。根据您的情况修改规则并保存文件。

3. 以 `root` 用户身份作为脚本运行文件。例如，如果您将文件命名为 `firescript`，可以这样运行：

```
# sb firescript
```

4. 查看规则是如何加载到内核的：

```
# iptables -L
```

5. 如果一切看起来正常，将现在内核中的规则保存到 `/etc/sysconfig/iptables`：

```
# cp /etc/sysconfig/iptables /etc/sysconfig/iptables-old
# service iptables save
```

从现在起，每次重启系统或重启 `iptables` 时都会读取这些规则。保存一份用于创建规则的脚本副本，以防以后再次需要。

### 示例 1：共享互联网连接的防火墙（外服务器）

防火墙配置可能差异巨大，取决于您想要实现，我根据几种不同的示例设置说明了如何配置防火墙。

此示例包含一个家庭或小型办公室局域网，在局域网和互联网之间有一个 `iptables` 防火墙。防火墙计算机还充当 Web 服务器、FTP 服务器和 DNS 服务器。图 14-2 显示了此配置。

![](img/c7605e408543e0a1829c1fd0cf2f687d_623_0.png)

图 14-2：使用 `iptables` 作为互联网和局域网之间的防火墙

# 第14章：计算机安全问题 589

如果你想使用接下来的示例防火墙脚本，你必须更改以下信息以匹配你的配置：

防火墙计算机 — 防火墙计算机设置如下：

- 本地主机（Local host） — `127.0.0.1`（IP 地址）和 `lo`（接口）。你通常不需要更改这些。

- 连接互联网 — `123.45.67.89`（IP 地址）和 `eth0`（接口）。请将它们分别替换为与互联网连接相关的静态 IP 地址和名称。

- 连接局域网（LAN） — `10.0.0.1`（IP 地址）和 `eth1`（接口）。请将 `10.0.0.1` 和 `eth1` 分别替换为与局域网连接相关的静态 IP 地址和名称。

- 局域网计算机 — 示例中局域网上的每台计算机的 IP 地址从 `10.0.0.2` 到 `10.0.0.254`。将 `10.0.0.255` 修改为与你的局域网地址范围匹配的数字。

这里是一个用于加载防火墙规则的脚本示例，可用于图 14-2 所示的配置：

```
# (1) 策略（默认）
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP

# (2) 用于接受的 TCP 数据包的用户定义链
iptables -N okay
iptables -A okay -p TCP --syn -j ACCEPT
iptables -A okay -p TCP -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A okay -p TCP -j DROP

# (3) INPUT 链规则

# 来自局域网的入站包规则
iptables -A INPUT -p ALL -i eth1 -s 10.0.0.0/24 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 127.0.0.1 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 10.0.0.1 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 123.45.67.89 -j ACCEPT
iptables -A INPUT -p ALL -i eth1 -d 10.0.0.255 -j ACCEPT

# 来自互联网的入站包规则

# 针对已连接的数据包
iptables -A INPUT -p ALL -d 123.45.67.89 -m state --state ESTABLISHED,RELATED -j ACCEPT

# TCP 规则
iptables -A INPUT -p TCP -eth0 --destination-port 21 -j okay
iptables -A INPUT -p TCP -eth0 --destination-port 22 -j okay
iptables -A INPUT -p TCP -eth0 --destination-port 80 -j okay
iptables -A INPUT -p TCP -eth0 --destination-port 113 -j okay

# UDP 规则
iptables -A INPUT -p UDP -eth0 --destination-port 53 -j ACCEPT
iptables -A INPUT -p UDP -eth0 --destination-port 2074 -j ACCEPT
iptables -A INPUT -p UDP -eth0 --destination-port 4000 -j ACCEPT

# ICMP 规则
iptables -A INPUT -p ICMP -eth0 --icmp-type 8 -j ACCEPT
iptables -A INPUT -p ICMP -eth0 --icmp-type 11 -j ACCEPT

# (4) FORWARD 链规则
# 接受我们想要转发的数据包
iptables -A FORWARD -i eth1 -j ACCEPT
iptables -A FORWARD -m state --ESTABLISHED,RELATED -j ACCEPT

# (5) OUTPUT 链规则
# 仅输出本地地址的数据包（防止欺骗）
iptables -A OUTPUT -p ALL -s 127.0.0.1 -j ACCEPT
iptables -A OUTPUT -p ALL -s 10.0.0.1 -j ACCEPT
iptables -A OUTPUT -p ALL -s 123.45.67.89 -j ACCEPT

# (6) POSTROUTING 链规则
-t nat -A POSTROUTING -o eth0 -j SNAT --to-source 123.45.67.89
```

我将上述脚本中的命令分为六个部分。以下文本描述了每个部分。

- (1) 策略 — `iptables -P` 命令设置了 `INPUT`、`OUTPUT` 和 `FORWARD` 链的默认策略。通过将这些策略都分配为 `DROP`，任何未匹配的数据包都会被丢弃。换句话说，为了让数据包通过，它必须被其他规则中的某一个匹配并接受（`ACCEPT`）。
