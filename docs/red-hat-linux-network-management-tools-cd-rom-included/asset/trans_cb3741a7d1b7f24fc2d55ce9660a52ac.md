

## ICMP 组

### ICMP 对象

| 对象名称 | OID | 对象类型 | 访问模式 | 描述 |
|-------------|-----|-------------|-------------|-------------|
| icmpEchoReps | icmp.9 | Counter | read-only | 接收到的 ICMP 回显应答消息数量 |
| icmpTimestamps | icmp.10 | Counter | read-only | 接收到的 ICMP 时间戳请求消息数量 |
| icmpInTimestampReps | icmp.11 | Counter | read-only | 接收到的 ICMP 时间戳应答消息数量 |
| icmpAddrMasks | icmp.12 | Counter | read-only | 接收到的 ICMP 地址掩码请求数量 |
| icmpAddrMasksReps | icmp.13 | Counter | read-only | 接收到的 ICMP 地址掩码应答消息数量 |
| icmpOutMsgs | icmp.14 | Counter | read-only | 系统尝试发送的 ICMP 消息数量 |
| icmpOutErrors | icmp.15 | Counter | read-only | 因 ICMP 问题导致系统无法发送的 ICMP 消息数量 |
| icmpOutDestUnreachs | icmp.16 | Counter | read-only | 发送的 ICMP 目标不可达消息数量 |
| icmpOutTimeExcds | icmp.17 | Counter | read-only | 发送的 ICMP 超时消息数量 |
| icmpOutParmProbs | icmp.18 | Counter | read-only | 发送的 ICMP 参数问题消息数量 |
| icmpOutSrcQuenchs | icmp.19 | Counter | read-only | 发送的 ICMP 源抑制消息数量 |
| icmpOutRedirects | icmp.20 | Counter | read-only | 发送的 ICMP 重定向消息数量 |
| icmpOutEchos | icmp.21 | Counter | read-only | 发送的 ICMP 回显请求消息数量 |
| icmpOutEchoReps | icmp.22 | Counter | read-only | 发送的 ICMP 回显应答消息数量 |
| icmpOutTimestamps | icmp.23 | Counter | read-only | 发送的 ICMP 时间戳请求消息数量 |
| icmpOutTimestampReps | icmp.24 | Counter | read-only | 发送的 ICMP 时间戳应答消息数量 |
| icmpOutAddrMasks | icmp.25 | Counter | read-only | 发送的 ICMP 地址掩码请求消息数量 |
| icmpOutAddrMaskReps | icmp.26 | Counter | read-only | 发送的 ICMP 地址掩码应答消息数量 |

### 查询 ICMP 组的示例输出

```text
icmp.icmpInMsgs.0 = 27
icmp.icmpInErrors.0 = 0
icmp.icmpInDstUnreachs.0 = 7
icmp.icmpInTimeExcds.0 = 0
icmp.icmpInParmProb.0 = 0
icmp.icmpInSrcQuenches.0 = 0
icmp.icmpInRedirects.0 = 0
icmp.icmpInEchos.0 = 8
icmp.icmpInEchoReps.0 = 12
icmp.icmpInTimestamps.0 = 0
icmp.icmpInTimestampReps.0 = 0
icmp.icmpInAddrMasks.0 = 0
icmp.icmpInAddrMaskReps.0 = 0
```

```text
icmp.icmpOutMsgs.0 = 10
icmp.icmpOutErrors.0 = 0
icmp.icmpOutDestUnreachs.0 = 2
icmp.icmpOutTimeExcds.0 = 0
icmp.icmpOutParmProbs.0 = 0
icmp.icmpOutSrcQuenchs.0 = 0
icmp.icmpOutRedirects.0 = 0
icmp.icmpOutEchos.0 = 0
icmp.icmpOutEchoReps.0 = 8
icmp.icmpOutTimestamps.0 = 0
icmp.icmpOutTimestampReps.0 = 0
icmp.icmpOutAddrMasks.0 = 0
icmp.icmpOutAddrMaskReps.0 = 0
```

