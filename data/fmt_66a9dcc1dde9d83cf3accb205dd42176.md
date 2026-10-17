
```c
event = (struct sctp_adaptation_info *) &event.adapt;

printf("SCTP_ADAPTATION_INFO: 0x%x\n", event->adapt.adaptation_ind);

break;

case SCTP_SHUTDOWN_INFO:

event = (struct sctp_shutdown_info *) &event.shutdown;

printf("SCTP_SHUTDOWN_INFO: assoc=0x%x\n", event->shutdown.assoc_id);

break;

case SCTP_PARTIAL_DELIVERY_INFO:

event = (struct sctp_partial_delivery_info *) &event.partial;

if (event->partial.event_type == SCTP_PARTIAL_DELIVERY_ABORTED)

printf("SCTP_PARTIAL_DELIVERY_ABORTED\n");

else

printf("Unknown SCTP_PARTIAL_DELIVERY_EVENT 0x%x\n", event->partial.event_type);

break;

default:

printf("Unknown notification event type=0x%x\n", event.header.type);

}
}
```

# 失败的消息

如果函数检测到失败的通知，它知道消息没有发送到对端。这意味着：(i)关联正在关闭，并且一个关联通知将很快发送（如果尚未到达），或者 (ii) 服务器正在使用部分可靠性扩展，且消息未成功发送（由于对传输施加的限制）。实际发送的数据可以通过 `ssf_data` 字段提供给函数（在我们的函数中没有检查该字段）。

## 适配层指示器

如果函数检测到适配层指示器，它将显示在设置消息（INIT 或 INIT-ACK）中传递的 32 位值。

## 部分交付通知

如果到达了部分交付通知，函数将宣布它。定义为此类写入的唯一事件是部分交付被中止。

## 关机通知

如果函数检测到此通知，它知道对端已发布了优雅关机。当关机序列完成后，此通知通常会紧跟着一个关联变更通知。

为了使用我们新函数的服务器修改见图 23.5。

```c
bzero(&evnts, sizeof(evnts));
evnts.sctp_data_io_event = 1;
evnts.sctp_association_event = 1;
evnts.sctp_address_event = 1;
evnts.sctp_send_failure_event = 1;
evnts.sctp_peer_error_event = 1;
evnts.sctp_shutdown_event = 1;
evnts.sctp_partial_delivery_event = 1;
evnts.sctp_adapt_layer_event = 1;
setsockopt(sock_fd, IPPROTO_SCTP, SCTP_EVENTS, &evnts, sizeof(evnts));
listen(sock_fd, LISTEN);
for ( ; ; ) {
len = sizeof(struct sockaddr_in);
rd_size = Sctp_recvmsg(sock_fd, readbuf, sizeof(readbuf),
(SA *)cliaddr, &len, &si, &msg_flags);
if (msg_flags & MSG_NOTIFICATION) {
print_notification(readbuf);
continue;
}
}
```

> 图 23.5 使用通知的修改后的服务器。

## 设置接收通知

在这里，服务器更改了设置，使其接收所有通知。

## 正常代码事件

此部分代码保持不变。

## 处理通知

在这里，服务器检查 `msg_flags` 字段。如果服务器发现数据是通知，它将调用我们的显示函数 `sctp_print_notification` 并循环读取下一条消息。

## 运行代码

我们启动客户端并发送如下所示的消息：

```bash
FreeBSD-lap: ./sctpclient01 10.1.1.5
[0]Hello
from str:1 seq:0 (assoc:c99e15a0):[0]Hello
Control-D
FreeBSD-lap:
```

在接收连接、消息和连接终止时，修改后的服务器会在每个事件发生时显示它。

```bash
FreeBSD-lap: ./sctpserv0
SCTP_ADPTION_INDICATION: 0x504c5253
SCTP_ASSOC_CHANGE: COMMUNICATION UP, assoc=c99e2680h
SCTP_SHUTDOWN_EVENT: assoc=c99e2680h
SCTP_ASSOC_CHANGE: assoc COMPLETE, assoc=c99e2680h
Control-C
```

如你所见，服务器现在会在事件在传输层发生时宣布它们。

## 23.5 无序数据

SCTP 通常提供数据的有序交付。SCTP 同时也提供可靠的无序服务。带有 `MSG_UNORDERED` 标志的消息在发送时没有顺序限制，并且一旦到达时即可被交付。无序数据可以在任何流中发送。不分配流序列号。图 23.6 显示了我们的客户端程序所需的更改，以便使用无序数据服务向回显服务器发送无序数据请求。

```c
18 out_sz = strlen(sendline); -- sctp_strcli_un.c
19 Sctp_sendmsg(sock_fd, sendline, out_sz,
20 to, tolen, 0, MSG_UNORDERED, sri.sinfo_stream, 0,0); -- sctp_strcli_un.c
```

> 图 23.6 一个发送无序数据的 SCTp 结构体。

## 使用无序服务发送数据

这与第 10.4 节开发的 `sctpstr_cli` 函数相同。在第 21 行，我们看到了唯一的改动：客户端显式地传递了 `MSG_UNORDERED` 标志以调用无序服务。通常，给定流内的所有数据都是通过序列号有序的。`MSG_UNORDERED` 标志导致带有此标志发送的数据按无序发送，没有序列号，并且一旦到达即可被交付，即使同一流上更早发送的其它无序数据尚未到达。

## 23.6 绑定地址子集

某些应用程序可能希望将机器 IP 地址的子集绑定到单个套字。在 TCP 和 UDP 中，传统上无法绑定地址子集的。`bind` 系统调用允许应用程序绑定单个地址或通配符地址。由于此限制，提供了新的函数调用 `sctp_bindx`，允许应用程序绑定到多个地址。注意，所有地址必须使用相同的端口号，如果端口号必须相同，请见 23.7。

```c
#include "un.h"
int sctp_bind_arg_list(int sock_fd, char *argv[], int argc)
{
struct addrinfo *res, *p;
void *bindbuf;
int addrcnt = 0;
int i;
bindbuf = calloc(argc, sizeof(struct sockaddr_storage));
p = (char *)bindbuf;
for (i = 0; i < argc; i++) {
sprintf(portbuf[i], "%s", argv[i]);
getaddrinfo(NULL, argv[i], AF_UNSPEC, SOCK_STREAM, &res);
if (res)
err_sys("getaddrinfo failed");
memcpy(p, res->ai_addr, res->ai_len);
freeaddrinfo(res);
addrcnt++;
p += res->ai_len;
}
if (sctp_bindx(sock_fd, bindbuf, addrcnt))
```
