
### 2.3 Scheduler

11. If the prev (current) task is in TASK_RUNNING state, then the current goodness is set to its goodness and it is marked as a better candidate to be scheduled than the idle task.

12. Now the runqueue is examined and a goodness of each process that can be scheduled on this cpu is compared with current value; the process with highest goodness wins. Now the concept of "can be scheduled on this cpu" must be clarified: on UP, every process on the runqueue is eligible to be scheduled; on SMP, only process not already running on another cpu is eligible to be scheduled on this cpu. The goodness is calculated by a function called $goodness()$, which treats realtime processes by making their goodness very high $(1000 + p->rt_priority)$, this being greater than 1000 guarantees that no SCHED_OTHER process can win; so they only contend with other realtime processes that may have a greater $p->rt_priority$. The goodness function returns 0 if the process' time slice ($p->counter$) is over. For non-realtime processes, the initial value of goodness is set to $p->counter$ – this way, the process is less likely to get CPU if it already had it for a while, i.e. interactive processes are favoured more than CPU bound number crunchers. The arch-specific constant $PROC\_CHANGE\_PENALTY$ attempts to implement "cpu affinity" (i.e. give advantage to a process on the same CPU). It also gives a slight advantage to processes with mm pointing to current $active\_mm$ or to processes with no (user) address space, i.e. kernel threads. The

13. if the current value of goodness is 0 then the entire list of processes (not just the ones on the runqueue!) is examined and their dynamic priorities are recalculated using simple algorithm:

```c
recalculate:
(
        struct task_struct *p;
        spin_unlock_irq(&runqueue_lock);
        read_lock(&tasklist_lock);
        for_each_task(p)
                p->counter = (p->counter >> 1) + p->priority;
        read_unlock(&tasklist_lock);
        spin_lock_irq(&runqueue_lock);
)
```

Note that we drop the `runqueue_lock` before we recalculate. The reason is that we go through entire set of processes; this can take a long time, during which the `schedule()` could be called on another CPU and select a process with goodness good enough for that CPU, whilst we on this CPU were forced to recalculate. Ok, admittedly this is somewhat inconsistent because while we (on this CPU) are selecting a process with the best goodness, `schedule()` running on another CPU could be recalculating dynamic priorities.

14. From this point on it is certain that `next` points to the task to be scheduled, so we initialise `next->has_cpu` to 1 and `next->processor` to `this_cpu`. The `runqueue_lock` can now be unlocked.

15. If we are switching back to the same task (`next == prev`) then we can simply reacquire the global kernel lock and return, i.e. skip all the hardware-level (registers, stack etc.) and VM-related (switch page directory, recalculate `active_mm` etc.) stuff.

16. The macro `switch_to()` is architecture specific, on i386, it is concerned with a) FPU handling, b) LDT handling, c) reloading segment registers, d) TSS handling and e) reloading debug registers.

## 2.4 Linux linked list implementation

Before we go on to examine implementation of wait queues, we must acquaint ourselves with the Linux standard doubly-linked list implementation. Wait queues (as well as everything else in Linux) make heavy use of them and they are called in jargon "list.h implementation" because the most relevant file is `list.h`.

include/linux/list.h.

The fundamental data structure here is `struct list_head`:

```c
struct list_head {
    struct list_head *next, *prev;
};

#define LIST_HEAD_INIT(name) { &(name), &(name) }

#define LIST_HEAD(name) \
    struct list_head name = LIST_HEAD_INIT(name)

#define INIT_LIST_HEAD(ptr) do { \
    (ptr)->next = (ptr); (ptr)->prev = (ptr); \
} while (0)

#define list_entry(ptr, type, member) \
    ((type *)((char *)(ptr)-(unsigned long)(&(type *)0)->member)))

#define list_for_each(pos, head) \
    for (pos = (head)->next; pos != (head); pos = pos->next)
```

The first three macros are for initialising an empty list by pointing both `next` and `prev` pointers to itself. It is obvious from C syntactic restrictions which ones should be used where – for example, `LIST_HEAD_INIT()` can be used for structure’s element initialisation in declaration, the second can be used for static variable initialising declarations and the third can be used inside a function.

The macro `list_entry()` gives access to individual list element, for example (from fs/file_table.c:fs_may_remount_ro()):

