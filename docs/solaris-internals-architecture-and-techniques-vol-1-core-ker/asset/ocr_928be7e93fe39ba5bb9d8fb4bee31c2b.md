# Kernel Dispatcher

365

```
ts_list_lock          ts_plisthead <---> tsproc <---> tsproc
  mutex --------- tsproc <--- tsproc ---> tsproc ---
  mutex --------- tsproc <--- tsproc ---> tsproc ---
  mutex --------- tsproc <--- tsproc ---> tsproc
```

Figure 9.4 tsproc Structure Lists

# 9.2.1 Dispatch Queues

Every processor on the system has its own dispatch queue (actually, a queue of queues), and per-processor scheduling information is maintained in the data structures that describe the processors in the kernel (CPU structures). Data structures make up the actual dispatch queues, which provide the linkage to the lists of runnable kthreads on the system and state information for each queue. Threads in the TS, IA, and SYS classes are placed on the per-processor dispatch queues.

A separate queue is maintained for threads that are runnable at a high priority enough to cause a kernel preemption. The Solaris kernel is, for the most part, preemptable, such that a processor executing in kernel (system) mode can be preempted by some higher-priority thread. Currently, the global dispatch priorities for RT class and interrupt threads are above SYS and can generate a kernel preemption. Since interrupt threads above do not actually go on a dispatch preempt, only unbound RT classes are placed on the kernel preempt (kp_preempt) queue. There is one such queue on systems that do not have processor sets configured. A kernel preempt queue is created when a processor is configured, so there is a per-processor kp_preempt queue plus one for the default processor set. Since the kernel will not allow every available processor on a system to be placed in a processor set, the number of kernel preempt queues on a system will always be the number of processor sets configured, plus one. Without processor sets configured, there is one kp_preempt systemwide. We discuss preemption later in detail.

The creation of the dispatch queues occurs at boot time during the Solaris initialization. A kernel dispatcher initialization routine, dispatch(), is called from the architecture-specific startup code, which builds the kernel preempt queue and the per-cpu dispatch queues. The kernel data structures that make up the complete dispatch queue picture are cp, disp_queue_info, and dispq structures, as shown in Figure 9.5 on page 368. It is during the dispatcher initialization that the default processor partition is created, where where the kernel preempt queue (cp_kp_queue) is maintained. Solaris 2.5.1, which does not have processor sets, the global kernel preempt queue was maintained in a separate disp_t structure, disp_kp_queue.

A quick note on terminology before we proceed. A processor partition is essential. A user's view of a processor set is what