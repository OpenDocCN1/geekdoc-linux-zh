# 5.2 A Day in the Life of a Software Interrupt

# 5.2.1 Concurrency in the Linux Communications Stack

As discussed in Chapter 2, the design of kernel functionality, including communications services, is concerned with both reliability and performance. The reliability is largely a feature of correctness of the protocol specifications and implementations, performance is much more than art. It is measured by several metrics, including code size, execution time, and memory use. Code size in Linux is typically on the low side. Execution time must also include the degree to which concurrency (both interleaving and multiprocessor concurrency) are exploited. Memory use is constrained by good discipline in the allocation of buffers and other dynamic structures (e.g., protocol management structures), and timelines in freeing up resources when no longer needed, or needed elsewhere. Another consideration is fairness, which is a topic for a whole book on its.

Within OS, a protocol stack is arranged as a pair of loosely coupled producer/consumer chains for output and input. This avoids well-known deadlock problems and gives a natural model for buffer use discipline, and for critical region protection State management (through the Protocol Control Block for each session) provides a connection between one system call and the next, and between threads that handle interrupts and handling system calls. Queues and counters provide data for flow control. Sleep/wake-up semaphores/queues are used to synchronize the sequence of processes/threads.

Critical regions are then kept to a minimum. User processes can only get to the kernel through system calls, and once there, the kernel has control, except for timer and device driver interrupts. Thus we have three levels of code accessing global data in the protocol stack state (PCB and socket structures):

+   - Upper-layer call

+   - Timer-event

+   - Lower-layer call

Using interrupt level setting or spinlocks as explained in Chapter 2 makes sure that code accessing or modifying the global state in the protocol stack is not preempted inappropriately. from one of these three "directions"

# 5.2.2 Producer/Consumer Chain

Ideally, a protocol stack consists of two chains of tasks, one for output, one for input. These are loosely coupled (e.g., via resource management, or via the protocol itself, for example when a data packet requires acknowledgment, and acknowledgments piggybacked on data). This is illustrated in Figure 5.1.