
```c
include/linux/sched.h
384   struct task_struct (
385     volatile long state;
386     struct thread_info *thread_info;
387     atomic_t usage;
388     unsigned long flags;
389     unsigned long ptrace;
390
391     int lock_depth;
392
393     int prio, static_prio;
394     struct list_head run_list;
395     prio_array_t *array;
396
397     unsigned long sleep_avg;
398     long interactive_credit;
399     unsigned long timestamp;
400     int activated;
401
402     unsigned long policy;
403     cpumask_t cpus_allowed;
404     unsigned int time_slice, first_time_slice;
405
406     struct list_head tasks;
407     struct list_head ptrace_children;
408     struct list_head ptrace_list;
409
410     struct mm_struct *mm, *active_mm;
411
413     struct linux_binfmt *binfmt;
414     int exit_code, exit_signal;
415     int pdeath_signal;
416
419     pid_t pid;
420     pid_t tgid;
421
426     struct task_struct * task_struct *real_parent;
427     struct task_struct *parent;
428     struct list_head children;
429 struct list_head_struct sibling;
430 struct task_struct *group_leader;
...
433 struct pid_link_pids[PIDTYPE_MAX];
434
435 wait_queue_head_t wait_child_it;
436 struct completion *fork_done;
437 int __user *set_child_tid;
438 int __user *clear_child_tid;
439
440 unsigned long rt_priority;
441 unsigned long it_real_value, it_prof_value, it_virt_value;
442 unsigned long it_real_incr, it_prof_incr, it_virt_incr;
443 struct timer_list real_time;
444 unsigned long uptime, stime, cstime,
445 unsigned long ncvsw, nicvsw, cncvsw, cncvsw
446 u64 state_time;
...
n450 uid_t uid, euid, sgid, fsuid;
451 gid_t gid, egid, sgid, fsgid, f_sgid;
452 struct group_info *group_info;
453 kernel_cap_t cap_effective, cap_inheritable, cap_permitted;
454 int keep_capabilities:1;
455 struct user_struct *user;
...
n457 struct rlimit rlim[RLIM_NLIMITS];
458 unsigned short used_math;
459 char comm[16];
...
n461 int link_count, total_link_count;
...
467 struct fs *fs;
469 struct files *files;
509 unsigned long exit_code;
510 struct siginfo_t *last_siginfo;
};
```

# 第 3 章 • 执行的主要模型

在内核中，进程描述符是一个名为 `task_struct` 的结构体，它跟踪进程的属性和信息。关于进程的所有内核信息都在那里。在进程的整个生命周期内，进程会与内核的许多方面进行交互，例如内存管理和调度。进程描述符记录了关于这些交互的信息，以及标准的 UNIX 进程属性。内核将所有进程描述符存储在一个名为 `task_list` 的循环链表中。内核还通过全局变量 `current` 保留了指向当前运行进程的 `task_struct` 的引用。（在本书中，我们一直使用 `current` 来表示当前运行进程的进程描述符。）

进程可能由一个或多个线程组成。每个线程都有与其关联的 `task_struct`，包括一个唯一的线程 ID。同一个进程中的线程共享相同的内存地址空间。

以下类别描述了进程描述符在进程生命周期内必须跟踪的一些类型：

- 进程属性
- 进程关系
- 进程内存空间
- 文件管理
- 信号管理
- 进程凭据
- 资源限制
- 调度相关字段

我们现在仔细查看 `task_struct` 结构中的字段。本节描述了它们的作用，并提了该字段涉及的实际处理。尽管许多字段用于与上述类别相关的活动，但某些超出了本书的范围。`task_struct` 结构定义在 `include/linux/sched.h` 中：

```c

include/linux/sched.h

384   struct task_struct (

385     volatile long state;

386     struct thread_info *thread_info;

387     atomic_t usage;

388     unsigned long flags;

389     unsigned long ptrace;

390

391     int lock_depth;

392

393     int prio, static_prio;

394     struct list_head run_list;

395     prio_array_t *array;

396

397     unsigned long sleep_avg;

398     long interactive_credit;

399     unsigned long timestamp;

400     int activated;

401

402     unsigned long policy;

403     cpumask_t cpus_allowed;

404     unsigned int time_slice, first_time_slice;

405

406     struct list_head tasks;

407     struct list_head ptrace_children;

408     struct list_head ptrace_list;

409

410     struct mm_struct *mm, *active_mm;

411

413     struct linux_binfmt *binfmt;

414     int exit_code, exit_signal;

415     int pdeath_signal;

416

419     pid_t pid;

420     pid_t tgid;

421

426     struct task_struct * task_struct *real_parent;

427     struct task_struct *parent;

428     struct list_head children;

429 struct list_head_struct sibling;

430 struct task_struct *group_leader;

...

433 struct pid_link_pids[PIDTYPE_MAX];

434

435 wait_queue_head_t wait_child_it;

436 struct completion *fork_done;

437 int __user *set_child_tid;

438 int __user *clear_child_tid;

439
```
