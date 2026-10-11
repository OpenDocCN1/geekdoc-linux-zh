
You can also observe whether there are signals being returned to the process (and what signals they might be) and whether there were any faults associated with the process. For example, you can use the `truss ping` command or the Oracle database equivalent `truss tnsping` (ping against an Oracle database) to determine how a network responds.

Here’s something else that is very useful. If you want to capture the entire session (that is, if the program you are running `truss` on is interactive and you want to capture your input as well as the output from `truss`), you can use the `script` command. You first run `script <filename>`, replacing `<filename>` with what you want the log of the session to be called, then run the `truss` command. After you have completed the interactive session with `truss` and the program you are testing, press the `Ctrl+D` key-stroke and the `script` will exit. You now have a file with a full log of your interaction.

## The Process Manager

Solaris provides a graphical utility called the Process Manager, which not only is visually more appealing than the `ps` command, it offers an interactive real-time display of processes executing on a system. To open the Process Manager, double-click the Process Manager icon (shown in the following graphic) in the Desktop_Apps window of the Application Manager. The Application Manager is accessible from the Applications control on the Applications subpanel of the front panel of the CDE.

![](img/256e02a6afce528d264a8d911fa0ff20_633_0.png)

In the Process Manager window shown in Figure 15.6, you see a list of processes with the following information included (from left to right):

- PID
- Name of the process
- Owner of the process; that is, the person who executed the process
- CPU%, which measures the percentage of microprocessor cycles that the process is consuming
- RAM, amount of memory that the process occupies
- Swap, how much virtual memory is consumed by the process
- Started, when the process was initiated
- Parent, the PID of the process that spawned or created the process
- Command, the `<pathname>/<filename>` of the program that created the process

**FIGURE 15.6**  
The Process Manager

![](img/256e02a6afce528d264a8d911fa0ff20_634_0.png)

Although the `top` command is a more powerful tool, the Process Manager is easier to work with and learn. There are a number of useful functions in the Process Manager for debugging and tracing processes as well as for identifying the owner. The Kill command (`Ctrl+C`) that allows you to terminate an errant process is found on the Process menu, which is shown in the following graphic.

![](img/256e02a6afce528d264a8d911fa0ff20_634_1.png)

When you're using the Process Manager to troubleshoot a system, the telltale sign of a runaway process is the existence of several identical jobs all owned by the same user. An example would be an errant script that initiates processes without checking to see if the previous processes complete themselves first. Also, if a process is using a considerable percentage of CPU time, that might indicate that the process is in an endless loop. Other telltale signs are processes that execute with high *nice* numbers (see the next section) or processes that are using more and more CPU time as they execute.

## Process Priorities

Solaris and Unix provide commands you can use to alter the scheduling priority under which a process runs. To view the default scheduling policies of the process scheduler, use the `disadmin` command.

> **WARNING** If you are going to change process priorities, be aware that you could cause your system to crash if you make a mistake. Take extra caution when adjusting priorities, and if possible, try your changes on a non-production system.

The `nice` command allows you to change a scheduling priority, whereas the `priocntl` command provides a general interface to the Unix scheduler. The `nice` command runs as a shell command, and not every process supports it. You can control what shell is used to execute the `nice` command; otherwise, it uses your default shell during execution. The `nice` command sets a priority (the so-called *nice* number) from 0 to 39 (or a range of 40), where 0 is the best and 39 is the worst. Processes inherit their *nice* number from their parent, and the `ps -el` lists the number in the NI column. Mostly, `nice` is supported for backward compatibility, and you should spend your time mastering the `priocntl` (priority control) command.

Processes are assigned a user execution level of from 1 to 19, and it is assumed that 10 is the default increment. A higher priority than 19 is run as 19. If a superuser enters a negative increment, the commands issued by the superuser with a negative increment are run with a higher priority than normal. Priority 1 is the highest level, 19 the lowest. The `nice` command's syntax allows you to specify the command as well as an argument used by that command.

You can adjust the *nice* number to a lower priority by raising it (either with a `nice -n <positive_name>` or `nice <negative_name>`) from 1 to 19 points, where 19 points (either `nice -n 19` or `nice -19`) will result in the maximum *nice* number of 39. You can raise the priority by lowering the *nice* number (using `nice -n <negative_name>`) to a *nice* total of 0 by using the smallest number, -20 (that is, `nice -n -20`). The default *nice* level is 20 (or `nice -n 0` from the command line). For the programmer, this scheme is different, because they can use the `nice()` function to set the nice level directly to 0 through 39.

> **TIP** If you have a large compile you need to run but still need to use the system as your desktop, you may run the compile at a higher nice level so that your other applications will have more time at the CPU.

> **WARNING** Inappropriate use of the *nice* command, and in particular the *priocntl* command, can cause your system to respond sluggishly and malfunction and possibly cause you to have to reboot your system should you alter the priority of an essential system function. Changing process priorities isn’t something end users typically do, and it’s rarely done in system administration.

The *priocntl* (priority control) command allows you to display (as you have seen previously with the `-l` option) or set the scheduling parameters of specific processes. The priority range for both time-sharing and interactive processes can range from -60 to +60; real-time processes have a maximum configured priority of 59. System functions like the scheduler and the paging mechanism (*pagedaemon*) are assigned higher priorities, typically in the high 90s so that they execute with strong preference. You can use the `ps -ec1` command to display the global priority of a process. That priority is shown in the seventh (PRI) column. Figure 15.7 shows the output of the `ps -ec1` command.

Using the *priocntl* command, you can alter the performance of the scheduler, allowing you access to the real-time, time-sharing, and interactive classes of processes. The *priocntl* man pages go into great detail about the options of this command.

To use the `priocntl` command to designate a process priority, do the following:

1. Switch to a superuser with the `su` command.
2. Start a process with a designated priority using the following command:

```
# priocntl -e -c <class> -m <userlimit> -p <pri> <commandname>
```

`-e` executes the command; `-c <class>` specifies the class, which is typically TS for time-sharing or RT for real time; `-m <userlimit>` is the maximum amount that you change your priority when `-p` is used; and `-p <pri> <commandname>` is the relative priority for the RT thread. When you use `-p`, you can change a user-designated priority by -20 to +20.

**FIGURE 15.7**  
The output of the `ps -ec1` command

![](img/256e02a6afce528d264a8d911fa0ff20_637_0.png)

3. Use `ps -ec1 | grep <commandname>` to make sure the process priority was actually changed.

You can also use the *priocntl* command to alter the scheduling parameters of a time-share process. The procedure is identical to the preceding one; the command syntax is as follows:

```
# priocntl -s -m <userlimit> -p <userpriority> -i <idtype> <idlist>
```

Here the options take on the following meanings: `-s` sets the upper limit on the user priority range and changes the priority; `-m <userlimit>` sets the maximum amount that you change your priority when `-p` is used; `-p <userpriority>` assigns a priority; and finally, `-i <idtype> <idlist>` uses these two parameters to identify a particular process. The `<idtype>` is the PID or UID. You can also change the class of a process using *priocntl*.
