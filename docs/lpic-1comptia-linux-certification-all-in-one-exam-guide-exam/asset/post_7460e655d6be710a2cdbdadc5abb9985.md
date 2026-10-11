
called the parent. The new process that was created by the first process is called the child. Every Linux process has a parent process. All Linux processes can trace their heredity back to the init process, which is the first process loaded by the kernel on system boot.

Every Linux process is assigned a process ID (PID) that uniquely identifies the process on the system. Processes are also assigned a PPID, which is the PID of the process’s parent process. Whenever you run a command from the shell prompt, a new shell (called a subshell) is created and the command is run within it. When the process is complete, the subshell is destroyed and control is returned to the original shell.

We then turned our attention to managing Linux processes. We first discussed how you go about creating processes. User processes are created by simply entering commands at the shell prompt. System processes are created by running a daemon startup script from your system’s init directory. Some distributions use System V init scripts, which are stored in /etc/rc.d/init.d. Other distributions use BSD init scripts, which are stored in /etc/init.d.

We next discussed how to view running processes. The first utility we looked at was the top utility. You load top by entering top at the shell prompt. You can press the H key while top is running to view a help screen that will show you how to sort by a specific column or even add columns of data to the display.

You can also use the ps command to view running processes. By default, the ps command only displays running processes associated with the current shell session. To view all running processes, use the -e option with the ps command. You can also use the -f and -l options with ps to view extended process information.

Next, we discussed how to prioritize processes on your system. A process’s overall priority is heavily influenced by its nice value. Nice values can range from -20 to +19. The lower the nice value, the higher the priority of the process. To adjust the nice value of a process when it’s loaded, you can use the nice command. The syntax is `nice -n nice_value command`. You can’t use a nice value lower than 0 unless you are logged in as root. You can also adjust the nice value of a running process without unloading it. This is done using the renice command. The syntax is `renice nice_value PID`.

Then we discussed how to run processes in the foreground and the background. By default, processes you launch from the shell prompt run in the foreground. In this situation, the shell prompt is locked until the process is complete. You can also run a process in the background. In this situation, the program runs, but it does so in the background and control is returned to the shell prompt, allowing you to run additional commands. This is done by simply appending a & character to the end of the command. When you do, the background process is assigned a job ID number.

You can move a process that is running in the background to the foreground by entering `fg job_ID` at the shell prompt. You can also move a foreground process into the background. To do this, first press CTRL-Z to stop the process. The process will then be assigned a job ID number. You can then enter `bg job_ID` to move the process to the background.

Finally, we discussed how to kill a running process from the shell prompt. You can use the kill command or the killall command to do this. Both of these commands use a variety of kill signals. Some of the most useful signals include:

- SIGHUP (1)
- SIGINT (2)
- SIGKILL (9)
- SIGTERM (15)

The syntax for kill is `kill –signal PID`. The syntax for killall is `killall –signal process_name`. When working with a hung process, you should try less aggressive kill signals, such as SIGINT and SIGTERM, before using more aggressive kill signals such as SIGKILL. I also pointed out that you can run a process using the nohup command to cause it to ignore the SIGHUP signal that is sent when a user logs out. This allows the process to continue running even though the user is no longer logged into the system.

At this point in the chapter, we shifted gears and discussed how to schedule processes to run automatically in the future. If you only need the process to run once in the future, you can use the at daemon. Before you can use at, you need to make sure the at daemon is running on your system. Then, you can enter `at time` at the shell prompt. The time value can be a fixed time, such as 10:00, or a relative time, such as tomorrow. You will then be presented with an at> prompt where you can enter a list of commands to run. Press CTRL-D when you’re done. You can use the atq command to view a list of pending at jobs. You can also use the atrm command to remove a pending at job.

If you need to schedule a process to run on a recurring basis, then you need to use the cron daemon instead of at. The cron daemon can run system jobs or user jobs. System cron jobs are created by creating script files in one of the following directories:

