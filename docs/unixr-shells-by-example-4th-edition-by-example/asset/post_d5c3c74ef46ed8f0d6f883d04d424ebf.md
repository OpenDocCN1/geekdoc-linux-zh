
## EXAMPLE 1.4

(C/TC Shell)

```
1 % cp filex filey
% echo $status
0
2 % cp xyz
Usage: cp [-ip] f1 f2; or: cp [-ipr] f1 ... fn d2
% echo $status
1
```

(Bourne, Bash, Korn Shells)

```
3 $ cp filex filey
$ echo $?
0
$ cp xyz
Usage: cp [-ip] f1 f2; or: cp [-ipr] f1 ... fn d2
$ echo $?
1
```

## EXPLANATION

1 The cp (copy) command is entered at the C shell command-line prompt. After the command has made a copy of filex called filey, the program exits and the prompt appears. The csh status variable contains the exit status of the last command that was executed. If the status is zero, the cp program exited with success. If the exit status is nonzero, the cp program failed in some way.

2 When entering the cp command, the user failed to provide two filenames: the source and destination files. The cp program sent an error message to the screen and exited with a status of 1. That number is stored in the csh status variable. Any number other than zero indicates that the program failed.

3 The Bourne, Bash, and Korn shells process the cp command as the C shell did in the first two examples. The only difference is that the Bourne and Korn shells store the exit status in the ? variable, rather than the status variable.

![](img/60a0b5d254bd6007403850f972cbfad8_54_0.png)

## EXPLANATION

- 1. The parent shell creates a copy of itself with the fork system call. The copy is called the child shell.
- 2. The child shell has a new PID and is a copy of its parent. It will share the CPU with the parent.
- 3. The kernel loads the grep program into memory and executes (exec) it in place of the child shell. The grep program inherits the open files and environment from the child.
- 4. The grep program exits, the kernel cleans up, and the parent is awakened.

## Killing Processes.

A process can be terminated by using keystroke-generated signals like Ctrl-C or Ctrl-\, or by using the kill command. This command may be used for killing background jobs or, if your terminal is in a frozen, unresponsive state, to kill the process that is causing the problem. The kill command is a built-in shell command that terminates a process by its PID or, if using job control, by the number of the job. To find the PID number, the ps command is used. See Example 1.5.

## EXAMPLE 1.3

```
1 $ sleep 60&
2 $ ps
PID TTY TIME CMD
27628 pts/7 0:00 sleep
27619 pts/7 0:00 bash
27629 pts/7 0:00 ps
3 $ kill 27628
4 $ ps
PID TTY TIME CMD
27631 pts/7 0:00 ps
27619 pts/7 0:00 bash
[1]+ Terminated sleep 60
```

## EXPLANATION

- 1 The sleep command does nothing, just pauses for 60 seconds, and is running in the background due to the ampersand at the end of the command
- 2 The ps command displays the currently running processes for this user.
- 3 The kill command is a built-in shell command. It takes, as an argument, the PID of the process it will kill. The PID for the sleep command is entered.
- 4 The ps command demonstrates that the sleep command has been terminated.

## 1.6 The Environment and Inheritance

When you log on, the shell starts up and inherits a number of variables, I/O streams, and process characteristics from the /bin/login program that started it. In turn, if another shell is spawned (forked) from the login or parent shell, that child shell (subshell) will inherit certain characteristics from its parent. A subshell may be started for a number of reasons: for handling background processing, for handling groups of commands, or for executing scripts. The child shell inherits the environment of its parent. The environment consists of process permissions (who owns the process), the working directory, the file creation mask, special variables, open files, and signals.

### 1.6.1 Ownership and Permissions

When you log on, the shell is given an identity. It has a real user identification (UID), one or more real group identification (GID), and an effective user identification and effective group identification (EUID and EGID). The EUID and EGID are initially the same as the real UID and GID. These ID numbers are found in the etc/passwd file and are used by the system to identify users and groups. The EUID and EGID determine what permissions a process has access to when reading, writing, or executing files. If the EUID of a process and the real UID of the owner of the file are the same, the process has the
