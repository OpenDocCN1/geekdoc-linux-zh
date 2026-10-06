
Although you need a wide screen xterm to view the output, you may find ps-A --forest you might find a helpful command in learning your system. Processes that aren't linked to others were either started by init or had their parents killed, and so they have been "adopted" by init. (Chapter 5 describes init and the boot procedure in more detail.) Most of these processes are fairly important—they're servers, login tools, and so on. Processes that hang off several others in this view, as xeyes and not in Listing 2.3, are most user processes launched from shell.

## top: A Dynamic ps Variant

If you know how much CPU time processes are consuming relative to another or if you want to quickly discover processes are consuming the most CPU time, a tool called top is for the job. (Wait, the text says "a called top", likely "a command called top") - let's re-read: "If you know how much CPU time processes are consuming relative to another or if you want to quickly discover which processes are consuming the most CPU time, a command called top is for the job. The top tool is a text-mode program, but of course it can be run in xterm or similar window, as shown in Figure 2.2; there are also GUI interfaces, like klima and gnome-system-monitor. By default, top sorts its entries by CPU time, and it updates every few seconds. This makes it a very good tool for sorting processes on an otherwise lightly loaded system—processes almost always appear in the first position or two, and they consume an inordinate amount of CPU time. Looking at Figure 2.2 you might find that Core.exe is such a process, but it is legitimately consuming a lot of CPU time. You'll need to be familiar with the purposes and normal habits of programs running on your system in order to make determinations; the needs of different programs vary so much that it's impossible to give a simple rule for judging when a process is consuming too much time.

Figure 2.2 The top command shows system information and information about the most CPU-intensive processes on a computer.

![](img/35f616c7eba4e79e12bfd762129c5d27_144_0.png)

## Managing Processes

Like Linux commands, top accepts several options. The most useful are listed here:

- -d delay This option specifies the delay between updates, which is normally five seconds,
- -p pid If you want to monitor specific processes, you can list them using this option. You'll need the PIDs, which you can discard earlier. You can specify up to 20 PIDs by using this option multiple times, once for each PID.
- -n iter You can tell top to display a certain number of updates (*iter*) and then quit. (Normally, top continues updating until you terminate the program.).
- -b This option specifies batch mode, in which top doesn't use the normal screen-update commands. You might use this to log CPU of targeted processes to a file, for instance. 

You can do more with top than what it updates by. When it's running, you can enter any of single-letter commands, some of which prompt you for additional information. These commands include the following:

- h and ? These keystrokes display help information.
- k You can kill a process with top. The top program will ask for a PID number, and if it's able to kill the process, it will do. (The upcoming section "Killing Processes" describes other ways to kill processes.
- q This option quits from top.
- r You can change a process's priority with top. You'll have to enter the PID number and a new priority value—a positive value will decrease its priority, and a negative value will increase its priority, assuming it has the default 0 priority to give. Only root may increase a process's priority. The renice* command (described shortly, in "Managing Priorities") is another way to accomplish this task.
- s This command changes the display's update rate, which you'll be asked to enter in (seconds).
- P This command sets the default to sort by CPU usage, which is the default.

You can change the display to sort by usage with top (both command-line options and interactive commands) than more are available to be summarized here; consult top's man page for more information.

One of the pieces of information provided by top is the load average, which is a measure of the demand for CPU time by updates. In Figure 2.2, you can see three load-average estimates on the top line; these correspond to the current load average and two previous measures. A system with no running CPU-intensive tasks has a load average of 0.0. High load averages reflect programs competing for available CPU time. You can also find the current load average using the uptime command, which displays the load average along with information on how long the computer has been running. The load average can be used in detecting runaway processes. For instance, if a system normally has a load average of 0.5 but suddenly gets stuck at a load average of 2.5, a CPU-hung processes may have hung—that is, unresponsive. Hung processes needlessly consume a lot of CPU time. You can use top to locate these processes and, if necessary, kill them.

## Chapter 2 • Managing Software

Most computers today include multiple CPUs or CPU cores. On such systems, the load average can equal the number of CPUs or cores before competition for CPU time begins. For instance, on a quad-core CPU, the load average can be as high as 4.0 without causing contention. Typically, one program can create a load of 1.0; however, multi-threaded programs create higher load averages, particularly on multi-core systems.

## jobs: Processes Associated With Your Session

The jobs command displays minimal information about the processes associated with the current session. In practice, jobs is of limited value, but it does have a few uses. One of these is to provide job ID numbers, but they're not the same. Jobs are numbered starting from 1 for each session, and in many cases, a shell has only a few associated jobs. The job IDs are used by a handful of utilities like PIDs, so you may need this information.

A second use of jobs is to ensure that all your programs have terminated prior to logging out. Under circumstances, logging out of a remote login session can cause the client program to freeze up if you've left programs running. A quick check with jobs will inform you of any forgotten processes and enable you to shut them down.

## Understanding Foreground and Background Processes

One of the most basic process-management tasks is to control whether a process is running in the foreground or the background—that is, whether it's monopolizing the use of the terminal from which it launched. Normally, when you launch a program, it takes over the terminal, preventing you from doing other work in that terminal. (Some programs, though, release the terminal. This is most common for servers and real GUI programs.)

If a program is running but you decide to use that terminal for something else, pressing Ctrl+Z suspends the program and gives you control of the terminal. (An important point is that this procedure suspends the program, if it's performing real work, that work stops!) This can be handy if, say, you're running a text editor in the text-mode and you use `fg` to change a filename so you can mention it in the file you're editing. Press Ctrl+Z and type `1` to get the file listing. To get back to the text editor, you then type `fg`, which restores the text editor to your terminal. If you've suspended several processes, add a job number, as in `fg 2` to restore job 2. You can obtain a list of jobs associated with a terminal by typing `jobs`, which displays the jobs and your job numbers.

A variant of `fg` is `bg`. Whereas `fg` restores a job to the foreground, `bg` restores a job to running status, in the background. You can use this command if the process you're running is a CPU-intensive task that requires no human interaction and you want to use the terminal in the meantime. Another use of bg is in a GUI environment. As an alternative to launching a program, use Ctrl+Z, and typing bg to run a program in the background, rather than edit a file with the NEEdit editor, you can **nedit myfile.txt**.
