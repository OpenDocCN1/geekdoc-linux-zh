# Advanced Bash–Scripting Guide

By convention, a command reads its input from fd 0 (stdin), prints normal output to fd 1 (stdout), and error output to fd 2 (stderr). If one of these fds is not open, you may encounter problems:

```
bash cat /etc/passwd >&-
cat: standard output: bad file descriptor
```

For example, when xterm runs, it first initializes itself. Before running the user's shell, xterm opens the terminal device (/dev/pts/n or something similar) three times.

At this point, Bash inherits these three file descriptors, and command (child process) by Bash inherits them in turn, except when you redirect the command. Redirection means reassining one of the file descriptors to another (by a pipe, or anything similar). File descriptors may be reassigned locally for a command, a subshell, a while or if for loop or globally, for the remainder of the shell (using exec).

ls > /dev/null means running ls with fd 1 connected to /dev/null.

```
bash exec 2>/dev/null
bash lsof -a p -- -d0,1
COMMAND PID USER FD TYPE DEVICE SIZE NAME
lsof 3621 0u CH 136,1 3 /dev/pts/1
lsof 3620 1u CH 136,1 3 /dev/pts/1
lsof 3620 2w CH 136,1 120 /dev/null
```

```
bash bash -c 'lsof -a p -- -d0,1,2' | cat
COMMAND PID USER FD TYPE DEVICE SIZE NAME
lsof 3709 0u CH 136,1 3 /dev/pts/1
lsof 3709 1u CH 136,1 3 /dev/pts/1
lsof 3709 2w CH 136,1 3 /dev/pts/1
```

```
bash echo "$(lsof -a p -- -d0,1,2)" >&6
COMMAND PID USER FD TYPE DEVICE SIZE NAME
lsof 4226 0u CH 136,1 3 /dev/pts/1
lsof 4226 1w FIFO 0,0 7520 pipe
lsof 4226 2w FIFO 0,0 7520 pipe
```

This works for types of redirection.

# Exercise: Analyze the following script.

```
#! /usr/bin/env bash
mkfifo /tmp/fifo1 /tmp/fifo2
while read a; do echo "FIFO1: $a"; done < /tmp/fifo1 &
? exec 7 > /tmp/fifo1
exec 8>(while read a; do echo "FD8: $a, to fd7"; done >&7)
```

Appendix A. Detailed Introduction to I/O and I/O Redirection