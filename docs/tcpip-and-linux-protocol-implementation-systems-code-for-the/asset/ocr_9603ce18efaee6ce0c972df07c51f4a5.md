# Protocol Implementation Framework 113

In Figure 5.5 see the definition of the core data structure to describe the tasklet queue structure:

# Figure 5.5 Task queue (TQ) structures: linux/include/linux/tqueue.h.

```
struct tq_struct {    /* linked list of active bh's */
struct list_head list;    /* must be initialized to zero */
unsigned long sync;        /* function to call it */
void (*routine)(void *);    /* argument to function it */
void *data;                };

typef struct list_head task_queue;
#define DECLARE_TASK_QUEUE(q) LIST_HEAD(q)
#define TQ_ACTIVE(q)          (!list_empty(&q))

extern task_queue tq_timer, tq_mediates, tq_disk;
```

Now we have to support legacy-deferred interrupts, since a great deal of code is still written in terms of this older Linux construct.

# Figure 5.6 TQ mapping to deferred processing/bh.. linux/include/linux/tqueue.h.

+   /*
* To implement your list of active bottom halves, use the following
* two definitions:
* DECLARE_TASK_QUEUE(my_task);
struct tq_struct my_task = {
routine: (void (*)(void *))my_routine,
data: &my_data
};

* To activate a bottom half on a list, use:
* queue_task(&my_task, &my_tqueue);
* To later run the queued tasks use
* run_task_queue(&my_tqueue);

* This allows you to do deferred processing. For example, you could
* have a task queue called tq_timer, which is executed within the timer
* interrupt.
*/