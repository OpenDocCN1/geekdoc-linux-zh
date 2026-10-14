
```c
40         sigval_t _sigval;

41     } _rt;

44     struct {

45         pid_t _pid;

46         uid_t _uid;

47         int_status;

48         clock_t utime;

49         clock_t _stime;

50     } _sigchld;

53     struct {

54         void*_addr;

55     } _sigfault;

58     struct {

59         int_band;

60         int_fd;

61     } _sigpoll;

62     } _sigfields;

63 } siginfo_t;
```

Figure 17.9 The siginfo structure

- 11 This extended information about a signal is recorded in a struct siginfo, or siginfo_t, as shown in Figure 17.9, from `<asm-i386/siginfo.h>`. Because different information is needed over different signals, the body of the structure is a large union, with options for different types of signal. This makes it look more complicated than it really is.

93 当此位被设置时，处理程序在信号传递后会被清除，并针对该信号的后续发生设置为 `SIG_DFL`。

97 处理程序必须在禁用中断的情况下执行。

99 这是一个占位符，出于历史原因仍然在那里。它不应用于新的处理程序。

121 此位仅供 PCI 和 EISA 设备的中断处理程序使用。它意味着处理程序支持中断线路的共享。

## 17.1.4 待处理信号队列

上一节检查了进程如何跟踪每个不同信号的句柄，但 `task_struct` 还有另一个指针字段，`pending`。它指向一个链表数据结构的表头，每个数据结构代表一个待处理的信号。

### 17.1.4.1 表示待处理队列的数据结构

用于实现这些待处理信号队列的数据结构如图 17.7 所示，来自 `<linux/signal.h>`。

```c
12 struct sigqueue {
13   struct sigqueue *next;
14   siginfo_t info;
15 };
1
17 struct sigpending {
18   struct sigqueue *head, **tail;
19   sigset_t signal;
20 };
```

图 17.7 信号队列的数据结构

- 12–15 此结构表示一个队列的一个实例。
- 13 这是（链式）队列的链接指针。
- 14 此字段包含有关信号的信息。它是一个 `struct siginfo_t` 结构体（见第 17.1.5.1 节）。
- 17–20 这是队列的头节点。它从挂载这些信号的进程的 `task_struct` 中的 `pending` 字段链接而来。
- 18 这是头指针，指向队列中的第一个元素。尾指针始终设置为最后一个条目的的 `next` 字段。
- 19 这是一个位图（见第 17.1.1 节）。每个位代表一个信号，如果该信号处于待处理状态，则该位就会被设置。它用于在搜索整个队列之前查找哪些信号（如果有）处于待处理状态。

### 17.1.4.2 为进程初始化 sigpending 结构

每个进程在它的 `task_struct` 中都有 `pending` 字段。这是一个 `struct sigpending` 结构体（见第 2.8 节）。该结构由图 17.8 所示的函数初始化，来自 `<linux/signal.h>`。

```c
214 static inline void init_sigpending(struct sigpending*sig)
215 {
216     sigmptset(&sig->signal);
217     sig->head = NULL;
218     sig->tail = &sig->head;
219 }
```

图 17.8 为进程初始化 sigpending 结构

- 我们将 `struct sigpending` 结构中 `signal` 字段的指针传递给此函数（见第 17.2.2.4 节），将其清除其中所有的位。
- 头指针设置为 `NULL`。
- 尾指针设置为 `struct sigpending` 结构中的 `head` 字段。

## 17.1.5 关于信号的扩展信息

信号机制的原始实现记录了信号处于待处理状态的事实。现代版本的 Unix 从发送者向目标进程传递大量的信号信息。本节检查了这些信息是如何封装的。

### 17.1.5.1 The siginfo structure

关于信号的扩展信息记录在 `struct siginfo`，或 `siginfo_t` 中，如图 17.9 所示，来自 `<asm-i386/siginfo.h>`。由于不同的信号需要不同的信息，结构体的体是一个大的联合，为不同类型的信号提供了选项。这使其看起来比实际上要复杂。

```c
8  typedef union sigval {
9      int sival_int;
10     void *sival_ptr;
11 } sigval_t;
12 
13 #define SI_MAX_SIZE    128
14 #define SI_PAD_SIZE    ((SI_MAX_SIZE/sizeof(int)) - 3)
15 
16 typedef struct siginfo {
17     int si_signo;
18     int si_errno;
19     int si_code;
20
```
```c
21 union {
22     int_pad[SI_PAD_SIZE];
25     struct {
26         pid_t _pid;
27         uid_t _uid;
28     } _kill;
31     struct {
32         unsigned int_timer1;
33         unsigned int_timer2;
34     _timer;
37     struct {
38         pid_t _pid;
39         uid_t _uid;
40         sigval_t _sigval;
41     } _rt;
44     struct {
45         pid_t _pid;
46         uid_t _uid;
47         int_status;
48         clock_t utime;
49         clock_t _stime;
50     } _sigchld;
53     struct {
54         void*_addr;
55     } _sigfault;
58     struct {
59         int_band;
60         int_fd;
61     } _sigpoll;
62     } _sigfields;
63 } siginfo_t;
```
