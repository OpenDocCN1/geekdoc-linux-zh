
# xxx 图表列表

- 8.91 通过哈希快速访问 FIB—刷新条目：`linux/net/ipv4/fib_hash.c` 612
- 8.92 访问 FIB—PROC FS 访问：`linux/net/ipv4/fib_hash.c` 612
- 8.93 访问 FIB—RT 访问 i：`linux/net/ipv4/fib_hash.c` 613
- 8.94 访问 FIB—RT 访问 ii：`linux/net/ipv4/fib_hash.c` 614
- 8.95 访问 FIB—RT 访问 iii：`linux/net/ipv4/fib_hash.c` 614
- 8.96 访问 FIB—RT 访问 iv：`linux/net/ipv4/fib_hash.c` 615
- 8.97 访问 FIB—初始化：`linux/net/ipv4/fib_hash.c` 615
- 8.98 IGMP 618
- 8.99 PIM SM 619
- 8.100 路由接口 i：`linux/include/net/route.h` 625
- 8.101 路由接口 ii：`linux/include/net/route.h` 626
- 8.102 路由接口 iii：`linux/include/net/route.h` 626
- 8.103 基础路由维护：`linux/net/ipv4/route.c` 627
- 8.104 基础路由维护操作：`linux/net/ipv4/route.c` 628
- 8.105 路由维护 API：`linux/net/core/rtnetlink.c` 628
- 8.106 路由 API 哈希键：`linux/include/net/route.h` 629
- 8.107 路由 API 表：`linux/include/net/route.h` 629
- 8.108 路由输出查找：`linux/net/ipv4/route.c` 630
- 8.109 路由查找 i—源情况：`linux/net/ipv4/route.c` 631
- 8.110 路由查找 ii—关闭情况：`linux/net/ipv4/route.c` 632
- 8.111 路由查找—环回缓存：`linux/net/ipv4/route.c` 633
- 8.112 路由查找—全 FIB 查找：`linux/net/ipv4/route.c` 633
- 8.113 路由查找—边界情况：`linux/net/ipv4/route.c` 634
- 8.114 路由路由—边界请求：`linux/net/ipv4/route.c` 634
- 8.115 路由路由—请求请求：`linux/net/ipv4/route.c` 634
- 8.116 路由路由请求—清理引用 (put)：`linux/net/ipv4/route.c` 635
- 8.117 路由路由请求—清理引用 (put)：`linux/net/ipv4/route.c` 636
- 9.1 保证有界延迟和利用率 647
- 9.2 网络层次结构 649
- 9.3 将流量混合到单根线路上 650
- 9.4 FIFO 共享 650
- 9.5 漏桶描述 656
- 9.6 令牌桶描述 656
- 9.7 路由器原理图 657
- 9.8 基于类的队列 660
- 9.9 qdisc 调调用图结构 663
- 9.10 队列规则细粒度结构—通过过滤器进行分类 665
- 9.11 队列规则应用过滤器 666
- 9.12 分类器：`linux/net/sched/cls_api.c` 666

# xxx 图表列表

- 9.13 分类器 i：`linux/net/sched/cls.api.c` 667
- 9.14 分类器 ii：`linux/net/sched/cls.api.c` 667
- 9.15 分类器 iii：`linux/net/sched/cls.api.c` 668
- 9.16 分类器 iv：`linux/net/sched/cls.api.c` 668
- 9.17 分类器 v：`linux/net/sched/cls.api.c` 669
- 9.18 分类器 vi：`linux/net/sched/cls.api.c` 669
- 9.19 分类器 vii：`linux/net/sched/cls.api.c` 670
- 9.20 分类器 viii：`linux/net/sched/cls.api.c` 671
- 9.21 分类器 ix：`linux/net/sched/cls.api.c` 671
- 9.22 分类器 x：`linux/net/sched/cls.api.c` 672
- 9.23 分类器 xi：`linux/net/sched/cls.api.c` 672
- 9.24 分类器—dump 输出：`linux/net/sched/cls.api.c` 673
- 9.25 分类器—dump 输出：`linux/net/sched/cls.api.c` 673
- 9.26 分类器—dump 输出：`linux/net/sched/cls.api.c` 674
- 9.27 分类器—初始化：`linux/net/sched/cls_u32.c` 675
- 9.28 通用 32 位分类器数据：`linux/net/sched/cls_u32.c` 675
- 9.29 API—分类器 i：`linux/net/sched/cls_u32.c` 676
- 9.30 API—分类器 ii：`linux/net/sched/cls_u32.c` 677
- 9.31 API—查找函数：`linux/net/sched/cls_u32.c` 678
- 9.32 API—杂项支持：`linux/net/sched/cls_u32.c` 679
- 9.33 API—初始化：`linux/net/sched/cls_u32.c` 679
- 9.34 API—删除键：`linux/net/sched/cls_u32.c` 680
- 9.35 API—删除分类器：`linux/net/sched/cls_u32.c` 681
- 9.36 API—新键：`linux/net/sched/cls_u32.c` 682
- 9.37 API—设置参数：`linux/net/sched/cls_u32.c` 683
- 9.38 API—更改参数：`linux/net/sched/cls_u32.c` 684
- 9.39 API—更改参数：`linux/net/sched/cls_u32.c` 685
- 9.40 API—遍历树：`linux/net/sched/cls_u32.c` 686
- 9.41 API—RTNetlink 通信：`linux/net/sched/cls_u32.c` 687
- 9.42 API—TC 操作：`linux/net/sched/cls_u32.c` 688
- 9.43 RSVP 打开：`linux/net/sched/cls_rvp.h` 689
- 9.44 RSVP—结构：`linux/net/sched/cls_rvp.h` 690
- 9.45 RSVP—策略函数：`linux/net/sched/cls_rvp.h` 690
- 9.46 RSVP—分类器 i：`linux/net/sched/cls_rvp.h` 691
- 9.47 RSVP—分类器 ii：`linux/net/sched/cls_rvp.h` 692
- 9.48 RSVP—杂项函数：`linux/net/sched/cls_rvp.h` 693
- 9.49 RSVP—删除：`linux/net/sched/cls_rvp.h` 694
- 9.50 RSVP—销毁：`linux/net/sched/cls_rvp.h` 694
- 9.51 RSVP—通用位：`linux/net/sched/cls_rvp.h` 695

# 图表列表 xxxvii

| 编号 | 描述 | 页码 |
| :--- | :--- | :--- |
| 9.52 | RSVP—回收或生成隧道：`linux/net/sched/cls_rvsp.h` 696 |
| 9.53 | RSVP—更改参数 i：`linux/net/sched/cls_rvsp.h` 697 |
| 9.54 | RSVP—更改参数 ii：`linux/net/sched/cls_rvsp.h` 697 |
| 9.55 | RSVP—更改参数 iii：`linux/net/sched/cls_rvsp.h` 698 |
| 9.56 | RSVP—更改参数 iv：`linux/net/sched/cls_rvsp.h` 699 |
| 9.57 | RSVP—更改参数 v：`linux/net/sched/cls_rvsp.h` 700 |
| 9.58 | RSVP—遍历 RSVP 树：`linux/net/sched/cls_rvsp.h` 700 |
| 9.59 | RSVP 分类器 API—结构：`linux/net/sched/cls_rvsp.c` 701 |
| 9.60 | 路由分类器 API—结构：`linux/net/sched/cls_route.c` 701 |
