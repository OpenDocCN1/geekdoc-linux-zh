
## The Xenomai Core and Nucleus

The Xenomai core is in charge of supplying all the operating system resources that skins may require to properly mimic traditional RTOS APIs. This requirement is a direct consequence of the underlying co-kernel design: because Xenomai runs on non-real-time Linux kernels, real-time processes must stick exclusively to calling Xenomai services in order to keep predictable latencies. Therefore, the Xenomai core also has to provide all of the basic RTOS resources; skins cannot rely on regular Linux services.

The Xenomai core is best described as an abstract RTOS because it defines generic building blocks. These can be specialized to implement any kind of real-time API that fits the generic model. The building blocks are gathered into a single loadable module called the Xenomai *nucleus* (which is in no way related to the component of ATI called the nucleus). The following are the main components that the Xenomai nucleus provides:

- A real-time thread object controlled by the Xenomai scheduler. The scheduler is a preemptive and fixed-priority, supporting a number of thread priority levels. FIFO ordering applies within a priority level. This scheduler also enables round-robin scheduling on a per-thread basis.

Each RTOS emulator bases its task or thread implementation on the Xenomai thread abstraction so that basic scheduling operations—such as priority management, preemption control, and eager suspension/resumption requests—are already available through the nucleus interface.

- A generic interrupt object that connects the RTOS skin to any number of IRQ lines provided by the underlying hardware. Because interrupt handling is one of the least well-defined areas in RTOS design, the nucleus focuses on providing a simple mechanism with sufficient hooks for each skin to emulate the specific behavior of its RTOS. Xenomai’s support for interrupts includes nested and shared interrupts.

- A memory allocator with predictable latencies that RTOS skins can specialize to support the dynamic allocation of variable-size memory blocks.

- An extendable synchronization object. This is one of the most important features of the Xenomai core. This object implements thread blocking on any kind of resource for all RTOS services. Xenomai supports timeouts, priority inheritance, and priority-based or FIFO queuing order when multiple threads have to block on a single resource. For instance, all kinds of semaphores, mutexes, condition variables, message queues, and mailboxes defined by the RTOSes are based on this core abstraction.

- Timer management, allowing any time-related service to create any number of software timers. Xenomai also implements the notion of a *time base*, by which software timers that belong to different RTOS skins can be clocked separately and concurrently, according to distinct frequencies, or even in a tickless fashion. A lot of traditional RTOSes are tick-based, expressing delays and timeouts as counts of ticks (what the Linux kernel calls jiffies). However, Linux and Xenomai also support tickless timing so that RTOS emulators may ask for nanosecond-level clock resolutions that are too fine-grained to depend on periodic operating system ticks.

To illustrate a typical use of Xenomai building blocks, let's look at the actual implementation of the `t_suspend()` call from the pSOS+ emulator module, which forcibly puts a given task on hold:

```c
u_long t_suspend(u_long tid)
{
    u_long ret = SUCCESS;
    ppostask_t *task;
    s1_t s;

    if (tid == 0) { /* Is this a self-suspension call? */
        if (xnppod_unlockable_p())
            /* E.g. we can't block on behalf on an ISR. */
            return -EPERM;

        /* Ok, ask the nucleus to schedule us out. */
        xnppod_suspend_self();

        /*
         * We woke up due to a Linux signal. We need to tell
         * the caller about this, so that regular signal
         * handling is carried out properly on the Linux side.
         */
        if (xnthread_test_info(&pzos_current_task()->threadbase, XNBREAK))
            return -EINTR;

        /*
         * Someone must have fired t_resume() upon us. Let's
         * go back to our caller to resume running.
         */
        return SUCCESS;
    }

    /* Protect from preemption in the Xenomai domain. */
    xnlock_get_irqsave(&xnlock, s);

    /* Let's check first whether the task identifier is valid. */
    task = pzos_h2obj_active(tid, PSOS_TASK_MAGIC, ppostask_t);
    if (!task) {
        ret = pzos_handle_error(tid, PSOS_TASK_MAGIC, ppostask_t);
        goto unlock_and_exit;
    }

    /* Is the target task already suspended? Ask the nucleus about this. */
    if (xnthread_test_state(task->threadbase, XNSUSP)) {
        ret = ERR_SUSP; /* Task already suspended. */
        goto unlock_and_exit;
    }

    /* Ok, let's ask the nucleus to hold on execution for that task. */
    xnpod_suspend_thread(&task->threadbase, XNSUSP_XN_INFINITE, XN_RELATIVE, NULL);

    if (task == pso_current_task() &&
        xthread_test_info(&task->threadbase, XNBREAK))
        ret = -EINTR;

unlock_and_exit:
    xlock_put_irqrestore(&mlock, s);

    return ret;
}
```

As the code sample shows, the Xenomai nucleus handles the most complex part of the system call by carrying out the actual suspension and maintaining task state information so that the pSOS emulator can decide what has to be done next. The rest of the code is just window-dressing around the **threadbase** anchor object, which is the thread-specific data structure exported by the nucleus to model real-time tasks.

