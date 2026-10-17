
lo 192.168.174.169 192.168.174.169

eth0 192.168.174.254 192.168.174.254

eth0 192.168.174.1 192.168.174.1

eth0 192.168.174.1 192.168.174.1

lo 192.168.174.255 192.168.174.255

<snip>

```

在输出中，你可以看到访问了多个目的地，但它们都在与源机器相同的子网内。如果系统执行了远程连接，它们也会出现。分析路由不仅可以让你确定访问了哪些互联网主机，还可能识别在横向移动尝试期间访问的本地网络主机。虽然 IP 地址很有用，但 DNS 名称也可以提供有用的上下文。`linux_route_cache` 的 `-R` 选项向输出添加了名称（通过 `socket-getbyaddr` Python 函数生成）。这是它的工作原理示例：

```
$ python vol.py --profile=LinuxDebian-3_x64 -f rtcache.lime linux_route_cache -R
```

| 接口 | 目的地 | 目的名称 | 网关 |
| --- | --- | --- | --- |
| lo | 127.0.0.1 | localhost | 127.0.0.1 |
| eth0 | 192.168.174.1 | | 192.168.174.1 |
| eth0 | 192.168.174.1 | | 192.168.174.1 |
| lo | 192.168.174.169 | | 192.168.174.169 |
| eth0 | 74.125.227.139 | dfw0s33-in-f5.100.net | 192.168.174.2 |
| eth0 | 192.181.132.250 | apps.pixie.yahoo.com | 192.168.174.2 |
| eth0 | 192.168.174.254 | 189.138.254 | 192.168.174.2 |
| lo | 192.168.174.255 | | 192.168.174.255 |

# 第三部分：Linux内存取证

## 分析目标

你的目标如下：

- 理解 ARP 缓存的内存存储机制：ARP 缓存存储在由列表和哈希表组成的深度嵌套数据结构中。为了维持网络操作，ARP 请求必须极快地响应，因此用于存储缓存的数据结构在搜索方面必须具有极高的效率。
- 检测横向移动：ARP 缓存提供了计算机最近分析并接触的所有系统列表。你可以通过寻找直接接触的系统，或通常情况下不会接触的子网路由器，来确定攻击者的横向移动移动。

## 数据结构

`neighbour` 结构用于表示 ARP 缓存中的一个条目：

```
>> neighbour('*)

'neighbour' (392 bytes)

0x0 : next                 ['pointer', ['neighbour']]

0x8 : tbl                  ['pointer', ['neigh_table']]

0x10 : parms               ['pointer', ['neigh_parms']]

0x18 : confirmed          ['unsigned long']

0x20 : updated            ['unsigned long']

0x28 : lock               ['__named_02ff3']

0x2c : refcnt            ['__named_038e']

0x30 : arp_queue          ['sk_buff_head']

0x48 : timer              ['timer_list']

0x98 : used               ['unsigned long']

0xc8 : probes            ['__named_038e']

0xa4 : flags              ['unsigned char']

0xa5 : nud_state          ['unsigned char']

0xa6 : type               ['unsigned char']

0xa7 : dead               ['unsigned char']

0xa8 : ha_lock           ['__named_03015']

0xb0 : ha                 ['array', 32, ['unsigned char']]

0xd0 : hh                 ['__hh_cache']

0x160 : output           ['pointer', ['void']]

0x168 : ops              ['pointer', ['neigh_ops']]

0x170 : rcu              ['rcu_head']

0x180 : dev              ['pointer', ['net_device']]

0x188 : primary_key      ['array', 0, ['unsigned char']]
```

### 关键点

关键点如下：

- `next`: 列表中的下一个 ARP 条目
- `tbl`: 指向所属 ARP 表的后向指针
- `primary_key`: 被接触机器的 IP 地址
- `ha`: 被接触机器的硬件 (MAC) 地址
- `dev`: 与缓存条目关联的接口的 `net_device` 结构，它允许恢复接口名称（如 `eth0`、`wlan1` 等）

`neigh_tables` 全局变量存储了邻居表列表。每个表都以哈希表的形式存储，其中数组索引存储了指向 `neighbour` 结构的指针。我们可以通过遍历 `next` 成员（一个列表）来列举所有的邻居节点。`linux_arp` 插件模拟了这种条目的枚举，并获取 IP 地址、MAC 地址和接口名称。以下显示了 `linux_arp` 针对 Debian 内存的输出：

```
$ vol.py --profile=LinuxDebian-3_2x64 -f debian.lime linux_arp

Volatility Foundation Volatility Framework 2.4

[:: ] at 00:00:00:00:00 on lo

[192.168.174.1 ] at 00:50:56:c0:00:08 on eth0

[192.168.174.2 ] at 00:50:56:fa:ad:55 on eth0

[192.168.174.254 ] at 00:50:56:e3:2e:81 on eth0
```
