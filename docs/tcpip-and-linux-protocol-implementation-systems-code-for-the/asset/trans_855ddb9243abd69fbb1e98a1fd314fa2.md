

# TCP/IP 与 Linux 协议实现

图 6.146 ICMP，路由器需求合规性：linux/net/ipv4/icmp.c。

- 4.3.2.8 (速率限制)
- SHOULD 能够限制错误消息速率 (OK)
- SHOULD 允许扩展速率限制 (OK，在源码中)
- SHOULD 发送消息
- 4.3.3.1 (目标不可达)
- 所有的规则都管理 IP 层，并在 i.p 中处理，而非在此处处理。
- 4.3.3.2 (重定向)
- 如果正在运行路由协议或在接口上启用了转发，则 MAY 忽略 ICMP 重定向 (OK -- 已忽略)
- 4.3.3.3 (源点扇塞)
- SHOULD NOT 产生 SQ 消息 (OK)
- 如果产生 SQ 消息，MUST 能够限制 SQ 速率 (OK，因为我们不产生它们)
- MAY 接收 SQ 消息 (OK -- 我们不接收)
- 4.3.3.4 (超时)
- 相关需求由 IP 处理（产生 TIME_EXCEEDED）。
- 4.3.3.5 (参数问题)
- MUST 为所有未被消息覆盖的错误生成这些 (OK)
- MUST 包含所指的值的原始值 (OK)

图 6.147 ICMP，路由器需求合规性：linux/net/ipv4/icmp.c。

- 4.3.3.6 (回显请求)
- MUST 实现回显服务器功能 (OK)
- MUST 在至少为 max(576, MTU) 的速率下处理 ER (OK)
- MAY 拒绝广播/多播 ER (我们不拒绝，但那没问题)
- SHOULD 具有一个用于静默 ER 的配置 (OK)
- 上述内容必须有一个默认值 = NO (OK)
- MUST 为回显请求/响应提供应用层接口 (OK)
- MUST 使用与请求发送时相同的源地址进行回复。
- 我们对不定的 ECM 是可以接受的，且它没有说明如何处理广播消息，一旦它是可选的。
- MUST 将数据从响应 复制到请求 (OK)
- MUST 更新记录路由 / 时间戳 (??)
- 如果可能，回复 MUST 使用与请求相同的源地址 (尚未实现)
- 4.3.3.7 (信息请求/响应)
- SHOULD NOT 产生或响应此消息 (OK)
- 4.3.3.8 (时间戳 / 时间戳响应)
- MAY 实现 (OK)
- MUST 回收到的每一个时间戳消息 (OK)
- MAY 丢弃请求。(OK，但请查看不一致之处)
- MUST 使用与请求发送时相同的源地址进行回复。(OK)
- 如果可能，MUST 使用反转的源回复 (尚未实现)
- SHOULD 处理路由 / 时间戳选项 (??)
- MUST 将响应传递到传输/用户层 (需要 RAW，就像 CHO 一样) (OK)
- 每秒必须更新时间戳计数至少 16 次 (OK)
- MUST 在几分钟内是“正确的” (OK)
- 4.3.3.9 (掩码请求/响应)
- MUST 支持接收 AMQ 并用 AMRe 响应 (OK)，但仅作为编译时选项
- 每个接口 SHOULD 有一个 AMRe 选项，MUST 默认值为 208 ND (尚未实现)
- 209 在知道正确的 AM 之前，MUST NOT 回复 AMRQ (OK)
- 210 在具有不同掩码的多个逻辑接口的物理接口上，MUST NOT 使用源地址 0.0.0.0 响应 AMRQ
- 212 (尚未实现)
- 213 SHOULD 检查并验证所有收到的 AMRQ (尚未实现)
- 214 SHOULD 忽略无效的 AMRQ (发送端) (尚未实现)
- 215 MUST 使用 AMRQ 的内容来确定正确的 AM (OK)
- 216 在配置地址后进行广播 AMRQ (OK -- 未执行)
- 217 如果未通过提取选项设置，MUST NOT 广播 AMRQ (OK，无选项)
- 218 MUST 使用 <NetPrefix> -1 ) 形式的广播地址 (OK)
- 219 4.3.3.1 (路由器公告与请求)
- 220 MUST 在所有网络上支持路由器发现协议的路由器部分
- 221 支持广播或多播寻址。(OK -- 由 gated 完成)
- 222 MUST 具有相应默认值的配置参数 (OK)

# 图 6.148 CMP，路由器需求合规性：linux/ipv4/icmp.c。

