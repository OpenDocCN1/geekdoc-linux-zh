
`INT8U OSTaskSuspend(INT8U prio);`

| 文件 | 调用来源 | 启的代码 |
| OS_TASK.C | 任务 | OS_TASK_SUSPEND_EN |

`OSTaskSuspend()`允许你的应用程序无条件地挂起（或阻塞）任务执行。可以通过指定自身的优先级编号或在任务不知道自己的优先级时指定`OS_PRIO_SELF`来挂起调用任务。在这种情况下，需要另一个任务来恢复被挂起的任务。如果当前任务被挂起，将发生重新调度，µ/OS-II将运行下一个就绪的高优先级任务。恢复挂起任务的唯一方法是调用`OSTaskResume()`。

任务挂起是累加的。这意味着如果被挂起的任务被延迟直到'n'个`tick`到期，则只有当时间到达且挂起被移除时，任务才会被恢复。此外，如果被挂起的任务正在等待信号量且信号量被触发，则任务将从信号量等待列表中移除（如果它是等待信号量的最高优先级任务），但在移除挂起状态之前，执行将不会恢复。

### 参数
`prio`指定要挂起的任务的优先级。你可以通过传递`OS_PRIO_SELF`来挂起调用任务，在这种情况下，将执行下一个高优先的任务。

### 返回值
`OSTaskSuspend()`返回以下错误代码之一：
- 1) `OS_NO_ERR`，如果调用成功。
- 2) `OS_TASK_SUSPEND_IDLE`，如果你尝试挂起µC/OS-II的空闲任务。这显然是不允许的。
- 3) `OS_PRIO_INVALID`，如果你指定的优先级高于最大允许值（即你指定的优先级 >= `OS_LOWEST_PRIO`），或者你没有指定`OS_PRIO_SELF`。
- 4) `OS_TASK_SUSPEND_PRIO`，如果你尝试挂起的任务不存在。

### 注意事项/警告
`OSTaskSuspend()`和`OSTaskResume()`必须成对使用。
被挂起的任务只能通过`OSTaskResume()`恢复。

### 示例
```
void TaskX(void *pdata)
{
    INT8U err;

    for (;) {
        err = OSTaskSuspend(OS_PRIO_SELF); /* 挂起当前任务 */
        /* 当另一个任务 .. */
        /* .. 显式恢复此任务时继续执行 */
    }
}
```

## `OSTaskQuery()`
`INT8U OSTaskQuery(INT8U prio, OS_TCB *pdata);`

| 文件 | 调用来源 | 启的代码 |
| --- | --- | --- |
| `OS_TASK.C` | 任务或 ISR | N/A |

`OSTask()`允许你的应用程序获取有关任务的信息。你的应用程序必须分配一个`OS_TCB`数据结构，用于接收目标任务控制块的“快照”。你的副本将包含`OS_TCB`结构中的每个字段。在访问`OS_TCB`结构的内容时应小心，特别是`OSTCBNext`和`OSTCBPrev`，因为它们将分别指向创建任务链中的下一个和上一个`OS_TCB`。

### 参数
`prio`是你想要获取数据的任务的优先级。你可以通过指定`OS_PRIO_SELF`获取有关调用任务的信息。
`pdata`是一个指向`OS_TCB`类型结构体的指针，该结构将包含任务控制块的副本。

### 返回值
`OSTaskQuery()`返回以下两个错误代码之一：
- 1) `OS_NO_ERR`，如果调用成功。
- 2) `OS_PRIO_ERR`，如果你尝试从无效的任务中获取信息。

### 注意事项/警告
任务控制块中的可用字段取决于以下配置选项（参见`OS_CFG`）：
- `OS_TASK_EN`
- `OS_TICK_EN`
- `OS_SEM_EN`
- `OS_DELAY_EN`

### 示例
```
void Task (void *pdata) {
    OS_TCB task_data;
    INT8U err;
    INT8U prio;

    for (;;) {
        prio = OS_PRIO_SELF;
        err = OSTaskQuery(prio, &task_data);
        if (err == OS_NO_ERR) {
            /* 使用 task_data */
        }
    }
}
```

