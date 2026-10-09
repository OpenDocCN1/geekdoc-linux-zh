process gets to run on the CPU, and the more that process will use the full cache as well as the same translation lookaside buffers (TLBs).$^{\dagger}$

The disadvantage of this option is that it has lower reaction times. This option is best for servers that are doing large batch jobs: applications that just need throughput and are run serially, without the need for fast process switching. Any application that requires low latencies and interaction between applications or users would not be well suited to this option. It is known to give a poor “desktop experience” because it can cause jitter during mouse movements and poor audio playback and recording.

# Voluntary Kernel Preemption

This preemption mode is more flexible than no preemption. It relies upon the insertion of points of voluntary preemption into the kernel where such preemption is known to be safe. A slight historical digression can explain how these preemption points are chosen.

The Linux kernel code is not allowed to call for a rescheduling of processes (done by calling the schedule() function) while interrupts are disabled. This is because the kernel code disables interrupts when some atomic operation is taking place on a CPU-specific variable or some lock is being taken that might also be used by an interrupt. With the Linux kernel being so complex, there are several areas of code that can cause a re- schedule, because they might allocate memory pages, access user space, or do a number of other things.

It is also a bug to reschedule while a spin lock is held,$^{\ddagger}$ because it can cause a large latency if a process is scheduled on a CPU that is currently waiting on a spin lock. Under the right conditions, a deadlock could even occur.

These bugs are hard to find because rescheduling can happen at so many places. Any access to user space may cause if the user memory was previously swapped out. Some areas of the kernel that allocate memory may cause a reschedule if memory is tight and pages need to be swapped out to accommodate the newly allocated memory. Just simply testing code was not enough to detect areas that have a spin lock held or interrupts disabled at the time of rescheduling, since the code that actually does the schedule may not be hit during testing. For example, if the user-space memory that is accessed happens to still be in memory or there is plenty of memory available when an allocation takes place, no scheduling will occur. Thus, during code testing, kernel de- velopers may never see the scenario where interrupts are disabled and a reschedule takes place. As soon as this code is out in the public and used by thousands of others, they encounter the bug. The Linux scheduler checks for this scenario and prints out nasty messages when it is detected.

$^{\dagger}$ TLBs cache page tables and are associated with individual processes by the kernel’s paging system.

$^{\ddagger}$ See the upcoming section “Preemptible Kernel.”