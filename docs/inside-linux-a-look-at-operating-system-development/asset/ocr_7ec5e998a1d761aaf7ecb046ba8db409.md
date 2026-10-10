its data and calls upon internal subroutines to complete the operation. For example, the code in Figure 5.2 makes an indirect call to `file->f_op->write(inode, file, buf, count)`. The introductory paragraph describes the idea of a virtual file system, discussed further in Section 5.3.2.

When the kernel subroutine finishes, it returns to `system_call`, which checks for rescheduling requests, and if none are needed, returns control to the user program. Rescheduling requests can lead to a context switch, described in Section 5.2.3.

It is also possible that a system call cannot be immediately completed—the most obvious example is the `sleep` system call. In this case, `system_call` is certain to return to a different process because the one which made the call has removed itself from the ready state. The `write` system call in the example program may force a delay because there is insufficient space for the data being written—it’s also possible that the system call could complete immediately because the system kernel can accept and buffer the entire message.

# 5.2 Process Control

Processes can be regarded as the raison d’être of a system kernel. We’ve seen how most everything else can be accomplished in a run-time library.

# 5.2.1 The Nature Of a Process

The classic definition of a process is “a program in execution”. The snapshot of this process in Figure 5.3 shows several components defining the state of the running program’s execution. These components are explained in the following paragraphs.

Besides the code component (which, incidentally, may be shared with other processes), the state of a process is defined by the value of all its data.

The operating system requires a modest amount of data to control each process. Although these data are maintained in an area of memory generally not accessible to the process, they are an essential part of the process state. They are used to record resource consumption (for billing and management), control peripherals and file access, manage the rest of