
# CHAPTER 1 | Monitoring Linux Processes

- Unique process identification (PID)
- CPU and real time already expended
- How much memory the process has allocated in various locations
- The location of process stdout, known as the controlling terminal
- The current process state

> IMPORTANT
The Linux version of ps supports three option formats:

- UNIX (POSIX) options, which may be grouped and not preceded by a dash
- BSD options, which may be grouped and not used with a dash
- GNU long options, which are preceded by two dashes
For example, `ps -aux` is not the same as `ps aux`.

The most common set of options, aux, displays all processes including without a controlling terminal. A long listing (options axax) provides more technical detail, but may display faster by avoiding user lookups. The similar UNIX syntax uses the options `ef` to display all processes.

```
[user@host]$ ps aux
USER PID %MEM VSZ RSS T STAT TIME COMMAND
root 1 0.1 0.1 51648 7504 ? S 17:45 0:03 /usr/lib/systemd/
system
root 2 0.0 0.0 0 ? S 17:45 0:00 [kthread]
root 3 0.0 0.0 0 ? S 17:45 0:00 [ksftirqd/0]
root 5 0.0 0.0 0 ? S< 17:45 0:00 [kworker/0:OH]
root 7 0.0 0.0 0 ? S 17:45 0:00 [migration/0]
```

```
...output omitted...
[user@host]$ ps -ef
UID PID PPID NI RSS WORD CHAN TTY TIME COMMAND
F 0 1 2 0 51648 ep_pol S ? 0:00 /usr/lib/systemd/
1 0 2 0 0 0 kthread S ? 0:00 [kthread]
1 0 3 2 0 0 smbpo S ? 0:00 [ksftirqd/0]
1 0 5 2 -2-0 worker S< ? 0:00 [kworker/0:OH]
1 0 7 2 -100 0 smbpo S ? 0:00 [migration/0]
...output omitted...
```

```
[user@host]$ ps -aux
UID PID PPID C TIME TTY TIME COMMAND
root 1 0 17:45 ? 00:00:00 /usr/lib/systemd/systemd --nitched-ro
root 2 0 17:45 ? 00:00:00 [kthread]
root 3 2 17:45 ? 00:00:00 [ksftirqd/0]
root 5 2 17:45 ? 00:00:00 [kworker/0:OH]
root 7 2 17:45 ? 00:00:00 [migration/0]
...output omitted...
```

By default, ps with no options selects all processes with the same effective ID (EUID) as the current user, and which are associated with the same terminal where ps was invoked.

- Processes in brackets (usually at the top of the list) are scheduled kernel threads.
- Zombies are listed as exiting or defunct.
- The output of ps displays once. Use top for a process display that dynamically updates.
- ps can display in tree format so that you can view relationships between parent and child processes.
- The default output is sorted by process ID number. At first glance, this may appear to be chronological order. To sort, use the -o or --sort options. Display order matches that of the system process table, which reuses rows as processes that die and new ones are created. Output may appear chronological, but is not guaranteed unless -o or --sort options are used.

# REFERENCES

> info libc signal (GNU C Library Manual) - Section 24: Signal Handling
- info libc processes (GNU C Library Manual) - Section 26: Processes
- ps(1) and signal(7) man pages

4. Which state represents a process that is sleeping until some condition is met?
a. D
b. R
c. S
d. T

# SOLUTION

# LISTING PROCESSES

Choose the correct answers to the following:

1. Which state represents a process that has been stopped or suspended?
a. D
b. R
c. S
d. T
e. Z

2. Which state represents a process that has released all its resources except its PID?
a. D
b. R
c. S
d. T
e. Z

3. Which process does a parent use to duplicate and create a new process?
a. exec
b. fork
c. zombie
d. syscall
e. reap

4. Which state represents a process that is sleeping until some condition is met?
a. D
b. R
c. S
d. T

# CHAPTER 8 | Monitoring and Managing Linux Processes

# CONTING JOBS

After completing this section, you should be able to use Bash job control to manage multiple processes started from the same terminal.

# DESCRIBING JOBS AND SESSIONS

Job control is a feature of the shell which allows a single shell instance to run and manage multiple commands. A job is associated with each pipeline entered at a shell prompt. All processes in the pipeline are members of the same process group. If only one command is entered at a shell prompt, it can be considered a "pipeline" of one command, creating a job with only one member.

Only one job can read input and keyboard generated signals from a particular terminal at a time. Processes that are part of it are foreground processes of the controlling terminal. A background process of that terminal is a member of any other job associated with that terminal. Background processes cannot read input or receive keyboard interrupts from the terminal, but may be able to write to it. A job in the background may be stopped (suspended) or it may be running. If a running background job tries to read from the terminal, it will be automatically suspended.

Each terminal is its own session, and can have a foreground process and any number of background processes. A job is part of exactly one session: the one belonging to its controlling terminal. The ps command shows the device name of the controlling terminal of a process in the TTY column. Some processes, such as system daemons, are started by the system and not from a shell prompt. Processes that do not have a controlling terminal are not members of a job and cannot be brought to the foreground. The ps command displays a question mark (?) in the TTY column for these processes.

# RUNNING JOBS IN THE BACKGROUND

Any command or pipeline can be started in the background by appending an ampersand (&) at the end of the command line. The Bash shell displays a job number (unique to the session) and the PID of the new process. The shell does not wait for the child process to terminate, but rather displays the shell prompt.

```
[user@host]$ sleep 10000 &
[1] 5947
[user@host]$

```

NOTE
When a command line containing a pipe is sent to the background using an ampersand, the PID of the last command in the pipeline is used as output. All processes in the pipeline are still members of that job.

```
[user@host]$ example_command | sort | mail -s "Sort output" &
[1] 5998
```

You can display the list of jobs that Bash is tracking for a particular session with the jobs command.

```
[user@host]$ jobs
[1]+ sleep 10000 &
[user@host]$]$
```

A background job can be brought to the foreground using the fg command with its job ID (%job number).

```
[user@host]$ fg %1
sleep 10000
```

In the preceding example, the sleep command is now running in the foreground on the controlling terminal. The shell itself is again asleep, waiting for this process to exit.

To send a process to the background, first press the keyboard generated suspend request (Ctrl+Z) in the terminal.

```
sleep 10000
^Z
[1]+ Stopped sleep 10000
[user@host]$
```

The job is immediately placed in the background and is suspended.

The ps j displays information relating to jobs. The PID is the unique process ID of the process. The PPID is the PID of the parent process of this process, the process that started (forked). The PGID is the PID of the process group leader, normally the first process in the job's pipeline. The SID is the PID of the session leader, which for a job is normally the interactive shell that is running on its controlling terminal. Since the example command is currently suspended, its process state is T.

| PPID | PGID | TTY | TPGID | SID | UID | COMMAND |
| --- | --- | --- | --- | --- | --- | --- |
| 2764 | 2768 | 2768 | pts/0 | 6337 | 1000 | 00:00 /bin/bash |
| 2768 | 5947 | 5947 | 2768 pts/0 | 6337 | 1000 | 00:00 sleep 10000 |
| 2768 | 6337 | 6337 | 2768 pts/0 | 6337 | R+ | 1000 | 00:00 ps j |

To start the suspended process running in the background, use the bg command with the same job ID.