```c
struct super_block {
    ...
    struct list_head s_files;
    ...
} *sb = &some_super_block;

struct file {
    ...
    struct list_head f_list;
    ...
} *file;

struct list_head *p;
for (p = sb->s_files.next; p != &sb->s_files; p = p->next) {
    struct file *file = list_entry(p, struct file, f_list);
    do something to 'file'
}
```

A good example of the use of `list_for_each()` macro is in the scheduler where we walk the runqueue looking for the process with highest goodness:

```c
static LIST_HEAD(runqueue_head);
struct list_head *tmp;
struct task_struct *p;
list_for_each(tmp, &runqueue_head) {
    p = list_entry(tmp, struct task_struct, run_list);
    if (can_schedule(p)) {
        int weight = goodness(p, this_cpu, prev->active_mm);
        if (weight > c)
            c = weight, next = p;
    }
}
```

Here, p->run_list is declared as struct list_head run_list inside task_struct structure and serves as anchor to the list. Removing an element from the list and adding (to head or tail of the list) is done by `list_del()` / `list_add()` / `list_add_tail()` macros. The examples below are adding and removing a task from runqueue:

```c
static inline void del_from_runqueue(struct task_struct * p)
{
    nr_running--;
    list_del(&p->run_list);
    p->run_list.next = NULL;
}

static inline void add_to_runqueue(struct task_struct * p)
{
    list_add(&p->run_list, &runqueue_head);
    nr_running++;
}

static inline void move_last_runqueue(struct task_struct * p)
{
    list_del(&p->run_list);
    list_add_tail(&p->run_list, &runqueue_head);
}

static inline void move_first_runqueue(struct task_struct * p)
{
    list_del(&p->run_list);
    list_add(&p->run_list, &runqueue_head);
}
```

## 2.5 Wait Queues

When a process requests the kernel to do something which is currently impossible but that may become possible later, the process is put to sleep and is woken up when the request is more likely to be satisfied. One of the kernel mechanisms used for this is called a 'wait queue'.

Linux implementation allows wake\-up semantics using TASK\_EXCLUSIVE flag. With waitqueues, you can either use a well\-known queue and then simply `sleep_on` / `sleep_on_timeout` / `interruptible_sleep_on` / `interruptible_sleep_on_timeout`, or you can define your own waitqueue and use add/remove\_wait\_queue to add and remove yourself from it and `wake_up/wake_up_interruptible()` to wake up when needed.

An example of the first usage of waitqueues is interaction between the page allocator (in mm/page_alloc.c; `__alloc_pages()`) and the kswapd kernel daemon (in mm/vmscan.c; kswap()), by means of wait queue kswapd_wait, declared in mm/vmscan.c; the kswapd daemon sleeps on this queue, and it is woken up whenever the page allocator needs to free up some pages.

An example of autonomous waitqueue usage is interaction between user process requesting data via `read(2)` system call and kernel running in the interrupt context to supply the data. An interrupt handler might look like (simplified `drivers/char/rtc_interrupt()`):

```c
static DECLARE_WAIT_QUEUE_HEAD(rtc_wait);
void rtc_interrupt(int irq, void *dev_id, struct pt_regs *regs)
{
    spin_lock(&rtc_lock);
    rtc_irq_data = CMOS_READ(RTC_INTR_FLAGS);
    spin_unlock(&rtc_lock);
    wake_up_interruptible(&rtc_wait);
}
```

So, the interrupt handler obtains the data by reading from some device-specific I/O port (CMOS_READ() macro turns into a couple outb/inb) and then wakes up whoever is sleeping on the `rtc_wait` wait queue.

Now, the `read(2)` system call could be implemented as:

```c
ssize_t rtc_read(struct file file, char *buf, size_t count, off_t *ppos)
{
    DECLARE_WAITQUEUE(wait, current);
    unsigned long data;
    ssize_t retval;
    add_wait_queue(&rtc_wait, &wait);
    current->state = TASK_INTERRUPTIBLE;
    do {
        spin_lock_irq(&rtc_lock);
        data = rtc_irq_data;
        rtc_irq_data = 0;
        spin_unlock_irq(&rtc_lock);

        if (data != 0)
            break;

        if (file->f_flags & O_NONBLOCK) {
            retval = -EAGAIN;
            goto out;
        }
        if (signal_pending(current)) {
            retval = -ERESTARTSYS;
            goto out;
        }
        schedule();
    }
}
```
