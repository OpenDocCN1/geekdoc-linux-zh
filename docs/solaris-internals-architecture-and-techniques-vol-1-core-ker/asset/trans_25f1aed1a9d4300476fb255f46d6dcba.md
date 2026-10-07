
如果您有多个 RT 线程或进程，请考虑是否需要对它们进行优先级排序（以便一个线程或进程比另一个获得处理器时间），并使用 `priocntl(1)` 相应地调整 RT 优先级。

上述建议使您的 RT 能够独占访问处理器（或多个处理器），具体取决于需求以及在处理器集中配置了多少个。您可以在系统和应用程序运行时动态地从处理器集中添加或删除处理器。

图 9.2 显示了 Solaris 支持的各种调度类，以及它们相对于全局（系统级）优先级的相对位置。中断优先级的范围取决于实时类是否加载。

![](img/a86367b95bf21add858c99948ac951c6_393_0.png)

图 9.2 Solaris 调度类与优先级

TS、IA 和 RT 调度类被实现为动态加载的内核模块。TS 类的内核二进制文件位于 `/kernel/sched` 目录；IA 和 RT 类位于 `/usr/kernel/sched` 目录。请注意，IA 类的多数支持函数由 TS 类代码处理。只有少数特定的 IA 类例程。SVS 类是内核的不可缺的一部分，不构建为动态加载模块。核心调度器类（dispatcher class）也是内核的不可缺的一部分，并在启动时与初始 unix 和 genunix 对象一起加载。

从架构角度来看，调度类的实现遵循类似于第 10 章描述的 vfs/vnode 架构的面向对象的设计。正如 vfs/vnode 实现定义的类系统相关和文件系统无关的例程使用宏调用来解析特定文件系统的代码（例如，对于 UFS 文件使用 `VFS_OPEN()` -> `ufs_open()`），内核调度器包含调度类特定的函数和调度类无关的函数；它还使用系统定义的宏来解析类特定的例程。

## 概述

在 Solaris 中，系统类数组在启动时初始化，数组中的每个条目都是一个 `sclass` 结构，每个加载的调度类对应一个。第356页图 9.3 所示的 `sclass` 结构包含以下结构成员：

- *cl_name* — 指向类名的指针（例如，分时系统的 TS）。
- *cl_init* — 指向类特定初始化函数的指针（例如，用于初始化分时类的 `ts_init()`）。
- *cl_funcs* — 指向类函数的指针；一个包含类特定函数指针的内核结构（例如 `fork`、`stop`、`sleep`、`preempt` 等）。
- *cl_lock* — 用于同步访问类结构的内核锁。
- *cl_count* — 计数器，维护尝试加载该类的线程计数。
- *cl_size* — 按线程维护的类数据的大小（字节）。这是通过内核线程的 `t_clidata` 指针引用的结构的大小。

`init` 例程在启动时对所有预加载的调度类进行调用。默认情况下，会加载分时类和系统类。交互类在 X Server 和窗口管理器启动时动态加载。只有实时类（real-time class）在默认环境中不加载。当使用 `proccnt(1)` 命令或 `proccnt(2)` 系统调用将线程设置为实时类时，操作系统将动态加载实时类模块。您可以使用 `dispadmin(1M)` 命令检查运行系统中当前加载了哪些调度类，如下所示。

```
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
```

现在，让我们一个进程放入实时调度类；进程 PID 833 是一个测试程序，它只需睡眠一分钟然后退出。

```
# priocntl -s -c RT -i pid 833
```

然后，我们再次查看系统上加载了哪些调度类：

```
# dispdamin -1
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
```

`crash(1M)` 中的类函数提供了该类、类名、init 函数的内核虚拟地址，以及类操作表地址，后者也称为类函数结构或类操作向量表。（操作向量表是描述指向函数指针数组的通用术语，这正是类函数 `cl_funcs` 结构的内容。）

类函数结构将所有类特定（依赖于调度类）的内核例程的函数指针封装在一起。它们本质上属于以下几类之一：类管理和线程控制。内核切换到特定调度类的适当例程，这与 vfs/vnode 结构中使用的方法本质相同。系统定义了一组宏；这些宏通过索引当前内核线程指针或系统类来解析为类特定函数。系统类和 kthread 结构都维护一个指向类函数结构的指针。例如，类特定的类间函数和退出类函数是通过系统类进行索引的。（必须调用这些函数以允许线程进入或退出调度类，因为内核线程到类操作表的链接尚未建立。）`enter-class` 函数的宏如下所示。

```
#define CL_ENTERCLASS(t, cid, clparsp, credp, bufp) \
(sclass[cid].cl_funcs->thread.cl_enterclass) (t, cid, \
(void *)clparsp, credp, bufp)
```

头文件 <sys/class.h>

## 概述

`enterclass` 例程的参数列表遵循宏 `CL_ENTERCLASS`。在第二行，系统类数组 `sclass[]` 使用类 ID（cid）进行索引（每个调度类都有唯一的类 ID）。通过指向类函数表的指针 `cl_funcs` 进入类特定代码。使用内核线程的宏示例是抢占例程。

```
#define CL_PREEMPT (*tp) ((tp))->cl_preempt
```

这里，`tp` 是指向当前线程的指针，`clfuncs` 是指向类函数表的指针。

以下是类特定例程的完整列表及其功能描述。更多细节请参见后续关于优先级和调度算法的讨论。每个例程名称指示哪个调度类提供了该函数。前五个函数属于类管理类，通常支持 `priocntl(2)` 系统调用，该调用由 `priocntl(1)` 和 `dispatchm(1)` 命令触发。`priocntl(2)` 也可以从应用程序调用。

- *ts_admin, rt_admin* — 获取或更改调度表中的值。
- *ts_getclinfo, ia_getclinfo, rt_getclinfo* — 获取调度类的信息。目前仅返回最大用户优先级（xx_maxupri）。
- *ts_parsmin, ia_parsmin, rt_parsmin* — 验证用户提供的优先级值以确保其在范围内。同时检查调用者的权限以确保请求的操作被允许。对于 TS 和 IA 类，根据最大用户优先级进行限制。对于 RT 类，不存在用户优先级的概念，根据最大 RT 优先级进行范围检查。这些函数支持 `priocntl(2)` 中的 `PC_SETPARMS` 命令。
- *ts_parmsout, rt_parmsout* — 支持 `priocntl(2)` 中的 `PC_GETPARMS` 命令。检索 kthread 的类特定调度参数。
- *ts_getclpri, rt_getclpri, sys_getclpri* — 获取优先级范围。对于每个调度类，返回最小（最低）和最大（最高）全局优先级。

以下函数用于线程支持和管理。

- *ts_enterclass, rt_enterclass, sys_enterclass* — 为线程进入调度类分配所需的资源。对于 TS 类，会分配 `tsproc` 结构。如果请求的类 ID 是 IA（记住，IA

