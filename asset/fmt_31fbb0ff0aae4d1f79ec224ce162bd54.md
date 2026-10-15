
```c
#include <tpi_daytime.h>

void tpi_bind(int fd, const void *addr, size_t addrlen) {
    struct {
        struct T_bind_req msg_hdr;
        char addr[128];
    } bind_req;
    struct {
        struct T_bind_ack msg_hdr;
        char addr[128];
    } bind_ack;
    struct {
        struct T_error_ack *error_ack;
        int flags;
    };

    bind_req.msg_hdr.type = T_BIND_REQ;
    bind_req.msg_hdr.addr_length = addrlen;
    bind_req.msg_hdr.addr_offset = sizeof(struct T_bind_req);
    bind_req.msg_hdr.conn_number = 0; /* sockaddr_in * */

    ctlbuf.len = sizeof(struct T_bind_req) + addrlen;
    ctlbuf.buf = (char *)&bind_req;
    putmsg(fd, &ctlbuf, NULL, 0);

    ctlbuf.maxlen = sizeof(struct T_error_ack);
    ctlbuf.len = 0;
    ctlbuf.buf = (char *)&bind_ack;
    flags = RE_NIP;
    getmsg(fd, &ctlbuf, (int)(long *)&flags);
    if (ctlbuf.len < (int)sizeof(struct T_error_ack))
        err_quit("bad length from getmsg");

    switch (bind_ack.msg_hdr.type) {
        case T_BIND_ACK:
            return;

        case T_ERROR_ACK:
            if (ctlbuf.len < (int)sizeof(struct T_error_ack))
                err_quit("bad length for T_ERROR_ACK");
            error_ack = (struct T_error_ack *)&bind_ack.msg_hdr;
            err_quit("error_ack from bind (%d, %d)",
    }
}
```

图 33.6 `tpi_bind` 函数：将本地地址绑定到端点。

### 这两个消息是

```c
struct T_bind_ack {
    /* T_BIND_ACK */
    long type;
    long addr_length;     /* address length */
    long addr_offset;     /* address offset */
    unsigned long conn_number; /* connect to be queued */
    /* followed by the bound address */
};
```

```c
struct T_error_ack {
    /* T_ERROR_ACK */
    long type;           /* primitive in error */
    long prim_error; /* TLI error code */
    long tli_error;      /* UNIK error code */
};
```

所有这些消息都以类型开头，查看类型并相应处理消息。我们不期望从提供者获取任何数据，因此在 `getmsg` 的第三个参数中指定空指针。

当我们验证返回的控制信息量时，它是长型整数的大小，我们必须小心 `sizeof` 操作符返回的是无符号整数值，但返回的 `len` 字段可能是 `-1`。由于小于比较是将左侧的符号值与右侧的无符号值进行比较，作为无符号值的比较可能为假。在补码架构上，`-1` 被视为无符号值是非常巨大的，导致 `-1` 大于 4（如果我们假设 long 占用 4 字节）。

### 处理回复

- 31-33 如果回复是 `T_BIND_ACK`，绑定成功，我们返回。绑定到端点的实际地址在 `bind_ack` 结构的 `addr` 成员中返回，我们忽略了它。
- 34-39 如果回复是 `T_ERROR_ACK`，我们验证接收到了错误消息，然后打印结构中的返回值。在这个简单的程序中，当发生错误时我们会终止；不会返回给调用者。

我们可以通过将主函数更改为绑定除 0 以外的端口来从绑定请求中看到这些错误。例如，如果我们尝试绑定端口 1（由于它小于 1024，需要超级用户权限），我们将得到：

```
aix tpi_daytime 206.62.226.33
T_ERROR_ACK from bind (3, 0)
```

错误 `EACCES` 在此系统中值为 3。如果我们将端口更改为大于 1023 的值，但该端口已被任何 TCP 端点占用，我们将得到：

```
aix tpi_daytime 206.62.226.33
T_ERROR_ACK from bind (2, 0)
```

错误 `EADDRDBUSY` 在此系统中值为 23。

## 第33.6节

此错误是 TPI 为了支持 TLI 而引入的新错误。支持 TLI 的旧版本 TPI 在请求的端口被占用时会绑定到一个未使用的端口上。这意味着服务器绑定必须将返回的地址（来自 `T_bind` 消息，如果第三个参数是非空指针，则 `t_bind` 会返回该地址）与请求的地址进行比较，如果它们不相等则需要处理。

图 33.10 中的下一个函数是 `tpi_connect`，用于与服务器建立连接。

## 填充请求结构并发送到提供者

TPI 定义了一个 `T_conn_req` 结构，其中包含了连接的协议地址和选项：

```c
struct T_conn_req {
    long PRIM_type; /* T_CONN_REQ */
    long DEST_length; /* 目标地址长度 */
    long DEST_offset; /* 目标地址偏移 */
    long OPT_length; /* 选项长度 */
    long OPT_offset; /* 选项偏移 */
    /* 后面是连接的协议地址和选项 */
};
```

在我们的 `tpi_bind` 函数中，我们定义了一个名为 `conn_req` 的所有者，它包含一个 `T_conn_req` 结构以及存放协议地址的空间。我们填充我们的 `conn_req` 结构，将处理选项的两个成员设置为 0。我们调用 `putmsg` 并带有控制信息和标志位 0，以向流中发送一个 `M_PROTO` 消息。
