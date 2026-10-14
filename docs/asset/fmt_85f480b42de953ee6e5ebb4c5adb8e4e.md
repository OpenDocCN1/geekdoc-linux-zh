
图 4.25a 和 4.25b 显示了内核实现的 INET/TCP 连接的控制流程以及来自 `sys_connect` 的主要例程。

`ip_route_output_key()`。`struct rt_key` 有四个字段：目的 IP、源 IP、TOI（服务类型）和输出接口号。系统的所有路由条目都哈希在全局表 `rt_hash_table` 中。这是一个 `struct rt_hash_bucket` 数组（见图 4.26）。

`struct rt_hash_bucket` 的成员链指向哈希冲突链，`lock` 用于保护哈希冲突链。如果我们在路由桶中找到了给定目的地的条目，我们就使用它，否则尝试尝试

# TCP 连接建立的内核实现

![](img/b3f231108facab5be0138b2cfd3f681a_193_0.png)

图 4.25a. `connect` 过程的代码流程。

通过调用 `ip_route_output_slow()` 为路由哈希桶创建一个新条目。我们返回到 `tcp_v4_connect()`。

**`ip_route_connect()` 结束。** 如果 `ip_route_connect()` 返回 `< 0`，意味着我们无法获取目的地的路由，因此我们从这里返回。我们

## 客户端设置

# 169

在需要分配新哈希桶的情况下。

![](img/b3f231108facab5be0138b2cfd3f681a_194_0.png)

图 25b. `connect` 过程的代码流程（续）。

`/ipv4/route.c`

```c
189 struct rt_hash_bucket {
190     struct rtable *chain;
191     rwlock_t      lock;
192 } __attribute__((__aligned__(8)));
```

图 26 路由表哈希桶。

已经得到了目的地的路由条目，我们需要对路由标志进行一些检查。如果路由标志 (`rt->rt_flags`) 设置为 `RTCF_MULTICAST` 或 `RTCF_BROADCAST`，我们返回错误，这意味着我们的目的是多广播或只连接到单播地址。我们现在用从路由表条目 (`rt->dst`) 获取的值更新 socket 缓存条目 (`sk->dst_cache`)。如果地址未设置，将 sock 源地址 (`sk->addr`) 的某些字段初始化为 `rt->src`。将目的地址 (`sk->ddaddr`) 初始化为 socket 传递的地址或从找到的路由表中获取的地址。将目的 (`sk->port`) 初始化为 socket 地址中的端口号 (`usin->sin_port`)。

*(注：由于提供的原文存在大量重复和碎片化，上述译文已根据逻辑结构进行了整合与翻译，并保留了所有原始格式标记)*

## TCP 连接建立的内核实现

`net/ipv4/tcp_ipv4.c`

```c
if ((tp->write_seq != tw->snd_nxt+65535+2) == 0)
    tp->write_seq = 1;
```

> cs 4.19. `__tcp_v4_check_established()`.

`net/ipv4/tcp_ipv4.c`

```c
sk->num = lport;
sk->sport = htons(lport);
```

> cs 4.20. `__tcp_v4_check_established()`.

`net/ipv4/tcp_ipv4.c`

```c
if ((sk->next != *sk) != NULL)
    (*sk)->pprev = &sk->next;
    *sk = sk;
    sk->pprev = sk;
    sk->hasht = hash;
```

> cs 4.21. `__tcp_v4_check_established()`.

`tcp_tw_deschedule(tw);`

```c
tcp_tw_deschedule(tw);
```

> cs 4.22. `__tcp_v4_check_established()`.

（类似于数据整合问题或连接重置）。我们跳出循环并继续其他初始化。

考虑到在完全搜索 TIME WAIT socket 列表后仍无法获取请求的端口号，我们使用端口桶（port bucket）在 `tcp_ehash` 表中查找所有处于 TCP_ESTABLISHED 状态的 socket。我们遍历链中的 socket 列表（`head->chain`），其中 `head` 是指向 `tcp_ehash` 桶的指针。在每次迭代中，我们通过调用 `tcp_IPV4_MATCH()` 来更新四元组以及与 socket 关联的接口。如果函数返回 FALSE，则我们无法使用该端口号并因此返回。

