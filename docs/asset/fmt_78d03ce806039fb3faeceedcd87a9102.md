
在数据包级别审查 DNS 通可以更好地理解用于包过滤或入侵检测系统（IDSS）的正常 DNS 流量（如图1 所示）。细微的细节很容易被忘记；简单的检查清单是一个很好的提醒，并可以节省管理工作。自 20 世纪 90 年代中期互联网爆发以来，DNS 一一直是互联网不可或缺的一部分。由于向几台根服务器提供了廉价的硬件捐赠，太阳微系统在 1999 年超级碗的广告中使用了口号“我们在 'dot.com' 中加了那个点（dot）”。尽管这些广告为太阳公司带来了新的销量，但它没有提及技术背景。对新技术的需求推动了 DNS 支持大量的额外 DNS 记录。最近，新的 `AAAA` 记录随着需要被逐渐添加。多年来，主要的 DNS 技术经过了调整，以支持从虚拟私有网络（VPN）和域控制器条目到可信的公密钥基础设施（PKI）交换。主要的 DNS 结构经受了时间的考验，并在未来几年将包含在核心数据通信结构中。可以创建自定义区域记录以适应任何应用程序需求；它只是一个目前没有其他应用程序使用的记录符号。DNS 的主要目标围绕查找过程。访问网站或接收邮件的用户依赖 DNS 获取正确信息。DNS 记录用于 99% 的 Web 事务。这使得 DNS 查找过程成为互联网的基础。查找过程对于查询响应的完整性至关重要。伪造响应与根服务器授权响应之间的信任关系是区分攻击服务器与有效信任服务器的唯一标准。DNS 是那个点（.`）。所有记录权威基于从根服务器开始的信任关系，它们控制着该点。使用表 8.2 所示的区域记录图，你应该能够轻松地使用如下的 `dig` 查询。`Dig` 是 `nslookup` 的最新替代品，在基于 Unix 的系统中很常见，微软 Windows 也可用。`Dig` 按其在 DNS 数据包中的原始方式组织查找结果。DNS 数据包分为四个部分：

- `QUESTION SECTION`
- `ANSWER SECTION`
- `AUTHORITY SECTION`
- `ADDITIONAL SECTION`

`QUESTION SECTION` 显示了初始的用户查询：

```
; QUESTION SECTION:
;;www.cs.berkeley.edu. IN A
```

`ANSWER SECTION` 显示了为了答案了了服务器：

```
; ANSWER SECTION:
www.cs.berkeley.edu. 86400 IN A
hyperion.cs.berkeley.edu.
hyperion.cs.berkeley.edu. 86400 IN A 169.229.60.105
```

`AUTHORITY SECTION` 列了负责 `cs.berkeley.edu` 的服务器：

```
;; AUTHORITY SECTION:
cs.berkeley.edu.      86400 IN NS ns.cs.berkeley.edu.
cs.berkeley.edu.      86400 IN NS ns.EECS.berkeley.edu.
cs.berkeley.edu.      86400 IN NS cgl.UCSF.edu.
cs.berkeley.edu.      86400 IN NS ns1.berkeley.edu.
cs.berkeley.edu.      86400 IN NS ns2.berkeley.edu.
cs.berkeley.edu.      86400 IN NS vanogh.cs.berkeley.edu.
```

`ADDITIONAL SECTION` 显示了权威 服务器的 IP 地址：

```
;; ADDITIONAL SECTION:
ns.cs.berkeley.edu.    86400 IN A 169.229.60.61
ns.EECS.berkeley.edu. 86400 IN A 128.32.244.25
cgl.UCSF.edu.         86400 IN A 128.32.27.20
vangogh.cs.berkeley.edu. 86400 IN A 128.32.112.208
```

# 402 第 8 章 · DNS 的攻击与防御

## 图 8.3 www.cia.gov 的权威路径

![](img/729efc56f204a2ebffb8295c3a2dfdfb_426_0.png)

为了方便域名使用，初始的点（dot）在日常中使用是被隐藏的，如果查询中不包含该点，通常假设它是隐藏的。执行包含不必要的点的 DNS 查询有时可以被用于信息泄露。只有在常见的管理实践或根服务器故障排除的原理证明（POC）中，查询中才会出现初始点。

图 8.3 显示的域名层次结构展示了权威是如何组织的。点是符号意义上的起点，由 13 台物理根服务器控制（见图 8.4）。与认知相反，这 13 台“服务器”实际上是许多负载均衡机器的集群。

所有根服务器（见表 8.3）均由独立实体拥有和运营，以最大限度地减少单点故障，唯一的例外是 A 和 J 根服务器。这两台服务器由 VeriSign 位于并运营，该公司还控制着所有 13 台根服务器和根服务器 IP 的中心权限。由于 2002 年 10 月 21 日晚上发生的半分布式拒绝服务（DDoS）攻击，根服务器 J 在 15 天后移动到了一个“秘密”物理位置。

`www.synergy.com`

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
