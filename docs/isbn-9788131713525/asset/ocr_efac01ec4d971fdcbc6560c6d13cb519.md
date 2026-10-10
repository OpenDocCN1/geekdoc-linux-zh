# ### 17.2 Kernel Preemption

In the early Linux days of Linux 1.x, there was no kernel preemption. This meant that when a user space process requested kernel services, no other task could be scheduled to run until that process either blocked (goes to sleep) waiting on something (usually I/O), or until the kernel request is completed. Making the kernel preemptable$^{3}$ means that while one process is running in the kernel, another process can preempt the first and be allowed to run even though the first process had not completed its in-kernel processing. Figure 17-2 illustrates this.

![](bbox=[0.07, 0.3, 0.88, 0.59])

In this figure, Process A has entered the kernel via a system call. Perhaps it was a call to write() to a device such as the console or a file. While executing in the kernel on behalf of Process A, Process B with higher priority is woken up by an interrupt. The kernel preempts Process A and assigns the CPU to Process B, even though Process A had neither blocked nor completed its kernel processing.

# #### 17.2.1 Impediments to Preemption

The challenge in making the kernel fully preemptable is to identify all the places in the kernel that must be protected from preemption. These are the *critical sections*

> ^{3} Interestingly, there is much debate on the correct spelling of *preemptable* I defer to the survey done by Rick Lehtbaum on www.linuxdevices.com/articles/AT5136316996.html.