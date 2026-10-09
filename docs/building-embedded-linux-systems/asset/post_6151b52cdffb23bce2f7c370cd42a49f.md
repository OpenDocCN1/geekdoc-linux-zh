
- Co-kernels are inherently lightweight, because they rely on the host kernel to provide non-time-critical services, which represent most of the feature set. Consequently, the price of implementing real-time guarantees in the system is paid only by the applications that require them. In other words, the Linux host kernel does not have to deal with real-time issues at all, aside from virtualizing the interrupt mask, which is a cheap operation.

However, this design excludes all the regular Linux drivers and libraries that rely on the standard kernel from the real-time domain, because they are not served by the co-kernel. In a number of application cases, this requirement may be a significant drawback, particularly when the implementation entangles non-real-time and time-critical activities, or simply because having regular drivers with bounded response times would fit the system’s need at a lower engineering cost.

Additionally, Xenomai is primarily about supporting traditional RTOS APIs over a Linux-based real-time framework so that projects can migrate legacy applications to Linux at a lower cost. In some cases, the dual kernel approach is the right one; in other cases, a fully native real-time Linux framework would deliver a better port. In any case, getting the best possible trade-off between Linux integration and real-time predictability should be the decisive factor in picking the right base technology.

As a matter of fact, the PREEMPT_RT effort¹ opens up a promising path to getting short, bounded latencies within a single kernel system for a variety of real-time application profiles and platforms.

Because the goal of the Xenomai project is to ease the porting of applications from traditional RTOSes to Linux, PREEMPT_RT creates opportunities to extend its relevance as a migration tool, provided the emulation technology is fully ported to a single-image real-time kernel.

At the time of this writing, as of Linux kernel 2.6.24, the Xenomai emulators are being ported to PREEMPT_RT-enabled kernels. This effort, codenamed Xenomai SOLO, is taking place in parallel with the normal development of the dual kernel version. It is cosponsored by the Open Source Automation Development Lab (http://www.osadl.org), DENX Software Engineering (http://www.denx.de), and the Xenomai project. This purely native implementation, coupled with the already existing native version of the RTDM layer, will complete the jigsaw puzzle.§ Traditional real-time applications will be ported more easily to Linux, keeping all options open for selecting the underlying kernel technology used to support them, and taking advantage of a growing base of drivers for industrial devices.

## CHAPTER 14

## The RT Patch

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_408_0.png)

Over the past few years, there has been a large effort in the Linux community to convert the Linux kernel into a true real-time operating system (RTOS), without the help of a microkernel. In order to achieve this, several changes to the kernel were necessary. For Linux to behave properly in a real-time environment, interrupt service routines must not be able to unconditionally preempt any process running on the CPU, protection for critical sections needs to be narrowed to block only those processes that might access them, and unbounded priority inversion must not be allowed. The pros and cons of native Linux real-time versus an accompanying microkernel were covered in Chapter 12.

In the past, several people have tried to implement a full real-time Linux kernel. Some have even built their businesses around it. In the 2.2 and 2.4 Linux time frame, TimeSys, a small real-time Linux company, branched off from the mainline kernel (the kernel provided by kernel.org), to create and support its own kernel that implemented the changes just mentioned. But maintaining a kernel outside the mainline Linux tree has proven to be very difficult.

Ingo Molnar, a major contributor to the Linux kernel, showed up on the real-time scene after watching others work on their efforts to turn the Linux kernel into an RTOS. Seeing some of the benefits of having real-time capabilities in Linux, Molnar started his own patch against the mainline kernel to add real-time features.

Molnar's approach was slightly different from others because his viewpoint was not that of real-time developers trying to convert Linux to their environment, but rather that of a long-term Linux hacker giving the system some real-time features that would improve the user's experience. Soon after Molnar started his RT patch, several other kernel developers joined him on his quest, and it evolved from Molnar's experiment to a robust real-time alternative. Many of the features that were developed in the RT patch have already made it into the mainline kernel. Some of these features include high-resolution timers, kernel lock validation, generic interrupts for all architectures, robust futexes, and even priority inheritance. We'll explain some of these features, and others that are being developed, in the following sections.

### Interrupts As Threads

The current Linux kernel² has several methods of handling the work of devices. When a device performs an asynchronous event that requires action by the CPU and interrupts are enabled, the device sends an interrupt signal that preempts the CPU from whatever it was doing to perform the interrupt service routine (ISR) for the device that issued the interrupt. The ISR is executed at a higher priority than any user task, and with interrupts disabled on the CPU or, at the bare minimum, with the current interrupt line masked off. So, the only thing that can preempt an ISR is another interrupt, and only if the ISR is nice enough to turn interrupts back on.

