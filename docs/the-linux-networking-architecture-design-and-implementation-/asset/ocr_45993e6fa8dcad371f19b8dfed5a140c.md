# APPENDIX B

# # Debugging in the Linux Kernel

Debugging is a helpful step when writing reliable software. This is normally not a big problem when one writes simple applications. There are appropriate tools, such as the gdb debugger and its graphic variant, ddd, and other useful tools (e.g., strace), to track system calls.

However, the prerequisites are different for debugging an operating-system kernel. Remember that it is the very task of an operating system environment to run applications and to catch as many exceptions as possible to ensure that the work of other applications is not at risk. The best known error in programs is a NULL pointer that references the memory NULL rather than a valid memory address. When an application wants to access this page or run the statement at this location, the operating system should catch this error and output a message (i.e., segmentation fault or memory protection violation). The faulty application can then be checked by step in a debugger to find the faults in the source code.

Unfortunately, it's not so easy to check an operating system for itself. The reason is that, when a NULL pointer occurs in the system itself, there is no way to stop the computer from crashing. It is often impossible to find the exact location of an error or even the faulty component. Despite these circumstances, this chapter introduces several ways to track the process of a problem in the kernel to discover potential sources of error.

In addition to prevent NULL pointer dereferences, it is also important to obtain information about the functionality of algorithms and kernel components at runtime, to be able to check for correct operation. In the selecting of an operating system, its correctness is as important as its stability.

# ### B.1 LOG OUTPUTS FROM THE LINUX KERNEL

One of the most common debugging techniques is the output of certain messages at strategic program positions—meaningful screen outputs are simply inserted (ideally before and after) at potential sources of error. This helps us to track the kernel's behavior and how it progresses. Of course, we could also output variable values and similar useful things.