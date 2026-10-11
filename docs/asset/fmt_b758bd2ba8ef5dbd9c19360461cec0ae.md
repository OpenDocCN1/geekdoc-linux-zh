
一如往常一样，一旦创建了访问列表，我们必须使用与 IP 列表相同的命令将其应用到接口上：

```
Corp(config)#ip access-group 110 in
或者：
Corp(config)#ip access-group 110 out
```

## 扩展访问列表 #2

```
Lab_A(config)#access-list 110 deny tcp host 172.16.50.5 eq 21
Lab_A(config)#access-list 110 deny tcp host 172.16.50.5 eq 23
Lab_A(config)#access-list 110 permit ip any any
Lab_A(config)#int fa0/1
Lab_A(config-if)# access-group 110 out

Router(config)#access-list 110 deny tcp host 172.16.48.0 0.0.0.255 eq 25
Router(config)#access-list 110 deny tcp host 172.16.192.0 0.0.0.255 eq 23
Router(config)#access-list 110 permit ip any any
Router(config)#interface Ethernet 1
Router(config-if)# access-group 110 out
Router(config)#interface Ethernet 2
Router(config-if)# access-group 110 out
```

仅允许来自源 B 财务服务器的 HTTP 访问。所有其他流量都将被允许。我们可能需要在三个测试语句中配置此内容：

```
Lab_A(config)#access-list 110 permit tcp host 192.168.17.22 172.22.89.26 eq 80
Lab_A(config)#access-list 110 deny tcp host 172.22.89.26 eq 80
Lab_A(config)#permit ip any any
Lab_A(config)#interface fastethernet 0/1
Lab_A(config-if)# access-group 110 out

webserver
access-list 253 permit tcp 172.16.5.0 0.0.0.255 eq any <-- 允许 172.16.5.* 访问任何人的端口
```

## 命名列表 - 以 "ip access-" 开头

```
Lab_A(config)#ip access-list standard BlockSales
Lab_A(config-std-nacl)#deny 172.16.40.0 0.0.0.255
Lab_A(config-std-nacl)#permit any
Lab_A(config-std-nacl)#exit
Lab_A(config)#int fa0/1
Lab_A(config-if)#ip access-group BlockSales
```

## 添加注释

```
R2(config)#access-list 110 remark Permit Bob from Sales To Finance
R2(config)#access-list 110 permit 172.16.40.1 172.16.50.0 0.0.0.255
R2(config)#access-list 110 deny 172.16.40.0 0.0.0.255 172.16.50.0 0.0.0.255
R2(config-ext-nacl)#remark Deny all of lists from Telnet
R2(config-ext-nacl)#No_Telnet
R2(config-ext-nacl)#deny tcp eq 23 172.16.40.0 0.0.0.255 172.16.50.0 0.0.0.255
R2(config-ext-nacl)#permit any
```

添加一条：

```
Lab_A(config)#show access-list
Extended IP access list 110
10 deny tcp host 172.16.30.5 eq ftp
20 deny tcp host 172.16.30.5 eq telnet
30 permit ip any
40 permit ip host 192.168.17.22 172.22.89.26 eq www
50 deny tcp host 172.16.22 eq www
Lab_A(config-ext-nacl)#permit
```

- `show access-list` - 显示所有访问列表及其参数。不显示接口。
- `show access-list 110` - 显示 `110` 的参数。不显示接口。
- `show ip access-list` - 显示访问列表。
- `show interfaces` - 显示应用了 ACL 的接口。
- `show running-config` - 显示应用了 ACL 的特定接口。

记住：你不能同一个接口上使用两个方向的列表；一个会覆盖另一个。

此扩展 ACL 用于允许 `10.1.1` 网络（入站）流量，并从外部接收未经请求的 ping。

```
interface Ethernet0/1
ip address 172.16.1.2 255.255.255.0
ip access-group 101 in
access-list 101 deny icmp any 10.1.1.0 0.0.255
access-list 101 permit ip any 10.1.1.0 0.0.255
```

注意：某些应用需要 keepalive 功能。如果是这样，你可能需要更细粒度的允许/拒绝 IP。

## OSPF 链路状态路由 - Dijkstra 算法

```
Central1(config)#interface loopback 0
Central1(config-if)# address 172.31.1.1 255.255.255
Central1(config)#router ospf 1
Central1(config-router)#network 10.10.0 0.0.0.0 area 0
Central1(config-router)#network 172.16.10.0 0.0.0.3 area 1 <-- 此掩码是 255 减去字节（此处为 252）
Central1(config-router)#network 172.16.10.0 0.0.3 area 2
Central1(config-if)#interface fa0/0 <-- 接口上应该发现邻居
```

为网络拥有默认路由，并传播到其他路由器。

```
Central1(config)#route 0.0.0.0 0.0.0.0 Fa0/0
Central1(config)#router ospf 1
Central1(config-router)#default-information-originate
```

## OSPF 中的 Loopback 和 RID

如果没有配置 loopback，路由器启动时最高的活动地址将成为路由器的 RID。Loopback 接口不会覆盖 `router-id`，不需要重启路由器即可生效。

1. 活动接口上的最高 IP
2. 逻辑接口（loopback）覆盖物理接口。
3. `router-id` 覆盖接口和 loopback 接口。

重启或使用 `clear ip ospf` 命令强制生效。

## IPv6 OSPF 路由 - 路由也附加到接口上。

```
Central1(config)#int f0
Central1(config-if)# ipv6 ospf 1 area 0
Central1(config)#ipv6 router 1
Central1(config-rt)#ipv6 route 1.1.1.1
Central1(config-rt)#do clear ip ospf
```

IPv6 RID 仍然存在 - 在全局配置的 OSPF 进程 ID 下：

```
ipv6 router 1
```

## 指定路由器 Designated Routers

- 默认情况下，所有 OSPF 路由器的优先级均为 `1`。
- 选举根据路由器优先级级别、最高 RID（如果是最高 IP 地址）进行。
- 备用指定路由器 `BDR` 是 `DR` 的备份者，`DR` 的备机。
- 接收所有更新但不分发；当 `DR` 下线时接替。

假设想要 `R1` 成为 `DR`，`R2` 成为 `BDR`。
