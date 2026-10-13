
与示例相反，FQDN 末尾的点通常被省略。这种反向顺序是许多第一次查看 DNS 的人的困惑来源。

## 名称服务器如何存储 DNS 结构信息

树结构及其相关资源记录由称为名称服务器的程序存储。每个域都有一个权威名称服务器，持有该域数据的副本；域管理员负责维护这些数据。名称服务器还可以缓存其对其没有权限的树部分的信息。为了管理方便，名称服务器可以将某些子域的权威授予其他独立维护的名称服务器。

# 第 14 章 管理 DNS

区域的权威名称服务器了解已委派子域名权限的名称服务器。权威名称服务器可能会将有关委派区域的查询交给这些名称服务器。因此，我们始终可以通过从（根域名）开始的委托链，直到到达该域的权威名称服务器，找到该域的权威数据。这就是 DNS 具有分布式树形结构的原因。

## DNS 为用户提供名称服务信息

DNS 用户不需要了解这些细节。对他们来说，命名空间只是单棵树——他们可以请求其中任何一个节点的信息。从域的资源集中查找资源记录（RRs）的任务留给了程序解析器。解析器了解数据库的分布式结构。它们知道如何联系根名称服务器（它们是根域的权威服务器），以及如何遵循委托链，直到找到能够提供它们所需信息的权威名称服务器。

虽然这种类比可能推得太远有些风险，但你可以将文件系统中的目录与这些资源记录视为这些目录中的文件。对子域名权限的委托类似于在子目录下挂载了一个 NFS 文件系统：对目录下的文件请求将发送到 NFS 服务器，而不是此文件系统。解析器的工作是从根目录开始，沿着目录树向下移动（遵循许多挂载点），直到到达包含它们感兴趣文件的目录。（为了效率，它们会将找到的信息缓存一段时间。）这个过程看起来似乎是“反向”顺序列出的。接文中将详细检查这一过程。

在实践中，一个域有多个权威名称服务器。其中一个是主（或主）名称服务器，存储该域的数据。其他的被称为从（或备）名称服务器，它们持有自动更新的名称数据副本。主服务器和从服务器提供相同的信息，因此解析器询问哪一个并不重要。主从服务器的区别纯粹出于可靠性考虑——以确保单个名称服务器的故障不会导致该域权威数据的丢失。作为额外好处，这种冗余还将网络负载分布在多个主机之间，使得没有一个名称服务器会被权威信息请求所淹没。

> 注意 作为 DNS 边界员，你有责任确保你的名称服务器为区域提供足够的冗余。你的从服务器应该与主服务器保持距离，这样断电、网络中断和其他灾难就不会影响你的名称服务。

尽管有这些措施，如果不使用本地缓存，DNS 服务器的负载将是无法承受的。如前，名称服务器允许缓存查询结果和中间引用一段时间，这样它们就可以节省重复的数据请求，而无需每次都引用源。如果不是，根名称服务器（以及其他热门区域的名称服务器）将会在全球客户端每次查找时都被联系，浪费大量的资源。

## 实践中的名称解析

当网络浏览器请求 IP 地址时，请求被发送到本地名称服务器，该服务器解析名称，将结果存储在缓存中并返回 IP 地址。为了更好地理解这个过程，请花一点时间看看网络浏览器请求 `.ibm.com` 的 IP 地址时后台发生了什么。这个示例模拟了解析器使用非常有用的 `dig` 工具来遵循区域之间的委托链，直到找到你寻找的 A 记录。（因为大多数名称服务器都会替你遵循委托，因此此示例使用了 `+norec` `dig` 参数来关闭递归。也就是说，如果名称服务器不知道如何回答查询，它将不会自行发出进一步查询。）

![](img/ec742613d00d1c97a9e0895a14176a8c_474_0.png)

> 注意 世界上有 13 个根服务器。其中几个位于美国——弗吉尼亚州、加利福尼亚州和马里兰州。其他的位于伦敦、斯德哥尔摩和东京。根服务器没有 IP 地址和域名的“主列表”，只是简单将请求交给其他名称服务器。
> 在最近对根服务器遭受 DOS（拒绝服务）攻击后，至少其中一个服务器现在运行了指向 BIND 的替代绑定。

