code. This code takes care (among other things) of arranging a possible input/output redirection and then replaces itself with the /bin/ls program file. At the end of the `ls` program, the child process ends, and the shell asks you for the next command.

The first process with the PID of 1 is created by the operating system kernel during boot. According to the convention this is a program called `/sbin/init`, and it is also called the “init process”. The init process is responsible for booting the system and, e. g., starting additional processes for system services running in the background.

**ps**  You can use the “`ps`” command to obtain information about the processes running on the system. In the simplest case, `ps` shows you all processes running on your current terminal (or, nowadays, the current terminal window on your graphical screen):

```
$ ps

PID TTY   STAT TIME COMMAND
 997 pts/8 S    0:00 -bash
1005 pts/8 R    0:00 ps
$ _
```

The PID and **COMMAND** columns speak for themselves. TTY gives the name of the terminal (“pts/something” usually refers to a terminal window), **TIME** the CPU time used by the processes so far, and **STAT** the “process state”.

A process on Linux is always in one of a number of states, namely (process state)

+   *   **Runnable (R)** The process may be assigned CPU time.
+   *   **Sleeping (S)** The process is waiting for an event, typically input or output—a key press or data from disk.
+   *   **In deep (uninterruptible) sleep (D)** The process is waiting for an event and cannot be disturbed. Processes should not remain in this state for too long because they can only be removed by booting the system. If that happens it is usually due to some error.
+   *   **Temporarily stopped (T)** The process was temporarily stopped by its owner or an administrator, but can continue running later on.
+   *   **Zombie (Z)** The process has really finished, but its exit code has not yet been picked up by its parent. This means the process cannot “die” but remains undead within the system. Unlike in real life, zombies are not really a problem because they do not take up resources other than a slot in the process table. If your system is infested with a horde of zombies, this indicates a problem with the program that created the processes in the first place—terminating that program should make the zombies disappear.

Use parameters to control which information `ps` provides. For example, you could enter a process number to find out about a particular process:

```
$ ps 1

PID TTY   STAT TIME COMMAND
 1 ?      Ss   0:00 init [2]
```

The `l` option gives you more detailed information about a process:

```
$ ps l $$

F   UID   PID  PPID PRI  NI VSZ  RSS WCHAN  STAT TTY      TIME COMMAND
 0  1000  3542 3491  20   0  21152 2288   -    Ss   pts/8  0:00 /bin/bash
```