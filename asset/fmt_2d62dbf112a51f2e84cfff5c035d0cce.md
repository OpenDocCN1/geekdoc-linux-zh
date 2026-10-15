
| Bell 追踪 | OGI 追踪 |
|---|---|
| 命中率 | 0.971 | 0.988 |
| 固有缺失率 | 0.029 | 0.012 |
| 最大缺失次数（每100 ms 间隔） | 6 | 189 |
| 缺失方差（每100 ms 间隔） | 1.3540 | 17.438 |
| 平均缺失次数（每100 ms 间隔） | 0.775 | 5.843 |

## 3.2 表格

模拟完美缓存的结果。

`OGI` 追踪捕获了一个部分活跃的半衰期游戏服务器，其特征是具有中等数量（约20个）的长寿命 `UDP` 流。

### 3.3.1 参考缓存实现

我们模拟了一个布隆过滤器 `[13]`，并使用了最优维度划分。在基准测试数据集上运行了冷分页和双缓冲老化策略。为了达到十亿分之一的分类错误概率，最优维度划分需要 30 个独立的哈希函数，这意味着每个缓存查找和插入操作都需要 30 次独立的单比特内存访问。

本章中的摘要缓存被选择为四路组式哈希表，带有 32 位流标识符位。每次查找和插入操作都需要 16 位的内存请求。由于其低复杂度和近乎最优的行为 `[10]`，我们选择了 `LRU` 缓存替换算法。

我们选择了四路组式缓存，其性能几乎等同于全交叉缓存 `[21]`。图 3.6 画了具有不同组关联性的摘要缓存的行为。

我们将我们的缓存与传统的基于四路层的 `IPv4` 和 `IPv6` 的哈希表进行了比较。每次查找和插入操作分别需要一个 512 字节或 148 字节的内存请求。

此处展示的所有结果结果的哈希处理都是使用 `SHA-1` `[26]` 哈希完成的。需要注意的是，`SHA-1` 哈希的加密强度并不是该领域内有效哈希函数的重要属性。只要它是通用哈希函数类的一员 `[27]` 即可。

## 3.3 评估

![](img/e172ff28bf6e0a7a974849165330f450_61_0.png)

在不同组关联性下，摘要缓存命中率随内存的变化（假设分类错误率为十亿分之一）。

## 3.6 图表

## 3 使用摘要缓存的高效数据包分类

### 3.3.2 结果

在评估缓存系统的性能时，我们必须考虑两个标准：我们必须检查整体命中率，以及缓存缺失率的平滑度。具有大批量缓存缺失的缓存是没用的，因为它会对数据包分类引擎造成压力。

图 3.7 画了各种缓存策略的命中率，摘要缓存的命中率等同于其大小十倍的 `IPv6` 缓存。更重要的是，摘要缓存的大缺失性能优于布隆过滤器缓存。摘要缓存产生的命中率等同于大小为 50-80% 的冷捕布隆过滤器，并优于大小为其两到三倍的双缓冲布隆过滤器缓存。

图 3.8 画了不同缓存方法的缓存缺失率方差，按每 100 ms 间隔聚合。从两条追踪中观察到，摘要缓存提供了优越的性能，使聚合缓存缺失的方差 最小化。

有趣的是，对于极小的缓存尺寸，摘要缓存表现出的命中率方差比所有其他方案都大。这可以归因于在该区间内的其他算法表现均均匀地糟糕。

随着缓存尺寸的增加，这种命中率性能得到提高，缓存缺失率的方差减少到一个非常小的数字。这是一个重要的观察，因为它意味着在这些追踪中，缓存缺失不受突发活动模式的主导。

为了考虑一个更具体的例子，我们构建了一个 2600 字节的四路组式摘要缓存。选择这个数字是为了恰好与单个 `IXP2000` 系列微引擎可用的本地内存量相。

图 3.9 展示了按每秒间隔聚合的缓存缺失率追踪。该图代表了数据包分类引擎在每秒内必须处理的数据包数量，以跟上流量负载。从图中观察，在最坏情况下，`Bell` 追踪的数据包分类引擎必须能够每秒分类约 60 个包 `pps`，而 `OGI` 追踪在最坏情况下为 260 `pps`。整个时间期间，`Bell` 和 `OGI` 追踪的平均数据包负载分别为 270.7 和 4335.4 `pps`。`Bell` 追踪的峰值数据包速率接近 1400 `pps`，而 `OGI` 追踪的峰值速率超过 8000 `pps`。

通过使用 2600 字节的摘要缓存，对于观测到的追踪，数据包分类引擎的峰值压力水平降低了 20 倍和 30 倍。

## 3.3 评估

![](img/e172ff28bf6e0a7a974849165330f450_63_0.png)

