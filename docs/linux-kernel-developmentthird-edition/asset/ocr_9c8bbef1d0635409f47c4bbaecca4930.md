it wants as long as the result is correct. Of course, this system call is as simple as they come, and there are not too many other ways to implement it.5

*SYSCALL_DEFINE0* is simply a macro that defines a system call with no parameters (hence the 0). The expanded code looks like this:

```
asmlinkage long sys_getpid(void)
```

Let’s look at how system calls are defined. First, note the *asmlinkage* modifier on the function definition. This is a directive to tell the compiler to look only on the stack for this function’s arguments. This is a required modifier for all system calls. Second, the function returns a *long*. For compatibility between 32- and 64-bit systems, system calls defined to return an int in user-space return a long in the kernel. Third, note that the *getpid()* system call is defined as *sys_getpid()* in the kernel. This is the naming convention taken with all system calls in Linux: System call *bar*() is implemented in the kernel as function *sys_bar*().

# ## System Call Numbers

In Linux, each system call is assigned a *syscall number*. This is a unique number that is used to reference a specific system call. When a user-space process executes a system call, the syscall number identifies which syscall was executed; the process does not refer to the syscall by name.

The syscall number is important; when assigned, it cannot change, or compiled applications will break. Likewise, if a system call is removed, its system call number cannot be recycled, or previously compiled code would aim to invoke one system call but would in reality invoke another. Linux provides a “not implemented” system call, *sys_ni_syscall*(), which does nothing except return -ENOSYS, the error corresponding to an invalid system call. This function is used to “plug the hole” in the rare event that a syscall is removed or otherwise made unavailable.

The kernel keeps a list of all registered system call in the system call table, stored in *sys_call_table*. This table is architectured; on x86-64 it is defined in *arch/x86/ kernel/syscall_64.c*. This table assigns each valid syscall to a unique syscall number.

# ## System Call Performance

System calls in Linux are faster than in many other operating systems. This is partly because of Linux’s fast context switch times; entering and exiting the kernel is a streamlined and simple affair. The other factor is the simplicity of the system call handler and the individual system calls themselves.

> 5 You might be wondering why does *getpid()* return *tgid*, the thread group ID? In normal processes, the TGID is equal to the PID. With threads, the TGID is the same for all threads in a thread group. This enables the threads to call *getpid()* and get the same PID.