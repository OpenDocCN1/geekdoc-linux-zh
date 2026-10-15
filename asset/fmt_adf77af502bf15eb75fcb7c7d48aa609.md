
在此服务器上，当它提供 IP 地址时，会打印 `DPOFFER` 消息。最后一条消息是来自客户端的 `DHCPACK`。

DHCP 日志文件 `/var/lib/dhcp/db/dhcpd.leases` 包含如下信息：

```
failover peer "digitalairlines" state {

  my state recover at 2 2006/07/04 09:57:39;

  partner state unknown-state at 2 2006/07/04 09:57:39;

}

failover peer "digitalairlines" state {

  my state recover at 2 2006/07/04 09:57:39;

  partner state recover at 2 2006/07/04 09:57:39;

}

failover peer "digitalairlines" state {

  my state recover-done at 2 2006/07/04 09:57:56;

  partner state recover at 2 2006/07/04 09:57:39;

}

failover peer "digital airlines" state {

  my state recover-done at 2 2006/07/04 09:57:56;

  partner state recover-done at 2 2006/07/04 09:57:39;

}

failover peer "digital airlines" state {

  my state normal at 2 2006/07/04 09:57:56;

  partner state recover-done at 2 2006/07/04 09:57:39;

}

failover peer "digital airlines" state {

  my state normal at 2 2006/07/04 09:57:56;

  partner state normal at 2 2006/07/04 09:57:39;

}

lease 10.0.0.120 {

  starts 2 2006/07/04 09:57:56;

  tstp 2 2006/07/04 09:57:56;

  binding state backup;

}

lease 10.0.0.119 {

  starts 2 2006/07/04 09:57:56;

  tstp 2 2006/07/04 09:57:56;

  binding state backup;

}

lease 10.0.0.120 {

  starts 2 2006/07/04 09:57:56;

  tstp 2 2006/07/04 09:57:56;

  binding state backup;

}
```

当备服务器发生故障（例如服务器关闭）并在稍后恢复时，在主服务器的 `/var/log/messages` 中会出现类似下面的消息：

| Jul 4 12:16:25 da10 dhcpd: peer digitalairlines: disconnected |
| Jul 4 12:16:25 da10 dhcpd: failover peer digitalairlines: I move from normal to communications-interrupted |
| Jul 4 12:20:06 da10 dhcpd: failover peer digitalairlines: peer moves from normal to normal |
| Jul 4 12:20:06 da10 dhcpd: failover peer digitalairlines: I move from communications-interrupted to normal |
| Jul 4 12:20:06 da10 dhcpd: pool 800e4138 10.0.0/24 total 20 free 10 backup 9 lts 0 |

在备服务器上，启动信息如下：

| Jul 4 12:21:01 da12 dhcpd: failover peer digitalairlines: I move from normal to startup |
| Jul 4 12:21:01 da12 dhcpd: failover peer digitalairlines: peer moves from normal to communications-interrupted |
| Jul 4 12:21:01 da12 dhcpd: failover peer digitalairlines: I move from startup to normal |
| Jul 4 12:21:01 da12 dhcpd: failover peer digitalairlines: peer moves from communications-interrupted to normal |
| Jul 4 12:21:01 da12 dhcpd: pool 800e40f8 10.0.0/24 total 20 free 10 backup 9 lts 0 |

> 为了防止被时间戳混淆，请确保您使用网络时间协议（ntp）同步所有服务器的时间戳。

客户端日志文件 `/var/lib/dhcpd/dhcpcd-eth0.info` 仅包含关于客户端配置以及提供该信息的 DHCP 服务器的信息：

![](img/b7f4ef3c9bdffc8caed3395478c04bab_151_0.png)

```
IPADDR=10.0.0.111

NETMASK=255.255.255.250

NETWORK=10.0.0.0

BROADCAST=10.0.0.255

GATEWAY=10.0.0.254

DOMAIN='digitalairlines.com'

DNS=10.0.0.254

DHCPSID=10.0.0.12

DHCGIADDR=0.0.0.0

DHCPSIADDR=0.0.0.0

DHCPSADDR=00:04:AC:D6:58:96

DHCPSHADDR=00:04:AC:D6:55:F4

DHCPFSNAME=''

LEASETIME=1800

RENEWALTTIME=900

REBINDTIME=1575

INTERFACE='eth0'

CLASSID='Linux 2.6.16.20-0.12-default i686'

CLIENTID=00:04:AC:D6:58:96
```

## 目标 7 排除 DHCP 故障

`dhcp-tools` 包包含了排除 DHCP 故障最重要的两个工具。它们将在目标中进行介绍：

- `dhcping`
- `dhcpcdump`

## dhcping

你可以使用 `dhcping` 实用程序检查 DHCP 服务器是否有响应。

你可以指定：

- 客户端想要保留的地址 (`-c`)
- 要查询的服务器 (`-s`)
- 客户端的硬件地址 (`-h`)

如果 DHCP 服务器有响应，将出现一条类似下面的消息：

```
da51:~ # dhcping -c 10.0.0.5 -s 10.0.0.51 -h 00:90:27:51:47:A9

Got answer from: 10.0.0.51
```

如果服务器没有响应，消息如下所示：

```
da51:~ # dhcping -c 10.0.0.5 -s 10.0.0.200 -h 00:90:27:51:47:A9

no answer
```

随后，服务器的日志文件将包含以下条目：

```
Nov 25 17:05:56 da51 dhcpd: DHCPREQUEST for 10.0.0.5 from 00:90:27:a4:96:1f via eth0

Nov 25 17:05:56 da51 dhcpd: DHCPACK on 10.0.0.5 to 00:90:27:a4:96:1f via eth0

Nov 25 17:05:56 da51 dhcpd: DHCPRELEASE of 10.0.0.5 from 00:90:27:a4:96:1f via eth0
```

## dhcpdump

你可以使用 `tcpdump` 工具来分析客户端和服务器之间的通信。为了这个目的，`tcpdump` 输出：

```
da51:~ # tcpdump -i eth0 | dhcp
```
