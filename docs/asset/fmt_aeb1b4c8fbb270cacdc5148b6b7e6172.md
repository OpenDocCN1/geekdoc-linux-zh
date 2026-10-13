
```
user@server20 ~]$ systemctl status NetworkManager
• NetworkManager.service - Network Manager
Loaded: loaded (/usr/lib/systemd/system/NetworkManager.service; enabled)
Active: active (running) Sat 2019-11-16 23:31:47 EST; 13h ago
Doc: NetworkManager(8)
Tasks: 3 (limit: 11516)
Memory: 11.3M
```

该服务正在运行中。

- 检查新接口的存在：

```
user@server20 ~]$ sudo nmcli d status | grep enp
enp0s3 connected enp0s3
enp0s8 disconnected
```

输出显示了名为 `enp0s8` 的新设备。它还没有附加连接。

- 添加 `add` 连接配置文件 `con` 并将其附加到新接口上。使用类型 `Ethernet`、设备名称 `ifname` `enp0s8`，以及匹配的连接名称 `con-name`、CIDR `ip4` `172.10.10.120/24` 和网关 `gw4` `172.10.10.1`。

```
user@server20 ~]$ sudo nmcli con add type Ethernet ifname enp0s8 con-name enp0s8
ip4 172.10.10.120/24 gw4 172.10.10.1
Connection 'enp0s8' (c9f81ca1-4418-4a8d-9f9a-b6e4368bba46) successfully added.
```

将连接信息在一个名为 `ifcfg-enp0s8` 的新文件中，并存储在 `/etc/sysconfig/network-scripts` 目录下。

### 4. 确认新连接状态：

```
[user@server20 ~] $ nmcli c s
NAME UUID TYPE DEVICE
enp0s3 7426fe5c-9bd4-42ad-84ad-3d15491082b9 ethernet enp0s3
enp0s8 c9f81ca1-4418-4a8d-9f9a-b6e4368baa46 ethernet enp0s8
```

输出结果显示新连接与网络设备的关联。

- 5. 检查 `ifcfg-enp0s8` 连接配置的内容：

```
[user@server20 ~] $ cat /etc/sysconfig/network-scripts/ifcfg-enp0s8
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=none
BOOTPROTO=none
IPADDR=172.10.10.120
PREFIX=24
GATEWAY=172.10.10.1
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6_INIT=yes
IPV6_AUTOCON==
IPV6_ROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp0s8
UUID=c9f81ca1-4418-4a8d-9f9a-b6e4368baa46
DEVICE=enp0s8
ONBOOT=yes
```

除了上述使用 `nmcli` 命令输入的配置项外，连接文件中还添加许多默认指令。`ONBOOT` 指令也被自动设置为 `yes`。此设置表明该连接将在系统重启动时自动启用。

- 6. 检查新连接的 IP 分配情况：

```
[user1@server20 ~]$ ip a
    enp0s8 <BROADCAST,MULTICAST,LOWER_UP> mtu 1500 qdisc fq_codel state UP group
    default qlen 1000
    link/ether 08:00:27:a1:18:b4 ff:ff:ff:ff:ff:ff
    inet 172.16.10.10/24 172.16.10.25 scope global noprefix enp0s8
        valid_lft forever preferred_lft forever
    inet fe80::9d:3bc7:a3b8:5bb3/64 scope link noprefix
        valid_lft forever preferred_lft forever
```

IP 已分配给接口。该连接将在本章的后续部分进行测试。

### 7. 禁用此连接以将其从接口上分离：

```
[user@server20 ~]$ sudo nmcli c down enp0s8
Connection 'enp0s8' successfully deactivated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/4)
```

连接配置现在已从接口分离，连接已取消激活。你可以通过 `nmcli c s` 进行检查。

### 8. 重新激活连接以将其附加到接口：

```
[user@server20 ~]$ sudo nmcli c up enp0s8
Connection successfully activated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/5)
```

连接配置现在已重新附加到接口，连接已激活。你可以通过 `nmcli c s` 进行检查。

本练习到此结束。

## 理解 hosts 表 (Hosts Table)

系统上使用的每个 IP 地址都应该分配一个主机名。在网络中有多个系统的环境中，采用某种主机名到 IP 地址的解析方法是明智的，以避免在访问时反复输入目标系统的 IP。DNS 是其中一种方法，它专为企业网络和互联网等大型网络设计。对于小型内部网络，使用本地 hosts 表 ` /etc/hosts ` 文件也很常见。该表用于维护本地网络系统主机名到 IP 的映射，允许我们仅通过主机名即可访问系统。在书中存在两个系统：IP 为 `192.168.0.110` 的 `server10.example.com` 及其别名 `server10`，以及 IP 为 `192.168.0.120` 的 `server20.example.com` 及其别名 `server20`。你可以如下所示将这些信息添加到 `server10` 和 `server20` 的 `/etc/hosts` 文件中：

```
192.168.0.110 server10.example.com server10
192.168.0.120 server20.example.com server20
```

文件的每一行第一列包含一个 IP 地址，第二列是官方（或规范）主机名，其之后是一个或多个可选的别名。官方主机名和一个或多个别名为用户提供了使用其中任何一个名称访问系统的灵活性。

> 考试贴士：在存在活跃的 DNS 且所有主机名均可解析的情况下，无需担心更新 hosts 文件。如上所述，使用 hosts 文件在小型网络中很常见，并且应该在每个单独系统上对其进行更新，以反映任何更改。

## 测试网络连通性 (Testing Network Connectivity)

RHEL 包含 `ping` 命令来检查两个系统之间的网络连通性。它使用目标系统的 IP 地址发送一系列 64 字节的互联网控制协议 `ICMP` 包。通过远程系统的响应验证连通性。通过 `-c` 选项，你可以指定要发送的包数。从 `server10` 向 `192.168.0.120` 发送两个包：

```
server10 ~ ping 192.168.0.120 -c 2
PING 192.168.0.120 (192.168.0.120) 56(84) bytes of data.
64 bytes from 192.168.0.120: icmp_seq=1 ttl=64 time=0.406 ms
64 bytes from 192.168.0.120: icmp_seq=2 ttl=64 time=0.418 ms
--- 192.168.0.120 ping statistics
2 packets transmitted, 2 received, 0% packet loss, time 38ms
rtt min/avg/max/dev = 406/412/418/06 ms
```

# 练习 17-5：更新 hosts 表并测试连通性
