

在 DDN 中写成

```
192.102.10.21
```

DDN 中属于五个地址类的有效 IP 地址范围如表 11.1 所示。表中给出的一些地址是特殊地址。

图 11.5 所示的互联网络通过四个路由器 R1–R4 连接四个网络。Net1 是一个 A 类网络，Net3 是一个 B 类网络，Net2 和 Net4 是 C 类网络。识别网络类别的方法是查看该网络上主机 IP 地址中最左边的十进制数字——在本例中为路由器的 IP 地址。请注意，路由器被分配的 IP 地址数量与它们连接的网络数量相同。例如，路由器 R1 连接 Net1 和 Net2，具有 IP 地址 121.1.1.1 和 192.102.10.1。同样，R3 被分配了三个 IP 地址，因为它互连了三个网络 Net1、Net3 和 Net4。

在特殊地址中，127.0.0.0（或 127.x.x.x，其中 x 可以是 0 到 255 之间的任意数字），也称为 localhost，由主机用于向自身发送数据包。它也常用于在应用程序在互联网上使用之前对其进行测试。另一个特殊地址是主机 ID 字段全为 1 的地址，即定向广播地址。该地址用于向网络上的所有主机发送数据包——即在本地网络上广播，其主机将该地址用作目标地址。

## 表 11.1 IPv4 地址类和有效 IP 地址

| 地址类 | 有效 IP 地址范围 |  |
|---|---|---|
|  | 最低 | 最高 |
| A | 0.0.0.0 | 127.255.255.255 |
| B | 128.0.0.0 | 191.255.255.255 |
| C | 192.0.0.0 | 223.255.255.255 |
| D | 224.0.0.0 | 239.255.255.255 |
| E | 240.0.0.0 | 247.255.255.255 |

![](img/02e070097d401d3bf7de4bf1c470b267_438_0.png)

图 11.5 一个由四个网络组成的互联网络，其中一个 A 类、一个 B 类和两个 C 类网络。

## 表 11.2 顶级互联网域

| 域类型 | 顶级域 | 分配给/用于 |
|---|---|---|
| 特殊 | ARPA | 专门用于互联网；目前为 second-e164.arpa、in-addr.arpa、ip6.arpa、uri.arpa、urn.arpa |
| 通用 | ACCOUNTANTS | Knob Town, LLC |
|  | ACTOR | United TLD HoldCo, Ltd. |
|  | AERO | 保留给航空运输业成员 |
|  | AIRFORCE | United TLD HoldCo, Ltd. |
|  | ARMY | United TLD HoldCo, Ltd. |
|  | ATTORNEY | United TLD HoldCo, Ltd. |
|  | BEER | Top-Level Domain Holdings Limited |
|  | BIKE | Grand Hollow, LLC |
|  | BIZ | 保留给企业 |
|  | BUILDERS | Atomic Madison, LLC |
|  | CAREERS | Wild Corner, LLC |
|  | CHRISTMAS | Uniregistry, Corp. |
|  | CHURCH | Holly Fields, LLC |
|  | COM | 保留给商业组织 |
|  | COOP | 保留给合作协会 |
|  | EDU | 保留给美国经美国教育部国家认可 accrediting 机构名单上机构认证的后中学教育机构 |
|  | GOV | 保留给美国政府 |
|  | INFO | 自 .com 以来第一个不受限制的顶级域，因此任何人——企业、营销人员等——都可以使用 |
|  | INT | 保留给政府间条约建立的组织 |
|  | MIL | 保留给美国军方 |
|  | MUSEUM | 保留给博物馆 |
|  | NAME | 保留给个人 |
|  | NET |  intended for internet service providers (ISPs) and telephone service providers |
|  | ORG |  intended for noncommercial communities but all are eligible to register |
|  | PRO |  restricted to credentialed professionals (this domain is being established) |
|  | ... |  |
|  | ZIP | Charleston Road Registry, Inc. |
|  | ZONE | Outer Falls, LLC |
| 国家代码 | AU | Australia |
|  | DE | Germany (Deutschland) |
|  | FI | Finland |
|  | JP | Japan |
|  | PK | Pakistan |
|  | ... |  |
|  | UK | United Kingdom |
|  | US | United States of America |

![](img/02e070097d401d3bf7de4bf1c470b267_441_0.png)

## 图 11.6 互联网域名层次结构的一部分。

名称系统（DNS）。DNS 实现了一个分布式的名字到地址映射数据库。一组专用主机运行名为名称服务器的服务器进程，这些进程接收来自应用程序软件（也称为客户端软件；参见第 11.7 节）的请求并协同工作，将域名映射到相应的 IP 地址。每个组织至少运行一个名称服务器，通常是 Berkeley Internet Name Domain（BIND）程序。应用程序使用 gethostname 等解析器函数来调用 DNS 服务。gethostname 解析器函数将主机名（简单或完全限定）映射到其 IP 地址，而 gethostbyaddr 将 IP 地址映射到其主机名。

一种替代的、且较旧的 DNS 服务使用方案是使用静态 hosts 文件，通常为 /etc/hosts。该文件包含域名及其 IP 地址，每行一个。以下命令显示了 Solaris 上示例 /etc/hosts 文件。

```
$ more /etc/hosts
#
# Copyright 2009 Sun Microsystems, Inc. All rights reserved.
# Use is subject to license terms.
#
# Internet host table
#
::1              localhost
127.0.0.1         localhost loghost
202.147.169.197   solarissrv
203.128.0.6       yamsrv1.ece.gatech.edu loghost
203.128.0.1       shahlami
192.168.1.1       suraj-ge0
$
```
