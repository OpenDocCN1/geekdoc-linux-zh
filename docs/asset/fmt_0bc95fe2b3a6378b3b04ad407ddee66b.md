
```
typedef struct os_tcb {
    OS_STK                  *OSTCBPtr;
    #if OS_TASK_CREATE_EXT
        void                    *OSTCBPtr;
        OS_STK                  *OSTBBottom;
        INT32U                  OSTCBSize;
        INT16U                  OSTCBOpt;
        INT16U                  OSTCBId;
    #endif

    #if (OS_Q_EN && (OS_MAX_QS >= 2))
        struct os_tcb           *OSTCBNext;
        struct os_tcb           *OSTCBPrev;
    #endif
    #if (OS_Q_EN && (OS_MAX_QS >= 2)) || OS_MOBOX_EN || OS_SEM_EN
        OS_EVENT                *OSTEventPtr;
    #endif

    #if (OS_Q_EN && (OS_MAX_QS >= 2)) || OS_MOBOX_EN
        void                    *OSTCBsg;
    #endif

    INT16U                  OSTDBly;
    INT8U                   OSTCBStat;
    INT8U                   OSTCBrio;

    INT8U                   OSTCBX;
    INT8U                   OSTCBY;
    INT8U                   OSTCBBitX;
    INT8U                   OSTCBBitY;

    #if OS_TASK_DEL_EN
        BOOLEAN                  OSTCBDReq;
    #endif
) OS_TCB;
```

# 列表 3.3，μC/OS 的任务控制块

`OSTCBPtr` 包含指向栈顶的指针。每个任务都有自己的栈大小，但同样重要的是每个栈可以是任何大小。某些商业内核假设所有栈都是等大的，除非你编写了完整的钩子函数。这种限制在所有任务都有不同栈需求的情况下浪费了 RAM，因为所有任务必须分配预期的最大栈大小。`OSTCBPtr` 是 `OS_TC` 结构中来自汇编代码（来自切换代码）的唯一字段。将 `OSTCBPtr` 放在结构的第一个条目便于从汇编代码访问该字段。

`OSTCBExtPtr` 是指向用户定义任务控制块扩展的指针。这允许你或 μ/C-OS 的用户在不更改 μC-OS 源代码的情况下扩展任务控制块。`OSTCBExtPtr` 仅由 `TaskCreateExt()` 使用，因此，你需要设置 `OS_TASK_CREATE_EN`。你可以创建一个包含每个任务名称的数据结构，跟踪任务时间、任务进出的切换次数（参见示例 #3）。注意：我决定将此指针直接放在栈指针之后，以防你需要访问该字段，这使得计算偏移量更容易。

`OSTBBottom` 是指向栈底的指针。如果处理器从高到低增长，`OSTBBottom` 将指向最低的内存位置。同样，如果处理器从低到高增长，`OSTCBTop` 将指向最高的栈地址。`OSTStackCheck()` 将运行时检查栈的大小。这允许你确定每个任务的可用空间。栈检查只有在你使用 `TaskCreateExt()` 创建任务时才能发生，因此你需要设置 `OS_TASK_CREATE_EN` 为 1 以启用此。

`OSTCBSize` 是一个变量，以元素数量而不是字节存储栈的大小。这意味着如果任务包含 1000 个元素且每个元素是 32 位的，那么栈的总大小为 4000 字节。同样，栈大小被 `OSTStackCheck()` 使用。

`OSTCBOpt` 是存储传递给 `TaskCreateExt()` 的“选项”的变量。因如此，该字段仅在设置 `OS_TASK_CREATE_EN` 为 1 时有效。μC/OS 目前定义了三个选项（参见 μ/OS-II；`OS_TASK_OPT_SHK`, `OS_TASK_OPT_STK_CLK` 和 `OS_TASK_SAVE_FP`），用于通过 `TaskCreateExt()` 指定为创建的任务启用栈检查。任务创建时需要清理栈。只有在你不进行栈检查时才需要清理栈。如果不指定 `OS_TASK_OPT_STK_CLK` 并删除任务，栈将报告错误的栈大小。如果你在创建后从未删除任务且你的启动代码清理了所有 RAM，那么可以通过不指定此选项来节省执行时间。

