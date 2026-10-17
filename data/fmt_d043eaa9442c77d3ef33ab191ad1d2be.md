
某些系统在执行无选项的 `ping` 时会提供性能信息；另一些系统则报告系统“存活”（is alive）。以下是检查本地系统与网络上名为 `austin` 的另一个系统之间连接的示例：

```
martyp $ ping austin
austin is alive
martyp $
```

在大多数 UNIX 变体中，你可以调整数据包大小和迭代次数，如下所示的 HP-UX 示例，指定数据包大小为 4096，间隔为 5：

```
# ping 12 4096 5
PING 12: 4096 bytes from
4096 bytes from 10.1.1.12: icmp seq=0, time=2.ms ms
4096 bytes from 10.1.1.12: icmp seq=1, time=2.ms ms
4096 bytes from 10.1.1.12: icmp seq=2, time=2.ms ms
4096 bytes from 10.1.1.12: icmp seq=3, time=2.ms ms
4096 bytes from 10.1.1.12: icmp seq=4, time=2.ms ms
```

```
---12 Ping Statistics-----
5 packets transmitted, 5 packets received, 0% packet loss
round-trip (ms) min/avg/max = 2/2/2
#
```

AIX 允许你通过 `-l` 指定间隔以及其他选项，包括包大小和迭代次数。以下示例显示了 AIX 系统的选项：

```
martyp $ ping -I 5 austin 4096 10
PING austin: 4096 data bytes
4104 bytes from austin (128.185.61): icmp seq=0.
time=8.ms
4104 bytes from austin (128.185.61): icmp seq=1.
time=9.ms
4104 bytes from austin (128.185.61): icmp seq=2.
time=9.ms
4104 bytes from austin (128.185.61): icmp seq=3.
time=9.ms
4104 bytes from austin (128.185.61): icmp seq=4.
time=8.ms
4104 bytes from austin (128.185.61): icmp seq=5.
time=9.ms
4104 bytes from austin (128.185.61): icmp seq=6.
time=9.ms
4104 bytes from austin (128.185.61): icmp seq=7.
time=9.ms
4104 bytes from austin (128.185.61): icmp seq=8.
time=9.ms
4104 bytes from austin (128.185.61): icmp seq=9.
time=9.ms
----austin PING Statistics
10 packets transmitted, 10 packets received, 0% loss
round-trip (ms) min/avg/max = 9/9/15
martyp $
```

在这个示例中，每五秒 `ping` 一次，包大小为 4096 字节，总共十次。现在回到我们的示例。我如何知道 `system1` 与路由器以及路由器另一侧的系统之间有连接？我使用 `ping` 命令。以下是我知道 `system1` 连接到 `router1` 的方式：（img/6969df54e516231f8e64fd1177ac1127_892_0.png)

```
$ ping router1

router1: 64 bytes

4 bytes from 128.185.61.2: icmp seq=0. time=0. ms

64 bytes from 128.185.61.2: icmp seq=1. time=0. ms

64 bytes from 128.185.61.2: icmp seq=2. time=0. ms
```

这里的每一行输出都代表设备返回的响应。这意味着该设备已做出响应。你可以持续获取这种响应直到终止 `ping`。如果没有产生所示的输出，则没有发生响应，你可能遇到了问题：（img/6969df54e516231f8e64fd117ac1127_893_0.png)

# netstat

从之前的子网掩码描述可以看出，一个主机到另一个主机的路由取决于路径。你可以使用 `netstat` 命令获取与路由相关的信息。`-r` 选项显示你想了解的路由表，`-n` 选项可以打印网络地址而不是名称。使用 `-v` 选项，可以获取路由相关的额外信息，例如子网掩码。在以下示例中，使用 `-r` 和 `-m` 选项执行 `netstat`，以便对比输出：（img/6969df54e516231f8e64fd1177ac1127_894_0.png)

| Dest/Netmask | Gateway | Flags | Refs | Use | Interface | Pmtu |
|---|---|---|---|---|---|---|
| 127.0.0.1 | 127.0.0.1 | UH | 0 | 1905 | lo0 | 4136 |
| 127.0.0.1 | 127.0.0.1 | UH | 0 | 343 | lan1 | 4136 |
| 127.0.0.1 | 127.0.0.1 | U | 2 | 0 | lan0 | 4136 |
| 10.1.1.0 | 10.1.1.0 | U | 2 | 0 | lan0 | 1500 |
| 10.1.1.0 | 10.1.1.0 | U | 2 | 0 | lan1 | 1500 |
| 127.0.0.1 | 127.0.0.1 | U | 0 | 0 | lo0 | 4136 |
| default | 10.1.1.1 | UG | 0 | 0 | lan1 | 1500 |

```
# netstat -r
Routing tables
Dest/Netmask
```

| Dest/Netmask | Gateway | Flags | Refs | Use | Interface | Pmtu |
|---|---|---|---|---|---|---|
| 127.0.0.1/255.255.255.255 | 127.0.0.1 | UH | 0 | 1916 | lo0 | 4136 |
| 127.0.0.1/255.255.255.255 | 127.0.0.1 | UH | 0 | 343 | lan1 | 4136 |
| 10.1.1.110/255.255.255.255 | 10..1.1.110 | U | 0 | 0 | lan0 | 4136 |
| 10.1.1.0/255.255.255.255 | 10.1.1.0 | U | 2 | 0 | lan0 | 1500 |
| 10.1.1.0/255.255.255.255 | 10.1.1.0 | U | 2 | 0 | lan1 | 1500 |
| 127.0.0.1/255.255.255.255 | 127.0.0.1 | U | 0 | 0 | lo0 | 4136 |
| default/0.0.0.0 | 10.1.1.1 | UG | 0 | 0 | lan1 | 1500 |

```
# netstat -r
Routing tables
Dest/Netmask
```

# netstat -r

Routing tables

Dest/Netmask
