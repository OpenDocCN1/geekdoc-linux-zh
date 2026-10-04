is to be run in the background (backgnd==TRUE) then SIGCHLD is set so that zombie child processes will not be created when the child processes terminate. This is the correct action here because the shell won't be wait()ing for them. If the command line will be run in the foreground then SIGCHLD is set to its default action, which also causes the system to generate zombies from child processes when they die, until the shell wait()s for them.

+   4. The next section is a loop, the body of which will be executed once for each simple command in the command line, with the variable i specifying which simple command to work on next.
5. The value j-1 gives the command number of the last simple command in the command line. Where this value is greater than zero, it means that there is more than one simple command in the pipeline. For each simple command whose number is less than j-1 a pipe needs to be created to pipe the output (outfd) of command number i to the input (infd) of command number i+1.
6. All the file descriptors and command line parameters needed by command number i are now available and ready so that simple command i can now be executed. The forkexec() function does just what its name implies - it creates a child process to run a simple command. Therefore, only in the parent process does the forkexec() function return.
7. If any I/O redirection or pipes were involved in the simple command that has just been started then the parent's copies of the file descriptors are closed here.
8. Finally, when all the simple commands have been started, if this command line is running in the foreground then the parent (tiny shell) process enters a loop to wait() for the termination of the last process in the pipeline, whose process ID will have been set in lastpid by the forkexec() function.

# 20.2.7 forkexec Function

The forkexec() function has the task of creating a child process with the fork() system call Then within the child process it performs any required I/O redirection before using execvp() to execute the required command.

```
forkexec(struct cmd *ptr)
{
    int i,pid;

    /* 1 */
    if (pid = fork())
    {
        /* 2 */
        if (backgnd==TRUE)
            printf("%d\n", pid);
```