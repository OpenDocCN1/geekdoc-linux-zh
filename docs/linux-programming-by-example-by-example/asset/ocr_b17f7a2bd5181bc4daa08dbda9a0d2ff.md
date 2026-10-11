called the *session ID*, which is merely the PID of the session leader. Sessions serve the same purpose for process groups as process groups serve for individual processes.

Say that you execute the same pipeline command mentioned earlier (that is, `ls -l /usr/include | sort | wc -l &`) in the background and execute other commands in the foreground. Now, if you are running these commands in an X Window terminal and shut down the terminal window while all these processes are running, the kernel sends a signal to the controlling process (the session leader), which in turn kills each process group as described in the previous paragraph.

Manipulating process groups and sessions is an advanced topic and is beyond the scope of this book. It is important, however, to understand the concepts and terminology because they have important implications for signals, which are covered in Chapter 5, "Signals."

# ## Manipulating Processes

This section discusses creating new processes, killing existing processes, and waiting on and monitoring processes. The `system`, `fork`, and `exec` calls create new processes. The `kill` function can be used to kill other processes, and a process can call either `exit` and `abort` in order to kill itself. Good resource management requires that parent processes wait for their children to terminate. The various `wait` functions handle this requirement.

# ### Creating Processes

Programmers frequently need to create new processes from within their programs. For example, suppose you create a program that manages a database of CD-ROM titles. Rather than having to create your own sorting routine, you would like to use the `sort` program to do the work. Linux provides three ways to accomplish this. The `system` call, provided by the standard C library, is one method. The `fork` and `exec` calls, however, are the "Linux way." This section looks at all three calls.

# ### Using system

The `system` function executes a shell command passed to it. Its prototype, declared in `<stdlib. h>`, is

```
```c
int system(const char *string);
```
```

`system` executes the shell command `string` by passing it to `/bin/sh`, returning after the command completes. Previous examples have demonstrated its use already. If, for some reason, `system` fails to invoke `/bin/sh`, it returns `127`. If another error occurs, `system` returns `-1`. The normal return value of `system` is the exit code of the command passed in `string`. If `string` is `NULL`, `system` returns 0 if `/bin/sh` is available or non-zero if it is not.