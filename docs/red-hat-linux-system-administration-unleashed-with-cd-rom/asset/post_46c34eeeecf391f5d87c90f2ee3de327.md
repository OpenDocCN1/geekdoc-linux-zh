
Just a note about how at displays time formats. By default, the time displayed will be in the format "YYYY-MM-DD HH:MM". However, if you set the environment variable POSIXLY_CORRECT, the time will be displayed in the format "Fri Mar 11 12:25:00 1999". All of the previous examples were displayed using the default format.

## The batch Utility

The batch utility is very similar to at, but it only executes jobs when the system load is less than a specified amount. The default system load level at which batch executes commands is under 0.8, but you can specify a different value using the atrun command (covered in "The atrun Utility" section later in this chapter). You might want to specify a different number because your system is rather busy and might not reach the default system load, or your batch jobs might require considerable system resources and you do not want to load the system unless there is sufficient overhead available. The syntax for batch is as follows:

```
batch [-V] [-q queue] [-f file] [-m] [-v] [TIME]
```

- -V Prints the version number of at out to standard error.
- -q Allows you to specify which queue to use. The queue syntax that batch accepts is the same as the queue syntax for at. Take a look at the at command section for more details on queues.
- -f file Tells batch to read the job commands from the specified file instead of reading them from standard input.
- -v Displays when the job is scheduled to be executed.
- -m Tells batch to send mail to the user when the specified job has been completed.

When passing the time specification to batch, you can use all the same formats as at (refer to the discussion on at time formats earlier in this chapter). As mentioned earlier in the "at Time Specifications" section, the allowable formats are specified in the /usr/doc/at-3.1.7/timespec file.

For examples using batch, take a look at the examples for at that were listed previously, because batch takes the same options as at. All examples that work with at should also work with batch, but with batch, you do not need to specify a time. If you do specify a time, the commands will be executed whenever the system load is under the specified amount.

## The atq Utility

The atq utility is used to output the status of any pending jobs for the current user. If executed as root, all pending jobs for all users are displayed. When jobs are displayed, there are four columns of information for each job: the job number, date, hour, and job class. The syntax for atq is as follows:

```
atq [-V] [-q queue]
```

- -V Prints the version number of at out to standard error.
- -q Allows you to specify the exact queue for which to display the status of pending jobs. If -q is not passed, all jobs, regardless of queue, will be displayed.

The following is an example of calling atq:

```
$ atq -q a
4        1999-08-22 07:00 a
6        1999-08-16 17:00 a
         1999-08-16 00:00 a
```

As you can see, this command lists out all pending jobs that are in the queue.

## The atrm Utility

The atrm utility is used to delete pending jobs from the queue. Its syntax is

```
atrm [-V] job [job...]
```

- -V Prints the version number of at out to standard error.
- job You can pass any number of jobs to atrm. Every job passed will be deleted from the queue, as long as it exists.

The following is an example of using the atrm utility:

```
$ atrm 2
```

As long as job 2 exists, no output should appear, meaning that the command completed successfully. Job 2 will be dequeued after executing the command and will no longer execute as scheduled.

## The atrun Utility

The atrun utility can be used to change the default load average under which jobs submitted via batch will be executed. The atrun command is actually a shell script that invokes the at daemon (located at /usr/sbin/atd) passing the -s option. The -s option tells the at daemon to process the at/batch queue only once, running only the next job in the queue.

The atrun command is supplied only for backward compatibility because some older programs may invoke it. You should avoid using atrun and call atd directly instead. The syntax for the atrun command is as follows:

```
atrun [-l load_avg]
```

- **-l** Allows you to change to the load average at which batch commands are executed. The default load average at which batch commands are executed is 0.8.

The following is an example of using the atrun command:

```
$ atrun -l 2
```

After executing this command, the load average at which batch commands are executed at will be 2, not 0.8. This might be needed on busy systems that never reach the 0.8 load.

## The at Daemon

The actual program that controls the behavior of at is known as the at daemon. The at daemon is located at /usr/sbin/atd. The actual purpose of atd is to run the jobs that have been queued by at. This is done in the background without user intervention. However, you can directly execute atd to change various parameters of atd's behavior. The following is the syntax for the at daemon:

```
atd [-l load_avg] [-b batch_interval] [-d] [-s]
```

As you can see, there are several parameters that you can pass to atd; the following is a description of each one:

- **-l** Allows you to specify the maximum load factor at which jobs queued by the batch command can be run. As mentioned earlier, the default option for this is 0.8. The current load of the system is determined by the /proc/loadavg file, and so a working /proc filesystem is necessary to make use of this feature.
- **-b** Allows you to specify the minimum time interval (in seconds) between which two batch jobs can be started. The default time interval is 60 seconds.
- **-d** Turns on the verbose debugging feature that outputs all error messages to standard error as opposed to logging all errors using syslog.
- **-s** Tells the at daemon to process the job queue one time. This feature is generally only used by the atrun script and is not particularly useful. Like atrun, the -s parameter is primarily provided only for backward compatibility.

When jobs are queued by either at or batch, they are stored in the /var/spool/at directory. This directory should be mode 700 and owned by the daemon user. To view the contents of the directory, you must log in as root, or you will be denied. Within the /var/spool/at directory is a subdirectory spool where all output is stored. This directory is useful when examining the results of at jobs and is also of mode 700 and owned by the daemon user.

When invoking either at or batch, you must pass the commands that are to be executed on standard input or specify a file that contains the commands. To specify a file, pass the -f option to either at or batch. When passing the commands to at or batch on standard input, you can end your input with the EOF character (Ctrl+D).

When at or batch is invoked, it has access to all the current environment variables except for TERM, DISPLAY, and _. It also retains the current working directory and the umask of the user invoking at. If a user invokes at or batch from an su shell, the real userid of the user is kept.

When atd executes any commands in the at queue, any results sent to either standard error or standard output are mailed to the user who originally queued the commands. The command used to send the mail is the standard /usr/sbin/sendmail. If you choose to install an MTA other than the Red Hat default of sendmail, be sure to keep /usr/sbin/sendmail as a symbolic link to your new MTA, or you will break that mail feature of atd. If a user invokes at or batch while in an su shell, because the actual userid of that user is retained, when the commands are executed, mail will be sent to the actual user, not root.

## Specifying Which Users Can Use at

You can have complete control over which users on your system can use the at utility. System security is the primary reason to limit access to at. Allowing users to start jobs when they are not logged in can be a potential security hole, however this is a matter best left to the system administrator. There are two files located in the /etc directory that allow you to limit which users are allowed to use the at utility. The /etc/at.deny file allows you to specify users that are not allowed to use the at utility. Usernames are listed one per line.

The /etc/at.allow file allows you to specify exactly which users are allowed to use at. Again, usernames are listed one per line. If /etc/at.allow does not exist but /etc/at.deny does exist, all users are allowed to use at, except the users listed in /etc/at.deny. If /etc/at.allow does exist but the /etc/at.deny file does not exist, only the users listed in /etc/at.allow are allowed to use at. If neither file exists, only the superuser account can be used to invoke at.

The default Red Hat 6.0 configuration for at comes with a blank /etc/at.deny, so all users can use at and batch out-of-the-box.
