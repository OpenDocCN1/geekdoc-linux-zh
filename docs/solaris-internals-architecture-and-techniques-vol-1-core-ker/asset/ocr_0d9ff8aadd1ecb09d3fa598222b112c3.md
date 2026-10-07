# The Solaris Kernel Dispatcher

have been configured and the thread has not been bound to a set, the cp_kp_queue for the default partition is selected. Bound threads in any scheduling-class, even RT threads, are placed on the dispatch queue or the processor they've been bound to.

The insertion of a thread on a dispatch queue is accomplished with the setfrontq() and setbackq() routines for the per-processor dispatch queues, and setpkgq() for the kernel preemption queue (or queues). The algorithm for setfrontq(), whose job is to place a thread at the front of a dispatch queue, is represented in the following pseudocode.

```
setfrontq()
if (thread is swapped out or on swap queue)
    call disp_swapped_setrun()
    return
if (uniprocessor system)
    selected_cpu = t_cpu
if (MP system with 1 online CPU)
    selected_cpu = t_cpu
else if (thread is not bound)
    if (thread_priority >= kpreemptpri)
        call setcpu()
        return
    selected_cpu = t_cpu
    if (thread was running on the same partition that dispatch cpu belongs to)
        if (thread_priority < highest-priority thread sitting on the queue)
            selected_cpu = cpu_choose()
    else
        selected_cpu = disp_lowpri_cpu()
```

> /*
at at this point, the processor and associated dispatch queue have been
*/

set thread state to TS_RUN / is runnable /
increment runnable thread count on dispatch queue structure - disp_runnable
place thread on dispatch queue bitmap to reflect added thread
set the dispatch_queue bitmap of thread placed on queue * disp_maxrunpri
if (priority > disp_maxrunpri)
    dispatch_queue->disp_maxrunpri = threadus_priority
call cpu_resched()

The selection of a dispatch queue for a TS/IA thread is essentially the selection of a processor, since each processor has its own dispatch queue. In the pseudocode for a uniprocessor or a multiprocessor system with one online processor, processor selection becomes trivial, which is why the code tests for those conditions up-front, immediately following the swapped thread test. A thread that is either swapped out or sitting in the swap queue needs to be reloaded before it can be placed on a dispatch queue.

To nudge the scheduler (PID 0), disp_swapped_setrun() will set one of two possible flags: either wake_sched or wake_sec, depending on the priority of the thread. These flags are tested in the clock interrupt handler, where wake_sched is tested every clock interrupt and wake_sched_sec is tested every 100 clock interrupts, or once every second. Threads at a priority greater than 99 (highest SYS class priority) wake up the scheduler right-away