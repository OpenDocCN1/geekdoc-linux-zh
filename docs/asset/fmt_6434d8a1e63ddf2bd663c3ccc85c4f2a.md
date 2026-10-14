
```text
  --description DESC      指定描述

  --metadata JSON         指定 JSON 格式的元数据:
```

![](img/729ff652633ff312828be609e679849e_177_0.png)

**图 7.14：未配置的 KVM 新网络**

### 添加网络设备

现在，我们可以将此网络添加到我们的虚拟机宿主机中，如图所示。首先，添加一个新设备，然后保存。为了使更改生效，请关闭虚拟机并重新启动。

![](img/729ff652633ff312828be609e679849e_178_0.png)

**图 7.15：虚拟主机的新网络设备**

### 分配 IP 地址

当服务器重启后，让我们为新的网络设备分配一个 IP。首先，通过列出所有网络设备获取新 IP 的名称，然后运行以下命令。

```bash
mahe@hrb-demo:~$ ip a
2: 1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
link/loopback 00000:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6 ::1/128 scope host
valid_lft forever preferred_lft forever
2: enp1s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 500 qdisc fq_codel state UP group default qlen 1000
link/ether 52:54:00:75:89 brd ff:ff:ff:ff:ff
inet 192.168.122.27/24 metric 100 brd 192.168.122.255 scope global dynamic enp10
valid_lft 3589 preferred_lft 3589sec
inet6 fe8:5054:ff66:7589/64 scope link
valid_lft preferred forever
3: enp7s0:<BROADCAST,MULT> mtu 1500 qdisc no state DOWN group default qlen 1000
link/ether 52:54:00:40:b1:16 brd ff:ff:ff:ff:ff
```

前面的命令显示了新网络设备 `enp7s0` 的名称。

### 配置网络

现在我们可以打开网络配置，通过运行以下命令为我们的网卡（NIC）设置 IP：

```bash
mahe@hrb-demo:~$ cat /etc/netplan/00-installer-config.yaml
### 这是由 'subiquity' 写入的网络配置
network:
  ethernets:
    enp1s0:
      dhcp4: true
    enp7s0:
      dhcp4: no
      addresses: [10.33.33.2/24]
  version: 2
mahe@hrb-demo:~$
```

这是 `netplan` 配置，其中添加了网卡的设置。现在，运行以下命令激活您的配置：

```bash
mahe@hrb-demo:~$ ip apply
```

### 验证网络

您可以使用以下命令验证其是否工作：

```text
lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
link/loopback 00000:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6 ::1/128 scope host
valid_lft forever preferred_lft forever
2: enp1s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 500 qdisc fq_codel state UP group default qlen 1000
link/ether 52:54:00:75:89 brd ff:ff:ff:ff:ff
inet 192.168.122.27/24 metric 100 brd 192.168.122.255 scope global dynamic enp10
valid_lft 3589 preferred_lft 3589sec
inet6 fe8:5054:ff66:7589/64 scope link
valid_lft preferred forever
3: enp7s0:<BROADCAST,MULT>UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
link/ether 52:54:00:40:b1:16 brd ff:ff:ff:ff:ff
inet 10.33.33.2/24 brd 10.33.33.255 scope global en7s0
valid_lft forever preferred_lft forever
inet6 fe80::5054:fe40:b16/64 scope link
valid_lft forever preferred_lft forever
```
