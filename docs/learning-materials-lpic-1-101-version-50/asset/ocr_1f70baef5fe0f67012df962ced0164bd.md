for a CPU time slot.

Although they allow to significantly improve CPU time utilization, relying solely on system calls to switch between processes is not enough to achieve satisfactory multi-tasking performance. A process that makes no system calls could control the CPU indefinitely. This is why modern operating systems are also *preemptive*, that is, a running process can be put back in the queue so a more important process can control the CPU, even if the running process has not made a system call.

# The Linux Scheduler

Linux, as a preemptive multi-processing operating system, implements a scheduler that organizes the process queue. More precisely, the scheduler also decides which queued *thread* will be executed—a process can branch out many independent threads—but process and thread are interchangeable terms in this context. Every process has two predicates that intervene on its scheduling: the *scheduling policy* and the *scheduling priority*.

There are two main types of scheduling policies: *real-time policies* and *normal policies*. Processes under a real-time policy are scheduled by their priority values directly. If a more important process becomes ready to run, a less important running process is preempted and the higher priority process takes control of the CPU. A lower priority process will gain CPU control only if higher priority processes are idle or waiting for hardware response.

Any real-time process has higher priority than a normal process. As a general purpose operating system, Linux runs just a few real-time processes. Most processes, including system and user programs, run under normal scheduling policies. Normal processes usually have the same priority value, but normal policies can define execution priority rules using another process predicate: the *nice value*. To avoid confusion with the dynamic priorities derived from nice values, scheduling priorities are usually called *static scheduling priorities*.

The Linux scheduler can be configured in many different ways and even more intricate ways of establishing priorities exist, but these general concepts always apply. When inspecting and tuning process scheduling, it is important to keep in mind that only processes under normal scheduling policy will be affected.

# Reading Priorities

Linux reserves static priorities ranging from 0 to 99 for real-time processes and normal processes are assigned to static priorities ranging from 100 to 139, meaning that there are 39 different priority levels for normal processes. Lower values mean higher priority. The static priority of an active process can be found in the sched file, located in its respective directory inside the `/proc`