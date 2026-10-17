
`interface eth0 => dst. <= src 192.168.1.2:49152 => 93.184.216.34:80 4.00Kb 4.00Kb 4.00Kb 192.168.1.2:49152 <= 93.184.216.34:80 3.00Kb 3.00Kb TX: cum: 4.00Kb peak: 4.00Kb rates: 4.00Kb 4.00Kb 4.00Kb RX: cum: 3.00Kb peak: 3.00Kb rates: 3.00Kb 3.00Kb TOTAL: cum: 7.00Kb peak: 7.00Kb rates: 7.00Kb 7.00Kb`

在上述 `iftop` 输出中，

`TX`: 发送速率。

`RX`: 接收速率。

`TOTAL`: 合计流量。

此输出有助于识别哪些主机正在消耗最多的带宽。

## 使用 `netstat` 显示网络统计

`netstat` 提供网络统计信息和连接详情。

```
$ netstat -tln
```

以下是预期的输出：

| Active Internet connections（仅限服务器） | Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 0 | 0.0.0.0:22 | 0.0.0.0:* | LISTEN |
| tcp6 | 0 | 0 | ::80 | *:* | LISTEN |
| udp | 0 | 0 | 0.0.0.0:123 | 0.0.0.0:* | |
| udp6 | 0 | 0 | ::123 | *:* | |

在上述 `netstat` 输出中，

`Proto`: 协议（TCP, UDP）。

`Recv-Q`: 接收队列。

`Send-Q`: 发送队列。

`Local Address`: 本地地址和端口。

`Foreign Address`: 远程地址和端口。

`State`: 连接状态（如 LISTEN, ESTABLISHED）。

此输出显示了活动连接和监听端口。

## 使用 `vnstat` 监控流量

`vnstat` 记录网络流量并提供使用统计。首先，安装 `vnstat`：

- `$ sudo apt-get install vnstat`
- 初始化数据库：
- `$ sudo vnstat -u eth0`

运行 `vnstat` 命令：

- `$ vnstat`

以下是预期的输出：

```
rx / tx / total / estimated eth0: Apr '24 1.95 GiB / 1.23 GiB / 3.18 GiB / 3.51 GiB today 50.34 MiB / 30.20 MiB / 80.54 MiB / 101.2 MiB
```

在下面的 `vnstat` 输出中，

`rx`: 接收的数据。

`tx`: 发送的数据。

`total`: 合计流量。

`estimated`: 特定期间的估计流量。

此输出提供了网络使用的概览。

## AlphaProject 网络性能

### 示例 1：使用 `ping` 检查连接性

确保 AlphaProject 的服务器可以访问数据库：

`$ ping db-server.gitfor.com`

以下是预期的输出：

```
PING db-server.gitfor.com (192.168.1.10): 56 bytes
from 192.168.1.10: icmp_seq=0 ttl=64 time=0.512 ms 64 bytes
from 192.168.1.10: icmp_seq=1 ttl=64 time=0.475 ms
```

### 示例 2：使用 `traceroute` 追踪路径

诊断到路由问题：

`$ traceroute web-server.gitfor.com`

以下是预期的输出：

```
traceroute to web-server.gitfor.com (192.168.1.20), 30 hops max, 60 bytes 1 192.168.1.1 (192.168.1.1) 1.223 ms 1.173 ms 1.157 ms 2 10.0.0.1 (10.0.0.1) 2.432 ms 2.427 ms 2.418 ms 3 172.16.0.1 (172.16.0.1) 15.367 ms
web-server.gitfor.com (192.168.1.20) 13.343 ms 13.320 ms 13.301
```

此输出有助于识别路径中的任何延迟。

### 示例 3：使用 `iftop` 监控带宽使用

监控 AlphaProject 网络的实时带宽使用：

`$ sudo iftop -i eth0`

以下是预期的输出：

```
interface eth0 => dst. <= src 192.168.1.2:49152 => 93.184.216.34:80 4.00Kb 4.00Kb 4.00Kb 192.168.1.2:49152 <= 93.184.216.34:80 3.00Kb 3.00Kb
TX: cum: 4.00Kb peak: 4.00Kb rates: 4.00Kb 4.00Kb 4.00Kb
RX: cum: 3.00Kb peak: 3.00Kb rates: 3.00Kb 3.00Kb
TOTAL: cum: 7.00Kb peak: 7.00Kb rates: 7.00Kb 7.00Kb
```

此输出显示了哪些连接正在消耗最多的带宽，有助于识别瓶颈。

### 示例 4：使用 `netstat` 显示网络统计

查看 AlphaProject 的活动网络连接和监听端口：

```
$ netstat -tuln
```

以下是预期的输出：

| Active Internet connections（仅限服务器） | Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 0 | 0.0.0.0:22 | 0.0.0.0:* | LISTEN |
| tcp6 | 0 | 0 | ::80 | *:* | LISTEN |
| udp | 0 | 0 | 0.0.0.0:123 | 0.0.0.0:* | |
| udp6 | 0 | 0 | ::123 | *:* | |

此输出有助于确保只有必要的服务在预期端口上运行并监听。

### 示例 5：使用 `vnstat` 监控流量

获取 AlphaProject 在过去一个月和今天的网络使用情况概览：

```
$ vnstat
```

以下是预期的输出：

```
rx / tx / total / estimated eth0: Apr '24 1.95 GiB / 1.23 GiB / 3.18 GiB / 3.51 GiB today 50.34 MiB / 30.20 MiB / 80.54 MiB / 101.2 MiB
```

此输出提供了随时间变化的网络使用概览，有助于识别流量峰值。

`htop` 是一个交互式进程查看器，与 `top` 相比，它的界面更符合用户习惯。它提供了彩色的系统指标显示，并允许更方便导航和进程管理。

安装 `htop`: `$ sudo apt-get install htop`

运行 `htop` 命令: `$ htop`

以下是预期的输出：

```
1 [ 1.6%] Tasks: 125, 1 running 2 [ 0.0%] Load average: 0.05 0.11 0.09 |||||||| 745M/2.0G] Uptime: 10 days, 23:17 Swp [0K/2.0G]
PID USER PRI NI VIRT RES SHR S CPU MEM% TIME+ Command
897 root 20 0 162M 2.5M 1.3M S 0.7 0.1 0:00.32 bash
1243 postgres 20 0
262M 11.2M 9.0M S 0.3 0.5 0:02.05 postgres
```

- 在上述 `htop` 输出中，
  `CPU` 进度条：显示每个 CPU 核心的使用率。
  内存和交换分区条：显示 RAM 和交换区的当前使用情况。
- 负载平均 (`Load Average`)：显示过去 1、5 和 15 分钟的系统平均负载。
- 运行时间 (`Uptime`)：指示系统运行了。
  进程 (`Processes`)：列出进程及其额外的详细信息，如 `CPU%` 和 `MEM%` 使用率。
- 要与 `htop` 交互，
  按 `F6` 排序列名。
  按 `F5` 切换树状视图。
  按 `F9` 杀死进程。
  按 `F10` 退出。

# 示例程序：实现系统监控

### 示例 1：使用 `top` 监控 CPU 和内存使用

运行 `top` 来监控 AlphaProject 的整体 CPU 和内存使用情况：
