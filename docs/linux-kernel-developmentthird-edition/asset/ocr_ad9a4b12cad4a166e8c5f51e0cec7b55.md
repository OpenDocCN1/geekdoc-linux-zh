Finally, the actual foo() system call is implemented. Because the system call must be compiled into the core kernel image in all configurations, in this example we define it in `kernel1/sys.c`. You should put it wherever the function is most relevant; for example, if the function is related to scheduling, you could define it in `kernel/sched.c`.

```
#include <asm/page.h>

/*
* sys_foo - everyone's favorite system call.
*
* Returns the size of the per-process kernel stack.
*/
asm(long) long sys_foo(void)
{
return THREAD_SIZE;
}

That is it! Boot this kernel and user-space can invoke the foo() system call.
```

# Accessing the System Call from User-Space

Generally, the C library provides support for system calls. User applications can pull in function prototypes from the standard headers and link with the C library to use your system call (or the library runtime that, in turn, uses your syscall.c). If you just wrote the system call, however, it is doubtful that glibc already supports it!

Thankfully, Linux provides a set of macros for wrapping access to system calls. It sets up the register contents and issues the trap instructions. These macros are named `__syscall{n}()`, where *n* is between 0 and 6. The number corresponds to the number of parameters passed into the syscall because the macro needs to know how many parameters to expect and, consequently, push onto registers. For example, consider the `open()` *defined as*

```
long open(const char *filename, int flags, int mode)
```

The syscall macro to use this system call without explicit library support would be

```
#define __NR_open 5
__syscall3(long, open, const char *, filename, int, flags, int, mode)
```

Then, the application can simply call open().

For each macro, there are 2 + 2 * n parameters. The first parameter corresponds to the return type of the syscall. The second is the name of the system call. Next follows the type and name for each parameter in order of the system call. The `__NR_open` define is in `<asm/unistd.h>;` it is the system call number. The `__syscall3` macro expands into a C function with inline assembly; the assembly performs the steps discussed in the previous section to push the system call number and parameters into the correct registers and issue