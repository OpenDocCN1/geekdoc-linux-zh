
## Listing 10.1 Continued

```bash
suspend
printf "%s\n" "Who woke me up?"
exit 0
```

When this script runs, it is stopped until a SIGCONT is received.

```bash
$ bash suspend_demo.sh &
[1] 9185
$ 
[1]+  Stopped                bash suspend_demo.sh
$ kill -SIGCONT 9185
$ Who woke me up?
[1]+  Done                   bash suspend_demo.sh
$ 
```

## Traps

While Bash is running interactively, it handles most signals on behalf of the user. When a script is running and special actions need to be taken, it is the responsibility of the script to handle the appropriate signals. The action taken by Bash depends on which signal was received.

- SIGQUIT is always ignored
- SIGTIN is ignored if job control is enabled; otherwise, it suspends the script
- SIGTTOU is ignored if job control is enabled; otherwise, it suspends the script
- SIGSTOP is ignored if job control is enabled; otherwise, it suspends the script
- SIGTSTP is ignored if job control is enabled; otherwise, it suspends the script
- SIGHUP is sent to all background tasks started by the script, waking up stopped tasks if necessary

For example, Bash normally handles the SIGHUP signal by passing the signal to all sub-scripts (unless `disown -h` is used). You can activate the same behavior in an interactive session by setting the `huponexit` shell option: When a session is terminated, SIGHUP is sent to all running jobs.

Other signals terminate a script unless a signal handler (or trap) is created. A trap is a set of commands that executes when a signal is received. The built-in `trap` command manages the signal handlers for a script.

The `-l` (list) switch lists all signals and their corresponding numbers.

Not all signals can be caught with traps. Some signals, such as SIGKILL, always terminate a script even if a signal handler is installed.

Signal handlers are created by supplying a command and a list of handlers to the `trap` command. Either the signal name or number can be used. SIGWINCH, for example, is the signal generated when a window changes its size. By installing a trap, a message can be displayed each time the window is resized.

```bash
$ trap "printf \"There are %s lines\n\" \"${LINES}\"" SIGWINCH
```

Altering the window size results in:

```bash
$ There are 32 lines
$ There are 43 lines
$ There are 37 lines
```

You can view the current trap with the `-p` (print) switch.

```bash
$ trap -p SIGWINCH
trap -- 'printf "There are %s lines\n" "${LINES}"' SIGWINCH
```

To restore the default handler, don’t supply a trap.

```bash
$ trap SIGWINCH
$ trap -p SIGWINCH
```

SIGUSR1 and SIGUSR2 are user-defined signals that have no pre-defined meaning. They can be freely used in scripts. When the following script receives a SIGUSR1 signal, it waits for the current command to complete, prints the message SIGUSR1, and resumes the script, as shown in Listing 10.2.

## Listing 10.2 trap_demo.sh

```bash
#!/bin/bash
#
# trap_demo.sh
#
# Wait indefinitely for SIGUSR1, print a message when one arrives.

shopt -s -o nounset
trap 'printf "SIGUSR1\n"' SIGUSR1

# Infinite loop!
while true ; do
    sleep 1
done

printf "%s\n" "Should never get here!" >&2
exit 192
```

The script continues until killed.

```bash
$ bash trap_demo.sh &
[1] 544
$ kill -SIGUSR1 544
SIGUSR1
$ kill 544
[1]+  Terminated              bash trap_demo.sh
```

The two most common uses for signal handlers are to awaken suspended scripts and to temporarily block signals for some critical commands that must not be interrupted. To temporarily ignore a signal, use empty quote marks or the `null` command as a signal handler and restore the original signal handler after the uninterruptable commands are finished.

```bash
trap : SIGINT SIGQUIT SIGTERM
# some command that must not be interrupted
trap SIGINT SIGQUIT SIGTERM
```

## Exit Handlers

An exit handler is a set of commands executed whenever a script is finished. Exit handlers use the non-existent signal `EXIT` (signal number 0), as shown in Listing 10.3.

## Listing 10.3 exithrap_demo.sh

