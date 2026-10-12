
µOS-II 为邮箱提供了五项服务：`OSMCreate()`、`OSMboxPend()`、`OSMboxPost()`、`OSMboxAccept()` 和 `OSMboxQuery()`。图 6-6 显示了任务、ISR 和邮箱之间关系的流程图。注意表示邮箱的符号是一个 I 型梁。邮箱的内容是一个指向消息的指针。指针所指向的内容取决于应用程序。邮箱只能包含一个指针（邮箱已满）或一个指向 NULL 的指针（邮箱为空）。如图 6-6 所示，任务或 ISR 可以调用 `OSMboxPost()`。然而，只允许任务调用 `OSMboxPend()` 和 `OSMboxQuery()`。

![](img/114817931de46def85b7b339e903e24f_149_0.png)

### 6.06.01 创建邮箱, `OSMboxCreate()`

创建邮箱的代码在列表 6.14 中，基本上与 `OSSemCreate()` 相同，不同之处在于 ECB 类型设置为 `OS_EVENT_TYPE_MBOX`，L.14(1)，并且我们没有使用 `.OSEvent` 字段，而是使用 `.OSEventPtr` 字段来处理消息指针 L.14(2)。

`OSMboxCreate()` 返回一个指向 ECB 的指针 L.14(3)。该指针必须在后续调用中使用，用于访问邮箱的 `OSMboxPend()`、`OSMboxPost()`、`OSMboxAccept()` 和 `OSMboxQuery()`。该指针基本上被用作邮箱句柄。注意，如果没有更多的 ECB，`OSMboxCreate()` 将返回一个 NULL 指针。

你应该注意，一旦创建了邮箱，就不能被删除。如果任务正在等待邮箱，删除消息邮箱对象将是“危险”的。

```c
OS_EVENT *OSMboxCreate(void *msg)
{
    OS_EVENT *pevent;
    OS_ENTER_CRITICAL();
    if (OSEventFreeList != (OS_EVENT*)0) {
        OSEventFreeList = (OS_EVENT*)OSEventFreeList->OSEventPtr;
    }
    OS_EXIT_CRITICAL();
    if (pevent != (OS_EVENT*)0) {
        pevent->OSEventType = OS_EVENT_TYPE_MBOX;
        pevent->OSEventPtr = msg;
        OSEventWaitListIn(pevent);
    }
    return (pevent);
}
```

### 列表 6.14，创建邮箱。

### 6.0.02 在邮箱处等待消息, `OsmboxPend`

在邮箱处等待消息的代码在 6.15 中所示。同样，代码是 `OSsemPend`，所以我将只讨论差异。`OsmboxPend` 验证被事件指向的 ECB 已由 `OsmboxCreate()` 创建 6.15(1)。当 `.OSEventPtr` 包含一个非空句针时 (2)，表示消息可用。在这种情况下，`OsmboxPend()` 将消息存储在 `msg` 中，并在 `.OSEventPtr` 中放置一个 NULL 指针以清空邮箱 6.15(3)。同样，这是你寻找的结果。这也是通过 `OsmboxPend()` 的最快路径。

如果消息不可用，`.OSEventPtr` 包含 NULL 指针，你应该检查该内容是否由 ISR 可用 6.15(4)。对于 `OSsemPend()`，你不应该在 ISR 中调用 `OsmboxPend()`，因为无法创建 ISR。我决定添加这种情况这种情况。然而，如果消息是可用的，即使从 ISR 调用 `OsmboxPend()` 也是成功的。通过查看任务 TCB 中的 `.OSTCB` 标志来检查 `OS_STAT_MBOX` 位是否仍设置，可以检测到超时。当该位设置时发生超时 6.15(5)。任务通过调用 `OSEventTO()` 从邮箱等待列表中移除 6.15(8)。注意，指针被设置为 NULL 6.15(9)，因为没有消息发送。如果任务 TCB 中的状态设置了 `OS_STAT_MBOX` 位，则消息已发送。调用的 `OsmboxPend()` 将接收到消息指针 6.15(10)。此外，指向 ECB 的链接被移除 6.15(11)。

```c
void OsmboxPend(OS_EVENT *pevent, INT16 timeout, INT8 *err)
{
    void *msg;

    OS_ENTER_CRITICAL();
    if (pevent->OSEventPtr != OS_EVENT_MBOX) { // (1)
        OS_EXIT_CRITICAL();
        *err = OS_ERR_EVENT_TYPE;
        return (void);
    }

    msg = pevent->OSEventPtr;
    if (msg != (void *)0) { // (2)
        pevent->OSEventPtr = (void *)0;
        OS_EXIT_CRITICAL();
        *err = OS_NO_ERR;
    } else if (timeout > 0) { // (4)
        OS_EXIT_CRITICAL();
        *err = OS_ERR_PEND;
    } else { // (5)
        OSTCBur->OSTCBStat |= OS_STAT_MBOX;
        OSTCBur->OSTCBd = timeout;
        OSEventWait(pevent);
        OS_EXIT_CRITICAL();
        OSCBEND(pevent);
        OS_ENTER_CRITICAL();
        if (OSTCBur->OSTCBsg != (void *)0) { // (6)
            msg = OSTCBur->OSTCBsg;
            OSTCBur->OSTCBStat = OS_STAT_RD;
            OSTCBur->OSEventPtr = (OS_EVENT *)0;
            OS_EXIT_CRITICAL();
            *err = OS_NO_ERR;
        } else if (OSTCBur->OSTCBStat & OS_STAT_MBOX) { // (7)
            OSEVENTTO(pevent); // (8)
            OS_EXIT_CRITICAL();
            msg = (void *)0; // (9)
            *err = OS_TIMEOUT;
        } else {
            msg = pevent->OSEventPtr; // (10)
            pevent->OSEventPtr = (void *)0;
            OSTCBur->OSEventPtr = (OS_EVENT *)0; // (11)
            OS_EXIT_CRITICAL();
            *err = OS_NO_ERR;
        }
    }
    return (msg);
}
```

### 6.0.63 向邮箱发送消息. `OsmboxPost()`

将消息放入邮箱的代码在 6.16 中所示。在确保 ECB 用作邮箱后 6.16(1)，`OsmboxPost()` 检查是否在等待消息到达邮箱 6.16(2)。当 ECB 中的 `OSEventGrp` 包含非零值时，等待消息的任务通过 `OSEventTaskReady()`（见节 6.2 *使任务就绪*）从列表中检索 6.16(3)。如果该任务就绪，则调用 `OSSched()` 检查就绪的任务现在是否是最高优先级的就绪任务。如果是，则将发生上下文切换（仅当从任务调用 `OsmboxPost()` 时）并执行就绪的任务。如果就绪的任务没有等待消息到达邮箱，则消息指针保存在邮箱中 6.16(5)。在邮箱中存储指针允许下一个任务调用 `osxend` 立即获取消息。

你应该注意，如果由 ISR 调用 `OsmboxPost()` 则不会发生上下文切换，因为从 ISR 切换只有在完成调用 `OSExitInt` 时才会发生，并且是最后的嵌套（见节 3.09，µOS 中的中断）。
