
接下来，我们添加了所需的 SA 扩展（图 19.6）。`sabd_sa_spi` 字段必须是网络字节序，因此我们对传递给函数的宿主机值调用了 `hton`。我们关闭了重放保护并将 SA 状态（图 19.7）设置为 `SABD_SASTRATE_MATURE`。我们将认证算法设置为命令行上指定的算法，并使用 `SABD_ELG_NONE` 指定不进行加密。

### 附加源地址

我们将源地址作为 `SADB_EXT_ADDRESS_SRC` 扩展添加到消息中。我们将协议设置为 0，这意味着该关联适用于所有协议。我们将前缀长度设置为对应 IP 版本的长度，IPv4 为 32 位，IPv6 为 128 位。长度字段的计算在除以 8 之前加 7，这确保了长度反映了所有 PF_KEY 扩展对齐到 64 位边界所需的填充。`sockaddr` 在扩展头之后被复制。

### 附加目的地址

以与源地址相同相同将目的地址作为 `SADB_EXT_ADDRESS_DST` 扩展添加。

### 附加密钥

我们将认证密钥作为 `SADB_EXT_KEY_AUTH` 扩展添加到消息中。我们以处理地址相同的方式计算长度字段，以便为变长密钥添加所需的填充。我们设置了位数，并将密钥数据复制到扩展头之后。

### 写入消息

我们使用 `print_sadb_msg` 函数打印消息，并将其写入套接字。

### 读取回复

我们从套接字中读取消息，直到收到一个地址指向我们的 PID 且为 `SADB_ADD` 消息的消息。然后我们使用 `print_sadb_msg` 函数打印消息并退出。

## 示例

我们运行程序发送针对 127.0.0.1 和 127.0.0.1 之间流量的 `SADB_ADD` 消息；换句话说，通过本地系统。

```
macos % add 127.0.0.1 127.0.0.1 HMAC-SHA-1 160 0123456789abcdef0123456789

Sending message:

SADB Message Add, errno 0, satype IPsec, seq 0, pid 62

SA: SPI=1 Reply=0 State=Mature

Authentication Algorithm: HMAC-SHA-1

Encryption: None

Source address: 127.0.0.1/32

Dest address: 127.0.0.1/32

Authentication key, 160 bits: 0x0123456789abcdef0123456789
```

请注意，回复回显了请求但没有包含密钥。这是因为回复是发送给所有人的。

## 19.5 动态维护 SA

为了更高的安全性，需要定期重新密钥。这通常由如 IKE (RFC 2409) [Harkins and Carnival 1998] 执行。

截至本文，IETF IPSsec 组正在开发 IKE 的替代方案。

当一对新主机之间需要 SA 时，守护进程使用 `SADB_REGISTER` 消息向内核注册自身，并在图 19.3 的 `sabd_satype` 字段中指定它可以处理的 SA 类型。如果进程可以处理多个 SA 类型，它会发送多个 `SADB_REGISTER` 消息，每个注册一个类型。在它的 `SADB_REGISTER` 回复消息中，内核包含一个算法扩展，说明支持哪些加密/认证机制。支持的算法由 `sadb_supported` 结构描述，如图 19.13；它在扩展头后面包含了一系列加密或认证描述。

```c
struct sabd_supported {
    u_int16_t sabd_supported_len;      /* 扩展 + 算法的长度 / 8 */
    u_int16_t sabd_supported_extype;   /* SAB_EXT_SUPPORTED (AUTH, ENCRYPT) / */
    u_int32_t sabd_supported_reserved; /* 留作后用 */
};
```

```c
struct sadb_alg {
    u_int8_t sabd_alg_id;             /* 来自图 19.8 的算法 ID / */
    u_int8_t sabd_alg_ivlen;           /* IV 长度，或为零 / */
    u_int16_t sabd_alg_minbits;        /* 最小密钥长度 / */
    u_int16_t sabd_alg_maxbits;        /* 最大密钥长度 / */
    u_int16_t sabd_alg_reserved;       /* 留作后用 */
};
```

> 图 19.12 生命周期扩展

对于系统支持的每个算法，一个 `sadb_alg` 结构跟在 `sadb_supported` 扩展头之后。图 19.14 显示了针对 SA 类型 `SADB_SATYPE_ESP` 消息的可能回复。

存在三种寿命扩展。`SABD_LIFETIME_HARD` 扩展分别提供 SA 的软和硬寿命。当软寿命到达时，SA 将失效。`SABD_LIFETIME_CURRENT` 扩展在 `SADB_DUMP`、`SADB_EXPIRE` 和 `SADB_GET` 回复中返回，描述当前关联的值。

## 第 19.5 动态维护 SADB

`sadb_msg_len`

```
sadb_msg()
sadb_msg_type = SADB_REGISTER
```

```
sadb_msg()
sadb_msg_type = SADB_REGISTER
sadb_supported()
sadb_supported_extype = SADB_EXT_SUPPORTED_AUTH
sadb_alg()
sadb_alg_id = SADB_ALG_MD5HMAC
ivlen = 0
minbits = 128
maxbits = 128
sadb_alg()
sadb_alg_id = SADB_ALG_SHAHMAC
ivlen = 0
minbits = 192
maxbits = 192
```

`sadb_msg_len`

```
sadb_supported()
sadb_supported_extype = SADB_EXT_SUPPORTED_ENCRYPT
sadb_alg()
sadb_alg_id = SADB_EALG_DES
ivlen = 0
minbits = 64
maxbits = 64
sadb_alg()
sadb_alg_id = SADB_EALG_3DES
ivlen = 8
minbits = 192
maxbits = 192
sadb_alg()
sadb_alg_id = SADB_EALG_NULL
ivlen = 0
minbits = 0
maxbits = 2048
```

`sadb_supported_len`

**图 19.14** 内核为 `SADB_REGISTER` 命令返回的数据。

我们的第一个示例程序如图 19.15 所示，它仅为给机制向内核注册并打印支持的算法回复。

## 密钥套接字
