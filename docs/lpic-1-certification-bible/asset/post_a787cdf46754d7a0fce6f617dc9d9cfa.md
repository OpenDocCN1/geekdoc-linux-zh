
| Setting | Meaning |
| :--- | :--- |
| \u | User name of the current user. |
| \h | The name of the computer running the shell (hostname). |
| \W | The base of the name of the current working directory. |
| \w | The full name of the current working directory. |
| \$ | Displays "$" for normal users and "#" for the root. |
| \! | History number of the current command. |
| \# | Number of the current command. |
| \d | Current date. |
| \t | Current time. |
| \s | Name of the shell. |
| \n | New line. |
| \\ | Backslash. |
| \[ | Begins a sequence of nonprintable characters. |
| \] | Ends a sequence of nonprintable characters. |
| \nnn | The ASCII character corresponding to the octal number nnn. |
| $(date) | Output from the date command (or any other command for that matter). |

## HOME

The HOME variable is used to represent the user's home directory. This directory is usually located in /home/username. So for a user with the user name angie, the home directory is located at /home/angie. This variable is useful with scripts that require the path to the user's home directory. The home directory setting for each user is contained in the /etc/passwd file.

## Managing Processes

### 1.3 GNU and UNIX Commands

- Create, Monitor, and Kill Processes. Includes running jobs in the foreground and background, bringing a job from the background to the foreground and vice versa, monitoring active processes, sending signals to processes, and killing processes. Includes using commands `ps`, `top`, `kill`, `bg`, `fg`, and `jobs`.

Whenever a command or job is executed in a shell, a process is created. Each process started is assigned a unique process id number or PID. These processes and PIDs can be viewed using the `ps` command. This command provides process status by presenting a snapshot of the current system processes. The information presented by the `ps` command is configured using a variety of switches. The most commonly used of these switches are shown in Table 2.5.

**Table 2-5: Switches Used with ps**

| Switch | Use |
| :--- | :--- |
| a | Displays processes for all users. |
| txx | Displays processes within controlling terminal txx. |
| u | Displays user information for the process. |
| l | Displays in long format with detailed information. |
| s | Displays information in signal format. |
| m | Displays memory information. |
| x | Displays processes without a controlling terminal. |
| S | Displays CPU time and page faults of child processes. |

In order to view all processes run on the system, the following command is used.

```bash
$ ps -aux
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 1 0.0 0.2 1120 372 ? S 18:26 0:05 init [3]
root 2 0.0 0.0 0 0 ? SW 18:26 0:00 [kflushd]
root 3 0.0 0.0 0 0 ? SW 18:26 0:00 [kupdate]
root 4 0.0 0.0 0 0 ? SW 18:26 0:00 [kpiod]
root 5 0.0 0.0 0 0 ? SW 18:26 0:00 [kswapd]
root 6 0.0 0.0 0 0 ? SWK 18:26 0:00 [mdrecoveryd]
root 272 0.0 0.5 1432 692 ? S 18:28 0:00 /sbin/pump -i eth
bin 316 0.0 0.3 1208 408 ? S 18:28 0:00 portmap
root 367 0.0 0.4 1172 528 ? S 18:28 0:00 syslogd -m 0
root 376 0.0 0.5 1436 760 ? S 18:28 0:00 klogd
nobody 390 0.0 0.4 1292 628 ? S 18:28 0:00 identd -e -o
nobody 394 0.0 0.4 1292 628 ? S 18:28 0:00 identd -e -o
nobody 395 0.0 0.4 1292 628 ? S 18:28 0:00 identd -e -o
nobody 396 0.0 0.4 1292 628 ? S 18:28 0:00 identd -e -o
nobody 397 0.0 0.4 1292 628 ? S 18:28 0:00 identd -e -o
```

The `ps` command is useful for providing a snapshot of the process status. However, there are times that you may want real-time information on the system processes. The `top` command is used for this purpose. Because this process itself is CPU intensive, it should be used only when necessary. The information presented by `top` can be arranged according to CPU usage, memory usage, and runtime. The most common way to run `top` is simply to type the command name at the command line. From within the `top` utility, type the `s` command and then specify the option that you wish to use. The options used with `top` are displayed in Table 2-6.

**Table 2-6: Options Used with top**

| Option | Use |
| :--- | :--- |
| d | Specifies the seconds between updates. |
| q | Specifies that there should be no delay between updates. |
| S | Specifies that child process information should be included in the information displayed. |
| s | Runs the process in secure mode. |
| i | Specifies that idle processes are to be ignored. |
| c | Displays the full command line of processes. |

Following is an example of the output produced by the `top` command. The `top` display is exited using the `q` key.

