
981   release:    netlink,
982   bind:       netlink,
983   connect:     netlink,
984   sockpair:   netlink,
985   accept:     netlink,
986   getname:    netlink,
987   poll:       netlink,
988   octl:       netlink,
989   listen:     netlink,
990   shutdown:   netlink,
991   setsopt:    netlink,
992   getsopt:    netlink,
993   sendmsg:    netlink,
994   recvmsg:    netlink,
995   mmap:       netlink,
996   sendpage:   netlink,
997 };

### cs 13.9. NETLINK STRUCTURES

## 13.5 NETLINK DATAS

`nl_table` 是一个 socket 指针数组。其大小为 `MAX_LINKS`。表中的每个元素对应一个协议族。

```c
net/netlink/af_netlink.c
66 static struct *nl_table[MAX_LINKS];
```

### 13.10. nl_table

| Family | Type |
| :--- | :--- |
| NETLINK_ROUTE | 0 |
| NETLINK_FIREWALL | 1 |
| NETLINK_USERSOCK | 2 |
| ... | ... |

### cs 13.5.2 rtnetlink_link

`rtnetlink_links` 被定义为 `rtnetlink_link` 结构体的指针数组。每个 `rtnetlink_link` 结构体对应特定的 netlink 命令——例如 `RTM_NEWQDIS`，这是一个用于添加新 qdisc 的命令。
- `doit`：指向一个根据控制消息中的命令被调用的函数。
- `dumpit`：指向一个在完成或出错时清理数据的函数。

`rtnetlink_link` 结构体包含 `doit` 和 `dump` 函数指针（图 13.2）。如果定义了 `CONFIG_NET_SCHED`，在注册网络设备时会初始化 `rtnetlink_links` 表格。

### cs 13.11. rtnetlink_link

```c
include/linux/rtnetlink.h
553 struct rtnetlink_link
554 {
555 int (*doit)(struct sk_buff *, struct nlsmsghdr *, void *attr);
556 int (*dumpit)(struct sk_buff *, struct netlink_callback *cb);
557 };
```

# NETLINK 数据结构

# 487

数据族

| | rtnetlink_links | 命令 |
|---|---|---|
| PF_UNSPEC 0 | | rtnetlink_link |
| | | rtnetlink_link |
| | | rtnetlink_link |
| PF_NETLINK 16 | | rtnetlink_link |

![](img/b3f231108facab5be0138b2cfd3f681a_506_0.png)

图 13.2. `rtnetlink_links` 和 `rtnetlink_link` 数据结构。

```c
net/sched/sch_api.c
1165 int _init_pktsched_init(void)
1166 {
1167     struct rtnetlink_link *link_p;
1180     link_p = rtnetlink_links[PF_UNSPEC];
1186     if (link_p) {
1187         link_p[RTM_NEWQDIS-RTM_BASE].do = tc_modify_qdisc;
1188         link_p[RTM_DELQDIS-RTM_BASE].do = tc_get_qdisc;
1189         link_p[RTM_GETQDIS-RTM_BASE].do = tc_get_qdisc;
1190         link_p[RTM_NEWQDIS-RTM_BASE].dump = tc_dump_qdisc;
1191         link_p[RTM_NEWCLASS-RTM_BASE].dump = tc_get_class;
1192         link_p[RTM_DELCLASS-RTM_BASE].do = tc_ctl_class;
1193         link_p[RTM_GETCLASS-RTM_BASE].do = tc_ctl_class;
1194         link_p[RTM_DELCLASS-RTM_BASE].dump = tc_dump_class;
1195     }
}
```

cs 13.13. `pktsched_init()`.

用作第 1180 行数组的索引。`rtnetlink_links` 全局变量被视为一个二维数组，其行对应数据族（family），每列对应该数据族中的命令（`struct rtnetlink_link`）。根据类型——例如 `RTM_NEWQDIS`（充作为新 qdisc 的命令），`struct rtnetlink_link` 用于 `RTM_NEWQDIS` 的函数指针指向第 1187 行的函数 `tc_modify_qdisc()`。同样，从第 1188 行到 1194 行，根据其他类型初始化了 `struct rtnetlink_link`（命令）的 `dump` 和 `do` 函数指针。

同样，用于向类中添加过滤器的队列规则过滤器函数指针在函数 `tc_filter_init()` (`cs 13.14`) 中初始化。

我们可以看到，对于添加/删除过滤器，get 过滤器函数指针在第 441–443 行初始化为 `tc_ctl_filter()` 函数。

# net/sched/cls_api.c

```c
432 int __init tc_filter_init(void)
433 {
434     struct rtnetlink_link *link_p = rtnetlink_links[PF_UNSPEC];
440     if (link_p) {
441         link_p[RTM_NEWTFIL_RTM_BASE] = tc_cl_tfiller;
442         link_p[RTM_DELTFIL_RTM_BASE] = tc_cl_tfiller;
443         link_p[RTM_GETFILTER_RTM_BASE] = tc_cl_tfiller;
444         link_p[RTM_GETFILTER-RTM_BASE] = tc_cl_dump_tfiller;
445     }
```

cs 13.14: `tc_filter_init ()`.

# net/ipv4/devinet.c

```c
952 static struct rtnetlink_link inet_inetlink_table[RTM_MAX_RTM_BASE+1] =
953     {inet_rtm_newrule, NULL},
960     {inet_rtm_deladdr, NULL},
961     {NULL, inet_dump_ifaddr},
962     {NULL, NULL},
963     {inet_rtm_newroute, NULL},
964     {inet_rtm_delroute, NULL},
965     {inet_rtm_getroute, inet_dump_fib},
966     {NULL, NULL},
974 #ifdef CONFIG_IP6_TABLE
975     {inet_rtm_newrule, NULL},
976     {inet_rtm_delrule, NULL},
977     {NULL, inet_dump_rules},
978     {NULL, NULL},
#endif
985 };
```
