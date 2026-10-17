
- 在辅助域名服务器上修改主配置文件 `named.rfc1912.zones`，在 zone 设置 type 为 `slave`，设置文件指定区域文件的存放位置，通过 `masters(主 DNS 服务器的 IP 地址);` 指定主域名服务器的地址。

设置完成后重启 DNS 服务，就能看到目标记录已经同步到辅助区域了。

为了数据的安全，在主域名服务器上指定由域名服务器从主域名服务器复制区域文件信息。这种方法是在主域名服务器的选项里添加 `allow-transfer(辅助 DNS 的 IP 地址或者是 IP 的范围)`，表示当前域名服务器的所有辅助服务器都可以将数据传输到指定的域名服务器；如果只是希望将某个区域的数据传输到指定的域名服务器，可以将 `allow-transfer` 放置到主配置文件的对应的区域中，这样的服务器就不会再复制到主域名服务器的区域信息。

说明：在主域名服务器允许区域文件的传输的，辅助域名服务器才能进行区域复制。只有在主域名服务器的选项中添加了 `allow-transfer();` 语句，辅助域名服务器能够从主域名服务器进行区域复制。

### 12.2.7 DNS 转发

当 DNS 客户端指定的域名服务器要求解析名称，而此域名服务器无法解析，将用缓存中的信息帮助解析其他服务器，通常会找到一个域名服务器来进行递归查询。为了减少服务器的负担，可以设置域名服务器转发(Forwarder)。

定义了域名转发后，本地域名服务器将使用转发器列表中的域名服务器，从缓存中的域名服务器来响应客户端的查询。配置了转发器列表的域名服务器将不能从自己响应的请求，发送给定义的转发服务器。

转发是在 `named.conf` 文件中的区域设置。要用到两个配置选项：

- `forwarders` 指令设置将 DNS 请求转发到哪个服务器，可以指定多个服务器的 IP 地址：

```
forwarders {
    DNS_IP1;
    DNS_IP2;
};
```

- `forward` 指令用于设置 DNS 转发模式。

语法：`forward first|only;`

- `forward first`: 设置优先 forwarders DNS 服务器域名解析，如果查询不到再使用本地 DNS 服务器域名解析。
- `forward only`: 设置只使用 forwarders DNS 服务器域名解析，如果查询不到则返回 DNS 客户端查询失败。

例：在学院某台主机上设置 DNS 域名转发器。

- ① 在需要进行域名转发的服务器上安装 BIND。
- ② 修改配置文件 `named.conf`。修改配置文件 `named.conf` 的 `options` 字段，并用 `forwarders` 和 `forward` 指令设置 DNS 转发，需要转发的远程 DNS 服务器为 `172.16.43.254`。

修改内容如下：

```
options {
    forwarders {
        172.16.43.254;
    };
    forward first;
}
```

## 项目 12 部署 DNS 服务

### 12.3 反思与进阶

- 1. 项目背景

随着学院客户端数量增加，访问量也随之增加，为了提高 DNS 解析的速度和可靠性，IT 会原有的主 DNS 服务器的基础上部署辅助 DNS 服务器。辅助 DNS 服务器的 IP 地址为 `172.16.43.250`。

- 2. 实施目的

- `1.` 明确 DNS 服务器的各种角色及操作。
- `2.` 掌握主服务器的安装与配置。
- `3.` 掌握辅助 DNS 服务器的配置。

- 3. 实施步骤

- `1.` 配置主机 IP 地址为 `172.16.43.250`，关闭防火墙，设置 `SELinux` 为 `Permissive`。

```bash
[root@localhost ~]# ifconfig ens33
ens33:flags=416<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
inet 172.16.43.250  netmask 255.255.255.0  broadcast 172.16.43.255
inet6 fe80::a67d:2c19:db5b:39ce prefix 64  scope 0x20<link>
ether 00:0c:29:04:af:ac  txqueuelen 1000
(Ethernet)
RX packets 2886  bytes 89833
(877.2 KiB)
```

![](img/ec0e037f26e46c767b8ae4c4c4a36e86_258_0.png)

部署辅助 DNS 服务器

## 学习环境 2 部署 Linux 网络服务

| RX errors | dropped 0 | overruns 0 | frame 0 |
|---|---|---|---|
| TX packets 228 | bytes 25689 | 25.0 KiB | |
| TX errors 0 | dropped 0 | overruns 0 | collisions 0 |

```bash
[root@localhost ~]# systemctl stop firewall
[root@localhost ~]# systemctl disable firewall
[root@localhost ~]# vi /etc/selinux/config
[root@localhost ~]# setenforce 0
[root@localhost ~]# getenforce
Permissive
```

`2.` 安装 `BIND` 软件包。

```bash
[root@localhost ~]# yum install -y
```

`3.` 在 IP 地址为 `172.16.43.254` 的主 DNS 服务器上配置：

① 修改全局配置文件 `named.conf`。在全局配置文件中增加 `allow-transfer(172.16.43.250)` 指定区域 DNS 服务器，如图所示。

```bash
[root@localhost ~]# vi /etc/named.conf
```

`4.` 在 IP 地址为 `172.16.43.250` 的辅助 DNS 服务器上配置：

- ① 修改辅助 DNS 服务器的全局配置文件 `named.conf`。

```bash
root@localhost ~]# cat /etc/named.conf
options {
  listen-on port 53 { any };
  listen-on ipv6-port 53 { any };
  directory "/var/named";
  dump-file "data/cache_dump.db";
  statistics-file "data/stats.txt";
  metrics-file "data/metrics.txt";
  recording-file "data/named";
  secrets-file "data/secrets";
  recursion yes;
  allow-query { any };
};
```

- ② 修改辅助 DNS 服务器的主配置文件 `named.rfc1912.zones`。

```bash
root@localhost ~# vim /etc/named.rfc1912.zones
zone "zhiyuan.com" {
  type slave;
  file "slaves/zhiyuan.zone";
  masters {172.16.43.254};
};

zone "172.16.in-addr.arpa" {
  type slave;
  file "slaves/zhiyuan.zone";
  masters {172.16.43.254};
};
```

辅助区域的配置文件放在 `slaves` 目录下是不必要的，也可以放在其他目录，但必须确保辅助区域的所有者和组是 `named`，否则 BIND 将无法从主区域传输信息。

`5.` 分别启动主服务器和辅助 DNS 服务器。

```bash
root@localhost ~# systemctl start named
```

`6.` 在辅助 DNS 服务器上进入 `slaves` 目录，查看对应的区域文件。

```bash
root@localhost ~# cd /var/named/slaves/
root@localhost slaves# ls
```

`7.` 测试。

① 在主 DNS 服务器中设置域名服务器。

```bash
root@localhost ~# vim /etc/resolv.conf

search zhiyuan.com
nameserver 172.16.43.254
nameserver 172.16.43.250
```

② 在 DNS 服务器中关闭 `named`。
