

Cluster member sheridan 不知道 clu_ftp_den 别名。

```
[sheridan]
# /usr/sbin/cluamgr -s all

Status of Cluster Alias: babylon5.dec.com

netmask: 0
aliasid: 1
flags: 7<ENABLED,DEFAULT,IP_V4>
connections rcvd from net: 5
connections forwarded: 5
connections rcvd within cluster: 0
data packets received from network: 1277
data packets forwarded within cluster: 174
datagrams received from network: 26
datagrams forwarded within cluster: 0
datagrams received within cluster: 28
fragments received from network: 0
fragments forwarded within cluster: 0
fragments received within cluster: 0
Member Attributes:
memberid: 1, selw=3, selp=1, rpri=1 flags=11<JOINED,ENABLED>
memberid: 2, selw=3, selp=1, rpri=1 flags=11<JOINED,ENABLED>
```

举例来说，假设你创建了一个别名，并且只有四成员集群中的三个成员实际加入该别名。当客户端使用集群别名请求 telnet/ftp/其他网络服务时，别名本身并不会固有限制其仅用于特定子集的网络服务。集群别名仅确定当网络上的客户端节点使用别名（毕竟它是一个 IP 地址）时将可能响应的集群成员列表。

图 16-7 记录了集群别名子系统所做的一些决策。端口可访问性可以通过使用 /etc/inetd.conf、/etc/inetd.conf.local、/etc/services 或 /etc/clua_services 文件来操作。

## 16.10.6 The inetd.conf.local File

为了提供对集群提供的网络服务更细粒度的控制，存在一个成员特定的 /etc/inetd.conf 文件版本，称为 /etc/inetd.conf.local。/etc/inetd.conf.local 文件提供了一种机制，使得集群中的单个成员可以有效地“关闭”其响应特定服务请求的能力。（这也可以反过来理解——也就是说，你可以集群范围内禁用所有服务，然后在适当成员的 /etc/inetd.conf.local 文件中重新启用选定的服务。）成员特定的本地文件在集群范围的 /etc/inetd.conf 文件之后读取。默认情况下，/etc/inetd.conf.local 文件的内容仅为注释（参见以下示例）。

Figure 16-7: Cluster Alias Connection Decision Tree

```
# cat /etc/inetd.conf.local
#
# ##############################################################################
#
# Internet server configuration database
#
# Description: The inetd.conf.local file is the second file that the inetd
# daemon reads for information on how to handle Internet service
# requests. It contains local services that can only
# be run on this member, and not other members, in a cluster.
# It can also be used to disable a service for this member
# by using 'disable' in the ServerPath field of a service.
#
# Precedence: Entries in inetd.conf.local will override entries in
# inetd.conf because it is read after inetd.conf.
```

![](img/a0df85c2e542a8d6c913113908553aa4_463_0.png)

```
#
# Syntax:  ServiceName  SocketType  ProtocolName  Wait/NoWait  UserName \\
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

如果我们在文件中添加以下行，则拥有此文件的集群成员将被禁止满足客户端对 telnet（或任何其他）服务的请求。

```
telnet stream tcp nowait root disable telnetd
```

上述行中的关键语法是“disable”，它将在 inetd 读取 /etc/inetd.conf 的内容之后被读取，从而在所有集群成员上启用 telnet 服务，除了在其成员特定的 /etc/inetd.conf.local 文件中包含“disable”语法的成员之外。

### NOTE:

此功能在 V5.0A 或 V5.1 中不起作用。它在 V5.1A 及更高版本中有效，但 V5.1A 的发行说明错误地指出它已损坏。（发行说明到你阅读本文时可能已被更正。）如果你仍在使用 V5.0A 或 V5.1，解决此问题的方法是从集群范围的 /etc/inetd.conf 文件中完全禁用该服务，然后在适当的成员特定的 /etc/inetd.conf.local 文件中重新启用它。

需要记住的关键点是，集群别名决定了哪些成员可以为使用该别名的客户端请求提供服务，但别名无法控制哪些服务在特定成员上可用。/etc/inetd.conf.local 文件提供了进一步确定哪些服务可从单个集群成员获得的能力。

这种额外的服务粒度控制并非免费。CLUA 在确保客户端请求最终被交付给能够完全响应的集群成员方面会付出额外的努力。例如，假设 selp 属性指示 member1 应该处理客户端对 telnet 服务的请求。进一步假设客户端使用集群别名将目标标识为集群（或集群的子集）。CLUA 子系统将基于 member1 具有最高的 selp 属性选择 member1 来处理该活动，但假设 member1 的

## Chapter 16

