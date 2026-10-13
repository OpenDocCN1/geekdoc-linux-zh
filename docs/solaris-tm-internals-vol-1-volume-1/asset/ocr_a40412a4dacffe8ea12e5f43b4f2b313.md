mon (PID 2), and `fsflush` (PID 3). These processes are created by an internal kernel `newproc()` function. The mechanics of process creation are illustrated in Figure 8.12.

![](bbox=[0.175, 0.207, 0.889, 0.456])

The `fork(2)` and `exec(2)` system calls are used extensively in the various software components that come bundled with Solaris as well as in hundreds of applications that run on Solaris. (However, more and more Solaris daemons and applications are being threaded with each release, which means that the programs use threads as an alternative to multiple processes.)

The `fork(2)` system call creates a new process. The newly created process is assigned a unique process identification (PID) and is a child of the process that called `fork`; the calling process is the parent. The `exec(2)` system call overlays the process with an executable specified as a path name in the first argument to the `exec(2)` call. The model, in pseudocode format, looks like this:

```
main(int argc, char *argv[], char *envp[]) {
        pid_t child_pid;
        child_pid = fork();
        if (child_pid == -1)
                perror("Fork\n"); /* fork system call failed */
        else if (child_pid == 0)
                execv(R/path/new_binaryS,argv); /* in the child, so exec */
        else
                wait()  /* pid > 0, we're in the parent */
}
```

The pseudocode above calls `fork(2)` and checks the return value from `fork(2)` (pid). Remember, once `fork(2)` executes successfully, there are two processes: `fork` returns a value of 0 to the child process and returns the PID of the child to the parent process. In the example, we called `exec(2)` to execute `new_binary` once in