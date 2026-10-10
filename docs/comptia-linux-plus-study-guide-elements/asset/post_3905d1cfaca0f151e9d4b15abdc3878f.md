
## Table 3.2 Common top Options (continued)

| Option Name | Meaning |
| :--- | :--- |
| -n *iter* | You can tell top to display a certain number of updates (*iter*) and then quit. (Normally, top continues updating until you terminate the program.) |
| -b | This option specifies batch mode, in which top doesn't use the normal screen update commands. You might use this to log CPU use of targeted programs to a file, for instance. |

You can do more with top than watch it update its display. When it's running, you can enter any of several single-letter commands, some of which prompt you for additional information. Table 3.3 summarizes these commands.

## Table 3.3 Common top Interactive Commands

| Option Name | Meaning |
| :--- | :--- |
| h or ? | These keystrokes display help information. |
| k | You can kill (terminate) a process with this command. The top program will ask for a PID number and signal number, and if it's able to kill it, it will do so. (The upcoming section "Killing Processes" describes other ways to kill processes.) |
| q | This option quits from top. |
| r | You can change a process's priority with this command. You'll have to enter the PID number and a new priority value—a positive value will decrease its priority, and a negative value will increase its priority, assuming it has the default 0 priority to begin with. Only root may increase a process's priority. The renice command (described shortly, in "Restricting Processes' CPU Use") is another way to accomplish this task. |
| s | This command changes the display's update rate, which you'll be asked to enter (in seconds). |
| p | This sets the display to sort by CPU usage, which is the default. |
| M | You can change the display to sort by memory usage with this command. |

More commands are available in top (both command-line options and interactive commands) than can be summarized here; consult the top man page for more information.

One of the pieces of information provided by top is the load average, which is a measure of the demand for CPU time by applications. In Figure 3.2, you’ll see three load-average estimates on the top line; these correspond to the load average in the previous one minute, five minutes, and 15 minutes. A system on which no programs are demanding CPU time will have a load average of 0. A system with one program running CPU-intensive tasks will have a load average of 1.0. Higher load averages reflect programs competing for available CPU time. You can also find the current load average via the uptime command, which displays the load average along with information on how long the computer has been running. The load average can be useful in detecting runaway processes. For instance, if a system normally has a load average of 0.5 but it suddenly gets stuck at a load average of 2.5, there may be a couple of CPU-hogging processes that have hung—that is, become unresponsive. Hung processes sometimes needlessly consume a lot of CPU time. You can use top to locate these processes and, if necessary, kill them.

You might think that a load average of 1.0 or below is optimal, since a higher load average means that the computer must divide its attention between competing processes. This is sometimes true, but sometimes it’s not. Modern computers often have two or more CPUs (or CPU cores), which means that the system can divide its CPU time between as many processes as it has cores with almost no slowdown. For instance, on a dual-core system, a load average of up to 2.0 will produce almost no speed reduction. Furthermore, modern CPUs are fast enough that the slowdown caused by the division of a CPU’s time between processes may be unimportant. Using nice (described in the next section) can interact with this factor. This effect is hard to quantify, though. Sometimes processes competing for CPU time will cause noticeable slowdown, as in the slow completion of a lengthy multimedia encoding job. Other times the slowdown will cause a barely noticeable effect, as in a fraction-of-a-second difference in the time required to display a program’s menu bar. Some Linux systems are intended to be run with greater-than-1.0 load averages, but with CPUs that are fast enough that the slowdown caused by these high load averages will be unimportant. This might be true of a multiuser server, for instance.

# Restricting Processes’ CPU Use

There may be times when you’ll want to prioritize your programs’ CPU use. For instance, you might be running a program that’s very CPU-intensive but that will take a long time to finish its work, and you don’t want that program to interfere with others that are of a more interactive nature. Alternatively, on a heavily loaded computer, you might have a job that’s more important than others that are running, so you might want to give it a priority boost. In either case, the usual method of accomplishing this goal is through the nice and renice commands. You can use nice to launch a program with a specified priority or use renice to alter the priority of a running program.

You can assign a priority to nice in any of three ways: by specifying the priority preceded by a dash (this works well for positive priorities but makes them look like negative priorities), by specifying the priority after a -n parameter, or by specifying the priority after an --adjustment= parameter. In all cases, these parameters are followed by the name of the program you want to run:

