
> 提示：随着你添加 `iptables` 规则，将必须加载更多的模块。当输入新规则时，相应的模块应该会被自动加载。在你添加几条规则后，运行 `lsmod | grep ^ip` 查看加载了哪些模块。注意这些模块。

# 第三部分：管理 Fedora RHEL

## 创建 iptables 规则

配置 `iptables` 的一种方法是向内核添加规则。后续节包含了以下 `iptables` 示例，内容如下：

- `iptables` — 使用此命令添加 (`-A`)、删除 (`-D`)、替换 (`-R`) 或插入 (`-I`) 规则。
- `save` — 使用此命令将规则保存到文件。
- `/etc/sysconfig/iptables` — 这是包含规则的文件。
- `/etc/sysconfig/iptables-config` — 你也可以为 `iptables` 设置设置。
- `/etc/init.d/` — 这是每次重启时必须运行的脚本。你也可以使用此脚本的不同选项检查状态或运行 `iptables-save`。

为了开始使用 `iptables`，我提供一组示例规则以及如何修改它们的描述。以下是加载任何集合的方法：

1. 停止 `iptables` 并清除所有规则：

```
# /etc/init.d/iptables stop
```

2. 使用任何文本编辑器添加示例所示的规则。根据你的情况修改规则。

## 第 14 章：计算机安全问题 591

3. 以 `root` 用户身份运行文件。例如，如果你将文件命名为 `firescript`，你可以这样运行：

```
# sh firescript
```

4. 查看规则是如何加载到内核的：

```
# iptables -L
```

5. 如果看起来正常，将现在内核中的规则保存到 `/etc/sysconfig/iptables` 文件中：

```
# cp /etc/sysconfig/iptables /etc/sysconfig/iptables-old
# service iptables save
```

从现在起，每次重启或重启 `iptables` 时都会读取这些规则。保存你用于创建规则的脚本副本，以防以后需要。

### 示例 1：共享互联网连接的防火墙（带服务器）

由于防火墙配置根据你想实现的目标而差异巨大，我说明了如何根据不同的示例设置来配置防火墙。这些设置结合了不同级别的安全需求。

此示例包含如下家庭或小型办公室局域网：一个 Fedora 系统作为局域网和互联网之间的 `iptables` 防火墙。防火墙计算机还作为 Web 服务器、FTP 服务器和 DNS 服务器使用。图 14-2 显示了这种配置。

![](img/e48e37bc567c450fab455ad1b714d8c3_624_0.png)

图 14-2：使用 `iptables` 作为互联网与局域网之间的防火墙

## 第三部分：管理 Fedora 和 RHEL

防火墙计算机 — 防火墙设置如下：

- 本地主机 — `127.0.0.1`（IP 地址）和 `lo`（接口）。你不需要更改这些。
- 连接到互联网 — `123.45.67.89`（IP 地址）和 `eth0`（接口）。将它们分别替换为与互联网连接相关的静态 IP 地址和接口名称。
- 连接到局域网（LAN） — `10.0.0.1`（IP 地址）和 `eth1`（接口）。将 `10.0.0.1` 和 `eth1` 分别替换为与局域网连接相关的静态 IP 地址和接口名称。
- 局域网上的计算机 — `10.0.0.2` — 示例局域网上的每台计算机 IP 地址范围从 `10.0.0.2` 到 `10.0.0.254`。将 `10.0.0.255` 修改为匹配你局域网范围的数字。

这是一个加载防火墙规则的脚本示例，可用于图 14-2 所示的配置：

```
# (1) 策略（默认）
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP
```

```
# (2) 用于接受 TCP 数据包的用户自定义链
iptables -N okay -p TCP --syn -j ACCEPT
iptables -A okay -p TCP -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A okay -p TCP -j DROP
```

```
# (3) INPUT 链规则
# 来自局域网的入站包规则
iptables -A INPUT -p ALL -i eth1 -s 10.0.0.0/24 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 127.0.0.1 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 10.0.0.1 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 123.45.67.89 -j ACCEPT
iptables -A INPUT -p ALL -i eth1 -d 10.0.0.255 -j ACCEPT
```

```
# 来自互联网的入站包规则

# 建立连接的数据包
iptables -A INPUT -p ALL -d 123.45.67.89 -m state --state ESTABLISHED,RELATED -j ACCEPT
```

```
# TCP 规则
iptables -A INPUT -p TCP -i eth0 --destination-port 21 -j okay
iptables -A INPUT -p TCP -i eth0 --destination-port 22 -j okay
iptables -A INPUT -p TCP -i eth0 --destination-port 80 -j okay
```

![](img/e48e37bc567c450fab455ad1b714d8c3_625_0.png)

## 第 14 章：计算机安全问题 593

```
iptables -A INPUT -p TCP -i eth0 --destination-port 113 -j okay
```

```
# UDP 规则
iptables -A INPUT -p UDP -i eth0 --destination-port 53 -j ACCEPT
iptables -A INPUT -p UDP -i eth0 --destination-port 2074 -j ACCEPT
iptables -A INPUT -p UDP -i eth0 --destination-port 4000 -j ACCEPT
```

```
# ICMP 规则
iptables -A INPUT -p ICMP -i eth0 --icmp-type 8 -j ACCEPT
iptables -A INPUT -p ICMP -i eth0 --icmp-type 11 -j ACCEPT
```

```
# (4) FORWARD 链规则
# 接受我们想要转发的数据包
iptables -A FORWARD -i eth0 -j ACCEPT
iptables -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT
```

```
# (5) OUTPUT 链规则
# 只输出具有本地地址的数据包（防止欺骗）
iptables -A OUTPUT -p ALL -s 127.0.0.1 -j ACCEPT
iptables -A OUTPUT -p ALL -s 10.0.0.1 -j ACCEPT
iptables -A OUTPUT -p ALL -s 123.45.67.89 -j ACCEPT
```

```
# (6) POSTROUTING 链规则
iptables -t nat -A POSTROUTING -o eth0 SNAT --to-source 123.45.67.89
```

我将上述脚本中的命令分成了六部分。接下来的文本描述了这些每个部分。

- `iptables` 命令为 `INPUT`、`OUTPUT` 和 `FORWARD` 链设置了默认策略。通过将这些策略中的每一个设置为 `DROP`，任何未匹配的数据包都会被丢弃。换句话说，数据包若要通过，必须被脚本中其他链之一特定匹配并接受（`ACCEPT`）。
- 我创建了一个名为 `okay` 的用户自定义链，用于对我将允许的请求 TCP 服务（Web、FTP 和 DNS 服务）的数据包进行更多检查。`-N` 选项创建了该链。下一行表示 SYN 数据包（`--syn`），即请求新连接的，允许通过。下一行允许与 `ESTABLISHED` 连接（已经有流量通过接口）或 `RELATED` 连接（正在启动新连接）关联的数据包。该组规则的最后一行告诉 `iptables` 丢弃（`DROP`）不符合条件的数据包。
