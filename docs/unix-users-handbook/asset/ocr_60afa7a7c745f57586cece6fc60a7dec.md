>0	An error occurred.

# EXAMPLES

The command:

```
kill 6135
```

signals process number 6135 to terminate. This gives the process an opportunity to exit gracefully (removing temporary files, etc.).

The following equivalent commands:

```
kill -s SIGKILL 6135
kill -s KILL 6135
kill -s 9 6135
kill -SIGKILL 6135
kill -KILL 6135
kill -9 6135
```

terminate process number 6135 abruptly by sending a SIGKILL signal to the process. This tells the kernel to remove the process immediately.

# WARNINGS

If a process hangs during some operation (such as I/O) so that it is never scheduled, it cannot die until it is allowed to run. Thus, such a process may never go away after the kill. Similarly, defunct processes (see ps(1)) may have already finished executing, but remain on the system until their parent reaps them (see wait(2)). Using kill to send signals to them has no effect.

Some non-HP-UX implementations provide kill only as a shell built-in command.

# DEPENDENCIES

This manual entry describes the external command /usr/bin/kill and the built-in kill command of the POSIX shell (see sh-posix(1)). Other shells, such as C and Korn (see csh(1) and ksh(1) respectively), also provide kill as a built-in command. The syntax for and output from these built-ins may be different.

# SEE ALSO

csh(1), ksh(1), ps(1), sh(1), sh-bourne(1), sh-posix(1), kill(2), wait(2), signal(5).

# STANDARDS CONFORMANCE

kill: SVID2, SVID3, XPG2, XPG3, XPG4, POSIX.2