
# `OSQAccept()`

```c
void *OSQAccept(OS_EVENT *pevent);
```

| 文件 | 调用来源 | 启用的代码 |
| --- | --- | --- |
| `OS_Q_C` | 任务或 ISR | `OS_Q_EN` |

`OSQAccept()`允许你检查从目标队列是否有可用消息。与`OSQPend()`不同，如果没有可用消息，`OSQAccept()`不会挂起调用任务。如果消息可用，该消息将返回给你的应用程序并从队列中提取出来。此调用通常由 ISR（中断服务程序）使用，因为 ISR 不允许在队列上等待消息。

## 参数

`pevent`是指向要接收消息的消息队列的指针。该指针在创建消息队列时会返回给你的应用程序（参见`OSQCreate()`）。

## 返回值

如果消息可用则返回消息指针；如果消息队列不包含消息，则返回`NULL`。

## 注意事项/警告

消息队列在使用之前必须创建。

## 示例

```c
OS_EVENT *CommQ;

void Task (void *pdata)
{
    void *msg;
    pdata = pdata;
    for (;;) {
        msg = OSQAccept(CommQ); /* 检查队列是否有消息 */
        if (msg != (void*)0) {
            /* 接收到消息，处理 */
        } else {
            /* 未接收到消息，执行 . * */
            /* .. 其他操作 */
        }
    }
}
```

# `OSQCreate()`

```c
OS_EVENT *OSQCreate(void **start, INT8U size);
```

| 文件 | 调用来源 | 启用的代码 |
| --- | --- | --- |
| `OS_Q_C` | 任务或启动代码 | `OS_Q_EN` |

`OSQCreate()`用于创建消息队列。消息队列用于允许任务或 ISR 向一个或多个任务发送指定大小的变量（消息）。所的消息的消息含义取决于应用程序。

## 参数

`start`是消息存储区域的基地址。消息存储区域声明为指向`void`指针的数组。

`size`是消息存储区域的大小（以项数计算）。

## 返回值

`OSQCreate()`返回分配给队列的事件控制块（ECB）的指针。如果没有可用的事件控制块，`OSQCreate()`将返回`NULL`指针。

## 注意事项/警告

队列在使用之前必须创建。

## 示例

```c
OS_EVENT *CommQ;
void *CommMsg[10];
```

```c
void main(void)
{
    OSInit(); /* 初始化 µC/OS-II */
    CommQ = OSQCreate(&CommMsg[0], 10); /* 创建 COMM Q */
    OSStart(); /* 启动多任务 */
}
```

# `OSQFlush()`

```c
INTU *OSQFlush(OS_EVENT *pevent);
```

| 文件 | 调用来源 | 启用的代码 |
| --- | --- | --- |
| `OS_Q.C` | 任务或 ISR | `OS_Q_EN` |

`OSQFlush()`用于清空消息队列的内容，基本上消除了所有发送到队列的消息。无论任务是正在等待队列（此时没有消息）还是队列包含一个或多个消息，该函数的执行时间都是相同的。

## 参数

`pevent`是指向消息队列的指针。该指针在创建消息队列（`OSQCreate()`）时会返回给你的应用程序。

## 返回值

返回以下代码之一：

- `1)` `OS_NO_ERR`，消息队列已刷空。
- `2)` `OS_ERR_EVENT_TYPE`，如果你尝试刷空消息队列以外的对象。

## 注意事项/警告

队列在使用之前必须创建。

## 示例

```c
OS_EVENT *CommQ;

void main(void) {
    INT8U err;
    OSInit();
    /* 初始化 µC/OS-II */
    err = OSQFlush(CommQ);
    OSStart();
    /* 启动多任务 */
}
```

# `OSQPend()`

```c
void *OSQPend(OS_EVENT *pevent, INT16U timeout, INT8U *err);
```

| 文件 | 调用来源 | 启用的代码 |
| --- | --- | --- |
| `OS_Q_C` | 任务 | `OS_Q_EN` |

`OSQPend()`用于从队列接收消息。消息是指定大小的变量，其用途取决于应用程序。如果没有可用消息，`OSQPend()`将挂起调用任务直到消息可用或超时。如果队列中存在消息，则该消息将返回给你的应用程序。

## 参数

`pevent`是指向要接收消息的消息队列的指针。该指针在创建消息队列时（参见`OSQCreate()`）会返回给你的应用程序。

`timeout`是任务等待消息的节数。超时为`0`表示任务不等待。

`err`是用于保存错误代码的变量。

## 返回值

- `1)` `OS_NO_ERR`，接收到消息。
- `2)` `OS_TIMEOUT`，超时发生。
- `3)` `OS_ERR_EVENT_TYPE`，如果你尝试等待消息队列以外的对象。

## 注意事项/警告

消息队列在使用之前必须创建。

## 示例

```c
OS_EVENT *CommQ;

void Task (void *pdata)
{
    void *msg;
    INT8U err;
    pdata = pdata;
    for (;;) {
        msg = OSQPend(CommQ, OS_WAIT_FOREVER, &err); /* 等待消息 */
        if (msg != (void*)0) {
            /* 接收到消息，处理 */
        }
    }
}
```

# `OSQPost()`

| 文件 | 调用来源 | 启用的代码 |
| --- | --- | --- |
| `OS_Q_C` | 任务或 ISR | `OS_Q_EN` |

`OSQPost()`用于通过队列向任务发送消息。消息是指定大小的变量，其用途取决于应用程序。如果队列已满，则向调用者返回错误代码。`OSQPost()`会立即返回调用者并将消息放入队列。如果队列中有任何任务在等待消息，则优先级最高的任务接收该消息。如果等待消息的任务优先级高于发送消息的任务，则高优先级任务将恢复，发送消息的任务将被挂起。换言之，将发生上下文切换。消息队列先进先出（FIFO），这意味着第一个发送的消息将是第一个接收的消息。

`pevent`是指向要放入消息的队列的指针。该指针在创建队列时（参见`OSQCreate()`）会返回给你的应用程序。

`msg`是发送给任务的实际消息。`msg`是指针大小变量，取决于应用程序。绝不能发送`NULL`指针。

## 返回值

- `1)` `OS_NO_ERR`，消息已放入队列
- `2)` `OS_Q_FULL`，如果队列已满

## 注意事项/警告

队列在使用之前必须创建。

## 示例

```c
OS_EVENT *CommQ;
void *CommMsg[100];

void Task(void *pdata)
{
    INT8U err;
    pdata = pdata;
    for (;;) {
        err = OSQPost(CommQ, (void *)CommMsg[0]);
        if (err == OS_NO_ERR) {
            /* 消息已放入队列 */
        } else {
            /* 队列已满 */
        }
    }
}
```