![](img/e172ff28bf6e0a7a974849165330f450_63_1.png)

## 3.7 命中率随内存的变化（不同组关联性）。Bell 追踪在左侧，OGI 追踪在右侧。

图表

## 3 摘要包分类

![](img/e172ff28bf6e0a7a974849165330f450_64_0.png)

缺失方差随内存 `$M$` 的变化（按100 ms 聚合）。`Bell` 追踪在左侧，`OGI` 追踪在右侧。

图表

## 3.4 硬件

![](img/e172ff28bf6e0a7a974849165330f450_65_0.png)

## 3.9 按秒间隔的缓存缺失率

## 3 使用摘要缓存的高效数据包分类

48

| 哈希层数 | 全缺失缓存吞吐量 |
|---|---|
| 0 | 990 MB/s |
| 1 | 868 MB/s |
| 2 | 729 MB/s |
| 3 | 679 MB/s |
| 4 | 652 MB/s |
| 5 | 498 MB/s |

## 3.3 表格

在模拟 `IXP200` 上的最坏数据流布隆过滤器性能。

## 3.5 结论

让我们考虑在该架构上实现数据包分类缓存的这种内存。如果我们使用这种内存来实现一个精确的 `IPv4` 缓存，我们最多可以存储 196 个流标识符。等效的 `IPv6` 缓存只能存储 69 个流。在 32 位四路组关联摘要缓存 `digest cache` 中使用这种内存，允许每个微引擎 `microengine` 缓存 640 个流。

如果我们使用 8 位四路组关联摘要缓存，我们仅需使用 1 KB 的片上内存内存和 38 KB 的 `SRAM`，即可为每个微引擎存储超过 1000 个流。

这种算法减少内存需求的能力在这一架构中尤为重要，因为内存传输寄存器具有局限性。每个微引擎可以访问 16 个 32 位内存传输寄存器，这意味着获取超过一个 `IPv4` 流标识符需要多次独立的内存访问，而这些访问必须是串行化的。由于独立内存访问的开销远大于单次长长度的内存访问，这会严重损害传统组关联缓存的性能。结合这些内存访问必须串行化（第一个访问必须完成后才能启动第二个访问）的事实，避免 `SRAM` 内存访问带来的性能收益变得至关重要。

作为对比，现代 `TCAM` 实现每秒可以执行 10 亿次查找 `[32]`。`IP2000` 每秒可以执行 2.33 亿次内存访问 `[31]`。即使不考虑 `TCAM` 所需的成本或功率，摘要缓存也成为了极具前景的替代方案。

这些论点使我们提出的技术成为为未来网络处理器创建高效缓存的首选。

## 3.5 结论

典型的数据包分类缓存是在尺寸和性能之间权衡。在本章中，我们提出了一种新型缓存架构，它能够高效有效地利用内存，并略微放了对准确性的要求。任何采用精确缓存算法的现有流缓存解决方案都可以通过采用我们的技术大幅提高性能，代价是牺牲一小部分准确性。

我们的技术在理论和实际性能上均优于之前的 `Bloom` 过滤器近似缓存算法，同时在解决此前 `Bloom` 过滤器缓存设计缺陷的同时，没有引入任何额外的缺点。

## 使用摘要摘要缓存实现高效数据包分类

该技术可以应用于新型两级精确缓存的设计，该设计可以利用分级内存的优势来加速精确缓存算法，并取得显著。

## 致谢

我们感谢 `Ed Kaiser` 和 `Chris Chambers` 对本文草稿版本提出的意见。我们还感谢匿名评审员提供的反馈。

美国科学基金会通过 `EIA-0130344` 号资助，以及英特尔公司的慷慨捐赠支持了这项工作。文中表达的任何观点、发现或建议均代表作者，不一定反映 `NSF` 或英特尔的观点。

## 参考文献

