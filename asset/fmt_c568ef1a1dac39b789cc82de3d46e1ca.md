
```
# buildah umount working-container
```

一旦 `dnf` 完成软件包安装，容器可以运行，并且可以按如下方式访问 bash 命令提示符：

```
# buildah run working-container bash
bash-5.1#
```

## 28.11 容器桥接网络

如上一章所述，容器网络是使用 Container Networking Interface (CNI) 桥接网络栈实现的。以下命令显示了运行容器的主机系统上的典型网络配置：

```
# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
        valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
    valid_lft forever preferred_lft forever
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:23:24:52:52:57 brd ff:ff:ff:ff:ff:ff
    altname enp0s25
    inet 192.168.86.35/24 brd 192.168.86.255 scope global dynamic noprefixroute
eno1
    valid_lft 68525sec preferred_lft 68525sec
    inet6 fd7f:886f:716a:0:223:24ff:fe52:5257/64 scope global dynamic noprefixroute
    valid_lft 1619sec preferred_lft 1619sec
    inet6 fe80::223:24ff:fe52:5257/64 scope link noprefixroute
    valid_lft forever preferred_lft forever
3: veth15d7e0730if2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master podman0 state UP group default qlen 1000
    link/ether 3e:3a:54:b8:d8:e1 brd ff:ff:ff:ff:ff:ff link-netns netns-658a3069-5c69-185f-ef34-621107da5a71
    inet6 fe80::3c3a:54ff:feb8:d8e1/64 scope link
    valid_lft forever preferred_lft forever
6: podman0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 3e:3a:54:b8:d8:e1 brd ff:ff:ff:ff:ff:ff
    inet 10.88.0.1/16 brd 10.88.255.255 scope global podman0
    valid_lft forever preferred_lft forever
    inet6 fe80::45e:83ff:fe68:4067/64 scope link
    valid_lft forever preferred_lft forever
```

在上面的示例中，主机有一个名为 `eno1` 的接口连接到外部网络，IP地址为 `192.168.86.35`。此外，已创建了一个名为 `podman0` 的虚拟接口，并分配了 IP 地址 `10.88.0.1`。在主机上运行的容器上运行相同的 `ip` 命令可能会产生以下输出：

```
# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
    valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
    valid_lft forever preferred_lft forever
2: eth0@if3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether b6:fb:88:16:8b:5e brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 10.88.0.8/16 brd 10.88.255.255 scope global eth0
    valid_lft forever preferred_lft forever
    inet6 fe80::b4fb:88ff:fe16:8b5e/64 scope link
    valid_lft forever preferred_lft forever
```

在这种情况下，容器的 IP 地址为 `10.88.0.8`。在主机上运行 `ping` 命令可以验证主机和容器确实位于同一子网中：

```
# ping 10.88.0.8
PING 10.88.0.8 (10.88.0.8) 56(84) bytes of data.
64 bytes from 10.88.0.8: icmp_seq=1 ttl=64 time=0.056 ms
64 bytes from 10.88.0.8: icmp_seq=2 ttl=64 time=0.039 ms
.
.
```

我们还可以使用 `podman network ls` 命令获取主机系统上当前可用的容器网络列表：

```
# podman network ls
NETWORK ID   NAME      DRIVER
2f259bab93aa podman    bridge
```

以下命令可用于显示容器网络的详细信息，在本例中为上述 `podman` 网络：

```
# podman network inspect podman
[
    {
        "name": "podman",
        "id": "2f259bab93aaaa2542ba43ef33eb990d0999ee1b4b557b7be53c0b7a1bb9",
        "driver": "bridge",
        "network_interface": "podman0",
        "created": "2023-04-11T08:49:20.489892751-04:00",
        "subnets": [
            {
                "subnet": "10.88.0.0/16",
                "gateway": "10.88.0.1"
            }
        ],
        "ipv6_enabled": false,
        "internal": false,
        "dns_enabled": false,
        "ipam_options": {
            "driver": "host-local"
        }
    }
]
```

新容器网络使用以下语法创建：

```
podman network create <network name>
```

例如，要创建一个名为 `demonet` 的新网络，将使用以下命令：

```
# podman network create demonet
```

## 在 RHEL 9 上使用容器

可以使用 `podman network ls` 命令验证新网络的存在：

```
# podman network ls
NETWORK ID      NAME           DRIVER
9692930055dc    demonet        bridge
2f259bab93aa    podman         bridge
```

创建网络后，可以按如下方式将其分配给容器：
