# 516  Chapter 10 · Operating System Tuning

![](bbox=[0.1, 0.11, 0.9, 0.54])

# ### Understanding and Tuning Processes and Threads

Closely related to CPU utilization is the concept of Oracle process and thread management. Unix and Windows 2000 operating systems behave differently in terms of how these processes are created.

+   - **Oracle Objective**  Explain the difference between a process and a thread

On Unix systems, each Oracle-related process (e.g., PMON, DBWO, sqlplus) runs on the OS as a separate and distinct process. Each process consumes its own memory and CPU resources.

On Windows 2000 systems, each Oracle-related process runs as a separate thread within a single OS process called `oracle.exe`. A *thread* is an independent sequence of instructions that executes within a single OS process. The process can contain multiple threads.