
这两行代码为输入链（入站流量）创建了规则，只要它们来自 DNS（参见 `/etc/services/`），两者都是接受的。我们还希望在该系统上浏览网页，所以在在连接启动时接受 TCP 数据包：

```
ipchains -A input -p TCP -y
```
...（此处之后原文已开始严重重复和乱码，翻译已按原文重复内容执行）。

## 表 10.4 内部网络常用的 IP 范围值

| 主机 | INT 值 | 伪装主机 |
|---|---|---|
| n192.168.1.1 | 192.168.0/24 | 192.168.1.1-192.168.254 |
| 192.168.1.1 | 192.168.0.0/16 | 192.168.1.1-192.168.255.254 |
| 10.1.1.1 | 10.1.1.0/24 | 10.1.1.1-10.1.254 |
| 10.1.1.1 | 10.1.0.0/16 | 10.1.1.1-10.1.255.254 |
| 10.1.1.1 | 10.0.0.0/8 | 10.1.1.1-10.255.255.254 |

完成这些更改后，创建规则的系统将充当内部网络其他系统的合理路由器。

## 端口转发

在你的极简防火墙后面，很有可能至少有一个你想向外部世界提供的服务。为了让外部世界的机器能够连接到你的内部网络，必须明确进行某些翻译，因为你内部网络中的 IP 地址在广大的互联网上是无效的。

在 Linux 内核 2.2 版本中，这种翻译是通过内核伪装代码以及一个名为 `ipmasqadm` 的工具（即 IP 伪装管理工具）完成的。`ipmasqadm` 的语法非常简单，如下：

```
ipmasqadm portfw -a P tcp -L MYip port -R server_ip port
```

例如，假设内部网络中的某台机器上运行着 Web 服务器。该机器的 IP 地址为 192.168.1.14，且 Web 服务器运行在标准端口上。你想让这个 Web 服务器也能通过标准端口对外部世界开放。你使用的命令是：

```
ipmasqadm portfw -a P tcp -L MYip port 80 -R 192.168.1.14 80
```

假设 `iptchains` 已经启用了内部网络的伪装以及该接口和端口的入站 TCP 连接，这就是启用将 80 端口转发到 192.168.1.14 的 80 端口所需的全部命令。

## 整合一切

为了让情况更清晰，让我们把目前为止所做整合在一起。列表 10.1 显示了一个使用了我们目前为止创建的所有规则的示例 bash 脚本。

## 使用 ipchains 进行防火墙路由

### 列表 10.1 示例 ipchains 脚本

```
#!/bin/bash

## 清除所有现有规则

ipchains -F

## 修改以反映你的网络

INTERNAL=eth1

EXTERNAL=eth0

## 在此处添加你的 IP 地址

MYIP=

# 如果适用，在此处添加你的内部网络加掩码

INT=192.168.1.0/24

## 如果适用，在此处添加你的服务器的地址

WEB=192.168.1.14

## 在 /etc/resolv.conf 中查找别名；允许查询

for DNS in $(grep 'names' /etc/resolv.conf|awk '{print $2}'); do

ipchains -A input -p UDP -s DNS domain \
  -j ACCEPT

ipchains -A input -p TCP -s DNS domain \
  -j ACCEPT

done

## 同样允许 ping 响应

ipchains -A input -p ICMP -s 0/0 echo-reply \
  -d $MYIP -j ACCEPT

## 允许文件传输的活动 ftp-data 连接

ipchains -A -p TCP -s 0/0 ftp-data \
  -d $MYIP 1024:5999 -j ACCEPT

ipchains -A input -p TCP -s 0/0 ftp-data \
  -d $MYIP 6255:-j ACCEPT

## 允许我们发起的其他 TCP 连接

ipchains -A input -p TCP ! -y -j ACCEPT

# 拒绝所有不是环回地址的内容

ipchains -A input -i !lo -p ICMP -j DENY -1

## 现在，如果有必要，启用伪装

if [ "$INT" != "*" ]; then

echo 1 >/proc/sys/net/ipv4/ip_forward

ipchains -A input -i $INT -s $INT -j ACCEPT

ipchains -A forward -s $INT -j MASQ

ipchains -A forward -j DENY -1

fi
```

### 列表 10.1 继续

```
## 并设置转发到我们 Web 服务器的端口

if [ "$WEB" = "" ]; then

nipchains -A input -d WEB -s 0/0 www -p TCP -j ACCEPT

ipmasquad portfw -a p tcp -L $MYIP 80 \
  -R WEB 80

fi

## 脚本结束
```
