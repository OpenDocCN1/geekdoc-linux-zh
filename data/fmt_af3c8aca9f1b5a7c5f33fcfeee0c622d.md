
```c
struct sockaddr_in myaddr, servaddr;

if (argc != 2)
    return err_quit("usage: tpi_daytime <IPAddress>");

fd = Open(TPI_TCP, O_RDWR, 0);

/* 绑定任何本地地址 */

bzero(&myaddr, sizeof(myaddr));
myaddr.sin_family = AF_INET;
myaddr.sin_addr.s_addr = htonl(INADDR_ANY);
myaddr.sin_port = htons(0);
tpi_bind(fd, &myaddr, sizeof(struct sockaddr_in));

/* 填充服务器地址 */

bzero(&servaddr, sizeof(servaddr));
servaddr.sin_family = AF_INET;
servaddr.sin_port = htons(13); /*日期服务器 */
Inet_pton(AF_INET, argv[1], &servaddr.sin_addr);
tpi_connect(fd, &servaddr, sizeof(struct sockaddr_in));

for ( ; ; ) {
    if ((n = tpi_read(fd, recvline, MAXLINE)) <= 0) {
        if (n == 0)
            break;
        else
            err_sys("tpi_read error");
    }
    recvline[n] = 0; /* 零终止 */
    puts(recvline, _stdout);
}
tpi_close(fd);
exit(0);
}
```

**图 31.8** 我们为 TPI 编写的日期客户端主函数。

**打开提供者，绑定本地地址** 我们打开对应于传输提供者的设备（通常为 `/dev/tcp`）。我们填充一个带有 `INADDR_ANY` 和端口 `0` 的 Internet 套接地址结构，告诉 TCP 将任何本地地址绑定到我们的端点。我们调用函数 `tpi_bind`（简称为 `tpi_bind`）来执行绑定。

# 填充服务器地址，建立连接

我们填充另一个 Internet 地址结构，内容为服务器的 IP 地址（从命令行获取）和端口（`13`）。我们调用 `tpi_connect` 函数建立连接。

**从服务器读取数据，复制到标准输出**
与我们其他的日期客户端一样，我们只需将数据从连接复制到标准输出，并在接收到服务器的 EOF（例如 FIN）时停止存储。然后我们调用 `tpi_close` 函数关闭我们的端点。

我们的 `tpi_bind` 函数所示图 3.19。
**填充 t_bind_req 结构**
`<sys/tihdr.h>` 头文件定义了 `T_bind_req` 结构。

```c
struct T_bind_req {
    t_scalar_t  PRIM_type;    /* T_BIND_REQ */
    t_scalar_t  ADDR_length;   /* 地址长度 */
    t_scalar_t  ADDR_offset;   /* 地址偏移量 */
    t_scalar_t CONID_number;  /* 请求连接 ID */
    /* 后面是协议地址 */
};
```
所有 TPI 请求都定义为以长整数类型开头的结构。我们定义了以 `T_bind_req` 结构开头的结构，后面跟着要绑定的缓冲区。TPI 提供者期望此缓冲区包含一个 `sockaddr_in` 结构。

我们填充 `t_bind_req` 结构，设置地址的 `ADDR_length`（Internet 结构）和 `ADDR_offset`（紧随 `bind_req` 结构之后）。我们无法保证该位置适用于 `sockaddr_in` 结构，因此我们使用 `memcpy` 将调用者的结构复制到我们的 `bind_req` 结构中。我们将 `CONID_number` 设置为 `0`，因为是客户端。

**调用 putmsg**
TPI 要求我们构建的结构作为 `M_PROTO` 消息传递给提供者。因此我们调用 `putmsg`，指定 `bind_req` 结构作为控制信息，标志为 `0`。

**调用 getmsg 读取高优先级消息**
`BIND_REQ` 请求的响应将是 `T_BIND_ACK` 消息或 `T_ERROR_ACK` 消息。这些确认消息是以高优先级（`M_PRI`）发送的，因此我们使用带有 `RS_PRI` 标志的 `getmsg` 读取它们。由于回复是高优先级消息，它将跳过流上的普通优先级消息。

```c
#include "tpi_daytime.h" // streams/tpi_bind.c

void tpi_bind(int fd, const void *addr, size_t addrlen)
{
    struct {
        struct T_bind_req msg_hdr;
        char addr[128];
    } bind_req;
    struct {
        struct T_bind_ack msg_hdr;
        char addr[128];
    } bind_ack;
    struct t_buf ctlbuf;
    struct T_error *error_ack;
    int flags;
    bind_req.msg_hdr.PRIM_type = T_BIND_REQ;
    bind_req.msg_hdr.ADDR_length = addrlen;
    bind_req.msg_hdr.ADDR_offset = sizeof(struct T_bind_req);
    bind_req.msg_hdr.CONID_number = 0; /* sockaddr_in */
    memcpy(bind_req.addr, addr, addrlen);
    ctlbuf.len = sizeof(struct T_bind_req) + addrlen;
    ctlbuf.buf = (char *)&bind_req;
    putmsg(fd, &ctlbuf, NULL, 0);
    ctlbuf.maxlen = sizeof(struct T_bind_ack);
    ctlbuf.len = 0;
    ctlbuf.buf = (char *)&bind_ack;
    flags = RS_PRI;
    getmsg(fd, &ctlbuf, NULL, &flags);
    if (ctlbuf.len < (int)sizeof(struct T_bind_ack))
        err_quit("bad length from getmsg");
    switch (bind_ack.msg_hdr.PRIM_type) {
        case T_BIND_ACK:
            return;
        case T_ERROR_ACK:
            if (ctlbuf.len < (int)sizeof(struct T_error_ack))
                err_quit("bad length for T_ERROR_ACK");
            error_ack = (struct T_error *)&bind_ack.msg_hdr;
            err_quit("T_ERROR ACK from bind (%d, %d)", error_ack->TLI_error, error_ack->UNIX_error);
        default:
            err_quit("unexpected message type: %d", bind_ack.msg_hdr.PRIM_type);
    }
}
```

图 31.9 `tpi_bind` 函数：将本地地址绑定到端点。

这两条消息如下：

```c
struct T_bind_ack {
    t_scalar_t   PRIM_type;      /* T_BIND_ACK */
    t_scalar_t   ADDR_length;    /* 地址长度 */
    t_scalar_t   ADDR_offset;     /* 地址偏移量 */
    t_scalar_t CONID_number;   /* 等队列的连接绑定 */
```
