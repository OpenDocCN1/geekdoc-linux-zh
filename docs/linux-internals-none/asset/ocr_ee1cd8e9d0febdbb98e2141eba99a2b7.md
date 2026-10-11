# The Linux VM Manager

```
```c
#define CT_TO_SECS(x)    ((x) / HZ)
#define CT_TO_USECS(x)   (((x) % HZ) * 1000000/HZ)

extern int nr_running, nr_threads;
extern int last_pid;

#include <linux/fs.h>
#include <linux/time.h>
#include <linux/param.h>
#include <linux/resource.h>
#include <linux/timer.h>

#include <asm/processor.h>

#define TASK_RUNNING        0
#define TASK_INTERRUPTIBLE  1
#define TASK_UNINTERRUPTIBLE2
#define TASK_ZOMBIE         4
#define TASK_STOPPED        8
#define TASK_EXCLUSIVE      32

#define __set_task_state(task, state_value)  \
        do { (task)->state = (state_value); } while (0)
#ifdef __SMP__
#define set_task_state(task, state_value)    \
        set_mb((task)->state, (state_value))
#else
#define set_task_state(task, state_value)    \
        __set_task_state((task), (state_value))
#endif

#define __set_current_state(state_value)     \
        do { current->state = (state_value); } while (0)
#ifdef __SMP__
#define set_current_state(state_value)        \
        set_mb(current->state, (state_value))
#else
#define set_current_state(state_value)        \
        __set_current_state(state_value)
#endif

/*
 * Scheduling policies
 */
#define SCHED_OTHER           0
#define SCHED_FIFO            1
#define SCHED_RR              2

/*
 * This is an additional bit set when we want to
 * yield the CPU for one re-schedule..
 */
#define SCHED_YIELD           0x10
```
```