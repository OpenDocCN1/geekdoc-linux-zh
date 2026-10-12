
# OSQPostFront()

`INT8U OSQPostFront(OS_EVENT *pevent, void *msg);`

| 文件 | 调用来源 | 启用的代码 |
| --- | --- | --- |
| `OS_Q_C` | 任务或 ISR | `OS_Q_EN` |

`OSQPostFront()` 用于通过队列向任务发送消息。`OSQPostFront()` 的行为与 `OSQPost()` 相似，不同之处在于消息插入到队列的头部。这意味着 `OSQPost()` 使队列的行为像是一个后入先出（LIFO）队列，而不是先入先出（FIFO）队列。消息的大小为指针大小的变量，其用途取决于应用程序。如果消息队列已满，则向调用者返回错误。`OSQPostFront()` 将立即返回给调用者，消息将不会被放入队列中。如果有任何任务正在队列等待消息，则优先级最高的任务将接收该消息。如果等待消息的任务优先级高于发送消息的任务，则高优先级任务将恢复运行，而发送消息的任务将悬挂起。换句话说，将发生上下文切换。

## 参数

`pevent` 是指向消息所存入队列的指针。该指针在创建队列时返回给应用程序（参见 `OSCreate()`）。

`msg` 是发送给任务的实际消息。`msg` 是一个指针大小的变量，且取决于应用程序。你绝对不能发布一个 `NULL` 指针。

## 返回值

`OSQPostFront()` 返回这两个错误代码之一：

- 1) `OS_NO_ERR`，如果消息已存入队列
- 2) `OS_Q_FULL`，如果队列已满

## 注意/警告

队列必须在使用之前创建。

## 示例

```c
OS_EVENT *CommQ;

CommRxBuf[100];

void CommTaskRx(void *pdata)

{

INT32 err;

pdata = pdata;

for (;;);

err = OSQPostFront(CommQ, (void *)&CommRxBuf[0]);

if (err == OS_NO_ERR)

/* 消息已存入队列 */

} else {

/* 队列已满 */

}

}
```

# OSQQuery()

| 文件 | 调用来源 | 启用的代码 |
| --- | --- | --- |
| `OS_Q_C` | 任务或 ISR | `OS_MBOX_EN` |

`OSQQuery()` 用于获取消息队列的信息。你的应用程序必须分配一个 `OS_DATA` 结构，用于接收来自消息队列事件控制块的数据。`OSQQuery()` 允许你确定是否有任何任务在队列等待消息、有多少个任务在等待（通过计算 `.EventTbl[]` 中的数量）、队列中有多少条消息、消息队列的大小，并在如果队列中至少有一条消息，检查将返回的下一条消息的内容。注意 `.EventTbl[]` 是由常量 `OS_EVENT_TBL_SIZE` 确定的。

## 参数

`pevent` 是指向消息队列的指针。该指针在创建队列时返回给你（参见 `OSCreate()`）。

`pdata` 是指向数据 `OS_DATA` 的指针，其包含以下字段：

```c
void *Msg;               /* 如果可用，则下一条消息 */
INT16 Msgs;               /* 队列中的消息数 */
INT16 OSSize;               /* 消息队列的大小 */
INT8U EventTbl[OS_EVENT_TBL_SIZE]; /* 等待列表 */
INT8U EventGrp;           /* 等待的任务数 */
```

## 返回值

`OSQQuery()` 返回两个错误代码之一：

- 1) `OS_NO_ERR`，如果调用成功
- 2) `OS_ERR_ARG`，如果你没有传递指向消息队列的指针

## 注意/警告

消息队列必须在使用之前创建。

## 示例

在此示例中，我们检查消息队列的内容以查看有多少个任务在等待它。