## `OSTaskDelay()`
`void OSTaskDelay(INT2U ticks);`

| 文件 | 调用来源 | 启的代码 |
| `OS_TASK.C` | 任务 | N/A |

`OSTaskDelay()`允许任务挂起指定的`tick`数。任务在指定的时间过去后恢复。

### 参数
`ticks`是要延迟的`tick`数。

### 返回值
`OSTaskDelay()`返回以下错误代码之一：
- 1) `OS_NO_ERR`，如果调用成功。
- 2) `OS_ARG_ERR`，如果`ticks`参数为0。

### 注意事项/警告
`OSTaskDelay()`不应在`ISR`中调用。

### 示例
```
void Task (void *pdata) {
    for (;;) {
        OSTaskDelay(100); /* 延迟 100 个 tick */
    }
}
```

## `OSTaskDelayUntil()`
`void OSTaskDelayUntil(INT32U ticks);`

| 文件 | 调用来源 | 启的代码 |
| `OS_TASK.C` | 任务 | N/A |

`OSTaskDelayUntil()`允许任务挂起直到指定的时间。任务在系统时间到达`ticks`时恢复。

### 参数
`ticks`是任务应该延迟到的系统时间。

### 返回值
`OSTaskDelayUntil()`返回以下错误代码之一：
- 1) `OS_NO_ERR`，如果调用成功。
- 2) `OS_ARG_ERR`，如果`ticks`小于当前时间。

### 注意事项/警告
`OSTaskDelayUntil()`不应在`ISR`中调用。

### 示例
```
void Task (void *pdata) {
    INT32U delay;

    delay = OSTick();
    for (;;) {
        delay += 100;
        OSTaskDelayUntil(delay); /* 延迟 100 个 tick */
    }
}
```

## `OSTaskResume()`
`INT8U OSTaskResume(INT8U prio);`

| 文件 | 调用来源 | 启的代码 |
| `OS_TASK.C` | 任务 | N/A |

`OSTaskResume()`允许恢复被挂起的任务。如果`prio`是`OS_PRIO_SELF`，则恢复调用任务本身。

### 参数
`prio`是要恢复的任务的优先级。如果`prio`是`OS_PRIO_SELF`，则恢复调用任务。

### 返回值
`OSTaskResume()`返回以下错误代码之一：
- 1) `OS_NO_ERR`，如果调用成功。
- 2) `OS_TASK_NOT_EXIST`，如果任务不存在。

### 注意事项/警告
任务不能恢复自己。

### 示例
```
void Task (void *pdata) {
    /* ... 某个任务被挂起 ... */
    OSTaskResume(OS_PRIO_SELF);    /* 恢复任务 */
}
```

`OSTimeDlyResume()`允许应用程序通过调用`OSTimeDly()`或`OSTimeDlyHMSM()`来恢复一个被延迟的任务。

### 参数
`prio`指定要恢复的任务的优先级。

### 返回值
`OSTimeDlyResume()`返回以下错误代码之一：
- 1) `OS_NO_ERR`，如果调用成功。
- 2) `OS_PRIO_INVALID`，如果指定的任务优先级大于`OS_LOWEST_PRIO`。
- 3) `OS_TIME_NOT_DLY`，如果任务没有在等待时间到期。
- 4) `OS_TASK_NOT_EXIST`，如果该任务尚未创建。

### 注意事项/警告
注意，你`绝对不能`调用此函数来恢复正在等待带超时时的事件的任务。这种情况会导致任务看起来像是超时了（除非你想要这种效果）。
你不能恢复一个调用了`OSTimeDlyHMSM()`且组合时间超过65535个`ticks`的任务。换句话说，如果时钟频率为100 Hz，则你将无法恢复调用了`OSTimeDlyHMSM(0, 10, 55, 35)`或更高值的延迟任务。
`(10 分钟 * 60 + 55 秒 + 0.35) * 100 ticks/second`

### 示例