如果我们到达这里，说明该 socket 符合使用该端口号的。在这里我们需要初始化一些 socket 字段，并进行一些清理工作。我们已经获取了端口，因此初始化 socket 字段（见 cs 4.20）。

将 socket 添加到 `tcp_ehash` 表的头部（见 cs 4.21）。

如果我们从 TIME_WAIT socket 列表中获取了哈希桶，则我们需要清理 time-wait 链表（见 cs 4.22）。现在从 TIME WAIT 桶中移除该 TIME WAIT socket，最后从 `tcp_ehash` 和 `tcp_bhash` 桶中移除该 socket（见 cs 4.23）。我们已获取请求的端口并完成操作，因此从 `__tcp_v4_check_established()` 返回。

`net/ipv4/tcp_ipv4.c`

```c
624
tcp_timeout_kill(tw);
```

### cs 4.23. `_tcp_v4_check_established();`

`net/ipv4/tcp_ipv4.c`

```c
716
tcp_bind_hash(hash);
```

### cs 4.24. `tcp_v4_hash_connect();`

`net/ipv4/tcp_ipv4.c`

```c
718
sk->sport = htons(rover);
719
__tcp_v4_hash(sk,0);
```

### cs 4.25. `tcp_v4_hash_connect();`

我们需要解释 `sock` 和 `tcp_tw_bucket` 结构之间的关系。还要解释 TIME_WAIT socket 的链接（`sk->next_death` 和 `sk->pprev_death`）。我们返回 `tcp_v4_hash_connect()`。如果我们为 socket 获取了端口，则跳出主循环；否则我们使用我们的端口号再次迭代循环。

我们已经离开了循环，这意味着我们要么获取了空闲端口号或共享端口号。我们在对哈希桶头部加锁并禁用下半部（bottom half）的情况下执行搜索过程。我们需要将 socket 链接到哈希桶所有者的列表（见 cs 4.24）。

我们需要将选定的端口号分配给 socket (`sk->sport`)，并在可能创建新哈希桶时对 socket 进行进行哈希处理；否则该字段将在 `__tcp_v4_check_established()` 中分配（见 cs 4.25）。如果为 socket 分配了新的哈希桶，条件 c4.26 应该为真，因为它是该哈希桶所有者列表中唯一的 socket，并且我们从这里返回。

让我们看看端口号已指定（`sk_num != 0`）的情况，获取该端口号的哈希桶指针（见 cs 4.27）。持有哈希桶的锁（`head->lock`），现在检查该 socket 是否为所指哈希桶中的唯一项（见 cs 4.28）。

`net/ipv4/tcp_ipv4.c`

```c
717
!sk->pprev
```

### cs 4.26. `tcp_v4_hash_connect();`

`net/ipv4/tcp_ipv4.c`

```c
733
struct tcp_ehash_bucket *head = &tcp_ehash[tcp_bhash(num)];
```

### cs 4.27. `tcp_v4_hash_connect();`

`net/ipv4/tcp_ipv4.c`

```c
736
if (tb->owners == sk && sk->next == NULL);
```

### cs 4.28. `tcp_v4_hash_connect();`

`net/ipv4/tcp_ipv4.c`

```c
839
sk->prot_info->af_inet_ = tp->write_seq->
```

### cs 4.29. `tcp_v4_hash_connect();`

如果指定了端口号（`sk_num != 0`），获取该端口号的哈希桶指针（见 cs 4.27）。持有哈希桶的锁（`head->lock`），现在检查该 socket 是否为所指哈希桶中的唯一项（见 cs 4.28）。

`net/ipv4/tcp_ipv4.c`

```c
817
sk->prot_info->af_inet_ = tp->write_seq->
```
