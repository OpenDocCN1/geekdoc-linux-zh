
内部防火墙保护内部网络免受外部访问。它将非本地流量转发到 DMZ 并限制入站流量。该防火墙配置为执行以下操作：

- 执行默认的拒绝所有包（`den-all-packets`）策略。
- 对指向 DMZ 服务或外部世界的内部流量进行伪装（Masquerade）。
- 仅允许响应内部请求而产生的入站流量。进入此防火墙的入站包不能设置 SYN 位。
- 限制内部网络对外部服务的访问。

## 主防火墙的作用

外部（主）防火墙保护整个企业网络，但其任务是执行以下操作：

- 执行默认的“拒绝所有包”策略。
- 允许从外部世界访问 DMZ 服务器。
- 对内部防火墙（代表内部节点）生成的指向外部世界的包进行伪装，使这些包看起来像是来自主防火墙的外部接口。

当防火墙正常工作时，一个典型的场景如下：

- 1. 内部局域网（LAN）工作站上的用户通过其 Web 浏览器对外部域名发起 HTTP 请求。
- 2. 内部防火墙将其请求伪装为来自其自己的外部接口（DMZ 站点）。
- 3. 主防火墙看到此出站包，对其进行伪装，并转发到外部世界。
- 4. 外部的 Web 服务器只知道主防火墙的外部 IP 地址请求访问外部域名。因此，Web 服务器向 DMZ 站点发送包，这确保了系统不知道用户是谁——并且（更重要的是）无法获取未经授权用户的账户信息。

注意，你可以决定不在内部防火墙上对出站包进行伪装——外部防火墙无论如何都会伪装——但如果你在内部防火墙上对出站包进行伪装，你就可以在外部（主）防火墙上使用更简单的包过滤规则。当实施一致时，这种安排可以在不损害安全的情况下增强性能。由于主防火墙将内部网络的所有包都视为来自一个地址——即内部的外部接口——因此，在主防火墙上创建访问规则时，你只需要处理这一个地址。

![](img/177ab5b774eeb101e12de61f8616d71a_538_0.png)

在这个示例中，我使用了一个 DMZ 网络 `192.168.1.0/24`（实际上是一个私有网络——但在现实世界中，你无法从互联网访问不可路由的私有网络）。在现实世界的 DMZ 中，你必须使用一个互联网可路由的非私有网络。要求你的 ISP 为你的公司分配一个子网——并将所有发往该子网的包路由到你防火墙的外部接口地址。为 DMZ 中的每台服务器分配一个真实的 IP 地址，以便它们可以通过你的防火墙从外部访问。同时注意，主防火墙的外部网络地址也是由你的 ISP 分配的；示例使用了在互联网上可路由的随机数。

为给定场景实现这些防火墙是一个独立的过程。注意，当你遵循接下来两个小节中的说明时，必须更改 IP 地址以匹配你自己的网络环境。

## 设置内部防火墙

要设置内部防火墙，请遵循以下步骤：

- 1. 创建一个 `sh` 脚本（命名为 `internal-firewall.sh`），如下定义内部网络的设置：

```
#!/bin/sh
IPTABLES=/sbin/iptables
INTERNAL_LAN="192.168.2.0/24"
```

```
INTERNAL_LAN_INTERFACE="eth1"
INTERNAL_LAN_INTERFACE_ADDR="192.168.2.254"
EXTERNAL_INTERFACE="eth0"
EXTERNAL_INTERFACE_ADDR="192.168.1.1"
```

- 2. 通过向脚本末添加以下行来清除过滤表（filter table）中的所有规则：

```
# 清除过滤表中的所有规则
$IPTABLES -F FORWARD
$IPTABLES -F INPUT
$IPTABLES -F OUTPUT
```

- 3. 通过向脚本添加以下行来实现默认策略：

```
# 创建默认丢弃和拒绝一切的策略
$IPTABLES -P FORWARD
$IPTABLES -P OUTPUT ACCEPT
$IPTABLES -P INPUT DROP
```

- 4. 通过添加以下行启用本地回环接口（loopback）：

```
# 启用回环
$IPTABLES -A input lo -p all -j ACCEPT
```

- 5. 启用 ping 等服务使用的互联网控制消息协议（ICMP）包：

```
$IPTABLES -A INPUT -p icmp -j ACCEPT
```