```c
OS_EVENT *CommQ;

void Task (void *pdata)

{

    OS_DATA qdata;

    INT32 err;

    INT8U nwait;      /* 等待队列的任务数 */

    pdata = pdata;

    for (;;) {

        err = OSQQuery(CommQ, &qdata);

        if (err == OS_NO_ERR) {

            nwait = 0;        /* 计算等待的任务 */

            if (qdata.EventGrp != 0) {

                for (int i = 0; i < OS_EVENT_TBL_SIZE; i++) {

                    nwait += qdata.EventTbl[i];

                }

            }

        }

    }

}
```

# OSSchedLock()

`void OSSchedLock(void);`

| 文件 | 调用来源 | 启用的代码 |
| --- | --- | --- |
| `OS_CORE.C` | 任务或 ISR | N/A |

`OSSchedLock()` 用于防止重新调度，直到其对应的函数 `OSSchedUnlock()` 被调用。调用 `OSSchedLock()` 的任务即使其他高优先级任务已就绪，也会保持对 CPU 的控制。然而，中断仍然会被识别和处理（假设中断已启用）。µ/OS-II 允许 `OSSchedLock()` 嵌套深度可达 4 层。当调用了等数量的 `OSSchedUnlock()` 时，调度将启用。

## 参数

无

## 返回值

无

## 注意/警告

调用 `OSSchedLock()` 后，你的应用程序不能执行任何会悬挂当前任务执行的系统调用，例如，你的应用程序不能调用 `OSTime()`, `OSTDelay()`, `OSSemPend()` 或 `OSPost()`。由于调度器被锁定，没有任务会被调度。由于调度器被锁定，没有任务会被调度。

## 示例

```c
void Task(void *pdata)

{

    OSSchedLock();

    /* 临界区 */

    OSSchedUnlock();

}
```

由于调度器被锁定，没有任务会被调度。

# OSsemPend()

```c
void OSsemPend(OS_EVENT *pevent, INT16U timeout, INTSU *err);
```

| 文件 | 调用自 | 代码启用 |
| --- | --- | --- |
| `OS_SEM.C` | 仅任务 | `OS_SEM_EN` |

`OSsemPend()` 用于任务获取资源的独占访问、与 ISR 同步或等待直到事件发生。如果任务调用 `OSsemPend()` 且信号量大于 0，则 `OSsemPend()` 将减少信号量并返回给调用者。然而，如果信号量等于 0，`OSsemPend()` 将任务放入信号量的等待列表中。任务将等待任务或 ISR 发送信号量，或者等待超时。如果在超时前发送了信号量，μC/OS-II 将恢复等待信号量的最高优先级任务。被 `OSTSuspend()` 挂起的任务可以通过调用 `OSTResume()` 获取信号量。

## 参数

`pevent` 是信号量的指针。该指针在创建信号量时返回给应用程序（参见 `OSsemCreate()`）。

`timeout` 用于在指定的时钟节拍内未接收到消息时恢复任务执行。`timeout` 值为0 表示任务等待消息。最大 `timeout` 为 65535 时钟节拍。超时值与时钟节拍同步。超时从可能立即发生的时钟节拍开始。

`err` 是变量指针，用于存储错误代码。`OSsemPend()` 将 `err` 设置为：

- 1) `OS_NO_ERR`，信号量可用
- 2) `TIMEOUT`，在规定时间内未收到信号
- 3) `OS_ERR_PEND_ISR`，你在 ISR 中调用了此函数，μC/OS-II 将挂起该 ISR。通常情况下，你不应调用 `OSsemPend()`。

## 返回值

## 注意/警告

信号量在使用前必须创建。

## 示例

```c
OS_EVENT *DispSem;
void DispTask(void *pdata)
{
  INT8U err;

  pdata = pdata;
  for (;;) {
    OSsemPend(DispSem, 0, err);
    /* 任务继续的唯一方式是 ... */
    /* ... 信号量被发送！ */
  }
}
```

# OSSemPost()

| 文件 | 调用自 | 代码启用 |
| --- | --- | --- |
| `OS_SEM.C` | 任务或 ISR | `OS_SEM_EN` |
