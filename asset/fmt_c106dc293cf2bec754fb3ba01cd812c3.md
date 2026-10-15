
```
if $int_internet ip saddr $net_class_e drop

if $int_internet ip saddr $loopback drop

if $int_internet ip saddr $subnet_external drop

}
}
```

### 启用 DNS 流量

识别 DNS 流量的规则最先。在 DNS 规则安装之前，除非使用 IP 地址，否则你的网络将无法定位互联网上的服务和主机。对于这些规则，`nft-vars` 文件添加了三个变量：

```
define nameserver_1 = <nameserver ip>

define nameserver_2 = <second nameserver ip>

define nameserver_3 = <third nameserver ip>
```

创建 `dns-policy` 文件来存放以下规则，然后使用命令 `-f dns-policy` 在主 `rc.firewall` 脚本中加载：

```
include "nft-vars"

table filter {

    chain input {

        daddr {$nameserver_1,nameserver_2,nameserver_3} udp sport 53 dport 53 accept

        daddr {$nameserver_1,nameserver_2,nameserver_3} tcp dport 53 accept

    }

    chain output {

        daddr {$nameserver_1,nameserver_2,nameserver_3} udp sport dport 53 accept

        daddr {$nameserver_1,nameserver_2,nameserver_3} tcp sport dport 53 accept

    }

}
```

`INPUT` 和 `OUTPUT` 链中的第一条规则匹配本地缓存的查询和远程 DNS 服务器的响应。本地服务器被配置为主服务器的从服务器；如果查询失败，本地服务器将失效。这种配置在小型办公室中并不常见。`INPUT` 和 `OUTPUT` 链中的后续规则匹配了当服务器响应大到无法放入 UDP 包时，通过 TCP 进行的标准 DNS 客户端请求。这些规则同时被转发服务器和标准客户端使用。

### TCP 客户端流量

通过 TCP 从计算机连接到互联网可以通过为你想要连接的服务器和服务添加特定的输出规则来实现。与之前一样，为此目的显示的规则假设已使用状态跟踪。如果没有启用状态跟踪，则需要在 `INPUT` 链中添加一条规则，以允许特定连接的回入流量。这些规则需要在 `nft-vars` 文件中添加 `server_smtp` 变量：

```
define server_smtp = <your SMTP server>
```

规则进入名为 `tcp-client-policy` 的文件中，然后使用命令 `-f tcp-client-policy` 加载到 `rc.firewall` 程序中：

```
include "nft-vars"

table filter {

    chain input {

        tcp dport {21,22,80,110,143,993,995,443} sport $ports_unpriv accept

        ip daddr $server_smtp tcp dport 25 sport $ports_unpriv accept

    }

}
```

### TCP 服务器流量

在本地服务器上启用服务以允许客户端连接，通过向 `INPUT` 链添加特定规则来实现。理想情况下，你可以将连接限制到已知客户端，并为源地址（`ip saddr <your client ip>`）添加规则，但在现实世界中这通常是不行的。以下文件通过命令 `-f tcp-server-policy` 加载到 `rc.firewall` 脚本中：

名为 `tcp-server-policy` 的规则包含以下内容，用于允许从本地服务器到端口 22 (SSH) 的连接：

```
include "nft-vars"

table filter {

  chain input {

    ip saddr $ip_external tcp sport $ports_unpriv dport (22) accept

  }

  chain output {

  }

}
```

### ICMP 流量

最后，最后对规则匹配入站和出 ICMP 流量。这些规则被加载到名为 `icmp-policy` 的文件中：

```
include "nft-vars"

table filter {

  chain input {

    icmp type {echo-reply,destination-unreachable,parameter-problem,source-quench,time-exceeded} accept

  }

  chain output {

    icmp type {echo-request,parameter-problem,source-quench} accept

  }

}
```

该文件通过命令 `-f icmp-policy` 添加到主 `rc.firewall` 脚本中。

### 使用 nftables 日志丢弃包

防火墙最后的规则记录了未被之前加载的规则处理的数据包。几乎所有要丢弃的传出包都被记录了，因为它们表示防火墙规则存在问题，或者未知（或未授权）的服务尝试联系外部世界。该文件名为 `log-policy`，包含以下规则。使用命令在默认策略之前加载该文件：

```
nft -f log-policy
```

## 优化带来了什么？

优化的目标是尽可能快地让数据包通过过滤处理，减少不必要的测试。理想情况下，你希望数据包以线速流过。以下是规则：

```
include "nft-vars"

table filter {

    chain input {

        log prefix="INPUT dropped: " limit rate 3/second

    }

    chain output {

        log prefix="OUTPUT dropped: " limit rate 3/second

    }

}
```
