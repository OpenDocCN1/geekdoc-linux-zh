

# 协议实现框架 205

```c
#if defined(CONFIG_ECONET) || defined(CONFIG_ECONET_MODULE)
    struct econet_opt *af_econet;
#endif
#if defined(CONFIG_ATM) || defined(CONFIG_ATM_MODULE)
    struct atm_vcc *af_atm;
#endif
#if defined(CONFIG_IRDA) || defined(CONFIG_IRDA_MODULE)
    struct irda_sock *irda;
#endif

protinfo();
```

图 5.149 Socket 状态 vii、定时器和回调：linux/include/net/sock.h。

```c
/* 这部分用于超时函数。 */
struct timer_list timer; /* 这是 sock 清理定时器。 */
struct deval stamp;

/* 标识和报告 IO 信号 */
struct socket *socket;

/* RPC 层私有数据 */
void *user_data;

/* 回调函数 */
void (*state_change)(struct sock *sk);
void (*data_ready)(struct sock *sk, int bytes);
void (*write_space)(struct sock *sk);
void (*error_report)(struct sock *sk);

int (*backlog_rcv)(struct sock *sk, struct sk_buff *skb);
void (*destruct)(struct sock *sk);
```

## 5.7.2 Socket 结构的未来

代码中有一条注释提到，作者们希望整理所有内容，这描述了一种更优雅的解决方案。

图 5.150 整理 socket 状态的提议：linux/include/net/sock.h。

- * 这个结构真的需要清理一下了。
- * 它大部分是用于 TCP 的，没有被任何其他协议使用。
/* */

# 206 TCP/IP 和 Linux 协议实现

```c
424 * 主意是开始逐渐移动到新的 struct struct
425 * 
426 * IMHD 较新的 struct 应该具有以下格式：
427 * 
428 *     struct sock {
429 *         sockmem [mem, proto, callbacks];
430 * 
431 *         union or struct {
432 *             ax26;
433 *         } ll1_pinfo;
434 * 
435 *         union {
436 *             ipv4;
437 *             ipv6;
438 *             ipx;
439 *             netrom;
440 *             rose;
441 *             x25;
442 *         } net_pinfo;
443 * 
444 *         union {
445 *             tcp;
446 *             udp;
447 *             spx;
448 *             netrom;
449 *         } tp_pinfo;
450 * 
451 * }
452 * 
453 * 这个主意失败了，因为 IPv6 迁移假设了双 IP/IPv6 socket。
454 * 所以，net_pinfo 实际上是 IPv6，而 protinfo 统一了所有其他
455 * 私有区域。
```

## 5.7.3 引用计数

在后面，socket 状态维护代码还有另外两个重要的方面。首先，我们看到了引用计数。

图 5.151 Socket 引用计数注释：linux/include/net/sock.h。

```c
947 /*
948 * 引用计数假设。
949 * 
950 * 每个 SOCKET 的用户都应该持有一个引用计数。
951 * 每个 socket 的访问点（一个哈希表桶、来自列表的引用、
952 * 运行中的定时器、在途的 skb）必须持有一个引用计数。
953 * 当引用计数变为 0 时，意味着它永远不会再次增加。
954 * 当引用计数变为 0 时，意味着该 socket 外部已没有
955 * 存在的引用，且当前 CPU 上的进程是最后一个使用
956 * 它的，并可以释放/销毁这个 socket。
957 * sk_free 从任何上下文调用：进程、bs、中断（IRQ）。当
958 * 它被调用时，socket 没有外部引用 -> sk_free
```

# 协议实现框架 207

- * 959 可能会释放分配给 socket 的后代资源，但
- * 960 在被调用时，socket 没有被任何
- * 961 哈希表、列表等引用。
- * 962 从外部（来自网络或另一个进程）递送的数据包
- * 963 并进入队列/接收队列的不应该在
- * 964 它们留在队列中时获取引用计数。否则，数据包会在漏洞中泄露，当
- * 965 socket 被一个 CPU 锁定而由另一个 CPU 进行解绑时。
- * 966 释放到 /dev/netlink（导致接收和错误队列），tcp
- * 967 泄露到 backlog。数据包 socket 在
- * 968 BR_NETPROTO_LOCK 内部完成所有处理，
- * 所以它会产生这种竞态条件。UNIX socket
- * 969 使用 SMP 锁，因此它们容易产生。
- 970 /

