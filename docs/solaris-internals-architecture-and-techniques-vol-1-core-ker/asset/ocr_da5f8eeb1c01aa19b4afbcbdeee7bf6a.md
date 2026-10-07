+   - TS — The timeshare scheduling class is the default class for processes and all the kernel threads within the process. It changes process priorities dynamically according to recent processor usage in an attempt to allocate processor resources among the kernel threads in the system. Process priorities and time quanta are calculated according to a timeshare scheduling table at each clock tick, or during wakeup after sleeping for an I/O. The TS class uses priority ranges 0 to 59.

+   - IA — The interactive class is an enhanced TS class used by the desktop window system to boost priority of threads within the window under focus. IA shares the priority numeric range with the TS class.

+   - SYS — The system class is used for kernel threads. Threads in the system class are bound threads; that, there is no time quantum—they run until they finish. The system class uses priorities 60 to 99.

+   - RT — The realtime class implements fixed priority, fixed time quantum scheduling. The realtime class uses priorities 100 to 159. Note that in the RT class have a higher priority over kernel threads in the SYS class.

The interrupt priority levels shown in Figure 1.5 are not available for use by anything other interrupt threads. The intent of their positioning in the priority scheme is to guarantee that interrupt threads have priority over all other threads in the system.

# 1.5 Interprocess Communication

Processes can communicate with each other by using one of several types of interprocess communication (IPC). IPC allows information transfer or synchronization to occur between processes. Solaris supports four different groups of interprocess communication: basic IPC, System V IPC, POSIX IPC, and advanced Solaris IPC.

# 1.5.1 Traditional UNIX IPC

Solaris implements traditional IPC facilities such as local sockets and pipes. A local socket is a network-like connection using the socket (2) system call to directly connect two processes.

A pipe channels data flow from one process to another through an object that operates like a file. Data is inserted at one end of the pipe and travels to the receiving processes in a first-in, first-out order. Data is read and written on a pipe with the standard file I/O system calls. Pipes are created with the pipe (2) system call or by a special pipe device created in the file system with mknod (1) and the standard file open (2) system call.