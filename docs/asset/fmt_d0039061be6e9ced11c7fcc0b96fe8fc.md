
```
# ping www.example.com
PING www.example.com (192.0.34.166) from 10.0.0.11: 56 (84) bytes of data
64 bytes from 192.0.34.166: icmp_seq=1 ttl=49 time=40.1 ms
64 bytes from 192.0.34.166: icmp_seq=2 ttl=49 time=42.5 ms
64 bytes from 192.0.34.166: icmp_seq=3 ttl=49 time=39.5 ms
64 bytes from 192.0.34.166: icmp_seq=4 ttl=49 time=38.4 ms
64 bytes from 192.0.34.166: icmp_seq=5 ttl=49 time=39.0 ms

--- www.example.com ping statistics ---
5 packets transmitted, 5 received, 0% loss, time 4035ms
rtt min/avg/max/mdev = 38.470/39.971/42.584/1.432 ms
```

在上述示例中，`ping` 数据包往返的平均时间约为 39 毫秒。

向几乎饱和的链路发送 `ping` 看起来像这样：

```
# ping www.example.com
PING www.example.com (192.0.34.166): from 10.0.0.11: 56 (84) bytes of data
64 bytes from 192.0.34.166: icmp_seq=1 ttl=62 time=1252 ms
64 bytes from 192.0.34.166: icmp_seq=2 ttl=62 time=1218 ms
64 bytes from 192.0.34.166: icmp_seq=3 ttl=62 time=1290 ms
64 bytes from 192.0.34.166: icmp_seq=4 ttl=62 time=1288 ms
64 bytes from 192.0.34.166: icmp_seq=5 ttl=62 time=1241 ms

--- www.example.com ping statistics ---
5 packets transmitted, 5 received, 0% loss, time 5032ms
rtt min/avg/max/mdev = 1218.059/1258.384/1290.861/28.000 ms
```

在此示例中，`ping` 数据包往返平均耗时 1.3 秒。从第一个示例到第二个示例，延迟增加了 31 倍！数据链路从正常工作到速度减慢 31 倍，这是链路利用率需要调查的明确迹象。

要更准确地衡量数据吞吐量，可以使用诸如 `tcpp` 这样的工具。要使用 `tcpp` 测试你的连接，你必须在网络和外部机器上安装 `tcpp` RPM 软件包。`tcpp` 软件包包含在本书附带的 DVD 中。如果你不确定该软件包是否已安装，只需在命令提示符下输入 `tcpp`。你应该看到类似以下内容：

```
# tcpp
Usage: tcpp -t [-options] host [ < in]
      tcpp -r [-options > out]
Common options:
 -l ## length of bufs read from or written to network (default 8192)
```

## TCP 选项

- `-u`：使用 UDP 代替 TCP

- `-p #`：要发送或监听的端口号（默认值 5001）

- `-s -t`：向网络发送模式

- `-r`：接收（丢弃）来自网络的所有数据

- `-a`：将缓冲区起始地址对齐到此模数（默认值 16384）

- `-O`：从模数偏移此值开始缓冲区（默认值 0）

- `-v`：详细模式：打印更多统计信息

- `-d`：设置 SO_DEBUG 套接字选项

- `-b #`：设置套接字缓冲区大小（如果支持）

- `-F X`：速率格式：K,M = kilo[bit,byte]；m,M = mega；g,G = giga

**特定于 -t 的选项：**

- `-W #`：写入网络的源缓冲区数量（默认值 2048）

- `-l`：不输出 TCP 写入（设置 TCP_NODELAY 套接字选项）

**特定于 -r 的选项：**

- `-B`：对于 -8，仅输出由 -1 指定的完整块（用于 TAR）

- `-T`："touch"：在读入时访问每个字节

第一步是在服务器机器上启动一个接收器进程：

```bash
# tcp -rs
tcp-r: buflen=8192, nbuf=2048, align=16384/0, port=5001 tcp
tcp-r: socket
```

`-r` 标志表示服务器机器将是接收方。`-s` 标志与 `-r` 标志配合使用，告诉 `tcp` 我们想要忽略任何接收到的数据。

下一步是让您的数据链路之外、拥有与您速度相近的网络链路的人员设置一个 `tcp` 发送进程：

```bash
# tcp -t8 server.example.com
tcp-t: buflen=8192, nbuf=2048, align=16384/0, port=5001 tcp  -->
server.example.com
tcp-t: socket
tcp-t: connect
```

让进程运行几分钟，然后在发送端按 Ctrl+C 停止测试。接收端随后需要一点时间来计算并展示结果：

```bash
# tcp -rs
tcp-r: buflen=8192, nbuf=2048, align=16384/0, port=5001 tcp
tcp-r: socket
tcp-r: accept from 64.223.17.21
tcp-r: 2102496 bytes in 70.02 real seconds = 29.32 KB/sec ***
tcp-r: 1226 I/O calls, msec/call = 58.49, calls/sec = 17.51
tcp-r: 0.0user  0.0sys  1.10real  0% 0+0d 0mxrss 0+2pf 0+0cw
```

在这个例子中，两个主机之间的平均带宽为每秒 29.32 KB。在一个遭受 DDoS 攻击的链路上，这个数字将是该数据链路额定实际带宽的极小一部分。

如果数据链路确实已饱和，下一步是确定连接来源。一种非常有效的方法是使用 `netstat` 命令，它包含在基础 Fedora 安装中。输入以下内容以查看连接信息：

```bash
# netstat -tupn
```

表 14-1 描述了此处使用的每个 `netstat` 参数。

### 表 14-1：`netstat` 参数

| **参数** | **描述** |

| :--- | :--- |

| `-t`，`-tcp` | 显示 TCP 套接字连接。 |

| `-u`，`-udp` | 显示 UDP 套接字连接。 |

| `-p`，`-program` | 显示每个套接字所属程序的 PID 和名称。 |

| `-n`，`-numeric` | 显示数字地址，而不是尝试确定符号主机、端口或用户名。 |

以下是输出可能看起来的样子示例：

![](img/b22364e57409c2481ba806e4e6b9309c_544_0.png)

输出按以下列组织：

- **Proto** — 套接字使用的协议。

- **Recv-Q** — 附加到此套接字的用户程序尚未复制的字节数。

- **Send-Q** — 主机未确认的字节数。

- **Local Address** — 套接字本地端的地址和端口号。

- **Foreign Address** — 套接字远程端的地址和端口号。

- **State** — 套接字的当前状态。表 14-2 提供了套接字状态的列表。

- **PID/Program name** — 拥有该套接字的进程 ID 和程序名称。

### 表 14-2：套接字状态

| 状态 | 描述 |

| :--- | :--- |

| ESTABLISHED | 套接字已建立连接。 |

| SYN_SENT | 套接字正在主动尝试建立连接。 |

| SYN_RECV | 收到来自网络的连接请求。 |

| FIN_WAIT1 | 套接字已关闭并正在关机。 |

| FIN_WAIT2 | 套接字正在等待远程端关闭。 |

| TIME_WAIT | 套接字在关闭后正在等待处理网络中仍然存在的包。 |

| CLOSED | 套接字未使用。 |

| CLOSE_WAIT | 远程端已关闭，正在等待套接字关闭。 |

| LAST_ACK | 远程端已关闭，且套接字已关闭，正在等待确认。 |

| LISTEN | 套接字正在等待传入的连接。 |

| CLOSING | 连接的两端均已关闭，但并非所有数据都已发送。 |