- [1] F. Bhabas [Note: likely Babesco] and G. Varghese, “Scalable packet classification,” Proceedings of ACM SIGCOMM 2001, August 2001, pp. 199–210.
- [2] A. Feldman and S. Mukukrishnan, “Tradeoffs for Packet Classification,” IEEE INFOCOM, 2000, pp. 1193–1202.
- [3] P. Gupta and N. McKeon, “Algorithms for packet classification,” IEEE Network Special, March/April 2001, 13(2), pp. 24–32.
- [4] T. V. Lakshman and D. Stiliadis, “High-speed policy-based packet forwarding using efficient multi-dimensional range matching,” Proceedings of ACM SIGCOMM 1998, August, 1998, pp. 203–214.
- [5] R. Srinivasan, G. Varghese, S. Suri, and M. Waldo, “Fast and stable layer-four switching,” Proceedings of ACM METRICS 1998, September, pp. 191–202.
- [6] Qiu, L. Varghese, and S. Suri, “Fast firewall implementations for software and hardware routers,” Proceedings of ACM METRICS 2001, pp. 344–345.
- [7] C. Partridge, et al., “A 50 GB/s Router,” IEEE/ACM Transactions on Networking, pp. 227–248.
- [8] F. Bhabas [Note: likely Babesco] and S. Singh, and G. Varghese, “Packet classification for core routers: Is there an alternative to CAM?” Proceedings of INFOCOM 2003, pp. 53–63.
- [9] K. Claff [Note: likely klaff], “Internet Characterization,” Ph.D. thesis, University of California, San Diego, 1994.
- [10] R. Jain, “Characteristics of destination locality in networks,” Journal of Computer Networks and ISDN Systems, 18(4), May 1990, pp. 243–254.
- [11] Xu, M. Singhal, and D. Agarwal [Note: likely Degrot], “A novel cache architecture to support layer-four packet classification at memory access speeds,” Proceedings of INFOCOM 2000, pp. 1445–1454.
- [12] C. Hui [Note: likely Huitama], IPv6: The New Internet Protocol (Second Edition), Prentice-Hall, 1998.
- [13] F. Chang, K. Li, and W. Feng, “Approximate caches for,” Proceedings of INFOCOM 2004, Hong Kong.
- [14] B. Blum [Note: likely Bloom], “Space/time tradeoffs with allowable errors,” Communications of ACM, 13(7), 1990, pp. 422–426.
- [15] T. Chi [Note: Chieh] and P. Pradhan, “High performance route using network processor,” Sixth International Symposium on High-Performance Computer (HPCA), 2000, pp. 409–418.
- [16] K. Gopalan, T. Chi [Note: Chieh], “Cache design for network,” IEEE/ACM Transactions on Networking, 2002, pp. 1–10.
- [17] SiberCore Technologies, SiberCAM Ultra-4.5M SCT4502 Product Brief, 2003.
- [18] J. Stone and Partridge, “When the CRC checksum disagree,” Proceedings of ACM SIGCOMM-00, August 2000, pp. 309–319.
- [19] D. Saltzer, D. Reed, and D. Clark, “End-to-End Arguments in System Design,” Journal of Computer and System Sciences, 2(1984), pp. 277–288.
- [20] D. Comer, *Network Systems Design Using Network Processors*, Prentice-Hall, 2003.
- [21] K. Li, F. Chang, and W. Feng, “Architectures for packet classification,” 11th International Conference on Networks (ICON) 2003, pp. 111–117.
- [22] C. Partridge, “Location and route caches,” NSF Workshop on Internet Statistics, www.caida.org/outreach/ismam/9602/partridge.html, 1996.
- [23] “Passive Measurement and Analysis,” National Laboratory for Network Research (NLR), pma.nnl.gov/net/
- [24] C. Fraser [Note: Frale], S. Moon, C. Biot, B. Lyles, and F. Tobagi, “Packet-Level Metrics from a Tier-1 IP Backbone,” ATL Technical Report TR01-ATL-10101, November 2001, Burlingame, California.
- [25] S. McCreary and K. Claff [Note: claff], “Trends in wide area traffic patterns from Ames Internet exchange,” ITC Specialist, Monterey, California, 2000.
- [26] FIPS 180-1, “Secure Hash Standard,” U.S. Department of Commerce/N.I.S.T., National Technical Information Service, Springfield, Virginia, April 1995.
- [27] L. Carter and M. Wegman, “Universal classes of hash functions,” Journal of Computer and System Sciences (1979), pp. 143–154.
- [28] Intel IXP1200 Network Processor, www.intel.com/design/network/products/npmfai/ix1200.html.
- [29] L. Sanchez, W. Milliken, A., Snoeren, F. Tchakountio, C. Jones, S. Kent, C. Partridge, and W. Strayer, “Hardware support for a hash-based IP traceback,” Proceedings of the 2nd DARPA Information Survivability Conference and Exposition, June 2001, pp. 146–152.
- [30] E. Johnson and A. Kunze, *IXP1200 Programming*, Intel Press, 2002.

# 面向 RapidIO、Hypertransport 和 PCI-Express 的灵活网络处理器接口

第 4 章

Christian Sauer

英飞凌科技股份公司（Infineon Technologies），公司研发部，慕尼黑

Matthias Gries, Kurt Kutezer

加州大学伯克利分校，电子研究实验室，伯克利

Jose Ignacio Gomez

马德里康普卢滕森斯大学，西班牙

新兴的通信协议标准（如 `PCI Express` 和 `RapidIO`）为尚未解决的网络处理器（`NPU`）正确标准化接口组的搜索注入了新动力。
