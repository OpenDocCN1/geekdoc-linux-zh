

# 402 第 8 章 · DNS 的攻击与防御

## 图 8.3 www.cia.gov 的权威路径

![](img/729efc56f204a2ebffb8295c3a2dfdfb_426_0.png)

为了方便域名使用，初始的点（dot）在日常中使用是被隐藏的，如果查询中不包含该点，通常假设它是隐藏的。执行包含不必要的点的 DNS 查询有时可以被用于信息泄露。只有在常见的管理实践或根服务器故障排除的原理证明（POC）中，查询中才会出现初始点。

图 8.3 显示的域名层次结构展示了权威是如何组织的。点是符号意义上的起点，由 13 台物理根服务器控制（见图 8.4）。与认知相反，这 13 台“服务器”实际上是许多负载均衡机器的集群。

所有根服务器（见表 8.3）均由独立实体拥有和运营，以最大限度地减少单点故障，唯一的例外是 A 和 J 根服务器。这两台服务器由 VeriSign 位于并运营，该公司还控制着所有 13 台根服务器和根服务器 IP 的中心权限。由于 2002 年 10 月 21 日晚上发生的半分布式拒绝服务（DDoS）攻击，根服务器 J 在 15 天后移动到了一个“秘密”物理位置。

www.synergy.com

**图 8.4** 根服务器的物理位置（图片感谢 ICANN©）
[www.icann.org)

## 根服务器地图

![](img/729efc56f204a2ebffb8295c3a2dfdfb_427_0.png)

注意

据传，根服务器 J 的秘密位置位于根服务器 A 的街对面。虽然物理位置可以防止现实世界中的灾难，但根服务器 A 和 J 一直通过独立的网络连接保持着事实上的隔离状态。

### 表 8.3 全球根服务器

| 根服务器 | 运营实体 | 物理位置 | IP 地址 |
|---|---|---|---|
| A | VeriSign Global Registry Services | 美国弗吉尼亚州赫尔登 | 198.41.0.4 |
| B | Information Sciences Institute | 美国加利福尼亚州马里纳德雷 | 128.9.0.107 |
| C | Cogent Communications | 美国弗吉尼亚州赫尔登 | 192.33.4.12 |
| D | University of Maryland | 美国马里兰州大学公园 | 128.8.10.90 |
| E | NASA Ames Research Center | 美国加利福尼亚州山景 | 192.203.230.10 |
| F | Internet Software Consortium | 美国加利福尼亚州帕洛奥托；美国加利福尼亚州旧金山 | IPv4: 192.5.54.241<br>IPv6: 2001:500::1035 |
| G | U.S. DOD Network Information Center | 美国弗吉尼亚州维也纳 | 192.112.36.4 |
| H | U.S. Army Research Lab | 美国马里兰州阿伯丁丁 | IPv4: 128.63.2.53<br>IPv6: 2001:500::1:803 |
| I | Autonomica | 瑞典斯德尔摩 | 192.36.148.17 |
| J | Verisign Global Registry Services | 美国弗吉尼亚州赫尔登 | 192.58.8.30 |
| K | Resaux IP Europeans - Network Coordination Centre | 英国伦敦 | 193.0.14.129 |
| L | Internet Corporation for Assigned Names and Numbers | 美国加利福尼亚州洛杉矶 | 198.32.64.12 |
| M | WIDE Project | 日本东京 | 202.12.27.33 |

如果你理解了全球 DNS 的初始足迹，就可以进行下一步：从左到右查看域名地址，初始点之后是顶级域名（TLD），它大致分为三大类（见表 8.4）。

### 表 8.4 TLD 类型

| TLD | 说明 | 域名 |
| :--- | :--- | :--- |
| gTLD | 通用顶级域名 | 表 8.5。 |
| ccTLD | 国家代码顶级域名 | 包括 240 个基于国际标准（ISO）国家代码的“国家代码”域名（完整列表可在 www.iana.org/cctld/cctld-who.htm找到）。 |
| .arpa | 用于技术基础设施目的 | 此基础设施 TLD 用于反向 DNS 和根服务器。 |

![](img/729efc56f204a2ebffb8295c3a2dfdfb_428_0.png)

大多数通用顶级域名（gTLD）是 1995 年颁发的原始 TLD。多年来，在理由获得批准后，增加了许多 TLD 条目。见表 8.5 的已添加的 TLD 列表。

### 表 8.5 通用 TLD

