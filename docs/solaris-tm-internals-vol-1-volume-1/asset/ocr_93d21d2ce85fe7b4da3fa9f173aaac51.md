identifiers, the address space, signal dispositions, signal handlers, and so forth. The basic process execution environment, minus the thread abstractions, is shown in Figure 8.1.

![](bbox=[0.196, 0.202, 0.902, 0.491])

*Figure 8.1* **Process Execution Environment**

Figure 8.1 shows the major components that establish the execution environment for a process. We introduce these abstractions here and discuss them in detail later in the chapter.

The address space defines the mapped memory pages for a process's various address space segments. The identifiers maintained for each process include the process PID, the PID of its parent process, and the ID of the process group the process belongs to. Process groups provide a linkage for processes under control of the same terminal and facilitate things like job control signal delivery and management, which are part of the session management abstraction.

Most processes have at least three opened files—commonly referred to as standard input (stdin), standard output (stdout), and standard error (stderr)—that define the source and destination of input and output character streams for the process. These files may link to device information for a controlling terminal or window or may represent a file in a file system. Signals provide a means by which a process can be notified of an event or condition that may alter the execution environment. All processes maintain signal masks, can alter the disposition of one or more signals, and can define signal handlers for particular signals. Finally, there exists a means by which processes are assigned an execution priority and scheduling class, which determine how much processor time the process will get relative to other processes executing on the system.