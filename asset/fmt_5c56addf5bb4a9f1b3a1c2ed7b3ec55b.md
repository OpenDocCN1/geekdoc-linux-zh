
传感器网络安全协议 [40] 由了一组针对高度资源受限的传感器网络优化的安全协议组成。`SPINS` 由两个主要模块组成：传感器网络加密协议（`SP`）和定时、高效、流、容错认证协议的微型版本（`μTESLA`）。`SNE` 提供数据认证、防止重放攻击的保护以及语义安全性，每条消息的通信开销为八字节。语义安全性意味着攻击者无法通过查看同一明文的多个加密版本来获取关于明文的任何信息。明文的加密使用共享秘密（发送者和接收者之间共享）。因此，同一条消息在不同的时间被加密。消息的完整性和机密性通过消息认证码（`MAC`）维持。这类似于使用秘密密钥认证方案从消息中得出的校验和。消息还携带了时间戳实例的计数值（类似于时间戳），以防止重放攻击。`μTESLA` 确保了认证广播，即接收数据包的节点可以确保其发送者的身份。它要求节点之间存在松散的时间同步，且最大同步误差有上限。`MAC` 密钥派自密钥链，通过应用单向函数 $F$（逆函数不易计算的单向函数）获得。所有节点都有一个初始密钥 $K_0$，它是密钥链中的某个密钥。密钥之间的关系遵循 $K_1=F(K_0)$，$K_2=F(K_1)$，而对于 $K_i=F(K_i)$，无法计算出 $K_{i+1}$。使用的密钥定期更换，由于节点同步到允许误差范围内的共同时间，它们可以在任何时间检测到使用哪个密钥来加密/解密数据包。基站定期向所有节点公布下一个密钥延迟，这个周期对所有节点都是已知的。在用于加密的密钥与其向所有接收者公布之间，还存在特定的时间间隔延迟。当基站传输数据包时，它使用一个仍然秘密（尚未公布）的 `MAC` 密钥。节点接收此数据包并将其缓存，直到适当的验证密钥公布。但是，数据包一接收到，就会检查 `MAC` 以确保在 `MAC` 中使用的密钥尚未公布，这意味着只有基站知道尚未公布的密钥可能发送了该数据包。一旦从基站接收到密钥公布包，数据包就会被解密。如果错过了其中一个密钥公布包，数据包将缓存到下一个时间间隔，然后进行认证。例如，假设 $K_j$ 的公布包没有到达节点；它将等待直到接收到 $K_{j+1}$，然后计算 $K_j=F(K_{j+1})$ 并解密在上一个时间间隔接收的数据包。

### 12.9.5 实时通信

对实时通信的支持对于用于监控或安全关键型系统的传感器网络至关重要。感知与采取适当行动之间的通信延迟会极大影响监控系统的质量。同样，在核电厂，温度或压力的异常检测必须实时传给控制系统。因此，路由的延迟保证对于此类系统非常有用。本节将讨论两种支持传感器网络实时通信的协议——`SPEED` 和 `RAP`。

### SPEED

一种支持传感器网络实时通信的无状态协议 `SPEED` 已在 [41] 中提出。

`SPEED` 是一种局部算法，提供实时单播、实时多播（向特定区域的所有节点多播），且不需要数据传输的支持。`SPEED` 的开销极小，因为它不需要路由表。这在尽力传输的 `MAC` 层是可能的，不需要特殊的 `MAC`。它还通过非确定性转发在网络分布流量和负载。

该协议需要邻居之间的定期信标。它还使用按需信标用于延迟估计和拥塞（背压）检测。这些用于适应网络的变化。节点的负载通过单跳延迟进行估算。测量是通过通过节点的数据包进行的，而不是单独的数据包。这最小化了开销。节点还会响应延迟估计以告知邻居估计延迟。数据包路由通过无状态非确定性地理转发（`SNGF`）执行。利用地理信息，数据包仅转发到靠近目的地的节点。在候选节点中，估计延迟最小的节点被选择中间节点的概率更高。如果没有满足延迟限制的节点，数据包将被丢弃。

