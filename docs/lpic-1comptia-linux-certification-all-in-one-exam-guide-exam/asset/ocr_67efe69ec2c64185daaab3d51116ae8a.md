+   • The parent/child relationship between processes
+   • The heredity of processes

Let’s first look at the parent/child relationship that exists between all processes.

# The Parent/Child Relationship Between Processes

Understand that any process running on a Linux system can launch additional processes. The process that launches the new process is called the parent process. The new process itself is called the child process.

This parent/child relationship constitutes the heredity of Linux processes. Because any process, including child processes, can launch additional processes, it is possible to have many generations of processes running on a system. This is shown in Figure 13-3.

In Figure 13-3, the first parent process spawned three child processes. Each of these three child processes spawned child processes of their own, making the first parent process a grandparent! Do you see now why we call it a “heredity” of processes?

For any process on a Linux system, then, we need to be able to uniquely identify it as well as its heredity. Whenever a process is created on a Linux system, it is assigned two resources:

+   • Process ID (PID) Number This is a number assigned to each process that uniquely identifies it on the system.
+   • Parent Process ID (PPID) Number This is the PID of the process’s parent process.

By assigning these two numbers to each process, we can track the heredity of any process through the system. With this in mind, let’s next discuss the structure of the process heredity on Linux.

# The Heredity of Processes

Notice in Figure 13-3 that I’ve depicted a “grandparent” process that spawned all of the other processes. This figure is drawn from a conceptual standpoint to illustrate the nature of the parent/child relationships between processes. However, it also can be used

![](bbox=[0.04, 0.71, 0.95, 0.98])