从输出可以看出，许多计数器的值都很低。这符合预期。某些对象（如 icmpInTimeExcds）的高计数表明存在配置问题或其他操作问题。

## TCP 组

tcp 组存储系统上传输控制协议 (TCP) 的统计和操作信息。该组包含一个表，用于存储系统上每个 TCP 连接的信息。图 6.11 显示了该组的树视图。

![图 6.11 tcp 组视图。](img/f265c9d1f2610aca197c430cbfcd51f5_327_0.png)

### TCP 对象

| 对象名称 | OID | 对象类型 | 访问模式 | 描述 |
|-------------|-----|-------------|-------------|-------------|
| tcpRtoAlgorithm | tcp.1 | Counter | read-only | 重传时间算法；可能的值包括 other(1)、constant(2)、rsrc(3) 和 varj(4) |
| tcpRtoMin | tcp.2 | Counter | read-only | 重传计时器的最小值 |
| tcpRtoMax | tcp.3 | Counter | read-only | 重传计时器的最大值 |
| tcpMaxConn | tcp.4 | Counter | read-only | 系统支持的 TCP 连接总数（或限制） |
| tcpActiveOpens | tcp.5 | Counter | read-only | 该系统支持的主动打开次数 |
| tcpPassiveOpens | tcp.6 | Counter | read-only | 该系统支持的被动打开次数 |
| tcpAttemptFails | tcp.7 | Counter | read-only | 该系统上发生的失败连接尝试次数 |
| tcpEstabResets | tcp.8 | Counter | read-only | 该系统上发生的复位次数 |
| tcpCurrEstab | tcp.9 | Counter | read-only | 处于 ESTABLISHED 或 CLOSE-WAIT 状态的 TCP 连接数量 |
| tcpInSegs | tcp.10 | Counter | read-only | 接收到的段数，包括错误接收的段 |
| tcpOutSegs | tcp.11 | Counter | read-only | 发送的段数，但不包括包含重传字节的段 |
| tcpRetransSegs | tcp.12 | Counter | read-only | 重传段的数量 |
| tcpConnTable | tcp.13 | Counter | read-only | TCP 连接信息 |
| tcpInErrors | tcp.14 | Counter | read-only | 错误接收的段数量 |
| tcpOutRsts | tcp.15 | Counter | read-only | 发送的包含 RST 标志的 TCP 段数量 |

### 轮询 Linux 系统的示例输出

```text
tcp.tcpRtoAlgorithm.0 = other(1)
tcp.tcpRtoMin.0 = 0
tcp.tcpRtoMax.0 = 0
tcp.tcpMaxConn.0 = 0
tcp.tcpActiveOpens.0 = 105422
tcp.tcpPassiveOpens.0 = 0
tcp.tcpAttempFails.0 = 2968
tcp.tcpEstabResets.0 = 0
tcp.tcpCurrEstab.0 = Gauge: 2
tcp.tcpInSegs.0 = 63591
tcp.tcpOutSegs.0 = 111130
tcp.tcpRetransSegs.0 = 1881
```

### tcpConnTable

`tcpConnTable` 表存储系统上 TCP 连接的具体信息。图 6.12 显示了该表的树视图。`tcpConnEntry` 对象用作表中的索引。该表的大小由系统上记录的连接数量决定。在繁忙的服务器上，它可能非常大。

![图 6.12 tcpConnTable 视图。](img/f265c9d1f2610aca197c430cbfcd51f5_331_0.png)

`tcpConnState` 对象标识连接的当前状态。有效值包括：closed(1)、listen(2)、sysSent(3)、sysReceived(4)、established(5)、finWait1(6)、finWait2(7)、closeWait(8)、lastAck(9)、closing(10)、timeWait(11) 和 deleteTCB(12)。除 `deleteTCB(12)` 外，这些状态值代表第 2 章“简单网络管理协议”中讨论的 TCP 状态机模型。回想一下，每个连接将处于这些定义状态之一。`deleteTCB(12)` 状态表示该连接的 TCP 控制块 (TCB) 已被删除。其余对象存储本地和远程 IP 地址及端口对。例如，考虑以下输出：

