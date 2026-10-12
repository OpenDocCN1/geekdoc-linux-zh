
Renaming the file also prevents the user from accessing his or her cron jobs. Usually, entering the `/usr/sbin/userdel -r` command is enough to remove any leftover files. It does no hurt, though, to check this directory after removing a user.

A good administrator should run a periodic check on the cron files used by regular users. This not only ensures the well-being of the system, but also verifies that the users are abiding by the terms of the fair-use agreement—a simple contract, whether written or oral, that the system will not be abused or used inappropriately. The best way to check up on what users are running is by logging cron jobs. Under Red Hat this is a fairly standard procedure. The cron log files are generally kept in the file `/var/log/cron`. Any text editor will print out the results of the past few days' or weeks' worth of cron files. These are also rotated periodically so you may have to consult renamed files such as `cron.1`, `cron.2`, and so on for older cron entries. A regular check to make sure the backups and routines are running correctly is also not a bad idea.

Administrators desiring to take a more proactive approach and be notified about the system's routines can also receive an e-mail from the cron daemon when the tasks it performs are complete. As mentioned previously, you insert a `MAILTO` value into the crontab file. Root is generally the catchall account for normal system cron jobs. But, as root, you can also insert the `MAILTO` variable into any user's crontab file and have the results mailed to yourself or someone else. Any empty `MAILTO` variable inserted into the crontab file will suppress all mail from cron. Though this suggestion may smack of despotism and not be condoned by the users themselves, I have found that some users will quickly abuse any freedom granted them on a system. As an administrator, you must be willing to play hardball when necessary.

If I wanted to have all the crontab results of the user `calvin` mailed to me, I would simply insert the following into the crontab file of `/var/spool/cron/calvin`:

```bash
MAILTO=kerry
```

Remember, to edit another user's crontab file, you must be root. To invoke the crontab file, I must enter the following:

```bash
crontab -u calvin -e
```

To suppress all mail from a particular user such as root, insert an empty `MAILTO` variable in that user's crontab file as follows:

```bash
MAILTO=
```

Red Hat, like many of the other Linux releases, runs cron jobs that rotate log files every week or so. These files can quickly become oversized and occupy more hard drive space than they are worth. The cron daemon rotates these files out by renaming them and then creating a new log file. After a certain time period, cron deletes these older logs. Log files will be kept long enough that any pertinent errors or tasks can be tracked. You can specify elsewhere just how long you want to keep certain log files. To find out more about how the system logs certain files, see Chapter 10, “Logging Errors.”

## Customizing Specific crontab Entries

Linux has other system cron entries. These cron jobs are set up by default during the installation process and are best left alone. The location of these files is the `*/etc/cron.d` directory. Much like the root cron jobs, which are user-defined, the jobs in this directory are system-defined. They deal mostly with the rotation of log files and a runtime cleanup procedure to clear out stale files or crashed programs. If programs need to be run continually or transitionally to monitor files or programs, they might be placed in this directory. However, this directory is normally reserved for programs that install their own series of cron jobs.

Another cause for caution that might be encountered under older versions of Red Hat, but less frequently with later releases, is the use of the default text editor to edit cron entries. The `crontab` command defaults to `vi` as the standard editor for changing the cron files. This text editor is not recommended for newer users, as its learning curve is rather steep. Beginning Linux users prefer a more functional and familiar editor like `joe` or `pico`, which are considered user-friendly to new beginners and can be used like most any word processor. The text editor `joe` is a throwback to the old `WordStar` days, whereas `pico` runs like the `Windows Notepad` text editor and can be considered a simple word processor. Each editor has its own set of commands for saving and editing files, but the commands are simple compared to those of `vi`. Though more difficult to grasp for neophytes, `vi` is extremely versatile and has a myriad of editing commands and can be called upon to perform most any function.

To use another text editor such as `joe` or `pico`, you must export another editor to the terminal variables. You can do so by entering the following command at the command line of the terminal at which you want to edit the crontab file:

```bash
export EDITOR=joe
```

At the end of this command, you input the name of the default editor you want—whether `joe`, `pico`, `jed`, or another editor. To make the change permanent, you will need either to edit your own `.profile` text file or to make the change global for all users by editing the `/etc/profile` file. You can accomplish this quite easily. Simply place the following lines within either of the two aforementioned files:

```bash
EDITOR=joe
export EDITOR
```

The changes will not take effect for that terminal session until after the source files have been reread. To change the variables, enter one of the following possible commands. Although the correct choice may depend upon your system's configuration, reviewing each of these choices should help give you an overview of the process. Each of the following commands will update your terminal session and will utilize the editor you selected.

```bash
source /etc/profile
source ~<username>/.profile
source /home/<username>/.bash_profile
```

Changing the default editor can mean the difference between making a successful cron entry and quickly becoming discouraged and giving up. I have seen too many beginning Linux users turn away from reaching their full potential with Linux due to frustration with a text editor.

### NOTE

> One important item to be aware of with cron files is that cron jobs will be performed only while the system is up and running. The same is true for the cron daemon: if it does not start up correctly or is shut down sometime during operation, the cron jobs scheduled for that interval will not be carried out. If the system is brought down for routine maintenance or because of an error, be mindful that those jobs will not be performed during that time period, but will pick up the next time after it is brought up.

Once you have made an entry in the crontab file, the system will immediately start consulting that particular file. The time at which a program, script, or file needs to be run depends on your scheduling. You can either have it start immediately after entering your task or schedule the execution of the task for a later date, as much as a month later.

## Setting Correct crontab Syntax

The manner in which cron jobs are implemented is important. Even though jobs are unique to each user, they still share the same syntax. The cron daemon recognizes a specific set of instructions and uses them to run the jobs as needed. The basic format is first to lay out the time in which the job needs to be performed and then give the command. It is customary also to explain the function of each cron job by placing a commented-out line at either the beginning or end of the job. Comments are lines that you don't want the program to read, but which serve as explanatory statements for other users. You usually indicate that a line is a comment by marking it with a pound sign (#). When reading the crontab file, the cron daemon will usually ignore these lines or the words following any pound sign on the same line.

The standard syntax for creating a crontab entry is as follows:

| minute | hour | day | month | weekday | command |
| :----- | :--- | :-- | :---- | :------ | :------ |
| 0–59 | 0–23 | 1–31 | 1–12 | 0–7 | /usr/local/bin/runme |

Some older UNIX systems provide an additional field that inputs the username for a particular function. Generally Red Hat doesn't provide such a field, but instead confines itself to the six-field format. The user field is sometimes found in the system's own crontab file, `/etc/crontab`.

Only certain numbers can be used for each field. Fields are separated by a single space, whereas multiple numbers in a field are grouped together with commas. As is customary with most UNIX systems, counting begins with zero. The only exception, in this instance, is in the weekday field, where both 0 and 7 equal Sunday and 1 equals Monday.

Generally, a tab separates the time fields from the command field. If the desired scheduling is for every day, then an asterisk is placed in the field instead of a number. Similar to a wildcard feature, the asterisk represents all possible numbers.

**TIP**
Be mindful of changes in time, such as daylight savings time, that might play havoc with some scheduling and can cause programs to run either twice or not at all. Red Hat Linux compensates for such changes if you specify them during the install, but it is best to double-check that your computer's time is in sync with standard time.