```bash
# top

11:51pm up 5:25, 3 users, load average: 0.00, 0.00, 0.00
43 processes: 42 sleeping, 1 running, 0 zombie, 0 stopped
CPU states: 0.1% user, 0.3% system, 0.0% nice, 99.4% idle
Mem: 127976K av, 124328K used, 3648K free, 47938K shrd, 88108K buff
Swap: 264056K av, 336K used, 263720K free 14080K cached

 PID USER PRI NI SIZE RSS SHARE STAT LIB %CPU %MEM TIME COMMAND
 902 root 18 0 856 856 668 R 0 0.5 0.6 0:00 top
 1 root 0 0 380 372 324 S 0 0.0 0.0 0:00 init
 2 root 0 0 0 0 0 SW 0 0.0 0.0 0:00 kflushd
 3 root 0 0 0 0 0 SW 0 0.0 0.0 0:00 kupdate
 4 root 0 0 0 0 0 SW 0 0.0 0.0 0:00 kswapd
 5 root 0 0 0 0 0 SW< 0 0.0 0.0 0:00 mdrecoveryd
 272 root -20 -20 0 0 0 SW< 0 0.0 0.0 0:00 pump
 316 bin 0 0 408 408 328 S 0 0.0 0.3 0:00 portmap
 367 root 0 0 528 528 428 S 0 0.0 0.4 0:00 syslogd
 376 root 0 0 760 760 388 S 0 0.0 0.5 0:00 klogd
 390 nobody 0 0 628 628 520 S 0 0.0 0.4 0:00 identd
 394 nobody 0 0 628 628 520 S 0 0.0 0.4 0:00 identd
 395 nobody 0 0 628 628 520 S 0 0.0 0.4 0:00 identd
 396 nobody 0 0 628 628 520 S 0 0.0 0.4 0:00 identd
 397 nobody 0 0 628 628 520 S 0 0.0 0.4 0:00 identd
 408 root 10 0 620 620 512 S 0 0.0 0.4 0:00 crond
 426 root 0 0 488 488 412 S 0 0.0 0.3 0:00 inetd
 436 root 0 0 1096 1096 968 S 0 0.0 0.8 0:00 sshd
 451 root 0 0 532 532 448 S 0 0.0 0.4 0:00 lpbd
```

There may be times that a process stops responding and must be terminated. This is done using the `kill` command. The `kill` command is used with the following syntax:

```bash
kill -s signal process
```

The process can be specified using the PID or the process name. Only the root user has the ability to kill processes belonging to another user. The default signal sent to a process with the `kill` command is the TERM signal. It is also possible to specify other signals with this command. The most common signal levels and their meanings are shown in Table 2-7.

**Table 2-7: Common Signal Levels and Meanings**

| Signal | Meaning |
| :--- | :--- |
| 1 | SIGHUP. Stops and restarts the process. |
| 9 | SIGKILL. Stops a process without allowing it to exit gracefully. |
| 15 | SIGTERM. Stops a process by allowing it to exit. |

A list of all available signal levels can be viewed using the `-l` option, as shown in the following example:

```bash
# kill -l
1) SIGHUP 2) SIGINT 3) SIGQUIT 4) SIGILL
5) SIGTRAP 6) SIGIOT 7) SIGBUS 8) SIGFPE
9) SIGKILL 10) SIGUSR1 11) SIGSEGV 12) SIGUSR2
13) SIGPIPE 14) SIGALRM 15) SIGTERM 17) SIGCHLD
18) SIGCONT 19) SIGSTOP 20) SIGTSTP 21) SIGTTIN
22) SIGTTOU 23) SIGURG 24) SIGXCPU 25) SIGXFSZ
26) SIGVTALRM 27) SIGPROF 28) SIGWINCH 29) SIGIO
30) SIGPWR 31) SIGSYS
```

An example of using the `kill` command to restart a process is shown below.

```bash
# kill -1 408
```

Some processes occupy the shell until they are completed. These processes are said to run in the foreground. No other processes can be started at the shell until these processes are completed. Other processes are said to run in the background. When a process runs in the background, the shell is available so that new processes can be started while the background process is running. Whether a process runs in the foreground or background depends on the process and how it is started. Typically, commands run from the command line are run in the foreground. To start a command-line process in the background, the `&` symbol is placed at the end of the command. The following is an example of starting the `netscape` process as a background process.

```bash
# netscape &
```

Running the process this way frees the shell to receive other commands while the `netscape` process runs. If you wish to move a current process from the foreground to the background, another method is used. The `^Z` command will stop a process running in the foreground. Once the process has been stopped, it can be moved into the background using the `bg jobnumber` command. The jobnumber will be discovered using the `jobs` command. This command will display the processes currently running in the background as well as stopped jobs. An example of the correct use of these commands is as follows:

```bash
# netscape
^Z
# jobs
[2]- Stopped netscape
# bg 2
```

In the above example, the `netscape` process is started and then stopped using the `^Z` command. The `jobs` command is then used to view the jobs currently running in the background as well as those that are stopped. Then the `bg` command is used to move the `netscape` process to the background.

It is also possible to move a process from the background to the foreground. This is done using the `fg jobnumber` command. To move the `netscape` process in the example above back to the foreground, the following command would be used:

```bash
# fg 2
```
