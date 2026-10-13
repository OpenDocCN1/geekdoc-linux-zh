The use of preemption control in application code is illustrated in the following pseudocode, showing preemption control being turned on and then off around the acquisition and freeing of a mutex lock.

```
mutex_t mylock;
mutex_init(&mylock);
schedctl_init();
.
.
schedctl_start();
mutex_lock(&mylock);

        do work while holding the mutex

mutex_unlock(&mylock);
schedctl_stop();
```

Without the activation turned on to enable preemption control, there’s a greater possibility that the thread will be forced to surrender the processor before it is able to free the lock. Think of preemption control as a means of telling the dispatcher “I’m about to grab a critical resource, so grant me a little extra execution time.”

Getting back to the ts_tick() code, we’ve entered the main processing segment of ts_tick() because the kthread was not running at a SYS class priority and its time quantum has expired. If preemption control has been turned on for the kthread, it is allowed an extra couple of clock ticks to execute, no priority tweaks are done, and ts_tick() is finished with the thread. There is a limit to how many additional clock ticks a kthread with preemption control turned on will be given. If that limit has been exceeded, the kernel sets a flag such that the thread will get one more time slice and on the next pass through ts_tick(), the preemption control switch will fail and normal tick processing will be done. In this way, the kernel does not allow the scheduler activation to keep the thread running indefinitely. If the requirement is that the thread must stay on the processor indefinitely, the RT class should be used.

Regular TS/IA tick processing involves adjusting the thread priority in the same way the priority is set in the fork return code (Figure 9.7 on page 379). ts_cpupri is used as an index into the TS dispatch table and is assigned a new value that is based on ts_tqexp from the index location. The user mode priority is calculated, ts_dispwait is set to 0, and a new dispatcher priority is derived from the TS/IA dispatch table. The new priority is based on the global priority value in the table row corresponding to ts_umdp1, which is used as the dispatch table array index. What’s different between the ts_tick() handler and the fork return scenario is that the thread’s priority is not set directly in ts_tick(), but rather in a thread_change_pri() kernel function. A change in a thread’s priority may warrant a change in its position on a queue; thread_change_pri() handles such a case. In the fork return, we are dealing with a new thread that has not yet been on a queue, so it’s not an issue.