The example that follows was taken from the VRTX emulator. It implements the *sc_pend()* call from the *mailbox* IPC, which makes the caller wait on a memory cell until some nonzero data has been written to it (this is a timed service, so the caller may specify a timeout value):

```c
char *sc_pend(char **mbxop, long timeout, int *errp)
{
    char *msg = NULL;
    vrtxtask_t *task;
    vrtxmb_t *mb;
    spl_t s;

    /* Protect from preemption in the Xenomai domain. */
    xlock_get_irqsave(&mlock, s);

    /* Find out our control block for this mailbox. */
    mb = mb_map(mbxop);

    if (!mb) {
        *errp = ER_NOSB;
        goto unlock_and_exit;
    }

    if (mb->msg != NULL) {
        /*
         * Something has been written in there already, return
         * that value without blocking the caller.
         */
        goto done;
    }

    /* May we block the calling context? */
    if (xnpod_unlockable_p()) {
        *errp = -EPERM;
        goto unlock_and_exit;
    }

    task = vrtc_current_task();

    /*
     * Set up a few status bits the VRTX way, so that inquiries
     * about the task state will return proper information.
     */
    task->vrtxtcb.TCBSTAT = TBMSBOX;

    if (timeout)
        task->vrtxtcb.TCBSTAT |= TBSDelay;

    /* We have to wait for a message now. */
    xsynch_sleep_on(&mb->xsynchbase, timeout, XN_RELATIVE);

    /* Are we waking up due to a Linux signal, or some unblocking call? */
    if (xntread_test_info(&task->threadbase, XNRERASE)) {
        *errp = -EINTR;
        goto unlock_and_exit;
    }

    /* Did we reach the timeout limit? */
    if (xntread_test_info(&task->threadbase, XNTIMEO)) {
        *errp = ER_TMO;
        goto unlock_and_exit;
    }

done:
    /*
     * Ok, we got a message, let's reset the mailbox before passing
     * it on to the caller.
     */
    msg = mb->msg;
    mb->msg = NULL;
    *errp = RET_OK;

unlock_and_exit:
    xslock_put_sigsrestore(&mslock, s);

    return msg;
}
```

Once again, the nucleus did most of the job of implementing the core activities. The main anchor object used here is the *synch* building block, which the Xenomai core exports to model a variety of IPC features.

## The Xenomai Skins

When looking at the Xenomai system, one is most struck by the lack of any central or master API for application development, not even a preferred API based on one of the popular RTOSes. In fact, the Xenomai core considers all RTOS APIs equal. Developers can pick any skin that fits the extremely flexible Xenomai model, or even develop a new skin in order to port applications from an RTOS that isn’t yet supported.

RTOS emulators, and more generally any kind of real-time API, are built on the Xenomai nucleus using the set of common building blocks described earlier. In practical terms, the skin representing an API is embodied in a loadable kernel module, just like the nucleus, and simply appears as a specialized Linux driver that the programmer may enable statically or as a module when building the target kernel image.

Xenomai comes with several canned real-time APIs:

- A POSIX interface maintained by Gilles Chanteperdrix, aiming at 1003.1b standard conformance. It acts as a drop-in replacement for the glibc services it reimplents over the Xenomai co-kernel. The POSIX interface works on top of both the LinuxThreads and NPTL-enabled Glibc.
- A VxWorks emulator, which mimics the WIND kernel 5.x API.
- A pSOS+ emulator based on the pSOS 2.x core API definition.
- A VRTX emulator, supporting both the VRTX32 and VRTX/sa system call interfaces.
- An uITRON-compliant skin, based on specification rev. 3.02 (E-level).
- A RTAI 3.x emulator for porting legacy applications embodied into kernel modules over Xenomai.
- A so-called native API, in the sense that it has been designed as part of the Xenomai development effort. This API is reminiscent of traditional RTOS APIs. Even if it has no particular preeminence over any other skin, it allows people with a non-POSIX RTOS culture to easily develop applications, based on a feature-full but still reasonably compact API.
- Last but not least, the Real-Time Driver Model (RTDM), which provides a unified interface to both users and developers of real-time device drivers. Specifically, it addresses the constraints of dual kernel–based systems like Xenomai, where applications exhibit both real-time and non-real-time runtime phases, depending on which kernel is controlling their tasks at any point in time. RTDM conforms to POSIX semantics (IEEE Std 1003.1) where available and applicable.

## How Xenomai Works

The fundamental difference between Xenomai and other dual kernel systems available for Linux (e.g., RTAI or RTLINUX) is a higher level of integration with the native Linux environment. For the Xenomai project, keeping the regular Linux programming model available for real-time applications has always been considered just as important as guaranteeing the lowest latency figures achievable on any given hardware.

This said, using a co-kernel technology raises several significant usability issues when programmers try to benefit from Linux’s rich POSIX environment. Sometimes real-time
