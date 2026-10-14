
```
[root@moksha]# ping parikrama

PING parikrama (192.168.1.4): 56 bytes of icmp_seq=1 ttl=255 time=0.297 ms

64 bytes from parikrama (192.168.1.4): icmp_seq=2 ttl=255 time=0.299 ms

64 bytes from parikrama (192.168.1.4): icmp_seq=3 ttl=255 time=0.293 ms

64 bytes from parikrama (192.168.1.4): icmp_seq=4 ttl=255 time=0.296 ms

64 bytes from parikrama (192.168.1.4): icmp_seq=5 ttl=255 time=0.297 ms

64 bytes from parikrama (192.168.1.4): icmp_seq=6 ttl=255 time=0.292 ms

--- parikrama statistics ---

6 packets transmitted, 6 received, 0% packet loss, time 505ms

rtt min/avg/max/dev = 0.292/0.295/0.299/0.020 ms
```

Figure 2.37. `ping` 程序的 TCP dump 输出。

```
Snoop output of ping command -
IP: ----- IP Header -----
IP: Version = 4
...
IP: Protocol = 1 (ICMP)
IP: Header checksum = 2c51
IP: Source address = 192.168.1.4, parikrama
IP: Destination address = 192.168.1.3, moksha
IP: No options
IP:
ICMP: ----- ICMP Header -----
ICMP:
ICMP: Type = 8 (Echo request)
ICMP: Code = 0 (ID: 950 Sequence number: 4)
ICMP: Checksum = 47ea
ICMP:
IP: ----- IP Header -----
IP: Version = 4
...
IP: Protocol = 1 (ICMP)
IP: Header checksum = bc22
IP: Source address = 192.168.1.3, moksha
IP: Destination address = 192.168.1.4, parikrama
IP: No options
IP:
ICMP: ----- ICMP Header -----
ICMP:
ICMP: Type = 0 (Echo reply)
ICMP: Code = 0 (ID: 950 Sequence number: 4)
ICMP: Checksum = 4fea
ICMP:
```

Figure 2.38. `ping` 请求的 Snoop 输出。

## 2.17 ARP/RARP

`ARP` 是一种设计用于链路层寻址地址解析协议。`RFC 2176` 详细规定了该协议。在本节中，我们将专门讨论以太网类型和 `IP`。在以太网链路上的 `IP` 中，一个以太网接口关联一个或多个 `IP` 地址。每个以太网接口都有特定的地址。

在以太网中，当我们需要向特定 `IP` 地址的主机发送数据包时，生成 `ARP` 来获取与之相关的硬件地址。`RARP` 是 `ARP` 的反向，我们想要对应以太网地址的 `IP` 地址。在这种情况下，`ARP` 头部中的目标硬件地址设置为已知硬件地址。`RARP` 服务器回复查询。`RARP` 可能由主机生成以获取自己的 `IP` 地址，主要用于网络启动客户端。注意 `RARP` 服务器应该在同一个子网内，因为 `RARP` 请求是广播，不会经过路由器。

`ARP` 和 `RARP` 的数据包如图 2.39 所示。

`hardware type`。这是一个 16 位字段，指示生成 `ARP`/`RARP` 的链路层标识。对于以太网，该字段设置为 1。对于 `RARP`，该字段设置为 `0x8035`。

`protocol type`。这是一个 16 位值，是与硬件地址关联的网络层协议的标识。对于 `IP`，该值为 4 `0x0800`。

`hardware addr len`。这是一个 8 位字段，包含硬件地址值的长度。对于以太网，硬件地址的长度为 6 字节。

`proto addr len`。这是一个 8 位字段，包含与硬件关联的协议地址的长度。在 `IPv4` 的情况下，该值为 4 字节。

| 16-bit hardware type | 16-bit protocol type |
|---|---|
| 8-bit hardware addr len | 8-bit proto addr len |
| | 16-bit operation code |
| | sender hardware addr |
| | sender protocol address |
| | destination hardware addr |
| | destination protocol address |

Figure 2.36. `ICMP` 请求-响应头部。

# 协议基础

操作码（`operation code`）。这是一个 16 位的值，表示要对 `ARP` 数据包进行执行的操作。由于请求和回复使用相同的数据包格式，因此该字段用于标识这是一个 `ARP` 请求还是回复。对于 `ARP` 请求和回复，其值分别为 1 和 2。对于 `RARP` 请求和回复，其值分别为 3 和 4。

发送者地址（`sender address`）。这是请求/响应源源的硬件地址。在以太网的情况下，其长度为 6 字节。

发送者协议地址（`sender protocol address`）。这是发送者的协议地址地址。在 `IPv4` 的情况下，其长度为 4 字节。

目标硬件地址（`destination hardware address`）。这是目标主机的硬件地址。在以太网的情况下，其长度为 6 字节。在 `RARP` 的情况下，它将被设置为未知 `IP` 的主机的硬件地址。该字段由 `ARP` 请求的回复填充。

目标协议地址（`destination protocol address`）。这是与目标硬件地址相关的协议地址。在 `ARP` 的情况下，该字段被设置为未知硬件地址的协议地址（`IPv4` 地址）。该字段由 `ARP` 请求的回复填充。

图 2.40 显示了 `ARP` 请求的嗅探输出。以太网头部中的目标地址被设置为所有 `0xff`。头部中的以太网类型被设置为 `0806`，即 `ARP`。`ARP` 头部中的 `HARDWARE` 类型设置为 1，即以太网。生成 `ARP` 的协议设置为 `0x0800`，表示 `IP`。硬件地址长度为 6 字节（以太网地址），协议地址长度设置为 4 字节（`IP` 地址）。操作码为 1，表示这是一个 `ARP` 请求。最后四行是发送者的硬件地址和 `IP` 地址；目标硬件地址为空，因为这需要为目标协议地址 `192.168.1.8` 查找。

```
------ Ether Header -----
ETHER:
ETHER: Packet 4 arrived at 22:08:22.13004
ETHER: Packet size = 42 bytes
ETHER: Destination = ff:ff:ff:ff:ff:ff (broadcast)
ETHER: Source = 00:c0:9f:61:8a:43,
ETHER: Ethertype = 0806 (ARP)
ETHER:
ARP:
ARP: ---- ARP/RARP Frame -----
ARP:
ARP: Hardware type = 1
ARP: Protocol type = 0800 (IP)
ARP: Length of hardware address = 6 bytes
ARP: Length of protocol address = 4 bytes
ARP: Opcode 1 (ARP Request)
ARP: Sender's hardware address = 0:c0:9f:61:8a:43
ARP: Sender's protocol address = 192.168.1.4, parikrama
ARP: Target hardware address = =
ARP: Target protocol address = 192.168.1.8, 192.168.1.8
ARP:
```
