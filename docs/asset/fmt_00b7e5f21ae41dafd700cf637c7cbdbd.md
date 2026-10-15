
```
#
# Syntax:  ServiceName  SocketType  ProtocolName  Wait/NoWait  UserName \
#                    ServerPath  ServerArgs
#
# ServiceName       name of an Internet service defined in the /etc/services file
# SocketType        type of socket used by the service, either stream or dgram
# ProtocolName      name of an internet protocol defined in the /etc/protocols file
# Wait/NoWait       determines whether the inetd daemon waits for
#                   a datagram server to release the socket before continuing
#                   to listen at the socket
# UserName          the login that inetd should use to start the server
# ServerPath        full pathname of the server
# ServerArgs        optional command line arguments that inetd should use to
#                   execute the server
```

如果我们在文件中添加以下行，则拥有此文件的集群成员将被禁止满足客户端对`telnet`（或任何其他）服务的请求。

```
telnet stream tcp nowait root disable telnetd
```

上述行中的关键语法是`disable`，它将在`inetd`读取`/etc/inetd.conf`的内容之后被读取，从而在所有集群成员上启用`telnet`服务，除了在其成员特定的`/etc/inetd.conf.local`文件中包含`disable`语法的成员之外。

### NOTE:

此功能在 V5.0A 或 V5.1 中不起作用。它在 V5.1A 及更高版本中有效，但 V5.1A 的发行说明错误地指出它已损坏。（发行说明到你阅读本文时可能已被更正。）如果你仍在使用 V5.0A 或 V5.1，解决此问题的方法是从集群范围的`/etc/inetd.conf`文件中完全禁用该服务，然后在适当的成员特定的`/etc/inetd.conf.local`文件中重新启用它。

需要记住的关键点是，集群别名决定了哪些成员可以为使用该别名的客户端请求提供服务，但别名无法控制哪些服务在特定成员上可用。`/etc/inetd.conf.local`文件提供了进一步确定哪些服务可从单个集群成员获得的能力。

这种额外的服务粒度控制并非免费。CLUA 在确保客户端请求最终被交付给能够完全响应的集群成员方面会付出额外的努力。例如，假设`selp`属性指示`member1`应该处理客户端对`telnet`服务的请求。进一步假设客户端使用集群别名将目标标识为集群（或集群的子集）。CLUA 子系统将基于`member1`具有最高的`selp`属性选择`member1`来处理该活动，但假设`member1`的

## Chapter 16

`/etc/inetd.conf.local` 文件。这将最终导致 CLUA 子系统根据`selp`选择下一个最佳成员。

这些决策会消耗额外的 CPU 周期。但是，一旦 TCP 连接建立，就不需要重复 CLUA 发现和路由过程。请注意，对于 UDP，由于 UDP 的无连接特性，CLUA 决策过程需要一定程度的重复。

以下输出展示了在默认`selp`和`selw`值下，集群成员作为网络服务器的正常轮询使用情况。

从客户端系统：

```
# rsh clua_den /usr/sbin/cluamgr -s clua_den | grep -E "^Status|^[Mm]ember" | more

Status of Cluster Alias: clua_den
Member Attributes:
memberid: 1, selw=1, selp=1, rpri=1 flags=11<JOINED,ENABLED>
memberid: 2, selw=1, selp=1, rpri=1 flags=31<JOINED,ENABLED,VIRTUAL>
```

```
# rsh clua_den hostname
molari.dec.com

# rsh clua_den hostname
sheridan.dec.com

# rsh clua_den hostname
molari.dec.com

# rsh clua_den hostname
sheridan.dec.com
```

如果我们更改其中一个成员（`molari`）的`selp`属性，则具有最高`selp`值的成员将始终被选中来处理来自客户端的服务请求，如下例所示。

```
[molari]
# cluamgr -a alias=clua_den,selp=2

[molari]
# cluamgr -s clua_den | grep -E "^Status|^[Mm]ember" | uniq

Status of Cluster Alias: clua_den
Member Attributes:
memberid: 1, selw=1, selp=1, rpri=1 flags=11<JOINED,ENABLED>
memberid: 2, selw=1, selp=2, rpri=1 flags=31<JOINED,ENABLED,VIRTUAL>
```

在客户端，现在的行为偏向于具有最高`selp`值的成员（`molari`）。

从客户端系统：

```
# rsh clua_den hostname
molari.dec.com
# rsh clua_den hostname
molari.dec.com
# rsh clua_den hostname
molari.dec.com
```

但如果在成员的`/etc/inetd.conf.local`文件中禁用了该服务，那么`selp`的主导地位将失去意义，如下例中成员`sheridan`收到请求所示。`kill -HUP`命令通知`inetd`配置文件已发生更改。

```
[molari]
# grep rshd /etc/inetd.conf.local
shell stream tcp nowait root disable /usr/sbin/rshd rshd
```

```
# kill -HUP 1049621
```

从客户端系统：

```
# rsh clua_den hostname
sheridan.dec.com
# rsh clua_den hostname
sheridan.dec.com
# rsh clua_den hostname
sheridan.dec.com
```

## 16.10.7 clua_services 文件

是不是开始觉得你已经掌握了 CLUA 和各种网络服务之间的关系？系好安全带——还有更多内容。还记得本章前面介绍的简洁的`/etc/services`文件吗？事实上，在集群中，CLUA 子系统使用的是`/etc/clua_services`文件。该文件的外观和感觉与`/etc/services`文件几乎相同，但它允许使用几个可以与各种服务关联的新集群属性。这些集群属性由文件开头的注释描述。
