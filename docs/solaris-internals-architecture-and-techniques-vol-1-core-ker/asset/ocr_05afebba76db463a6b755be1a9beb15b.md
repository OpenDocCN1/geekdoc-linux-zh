voluntarily surrenders the processor or is preempted when a higher-priority thread becomes runnable. TS/IA threads can also be placed in the SYS class for a short time if the thread is holding a critical resource; a RW lock, or a page lock on a memory page.

The RT class provides real-time scheduling behavior through a fixed priority scheduling policy that has kernel precedence capabilities. RT class have a higher global priority than that of TS and SYS threads. Real-time applications require a minimum, consistent, and deterministic dispatch latency, so when an event occurs that a real-time thread needs to process, the thread gets priority over other threads (all but interrupt threads) on the system for execution on a pro-cessor.

Other kernel enhancements were needed to provide real-time application support, such that a real-time thread that needed a processor could cause the kernel to be preempted from what what it was doing in order to allow the real-time thread to run. Most of the kernel is preemptable; a few critical code paths are non-preemptive, for example, when state information is saved or manipulated, as during a context switch.

The second thing that needed to be addressed was memory locking. A real-time thread cannot usually afford to be exposed to the latency involved in resolving a page fault, which causes execution to be suspended. This problem was addressed by addition of a memory locking facility, so that the developer of a real-time application can use the memcntl(2) system call or mlock(3C) library function to lock a range of pages in physical memory, keeping the memory pages resident in RAM.

These features, combined with processor sets, exclusive thread-to-processor set binding (see Chapter 1, "System Overview\ and the ability to take a processor out of the interrupt pool, combine to make Solaris an outstanding choice for a great real-time applications. A properly configured system that is, a system with sufficient number of processors and memory, can provide a dispatch latency on the order of 1 millisecond or less. For absolute minimum latency for a real-time process, we recommend that you take the following steps.

+   - Size the system appropriately so the Solaris processor requirements for running kernel threads for memory management, STREAMS processing, network and disk I/O, etc., can be met without impeding system performance. Remember, such processing is done by the kernel on behalf of the applications it is running, which determines the load.

+   - Configure a processor set (Solaris 2.6 or later). The processor set can have one processor if it meets the real-time application requirements.

+   - Disable interrupts to the processor dedicated to running the RT processor(es).

+   - Place your processor or processes in the RT scheduling class, and bind them to the processor set.