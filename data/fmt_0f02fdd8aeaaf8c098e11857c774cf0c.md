
# 激活环回接口

```bash
/sbin/ifconfig lo 127.0.0.1
```

# 设置路由

```bash
/sbin/route add -net 127.0.0.0
```

列表 13.1 环回接口的初始化。

列表 13.2 显示了以太网卡的配置。如果电脑连接到令牌环网（`TokenRing`），则必须指定 `tr0` 而不是 `eth0`。这不仅激活了接口，还通过建立相应的路由确保了计算机的可访问性。指标值（`metrics`）指示这些路由的“成本”，因此在互联网上可以选择一条经济的路由。

```bash
# 激活以太网接口

/sbin/ifconfig eth0 `IPADDR` broadcast `$BROADCAST` \netmask `$NETMASK`

# 设置路由

/sbin/route add -net `$NETMASK` default `$GATEWAY` metric 1
```
