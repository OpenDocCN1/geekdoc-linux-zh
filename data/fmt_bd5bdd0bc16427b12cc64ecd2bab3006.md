
# dispadmin -l

CONFIGURED CLASSES

=====

SYS (System Class)

TS (Time Sharing)

IA (Interactive)

```
或者，为了获取更多信息，`crash(1M)` 工具中有一个类函数。
```

# /etc/crash

dumpfile = /dev/mem, namelist = /dev/ksym, outfile = stdout

> class

SLOT CLASS INIT FUNCTION CLASS FUNCTION

0 SYS 100fdd10 1042c5a0

1 TS 10137c2c 1045ef90

2 IA 10137d0c 1045f080

现在，让我们一个进程放入实时调度类；进程 PID 833 是一个测试程序，它只需睡眠一分钟然后退出。

```
# priocntl -s -c RT -i pid 833
```

然后，我们再次查看系统上加载了哪些调度类：

```
# dispdamin -1
```

CONFIGURED CLASSES

===================

SYS (System Class)

TS (Time Sharing)

IA (Interactive)

RT (Real Time)

# /etc/crash

dumpfile = /dev/mem, namelist = /dev/ksys, outfile = /dev

class

SL CLASS INIT FUNCTION

0 SYS 100ffd10 1042c5a0

1 TS 10137c2c 1045ef90

2 IA 10137d0c 1045f080

3 RT 102025b8 7802f668

`crash(1M)` 中的类函数提供了该类、类名、init 函数的内核虚拟地址，以及类操作表地址，后者也称为类函数结构或类操作向量表。（操作向量表是描述指向函数指针数组的通用术语，这正是类函数 `cl_funcs` 结构的内容。）

类函数结构将所有类特定（依赖于调度类）的内核例程的函数指针封装在一起。它们本质上属于以下几类之一：类管理和线程控制。内核切换到特定调度类的适当例程，这与 vfs/vnode 结构中使用的方法本质相同。系统定义了一组宏；这些宏通过索引当前内核线程指针或系统类来解析为类特定函数。系统类和 kthread 结构都维护一个指向类函数结构的指针。例如，类特定的类间函数和退出类函数是通过系统类进行索引的。（必须调用这些函数以允许线程进入或退出调度类，因为内核线程到类操作表的链接尚未建立。）
`enter-class` 函数的宏如下所示。

```
#define CL_ENTERCLASS(t, cid, clparsp, credp, bufp) \
(sclass[cid].cl_funcs->thread.cl_enterclass) (t, cid, \
(void *)clparsp, credp, bufp)
```

头文件 `<sys/class.h>`

## 概述

`enterclass` 例程的参数列表遵循宏 `CL_ENTERCLASS`。在第二行，系统类数组 `sclass[]` 使用类 ID（`cid`）进行索引（每个调度类都有唯一的类 ID）。通过指向类函数表的指针 `cl_funcs` 进入类特定代码。使用内核线程的宏示例是抢占例程。

```
#define CL_PREEMPT (*tp) ((tp))->cl_preempt
```
