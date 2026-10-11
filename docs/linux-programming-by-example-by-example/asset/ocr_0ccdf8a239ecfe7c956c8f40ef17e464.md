library `malloc`'s shortcomings, such as memory fragmentation or the lack of automatic freeing of unused memory (garbage collection). You will also use system calls without realizing it. Almost every system call has a function of the same name in the standard C library. Moreover, many functions in the standard library invoke system calls, `printf`, for example, uses the `write` system call. You can also call `write` directly.

> * To find detailed coverage of the write system call, see "Reading and Writing Files," page 141.

# Using System Calls

Using system calls is as simple as calling a function. From the point of view of application programmers, the distinction between system calls and regular library functions is inconsequential. The interface is the same. To use them, all you need to do is include the header file `<unistd.h>` in your code.

Of course, you will need to understand what system calls do. Their behavior, parameters, and return values are documented in the section 2 manual pages. Because system calls have similarly named library functions, which are documented in the section 3 manual pages, it is generally wise to look at both sections to obtain a complete understanding of how they behave.

# *Common System Calls*

With over 190 system calls, it is beyond the scope of this book to discuss each one. Nevertheless, you learn many of them in other chapters. This section introduces the most common system calls, referring you to the appropriate chapters in which each group of calls is discussed.

# Process Management

Process management is covered in Chapter 4, "Processes." This group of system calls handles the creation and manipulation of programs. The `fork`, `vfork`, and `execve` calls create new processes. Similarly, `kill` and `exit` terminate processes. Processes have a unique PID, owner, creator and other identifiers that can be obtained with the system calls listed here:

+   - `getpid` Returns the calling process's process ID

+   - `getuid` Returns the user ID of the user that created the process

+   - `getgid` Returns the group ID of the user that created the process

+   - `getppid` Returns the calling process's parent process ID

+   - `geteuid` Returns the calling process's effective user ID

+   - `getegid` Returns the calling process's effective group ID