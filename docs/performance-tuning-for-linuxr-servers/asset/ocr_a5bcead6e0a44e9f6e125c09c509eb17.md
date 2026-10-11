# **Symmetric Multithreading (SMT)**

Recently, processors started providing multithread support in a single physical CPU. In Symmetric Multithreading (SMT), a single physical CPU appears as two or more virtual CPUs. These virtual CPUs share the core resources of the physical processor, which include the execution engine and processor cache.

Symmetric multithreading allows two or more tasks to be executed simultaneously in the processor, which results in increased performance of the processor. But it has scheduler implications.

Consider a case where a system has two physical CPUs that support four virtual CPUs. The system's performance will be better if the scheduler is aware of the fact that the four virtual CPUs are not the same. If there are only two tasks in the system, the scheduler should place both of them in two different physical CPUs. Also, when a task that was running on a virtual CPU is ready to run, it should be placed in the same physical CPU to take advantage of the cache warmth.

Whether you run a physical CPU or a virtual one, Linux strives to provide ultimate performance. With the version 2.6 release of the multiqueue scheduler, Linux is working hard to give you what you need!