`SPEED` 使用邻居反馈环（`NFL`）来不断维护估计延迟，因此不需要频繁更新估计值。当数据包必须丢弃时，说明没有满足延迟限制的路径，减少到下游节点（更靠近接收者的节点）的压力率以避免拥塞，从而维持延迟。`NFL` 发布背压信标以指示平均延迟。增加的延迟会被注意到，`NFL` 据此减少选择拥塞节点进行路由的概率，直到拥塞缓解并减少。这可以递归进行，将背压从下游传播到上游节点（更靠近发送者的节点），以缓解热点的拥塞。

许多路由算法可能会遇到没有靠近目的地的节点可以转发数据包的情况。这被称为“空洞（void）”。`SPEED` 通过发布估计延迟为无限的背压使用空洞回避技术。这将触发对替代路径的搜索。在这里，如果存在任何满足延迟限制的路径，它将被检测到。

由 `SPEED` 开发。该协议通过提供最大延迟保证，为传感器网络上的实时通信提供了支持。

# RAP

`RAP` [42] 为应用程序提供了处理查询的 `API`。基站（`BS`）中的应用层程序可以指定的事件信息类型、查询目标区域以及获取信息的截止日期。`RAP` 的底层层确保查询被发送到指定区域内的所有节点，并将结果传回基站。`RAP` 协议栈由传输层的位置地址协议（`LAP`）、用于地理路由协议的速率单调调度算法（`VMS`）以及支持优先划分的基于竞争的 `MAC` 方案组成。

`RAP` 是一种无连接的传输协议，它使用位置来寻址节点，而不是像 `IP` 地址那样唯一的寻址方案。它支持三种通信方式：单播、区域多播和区域任播。`VMS` 基于“数据包请求速度”的概念，该概念同时反映了时间限制和距离限制。因此，请求速度是数据包紧急程度的衡量标准。如果一个数据包能够以其请求速度传输（即在指定时间内覆盖该距离），那么它就能满足截止日期。`VMS` 给具有请求速度的数据包赋予更高的优先级。数据包的速度计算为发送者与接收者之间的地理距离与截止日期的比值。动态 `VMS` 在每个中间节点重新计算速度，因此在此之前速度慢于请求速度的数据包可以获得更高的优先级。这被映射到 `MAC` 层优先级，并由基于竞争的 `MAC` 层处理。此处的协议为需要实时支持的应用层程序提供了方便的服务。

## 12.10 总结

传感器网络实现了一个无处不在的分布式网络，以创建一个智能环境。传感器网络的可能性非常广泛，包括智能建筑、传感器控制的化工厂以及隐蔽军事行动。传感器网络的研究方向是克服可扩展性、可靠性、健壮性和能效率方面的挑战，以便在高度受限的场景中实现各种应用。

传感器节点的硬件设计需要进一步微型化，并且需要开发高效的硬件和操作系统。在 `MAC` 层，需要为传感节点的移动性做出规定。关于路由、网络建立和维护的新想法仍处于开发阶段。同样，一种功耗和计算成本有限、且能够与 `TCP` 或 `UDP` 接口的传输层协议仍在规划中。处理感知数据以及开发特定于应用的查询语言，将有助于微调传感器网络在各种应用中的性能。由于传感器网络协议栈的每一层都存在开放性问题，这是一个仍处于初始阶段但极具前景的概念。

## 12.11 问题

- 1. 自组无线网络和传感器网络之间的主要区别是什么？

- 2. 在传感器网络中，聚类架构相比于分层架构的优势是什么？

- 3. 考虑 `LEACH` 协议的第三次迭代。如果每个簇所需的节点数为十个，那么节点在生成随机数时计算出的阈值是多少？

- 4. 在传闻路由（rumor routing）的实现中，代理具有表 12.1 所示的表，从节点 $B$ 携带表 12.2 到达节点 $A$。更新后表的状态如何？

