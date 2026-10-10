Many Unix implementations rely on a common architectural feature: there are multiple modes of operation and the user mode can be switched without affecting the privileged mode of operation. We’ve seen in Sec- tion 5.1.2 how a system call leads to a privileged mode of operation. Once in this privileged mode, the kernel code can change the param- eters of the user mode of operation as easily as it can switch the stack pointer from one process’ stack to another. The real distinction among processes is held in the other registers, including the stack pointer and the memory management registers.

In the implementation of Linux for the x86 architecture, the bounce point uses a single instruction which saves all the registers in the current task state segment (TSS) and retrieves new register values from the new TSS. Because the instruction pointer (IP) is one of those registers, and the same trampoline code is used for all context switching, the instruction pointers saved in all the TSSs have the same value.

# User Threads

A thread is a process-like entity which shares much of its context with its siblings. Because of this sharing, switching among sibling threads involves less data manipulation and therefore less time than for heavy- weight processes. (If threads cost as much as processes to context switch, there would be no use for threads.) The switching between threads can be co-operative or preemptive, but in any event, the whole process is subject to preemptive scheduling.

This low cost switching makes threads ideal for a tightly-coupled set of subroutines working on a common problem, perhaps created im- plicitly out of the source program. Little performance is lost, yet the programmer is able to express a solution which better matches the prob- lem.

Threads can be implemented in several ways—entirely as user code, with kernel support, or entirely within the kernel.

The pthreads project has developed user level multithreading for Linux. It is derived from a portable implementation, called C-threads, which runs on a number of Unix systems.

> ⁵ftp://tsx-11.mit.edu/pub/threads