- 6. 添加这些行允许内部局域网访问防火墙接口：

```
$IPTABLES -A input -i $INTERNAL_LAN_INTERFACE
-s $INTERNAL_LAN
```

- 7. 允许内部局域网访问接口的转发包：

```
$IPTABLES -A output -i $INTERNAL_LAN_INTERFACE
$INTERNAL_LAN
```

- 8. 为发往外部世界的包设置伪装：

```
$IPTABLES -t nat -A POSTROUTING -o $EXTERNAL_INTERFACE
-s $INTERNAL_LAN
```

- 9. 添加这些行允许来自内部局域网的包：

```
$IPTABLES -A FORWARD -s $INTERNAL_LAN -j ACCEPT
```

此时，你已经有一个可以对外部服务器流量进行伪装的防火墙。现在你需要决定内部可以访问哪些服务——例如 HTTP、SMTP、POP3——并为它们创建特定的防火墙。

## 设置主防火墙

要设置外部（主）防火墙，创建一个名为 `firewall-primary.sh` 的 `sh` 脚本，如 Listing 2 所示：

### Listing 2: firewall-primary.sh

```
#!/bin/sh
IPTABLES=/sbin/iptables
DMZ_LAN="192.168.1.0/24"
DMZ_INTERFACE="eth1"
DMZ_INTERFACE_ADDR="192.168.1.254"
WORLD_INTERFACE="eth0"
WORLD_INTERFACE_ADDR="207.65.6"
INTERNAL_LAN="192.168.2.0/24"
INTERNAL_LAN_INTERFACE="eth1"
INTERNAL_LAN_INTERFACE_ADDR="192.168.2.254"
EXTERNAL_INTERFACE="eth0"
EXTERNAL_INTERFACE_ADDR="192.168.1.1"

# 清除过滤表中的所有规则
$IPTABLES -F FORWARD
$IPTABLES -F INPUT
$IPTABLES -F OUTPUT

# 创建默认丢弃和拒绝一切的策略
$IPTABLES -P FORWARD
$IPTABLES -P OUTPUT ACCEPT
$IPTABLES -P INPUT DROP

# 启用回环
$IPTABLES -A input lo -p all -j ACCEPT

# 启用互联网控制消息协议（ICMP）
# 用于 ping 等服务
$IPTABLES -A INPUT -p icmp -j ACCEPT

# 允许 DMZ LAN 访问防火墙接口
$IPTABLES -A input -i $DMZ_INTERFACE
-s $DMZ_LAN

# 允许来自接口的转发包
$IPTABLES -A output -i $DMZ_INTERFACE
-d $DMZ_LAN

# 为发往外部世界的包设置伪装
$IPTABLES -t nat -A POSTROUTING -o $EXTERNAL_INTERFACE
-s $INTERNAL_LAN

# 允许来自内部局域网的包
$IPTABLES -A FORWARD -s $INTERNAL_LAN -j ACCEPT
```

下一步是为 DMZ 中提供的服务添加规则。

## 访问 DMZ 中的 FTP 服务器

你想允许外部世界访问 FTP，但你也想监管它以防止 FTP 成为安全风险。以下代码为此类策略奠定了基础：

```
# 允许来自外部世界的 FTP 连接
$IPTABLES -A input -i $WORLD_INTERFACE
-p tcp
-s 0/0 1024-65535
-d $DMZ_FTP_SERVER_ADDR 21
-j ACCEPT

# 允许指向外部世界的 FTP 连接
$IPTABLES -A output -i $WORLD_INTERFACE
-p tcp ! -y
-s $DMZ_FTP_SERVER_ADDR 21
-d 0/0 1024-65535
-j ACCEPT

# 允许来自外部世界的 FTP 数据通道连接
$IPTABLES -A input -i $WORLD_INTERFACE
-p tcp
-s 0/0 1024-65535
-d $DMZ_FTP_SERVER_ADDR 1024-65535
-j ACCEPT

# 允许来自外部世界的 FTP 数据通道
$IPTABLES -A output -i $WORLD_INTERFACE
-p tcp ! -y
-s $DMZ_FTP_SERVER_ADDR 1024-65535
-d 0/0 1024-65535
-j ACCEPT
```

## 在 DMZ 中访问 Apache 服务器