`OSTBID` 是用于持有任务标识符的变量。该字段目前未使用并已为未来的增加而预留。

`OSTCBNext` 和 `OSTCBPrev` 用于双链 `OS_TCB`。该 `OS_TCB` 链被 `OSTimeTick()` 用于更新每个任务的 `OSTCBID`。`OS_TCB` 用于每个任务在链接时

当任务被创建时，当任务被删除时，`OS_TCB` 从列表中移除。使用双向链表来允许链中的元素被快速插入或删除。

`OSTCBEventPtr` 是指向事件控制块的指针，稍后将进行描述（见第 6 章，任务间通信与同步）。

`OSTCBag` 是指向发送到任务的消息的指针。该字段的使用将在稍后进行描述（见第 6 章，任务间通信与同步）。

`OSTDBly` 用于任务需要延迟特定数量的时钟周期（clock ticks）或任务需要挂起等待事件发生的情况。在这种情况下，该字段包含任务允许等待事件发生的时钟周期数。当此值为 0 时，任务将被延迟或在等待事件时没有超时设置。

`OSTCBStat` 包含任务的状态。当 `OSTCBStat` 为 0 时，任务处于就绪运行状态。`OSTCBStat` 可以被赋予其他值，这些值在 uCOS_II 中有所描述。

`OSTCBrio` 包含优先级。高优先级任务具有低 `OSTCBrio` 值（即值越低，优先级越高）。

`OSTCBX`、`OSTCBY`、`OSTCBXt` 和 `OSTCBBy` 用于加速任务进入就绪运行状态，或在运行时让任务等待事件（以避免竞争）。这些字段的值在任务创建或任务优先级更改时会更新。值的获取方式如下：

```
OSTCBY          = priority >> 3;
OSTCBBy         = OSMapTbl[priority >> 3];
OSTCBX          = priority & 0x07;
OSTCBXt         = OSMapTbl[priority & 0x07];
```

## 3.4. 计算 OS_TCB 成员。

`OSTCBDelReq` 是一个布尔值，用于指示任务是否请求删除当前任务。该字段的使用将在稍后进行描述（见第 4 章，任务管理）。

应用程序可以拥的最大任务数（`OS_MAX_TASKS`）在 `OS_CF.H` 中指定，它决定了 uC/OS-II 分配的 `OS_TCBs` 数量。你可以通过将 `OS_MAX_TASKS` 设置为应用程序所需的实际任务数量来减少 RAM 占用。所有 `OS_TCBs` 都放置在 `OSTCBtl[1]` 中。注意，uC/OS-II 为内部使用额外分配了 `N_SYS_` 个 `OS_TCBs`（其中一个用于空闲任务，如果 `OS_TASK_STAT_EN` 设置为 1，则另一个将用于统计任务）。当 uC/OS-II 初始化时，此表中的所有 `OS_TCBs` 会以单向链表的形式连接在链中，如图 3.2 所示。当任务被创建时，`OSTCBFreeList` 指向的 `OS_TCB` 被调整指向链中的下一个 `OS_TCB`。当任务被删除时，其 `OS_TCB` 返回空闲 `OS_TCBs` 列表。

| `OSTCBtl[OS_MAX_TASKS+OS_N_SYS_TASKS-1]` | `OSTCBtl[0]` | `OSTCBtl[1]` | `OSTCBtl[2]` | `OSTCBFreeList` | `OSTCBNex` | `OSTCBNex` | `OSTCBNex` | `OSTCBNex` | 0 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

图 3-2，空闲 `OS_TCBs` 列表

## 3.04 任务就绪列表 (Ready List)

每个任务都被分配一个 0 到 `OS_LOWEST_PRIO` 之间的唯一优先级级别（包含边界，见 `OS_CFG.H`）。当 mC/OS-II 初始化时，优先级 `OS_LOWEST_PRIO` 被分配给空闲任务。你应该注意，`OS_MAX_TASKS` 和 `OS_LOWEST_PRIO` 是无关的。你可以在应用程序中只拥有 10 个任务，同时仍拥有 32 个优先级级别（如果你将 `OS_LOWEST_PRIO` 设置为 31）。
