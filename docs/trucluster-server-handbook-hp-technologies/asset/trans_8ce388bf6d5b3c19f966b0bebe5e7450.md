

REQUEST from 192.168.0.69.520 Wed Sep 18 20:19:04:
RESPONSE from 192.168.0.69.520 Wed Sep 18 20:19:09:

Wed Sep 18 20:19:09:
ADD dst 192.206.126.99, router 192.168.0.69, metric 15,
    flags UP|GATEWAY|HOST state CHANGED timer 0
ADD dst 192.206.126.0, router 192.168.0.69, metric 2,
    flags UP|GATEWAY state CHANGED timer 0

我们停止了 routed 守护进程，并使用 "routed -q" 命令在后台重新启动它，以消除重复的跟踪输出。客户端节点的路由表中包含了以下条目，这些条目是由定义了 clua_den_virt 别名的集群成员上运行的 gated 发送给它的。这两个条目都表明，sheridan（一个集群成员）是通往目的地的路径。第一个条目是网络条目；第二个条目是主机条目。

```
# netstat -r
..
192.206.126      sheridan.dec.com UG      0    0 cu0
clua_den_virt    sheridan.dec.com UGH     0    0 cu0
..
```

在接下来的序列中，客户端路由表中的主机特定条目显示了流量，但网络计数器却没有变动。主机路由优先于网络路由。

```
# rsh clua_den_virt hostname
sheridan.dec.com
# rsh clua_den_virt hostname
sheridan.dec.com
```

```
# netstat -r
..
192.206.126      sheridan.dec.com UG      0    0 tu0
clua_den_virt    sheridan.dec.com UGH     2   13 tu0
..
```

当客户端尝试访问虚拟子网上的另一个节点，而该节点目前并未在客户端路由表中以主机路由形式体现时，就会使用网络路由。这可能有助于通过一条网络通告来汇总集群中虚拟子网上的一系列集群别名。

```
# ping 192.206.126.98
PING 192.206.126.98 (192.206.126.98): 56 data bytes

----192.206.126.98 PING Statistics----
6 packets transmitted, 0 packets received, 100% packet loss
```

```
# netstat -r
192.206.126        sheridan.dec.com UG        0      6 tu0
clua_den_virt      sheridan.dec.com UGH       0     13 tu0
...
```

回到集群上，我们可以看到相应的计数器在增长。如果客户端请求的最终目的地是另一个集群成员，“转发”计数就会增加，这表明集群路由（转发）正在发生。

```
# cluamgr -s clua_den_virt
Status of Cluster Alias: clua_den_virt
netmask: ffffff
aliasid: 3
flags: 5<ENABLED,IP_V4>
connections rcvd from net: 4
connections forwarded: 0
connections rcvd within cluster: 4
data packets received from network: 22
data packets forwarded within cluster: 0
datagrams received from network: 0
datagrams forwarded within cluster: 0
datagrams received within cluster: 0
fragments received from network: 0
fragments forwarded within cluster: 0
fragments received within cluster: 0
Member Attributes:
memberid: 2, selw=1, selp=1, rp ri=1 flags=31<JOINED,ENABLED,VIRTUAL>
```

## 16.8.1 不常见，有点虚拟

如果你在《韦氏词典》中查找“virtual”一词，会看到如下定义：“在本质上或效果上存在，尽管未得到正式承认或认可”。或者你可以简化这个定义，直接说“virtual”就是“假的”。所以当我们谈论虚拟子网时，实际上是在谈论一个“假的”子网。说它假，是因为该子网上并没有真正定义任何接口。假设我们只想使用虚拟子网中的几个地址作为别名呢？

根据上一节的内容，我们可以通过在 cluamgr 命令中附加 “virtual” 或 “virtual=t” 语法，使用虚拟子网中的地址来创建别名，例如：

```
# cluamgr -a alias=clua_den_virt,mask=255.255.255.0,join,virtual=t
```

别名 clua_den_virt 对应于一个 IP 地址（192.206.126.99），该地址位于一个没有真实接口的子网上。想一想，如果我们使用完全相同的语法，但省略 “virtual=t”，那会意味着什么？这个别名不仍然是位于一个“假的”子网上吗？确实如此，但不会有到该子网的网络路由通告，只会有主机路由的通告。

