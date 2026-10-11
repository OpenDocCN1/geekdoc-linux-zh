A sample run produced the following output:

![](bbox=[0.03, 0.11, 0.16, 0.155])

# ### Output

```
$ ./waiter
in child
    child pid = 4502
    child ppid = 4501
in parent
    parent pid = 4501
    parent ppid = 4429
    child exited with 0
```

This program is similar to the previous child.c, except that it adds a waitpid statement. It specifically waits for the child process specified by child to return and also displays the child’s exit status. Notice that output from the parent and child processes is not mixed together like it was in child.c. The parent process’s execution stops until the child exits. waitpid (and wait) returns the PID of the child that exited, 0 if WNOHANG was specified in options, or -1 if an error occurs.

# ## Killing Processes

A process can terminate for one of five reasons:

+   - Its main function calls return
+   - It calls exit
+   - It calls _exit
+   - It calls abort
+   - It is terminated by a signal

The first three reasons are normal terminations, the last two are abnormal terminations. Regardless of why a process terminates, though, the same kernel code eventually executes, closing open files, releasing memory resources, and performing any other required cleanup. Because this book assumes C programming competency, hopefully the return function needs no explanation.

# ## The exit Functions

You have seen the exit function, which is part of C’s standard library, used in programs throughout this chapter. Rather than provide another example, its prototype is listed, as declared in <stdlib.h>:

```
int exit(int status);
```

exit causes normal program termination and returns status to the parent process. Functions registered with atexit are executed.