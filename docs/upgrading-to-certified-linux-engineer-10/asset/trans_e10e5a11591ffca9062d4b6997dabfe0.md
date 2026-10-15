

需要修改主配置文件：

```
ddns-update-style none;

default-lease-time 86400;
max-lease-time 86400;

option domain-name "digitalairlines.com";
option domain-name-servers 10.0.0.254;

option routers 10.0.0.254;

subnet 10.0.0.0 netmask 255.255.255.0 {
    pool {
        failover peer "digitalairlines";
        deny dynamic bootp clients;
        range 10.0.0.101 10.0.0.120;
    }
}
```

所有故障转移配置都必须在 pool 语句中定义。如果使用多个池，则需要在每个池中定义故障转移配置。

> 为了能够识别故障转移配置的名称，它必须在池定义之前定义。这就是为什么 include 语句写在 /etc/dhcpd.conf 的末尾。

故障转移不适用于包含分配给 bootp 客户端的地址的地址分配池。因此，必须定义语句 deny dynamic bootp clients;。

在主服务器上启动 DHCP 服务器时，你将在 /var/log/messages 中看到如下信息：

```
Jul  4 11:52:29 da10 dhcpd: failover peer digitalairlines:
I move from recover to startup
Jul  4 11:52:44 da10 dhcpd: failover peer digitalairlines:
I move from startup to recover
Jul  4 11:54:57 da10 dhcpd: failover peer digitalairlines:
peer moves from unknown-state to recover
Jul  4 11:54:57 da10 dhcpd: failover peer digitalairlines:
requesting full update from peer
Jul  4 11:54:57 da10 dhcpd: Sent update request all message
to digitalairlines
Jul  4 11:54:57 da10 dhcpd: failover peer digitalairlines:
peer moves from recover to recover
Jul  4 11:54:57 da10 dhcpd: failover peer digitalairlines:
requesting full update from peer
Jul  4 11:54:57 da10 dhcpd: Sent update done message to
digitalairlines
Jul  4 11:54:57 da10 dhcpd: Update request all from
digitalairlines: nothing pending
Jul  4 11:54:57 da10 dhcpd: failover peer digitalairlines:
peer update completed.
Jul  4 11:54:57 da10 dhcpd: failover peer digitalairlines:
I move from recover to recover-done
Jul  4 11:54:57 da10 dhcpd: failover peer digitalairlines:
I move from recover-done to normal
Jul  4 11:54:57 da10 dhcpd: failover peer digitalairlines:
peer moves from recover-done to normal
Jul  4 11:54:57 da10 dhcpd: pool 800e4138 10.0.0/24 total
20 free 20 backup 0 lts -10
Jul  4 11:54:57 da10 dhcpd: pool 800e4138 10.0.0/24 total
20 free 20 backup 0 lts 10
```

在稍后启动的从服务器上，/var/log/messages 中会出现如下信息：

```
Jul  4 11:55:52 dal2 dhcpd: failover peer digitalairlines:
I move from recover to startup
Jul  4 11:55:52 dal2 dhcpd: failover peer digitalairlines:
peer moves from unknown-state to recover
Jul  4 11:55:52 dal2 dhcpd: failover peer digitalairlines:
requesting full update from peer
Jul  4 11:55:52 dal2 dhcpd: failover peer digitalairlines:
I move from startup to recover
Jul  4 11:55:52 dal2 dhcpd: Sent update request all message
to digitalairlines
Jul  4 11:55:52 dal2 dhcpd: Sent update done message to
digitalairlines
Jul  4 11:55:52 dal2 dhcpd: Update request all from
digitalairlines: nothing pending
Jul  4 11:55:52 dal2 dhcpd: failover peer digitalairlines:
peer update completed.
Jul  4 11:55:52 dal2 dhcpd: failover peer digitalairlines:
I move from recover to recover-done
Jul  4 11:55:52 dal2 dhcpd: failover peer digitalairlines:
peer moves from recover to recover-done
Jul  4 11:55:52 dal2 dhcpd: failover peer digitalairlines:
I move from recover-done to normal
Jul  4 11:55:52 dal2 dhcpd: failover peer digitalairlines:
peer moves from recover-done to normal
Jul  4 11:55:52 dal2 dhcpd: pool 800e40f8 10.0.0/24 total
20 free 20 backup 0 lts 10
Jul  4 11:55:52 dal2 dhcpd: pool response: 10 leases
```

当客户端请求 IP 地址时，你将在 /var/log/messages 中看到如下信息：

```
Jul 4 11:59:26 dal0 dhcpd: DHCPREQUEST for 192.168.5.16 from 00:04:ac:d6:58:96 via eth0: ignored (not authoritative).
Jul 4 11:59:30 dal0 dhcpd: DHCPREQUEST for 192.168.5.16 from 00:04:ac:d6:58:96 via eth0: ignored (not authoritative).
Jul 4 11:59:36 dal0 dhcpd: pool 800e4138 10.0.0/24 total 20 free 10 backup 10 its 0
Jul 4 11:59:36 dal0 dhcpd: DHCPDISCOVER from 00:04:ac:d6:58:96 via eth0
Jul 4 11:59:36 dal0 dhcpd: DHCPREQUEST for 10.0.0.111 (10.0.0.12) from 00:04:ac:d6:58:96 via eth0: lease owned by peer
Jul 4 11:59:37 dal0 dhcpd: DHCPOFFER on 10.0.0.110 to 00:04:ac:d6:58:96 (linux-5ncs) via eth0
```

在这种情况下，客户端发送 DHCPREQUEST 以获取与上次相同的 IP 地址（192.168.5.16）。该地址不在范围定义中，因此服务器拒绝提供此地址。客户端随后发送 DHCPDISCOVER 以检测 DHCP 服务器。

客户端的下一条消息是针对 IP 地址 10.0.0.111 的 DHCPREQUEST，该地址由从服务器提供（“lease owned by peer”）。最后一条消息是从服务器发出的 DHCPOFFER。

