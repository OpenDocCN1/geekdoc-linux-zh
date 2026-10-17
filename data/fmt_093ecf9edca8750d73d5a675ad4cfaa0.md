
### 3.2.2.3 run_list

`run_list`字段指向运行队列。运行队列包含所有待运行进程的列表。有关运行队列结构体的更多信息，请参阅“基本结构”章节。

## 3.2. array

数组字段指向运行队列的优先级数组。本章的“跟踪进程：基本调度器的构建”部分详细解释了该数组。

### 3.2.2.5 sleep_avg

`sleep_avg`字段用于计算任务的有效优先级，它是任务睡眠的平均时钟滴数。

### 3.2.2.6 timestamp

`timestamp`字段用于在任务睡眠或让出时计算`sleep_avg`。

### 3.2.2.7 interactive_credit

`interactive_credit`字段与`sleep_avg`和`activated`字段一起使用，计算`sleep_avg`。

### 3.2.2.8 policy

策略决定进程的类型（例如分共享或实时）。进程的类型严重影响优先级调度。有关该字段的更多信息，请参阅第7章。

### 3.2.2.9 cpus_allowed

`cpus_allowed`字段指定哪些CPU可能会处理某个任务。这是多处理器系统中指定特定任务可以在哪个CPU上运行的一种方法。

### 3.2.2.10 time_slice

`time_slice`字段定义了允许运行的最大时间。

## 第3章 进程：执行的主要模型

### 3.2.2.11 first_time_slice

`first_time_slice`字段被重复设置为0，并跟踪调度时间。

### 3.2.2.12 activated

`activated`字段跟踪睡眠平均值的递增和减少。如果一个不可中断的任务被唤醒，该字段被设置为-1。

### 3.2.2.13 rt_priority

`rt_priority`是一个静态值，只能通过`schedule()`更新。该值对于支持实时任务是必须的。

### 3.2.2.14 nivscw and nvcsw

存在不同类型的上下文切换。内核为了记录原因跟踪了这些切换。全局切换计数被设置为四种不同的切换计数之一，取决于上下文切换涉及的转换类型（有关上下文切换的更多信息，请参阅第7章）。这些是基本上下文切换的计数器：

- `nivscw`字段（非自愿上下文切换次数）统计应用于任务的内核抢占次数。只有当任务从内核抢占返回且切换计数设置为`nivscw`时，该计数才会递增。
- `nvcsw`字段（自愿上下文切换次数）统计不是基于内核抢占的上下文切换。如果之前的状态不是活跃的抢占，则切换计数设置为`nvcsw`。

## 3.2.3 进程关系相关字段

`task_struct`的以下字段是与进程关系相关的。每个任务或进程$p$都有创建一个它的父进程。进程$p$也可以创建进程，因此可能有子进程。由于$p$的父进程可能创建了多个进程，进程$p$可能有兄弟。图3.4说明了所有这些进程的`task_struct`是如何相关的。

## 3.2 进程描述符

91

![](img/6525157588f931c50a65c5a42af9a432_118_0.png)

图3.4
进程关系

*(注：由于原文中存在大量重复的OCR错误内容，已按要求清理并进行逻辑翻译)*

## 3.2 进程描述符

| task_struct |
| :--- |
| current | ...cap_effective... |
| | ...cap_inheritable... |
| | ...cap_permitted... |
| | keep_capabilities |

图3.6
进程能力相关字段

### 3.2.5.1 cap_effective, cap_inheritable, cap_permitted 和 keep_capabilities

用于支持能力模型的结构在`include/linux/security.h`中定义，类型为无符号32位值。每个32位掩码对应一个能力集（capability set）；每个能力都分配给以下字段中的一个位：

- `cap_effective`。进程当前可以使用的能力。
- `cap_inheritable`。通过`execve`调用传递的能力。
- `cap_permitted`。可以转变为有效能力或可继承能力的的能力。

理解这三种类型之间区别的一种方法，是将“许可能力（permitted capabilities）”比作父母提供的、经过简化的基因池。在父母提供的遗传特质中，我们可以展示其中的一部分（有效特性）并/或将它们传递下去（可继承）。许可能力更多地代表一种可能性，而有效能力则是现实状态。

因此，`cap_effective`和`cap_inheritable`始终是`cap_permitted`的子集。

- `keep_capabilities`。跟踪进程在调用`setuid()`时是丢弃还是保持其能力。

表3.2列出了在`include/linux/capability.h`中定义的一些支持的能力。

#### 表3.2
选定的能力

| 能力 | 描述 |
| :--- | :--- |
| CAP_CHOWN | 忽略`chown()`实施的限制 |
| CAP_FOWNER | 忽略文件权限限制 |
| CAP_FSETID | 忽略文件上的setuid和setgid限制 |
| CAP_KILL | 发送信号时忽略ruid和euid |
| CAP_SETGID | 忽略与uid相关的权限检查 |
| CAP_SETUID | 忽略与uid相关的权限检查 |
| CAP_SETCAP | 允许进程设置其能力 |

内核通过调用`capable`并向能力变量传递参数来检查特定能力是否已设置。通常，该函数检查能力位是否设置在`cap_effective`集中；如果是，它会将`current->flags`设置为`PF_SUPERPRIV`，这表示已授予该能力。如果授予能力，函数返回1；如果未授予则返回0。

三个系统调用与能力的操相关：`capget()`、`capset()`和`prctl()`。前两个允许进程获取和设置其能力，而`prctl()`系统调用则允许操作`current->keep_capabilities`。

### 3.2.6 进程限制相关字段

任务使用由硬件和调度器提供的若干资源。为了跟踪这些资源的使用情况以及可能应用于进程的任何限制，我们拥有以下字段。

### 3.2.6.1 rlim

`rlim`字段包含一个数组，通过维护资源限制值来实现资源的控制和计数。图3.7展示了`task_struct`的`rlim`字段。

![](img/6525157588f931c50a65c5a42af9a432_124_0.png)

图3.7
task_struct资源限制

Linux意识到需要限制进程允许使用的某些资源数量。由于进程使用的资源种类和数量随进程而异，有必要以进程为单位保留这些信息。在进程描述符中还有哪里更合适呢？

`rlimit`描述符（`include/linux/resource.h`）具有`rlim_cur`和`rlim_max`字段，它们是适用于该资源的当前限制和最大限制。限制的“单位”取决于结构所引资源类型。

```c
include/linux/resource.h

struct rlimit {
    unsigned long  rlim_cur;
    unsigned long  rlim_max;
};
```
