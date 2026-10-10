
默认的 NIS 服务器配置知道 `auto.master` 和 `auto.home` 映射；但对 `auto.software` 一无所知。由于这种用例，你必须编辑 `/var/yp/Makefile`。你需要在以 `all;` 开头的行末尾添加你的映射名称，然后转到现有映射的条目（例如 `auto.home`），复制它，并用你的映射名称替换现有的映射。

`/home` 是挂载的，通过单行配置即可控制所有主目录。挂载的设备在匹配文本应被插入的位置包含一个安培符（`&`）。在这种情况下，如果用户尝试 `cd` 进入 `/home/mario`，文件系统 `homesvr:/export/home/mario` 就会挂载到 `/home/mario`。

一个局限性在于，这是一个“全有全无”的方案。你要么使用通配符作为唯一的行，要么必须手动指定每个目录。然而，你可以多次替换通配符。例如，假设每个用户的工作站都以用户 ID 命名并包含其主目录。你可以使用以下行：

```
* -defaults,soft,intr &:/export/home/
```

但是，如果你想将用户的主目录聚类在几台服务器上，你需要在 `auto.home` 中列出每个用户，或者使用可执行映射。

![](img/f36419c0b225d12fa66de83fa271829b_676_0.png)

# Debian 系统管理 第二部分

可执行映射是一个程序或脚本，它接受一个键作为参数并返回自动挂载行，如果键不存在则不输出。它在 `auto.master` 映射中以文件名的形式指定；且必须由 `root` 执行。列表 19.10 显示了一个示例 `bash` 脚本，它将名称以 a 到 m 字母开头的用户映射到一台服务器，将所有其他用户映射到另一台服务器。当然，这可以根据需要变得非常复杂——例如，查找另一个 NIS 映射或查询数据库。

## 列表 19.10 `/usr/local/sbin/usermap`，一个可执行的自动挂载映射

```bash
#!/bin/bash
case $1" in
 [a-m]*)
  echo "$1 -defaults,soft,intr svr01:/export/home/$1"
  ;
 default)
  echo "$1 -defaults,soft,intr svr02:/export/home/$1"
esac
```

要使用此映射，你的 `auto.master` 文件包含以下行：

```
/home    /usr/local/sbin/usermap
```

如你所见，自动挂载器结合 NIS 和 NFS 可以消除管理大型 Linux 或 UNIX 网络中的许多头问题。例如，如果你添加或删除一个服务器，或者需要在服务器之间移动内容，你只需要修改 NIS 主服务器上的映射并推送映射（通过简单的 `make`），所有客户端都将自动更新。

# TCP/IP 故障排除工具

配置好 TCP/IP 网络后，问题很少出现。然而，“很少”并不意味着永远不会。运行中的设备会故障，线路会中断，电缆也会连接问题。此外，问题在网络主机的初始配置期间也会发生。

在 Linux 中，有三个基础的网络故障排除工具。其中两个（`ping` 和 `traceroute`）与主机到达另一个主机的能力有关，第三个（`tcpdump`）有助于分析网络中的流量。后续章节将介绍其中一些工具。

## ping

最基础的网络故障排除工具是 `ping` 程序。它以潜水艇声纳发出的声音命名，`ping` 会向另一个主机发送数据包并等待该主机的回复。`ping` 主要用于查看网络上的机器是否可以通信。如果它们可以互相 `ping`，那么它们应该能够向网络上的其他机器发送几乎任何数据。`ping` 使用 `ICMP`（互联网控制消息协议），这是一个运行在 `IP` 之上的协议，设计用于路由和可达性信息等控制消息。

使用 `ping` 最常见的方法是向它传递主机名或地址：

```
% ping server.company.com
PING server.company.com (10.0.1.10): 56 data bytes
64 bytes from 10.0.1.10: icmp_seq=0 ttl=82.239 ms
64 bytes from 10.0.1.10: icmp_seq=1 ttl=82.808 ms
64 bytes from 10.0.1.10: icmp_seq=2 ttl=82.994 ms
64 bytes from 10.0.1.10: icmp_seq=3 ttl=81.635 ms
```

