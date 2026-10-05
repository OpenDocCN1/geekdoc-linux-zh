

# 协议实现框架

```c
* 分配额外的空间。
* 当调用者希望修改数据并需要数据的
* 私有拷贝以进行修改，以及为新字段留出更多空间时使用。
* 失败时返回 NULL，成功时返回缓冲区指针。
* 返回的缓冲区引用计数为 1。
* 如果此函数从中断中调用，必须将 GFP_ATOMIC
* 作为分配优先级。
*/
struct sk_buff *skb_copy_expand(const struct sk_buff *skb,
    int headroom,
    int tailroom,
    int gfp_mask)
{
    struct sk_buff *n;
    /* 分配拷贝缓冲区 */
    n=alloc_skb(headroom + (skb->tail - skb->data) + tailroom,
        gfp_mask);
    if(!NULL)
        return NULL;
    skb_reserve(n, headroom);
    /* 设置尾指针和长度 */
    skb_put(n, skb->len);
    /* 仅拷贝数据。 */
    memcpy(n->data, skb->data, skb->len);
    copy_header(n, skb);
    return n;
}
```

最后，我们看到了设置实际缓冲区池的代码。

图 5.135 初始化套接字缓冲区全局数据：linux/net/core/skbuff.c。

```c
void __init_skb_init(void)
{
    int i;
    skbuff_head_cache = kmem_cache_create("skbuff_head_cache",
        sizeof(struct sk_buff),
        0,
        SLAB_HWCACHE_ALIGN);
```

# TCP/IP 与 Linux 协议实现

```c
481             skb_headerinit, NULL);
482     if (skbuff_head_cache)
483             panic("cannot create skbuff cache");
484
485     for (i=0; i<NR_CPUS; i++)
486                 skb_queue_head_init(&skb_head_pool[i].list);
487 }
```

# 5.7 协议控制块的一天

这里是与 INET 协议族中流型套接字状态相关的协议相关数据。

5.1336 TCP 状态：linux/include/net/tcp.h

```c
59      * 如果此失败，端口将无法共享。
60      *
61      * 有趣的点是测试 #2。这是一个全天运行的 FTP
62      * 服务器。当我们优化这个用例时，我们使用了下面特定的标志位：
63      * 当我们将套接字添加到绑定桶列表（bind bucket list）时，我们执行
64              * check_of: (netsk->reuse_aa && (netsk->state == TCP_LISTEN));
65      * 只要所有添加到绑定桶的套接字通过了这个测试，
66      * 标志位就会被设置。
67      * 结果的情况是 tcp_v4[4].verify_bind(bind) 只需要检查
68      * 这个标志位，如果它被设置且尝试绑定的套接字
69      * sk_reuse 被设置，我们完全不需要遍历所有者列表，
70      * 我们直接返回可以将该套接字绑定到请求的本地端口。
71      *
72      * 听起来工作很多，但这是值得的。在更朴素的
73      * 实现中（例如 FreeBSD 等），端口的列表
74      * 必须为 FTP 服务器打开的每个数据端口进行遍历。
75      * 不可否认，这并不具备扩展性。当几千个 FTP
76      * 用户加载到你的机器时，知道以 O(1) 时间创建
77      * 新端口不是很好吗？Dave 是这么认为的。
78      */
79  struct tcp_bind_bucket {
80      unsigned short port;
81      unsigned short host;
82              struct fast_reuse;
83              struct tcp_bind_bucket *next;
84              *owners;
85              struct sock sock;
86              struct tcp_bind_bucket *pprev;
87  };
88  struct tcp_bind_hashbucket {
89      spinlock_t lock;
90              struct tcp_bind_bucket *chain;
91  };
```

# 图 5.137 TCP 状态标志：linux/include/net/tcp.h。

```c
extern struct tcp_hashinfo {
    /* 用于完整标识的套接字。这里的套接字
     * 不带通配符且具有以下不变性：
     * TCP_ESTABLISHED <= sk->state < TCP_CLOSE
     *
     * 表的第一部分用于 TIME_WAIT 状态的套接字，后半部分
     * 仅用于 TIME_WAIT 套接字。 */
    struct tcp_ehash_bucket __tcp_ehash;
    /* 好了，为了快速绑定/连接，
     * 也需要 TCP 哈希。 */
    struct tcp_bind_hashbucket __tcp_bbash;
    int __tcp_bbash_size;
    int __tcp_ehash_size;
    /* 所有 TCP_LISTEN 状态的套接字都会在这里。
     * 通配符套接字可以存在。哈希函数
     * 用于本地端口。 */
    struct sock __tcp_listening_hash[TCP_HTABLE_SIZE];
```

