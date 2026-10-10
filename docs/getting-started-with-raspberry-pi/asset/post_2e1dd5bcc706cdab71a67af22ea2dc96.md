
kulpdated. You might have noticed two instances of pdflush in the ps output. A new instance is created if the kernel senses that existing instances have their hands full, servicing disk queues. This improves throughput, especially if your system has multiple disks and many of them are busy.

As you saw in the preceding chapter, kjournald is the generic kernel journaling thread, which is used by filesystems such as EXT3.

The Linux Network File System (NFS) server is implemented using a set of kernel threads named nfsd.

Our example kernel thread relinquishes the processor until it gets woken up by parts of the kernel responsible for monitoring the data structures of interest. When awake, it invokes a user mode helper program and passes appropriate identity codes in its environment.

To create a kernel thread, use kernel_thread():

```
ret = kernel_thread(mykthread, NULL,
     CLONE_FS | CLONE_FILES | CLONE_SIGHAND | SIGHCLD);
```

The flags specify the resources to be shared between the parent and child threads. CLONE_FILES specifies that open files are to be shared, and CLONE_SIGHAND requests that signal handlers be shared.

Listing 3.1 shows the example implementation. Because kernel threads usually act as helpers to device drivers, they are created when the driver is initialized. In this case, however, the example thread can be created from any suitable place, for instance, init/main.c.

The thread starts by invoking daemonize(), which performs initial housekeeping and changes the parent of the calling thread to a kernel thread called kthreadd. Each Linux thread has a single parent. If a parent process dies without waiting for its child to exit, the child becomes a zombie process and wastes resources. Reparenting the child to kthreadd, avoids this and ensures proper cleanup when the thread exits.[1]

[1] In 2.6.21 and earlier kernels, daemonize() reparents the calling thread to the init task by calling reparent_to_init().

Because daemonize() blocks all signals by default, use allow_signal() to enable delivery if your thread desires to handle a particular signal. There are no signal handlers inside the kernel, so use signal_pending() to check for signals and take appropriate action. For debugging purposes, the code in Listing 3.1 requests delivery of SIGKILL and dies if it’s received.

kernel_thread() is deprecated in favor of the higher-level kthread API, which is built over the former. We will look at kthreads later on.

### Listing 3.1. Implementing a Kernel Thread

```c
static DECLARE_WAIT_QUEUE_HEAD (myevent_waitqueue);
rwlock_t myevent_lock;                /* Holds the identity of the
                                       troubled data structure.
                                       Populated later on */
extern unsigned int myevent_id;

static int mykthread(void *unused)
{
    unsigned int event_id = 0;
    DECLARE_WAITQUEUE(wait, current);
    /* Become a kernel thread without attached user resources */
    daemonize("mykthread");

    /* Request delivery of SIGKILL */
    allow_signal(SIGKILL);

    /* The thread sleeps on this wait queue until it's
       woken up by parts of the kernel in charge of sensing
       the health of data structures of interest */
    add_wait_queue(&myevent_waitqueue, &wait);

    for (;;) {
        /* Relinquish the processor until the event occurs */
        set_current_state(TASK_INTERRUPTIBLE);
        schedule();  /* Allow other parts of the kernel to run */
        /* Die if I receive SIGKILL */
        if (signal_pending(current)) break;
        /* Control gets here when the thread is woken up */
        read_lock(&myevent_lock);  /* Critical section starts */
        if (myevent_id) {  /* Guard against spurious wakeups */
            event_id = myevent_id;
        }
        read_unlock(&myevent_lock); /* Critical section ends */
        /* Invoke the registered user mode helper and
           pass the identity code in its environment */
        run_umode_handler(event_id); /* Expanded later on */
    } else {
        read_unlock(&myevent_lock);
    }

    set_current_state(TASK_RUNNING);
    remove_wait_queue(&myevent_waitqueue, &wait);
    return 0;
}
```

If you compile and run this as part of the kernel, you can see the newly created thread, *mykthread*, in the ps output:

```
bash> ps -ef
    UID          PID   PPID C STIME TTY     TIME CMD
    root           1      0 0 21:56 ?     00:00:00 init [3]
    root           2      1 0 22:36 ?     00:00:00 [ksoftirqd/0]
    ...
    root          111      1 0 21:56 ?     00:00:00 [mykthread]
    ...
```

Before we delve further into the thread implementation, let's write a code snippet that monitors the health of a data structure of interest and awakens mykthread if a problem condition is detected:

