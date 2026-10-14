

![](img/a0df85c2e542a8d6c913113908553aa4_449_0.png)

## 图 16-5：公共子网：物理视图与逻辑视图

将对客户端透明。超出本地网络的路由将仅涉及主机路由（无网络路由）。

假设你的站点没有空闲的 IP 地址。这是否意味着你不能使用集群别名？这种糟糕的情况将消除集群中更重要的功能之一。

解决方案是使用来自“虚拟子网”的 IP 地址。“虚拟子网”由与任何真实接口都无关联的 IP 地址组成。客户端将通过充当该别名路由器的集群成员来访问虚拟子网中的 IP 地址（自然由集群别名使用）。在处理高流量时，公共子网可能比虚拟子网提供更好的性能，尽管虚拟子网提供了更大的灵活性。

处理虚拟子网时的一个显著区别是，gated 通告的路由将同时是网络路由和主机路由（公共子网仅通告主机路由）。

![](img/a0df85c2e542a8d6c913113908553aa4_449_1.png)

## 图 16-6：虚拟子网：物理视图与逻辑视图

即使为子网分配了多个别名，网络路由也应每个成员通告一次。

### 注意：

你不能使用集群互连所用子网中的地址。这对公共子网别名同样适用。此外，虚拟子网中的地址不能在网络上使用。如果你选择的虚拟子网恰好是现实世界中某个真实子网，那么通用路由器不应在外部路由此子网。

使用 cluamgr 命令在子网上设置虚拟选项。

```
# cluamgr -a alias=clus_den,virtual
```

以下输出显示集群成员使用虚拟子网创建集群别名。请注意，该 IP 地址不得与真实接口关联。

```
# grep clus_den_virt /etc/hosts
192.206.126.99  clus_den_virt
```

```
# cluamgr -a alias=clus_den_virt,mask=255.255.255.0,join,virtual=t
```

```
# cluamgr -s clus_den_virt
Status of Cluster Alias: clus_den_virt
netmask: ffffff
Member Attributes:
memberid: 20, selw=1, selp=1, rpri=1 flags=31<JOINED,ENABLED,VIRTUAL>
```

集群别名路由尚未重启。请注意，路由表中有 15 个条目，ARP 缓存中没有与别名相关的任何内容。

```
# netstat -r | wc -l
15
```

```
# arp clus_den_virt
clus_den_virt (192.206.126.99) -- no entry
```

重启当前集群成员上的路由后，路由表增加了两个条目。ARP 表没有显示额外数据，因为虚拟子网不像公共子网路由那样直接依赖代理 ARP。

```
# cluamgr -r start
```

```
# arp clus_den_virt
clus_den_virt (192.206.126.99) -- no entry
```

```
# netstat -r | wc -l
17
```

```
# netstat -r

192.206.126    localhost    UG    0    0 100
clus_den_virt  localhost    UH    0    0 100
```

以下输出来自客户端节点。我们运行了 routed 守护进程，并指定它以静默模式运行（-q 不发送出站路由通告）并显示其活动跟踪（-t）。routed 守护进程与 gated 守护进程一样理解 RIP 协议。因此，在网络中混合使用 routed 和 gated 守护进程是合法的，只要两者不在同一网络节点上运行即可。输出的第一部分是标准的 routed 启动序列，它发送广播（192.168.0.255）以宣布其存在，并从自身的端口 520（192.168.0.104.520）收到回音。到目前为止，一切正常。

```
# routed -q -t

Tracing packets started Wed Sep 18 20:04:53 2002

Wed Sep 18 20:04:53:
ADD dst 127.0.0.0, router 127.0.0.1, metric 1,
flags UP state PASSIVE|INTERFACE|CHANGED|EXTERNAL timer 0
ADD dst 192.168.0.0, router 192.168.0.104, metric 1,
flags UP state INTERFACE|CHANGED timer 0
STOCADDRT: File exists
REQUEST to 192.168.0.255 0 Wed Sep 18 20:04:53:
REQUEST from 192.168.0.104.520 Wed Sep 18 20:04:53:
```

此后的 routed 跟踪发生在集群成员上发出“cluamgr -r start”命令之后。集群上的 gated 守护进程（地址为 192.168.0.69）向客户端通告了两个条目：一条网络路由，标识了当尝试访问网络 192.206.126 上的节点时与之通信的路由器；一条主机路由，标识了当尝试访问地址为 192.206.126.99 的接口时与之通信的路由器。这些条目被添加到客户端路由表中的当前信息中。