- * 972 / 获取 socket 引用计数。此操作仅当
- * 973 它已经获取了 f.. 且在哈希表
- * 974 或列表中找到且在锁下进行查找
- * 975 时有效，防止哈希表修改
- * 976 /

图 5.152 socket 管理的内联函数：linux/include/net/sock.h。

```c
static inline void sock_hold(struct sock *sk)
{
    atomic_inc(sk->refcnt);
}
/* 在上下文中获取 socket，假设 socket 引用
不会变为 0。在任何 socket 上下文中都是 true。 */
static inline void _sock_put(struct sock *sk)
{
    atomic_dec(sk->refcnt);
}
/* 获取 socket 并销毁它，如果它是最后一个引用。 */
static inline void sock_put(struct sock *sk)
{
    if (atomic_dec_and_test(sk->refcnt))
        sk_free(sk);
}
```

图 5.153 socket 管理的内联函数：linux/include/net/sock.h。

- * 998 从进程上下文将 socket 分离。
- * 999 从等待队列和 inode 分离。
- * 1000 注意 inode 持有该 socket 的引用计数，
- * 1001 我们在这个函数中不释放它，因为协议
- * 1002 需要这个 socket（TCP）。
- * 1004 /

# TCP/IP 和 Linux 协议实现

```c
1005 static inline void sock_orphan(struct sock *sk)
{
    1007 write_lock(sk->callback_lock);
    1008 sk->dead = i;
    1009 sk->socket = NULL;
    1010 sk->sleep = NULL;
    1011 write_unlock(sk->callback_lock);
}
```

图 5.114 socket 管理的内联函数：linux/include/net/sock.h。

```c
1014 static inline void sock_graft(struct sock *sk, struct socket *parent)
{
    1016 write_lock(sk->callback_lock);
    1017 sk->sleep = &parent->wait;
    1018 parent->sk = sk;
    1019 sk->socket = parent;
    1020 write_unlock(sk->callback_lock);
}

1023 static inline int sock_i_uid(struct sock *sk)
{
    1025 int uid;
    1026 read_lock(sk->callback_lock);
    1028 uid = sk->socket->inode->i_uid ?: 0;
    1029 read_unlock(sk->callback_lock);
    1030 return uid;
}

1032 static inline unsigned long sock_i_ino(struct sock *sk)
{
    1034 unsigned long ino;
    1036 read_lock(sk->callback_lock);
    1038 ino = sk->socket->inode->i_ino ?: 0;
    1039 read_unlock(sk->callback_lock);
    1040 return ino;
}
```

## 5.7.4 Socket 和 路由

接下来，我们看到将 socket 与路由关联的代码。

图 5.155 路由状态：linux/include/net/sock.h。

```c
1043 static inline struct dst_entry *
__sk_dst_get(struct sock *sk)
{
    1046 return sk->dst_cache;
}
```

# 协议实现框架 209

```c
1048 static inline struct dst_dst_entry *
__sk_dst_check(struct sock *sk, u32 cookie)
{
    1101 struct dst_dst_entry *dast = sk->dst_cache;
    1103 if (dast && dast->obsolete && dast->ops->check(dast, cookie) == NULL) {
       1104 sk->dst_cache = NULL;
       1105 return NULL;
    }
    1108 return dast;
}

1111 static inline struct dst_dst_entry *
sk_dst_check(struct sock *sk, u32 cookie)
{
    1114 struct dst_dst_entry *dast = sk_dst_get(sk);
    1116 if (dast && dast->obsolete && dast->ops->check(dast, cookie) == NULL) {
       1117 sk_dst_reset(sk);
       1118 return NULL;
    }
    1121 return dast;
}
```

有一组函数可以安全地向 socket 读写队列数据（记得 socket 是在用户进程和内核线程之间共享的）。

图 5.158 数据报管理接口：linux/include/net/sock.h。

```c
1225 /*
* 如果收到的数据报可以容纳，则将其入队。流式和顺序化
* 协议通常不使用此方法，因为它们需要将缓冲区放入
* 并对其进行处理。

* 使用内联是因为因为它非常短，并且对于几乎每一个收到的
* 数据包都会调用。
*/
1234 static inline void skb_set_owner_w(struct sk_buff *sk, struct sock *sk)
{
    1236 sock_hold(sk);
    1237 skb->sk = sk;
    1238 skb->destructor = sock_wfree;
    1239 atomic_add(skb->truesize, skb->wmem_alloc);
}
```

