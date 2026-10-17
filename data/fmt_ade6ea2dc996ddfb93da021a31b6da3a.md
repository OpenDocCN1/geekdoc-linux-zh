
```
struct vm_area_struct * mmap_avl; /* tree of VMAs */
struct vm_area_struct * mmap_cache; /* last find_vma result */
pgd_t * pgd;
atomic_t mm_users; /* How many users with user space? */
atomic_t mm_count; /* How many references to "struct mm_struct" (users count as 1) */
int map_count; /* number of VMAs */
struct semaphore mmap_sem;
spinlock_t page_table_lock;
unsigned long context;
unsigned long start_code, end_code, start_data, end_data;
unsigned long start_brk, brk, start_stack;
unsigned long arg_start, arg_end, env_start, env_end;
unsigned long rss, total_vm, locked_vm;
unsigned long def_flags;
unsigned long cpu_vm_mask;
unsigned long swap_cnt; /* number of pages to swap on next pass */
unsigned long swap_address;
/*
 * This is an architecture-specific pointer: the portable
 * part of Linux does not know about any segments.
 */
void * segments;
};

#define INIT_MM(name) { \
    &init_mmap, NULL, NULL, \
    swapper_pg_dir, \
    ATOMIC_INIT(2), ATOMIC_INIT(1), 1, \
    __MUTEX_INITIALIZER(name.mmap_sem), \
    SPIN_LOCK_UNLOCKED,
    0, \
    0, 0, 0, 0, \
    0, 0, 0, \
    0, 0, 0, \
    0, 0, 0, \
    0, 0, 0, 0, NULL }

struct signal_struct {
    atomic_t count;
    struct k_sigaction action[_NSIG];
    spinlock_t siglock;
};

#define INIT_SIGNALS { \
    ATOMIC_INIT(1), \
    { {{0,}}, }, \
    SPIN_LOCK_UNLOCKED }

/* Some day this will be a full-fledged user tracking system.
 * Right now it is only used to track how many processes a
 * user has, but it has the potential to track memory usage etc.
 */
struct user_struct;

struct task_struct {
    /* these are hardcoded - don't touch */
    volatile long state;    /* -1 unrunnable, 0 runnable, >0 stopped */
    unsigned long flags;    /* per process flags, defined below */
    int sigpending;
    mm_segment_t addr_limit;        /* thread address space:
                0-0xBFFFFFFF for user-thread
                0-0xFFFFFFFF for kernel-thread
        */
    struct exec_domain *exec_domain;
    volatile long need_resched;

    cycles_t avg_slice;
    int lock_depth;         /* Lock depth. We can context switch in and out
                                of holding a syscall kernel lock... */
    /* begin intel cache line */
    long counter;
    long priority;
    unsigned long policy;
    /* memory management info */
    struct mm_struct *mm, *active_mm;
    int has_cpu;
    int processor;
    struct list_head run_list;
    struct task_struct *next_task, *prev_task;
    int last_processor;

    /* task state */
    struct linux_binfmt *binfmt;
    int exit_code, exit_signal;
    int death_signal; /*  The signal sent when the parent dies  */
    /* ??? */
    unsigned long personality;
    int dumpable:1;
    int dis_exec:1;
    pid_t pid;
    pid_t pgrp;
    pid_t tty_old_pgrp;
    pid_t session;
    /* boolean value for session group leader */
    int leader;
    /*
    * pointers to (original) parent process, youngest child, younger sibling,
    * older sibling, respectively.  (p->father can be replaced with
    * p->p_ptr->pid)
    */
    struct task_struct *p_opptr, *p_pptr, *p_cptr, *p_ystr, *p_osptr;

    /* PID hash table linkage. */
    struct task_struct *pidhash_next;
    struct task_struct **pidhash_pprev;

    wait_queue_head_t wait_chldexit;        /* for wait4() */
    struct semaphore *vfork_sem;            /* for vfork() */
}
```
