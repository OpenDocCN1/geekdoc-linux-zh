
`kernel/audit.c`

```c
struct audit_buffer {
    struct list_head      list;      /* 格式化就绪等待发送 */
    struct sk_buff         *skb;      
    struct audit_context *ctx; /* NULL 或关联上下文 */
    gpf_t                 gpf_mask;
};
```

`list` 是列表元素，允许将缓冲区存储在各种列表中。由于使用套接字与内核和用户通信，使用了 `sk_buff` 套接缓冲区来封装消息。连接上下文由 `ctx` 实现（如果没有系统调用审计之外的上下文，则其可能为 `NULL` 指针），`gpf_mask` 最终决定要满足哪些内存池分配。

由于审计缓冲区被频繁使用，内核保留了许多预分配的 `audit_buffer` 实例备用。`audit_buffer_alloc` 和 `audit_buffer_free` 分别释放它们——审计缓冲区缓存的处理由缓冲区本身隐式完成。它们的实现非常简单，因此在此在此进一步讨论。

从用户空间传输到内核的审计规则由以下结构表示³。

```c
<audit.h>
struct audit_rule_data {
    u32 flags;          /* AUDIT_PER_(TASK,CALL), AUDIT_PREPEND */
    u32 action;         /* AUDIT_NEVER, AUDIT_POSSIBLE, AUDIT_ALWAYS */
    u32 field_count;
    u32 mask[AUDIT_BITMASK_SIZE]; /* 受影响的系统调用(s) */
    u32 fields[AUDIT_MAX_FIELDS];
    u32 values[AUDIT_MAX_FIELDS];
    u32 fieldflags[AUDIT_MAX_FIELDS];
    u32 buflen         /* 字符串字段的总长度 */
    char buf[];         /* 字符串字段缓冲区 */
};
```

首先，`flags` 表示规则何时被激活。可能的选择有如下：

```c
<audit.h>
#define AUDIT_FILTER_USER  0x0  /* 将规则应用于用户生成的消息 */
#define AUDIT_FILTER_TASK  0x1  /* 在任务创建时应用规则（非系统调用） */
#define AUDIT_FILTER_ENTRY 0x2  /* 在系统调用进入时应用规则 */
```

> ³ 之前的内核版本使用了稍为简单的 `audit_rule`，它不允许非整数或变长度的字符串字段。该结构仍然存在于内核中以提供与用户向后兼容，但不会被新代码使用。

```c
<audit.h>
#define AUDIT_FILTER_WATCH 0x03 /* 将规则应用于文件系统监视器 */
#define AUDIT_FILTER_EXIT 0x04 /* 在系统调用退出时应用规则 */
#define AUDIT_FILTER_TYPE 0x05 /* 在系统调用进入时应用规则 */
```

当发生匹配时，`AUDIT_NEVER` 什么都不做，而 `AUDIT_ALWAYS` 生成审计记录。由于审计缓冲区被频繁使用，内核保留了许多预分配的 `audit_buffer` 实例备用。`audit_buffer_alloc` 和 `audit_buffer_free` 分别释放它们——审计缓冲区的处理由缓冲区本身隐式完成。它们的实现非常简单，因此在此不再讨论。

从用户空间传输到内核的审计规则由以下结构表示³

```c
<audit.h>
struct audit_rule_data {
    u32 flags;          /* AUDIT_PER_(TASK,CALL), ... */
    u32 action;         /* AUDIT_NEVER, AUDIT_POSSIBLE, AUDIT_ALWAYS */
    u32 field_count;
    u32 mask[AUDIT_BITMASK_SIZE];
    u32 fields[AUDIT_MAX_FIELDS];
    u32 values[AUDIT_MAX_FIELDS];
    u32 fieldflags[AUDIT_MAX_FIELDS];
    u32 buflen         /* 字符串字段的总长度 */
    char buf[];         /* 字符串字段缓冲区
};
```

首先，`flags` 表示规则何时用于激活。可能的选择有：

```c
<audit.h>
#define AUDIT_FILTER_USER  0x0  /* 将规则应用于用户生成的消息 */
#define AUDIT_FILTER_TASK  0x1  /* 在任务创建时应用规则（非系统调用） */
#define AUDIT_FILTER_ENTRY 0x2  /* 在系统调用进入时应用规则 */
```

> ³ 之前的内核版本使用了稍为简单的 `audit_rule`，它不允许非整数或变长度的字符串字段。该结构仍然存在于内核中以提供与用户向后兼容，但不会被新代码使用。

```c
#define AUDIT_FILTER_WATCH 0x03 /* 将规则应用于文件系统监视器 */
#define AUDIT_FILTER_EXIT 0x04 /* 在系统调用退出时应用规则 */
#define AUDIT_FILTER_TYPE 0x05 /* 在系统调用进入时应用规则 */
```

当发生匹配时，`AUDIT_NEVER` 什么都不做，而 `AUDIT_ALWAYS` 生成审计记录。由于审计缓冲区被频繁使用，内核保留了许多预分配的 `audit_buffer` 实例备用。`audit_buffer_alloc` 和 `audit_buffer_free` 分别释放它们——审计缓冲区的处理由缓冲区本身隐式完成。它们的实现非常简单，因此在此不再讨论。

值被嵌入到提供实际数据的层级结构中。为了实现这一点，以下摘录显示了存储的 IPC 对象的审计信息：

```c
kernel/auditsc.c
struct audit_aux_data_ipctcl {
    struct audit_aux_data  d;
    struct ipc_perm         p;
    unsigned long          qbytes;
    uid_t                   uid;
    gid_t                   gid;
    mode_t                  mode;
    u32                     oid;
};
```

注意，`struct audit_aux_data` 位于 `audit_aux_data_ipc` 的开头；真实的负载紧随其后。这允许使用通用的列表遍历和操作方法。通过强制转换为特定数据类型即可获取正确的信息。

目前，内核为许多对象类型定义了辅助数据结构：

- `audit_aux_data_ipctcl`（用于类型为 `AUDIT_IPC` 和 `AUDIT_IPC_SET_PERM` 的辅助对象）
- `audit_aux_data_socketcall`（类型 `AUDIT_SOCKCALL`）
- `audit_aux_data_sockaddr`（类型 `AUDIT_SOCKADDR`）
- `audit_aux_data_datapath`（类型 `AUDIT_AVC_PATH`）
- `audit_aux_data_datave`（类型 `AUDIT_EXECVE`）
- `audit_aux_data_mq_` (open, sendrecv, notify, getsetattrtr)（类型 `AUDIT_MQ_(OPEN, SENDRECV, NOTIFY, GETSEATTRTR)`）
- `audit_aux_data_fd_pair`（类型 `AUDIT_FD_PAIR`）

由于所有辅助审计数据结构的通用结构是类似的，本节不再特意显示它们。你可以参考 `kernel/auditsc.c` get它们的定义。

格式化审计记录的基础数据结构定义如下：

```c
kernel/audit.c
struct audit_buffer {
    struct list_head      list;      /* 格式化就绪等待发送 */
    struct sk_buff         *skb;      
    struct audit_context *ctx; /* NULL 或关联上下文 */
    gpf_t                 gpf_mask;
};
```
