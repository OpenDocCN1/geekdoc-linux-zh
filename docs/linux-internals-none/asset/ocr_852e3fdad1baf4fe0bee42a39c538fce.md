# The Linux VM Manager

```
#define DEF_PRIORITY (20*HZ/100) /* 200 ms time slices */
/*
 * INIT_TASK is used to set up the first task table, touch at
 * your own risk! Base=0, limit=0x1ffffff (=2MB)
 */
#define INIT_TASK(tsk) \
(
 state: 0, \
 flags: 0, \
 sigpending: 0, \
 addr_limit: KERNEL_DS, \
 exec_domain: &default_exec_domain, \
 lock_depth: -1, \
 counter: DEF_PRIORITY, \
 priority: DEF_PRIORITY, \
 policy: SCHED_OTHER, \
 mm: NULL, \
 active_mm: &init_mm, \
 run_list: LIST_HEAD_INIT(tsk.run_list), \
 next_task: &tsk, \
 prev_task: &tsk, \
 p_opptr: &tsk, \
 p_pptr: &tsk, \
 wait_chldexit: __WAIT_QUEUE_HEAD_INITIALIZER(tsk.wait_chldexit), \
 real_timer: { \
 function: it_real_fn \
 }, \
 cap_effective: CAP_INIT_EFF_SET, \
 cap_inheritable: CAP_INIT_INH_SET, \
 cap_permitted: CAP_FULL_SET, \
 rlim: INIT_RLIMITS, \
 comm: "swapper", \
 thread: INIT_THREAD, \
 fs: &init_fs, \
 files: &init_files, \
 sigmask_lock: SPIN_LOCK_UNLOCKED, \
 sig: &init_signals, \
 signal: ({0}), \
 blocked: ({0}), \
 sigqueue: NULL, \
 sigqueue_tail: &tsk.sigqueue, \
 exit_sem: __MUTEX_INITIALIZER(tsk.exit_sem)
)
```

```
#ifndef INIT_TASK_SIZE
# define INIT_TASK_SIZE 2048*sizeof(long)
#endif
```

```
union task_union {
 struct task_struct task;
 unsigned long stack[INIT_TASK_SIZE/sizeof(long)];
```