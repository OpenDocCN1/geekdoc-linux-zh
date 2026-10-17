
# Unknown clients get this pool.

```
pool {

    option domain-name-servers 10.0.0.254;

    max-lease-time 300;

    range 10.0.0.100 10.0.0.250;

    allow unknown-clients;

}
```

# Known clients get this pool.

```
pool {

    option domain-name-servers 10.0.0.251, 10.0.0.252;

    max-lease-time 28800;

    range 10.0.0.5 10.0.0.99;

    deny unknown-clients;

}
```

}

也可以为已知客户端和未知客户端设置完全不同的子网。“已知客户端”是指使用 `host` 语句将 IP 地址分配给 MAC 地址。池存在于共享网络的级别，因此 `pool` 声明中的地址范围可以位于不同的子网。

正如您在前面的示例中看到的，池可以具有许可列表来控制哪些客户端允许访问该池以及哪些不允许。

池的许可列表中的每个条目都以 `allow` 或 `deny` 关键字引入。如果池具有许可列表，则只有与许可列表上的特定条目匹配的客户端才有资格从该池分配地址。

如果池具有拒绝列表，则只有与拒绝列表上的任何条目都不匹配的客户端才有资格。如果池同时存在许可列表和拒绝列表，则只有与许可列表匹配且与拒绝列表不匹配的客户端才会被允许访问。

## 目标 2 配置 DHCP 故障转移

本目标涵盖以下主题：

- DHCP 故障转移基础
- 配置故障转移

### DHCP 故障转移基础

故障转移协议允许两个 DHCP 服务器（不超过两个）共享一个公共地址池。每个服务器在任何给定时间都将拥有池中大约一半的可用 IP 地址用于分配。

如果一台服务器失败，另一台服务器将继续从池中续订租约，并从通信丢失前拥有的可用地址的一半中分配新地址。

当一台从未与故障转移对等方通信过的服务器启动时，它必须建立通信并与对等方同步，然后才能为客户端提供服务。这可能发生在您刚刚配置 DHCP 服务器首次执行故障转移时，也可能发生在其中一台故障转移服务器失败并丢失其数据库时。

初始恢复过程旨在确保当一个故障转移对等方丢失其数据库然后重新同步时，失败服务器在失败前分配的任何租约都将被 honoured。当失败服务器启动时，它注意到自己没有保存的故障转移状态并尝试联系其对等方。

建立联系后，它会向对等方请求其租约数据库的完整副本。对等方随后发送其完整数据库并发送一条消息表示已完成。失败的服务器然后等待 `MCLT`（最大客户端提前时间）过去。一旦 `MCLT` 过去，两台服务器都将转换回正常操作。

此等待期可确保失败服务器在与合作伙伴失去联系期间可能分配的任何租约都已过期。

在失败服务器恢复期间，其合作伙伴保持在 `partner-down` 状态，这意味着它正在为所有客户端提供服务。失败服务器在转换到正常操作之前根本不会为 DHCP 客户端提供任何服务。

在两种服务器都检测到它们从未与合作伙伴通信过的这种情况下，它们都会进入此恢复状态并遵循我们刚刚描述的程序。在这种情况下，在 `MCLT` 过期之前不会为 DHCP 客户端提供任何服务。

### 配置故障转移

在故障转移配置中，您必须决定哪台服务器充当主服务器，哪台充当从服务器。两台服务器都需要为它们共享的基本 DHCP 服务具有相同的配置。它们仅在故障转移设置上有所不同。因此，建议在两台机器上都有一个公共配置文件，该文件包含在文件 `/etc/dhcpd.conf` 中。

主服务器的配置文件如下所示：

```
failover peer "digitalairlines" {

    primary;

    address 10.0.0.10;

    port 847;

    peer address 10.0.0.12;

    peer port 647;

    max-response-delay 180;

    mclt 1800;

    split 128;

    load balance max seconds 3;

}

# Now we include the identical configuration on both
# machines

include "/etc/dhcpd.conf.master";
```

