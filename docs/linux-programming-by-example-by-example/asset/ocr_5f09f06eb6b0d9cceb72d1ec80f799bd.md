# What Is a Process?

A *process* is an instance of an executing program and also the operating system’s basic scheduling unit. A process is considered a running program and consists of the following elements:

+   • The program’s current *context*, which is the program’s current execution status
+   • The program’s current working directory
+   • The files and directories to which the program has access
+   • The program’s *credentials* or access rights, such as its file mode and ownership
+   • The memory and other system resources allocated to the process

Processes are also Linux’s basic scheduling unit. The kernel uses processes to control access to the CPU and other system resources. Linux processes determine which programs run on the CPU, for how long, and with what characteristics. The kernel’s scheduler allocates CPU execution time, called *time slices*, among all processes, preempting each process in turn when its time slice expires.

The time slices are small enough that, on a single processor system, several processes appear to be running simultaneously. Each process also contains enough information about itself that the kernel can switch it in and out of execution as necessary.

# Process Attributes

Processes have attributes or characteristics that identify them and define their behavior. The kernel also maintains a great deal of information about each process internally and provides an *interface* or group of function calls to obtain this information. The following sections discuss what this information is and the interfaces for obtaining and manipulating it.

# Process Identifiers

The basic attributes of a process are its process ID, *PID*, and its parent process ID, *PPID*. Both the PID and the PPID are positive, non-zero integers. A PID uniquely identifies a process. A process that creates a new process is said to have created a *child process*. Conversely, the process that created a child process is called the *parent process*.

All processes ultimately trace their lineage to the process with PID 1, which is the `init` process. `init` is the first process to start after the kernel boots. `init` brings up the system, starts daemons, and runs other programs