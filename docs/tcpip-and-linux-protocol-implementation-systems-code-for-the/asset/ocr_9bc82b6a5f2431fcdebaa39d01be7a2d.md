# TCP/IP and Linux Protocol Implementation

Processes use of kernel services to share resources (as discussed previously) such as CPU, memory, disk, files, networks, and so on.

In their extremely useful book, Beck et al. [5], describe the two different ways that we can look at the relationship between a process and the kernel. To paraphrase what they say:

**Process viewpoint.** From above, the kernel provides services to processes. Processes access these services by making system calls, which appear to be calls to library functions that carry out some work and return. Processes feel like they are on their own—they appear to have a system dedicated to them. When a user program enters a system call, the kernel takes over and has more privileges to access more of the system—because of this, parameters to system calls are extremely constrained, well defined, and carefully checked.

**Kernel viewpoint.** From below, the kernel runs the system. The kernel can access all memory, all devices, and all additional hardware (kernel registers, MMU, and so on). The kernel is structured as a set of cooperating tasks, but there are no protection domains between these tasks, and the switching between them is entirely cooperative. Programming mistakes are disastrous (hence, why systems programmers are paid more than application programmers). When the kernel runs a user's code, it runs it in a less privileged mode to make sure that user programming errors do not infect it. We can see this separation of concerns illustrated in Figure 2.6.

![](bbox=[0.142, 0.613, 0.673, 0.903])

**Figure 2.6** System calls.