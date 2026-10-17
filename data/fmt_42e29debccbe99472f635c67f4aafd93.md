
## SCTP_DEFAULT_SEND_PARAM 套接字选项

SCTP 有许多可选的发送参数，这些参数通常作为辅助数据传递，或者与 `sctp_sendmsg` 函数一起使用（该函数通常实现为向用户传递辅助数据的库调用）。希望发送大量具有相同参数的消息的应用程序可以使用此选项设置默认参数，从而避免使用辅助数据或调用 `sctp_sendmsg`。此选项的输入为 `sctp_sndcvinfo` 结构体。

```c
struct sctp_sndcvinfo {
    u_int16_t sinfo_stream;
    u_int16_t sinfo_ssn;
    u_int16_t sinfo_flags;
    u_int32_t sinfo_pid;
    u_int32_t sinfo_context;
    u_int32_t sinfo_timolive;
    u_int32_t sinfo_tsn;
    u_int32_t sinfo_cumtsn;
    sctp_assoc_t sinfo_assoc_id;
};
```

这些字段的定义如下：

- `sinfo_stream` 指定了所有消息将发送的默认流。
- `sinfo_ssn` 在设置默认选项时被忽略。当使用 `recvmsg` 函数或 `sctp_recvmsg` 函数接收消息时，该字段将保存对端在 SCTP DATA 块的序列号（SSN）字段中放置的值。
- `sinfo_flags` 决定了应用于后续消息发送的默认标志。允许的标志值可以在图 7.16。
- `sinfo_pid` 提供了在所有数据事务中设置 SCTP 有效负载协议标识符时使用的默认值。
- `sinfo_context` 指定了放置在 `sinfo_context` 字段中的默认值，当消息无法发送到对端且被丢弃时，该值作为本地标签提供。
- `sinfo_timolive` 决定了应用于所有消息发送的默认生命周期。SCTP 栈使用生命周期字段判断何时由于延迟过多（在首次传输之前）丢弃传出的消息。如果两个端点支持部分可靠性选项，则生命周期还用于指定消息在首次传输后的有效时间。
- `sinfo_tsn` 在设置默认选项时被忽略。当使用 `recvmsg` 函数或 `sctp_recvmsg` 函数接收消息时，该字段将保存对端在 SCTP DATA 块的传输序列号（TSN）字段中放置的值。
- `sinfo_cumtsn` 在设置默认选项时被忽略。当使用 `recvmsg` 函数或 `sctp_recvmsg` 函数接收消息时，该字段将保存本地 SCTP 栈与远端对端的当前 TSN。
- `sinfo_assoc_id` 指定了请求者希望再次设置默认参数的关联标识。对于一对一套接字，此字段被忽略。

| 常量 | 描述 |
|---|---|
| `MSG_ABORT` | 调用关联的强制终止（ABORTIVE termination） |
| `MSG_ADDR_OVER` | 指定 SCTP 应该覆盖主地址并改用提供的地址 |
| `MSG_EOF` | 在发送此条消息后调用平滑终止（graceful termination） |
| `MSG_PR_BUFFER` | 启用基于缓冲区的部分可靠性（partial reliability）特性（如果可用） |
| `MSG_PR_SCTP` | 在此消息上启用部分可靠性（如果可用） |
| `MSG_UNORDERED` | 指定此消息使用无序消息服务 |

图 7.16 `sinfo_flags` 字段允许的 SCTP 标志值。

请注意，默认设置只会影响未使用 `sctp_sndrvinfo` 结构体发送的消息。`sctp_sendmsg` 或 `sendmsg` 函数（带有辅助数据）将覆盖默认设置。除了设置默认值外，此选项还可以通过 `sctp_opt_info` 函数检索默认参数。

## SCTP_DISABLE_FRAGMENTS 套接字选项

SCTP 通常会将任何无法放入单个 SCTP 数据包的用户消息分片为多个 DATA 块。设置此选项将禁用发送端的此行为。当禁用时，默认行为是禁用此选项；SCTP 通常会分片用户消息。

此选项可能被希望控制消息大小的应用程序使用，以确保每个用户应用程序消息都能放入单个 IP 数据包中。启用此选项的应用程序必须准备好处理错误（即其消息太大），方法是提供应用层分片或提供更小的消息。

## SCTP_EVENTS 套接字选项

此选项允许应用程序获取、启用或禁用各种 SCTP 通知。SCTP 通知是 SCTP 栈发送给应用程序的消息。该消息作为普通数据读取，其中 `recvmsg` 函数的 `msg_flags` 字段被设置为 `MSG_NOTIFICATION`。未准备好使用 `recvmsg` 或 `sctp_recvmsg` 的应用程序不应启用事件。可以使用此选项并传递 `sctp_event_subscribe` 结构体订阅 8 种不同类型的事件。任何值 0 代表非订阅，值 1 代表订阅。

`sctp_event_subscribe` 结构体包含以下内容：

```c
struct sctp_event_subscribe {
    u_int8_t sctp_data_io_event;
    u_int8_t sctp_association_event;
    u_int8_t sctp_address_event;
    u_int8_t sctp_send_failure_event;
    u_int8_t sctp_context_event;
    u_int8_t sctp_timolive_event;
    u_int8_t sctp_tsn_event;
    u_int8_t sctp_cumtsn_event;
    u_int8_t sctp_assoc_id_event;
};
```
