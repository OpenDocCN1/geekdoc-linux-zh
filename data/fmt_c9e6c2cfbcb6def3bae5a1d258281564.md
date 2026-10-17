
```c
95     keytext->sadb_key_len = (sizeof(keytext) + (keybits / 8) + 7) / 8;

96     keytext->sadb_key_extype = SABD_EXT_KEY;

97     keytext->sadb_key_bits = keybits;

98     keytext->sadb_key_reserved = 0;

99     memcpy(keytext + 1, keydata, keybits / 8);

100    len += keytext->sadb_key_len * 8;

101    p += keytext->sadb_key_len * 8;

102 

103    msg->sadb_msg_len = len / 8;

104    printf("Sending message:%d\n", len);

105    print_sadb_msg(buf, len);

106    write(s, buf, len);

107 

108    printf("\nReply returned:\n");

109    /* 读取并解析 SADB_ADD 条目，忽略其他项 */
110    for (;;) {
111        int msglen;
112        struct sadb_msg *msgp;

113        msglen = read(buf, sizeof(buf));
114        msgp = (struct sadb_msg *)buf;
115        if (msgp->sadb_msg_pid == mypid && msgp->sadb_msg_type == SADB_ADD) {
116            print_sadb_msg(msgp, msglen);
117            break;
118        }
119    }
120    close(s);
121 }
```

我们在图 19.11 展示了添加静态 SADB 条目的程序。

# PF_KEY 套字和保存 PID

55-56 与之前，打开一个 PF_KEY 套字并保存 PID 以备后用。

# 构建通用消息头

57-67 我们为 `SADB_ADD` 消息构建通用消息头。直到在写入消息之前才设置 `sadb_msg_len` 项，因为它反映了整个消息的长度。`len` 变量维护消息的运行长度，`p` 指针指向缓冲区中第一个未使用的字节。

# 添加 SA 扩展

57-67 接下来，我们添加 SA 扩展（图 19.6）。`sadb_sa_spi` 字段必须是网络字节序，因此我们对传递给函数的主机值调用 `htonl`。我们关闭重放保护，并将 SA 状态（图 19.7）设置为 `SABD_SASTATE_MATURE`。我们将认证算法设置为命令行上指定的算法值，并使用 `SABD_EALG_NONE` 指定不进行加密。

# 添加源地址

68-76 我们将源地址作为 `SABD_EXT_ADDRESS_SRC` 添加到消息中。我们将协议扩展为 0，这意味着该关联适用于所有协议。我们将前缀长度设置为对应 IP 版本的适当长度，IPv4 为 32 位，IPv6 为 128 位。长度字段的计算加了 7 并除以 8，这确保了对齐到 64 位边界所需的长度填充适用于所有 PF_KEY 扩展。`sockaddr` 复制在选项头之后。

# 添加目的地址

77-85 目的地址以 `SABD_EXT_ADDRESS_DST` 扩展添加，方式与源地址相同。

# 添加密钥

86-94 我们作为 `SABD_EXT_KEY_AUTH` 将认证密钥添加到消息中。我们像地址一样计算长度字段，以便为变长度密钥添加填充。我们设置位数并将密钥数据复制到扩展头之后。

# 写入消息

95-98 我们使用 `print_sadb_msg` 函数打印消息，并将其写入套字。

# 读取回复

99-111 我们从套字读取消息，直到接收到针对我们 PID 的 `SADB_ADD` 消息。然后我们使用 `print_sadb_msg` 函数打印该消息并退出。

SADB 消息 dump，errno 0, satype IPSec AH, seq 0, pid 6246
SA: SPI=39030 Reply Window=0 State=Mature
认证算法: HMAC-SHA-1
加密算法: None
源地址: 127.0.0.1/32
目的地址: 127.0.0.1/32

注意，回复中没有包含密钥。这是因为回复被发送到了所有 PF_KEY 套接字，但不同的 PF_KEY 套接字可能属于不同保护域的套接字，密钥数据不应跨保护域。在将 SA 添加到数据库后，我们 ping 127.0.0.1 以触发 SA 的使用，然后 dump 数据库查看添加了什么。

`macosx % dump`
正在发送 dump 消息：
S dump, errno 0, satype unspecified, seq 0, pid 6283

返回的消息：
SADB Dump, errno 0, satype IPSec AH, seq 0, pid 6283
SA: SPI=39030 Reply Window=0 State=Mature
认证算法: HMAC-SHA-1
加密算法: None
[unknown extension 19]
当前生命周期：
36 次分配，0 字节
添加于 Thu Jun 5 21:01:31 2003，首次使用于 Thu Jun 5 21:15:07 2003
源地址: 127.0.0.1/128 (IP 协议 255)
目的地址: 127.0.0.1/128 (IP 协议 255)
认证密钥，160 位: 0x123456789abcdef0123456789abcdef01234567

我们从 dump 中看到内核已将我们的 IP 协议更改为 255。这是由于该实现，而不是 PF_KEY 套接字的通用属性。此外，内核将前缀长度从 32 更改为 128。这似乎是内核内部 IPv4 和 IPv6 之间一个令人困惑的问题。内核返回了一个 dump 程序无法理解的扩展（19）。未知扩展通过长度字段跳过。返回的生命周期扩展（图 19.12）包含了 SA 的当前生命周期扩展。

## 图 19.12 生命周期周期扩展。

```c
struct sadb_lifetime {
	int16_t sadb_lifetime_len;           /* 扩展长度 / 8 */
	int16_t sadb_lifetime_extype;      /* SADB_EXT_LIFETIME_(SOFT, HARD, CURRENT)) */
	uint32_t sadb_lifetime_allocations; /* 连接、端点或流的数量 */
	uint64_t sadb_lifetime_bytes;      /* 字节数 */
	uint64_t sadb_lifetime_addtime;   /* 创建时间，或从
		创建到到期的时间 */
	uint64_t sadb_lifetime_usetime;   /* 首次使用时间，或从
		首次使用到到期的时间 */
};
```

有不同的生命周期扩展。`SADB_LETIME_SOFT` 和 `SADB_LETIME_HARD` 扩展分别为 SA 指定软生命周期和硬生命周期。当达到软生命周期时，内核会发送 `SADB_EXPIRY` 消息；当达到硬生命周期后，SA 将不再被使用。`SADB_LETIME_CURRENT` 扩展在 `SADB_DUMP`、`SADB_EXPIRE`、`SADB_GET` 响应中返回，用于描述当前关联的值。

## 19.5 动态维护 SA

为了更高的安全性，需要定期重新密钥。这通常由诸如 IKE 等协议（RFC 2409）完成。在本书期间，IETF IPSec 工作组正在开发 IKE 的替代方案。

当一对新主机之间需要 SA 时，守护进程使用图 19.3 中的 `satype` 字段，通过它可以处理的 SA 类型向内核注册。如果守护进程可以处理多个 SA，它会发送多个 `SADB_REGISTER` 消息，每个注册一个类型。在它的 `SADB_REGISTER` 消息中，内核包含一个支持扩展，指示支持哪些加密或认证机制以及相应的密钥长度。支持扩展由图 19.13 所示的 `sadb_supported` 结构描述；它在在扩展头之后包含一系列 `sadb_alg` 结构描述。

## 图 19.13 支持的扩展。

```c
struct sadb_supported {
    uint16_t sadb_supported_len;      /* 扩展 + 算法 / 8 */
    uint16_t sadb_supported_extype;   /* SADB_EXT_SUPPORTED_[AUTH, ENCRYPT] */
    uint32_t sadb_supported_reserved; /* 预留 */
```
