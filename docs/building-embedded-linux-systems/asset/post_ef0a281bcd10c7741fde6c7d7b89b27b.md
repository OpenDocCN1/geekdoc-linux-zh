
Once again, unfortunately, the POSIX specification states that implementations supporting the *priority scheduling* option may always use a priority-based queueing order. Otherwise, the order remains unspecified, leaving the POSIX implementation to do whatever it sees fit with no recourse by the application programmer. The POSIX specification even goes on to say: “Synchronization primitives that attempt to interfere with scheduling policy by specifying an ordering rule are considered undesirable.” And as a matter of fact, the POSIX interface does not allow it. Because it has a direct impact on the scheduling order, this disparity between POSIX and other popular RTOSes can raise subtle bugs whenever the application strictly depends on the behavior depicted in another vendor’s specification. In modern Linux kernels, most POSIX IPC services are based on the Fast Userspace Mutex (*futex*) support, which always uses a priority-based queueing order for all tasks belonging to the real-time scheduling class. Therefore, no FIFO queueing order could be available for those IPCs anyway.

- Traditional RTOSes allow an application to lock the scheduler, effectively preventing the current task from being preempted by any other, regardless of their respective priorities. Even if the rationale for using such a feature is questionable, since this basically boils down to asking a real-time system to ignore task priorities, a number of legacy applications still use it. We think it fortunate that, in this case, POSIX does not define any such option, but the drawback is that legacy code is left with a missing feature. The scheduler lock may often be replaced by recursive mutexes, properly set to protect the same section of code from preemption. However, in some cases, the original code is so entangled that removing the giant lock could have unexpected and unfortunate side effects. It all depends on how much of the original implementation has to change, and how much time is available to fix the potential regression errors.

To sum up, two real-time APIs may be similar, but still have subtle differences that could change the way applications actually behave if the original system calls were simply mapped to their closest equivalents in the target environment. Therefore, moving from a non-POSIX interface to Linux’s POSIX-based one may introduce unexpected issues, particularly in stable applications that one wants to change only in small steps, and very carefully.

At the same time, the similarities among the traditional RTOSes are obvious, so building a common software framework for developing these emulators makes sense.

For instance, what are the actual differences among VxWorks, pSOS+, Virtuoso, VRTX, and Chorus O/S semaphores? VxWorks may support mutexes as part of its semaphore API, whereas other RTOSes may implement mutexes separately or not at all, but the basic semaphore model they all use must behave identically in all implementations.

In the same vein, all traditional RTOSes offer, at the very least, a preemptive, fixed-priority task scheduler, and most support round-robin scheduling, too. They all offer familiar IPC mechanisms, such as event flag groups, mailboxes, and message queues. Memory management features, such as fixed-size or dynamic block allocators, can be found with little core differences among a variety of embedded real-time systems, regardless of whether one calls them partitions, regions, or heaps.

In other words, a significant number of commonalities among traditional RTOSes may be abstracted into a framework so that only the proper window-dressing has to be provided on top in order to mimic each RTOS’s interface properly.

# The Xenomai Architecture

Xenomai eases the porting process from traditional embedded environments to Linux by providing real-time API emulators that mimic the system calls exactly as described by RTOS vendor specifications. Thus, Xenomai preserves the real-time guarantees that applications rely on. Because all Xenomai emulators are built from a common set of building blocks, leveraging the commonalities found among RTOSes, each of those emulators benefits, at no cost, from improvements made to the Xenomai core.

Figure 13-1 shows the overall architecture of Xenomai.

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_389_0.png)

## The Interrupt Pipeline

In order to keep latency predictable for real-time tasks, we must ensure that the regular Linux kernel never defers external interrupts. The interrupts should be blocked or masked for minimal times at the hardware level and be delivered as quickly as possible to Xenomai, regardless of whether the Linux kernel would accept them. At the same time, interrupts directed at the Linux kernel should never trigger a handler when the kernel is in a section where it blocks interrupts.

Therefore, we need an additional piece of software between the hardware, Linux, and Xenomai, to act as a virtual programmable interrupt controller. This allows Linux and Xenomai to maintain separate masks for interrupts and policies for handling interrupts. The software layer Xenomai uses for that purpose is called the *interrupt pipeline*, or I-pipe. It is based on a technical proposal for a system called Adeos, by the author of this book's first edition, Karim Yaghmour. The I-pipe is a simplified implementation of his proposal that relies on a modification of the Linux kernel sources for virtualizing the interrupt mask, instead of depending on features of the x86 chip.

The I-pipe organizes the system as a set of domains connected through a software pipeline. In the I-pipe implementation, these domains share a single address space, which proves useful when a thread needs to invoke services at one point from Linux and at another point from Xenomai.

At the Linux kernel level, a domain is usually a kernel module that calls some I-pipe service to register itself. The I-pipe implementation is available as patches against a number of Linux 2.4 and 2.6 versions, because it has to be specifically adapted to each version of the core kernel code.

Within an I-pipe-enabled kernel, Xenomai is the highest priority domain, ahead of the Linux kernel itself. The I-pipe dispatches events such as interrupts, system calls, processor faults, and other exceptions to domains according to each domain's static priority.

Xenomai registers a set of handlers for various I-pipe events. These handlers notify Xenomai of any noteworthy event before Linux can handle it. This way, Xenomai can process the event in order to have both the real-time system and the regular Linux kernel share it properly.

For instance, when a processor exception is caught on behalf of a real-time task controlled by the Xenomai co-kernel, the co-kernel usually lets the regular kernel handle the fault, because there's no point in duplicating the exception-handling code that Linux already provides. However, the faulting task has to re-enter a normal Linux context before doing so. The exception handler allows Xenomai to intervene during processor faults and exceptions so that it can switch faulting tasks back to a normal Linux context when required.

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_391_0.png)

> *Figure 13-2. The interrupt pipeline*

One of the most important aspects of the I-pipe is that it exposes an architecture-neutral API, which has been ported to a variety of CPUs. This way, client domains such as Xenomai require changes to only a small amount of architecture-dependent code when developers port the domains to other CPUs, and they may rely on a normalized interface to hook onto the host hardware platform.

Figure 13-2 shows the main characteristics of an I-pipe-enabled Linux kernel, with a number of domains receiving external events in sequence, and a per-domain virtual interrupt mask that preserves the ability to lock out interrupts when the domain code requires it. In essence, the I-pipe replaces the hardware interrupt mask provided by the CPU with multiple virtual masks so that domains may run unaffected by another domain’s action on their own interrupt state.

The way Xenomai puts the interrupt pipeline into action is described in detail at [http://www.xenomai.org/documentation/branches/v2.3.x/Life-with-Adesos-rev_B.pdf](http://www.xenomai.org/documentation/branches/v2.3.x/Life-with-Adesos-rev_B.pdf).

# The Hardware and System Abstraction Layers

The Xenomai hardware abstraction layer (HAL) gathers all the CPU and platform-dependent code needed to implement a particular Xenomai port so that every layer starting from the nucleus and higher is free from machine-dependent code.

The Xenomai HAL is combined with a system abstraction layer (SAL), which makes the bulk of the nucleus and skims more portable as well. Xenomai uses HAL and SAL to place its core services on top of an event-driver simulator. This tool is heavily used in testing and debugging new RTOS skins so that developers can run them in a fully sandboxed environment in the context of a regular Linux process.
