![](bbox=[0.18, 0.11, 0.95, 0.45])

**Figure 5-16** POSIX Global Real-Time Run Queue

The beginning of the POSIX run queue from the kernel's point of view is a data structure named `rt_sched_info`:

# Listing 5.7 g4 fields structure mp_threadhd

```
    This is the total number of runnable threads waiting on all
    queue's headers in this POSIX queue
    0 0 4 0 int rts_ready

    This index points into the qp() header array and directs the
    kernel to the best queue to search for a runnable kthread
    4 0 4 0 int rts_bestq

    This is where the tunable number of POSIX queues is stored
    8 0 4 0 int rts_numpti

    Timeslice value for the SCHED_RR policy (set to system
    timeslice value)
    12 0 4 0 int rts_rr_timeslice

    Per priority timeslice for SCHED_RR2 policy (currently also
    set to system timeslice value)
    16 0 4 0 * rts_timeslice

    Pointer to the mp_threadhd array structure (the head of the
    header array)
    20 0 4 0 * rts_qp

    A pointer to the spinlock used to make this queue mp-safe
    24 0 4 0 * rts_lock

    Points to the pset to which this run queue is attached
    28 0 4 0 * rts_pset
```