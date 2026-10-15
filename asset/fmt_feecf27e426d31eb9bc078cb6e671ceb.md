
# `netstat -an | grep SYN_RCVD | wc -l`

将系统在正常条件下返回的值作为基准。你也可以通过查看 `netstat` 摘要来检测 TCP SYN 攻击，输出应该如下：

| TCP | tcptoAlgorithm | tcptoMin | 400 |
| --- | --- | --- | --- |
| tcptoMax | tcpMaxConn | -1 |
| tcpActiveOpens | 4821 | tcpPassiveOpens | 1179 |
| tcpAttemptFails | 4675 | tcpResets | 5 |
| tcpCurrEstab | 2 | tcpOutSegs | 134889 |
| tcpOutDataSeg | 100583 | tcpOutDataBytes | 129482 |
| tcpRetransSegs | 62 | tcpRetransSegs | 34302 |
| tcpOutAck | 29722 | tcpOutDelayed | 7869 |
| tcpOutUrg | 0 | tcpOutUpdate | 97 |
| tcpOutWinProbe | 3 | tcpOutControl | 11973 |
| tcpOutRsts | 4672 | tcpRetransSegs | 3 |
| tcpInSegs | 183296 | tcpAckSegs | 91907 |
| tcpInAckBytes | 1294013 | tcpInDupAck | 421 |
| tcpInAckUnsent | 0 | tcpInOrderSegs | 96602 |
| tcpInOrderBytes | 1536244 | tcpInOrderSegs | 2 |
| tcpInOrderBytes | 2166 | tcpInDupSegs | 8 |
| tcpInDupBytes | 4561 | tcpInPartSegs | 0 |
| tcpInPartDupBytes | 0 | tcpInWinSegs | 0 |
| tcpInPastWinBytes | 0 | tcpInWinProbe | 0 |
| tcpInWinUpdate | 3 | tcpInClosed | 2 |
| tcpRttNoUpdate | 20 | tcpRttUpdate | 90670 |
| tcpTimRetrans | 33 | tcpTimRetransDrop | 0 |
| tcpTimKeepalive | 778 | tcpTimKeepaliveProbe | 0 |
| tcpTimKeepaliveDrop | 0 | tcpListenDrop | 0 |
| tcpListenDropQ0 | 0 | tcpHalfOpenDrop | 0 |
| tcpOutSackRetrans | 0 |

通过检查参数 `tcpTimRetransDrop` 和 `tcpListenDrop` 的值可以识别 TCP SYN 攻击。`tcpTimRetransDrop` 参数显示了自启动以来由于超时导致的异常数量，该值包含了 SYN 请求和已建立的 TCP 连接。`tcpListenDrop` 参数显示了系统启动以来由于 TCP 队列溢出而被拒绝的 SYN 请求数量。如果 `tcpListenDrop` 值随着 `tcpTimRetransDrop` 的值快速增加，则系统极可能正遭受 TCP SYN 攻击。

另一种判断 Solaris 系统是否遭受 TCP SYN 攻击的方法是使用 `snnoop` 实用程序监控出主机的流量。虽然这不是检测 SYN 攻击的理想方法，但使用 `snnoop` 验证 SYN 泛洪的发生可能非常有用。简单地监控目标为受攻击主机的 TCP 流量。以下示例显示了 SYN 泛洪的样本跟踪：

```bash
# snnoop -d le0 -o /tmp/snoop.log -v host attack.hacker.org

# host solaris.victim.com tcp and port 22

1. 0.0000 attack.hacker.org -> solaris.victim.com TCP D=22
S=42369 Seq=2982763941 Len=0=Win=4096

2. 0.0034 attack.hacker.org -> solaris.victim.com TCP D=22
S=61389 Seq=997843043 Len=0=Win=2048

3. 1.92965 attack.hacker.org -> solaris.victim.com TCP D=22
S=37583 Seq=4106242639 Len=0=Win=4096

7. 1.85421 attack.hacker.org -> solaris.victim.com TCP D=22
S=61620 Seq=2182414901 Len=0=Win=2048

9. 1.93544 attack.hacker.org -> solaris.victim.com TCP D=22
S=45278 Seq=1561416019 Len=0=Win=1024

11. 1.91951 attack.hacker.org -> solaris.victim.com TCP D=22
S=53009 Seq=3348440882 Len=0=Win=3072

13. 1.77750 attack.hacker.org -> solaris.victim.com TCP D=22
S=63144 Seq=941883255 Len=0=Win=4096
```

## 深度解析攻击 • 第10章

```bash
15. 1.86887 attack.hacker.org -> solaris.victim.com TCP D=22
S=61460 Seq=1188106034 Len=0 Win=1024

17. 1.82336 attack.hacker.org -> solaris.victim.com TCP D=22
S=53869 Seq=1735024976 Len=0 Win=3072

19. 1.98871 attack.hacker.org -> solaris.victim.com TCP D=22
S=45286 Seq=2771164840 Len=0 Win=1024
```

所示的数据包是从攻击者主机 `attack.hacker.org` 向目标 `solaris.victim.com` 发送的 SYN 包。缺失的包（数据包 2、4、6、8 等）是 `solaris.victim.com` 向攻击者发送的 SYN-ACK。协议为 TCP，目标端口为 22（D=22），以及攻击者的源端口（跟踪轨迹中的 `S=` 字段）和攻击者的 TCP 序列号（如 `Seq=` 字段所示）。

在防御 TCP SYN 洪水攻击时，Solaris 管理员必须执行以下两点：

- 缩短中止定时器（abort timer）的值
- 延长 TCP 连接队列的长度

可以使用内核参数 `tcp_ip_abort_interval` 来缩短中止间隔。该参数的值单位是毫秒，默认间隔为 18000 毫秒，即 180 秒。如需更改此值，应使用 `ndd` 工具。要将超时时间设为 60 秒，系统管理员可以使用：

```bash
# ndd -set /dev/tcp tcp_ip_abort_interval 60000
```

内核参数 `tcp_conn_req_max_q0` 控制 Solaris 2.6 及更高版本中未建立的 TCP 连接的队列大小（在带有补丁 103581-11 的 Solaris 2.5.1 中亦然）。`tcp_conn_req_max_q0` 的默认值为 1024。要增加队列大小，请使用以下命令：

```bash
# ndd -set /dev/tcp tcp_conn_req_max_q0 2048
```

需要考虑的一点是，增加 TCP 连接队列的大小会导致内核消耗更多内存。内存有限的系统可能会因为缓解 TCP SYN 洪水攻击的尝试而无法使用。

另一个需要考虑的点是，TCP SYN 洪水攻击可以耗尽已建立连接队列。这种攻击对黑客来说没有那么吸引力，因为连接可以追溯到源，但它仍然是一个问题。Solaris 2.6 及更高版本（以及带有补丁 103582-11 的 Solaris 2.5.1）提供了对已建立 TCP 连接队列大小的控制。

![](img/ab996f014aa8c5c7de3d77cc73ef5ce3_317_0.png)

### 第10章 • 深度解析

这种控制通过内核参数 `tcp_conn_req_max_q` 提供（注意该队列名称与不稳定 TCP 连接队列名称之间的相似性）。其默认值为 128。要将已建立的 TCP 连接队列增加到 256，命令是：

```bash
# ndd -set /dev/tcp tcp_conn_req_max_q 256
```