A well-written device driver puts as little work as possible into the ISR and pushes other work to a kernel thread, a tasklet, or a softirq. These are the other methods that Linux provides for devices to finish the work needed by asynchronous events, such as device activity.

A *softirq* is a service routine that is performed after the return of an ISR and before resuming the process that was interrupted. If too many softirqs are queued, the kernel wakes up a high-priority kernel thread (ksoftirqd) to finish them. There’s been debate in the kernel development as to what qualifies as “too many softirqs.” The *ksoftirqd* thread is started whenever a softirq is started with interrupts disabled, or if a softirq routine is processed more than once before returning back to the process that was preempted.

A *tasklet* is similar to a softirq in that it also occurs after an ISR and before resuming the interrupted process. The difference between a softirq and a tasklet is that the same softirq can run simultaneously on two separate CPUs, whereas a tasklet cannot. A softirq therefore has to use locks to protect against concurrent accesses to any nonlocal data or other resources, whereas a tasklet does not; in other words, a tasklet need not be reentrant.

Another difference between tasklets and softirqs is that a tasklet function may run on a different CPU from the one that raised (triggered) the tasklet. Tasklets are in fact implemented by a softirq. The softirq function that implements tasklets just makes sure that two tasklet functions are not running at the same time. This also means that tasklets can be executed by the *ksoftirqd* thread.

A kernel thread is a thread that runs only within the kernel, and can be awakened by an ISR to handle any work left to be completed by an interrupt service routine, so that the ISR can return quickly and allow whatever process or kernel activity was preempted to resume. A kernel thread acts much like other threads in Linux. It can be scheduled, have its priority changed, run on given CPUs, and be manipulated by the system administrator like any other thread in the system.

In this case, the ISR would usually utilize a *work queue*. A work queue is a kernel utility that, like its name suggests, queues up work to be run in a worker kernel thread. There is a generic worker kernel thread called *keventd* that will execute work functions by the kernel if the kernel did not allocate a specific work queue. Any work queued to the generic *keventd* thread needs to wait for all the previous work functions that were queued ahead of it, because a queue handles work in a FIFO order.

A kernel thread entails a bit more overhead than a softirq or tasklet but is much more *flexible*. A *softirq* and tasklet under the non-RT Linux kernel cannot be preempted by any process at any priority. Conversely, a *softirq* and tasklet can preempt any process. So, even though the overhead of a kernel thread is slightly more than a softirq and tasklet, it allows the kernel scheduler to be more flexible and gives more control to the system administrator. (However, kernel threads may ignore signals.) This flexibility is especially important to running a real-time environment.

When a *routine* is performed by an ISR, *softirq*, or tasklet, any process that is running on the CPU will be preempted by it. They will even preempt kernel threads that are doing work for other devices. This Linux *behavior* effectively creates a policy that makes ISRs, *softirqs*, and tasklets the highest-priority events in the system. In order to lower latencies that these routines impose on the system, the RT patch transforms them all into kernel threads.

#### Hard IRQs As Threads

A hard interrupt request (IRQ) is a sort of envelope around an ISR, lasting from the time the interrupt preempts the CPU to the time the ISR returns the CPU back to normal processing. This can lead to *interrupt inversion*, where an interrupt service *routine* takes time away from a high-priority process in order to perform work that is of lower priority. Figure 14-1 illustrates the latency caused by an ISR that takes away processing time from a high-priority process. The latency consists of both arrows labeled “context switch,” in addition to the ISR running time.

Obviously, we cannot keep the hardware interrupt from preempting the CPU. But the RT patch shortens the time of *interrupt inversion* to a bare minimum. It does this by converting the interrupt handlers into threads. When an interrupt is triggered, the ISR just wakes up a kernel thread that will run the function registered by the device driver, instead of the ISR running the interrupt handler itself. Figure 14-2 illustrates the RT patch’s handling of interrupts.

When an interrupt is triggered, whatever is currently executing on the CPU will still be preempted. But this time, the only activity performed before returning to the previous process or thread is the masking of the interrupt line and the waking of the interrupt service thread. If the interrupt service thread is of a higher priority than the currently running thread, it will be immediately scheduled and preempt the process that the interrupt preempted. If the original thread was of a higher priority than the interrupt service thread, processing continues with the original thread, and the interrupt service

---
2. 2.6.22 as of this writing.