```
-- server.company.com ping statistics --
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 81.638/82.169/83.239 ms
```

在这种情况下，`ping` 每秒 `ping` 目标主机一次，直到你按下 `Ctrl+C`。在该时刻，它会打印统计信息。在统计信息中，你可以看到发送和接收的数据包数量、最小、平均和最大往返时间。`ping` 有许多选项，常见的有：

| 选项 | 功能 |
| :--- | :--- |
| `-c` | 发送计数 |
| `-n` | 显示数字地址而非主机名 |
| `-r` | 记录路由 |
| `-q` | 静默。仅输出最终统计信息 |
| `-v` | 详细 |

在排除故障时，你应该首先 `ping` 默认网关。之后，你可以 `ping` 通往目的地的。这有助于确定问题所在。如果你无法 `ping` 默认网关，问题可能在本地网络上。

# Debian 系统管理 第二部分

所有 TCP/IP 数据包都有一个名为 `TTL`（生存时间）的字段。该字段会被每个路由器减少。当它变为零时，路由器丢弃数据包并返回过期通知。`ping` 使用默认 `TTL` 255，许多程序如 `traceroute` 使用较小的 `TTL`。`Traceroute` 会增加数据包的 `TTL`，直到到达目的地。

## traceroute

`traceroute` 程序是 TCP/IP 故障排除的主力。它通过发送 `TTL` 逐渐增加的数据包来绘制数据包的路径。其工作原理如下：`traceroute` 开始发送 `TTL` 为 1 的数据包。第一个路由器减少 `TTL`（变为 0）并返回响应。如果不是目标主机，`traceroute` 程序将 `TTL` 加1（新值为 2）并发送另一个数据包。下一个路由器同样如此。直到你到达目标主机或达到最大 `TTL`（默认值为 30，可以通过 `-m` 更改）。

`traceroute` 为每个 `TTL` 发送三个数据包，并报告每个数据包的往返时间。`traceroute` 的用法与 `ping` 相同——提供目标地址。列表 19.11 显示 `traceroute` 的输出示例：

## 列表 19.11 traceroute 输出示例

```
maria@chaos=: 511 $ /usr/bin/traceroute www.umbral.com
taceroute to xmaya.umbral.com (207.87.18.30) 30 hops, 40 bytes
1 master.spin.com (200.13.81.123) 120.75 ms 126.72 ms 109.53 ms
2 octopus.spin.com (200.13.81.32) 110.042 ms 104.654 ms 99.599 ms
3 200.33.218.161 (200.33.218.161) 119.539 ms 105.697 ms 109.663 ms
4 rri1.mxdefnd.antel.net (200.33.209.1) 131.556 ms 112.767 ms 109.6 ms
5 bordercore-hshi0.Dallas.com (146.67.249) 159.54 ms 155.357 ms
169.598
```

# 高级网络管理工具

# 第 19 章

```
6 6core9.dallas.cw.net (204.70.89) 159.483 ms 156.364 ms 159.628 ms

7 dfw2-core2-s1-0-0.atlas.digex (165.117.59.13) 169.505 ms 156.024 ms 149.628 ms

8 lax1-core1-s8-0-0.atlas.digex (165.117.50.25) 199.497 ms 194.006 ms 189.621 ms

9 sjc4-core2-s5-0-0.atlas.digex (165.117.53.74) 199.489 ms sjc4-core2-s5-0-atlas.digex (165.117.56.110) 191.025 ms

10 sjc4-core6-pos1-1.atlas.digex (199.117.569) 201.031 ms 196.195 ms 199.584 ms

11 sjc4-wscore-p1-0.wsmg.digex (199.125.178.37) 306.468 ms 366.267 ms 199.481 ms
```
