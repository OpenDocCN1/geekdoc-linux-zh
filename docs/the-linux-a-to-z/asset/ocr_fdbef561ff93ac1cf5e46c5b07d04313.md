# Tiny Threads – Case Study

You have seen that in Linux the main unit of concurrency is the process. In order to switch between executing one process and the next quite a lot of work is involved. This context switch overhead is necessary because, in general, Linux needs to make sure that any pair of processes are protected from interfering with each other, especially when you consider that the processes may not even belong to the same user.

Very often, however, you will want to write programs that are aware of the existence of each other and which can co-operate with each other towards some common goal. The standard solution to this problem is interprocess communication mechanisms.

It doesn’t matter which of the IPC mechanisms you choose to use; there is still the context switch overhead to contend with whenever normal processes need to work together.

The way to overcome this is to use the concept of threads. Each Linux process has its own text, data and system memory areas and data structures, and its own time slices on the processor so that each process can proceed independently at its own pace. The idea behind threads is that each process can have its processor time slices shared between several concurrent threads, each of which also shares the memory and data structures of the process to which it belongs.

The amount of effort involved in context switching between two co-operating threads within a single process is much smaller than the effort of switching between two processes. This is mainly because the threads within a process are all sharing the same text, data and system memory areas and data structures so that no effort is expended in rearranging these things.

Since the threads are specifically designed to be co-operative and not antagonistic, nothing needs to be done by the kernel to protect the threads within a single process from each other.

Threads may, therefore, be considered as lightweight processes; light in the amount of effort required to context switch between them when compared to the