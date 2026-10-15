
There are only two ways for a process to terminate: either "normally" by calling one of various exit functions⁶ such as `exit()`, or "abnormally" and involuntarily as a result of receiving a signal that killed it, or calling `abort()`. (When a program either reaches the end of its code or executes a return, this results in an implicit call to `exit()`.) In either case, the parent can call `wait()`

⁶There are two other exit functions, including `_exit()` and `_Exit()`.

![](img/edd55012c780b4e999320d08ab27959e_400_0.png)

## 图 7.5：双字节退出状态。

to determine the cause of termination. There are three different POSIX-compliant `wait()` system calls:

```
#include <sys/types.h>
#include <sys/wait.h>

pid_t wait(int *status);
pid_t waitpid(pid_t pid, int *status, int options);
int waitid(idtype_t idtype, id_t id, siginfo_t *infop, int options);
```

The `wait()` function causes the executing process to suspend its execution until any one of its children terminates. When a child terminates, the kernel sends a `SIGCHLD` signal to its parent, unless the parent has indicated that it does not want these signals. Upon receipt of a `SIGCHLD` signal, the parent resumes in the `wait()` code. The return value of `wait()` is the process-id of the child that just terminated or was just killed. It does not matter which child terminates. The process is resumed if any child terminates. If a process calls `wait()` but it has no children, `wait()` returns immediately with a `-1`.

The purpose of the `status` parameter is to receive information about how the child terminated. It is a pointer to a two-byte integer. If the child terminated normally using the `exit()` call, then the high-order byte of the value received by `wait()` contains the low-order byte of the integer passed in the `exit()` call's argument, and the low-order byte of the received value is 0. If the child terminated abnormally because of an unhandled signal, then the low-order byte of the received value contains the signal value. If the child was terminated by a signal, then in particular bit 7 is set if there was a core dump. Figure 7.5 shows how the two bytes of the `status` are arranged.

Based on these facts, the following code can be used for querying and extracting the status and signal state:

```
if ((status & 0x000000FF) ==0)
    /* low-order byte is zero, so high-order byte has status */
    exitStatus = status >> 8;  /* exitStatus contains exit status */
else {
    signum = status%128;  /* signum contains signal */
    if ( status & 0x00000080 )
```

> 7 The convention when using `exit()` is to supply a zero on success and some non-zero value on failure.

> 8 The fact that a core dump is supposed to occur does not mean that there will be a core file in your working directory. If your shell has been configured so that core dumps are disabled, then you will not see the file. On some systems, you can enable the core dump by running the command "`ulimit -c unlimited`", which allows your processes to create core files of unlimited size. The `ulimit` command is part of `bash` and you can read the `bash` man page for more details.

```
/* core dump took place */
}
```

However, using the following macros, which are defined in `<sys/wait.h>`, makes the code more portable:

```
if (WIFEXITED(status))
    /* true implies exit() was called to terminate the child  */
    exit_status = WEXITSTATUS(status); /* extract exit status */
else if ( WIFSIGNALED(status) ) {
    /* true if signal killed child */
    signum = WTERMSIG(status); /* extract signal that killed child */
#ifdef WCOREDUMP
    if ( WCOREDUMP(status) )
        /* true if a core dump took place  */
#endif
}
```

- The `WIFEXITED(status)` macro returns true if the child terminated normally, i.e., by calling `exit(3)` or `_exit(2)`, or by returning from `main()`. In this case the `WEXITSTATUS(status)` macro returns the exit status of the child. This macro should only be employed if `WIFEXITED()` returned true.