| gTLD | 引入时间 | 目的 | 运营方 |
|---|---|---|---|
| .aero | 2001 | 航空运输业 | Societe Aeronautiques (SITA) |
| .biz | 2001 | 商业 | NeuLevel |
| .com | 1995 | 无限制（但用于商业注册者） | VeriSign, Inc. |
| .coop | 2001 | 合作社 | Dotoperation LLC |
| .edu | 1995 | 美国教育机构 | EDUCAUSE |
| .gov | 1995 | 美国政府 | Afisa |
| .info | 2001 | 无限制使用 | Internet Assigned Authority |
| .int | 1998 | 国际条约 | U.S. DoD Domain Management (Dom) |
| .mil | 1995 | 美国军事 | Global Name Registry |
| .museum | 2001 | 博物馆 | Public Interest Registry, Inc. |
| .name | 1995 | 无限制（但用于网络提供商等） | VerSign Global Services 直到2002年底 |
| .pro | 2002 | 会计师和其他专业人士 | RegistryPro, LTD |

![](img/729efc56f204a2ebffb8295c3a2dfdfb_429_0.png)

在 TLD 中，委托授权是有效的。TLD 并不总是由根服务器提供，它们通常托管在接收根服务器授权的 TLD 系统上。可以通过 `dig` 获取特定 TLD 的列表。例如，如果你想知道哪些服务器托管 .mil TLD，可以运行以下命令：

```
[specialops]# dig mil. NS

```

```
DIG 9.2.1 mil. NS
;; global options:
;; Got answer:
;; --HEADER<< opcode: query, status: NOERROR, id: 50277
;; flags: qr ra; QUERY: 1, ANSWER: 11, ADDITIONAL: 11
```

```
; QUESTION SECTION:
mil. IN NS
```

```
; ANSWER SECTION:
mil. 86151 IN NS CON1.NIPR.mil.
mil. 86151 IN NS B.ROOT-SERVERS.NET.
mil. 86151 IN NS A.ROOT-SERVERS.NET.
mil. 86151 IN NS EUR1.NIPR.mil.
mil. 86151 IN NS PAC1.NIPR.mil.
mil. 86151 IN NS H.ROOT-SERVERS.NET.
mil. 86151 IN NS G.ROOT-SERVERS.NET.
mil. 86151 IN NS CON2.NIPR.mil.
mil. 86151 IN NS EUR2.NIPR.mil.
mil. 86151 IN NS E.ROOT-SERVERS.NET.
mil. 86151 IN NS PAC2.NIPR.mil.
```

```
; ADDITIONAL SECTION:
CON1.NIPR.mil. 172551 IN A 199.252.175.234
B.ROOT-SERVERS.NET. 154404 IN A 128.9.0.107
A.ROOT-SERVERS.NET. 154404 IN A 198.41.0.4
EUR1.NIPR.mil. 172551 IN A 199.252.154.234
PAC1.NIPR.mil. 172551 IN A 199.252.180.234
H.ROOT-SERVERS.NET. 154404 IN A 128.63.2.53
```

```
G.ROOT-SERVERS.NET. | 154404 | IN | A | 192.112.36.4
| CON2.NIPR.mil. | 172551 | IN | A | 199.252.173.234
| EUR2.NIPR.mil. | 172551 | IN | A | 199.252.143.234
| E.ROOT-SERVERS.NET. | 154404 | IN | A | 192.203.230.10
| PAC2.NIPR.mil. | 172551 | IN | A | 199.252.155.234
```

```
; Query time: 18 msec
;; SERVER: 207.20.85.63(207.20.85.66)
;; WHEN: Sun Jan 5 17:11:31 2003
;; MSG SIZE rcvd: 412
```

你可以看到 .mil TLD 分布非常均匀。然而，并不是所有 TLD 都能满足国防信息局（DISA）要求的可靠性。许多新的 TLD 还没有变得壮大，正如 .info TLD 所示：

```
[specialops]# dig info. NS
```

```
<< DIG 9.2.1 info. NS
;; global options:
printcmd
;; Got answer:
;; --HEADER<< opcode: QUERY, status: NOERROR, id: 18402
;; flags: qr ra da QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 2
```

```
; QUESTION SECTION:
IN NS
```

```
; ANSWER SECTION:
info. | 85916 | IN | NS | tld2.ultradns.net
info. | 85916 | IN | NS | tld1.ultradns.net.
```

```
; ADDITIONAL SECTION:
tld2.ultradns.net. | 124154 | IN | A | 204.74.113.1
tld1.ultradns.net. | 124154 | IN | A | 204.74.112.1
```

```
; Query time: 16 msec
```

