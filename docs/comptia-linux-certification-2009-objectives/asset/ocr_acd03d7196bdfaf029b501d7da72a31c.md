# # Child Processes

A process created by a running process is called a **child process**. The process table contains **parent processes** and any child processes that may have been started. There may be several levels of processes. The parent process can spawn a child process, the child process can spawn another child process, and so on. The parent process must be running for the child processes to run. Parent processes are assigned a unique **Parent Process ID (PPID)**.

![](bbox=[0.15, 0.22, 0.85, 0.48])

*Figure 10-7: Process tree showing parent and child processes.*

# ## Identifying Child Processes

Identifying child processes is not an easy task, especially if there are multiple processes and child processes running at the same time. By examining the order of the PIDs, you may be able to determine the order in which the processes were created and infer which processes are related.

# # The pstree Command

The `pstree` command enables you to list the processes running in a Linux system in a tree-like format. This helps track parent and child processes. All processes are listed as child processes to `init` and this is represented by the initial branching. The processes started within a shell will branch out of the shell's parent process.

![](bbox=[0.76, 0.65, 0.9, 0.72])