表 12.1 代理表

| 事件 | 距离 |
| :--- | :--- |
| E1 | 4 |
| E2 | 2 |

表 12.2 节点表

| 事件 | 距离 | 方向 |
| :--- | :--- | :--- |
| E1 | 3 | D |
| E2 | 3 | C |
| E3 | 3 | D |

- 5. 考虑图 12.22 所示的网络拓扑结构。顺序路由已形成以节点 $C$ 和 $D$ 为根的树。节点 $F$ 发出优先级为 2 和 3 的包。它们将通过什么路径到达汇点？

- 6. 考虑图 12.23 所示的网络拓扑结构。边上的数字表示特定跳的成本。如果汇点是 $D$，请展示代价场（cost-field）方法确定最优路径的逐步步骤。

![](img/9a644da879f5b6931b062d2fa3b8e81a_712_0.png)

- 距离汇一点跳
- 以节点 C 为根的树
- 以节点 D 为根的树

**图 12.22.** 问题 5 的网络拓扑结构。

![](img/9a644da879f5b6931b062d2fa3b8e81a_712_1.png)

**图 12.23.** 问题 6 的网络拓扑结构。

## 12.11 节 问题

7. 节点 A 和 B 之间提供三条路径，如图 12.24 所示。每条链路上的数字表示链路的（能量，延迟）。如果采用代价场方法进行路由，当使用的指标为 (a) 能量、(b) 延迟和 (c) 能量 × 延迟时，将选择哪条路径？

![](img/9a644da879f5b6931b062d2fa3b8e81a_713_0.png)

图 12.24 问题 7 的网络拓扑结构。

8. 考虑图 12.25 所示的网络拓扑结构。边上的数字表示特定跳的成本。如果汇点是 $D$，请展示代价场方法确定最优路径的逐步步骤。

![](img/9a644da879f5b6931b062d2fa3b8e81a_713_1.png)

图 12.25 问题 8 的网络拓扑结构。

9. 节点 A 和 B 之间提供三条路径，如图 12.26 所示。每条链路上的数字表示链路的（能量，延迟）。如果采用代价场方法进行路由，当使用的指标为 (a) 能量、(b) 延迟和 (c) 能量 × 延迟时，将选择哪条路径？

10. 考虑图 12.27 所示的网络拓扑结构。边上的数字表示特定跳的成本。如果汇点是 $D$，请展示代价场方法确定最优路径的逐步步骤。

# 694

## 参考文献

[10] S. Ratnasamy 等人，`GHT: A Geographic Hash Table for Data-Centric Storage, Proceedings of ACM Workshop on Wireless Sensor Networks and Applications 2002`, pp. 78-87, 2002年9月。

[11] I. Stoica, R. Morris, D. Liben-Nowell, D. Karger, M. F. Kaashhoek, F. Dabek 和 H. Balakrishnan，`Chord: A Scalable Peer-to-Peer Lookup Service for Internet Applications, Proceedings of ACM SIGCOMM 2001`, pp. 149-160, 2001年8月。

[12] B. Y. Zhao, J. Kubiatowicz 和 A. D. Joseph，`Tapestry: An Infrastructure for Fault-Tolerant Wide-Area Location and Routing, Technical Report UCB/CDS-01-1141, Computer Science Division, U. C. Berkeley`, 2001年8月。

[13] B. Karp 和 H. T. Kung，`GPSR: Greedy Perimeter Stateless Routing for Wireless Sensor Networks, Proceedings of ACM MOBOMIC 2000`, pp. 243-254, 2000年8月。

[14] L. Li 和 J. Y. Halpern，`Minimum Energy Mobile Wireless Networks Revisited, Proceedings of IEEE ICC 2001`, pp. 278-283, 2001年6月。

[15] S. Lindsay 和 C. S. Raghavendra，`PEGASIS: Power-Efficient Gathering in Sensor Information Systems, Proceedings of IEEE ICC 2001`, vol. 3, pp. 1125-1130, 2001年6月。