- /etc/cron.hourly
- /etc/cron.daily
- /etc/cron.weekly
- /etc/cron.monthly

You can also create a crontab file and save it in the /etc/cron.d directory. A crontab file contains one line for each command that is to be run. Each line contains six fields:

- 1 Minutes
- 2 Hour
- 3 Day
- 4 Month
- 5 Day of the week
- 6 Command to be run

In addition to system jobs, you can also use cron to create user jobs. User cron jobs are stored in /var/spool/cron/tabs. A user can create a crontab file by entering `crontab –e` at the shell prompt. The user then creates one line for each scheduled command using the syntax just described. After creating the crontab file, you can use the `crontab –l` command to view your crontab file. You can also use the `crontab –r` command to remove your crontab file.

## Accelerated Review

- Whenever you run a command from the shell prompt, a process is created on the system.
- When a process loads, the program's code is loaded into RAM and is executed by the CPU.
- Linux is a multitasking operating system.
- Most CPUs can only run one process at a time.
- Linux continually switches CPU time among the many processes loaded into RAM, making it appear that the CPU is processing many processes concurrently.
- When the init process loads a daemon from an init script, a system process is created.
- When an end user enters a command at the shell prompt, a user process is created.
- User processes are associated with a shell session; system processes are not.
- Linux processes can spawn other Linux processes.
- The process that spawned another process is called the parent.
- The new process that was created by the first process is called the child.
- Every Linux process has a parent process.
- All Linux processes can trace their heredity back to the init process, which is the first process loaded by the kernel on system boot.
- Every Linux process is assigned a process ID (PID) that uniquely identifies the process on the system.
- Processes are assigned a PPID value, which is the PID of the process's parent process.
- Whenever you run a command from the shell prompt, a subshell is created and the command is run within it.
- When the process is complete, the subshell is destroyed and control is returned to the original shell.
- User processes are created when you enter commands at the shell prompt.
- System processes are created when you run a daemon startup script from your system's init directory.
- Some distributions use System V init scripts, which are stored in /etc/rc.d/init.d.
- Some distributions use BSD init scripts, which are stored in /etc/init.d.
- You can use the top utility to view system processes. You load top by entering top at the shell prompt.
- You can press the H key while top is running to view a help screen that will show you how to configure the data displayed by top.
- You can use the ps command to view running processes.
- By default, the ps command only displays running processes associated with the current shell session.
- You can use the -e option with the ps command to view all running processes.
- You can use the -f and -l options with ps to view extended process information.
- Linux allows you to prioritize processes running on your system.
- A process’s overall priority is heavily influenced by its nice value.
- Nice values can range from -20 to +19.
- The lower the nice value, the higher the priority of the process.
- You can use the nice command to adjust the nice value of a process as it’s loaded.
- To use nice, you enter `nice -n nice_value command`.
- You can’t assign a nice value lower than 0 unless you are logged in as root.
- You can also adjust the nice value of a running process without unloading it using the renice command.
- The syntax for using renice is `renice nice_value PID`.
- By default, processes you launch from the shell prompt run in the foreground.
- Foreground processes lock the shell prompt until the process is complete.
- You can run Linux processes in the background.
- Background processes return control to the shell prompt.
- You can run a process in the background by appending an & character to the end of the command.
- When you load a process into the background, the process is assigned a job ID number.
- You can move a process that is running in the background to the foreground by entering `fg job_ID` at the shell prompt.
- You can move a foreground process into the background by pressing CTRL-Z to stop the process and then entering `bg job_ID` to move the process to the background.
- You can use the kill or the killall commands to kill a running process.
- There are many kill signals that can be sent using kill or killall; some of the most useful include:
  - SIGHUP (1)
  - SIGINT (2)
  - SIGKILL (9)
  - SIGTERM (15)
- To kill a process with kill, enter `kill -signal PID` at the shell prompt.
