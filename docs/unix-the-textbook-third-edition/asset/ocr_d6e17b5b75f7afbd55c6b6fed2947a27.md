+   - The environment
+   - The root directory
+   - The set-user-ID (SUID) and set-group-ID (SGID) status
+   - The signal settings
+   - The time left before an alarm goes off
+   - The value of the file creation mask, umask

Although the child process is an exact copy of the memory image of the parent process, the two differ from each other in many ways:

+   - Both processes have their own process IDs (PIDs).
+   - Both have different parent processes.
+   - Both have their own copies of the PPFDT.
+   - The resource utilization for the child process is set to 0.
+   - The child process has only one thread of execution, and if the parent process is multithreaded, the other threads do not release the resources held by them.

Since the parent and child processes have copies of the same PPFDT, both can do I/O with files that the parent process had opened before creating the child process and this I/O is visible in both processes. In other words, the change is the position of the file pointer due to read(), write(), and lseek() calls by either process is visible in the other process. So, if either process reads N bytes from an already open file, the file pointer is incremented by N and the next read or write operation by parent or child is performed at the new position of the file pointer.

The fork() call may fail for the reasons listed in Table 19.2.

The vfork() system call is a lighter version of fork(). It creates a child process exactly like fork() but does not copy the address space of the parent; it copies the address space on demand—that is, when the child's memory image is needed. The vfork() system call is used instead of fork(), particularly if the child process uses the execve() system call (or a variant) or the exec() library call (or a variant) right after its creation to overwrite itself

# TABLE 19.2 Reasons for the fork() System Call to Fail

| Reason for Failure | Value of errno |
|---|---|
| The limit on the maximum number of processes that may run on the system simultaneously would be exceeded | EAGAIN |
| The limit on the maximum number of processes that may run under a user would be exceeded | EAGAIN |
| The resource limit set for the process has been reached | EAGAIN |
| Insufficient swap space for the new process | ENOMEM |