```c
/** Executed by parts of the kernel that own the
data structures whose health you want to monitor */
/** ... */

if (my_key_datastructure looks troubled) {
    write_lock(&myevent_lock); /* Serialize */
    /* Fill in the identity of the data structure */
    myevent_id = datastructure_id;

    write_unlock(&myevent_lock);

    /* Wake up mykthread */
    wake_up_interruptible(&myevent_waitqueue);
}

/* ... */
```

Listing 3.1 executes in process context, whereas the preceding snippet runs from either process or interrupt context. Process and interrupt contexts communicate via kernel data structures. Our example uses *myevent_id* and *myevent_waitqueue* for this communication. *myevent_id* contains the identity of the data structure in trouble. Access to *myevent_id* is serialized using locks.

Note that kernel threads are preemptible only if *CONFIG_PREEMPT* is turned on at compile time. If *CONFIG_PREEMPT* is off, or if you are still running a 2.4 kernel without the preemption patch, your thread will freeze the system if it does not go to sleep. If you comment out *schedule()* in Listing 3.1 and disable *CONFIG_PREEMPT* in your kernel configuration, your system will lock up.

You will learn how to obtain soft real-time responses from kernel threads when we discuss scheduling policies in Chapter 19, "Drivers in User Space."

## Process States and Wait Queues

Here's the code region from Listing 3.1 that puts mykthread to sleep while waiting for events:

```c
add_wait_queue(&myevent_waitqueue, &wait);
for (;;) {

    /* ... */
    set_current_state(TASK_INTERRUPTIBLE);
    schedule(); /* Relinquish the processor */
    /* Point A */

    /* ... */
}
set_current_state(TASK_RUNNING);
remove_wait_queue(&myevent_waitqueue, &wait);
```

The operation of the preceding snippet is based on two concepts: *wait queues* and *process states*.

Wait queues hold threads that need to wait for an event or a system resource. Threads in a wait queue go to sleep until they are woken up by another thread or an interrupt handler that is responsible for detecting the event. Queuing and dequeuing are respectively done using `add_wait_queue()` and `remove_wait_queue()`, and waking up queued tasks is accomplished via `wake_up_interruptible()`.

A kernel thread (or a normal process) can be in any of the following process states: running, interruptible, uninterruptible, zombie, stopped, traced, or dead. These states are defined in `include/linux/sched.h`:

- A process in the **running** state (`TASK_RUNNING`) is in the scheduler run queue and is a candidate for getting CPU time allotted by the scheduler.
- A task in the **interruptible** state (`TASK_INTERRUPTIBLE`) is waiting for an event to occur and is not in the scheduler run queue. When the task gets woken up, or if a signal is delivered to it, it re-enters the run queue.
- The **uninterruptible** state (`TASK_UNINTERRUPTIBLE`) is similar to the **interruptible** state except that receipt of a signal will not put the task back into the run queue.
- A **stopped** task (`TASK_STOPPED`) has stopped execution due to receipt of certain signals.
- If an application such as strace is using the ptrace support in the kernel to intercept a task, it'll be in the **traced** state (`TASK_TRACED`).
- A task in the **zombie** state (`EXIT_ZOMBIE`) has terminated, but its parent did not wait for the task to complete. An exiting task is either in the `EXIT_ZOMBIE` state or the `dead` (`EXIT_DEAD`) state.

You can use `set_current_state()` to set the run state of your kernel thread.

Let's now turn back to the preceding code snippet. mythread sleeps on a wait queue (myevent_wait_queue) and changes its state to `TASK_INTERRUPTIBLE`, signaling its desire to opt out of the scheduler run queue. The call to schedule() asks the scheduler to choose and run a new task from its run queue. When code responsible for health monitoring wakes up mythread using `wake_up_interruptible(myevent_wait_queue)`, the thread is put back into the scheduler run queue. The process state also gets simultaneously changed to `TASK_RUNNING`, so there is no race condition even if the wake up occurs between the time the task state is set to `TASK_INTERRUPTIBLE` and the time schedule() is called. The thread also gets back into the run queue if a `SIGKILL` signal is delivered to it. When the scheduler subsequently picks mythread from the run queue, execution resumes from Point A.

## User Mode Helpers

Mythread invokes `run_umode_handler()` in Listing 3.1 to notify user space about detected events:

```c
/* Called from Listing 3.1 */
static void
run_umode_handler(int event_id)
{
    int i = 0;
    char *argv[2], *envp[4], *buffer = NULL;
```
