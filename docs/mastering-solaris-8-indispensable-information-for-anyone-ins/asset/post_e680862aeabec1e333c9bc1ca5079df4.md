
such as the **ufsdump** command. Unless there is a command in the crontab file that redirects output, **cron** also mails you notification that it ran and indicates any errors. A very common use of the **cron** command is to launch a script every night or week that will roll over all of your log files, keeping any individual one from becoming too large.

A job can be a command or a script that contains one or more commands. The program's configuration files can be found at **/etc/cron.d**, and when it runs, it checks to see if there is a **cron.deny** file that specifies whether or not a user can run the command. A blank **cron.deny** file allows all users to run a **cron** job. The **cron** command also checks for a **cron.allow** file, and if one exists, **cron** will allow only users specified in the file to run a **cron** job. If the **cron.allow** file exists and no users are specified, only a superuser can run the **cron** job.

The **cron** command has the following two types of syntax:

```
crontab <time> <date> <pathname>/<filename>
crontab <time> <date> <options> (<username> list)
```

Use the first version of the command to specify the file that contains the **cron** commands and the second version of the command to allow a superuser to modify the file for a user using the default file location.

There are three main options that you can use with version number 2 of the **cron** utility:

-   **-e option** The -e (edit) option opens your text editor so that you can create or edit the specified user's or commands prior to their being run.
-   **-l option** The -l (list) option displays the jobs listed in the specified user's or your crontab file.
-   **-r option** The -r (remove) option deletes the crontab file that you specify.

> **WARNING** Be careful when you use the **-r** option. If you are root and you type **crontab -r** with no username, the root's crontab file will be deleted without a dialog box appearing to ask you if you are sure. Then all you can do is go to your backup to retrieve it.

The time and date are required options that tell **cron** when to execute the command file. There are five fields that precede a crontab entry in a file:

-   Minutes from 0 to 59
-   Hours from 0 to 23
-   Day of the month from 1 to 31
-   Month of the year from 1 to 12
-   Day of the week from 0 to 6, where 0 is Sunday

To specify a repeating value, use an asterisk in place of one of the five fields. For example, a file containing the `ufsdump` command that would execute every day at 3 A.M. would be entered by the root user at the console in the following way:

```
# crontab
0 3 * * * /usr/opt/dump routine
Ctrl+D
```

However, if you perform the preceding operation, your `crontab` file will be deleted and replaced by your new entry. Unless you want to do that and you are willing to lose anything you had in the `crontab` file, use the `crontab -e` command to change your `crontab` files.

When you gave the `crontab -l` command, you’ll see the entry `0 3 * * * /usr/opt/dump routine` in your file. To take a look at the standard system `crontab`, use the `crontab -l root` command. Figure 15.13 shows the default entries. Notice that `crontab` runs a check to see if the cron log file is at its limit at 3:10 A.M. every Sunday and Thursday. cron also creates a new system log at 3:10 on Sunday and adjusts any time differences it finds with the computer’s system clock at 2:01 every day (line 4).

![](img/256e02a6afce528d264a8d911fa0ff20_650_0.png)

# Memory

In order to better understand the way processes work, it is valuable to know how they use memory. By examining the consumption of memory, you can diagnose a malfunctioning system and optimize a system for performance.

As described in Chapter 5, Solaris creates a memory-based file system called the temporary file system (TMPFS) to track the physical and virtual memory in your system. Some of the TMPFS is stored on disk as virtual memory, and some of the data for the TMPFS is stored in physical memory. The TMPFS describe the combination of the two types of memory and was created to improve performance for processes that create temporary files that will be used later for additional work. Program compilations, for example, are programs that create and use tmp files. You'll find the temporary file system mounted by default by the automounter (vfstab) at the `/tmp` mount point. The contents of the TMPFS is volatile and is lost when you reboot your system.

When you store files in the tmp folder, you are essentially using up system memory. Storing large files in the tmp folder can have an impact on the amount of system memory that other programs have available to run. Additionally, when a large program or group of programs consuming a lot of RAM is resident in memory, the amount of space available in the tmp folder and that the TMPFS can use is reduced by a like amount. The TMPFS is also limited in terms of the number of files that it can hold by the amount of physical memory installed in your system, and that limitation is not altered by the size of virtual memory on disk that you create. The TMPFS is created and deleted using the swap command, but it is otherwise handled in a manner entirely analogous to using the mount command on other file systems.

## Physical Memory

Solaris 8 stores an image of the physical memory of the system in a special file called `/dev/mem` and an image of the kernel virtual memory at `/dev/kmem`. These files can be used to examine a system's memory or to patch the system for an upgrade. Entries in the mem file are byte addresses in memory interpreted as memory addresses. Byte addresses in the kmem file are references to kernel virtual memory addresses. Any nonexistant locations are stored as errors in these files.

The kmem file can access up to 4GB of kernel virtual memory. Because the mem file references real physical memory, it is the same size as the installed RAM. When RAM is greater than 4GB, Solaris uses special techniques to access the additional information on disk.

You can use the sar (system activities resources) command to monitor various system activities. What you see with the sar command depends upon the option you use. In particular, for memory, you would use this command with the -g, -k, -p, -r, and -w options. The sar options are as follows:

-   -a option Displays file access operation statistics.
-   -A option Displays overall system performance.
-   -b option Displays buffer activity statistics for caching metadata.
-   -c option Displays system call statistics.
-   -d option Displays disk activity statistics.
-   -g option Displays page-out and memory-freeing activity averages.
-   -k option Displays a report on the Kernel Memory Allocator (KMA). The KMA is a kernel subsystem used to allocate and free memory as required.
-   -m option Displays a report on interprocess communications activities.
-   -p option Reports the page-in activity for protection and translation faults.
-   -q option Determines the average queue length when the queue is occupied, as well as the percentage of time that the queue is occupied.
-   -r option Displays a report on the number of memory pages and swap file blocks that are free.
-   -u option Creates a report to display CPU utilization.
-   -v option Checks on the status of the process table, inode table, file table, and shared memory record table.
-   -w option Displays swapping and switching activity.
-   -y option Monitors terminal devices.

You can use the sadc, sa1, and sa2 commands to periodically collect the data on system activity and save it into a binary file. Each day’s results are stored as a separate file. The sadc is typically run once an hour or whenever a system boots into the multiuser mode. The syntax for the sadc command is as follows (the `<time>` variable refers to the time interval between data collection):

```
/usr/lib/sa/sadc <time> <number> <outputFile>
```

> **WARNING** Be careful when using the sar command because it logs all events over a 31+ day period. It can create data files that are quite large. Even medium-size servers can run out of space over a weekend if you are not attentive and don’t realize that, although sar reports only the specific things you asked it for, it logs all events.

## Virtual Memory

The virtual memory system extends physical memory by allowing programs and data segments to be swapped or paged to disk as needed. When a segment isn’t accessed in a while, it is overwritten with newer information. The paging algorithm is optimized to maintain on disk segments that are the most likely to be recalled by active processes.