```bash
#!/bin/bash
#
# exithrap_demo.sh
#
# Display "Goodbye" when this script exits.

shopt -s -o nounset
trap 'printf "Goodbye\\n"' EXIT

sleep 5

exit 0
```

When the shell is exited, the message `Goodbye` is printed.

```bash
$ bash exithrap_demo.sh
Goodbye
```

When there is a lot of cleaning up to do, exit handlers usually invoke a shell function to perform the work. Shell functions are described in Chapter 14, "Functions and Script Execution."

## The killall Command

The Linux `killall` command kills by a program name instead of by a process ID number. As the name suggests, all matching jobs are killed. If an absolute path is specified, only processes running a particular file are killed.

```bash
$ sleep 15 &
[1] 1225
$ killall sleep
[1]+ Terminated               sleep
```

There are a number of switches for `killall`. The `-e` switch doesn’t kill swapped out processes with long filenames. The `-g` switch kills the process group. The `-i` switch prompts before killing. The `-q` switch suppresses the warning when no processes are killed. The `-w` switch forces `killall` to wait until all processes have finished running.

## Being Nice

All Linux programs run with a priority number between -20 and 19. The priority indicates the importance of the program, with lower numbers getting more time running than higher numbers.

The Linux `nice` command changes the priority of a command. `nice` should always be used when a script consumes a lot of resources in order to prevent more important jobs, such as handling user sessions, from being slowed or interrupted. Background tasks are automatically niced by Bash when they are started.

By default, `nice` reduces the priority (that is, it increases the priority number) by 10. Any number can be used, but the priority can only be reduced and it can never be less than 19. (The superuser, however, can reduce or increase the priority of any program.) The adjustment can be specified as a number after a minus sign, or by using the more readable `--adjustment=VALUE` (or `-n VALUE`) switch.

```bash
$ nice --adjustment=20 big_script.sh &
```

A corresponding `renice` command changes the priority of a running background task. As with `nice`, the priority can only be reduced. Unlike `nice`, the priority is a specific priority, not an offset.

The priority is a number immediately after the command (with no -). The optional `-p` (PID) switch indicates the parameters are process identification numbers. The `-g` switch indicates a list of process groups. The `-u` switch indicates usernames to change. Obviously, you can only `renice` programs that you own.

```bash
$ bash big_script.sh &
[1] 22516
$ renice 10 22516
22516: old priority 0, new priority 10
```

## Process Status

The `jobs` command shows basic information about a background task. For more detailed information, Linux has a `ps` (process status) command. This command has many switches, some with leading minus signs and some without. Some of these switches are for compatibility with other operating systems. A complete list is given in the chapter's reference section.

For purposes of shell scripting, the most useful switches are `-lu`, which lists all the processes running for a particular user in long format.

```bash
$ ps -lu ken
  F S   UID   PID  PPID C PRI NI ADDR SZ WCHAN TT  TIME CMD
100 S 500 1838 1837 0 62 0 - 547 wait4 pts/1 00:00:01 bash
000 R 500 2274 1838 0 72 0 - 611 - pts/1 00:00:00 ps
```

The important columns in the long format are as follows:

| Column | Description |
| :----- | :---------- |
| S      | Process state |
| UID    | User ID of the session running the program |
| PID    | The process identification number |
| PPID   | The process identification number of the program that ran the program listed |
| PRI    | The Linux priority value |
| NI     | The nice value |
| TTY    | The tty device used by the program, as returned by the tty command |
| TIME   | CPU time used by the process |
| CMD    | The name of the command |

The state of the process is a general indication as to whether it is running and, if not, why not:

- D—Uninterruptible sleep usually caused by waiting on input or output
- R—Running or waiting to run
- S—Sleeping
- T—Traced or stopped
- Z—A defunct (“zombie”) process waiting to be deleted

Be aware that `ps` has been known to change significantly between different versions of Linux. For best portability, `ps` should be used only for debugging unless the more advanced switches are avoided.

Using signals and traps allows scripts to work in tandem and alert each other to important events. Exit handlers guarantee that whenever a script exits, all necessary cleanup commands are executed. The `nice` command ensures that high-priority scripts get the most attention by Linux. The next couple of chapters examine the tools provided by Linux for scripts to work with data.
