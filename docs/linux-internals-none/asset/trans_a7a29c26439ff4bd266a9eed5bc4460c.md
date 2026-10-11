

```c
               fd_set close_on_exec_init;
               fd_set open_fds_init;
               struct file * fd_array[NR_OPEN_DEFAULT];
       };

#define INIT_FILES { \
                ATOMIC_INIT(1), \
                RW_LOCK_UNLOCKED, \
                NR_OPEN_DEFAULT, \
                __FD_SETSIZE, \
                0, \
                &init_files.fd_array[0], \
                &init_files.close_on_exec_init, \
                &init_files.open_fds_init, \
                { { 0, } }, \
                { { 0, } }, \
                { NULL, } \
      }

struct fs_struct {
                atomic_t count;
                int umask;
                struct dentry * root, * pwd;
      };

#define INIT_FS { \
                ATOMIC_INIT(1), \
                0022, \
                NULL, NULL \
      }

/* 最大活动映射区域数。这是一个随机的（大）数字 */
#define MAX_MAP_COUNT     (65536)

/* 激活 AVL 树时的映射区域数量。这是任意选择的。 */
#define AVL_MIN_MAP_COUNT 32

struct mm_struct {
                struct vm_area_struct * mmap;         /* VMA 列表 */
                struct vm_area_struct * mmap_avl;     /* VMA 树 */
                struct vm_area_struct * mmap_cache;   /* 最近一次 find_vma 的结果 */
                pgd_t * pgd;
                atomic_t mm_users;                   /* 有多少用户处于用户空间？ */
                atomic_t mm_count;                    /* 对 "struct mm_struct" 的引用计数（用户计数为 1） */
                int map_count;                        /* VMA 的数量 */
                struct semaphore mmap_sem;
                spinlock_t page_table_lock;
                unsigned long context;
                unsigned long start_code, end_code, start_data, end_data;
                unsigned long start_brk, brk, start_stack;
                unsigned long arg_start, arg_end, env_start, env_end;
                unsigned long rss, total_vm, locked_vm;
                unsigned long def_flags;
                unsigned long cpu_vm_mask;
                unsigned long swap_cnt; /* 下一次路径中需要换出的页面数 */
                unsigned long swap_address;
                /**
                 * 这是一个架构特定的指针：Linux 的可移植部分
                 * 不知道任何关于段的信息。
                 */
                void * segments;
      };

#define INIT_MM(name) {
        &init_mmmap, NULL, NULL,
        swapper_pg_dir,
        ATOMIC_INIT(2), ATOMIC_INIT(1), 1,
        __MUTEX_INITIALIZER(name.mmmap_sem),
        SPIN_LOCK_UNLOCKED,
        0,
        0, 0, 0, 0,
        0, 0, 0,
        0, 0, 0, 0,
        0, 0, 0,
        0, 0, 0, 0, NULL }

struct signal_struct {
        atomic_t count;
        struct k_sigaction action[_NSIG];
        spinlock_t siglock;
      };

#define INIT_SIGNALS {
        ATOMIC_INIT(1),
        { {{0}}, },
        SPIN_LOCK_UNLOCKED }

/**
 * 有一天，这将是一个完整的用户跟踪系统。
 * 目前它仅用于跟踪用户拥有多少个进程，
 * 但它具有跟踪内存使用量等的潜力。
 */
struct user_struct;

struct task_struct {
        /* 这些是硬编码的 - 请勿触碰 */
        volatile long state; /* -1 不可运行, 0 可运行, >0 停止 */
        unsigned long flags; /* 每进程标志，定义如下 */
        int sigpending;
        mm_segment_t addr_limit; /* 线程地址空间：
                                    用户线程为 0-0xBFFFFFFF
                                    内核线程为 0-0xFFFFFFFF
                                    */
        struct exec_domain *exec_domain;
        volatile long need_resched;

        cycles_t avg_slice;
        int lock_depth; /* 锁深度。我们可以进出系统调用内核锁的持有状态... */

        /* 开始 intel 缓存行 */
        long counter;
        long priority;
        unsigned long policy;
        /* 内存管理信息 */
        struct mm_struct *mm, *active_mm;
        int has_cpu;
        int processor;
        struct list_head run_list;
        struct task_struct *next_task, *prev_task;
        int last_processor;

        /* 任务状态 */
        struct linux_binfmt *binfmt;
        int exit_code, exit_signal;
        int pdeath_signal; /* 父进程死亡时发送的信号 */
        /* ??? */
        unsigned long personality;
        int dumpable:1;
        int did_exec:1;
        pid_t pid;
        pid_t pgrp;
        pid_t tty_old_pgrp;
        pid_t session;
        /* 会话组领导的布尔值 */
        int leader;
        /*
         * 指向（原始）父进程、最年幼的子进程、较年幼的兄弟进程、
         * 较年长的兄弟进程的指针，分别对应。（p->father 可以用
         * p->p_ptr->pid 替代）
         */
        struct task_struct *p_opptr, *p_pptr, *p_cptr, *p_ysptr, *p_osptr;

        /* PID 哈希表链接。 */
        struct task_struct *pidhash_next;
        struct task_struct **pidhash_pprev;

        wait_queue_head_t wait_chldexit; /* 用于 wait4() */
        struct semaphore *vfork_sem; /* 用于 vfork() */
        unsigned long rt_priority;
        unsigned long it_real_value, it_prof_value, it_virt_value;
        unsigned long it_real_incr, it_prof_incr, it_virt_incr;
        struct timer_list real_timer;
        struct tms times;
        unsigned long start_time;
        long per_cpu_utime[NR_CPUS], per_cpu_stime[NR_CPUS];
        /* 内存错误和交换信息：这可以被看作是 mm 特定的，或者
            线程特定的 */
        unsigned long min_flt, maj_flt, nswap, cmin_flt, cmaj_flt, cswap;
        int swappable:1; /* 进程凭证 */
        uid_t uid, euid, suid, fsuid;
        gid_t gid, egid, sgid, fsgid;
        int ngroups;
        gid_t groups[NGROUPS];
        kernel_cap_t cap_effective, cap_inheritable, cap_permitted;
        struct user_struct *user;
        /* 限制 */
        struct rlimit rlim[RLIM_NLIMITS];
        unsigned short used_math;
        char comm[16];
        /* 文件系统信息 */
        int link_count;
        struct tty_struct *tty; /* 如果没有 tty 则为 NULL */
        /* IPC 相关 */
        struct sem_undo *semundo;
        struct sem_queue *semsleeping;
        /* 此任务的 CPU 特定状态 */
        struct thread_struct thread;
        /* 文件系统信息 */
        struct fs_struct *fs;
        /* 打开文件信息 */
        struct files_struct *files;
        /* 信号处理程序 */
        spinlock_t sigmask_lock; /* 保护信号和阻塞状态 */
        struct signal_struct *sig;
        sigset_t signal, blocked;
        struct signal_queue *sigqueue, **sigqueue_tail;
        unsigned long sas_ss_sp;
        size_t sas_ss_size;
        /* 线程组跟踪 */
        u32 parent_exec_id;
        u32 self_exec_id;
        /* 保护字段分配/释放 */
        struct semaphore exit_sem;
};

/* 每进程标志 */
#define PF_ALIGNWARN  0x00000001 /* 打印对齐警告消息 */
                                /* 尚未实现，仅用于 486 */
#define PF_STARTING   0x00000002 /* 正在创建 */
#define PF_EXITING    0x00000004 /* 正在关闭 */
#define PF_TRACED     0x00000010 /* 如果调用了 ptrace (0) 则设置 */
#define PF_TRACESYS   0x00000020 /* 正在跟踪系统调用 */
#define PF_FORKNOEXEC 0x00000040 /* 已 fork 但未 exec */
#define PF_SUPERPRIV  0x00000100 /* 使用了超级用户权限 */
#define PF_DUMPCORE   0x00000200 /* 已转储核心 */
#define PF_SIGNALED   0x00000400 /* 被信号杀死 */
#define PF_MEMALLOC   0x00000800 /* 正在分配内存 */
#define PF_VFORK      0x00001000 /* 在 mm_release 中唤醒父进程 */
#define PF_USEDGPU    0x00100000 /* 任务在此量子中使用了 FPU (SMP) */
#define PF_TRACE      0x00200000 /* 延迟跟踪 (用于 m68k, i386) */

/*
 * 将堆栈限制在一个合理的默认值：root 总是可以
 * 在需要时增加此限制。8MB 似乎很合理。
 */
#define _STK_LIM (8*1024*1024)

#define DEF_PRIORITY (20*HZ/100) /* 200 毫秒时间片 */

/*
 * INIT_TASK 用于设置第一个任务表，
 * 使用它风险自负！Base=0, limit=0x1ffffff (=2MB)
 */
#define INIT_TASK(name) \
/* 状态等 */ { 0,0,0,KERNEL_DS,&default_exec_domain,0, \
/* avg_slice */ 0, -1, \
/* counter */ DEF_PRIORITY,DEF_PRIORITY,SCHED_OTHER, \
/* mm */ NULL, &init_mm, \
/* has_cpu */ 0,0, \
/* run_list */ LIST_HEAD_INIT(init_task.run_list), \
/* next_task */ &init_task,\&init_task, \
/* last_proc */ 0, \
/* binfo */ NULL, \
/* ec,brk,.. */ 0,0,0,0,0,0, \
/* pid 等 */ 0,0,0,0,0,0, \
/* 进程链接 */ &init_task,&init_task,NULL,NULL,NULL, \
/* pidhash */ NULL, NULL, \
/* chld wait */ __WAIT_QUEUE_INITIALIZER(name.wait_chldexit), NULL, \
/* timeout */ 0,0,0,0,0,0,0, \
/* timer */ { NULL, NULL, 0, 0, it_real_fn }, \
/* utime */ {0,0,0,0},0, \
/* 每 CPU 时间 */ { 0 }, {0 }, \
/* fil */ 0,0,0,0,0,0, \
/* swp */ 0, \
/* 进程凭证 */ \
/* uid 等 */ 0,0,0,0,0,0,0,0, \
/* 补充组 */ 0, {0}, \
/* caps */ CAP_INIT_EFF_SET,CAP_INIT_INH_SET,CAP_FULL_SET, \
/* user */ NULL, \
/* rlimits */ INIT_RLIMITS, \
/* math */ 0, \
/* comm */ "swapper", \
/* fs 信息 */ 0,NULL, \
/* ipc */ NULL, NULL, \
/* thread */ INIT_THREAD, \
/* fs */ &init_fs, \
/* files */ &init_files, \
/* signals */ SPIN_LOCK_UNLOCKED, &init_signals, { {0} }, { {0} }, NULL, \
&init_task.sigqueue, 0, 0, \
/* exec cts */ 0,0, \
/* exit_sem */ __MUTEX_INITIALIZER(name.exit_sem),
```