```
nice [argument] [command [command-arguments]]
```

For instance, the following three commands are all equivalent:

```
$ nice -12 number-crunch data.txt
$ nice -n 12 number-crunch data.txt
$ nice --adjustment=12 number-crunch data.txt
```

All three of these commands run the number-crunch program at priority 12 and pass it the data.txt file. If you omit the adjustment value, nice uses 10 as a default. The range of possible values is –20 to 19, with negative values having the highest priority. Only root may launch a program with increased priority (that is, give a negative priority value), but any user may use nice to launch a program with low priority. The default priority for a program run without nice is 0.

If you've found that a running process is consuming too much CPU time or is being swamped by other programs and so should be given more CPU time, you can use the renice program to alter its priority without disrupting the program's operation. The syntax for renice is as follows:

```
renice priority [(-p) pids] [(-g) pgpids] [(-u) users]
```

You must specify the priority, which takes the same values as with nice. In addition, you must specify one or more PIDs (pids), one or more group IDs (pgpids), or one or more usernames (users). In the latter two cases, renice changes the priority of all programs that match the specified criterion—but only root may use renice in this way. Also, only root may increase a process's priority. If you give a numeric value without a -p, -g, or -u option, renice assumes the value is a PID. You may mix and match these methods of specification. For instance, you might enter the following command:

```
# renice 7 16580 -u pdavison tbaker
```

This command sets the priority to 7 for PID 16580 and for all processes owned by pdavison and tbaker.

# Killing Processes

Sometimes reducing a process's priority isn't a strong enough action. A program may have become totally unresponsive, or you might want to terminate a process that shouldn't be running at all. In these cases, the kill command is the tool to use. This program sends a signal (a method that Linux uses to communicate with processes) to a process. The signal is usually sent by the kernel, the user, or the program itself to terminate the process. Linux supports many numbered signals, each of which is associated with a specific name. You can see them all by typing kill -l. If you don't use -l, the syntax for kill is as follows:

```
kill -s signal pid
```

Although Linux includes a `kill` program, many shells, including Bash and csh, include built-in `kill` equivalents that work in much the same way as the external program. If you want to be sure you're using the external program, type its complete path, as in `/bin/kill`.

The `-s signal` parameter sends the specified signal to the process. You can specify the signal using either a number (such as 9) or a name (such as SIGKILL). The signals you're most likely to use are 1 (SIGHUP, which causes many server programs to reread their configuration files), 9 (SIGKILL, which causes the process to exit without performing routine shutdown tasks), and 15 (SIGTERM, which causes the process to exit but allow it to close open files and so on). If you don't specify a signal, the default is 15 (SIGTERM). You can also use the shortened form `-signal`. If you do this and use a signal name, you should omit the SIG portion of the name—for instance, use KILL rather than SIGKILL. The `pid` option is, of course, the PID for the process you want to kill. You can obtain this number from `ps` or `top`.

The `kill` program will kill only those processes owned by the user who runs `kill`. The exception is if that user is `root`; the superuser may kill any user's processes.

A variant on `kill` is `killall`, which has the following form:

```
killall [options] [--] name [...]
```

This command kills a process based on its name rather than its PID number. For instance, `killall vi` kills all the running processes called `vi`. You may specify a signal in the shortened form (`-signal`) or by prepending the signal name with `-s` or `--signal`. As with `kill`, the default is 15 (SIGTERM). One potentially important option to `killall` is `-i`, which causes it to ask for confirmation before sending the signal to each process. You might use it like this:

```
$ killall -i vi
Kill vi(13211) ? (y/n) y
Kill vi(13217) ? (y/n) n
```

In this example, two instances of the `Vi` editor were running, but only one should have been killed. As a general rule, if you run `killall` as `root`, you should use the `-i` parameter; if you don't, it's all too likely that you'll kill processes that you should not, particularly if the computer is being used by many people at once.

Some versions of Unix provide a `killall` command that works differently from Linux's `killall`. This alternate `killall` kills all the processes started by the user who runs the command. This is a potentially much more destructive command, so if you ever find yourself on a non-Linux system, *do not use `killall`* until you've discovered what that system's `killall` does, say by reading the `killall` man page.