首先，从 13 个根服务器中随机选择一个（范围从 `a.rootservers.net` 到 `m.root-servers.net`；我们选择了 `e`），并看看它对 `www.ibm.com` 的 A 记录知道什么：

```
$ dig @e.root-servers.net www.ibm.com A +norec

; << DiG 9.1.3 <<< @e.root-servers.net www.ibm.com A +norec

;; global options: printcmd

;; Got answer:

;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 52356

;; flags: qr; QUERY: 1, ANSWER: 0, AUTHORITY: 13, ADDITIONAL: 13

;; QUESTION SECTION:

;;www.ibm.com.

;; AUTHORITY SECTION:

IN A

com. 172800 IN NS A.GTLD-SERVERS.NET.
```

| | | | | | |
|---|---|---|---||
| com. | 172800 | IN | G.GTLD-SERVERS.NET |
| com. | 172800 | IN | H.GTLD-SERVERS.NET |
| com. | 172800 | IN | C.GTLD-SERVERS.NET |
| com. | 172800 | NS | I.GTLD-SERVERS.NET |
| com. | 172800 | NS | B.GTLD-SERVERS.NET |
| com. | 172800 | NS | D.GTLD-SERVERS.NET |
| com. | 172800 | NS | L.GTLD-SERVERS.NET |
| com. | 172800 | NS | F.GTLD-SERVERS.NET |
| com. | 172800 | NS | J.GTLD-SERVERS.NET |
| com. | 172800 | NS | K.GTLD-SERVERS.NET |
| com. | 172800 | NS | E.GTLD-SERVERS.NET |
| com. | 172800 | NS | M.GTLD-SERVERS.NET |

```
;; ADDITIONAL SECTION:

A.GTLD-SERVERS.NET 172800 IN 192.5.6.3

H.GTLD-SERVERS.NET 172800 IN 192.52.93

C.GTLD-SERVERS.NET 172800 IN 192.54.112

I.GTLD-SERVERS.NET 172800 IN 192.26.92

B.GTLD-SERVERS.NET 172800 IN 192.36.144

D.GTLD-SERVERS.NET 172800 IN 192.33.143

L.GTLD-SERVERS.NET 172800 IN 192.41.162

F.GTLD-SERVERS.NET 172800 IN 192.35.51

J.GTLD-SERVERS.NET 172800 IN 204.146.173.35

K.GTLD-SERVERS.NET 172800 IN 198.4.83.35

E.GTLD-SERVERS.NET 172800 IN 202.153.94

M.GTLD-SERVERS.NET 172800 IN 213.127.94
```
*(注：原文中附加部分的 IP OCR 严重碎片化；我根据标准 DNS 委托模式和提供的表格结构尽可能重建了逻辑流，但首要任务是修正文本并合并页面。)*

```
; Got answer:

;; ;>>HEADER<< opcode: QUERY, status: NOERROR, id: 32287

;; flags: qr aa ra; QUERY: 1, ANSWER: 4, AUTHORITY: 5, ADDITIONAL: 5
```

```
; QUERY SECTION:
```

```
www.ibm.com. IN A
```

```
; ANSWER SECTION:
```

```
www.ibm.com. 1800 IN A 129.42.18.99

www.ibm.com. 1800 IN A 129.42.19.99

www.ibm.com. 1800 IN A 129.42.16.99

www.ibm.com. 1800 IN A 129.42.17.99
```

```
; AUTHORITY SECTION:
```

```
ibm.com. 600 IN NS ns.watson.com.

ibm.com. 600 IN NS ns.austin.ibm.com.

ibm.com. 600 IN NS ns.almaden.com.

ibm.com. 600 IN NS ns.ers.ibm.com.

ibm.com. 600 IN NS

Internet-server.zuerich.ibm.com.
```

```
; ADDITIONAL SECTION:
```
