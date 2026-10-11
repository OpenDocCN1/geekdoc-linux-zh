

```c
struct rlimit rlim [RLIM_NLIMITS];
unsigned short used_math;
char comm [16];
/* 文件系统信息 */
int link_count;
struct tty_struct *tty; /* 如果没有终端则为 NULL */
/* IPC 相关 */
struct sem_undo *semsundo;
struct sem_queue *ssemwaiting;
/* 此任务的 CPU 特定状态 */
struct thread_struct thread;
/* 文件系统信息 */
struct fs_struct *fs;
/* 打开文件信息 */
struct files_struct *files;
/* 信号处理程序 */
spinlock_t sigmask_lock;  /* 保护 signal 和 blocked */
struct signal_struct *sig;
sigset_t signal, blocked;
struct signal_queue *sigqueue, **sigqueue_tail;
unsigned long sas_ss_sp;
size_t sas_ss_size;

/* 线程组跟踪 */
u32 parent_exec_id;
u32 self_exec_id;
/* 字段分配/释放的保护 */
struct semaphore exit_sem;
};

/*
 * 每个进程的标志
 */
#define PF_ALIGNWARN       0x00000001  /* 打印对齐警告消息 */
/* 尚未实现，仅用于 486 */
#define PF_STARTING        0x00000002  /* 正在创建 */
#define PF_EXITING         0x00000004  /* 正在关闭 */
#define PF_PTRACE          0x00000010  /* 如果调用了 ptrace (0) 则设置 */
#define PF_TRACE           0x00000020  /* 跟踪系统调用 */
#define PF_FORKNOEXEC      0x00000040  /* fork 但未 exec */
#define PF_SUPERPRIV       0x00000100  /* 使用了超级用户权限 */
#define PF_DUMPCORE        0x00000200  /* 已转储核心 */
#define PF_SIGNALED        0x00000400  /* 被信号杀死 */
#define PF_MEMALLOC        0x00000800  /* 正在分配内存 */
#define PF_VFORK           0x00001000  /* 在 mm_release 中唤醒父进程 */

#define PF_USEDFPU         0x00100000  /* 任务在此时间片使用了 FPU (SMP) */
#define PF_TRACE           0x00200000  /* 延迟跟踪 (用于 m68k, i386) */

/*
 * 将栈限制设置为某个合理的默认值：root 如果需要
 * 总是可以增加这个限制..  8MB 似乎是合理的。
 */
#define _STK_LIM           (8*1024*1024)

#define DEF_PRIORITY (20*HZ/100) /* 200 ms 时间片 */
/*
 * INIT_TASK 用于设置第一个任务表，修改请
 * 自担风险！Base=0, limit=0x1ffffff (=2MB)
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

#ifndef INIT_TASK_SIZE
# define INIT_TASK_SIZE 2048*sizeof(long)
#endif

union task_union {
 struct task_struct task;
 unsigned long stack[INIT_TASK_SIZE/sizeof(long)];
};

extern union task_union init_task_union;

extern struct mm_struct init_mm;
extern struct task_struct *init_tasks[NR_CPUS];

/* PID 哈希。(这是否应该是动态的？) */
#define PIDHASH_SZ (4096 >> 2)
extern struct task_struct *pidhash[PIDHASH_SZ];

#define pid_hashfn(x) (((x) >> 8) ^ (x)) & (PIDHASH_SZ - 1))

extern __inline__ void hash_pid(struct task_struct *p)
{
    struct task_struct **htable = &pidhash[pid_hashfn(p->pid)];

    if ((p->pidhash_next = *htable) != NULL)
        (*htable)->pidhash_pprev = &p->pidhash_next;
    *htable = p;
    p->pidhash_pprev = htable;
}

extern __inline__ void unhash_pid(struct task_struct *p)
{
    if (p->pidhash_next)
        p->pidhash_next->pidhash_pprev = p->pidhash_pprev;
    *p->pidhash_pprev = p->pidhash_next;
}

extern __inline__ struct task_struct *find_task_by_pid(int pid)
{
    struct task_struct *p, **htable = &pidhash[pid_hashfn(pid)];

    for (p = *htable; p && p->pid != pid; p = p->pidhash_next)
        ;

    return p;
}

/* 按 UID 进行进程收费。 */
extern int alloc_uid(struct task_struct *);
void free_uid(struct task_struct *);

#include <asm/current.h>

extern unsigned long volatile jiffies;
extern unsigned long itimer_ticks;
extern unsigned long itimer_next;
extern struct timeval xtime;
extern void do_timer(struct pt_regs *);

extern unsigned int * prof_buffer;
extern unsigned long prof_len;

extern unsigned long prof_shift;

#define CURRENT_TIME (xtime.tv_sec)

extern void FASTCALL(__wake_up(wait_queue_head_t *q, unsigned int mode));
extern void FASTCALL(__wake_up_sync(wait_queue_head_t *q, unsigned int mode));
extern void FASTCALL(sleep_on(wait_queue_head_t *q));
extern long FASTCALL(sleep_on_timeout(wait_queue_head_t *q,
    signed long timeout));

extern void FASTCALL(interruptible_sleep_on(wait_queue_head_t *q));
extern long FASTCALL(interruptible_sleep_on_timeout(wait_queue_head_t *q,
    signed long timeout));
extern void FASTCALL(wake_up_process(struct task_struct * tsk));

#define wake_up(x)        __wake_up(x,TASK_UNINTERRUPTIBLE | TASK_INTERRUPTIBLE |
                          TASK_EXCLUSIVE)
#define wake_up_all(x)    __wake_up(x,TASK_UNINTERRUPTIBLE | TASK_INTERRUPTIBLE)
#define wake_up_sync(x)   __wake_up_sync(x,TASK_UNINTERRUPTIBLE |
                          TASK_INTERRUPTIBLE | TASK_EXCLUSIVE)
#define wake_up_interruptible(x)   __wake_up(x,TASK_INTERRUPTIBLE | TASK_EXCLUSIVE)
#define wake_up_interruptible_all(x)     __wake_up(x,TASK_INTERRUPTIBLE)
#define wake_up_interruptible_sync(x)    __wake_up_sync(x,TASK_INTERRUPTIBLE |
                                        TASK_EXCLUSIVE)

extern int in_group_p(gid_t);
extern int in_egroup_p(gid_t);

extern void flush_signals(struct task_struct *);
extern void flush_signal_handlers(struct task_struct *);
extern int dequeue_signal(sigset_t *, siginfo_t *);
extern int send_sig_info(int, struct siginfo *, struct task_struct *);
extern int force_sig_info(int, struct siginfo *, struct task_struct *);
extern int kill_pg_info(int, struct siginfo *, pid_t);
extern int kill_s1_info(int, struct siginfo *, pid_t);
extern int kill_proc_info(int, struct siginfo *, pid_t);
extern int kill_something_info(int, struct siginfo *, int);
extern void notify_parent(struct task_struct *, int);
extern void force_sig(int, struct task_struct *);
extern int send_sig(int, struct task_struct *, int);
extern int kill_pg(pid_t, int, int);
extern int kill_s1(pid_t, int, int);
extern int kill_proc(pid_t, int, int);
extern int do_sigaction(int, const struct k_sigaction *, struct k_sigaction *);
extern int do_sigaltstack(const stack_t *, stack_t *, unsigned long);

extern inline int signal_pending(struct task_struct *p)
{
    return (p->sigpending != 0);
}

/* 重新评估任务是否有待发送的信号。
 * 每次 blocked sigset_t 改变时都需要这样做。
 * 所有调用者都应持有 t->sigmask_lock。 */

static inline void recalc_sigpending(struct task_struct *t)
{
	unsigned long ready;
	long i;

	switch (_NSIG_WORDS) {
	default:
		for (i = _NSIG_WORDS, ready = 0; --i >= 0 ;)
			ready |= t->signal.sig[i] &~ t->blocked.sig[i];
		break;

	case 4: ready = t->signal.sig[3] &~ t->blocked.sig[3];
		ready |= t->signal.sig[2] &~ t->blocked.sig[2];
		ready |= t->signal.sig[1] &~ t->blocked.sig[1];
		ready |= t->signal.sig[0] &~ t->blocked.sig[0];
		break;

	case 2: ready = t->signal.sig[1] &~ t->blocked.sig[1];
		ready |= t->signal.sig[0] &~ t->blocked.sig[0];
		break;

	case 1: ready = t->signal.sig[0] &~ t->blocked.sig[0];
	}

	t->sigpending = (ready != 0);
}

/* 如果我们位于备用信号栈上，则返回真。 */

static inline int on_sig_stack(unsigned long sp)
{
	return (sp - current->sas_ss_sp < current->sas_ss_size);
}

static inline int sas_ss_flags(unsigned long sp)
{
	return (current->sas_ss_size == 0 ? SS_DISABLE
			: on_sig_stack(sp) ? SS_ONSTACK : 0);
}

extern int request_irq(unsigned int,
				void (*handler)(int, void *, struct pt_regs *),
				unsigned long, const char *, void *);
extern void free_irq(unsigned int, void *);

/*
 * 现在这变成了一个例程而不是宏，如果
 * 返回真则设置一个标志（以便进行 BSD 风格的计费，当进程使用 root 权限时会被标记）。
 * 这意味着你应该先执行正常的权限检查，最后再检查 user()。
 *
 * [1997 年 12 月 -- Chris Evans]
 * 为了正确性，上述考虑需要扩展到
 * fusser()。这是通过移动 fusser() 检查来实现的
 */
```

