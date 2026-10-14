
cs 13.22. `netlink_unicast()`.

当前进程；如果没有过载，它在第 450 行将当前进程状态更改为 `TASK_RUNNING`。最后，在第 463 行将 `sk_buff` 压入 socket 的接收队列，并在第 464 行调用函数 `sk->data_ready(sk_len)`。该函数指针初始化为 `netlink_data_ready()` 函数（见第 13.3 节）。

## 13.8.2 `netlink_data_ready()`.

`netlink_data_ready()` 调用 rtnetlink socket 的 `data_ready` 函数指针，即第 690 行的 `rtnetlink_rcv()` 函数（13.23）。

## 13.8.6 `rtnetlink_rcv()`.

`rtnetlink_rcv()` 在第 443 行（13.24）的 `while` 循环中从 socket 的接收队列中出队 `sk_buff`，并对每个 `sk_buff` 在第 444 行调用函数 `rtnetlink_rcv_skb()` 处理数据。

## 13.8.7 `rtnetlink_rcv_skb()`.

`rtnetlink_rcv_skb()` 将第 405 行（13.25）的 `sk_data` 指针强制转换为 `struct nlmsdr`，即 netlink 头部。`skb->data` 是 netlink 数据包的起始地址（见第 13.7 节）。然后 `rtnetlink_rcv_skb()` 在第 411 行将 netlink 头部作为参数之一调用函数 `rtnetlink_rcv_msg()`。

```c
netlink/af_netlink.c

687 void netlink_data_ready(struct sock *sk, int len)

688 {

689     if (sk->protoinfo->af_netlink->data_ready)

690         sk->protoinfo->af_netlink->data_ready(sk, len);

}
```

cs 13.23. `netlink_data_ready()`.

```c
net/core/rtnetlink.c

435 static void rtnetlink_rcv(struct sock *sk, int len)

436 {

437     do {

442         while ((skb = skb_dequeue(&sk->receive_queue)) != NULL) {

443             if (rtnetlink_rcv_skb(skb)) {

444                 if (sk->len)

445                     skb_queue_head(&sk->receive_queue, skb);

446                 else

447                     kfree_skb(skb);

448                 break;

449             }

450         kfree_skb(skb);

451     }

454     up(&rtnl_sem);

455     while (rtnl && rtnl->receive_queue_len);

456 }
```

cs 13.24. `rtnetlink_rcv()`.

```c
net/core/rtnetlink.c

397 extern __inline int rtnetlink_rcv_skb(struct sk_buff *skb)

398 {

405     nlh = (struct nlmsghdr*)skb->data;

411     if (rtnetlink_rcv_msg(skb, nlh, &err)) {

419     }

425 }
```

cs 13.25. `rtnetlink_rcv_skb()`.

## 13.8.2 `rtnetlink_rcv_msg()`.

`rtnetlink_rcv_msg()` 首先从第 289 行和 299 行（13.26）的 netlink socket 提取类型和 family。netlink 头部（`nlh`）作为该函数的输入。`doit` 函数存储在 netlink 表中。在第 378 行根据 `family` 调用 `tc_modify_qdisc()`。在这种情况下，对于添加 filter，`doit` 指向 `tc_ctl_filter`；对于获取 qdisc，`doit` 指向 `tc_qdisc()` 函数。

```c
net/core/rtnetlink.c

272 rtnetlink_rcv_msg(struct sk_buff *skb, struct nlmsghdr *nlh, int *err)

273 {

289     type = nlh->nlmsg_type;

299     type = RTM_BASE;

305     family = (struct rtgenmsg*)NLMSG_DATA(nlh)->rtgen_family;

311     link_tab = rtnetlink_links[family];

312     if (link_tab == NULL)

313         link_tab = rtnetlink_links[PF_UNSPEC];

314     link = &link_tab[type];

374     if (link->doit == NULL)

375         link = &(rtnetlink_links[PF_UNSPEC][type]);

378     err = link->doit(skb, nlh, void *rta);

390 }
```
