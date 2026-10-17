
```bash
table filter {
  chain input {
    ct established,related accept
    ct state invalid log "INVALID input: * limit 3/second
    drop
  }
  chain output {
    ct established,related accept
    ct state invalid log "INVALID output: * limit 3/second"
  }
}
```

以下是 `default-policy` 的内容：

```bash
table filter {
  chain input {
    drop
  }
  chain output {
    drop
  }
table nat {
  chain postrouting {
    drop
  }
  chain prererouting {
    drop
  }
}
```

以下是 `dns-policy` 的内容：

```bash
include "nft-vars"
table filter {
  chain input {
    ip daddr {$nameserver_1,$nameserver_2,$nameserver_3 } udp sport
    53 dport 53 accept
    ip daddr {$nameserver_1,$nameserver_2,$nameserver_3 } tcp sport
    53 dport $ports_unpriv accept
    ip daddr {$nameserver_1,$nameserver_2,$nameserver_3 } udp sport
    53 dport $ports_unpriv accept
  }
  chain output {
    ip daddr {$nameserver_1,$nameserver_2,$nameserver_3 } udp sport
    53 dport 53 accept
  }
}
```

# 录 B 防火墙示例与支持脚本

```bash
ip daddr {$nameserver_1,$nameserver_2,$nameserver_3 } tcp sport
$ports_unpriv tcpport 53 accept
ip daddr {$nameserver_1,$nameserver_2,$nameserver_3 } udp sport
$ports_unpriv udpport 53 accept
}
```

以下是 `icmp-policy` 的内容：

```bash
include "nft-vars"
table filter {
  chain input {
    icmp type {echo-reply,destination-unreachable,parameter-problem,source-quench,time-exceeded } accept
  }
  chain output {
    icmp type {echo-request,parameter-problem,source-quench } accept
  }
}
```

以下是 `invalid-policy` 的内容：

```bash
include "nft-vars"
table filter {
  chain input {
    if $int_internet saddr $ip_external drop
    if $int_internet saddr $net_class_a drop
    if $int_internet saddr $net_class_b drop
    if $int_internet saddr $net_class_c drop
    if $int_internet protocol udp daddr $net_class_d accept
    if $int_internet saddr $net_class_e drop
    if $int_internet saddr $int_loopback drop
    if $int_internet saddr $broadcast_dest drop
  }
  chain output {
  }
}
```

以下是 `localhost-policy` 的内容：

```bash
include "nft-vars"
table filter {
  chain input {
    ifname $int_loopback accept
  }
  chain output {
    ifname $int_loopback accept
  }
}
```

以下是 `log-policy` 的内容：

```bash
include "nft-vars"
table filter {
  chain input {
    log prefix "INPUT packet dropped: " limit 3/second
  }
  chain output {
    log prefix "OUTPUT packet dropped: " limit 3/second
  }
}
```

以下是 `setup-tables` 的内容：

```bash
include "nft-vars"
table filter {
  chain input {
    type filter hook input priority 0;
  }
  chain output {
    type filter hook output priority 0;
  }
}
```

以下是 `tcp-client-policy` 的内容：

```bash
include "nft-vars"
table filter {
  chain input {
  }
  chain output {
    tcp dport {21,80,143,443} sport $ports_unpriv accept
    ip daddr $server_smtp tcp sport $ports_unpriv accept
  }
}
```

以下是 `tcp-server-policy` 的内容：

```bash
include "nft-vars"
table filter {
  chain input {
    ip daddr $ip_external tcp dport {22} accept
  }
  chain output {
  }
}
```

此页故意留空

# 术表

本术表定义了书中使用的术语和缩写。多词术语按术语中的主要名词进行字母排序，后面跟着逗号和术语的其他部分。

`ACCEPT` 防火墙规则决策，允许数据包通过其下一个目的地。

`accept-everything-by-default` 一种策略，接受所有未匹配链防火墙规则的数据包。因此，大多数防火墙规则都是拒绝（DENY）。

`ACK` 用于确认接收到先前分段的 TCP 标志。

`application-level gateway` 参见 `proxy, application-level.` 通常称为 ALG、应用层（或层）网关。在防火墙术语中，ALG 通常指特定的应用程序模块，为嵌入地址插入应用程序负载并识别与会话相关的次级流。

`AUTH` TCP 服务端口 113，与已识别的用户关联。

`authentication` 确定实体是否为其所声称的身份或对象的过程。

`authorization` 确定实体可以使用哪些服务和资源的过程。

`bastion` 参见 `firewall`, bastion。

`BIND` 伯克互联网域名（Berkeley Internet Name Domain），DNS 协议的 Berkeley 实现。

`BOOT` 引导协议（Bootstrap Protocol），磁盘工作站用于发现其 IP 地址和启动服务器的位置，并在启动前通过 TFTP 启动系统下载。BOOTP 是为了取代 RARP 开发的。

`BOOTPC` UDP 服务端口 68，与 BOOTP 和 DHCP 客户端关联。

`bootpd` BOOTP 服务器程序。

`BOOTPS` UDP 服务端口 67，与 BOOTP 和 DHCP 服务器关联。

# 录 C 术表

`border router` 位于网络边缘或边界的路由数据包的设备。

`broadcast` 一种指向并发送到连接到网络或子网的所有接口的 IP 包。

`CERT` 计算机应急响应小组，是 1988 年网络蠕虫后在卡内基梅隆大学软件工程学院成立的一个信息协调中心和互联网安全预防中心。

`chain` 定义哪些数据包可以进入或离开网络接口的规则列表。