# 图 5.138 TCP 连接状态：linux/include/net/tcp.h。

```c
/* 以上所有内容在启动时写入一次，
 * 之后主要是是读取访问。
 *
 * 现在对齐到一个新缓存，因为以下内容
 * 经常是脏。 */
spinlock_t __tcp_hash_lock;
__attribute__((aligned(SMP_CACHE_BYTES)));
atomic_t __tcp_hash_users;
wait_queue_head_t __tcp_hash_wait;
spinlock_t __tcp_portalloc_lock;
} struct tcp_hashinfo {
    define ehash (tcp_hashinfo->ehash)
    define bbash (tcp_hashinfo->bbash)
    define ehash_size (tcp_hashinfo->ehash_size)
    define bbash_size (tcp_hashinfo->bbash_size)
    define listening_hash (tcp_hashinfo->listening_hash)
    define hash_lock (tcp_hashinfo->hash_lock)
    define hash_users (tcp_hashinfo->hash_users)
    define hash_wait (tcp_hashinfo->hash_wait)
    define port_alloc_lock (tcp_hashinfo->port_alloc_lock);
};
kmem_cache_t *tcp_bucket_cache;
```

# TCP/IP 与 Linux 协议实现

```c
extern struct tcp_bind_bucket *tcp_bucket_create(struct tcp_bind_hashbucket *head,
                               unsigned short num);
extern void tcp_bucket_unlock(struct sock *sk);
extern int tcp_port;
extern struct sock *tcp_v4_lookup(unsigned addr, unsigned short port, int def);
/* 这些是与 AF 无关的 */
```

图 5.139 TCP 状态变量：linux/include/net/tcp.h。

```c
{
  return (port &
}
/* 这是一个 TIME_WAIT 桶。它解决了高负载服务器
 * 上该状态套接字的内存消耗问题，
 * 而没有违反协议规范。 */
struct tcp_tw_bucket {
  /* 精确匹配 struct sock 的开头。
   * 我知道这很糟糕，但如果我创建一个 "struct sock_seq"，
   * 我就得编辑每一个网络文件。DaveM */
  __u32           addr;
  __u32           rcv_seq;
  __u16           dport;
  unsigned short num;
  int             dev_if;
  struct sock     next;
  struct sock     prev;
  struct sock     bind_next;
  struct sock     bind_pprev;
  unsigned char   state;
  unsigned char   substate; /* "zapped" 被替换为 "substate" */
  __u16           unsigned short;
  unsigned char   reuse;
  unsigned char   rcv_wnd; /* 它也是 TCP 桶特有的 */
  atomic_t        refcnt;
/* 这些是我们的。 */
int             hash_count;
int             timeout;
  __u32           rcv_next;
  __u32           snd_next;
  __u32           rcv_wnd;
  __u32           seq_next;
```

TCP 状态机的内容远于此，但我们将在第 7 章查看。

# 5.7.1 套接字和路由相关的传输状态

由于历史原因，某些与传输协议相关的状态保存在套接字结构中（无论如何，它是每个连接、每个进程对应的；对于面向连接的单播协议这不是一个糟糕的错误，虽然未来对于同一台机器上有多个进程的可靠组播协议这可能是问题）。

路由相关的状态将在第 8 章讨论。总之，Linux 通信协议栈中最强大的数据结构之一包含在命名简单的 sock.h 文件中。

与之一起的是 `tcp_opt` 结构，它将在 7 章中详细讨论。

图 5.140 套接字 TCP 状态起始：linux/include/net/sock.h。

```c
struct tcp_opt {
    int         tcp_header_len; /* 要发送的 TCP 头部字节 */
    /*
    头部预测标志
    unsigned    0x5710 << 16 + snd_win 在网络字节序
    /*
    __u32 pred_flags;
    /*
    按照正确名称命名 RFC793 变量。这意味着你可以
    将代码和规范并排阅读（并笑……）
    参见 RFC793 和 RFC1122。RFC 使用大写字母编写这些。
    */
    */
```

还有 IP、级别信息（例如 `struct ipv6_pinfo` 和 `struct inet_opt`），以及套接字层的数据本身。

图 5.141 套接字相关 IP 选项：linux/include/net/sock.h。

```c
struct inet_opt {
    int             ttl;                /* TTL 设置 */
    int             tos;                /* TOS */
    unsigned        cmsg_flags;
    struct          ip_options *opt;   /* 头部？ */
    unsigned char  hdrincl;
    __u8            mc_ttl;             /* 组播 TTL */
    __u8            mc_loop;            /* 回环 */
    unsigned        recverr : 1;
};
```