- 223 5.2.7.1 (目标不可达)
- 224 MUST 生成 DU (OK)
- 225 SHOULD 选择一个最佳匹配的响应码 (OK)
- 226 SHOULD NOT 生成主机隔离代码 (OK)
- 227 在管理过滤数据包时，SHOULD 使用 Communication Administrat Prohibited (尚未实现 -- 缺陷兼容性) 并且静默处理
- 229 MAY 包含一个配置选项，不生成上述内容并丢弃内部包 (OK)
- 231 MUST 包含一个不生成 Violation 的代码选项（当使用了优先级控制代码时，我们完全不生成它们）
- 233 当同一网络上的其他主机可能可达时，MUST 使用 Unreachable 或 Host Unknown 代码 (OK -- 目前没有不可达的)
- 235 MUST 使用新形式的分片需要和 Def Set 消息 (OK)
- 236 5.2.7.2 (重定向)
- 237 MUST NOT 生成重定向 (OK)
- 238 MUST 能够生成主机重定向 (OK)
- 239 SHOULD 能够生成 +TOS 重定向 (由于我们未使用 TOS)
- 240 MUST 有一个选项使用主机重定向而不是 Host+TOS (OK)
- 241 当 +TOS 重定向转发到同一接口且目标与源地址处于同一子集时 (OK)
- 245 使用路由协议时，MUST NOT 遵循重定向 (OK)
- 246 不使用路由协议时，MAY 使用重定向 (OK，编译时选项)
- 247 不作为路由器工作时，MUST 符合主机要求 (OK)
- 248 5.2.7.3 (超时)
- 249 由于 TTL=0 丢弃包时，MUST 生成 Time Exceeded Code (OK)
- 250 MAY 有一个接口选项来禁用 TE 消息的生成，但默认为“产生” (OK -- 我们不支持)

# TCP/IP 与 Linux 协议实现

现在查看与 ICMP 关联的数据。

图 6.149 ICMP 全局数据：linux/net/ipv4/icmp.c。

```
288 struct icmp_mib icmp_statistics/*WR_CPUS*/
290 /* 来自目标的错误消息数组。 */
291 /* RFC 1222: 3.2.1 规定 UNREACH, HOSTUNREACH 和 SR 必须视为瞬态元素。 */
292
293 struct icmp_err icmp_err_convert[] = {
294 {UNREACH, 0}, /* ICMP_REACH */
295 {HOSTUNREACH, 0}, /* ICMP_HOST_REACH */
296 {EMPROTO, 0}, /* ICMP_PROT_REACH */
297 {ECHOINFIUSED, 1}, /* ICMP_PORT_REACH */
298 {MSGSIZE, 0}, /* ICMP_FRAG_NEEDED */
299 {EPOPTOUNS, 0}, /* ICMP_SR_FAILED */
300 {UNREACH, 1}, /* ICMP_HOST_UNKNOWN */
301 {ECHOSTOWN, 1}, /* ICMP_HOST_ISOLATED */
302 {ENET, 1}, /* ICMP_NET */
303 {ECHOUNREACH, 1}, /* ICMP_HOST */
304 {EUNREACH, 1}, /* ICMP_RETOS */
305 {HOSTUNREACH, 1}, /* ICMP_PKT */
306 {UNREACH, 1}, /* ICMP_FILTERED */
307 {UNREACH, 1}, /* ICMP_VIOLATION */
308 {UNREACH, 1}, /* ICMP_CUTOFF */
309 };
310 /* echo 的控制参数
311 int sysctl_echo_ignore_all = 0;
312 int sysctl_echo_ignore_broadcasts = 0;
313 int sysctl_echo_ignore_bogus_responses = 0;
```

# 基础设施协议 313

```
/*
 * ICMP socket 是流控我们的 ICMP 输出以及保持所有层整洁接口的最方便方法。
 * 无 socket 的 ICMP 是非重入的（与 ICMPv6 不同，后者是强非重入的）。稍后它将是重入的，并且可以移除锁。
 */
struct inode icmp_inode;
struct socket *icmp_socket=&icmp_inode.u.socket;

static int icmp_xmit_holder = -1;

图 6.150 ICMP 全局数据：linux/net/ipv4/icmp.c。

```
/*
 * ICMP 控制数组规定了对每个类型的操作。 */
struct icmp_control {
    unsigned long *output; /* 增加输出的地址 */
    unsigned long *input; /* 增加输入的地址 */
    void (*handler)(struct icmphdr *icmp, struct sk_buffer *skb, int len);
    short error; /* 此 ICMP 是错误 */
    int *timeout; /* 速率限制 */
};
static struct icmp_control icmp_pointers[NR_ICMP_TYPES+1];
```

图 6.151 ICMP-传输锁：linux/net/ipv4/icmp.c。

```
/* ICMP 传输锁。 */
static int icmp_xmit_lock_bb(void)
{
    if (spin_trylock(&icmp_socket->sk->lock)) {
        if (icmp_xmit_holder == smp_processor_id())
            return -EAGAIN;
        spin_lock(&icmp_socket->sk->lock);
    }
    icmp_xmit_holder = smp_processor_id();
    return 0;
}

static inline_ int icmp_xmit_lock_bb(void)
{
    int ret;
    local_bb_disable();
    ret = icmp_xmit_lock_bb();
    if (ret)
        local_bb_enable();
    return ret;
}

static void icmp_xmit_unlock_bb(void)
{
    icmp_xmit_holder = -1;
    spin_unlock(&icmp_socket->sk->lock);
}

static inline_ void icmp_xmit_unlock(void)
{
    icmp_xmit_unlock_bb();
    local_bb_enable();
}
```

