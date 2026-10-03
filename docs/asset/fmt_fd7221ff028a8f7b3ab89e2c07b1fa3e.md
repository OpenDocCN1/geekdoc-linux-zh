
# MikroTik 基础配置

```bash
[admin@MikroTik]/ip route add gateway=10.42.0.1
[admin@MikroTik]/ip firewall nat add chain=src action=masquerade
[admin@MikroTik]/ip dns set servers=8.8.8
[admin@MikroTik]> ping yahoo.com
```

# 启动 Ubuntu 服务器

- 打开终端
- 设置静态 IP

编辑网络配置文件：

```bash
sudo vim /etc/network/interfaces
```

配置内容如下：

```yaml
auto eth0
iface eth0 inet static
address 192.168.88.10
netmask 255.255.255.0
gateway 192.168.88.1
```

重启网络服务：

```bash
sudo /etc/init.d/networking restart
```

之后你就能连接互联网了。

# 安装 DHCP 服务器

更新仓库：

```bash
sudo apt-get update
```

安装 DHCP 软件包：

```bash
sudo apt-get install isc-dhcp-server
```

# 配置服务器

进入配置目录并编辑配置文件：

```bash
cd /etc/dhcp
vim dhcpd.conf
```

配置示例：

```bash
option domain-name "mydomain.org";
### 添加一个域名
option domain-name-servers 8.8.8;
```

## 基础子网声明

```bash
subnet 192.168.88.0 netmask 255.255.255.0 {
    range 192.168.88.20 192.168.88.200;
    option routers 192.168.88.1;
}
```

参数说明：

```bash
# 解释
subnet <give the network> netmask <give subnet> {
    range <starting ip in the range> <ending ip of the range>;
    option routers <gateway>
}
```

# 重启服务器

```bash
sudo /etc/init.d/isc-dhcp-server restart
```

# 客户端侧

启动客户端（此处以 VPCS 为例）：

```bash
PC-1> ip dhcp
DDORA
IP 192.168.88.21/24 GW 192.168.88.1
```

测试连通性：

```bash
PC-1> ping 8.8.8.8
84 bytes from 8.8.8.8 icmp_seq=1 ttl=116 time=59.929 ms
84 bytes from 8.8.8.8 icmp_seq=2 ttl=116 time=65.707 ms
```

如果你运行的是 Linux 客户端，打开终端并输入：

```bash
dhclient
```