[16] S. Lindsay, C. S. Raghavendra 和 K. M. Sivaling，“Data-Gathering Algorithms in Sensor Networks Using Energy Metrics,” `IEEE Transactions on Parallel and Distributed Systems`, vol. 13, no. 9, pp. 924-935, 2002年9月。

[17] E. Shih, S. Cho, I. Necks, R. Min, A. Sinha, A. Wang 和 A. Chandrakasan，“Physical Layer Debris Protocol and Algorithm for Energy-Efficient Sensor Networks,” `Proceedings of ACM MOBOMIC 2001`, pp. 272-286, 2001年7月。

[18] A. Woo 和 D. Culler，“A Transmission Control Scheme for Media Access in Sensor Networks,” `Proceedings of ACM MOBOMIC 2001`, pp. 221-235, 2001年7月。

[19] K. M. Sivaling，“On Wireless Sensor Protocols,” `International Conference on High-Performance Computing 2002`, 印度班加罗尔，2002年12月。

[20] A. Savvides, C. Han 和 M. B. Srivastava，“Dynamic Fine-Grained Localization in Ad Hoc Networks of Sensors,” `Proceedings of ACM MOBOMIC 2001`, pp. 166-179, 2001年7月。

[21] A. Nasipari 和 K. Li，“Directionality-Based Localization Scheme for Wireless Sensor Networks,” `Proceedings of ACM Workshop on Wireless Sensor Networks and Applications 2002`, pp. 105-111, 2002年9月。

[22] Y. Wang, W. Ruml, Y. Zhang 和 M. P. J. Fromherz，“Localization from Mere Connectivity,” `Proceedings of ACM MOBIHOC 2003`, pp. 201-212, 2003年6月。

## 参考文献

[23] T. Clouqueur, V. Phipatanuasphorn, P. Ramanathan 和 K. K. Saluja，“Sensor Deployment Strategy for Target Detection,” `Proceedings of ACM Workshop on Wireless Sensor Networks and Applications 2002`, pp. 42-48, 2002年。

[24] IEEE 802.15 无线个人局域网工作组，`www.ieee802.org/15/pub/TG4.html`

[25] DARPA SensIT 程序全球时间，`http://dsn.darpa.mil/ixo/sensit`

[26] Zigbee 联盟官方网站，`www.zigbee.org/`

[27] V. Raghunathan 等人，“Energy-Aware Wireless Microsensor Networks,” `IEEE Signal Processing Magazine`, vol. 19, no. 2, pp. 40-50, 2002年3月。

[28] H. Kopetz 和 W. Schwab，“Global Time in Distributed Real-Time Systems,” `Technical Report 15/89`, 维也纳技术大学，1989年。

[29] A. Ebner, H. Rohling, R. Halmann 和 M. Loft，“Synchronization in Ad Hoc Networks Based on TDD,” `Proceedings of IEEE PIMRC 2002`, vol. 4, pp. 1650–1654, 2002年9月。

[30] J. Elson 和 D. Estrin，“Time Synchronization for Wireless Sensor Networks,” `Proceedings of IEEE IPDPS Workshop on Parallel and Distributed Computing Issues in Wireless Networks and Mobile Computing 2001`

[31] A. Ebner, H. Rohling, R. Halmann 和 M. Loft，“Synchronization in Ad Hoc Networks Based on TDD,” `Proceedings of IEEE PIMRC 2002`, vol. 4, pp. 1650–1654, 2002年9月。

[32] J. Elson 和 D. Estrin，“Time Synchronization for Wireless Sensor Networks,” `Proceedings of IEEE IPDPS Workshop on Parallel and Distributed Computing Issues in Wireless Networks and Mobile Computing`

[33] A. Ebner, H. Rohling, R. Halmann 和 M. Loft，“Synchronization in Ad Hoc Networks Based on TDD,” `Proceedings of IEEE PIMRC 2002`, vol. 4, pp. 1650–1654, 2002年9月。