此示例对等声明中的语句如下：

- **主服务器和辅助服务器。** 确定服务器是主服务器还是辅助服务器，如前所述。
- **地址。** 指定服务器应在其上侦听来自其故障转移对等方的连接的 IP 地址或 DNS 名称。
- **端口。** 指定服务器应在其上侦听来自其故障转移对等方的连接的 TCP 端口（默认值：647 和 847）。必须指定此参数，因为故障转移协议尚未保留 TCP 端口号。
- **对端地址。** 指定服务器为了到达其故障转移对等方而应连接的 IP 地址或 DNS 名称。
- **对端端口。** 指定服务器为了向故障转移对等方发送故障转移消息而应连接的 TCP 端口。必须指定此参数，因为故障转移协议尚未保留 TCP 端口号。对端端口可以与端口相同。
- **最大响应延迟。** 指定 DHCP 服务器在未收到来自其故障转移对等方的消息后等待多少秒，才假定该连接已失败。

此数字应足够小，使得暂时性网络故障导致连接中断时，不会使服务器长时间失去通信；同时又要足够大，以免服务器不断建立和断开连接。

必须指定此参数。

- **最大客户端提前时间。** 定义最大客户端提前时间（Maximum Client Lead Time）。该参数必须在主服务器上指定，也可以在辅助服务器上指定。这是任一故障转移对等方在不联系另一方的情况下可以续订租约的时间长度。

此值设置得越长，运行中的服务器在进入 `PARTNER-DOWN` 状态后恢复 IP 地址所需的时间就越长。设置得越短，服务器在无法通信时承受的负载就越大。

建议值为 1800。

- **拆分值。** 指定主服务器和辅助服务器之间用于负载均衡的拆分比例。

每当客户端发起 DHCP 请求时，DHCP 服务器会对客户端标识执行哈希计算。如果哈希结果小于拆分值，则由主服务器应答；如果结果大于或等于拆分值，则由辅助服务器应答。

有意义的值为 128，且只能在主服务器上配置。

- **负载均衡最大秒数。** 指定一个截止时间，超过该时间后负载均衡将被禁用。该截止时间基于客户端发送其第一条 `DHCPDISCOVER` 或 `DHCPREQUEST` 消息后的秒数。

手册页建议将此值设置为 3 或 5。其效果是，如果其中一个故障转移对等方进入响应故障转移消息但不响应某些客户端请求的状态，另一个故障转移对等方将在客户端重试时自动接管其客户端负载。

## 升级到 Linux 认证工程师 10

辅助服务器的配置文件如下所示：

```
failover peer "digitalairlines" {

    secondary;

    address 10.0.0.12;

    port 647;

    peer address 10.0.0.10;

    peer port 847;

    max-response-delay 180;

    load balance max seconds 3;

}

# Now we include the identical configuration on both
# machines

# include "/etc/dhcpd.conf.master";
```

与主服务器配置的差异在于：语句 `secondary`、缺少语句 `mclt` 和 `split`，以及 `address`、`port`、`peer address` 和 `peer port` 的值互换。

主 DHCP 服务器配置包含在文件 `/etc/dhcpd.conf.master` 中，该文件被两个配置所包含。

为了让 DHCP 服务器找到该文件，需要将其复制到 DHCP 服务器的 chroot 环境中。实现此目的的最佳方法是修改 `/etc/sysconfig/dhcpd` 中的 `DHCP_CONF_INCLUDE_FILES` 变量：`DHCP_CONF_INCLUDE_FILES="/etc/dhcpd.conf.master"`

需要修改主配置文件：

```
ddns-update-style none;

default-lease-time 86400;

max-lease-time 86400;

option domain-name "digitalairlines.com";

option domain-name-servers 10.0.0.254;

option routers 10.0.0.254;

subnet 10.0.0.0 netmask 255.255.255.0 {

    pool {

        failover peer "digitalairlines";

        deny dynamic bootp clients;
```
