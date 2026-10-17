
``` 
21 struct kern_rta
22 {
23     void            *rta_dst;
24     void            *rta_src;
25     int             *rta_iif;
26     int             *rta_oif;
27     void            *rta_gw;
28     u32            *rta_priority;
29     void            *rta_prefsrc;
30     struct rtattter *rta_mx;
31     struct rtattter *rta_mg;
32     unsigned char *rta_protoinfo;
33     unsigned char *rta_flow;
34     struct rta_cacheinfo *rta_ci;
35 };
```

如前所述，在经过漫长的智能查找转发信息库条目后，最终结果是下一跳。这个数据结构（见图 8.5）相对简单；我们要么被告知下一跳网关的 IP 地址，或者是输出设备——如果我们有一个点对点链路，只需要输出设备即可，此时下一跳地址无关。Linux 还支持多路径路由，我们可以在多个链路之间负载均衡。它还指示了到目的地的范围（scope）。

# 图 8.5 FIB 下一跳数据结构：`/linux/include/net/ip/fib.h`

```
37 struct fib_nh
38 {
39     struct net_device   *nh_dev;
40     unsigned        *nh_flags;
41     unsigned char      *nh_scope;
42     #ifdef CONFIG_IP_ROUTE_MULTIPATH
43     int             *nh_weight;
44     int             *nh_power;
45     #endif
46     #ifdef CONFIG_NET_CLS_ROUTE
47         u32             *nh_classid;
48     #endif
49     int             *nh_oif;
50     u32             *nh_gw;
51 };
```

FIB 信息不仅仅是一个下一跳。还有其他数据，如图 8.6 所示。这包含了多路径的可能性、基于源的偏好以及一些稍后会查看的维护数据。

# 554 TCP/IP 实现

图 8.6 主结构：`/linux/include/net/ip_fib.h`

```
57 struct fib_info
58 {\
59     struct fib_info      *fib_next;
60     struct fib_info      *fib_prev;
61     struct fib_info      *fib_ref;
62     atomic_t               fib_dead;
63     unsigned char         fib_flags;
64     u32                   fib_type;
65     unsigned char         fib_scope;
66     unsigned char         fib_len;
67     int                   *fib_metric;
68     int                   *fib_priority;
69     int                   *fib_nex;
70     int                   *fib_dev;
71     unsigned char         *fib_next;
72     #ifdef CONFIG_IP_ROUTE_MULTIPATH
73     int             *fib_weight;
74     int             *fib_power;
75     #endif
76     #ifdef CONFIG_NET_CLS_ROUTE
77         u32             *fib_classid;
78     #endif
79     int                   *fib_oif;
80     u32                   *fib_gw;
81 };
```

# 路由 555

整体结构（见图 8.6）是复杂的。通常，`fib_result` 类型（见图 8.7）相对简单；我们要么被告知下一跳网关的 IP 地址，或者是输出设备——如果我们有一个点对点链路，只需要输出设备即可，此时下一跳地址无关。Linux 还支持多路径路由，我们可以在多个链路之间负载均衡。它还指示了到目的地的范围（scope）。

`fib_table` 结构是 FIB 的更通用的接口，包括指向各种访问函数的指针，因此可以通过路由来编写新的 FIB 函数。

# 8.8 FIB 通用接口：`/linux/include/net/ip/fib.h`
