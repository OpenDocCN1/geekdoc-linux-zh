
如果远程系统不确认保活包，TCP 将使用以下重传计时器之一，并在其过期后终止连接：

| 状态 | 定时器 | 默认值 |
| --- | --- | --- |
| 已建立连接 | `tcp_ip_abort_interval` | 60000 ms (10 分钟) |
| 连接建立 | `tcp_ip_abort_cinterval` | 240000 ms (4 分钟) |
| 连接终止 | `tcp_keepalive_detached_interval` | 240000 ms (4 分钟) |

### 5.1.1.4 TCP 等待延迟

默认情况下，Windows 2000 在连接关闭后会保持 240 秒（四 分钟）的套接对。要更改此值，请编辑以下注册表项：
`HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\TcpWaitDelay`

此参数的值范围于 30 到 300 秒之间。
HP-UX 默认情况下，TCP 端点在等待延迟中保持 60 秒的时间间隔。该值可以使用 `ndd -set /dev/tcp tcp_time_wait_interval` 命令进行更改。该命令的参数指定单位为毫秒，范围从 100 毫秒到 600,000 毫秒。

### 5.1.2 仅限 Windows 2000 的调优参数

Windows 2000 允许通过注册表对 TCP 进行调优，这在 HP-UX 中没有对应项。以下是一些注册表项的列表。更多信息请参见注册表参考。

- `TcpDelAcks`. 更改 ACK 计时器。默认值为 200 毫秒。
- `SacOpts`. 启用/禁用选择性确认（SACKs）。默认启用。
- `TcpMaxDataRetransmissions`. 决定 TCP 在现有连接上重传未确认数据段的次数。TCP 会重传数据段直到其被确认，或直到该值超时。默认值为五。
- `TcpMaxConnectRetransmissions`. 决定 TCP 重传未应答新连接请求的次数。TCP 会重传新连接请求直到收到响应，或直到该值超时。默认值为二。
- `TcpMaxDupAcks`. 指定多少个重复 ACK（针对相同序列号的 ACK）构成重传段的信号。默认值为二。

### 5.1.3 仅限 HP-UX 的调优参数

以下是 HP-UX `ndd` 命令的参数列表，这些参数在 Windows 2000 中没有对应的注册表项。更多信息请使用 `ndd -h` 命令。例如：

```
ndd -h tcp_conn_request_max
```
