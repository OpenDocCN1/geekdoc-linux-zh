
```
$ nohup find / -name foo -print 1> foo.paths 2> /dev/null &
[1] 62808
$ kill -1 62808
$ jobs
[1]+ Running  nohup find / -name foo -print > foo.paths 2> /dev/null &
$ kill 62808
$ <Enter>
[1]+ Terminated  nohup find / -name foo -print > foo.paths 2> /dev/null
$ jobs
$
```

If you separate commands with semicolons, you can run them with nohup. In the following session, GenData generates some data and puts it in a file called employees, and the sort command sorts the file and stores the sorted version in the employees.sorted file.

```
$ nohup GenData > employees ; sort employees > employees.sorted &
[2] 15931
$
```

In the following in-chapter exercises, you will use the kill command to practice abnormal termination of processes, and the nohup and ps -a commands to appreciate how you can run processes that do not terminate when you log out.

## EXERCISE 10.7

Give a command for terminating processes with PID 10974 and jobID 3.

## EXERCISE 10.8

Run the first of the nohup commands, use ps to verify that the command is executing, log out, log in again, and use the ps -a command to determine whether the find command is running.

## 10.7 PROCESS HIERARCHY IN UNIX

When you turn on your UNIX system, the kernel—after performing some checks and other household tasks—creates the first process from scratch. In PC-BSD, this process is called kernel and in Solaris it is called sched. This process, which has no parent, has PID 0. The PPID of this process is also 0. It then spawns several other processes, which are meant to handle several important kernel tasks, including tasks related to virtual memory, file handling, interrupt handling, and performing various tasks at boot time such as

initializing hardware ports. A list of a few of these processes and their purpose is given in Table 10.12.

### TABLE 10.12 Some of the Key Processes Created by kernel (on PC-BSD) and sched (on Solaris)

| PC-BSD | Solaris | Purpose |
|---|---|---|
| init | init | Granddaddy of all user processes; all user-level services, including all Internet services, and user processes run under the children of this process. |
| pagedaemon | pageout | Read/write pages from/to disk |
| bufdaemon | fsflush | Supplies clean pages/buffers by writing dirty pages/buffers to disk |
| zfskern | zpool-rpool | Performs I/O tasks related to ZFS pools |
| intr | intrd | Handles all interrupts (lower-half of the kernel) |
| vmdaemon | vmtasks | Moves processes from main memory to disk storage |

The init process is the granddaddy of all user processes that are created, so long as the system is up and running. The init process has a PID of 1 and runs with superuser privileges. The executable binary for the process is in the file /sbin/init under PC-BSD and in /usr/sbin/init under Solaris. This process, after performing several activities, as given in the /etc/rc file, reads the /etc/ttys file to determine which I/O (terminal) lines are to be active. For each active line, init starts a getty process from /etc/getty. The getty process, also running in superuser mode, sets terminal attributes, such as baud rate, as specified in the file /etc/termcap. It then displays the login: prompt, inviting you to log on to the terminal.

At the login: prompt, when you type your login name and press <Return>, the getty process forks a child. The child process executes the exec system call to become a login process with your login name as its parameter. The login process prompts you for your password and checks the validity of your login name and password. If it finds both to be correct, the login process execs to become your login shell. If the login process does not find your login name in the /etc/passwd file or finds that the password that you entered does not match the one in the /etc/passwd file, it displays an error message and terminates. Control goes back to the getty process, which redisplays the login: prompt. Once in your login shell, you can do your work and terminate the shell by pressing <Ctrl+D> or running the exit command. When you do so, the shell process terminates and control goes back to the getty process, which displays the login: prompt, and life goes on.

When you login through the ssh command, the sshd daemon (the Secure Shell server process) on the remote machine creates a child sshd process for you (your private sshd) that handles communication with your client. The server sshd goes back and looks for more SSH connection requests from other clients. Your private sshd spawn another sshd process that overwrites itself with a pseudo terminal pts/1, which prompts you for the password. When you enter the correct password, it runs the login shell process for you. By default, the login shell is C shell on PC-BSD and Bash on Solaris. You run your commands under your
