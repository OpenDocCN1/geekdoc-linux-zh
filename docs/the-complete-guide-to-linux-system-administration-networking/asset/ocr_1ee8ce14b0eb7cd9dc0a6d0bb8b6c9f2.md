When a process ends, it is said to exit. When a process exits, the information about that process that the kernel was maintaining is discarded, and all the resources that the kernel had allocated to that process are released, so they can be allocated to other processes.

Note that the information that the kernel maintains about a process is different from the process itself or the data it maintains. For example, if you start the ls command in a shell, the kernel maintains information about the ls command as a process. But the command itself—the executable programming code that makes up the ls utility—is located separately in memory, as is the data that the ls command might need to work with the file listings it is creating.

# Process States

The state of each process running on Linux is carefully watched by the kernel. You can view these states using the utilities described in the next section. Possible states include:

+   - **Running:** The process is executing, though it must wait for its assigned time slices and must pause for a few microseconds between steps in its execution.
+   - **Sleeping:** The process is waiting for something to happen that doesn't depend on the kernel giving it another time slice. For example, it might be waiting on some input from a device. When a process is sleeping, it doesn't consume any CPU processing time, though it still has memory allocated to it by the kernel and the program itself.
+   - **Stopped:** The process has been halted before it exited normally; this is typically only seen when you are debugging programs that you are writing.
+   - **Zombie:** A zombie process is a process that is no longer active—the program itself has been closed, for example—but the Linux kernel is still maintaining information about the process and allocating resources to it. The kernel regularly clears out any zombie processes and frees up their resources.

# Swap Space

Sometimes the kernel needs to allocate more resources in the form of system memory than the system actually has. In this situation, the kernel copies some information from memory to the swap space—typically a separate hard disk partition called a swap partition. Swap space is also called virtual memory because it acts like memory: it holds programs and data used by the Linux kernel in a way that acts like an extension of the system's RAM. As you view information on processes, you can see which are swapped out. When the kernel does this, the process cannot run until it is swapped in again. On a very busy system or a system without sufficient system memory, processes are continuously being swapped in and out as their state changes. Thrashing occurs when the kernel spends so much time moving processes to and from the swap space that the kernel and the processes bog down and work inefficiently. You might even notice this if you hear your disk drive working (or see a status