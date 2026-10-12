
## Cron System Directories

Inside each of those four directories (cron.hourly, cron.daily, cron.weekly, and cron.monthly) is a collection of shell scripts that are run by run-parts. For example, in cron.daily are scripts such as rpm, which saves a list of your packages in /var/log/rpmpkgs every day; logrotate, which handles backing up of log files; and makedatbase, which updates the whatis database. You can add other system tasks to these directories if you want to, but you should be careful to ensure your scripts are correct.

### CAUTION

The cron daemon reads all the system crontab files and all user crontab files once a minute (on the minute; that is, at 6:00:00, 6:01:00, and so on) to check for changes. However, any new jobs it finds are not executed until at least one minute has passed.

For example, if it is 6:01:49 (that is, 49 seconds past one minute past 6 a.m.) and you set a cron job to run at 6:02, it will not execute. At 6:02, the cron daemon rereads its configuration files and sees the new job, but is not able to execute it. If you set the job to run at 6:02 a.m. every day, it will be executed the following morning and every subsequent morning.

This same situation exists when deleting jobs. If it is 6:01:49 and you have a job scheduled to run at 6:02, deleting the job makes no difference: cron runs it before it rereads the crontab files for changes. However, after it has reread the crontab file and noticed the job is no longer there, it is not executed on subsequent days.

There are alternative ways of specifying dates. For example, you can use sets of dates and times by using hyphens or commas, such as hours 9-15 would execute at 9, 10, 11, 12, 13, 14, and 15 (from 9 a.m. to 3 p.m.), whereas 9,11,13,15 would miss out at the even hours. Note that it is important that you do not pass spaces into these sets because the cron daemon would interpret them as the next field. You can define a step value with a slash (/) to show division: \*/4 for hours means “every four hours all day,” and 0-12/3 means “every three hours from midnight to noon.” You can also specify day and month names rather than numbers, using three-character abbreviations: Sun, Mon, Tue, Fri, Sat for days, or Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec for months.

As well as system jobs, there are also user jobs for those users who have the correct permissions. User jobs are stored in the /var/spool/cron directory, with each user having his own file named after his username-for instance, /var/spool/cron/paul or /var/spool/cron/root. The contents of these files contain the jobs the user wants to run and take roughly the same format as the /etc/crontab file, with the exception that the owner of the job should not be specified because it is always the same as the filename.

To edit your own crontab file, type crontab -e. This brings up a text editor (vi by default, but you can set the EDITOR environment variable to change that) in which you can enter your entries. The format of this file is a little different from the format for the main crontab because this time there is no need to specify the owner of the job—it is always you.

So, this time each line is made up of six fields: minute (0-59), hour (0-23), day of the month (1-31), month of the year (1-12), day of the week (0-7), and then the command to run. If you are using vim and are new to it, press i to enter insert mode to edit your text; then press Esc to exit insert mode. To save and quit, type a colon followed by **wq** and press Enter.

When programming we tend to use a sandbox subdirectory in our home directory where we keep all sorts of temporary files that we were just playing around with. We can use a personal job to empty that directory every morning at 6 a.m. so that we get a fresh start each morning. Here is how that would look in our crontab file:

```
0 6 * * * rm -rf /home/paul/sandbox/*
```

If you are not allowed to schedule jobs, you will be stopped from editing your crontab file.

When your jobs are placed, you can use the command crontab -l to list your jobs. This just prints the contents of your crontab file, so its output is the same as the line you just entered.

If you want to remove just one job, the easiest thing to do is type crontab -e to edit your crontab file in vim; then, after having moved the cursor to the job you want to delete, type dd (two ds) to delete that line. If you want to delete all your jobs, you can use crontab -r to delete your crontab file.

## Basic Shell Control

Fedora includes a rich assortment of capable, flexible, and powerful shells. Each shell is different but has numerous built-in commands and configurable command-line prompts and might include features such as command-line history, the capability to recall and use a previous command line, and command-line editing. As an example, the bash shell is so powerful that it is possible to write a minimal web server entirely in bash's language using 114 lines of script (see the link at the end of this chapter).

Although there are many shells to choose from, most people stick with the default, bash. This is because bash does everything most people need to do, and more. Change your shell only if you really need to.

Table 15.1 lists each shell, along with its description and location, in your Fedora file system.

### TABLE 15.1 Shells with Fedora

| Name | Description | Location |
| :--- | :--- | :--- |
| ash | A small shell (sh-like) | /bin/ash |
| ash.static | A version of ash not dependent on software libraries | /bin/ash.static |
| bash | The Bourne Again Shell | /bin/bash |
| bsh | A symbolic link to ash | /bin/bsh |
| csh | The C shell, a symbolic link to tcsh | /bin/csh |
| ksh | The Korn shell | /bin/ksh, /usr/bin/ksh |
| pdksh | A symbolic link to ksh | /usr/bin/pdksh |
| rsh | The restricted shell (for network operation) | /usr/bin/rsh |
| sash | A standalone shell | /sbin/sash |
| sh | A symbolic link to bash | /bin/sh |
| tcsh | A csh-compatible shell | /bin/tcsh |
| zsh | A compatible csh, ksh, and sh shell | /bin/zsh |

### LEARNING MORE ABOUT YOUR SHELL

All the shells listed in Table 15.1 have accompanying man pages, along with other documentation under the `/usr/share/doc` directory. Some of the documentation can be quite lengthy, but it is generally much better to have too much documentation than too little! The bash shell includes more than 100 pages in its manual, and the zsh shell documentation is so extensive that it includes the zshall meta man page (use man zshall to read this overview!).

## The Shell Command Line

Having a basic understanding of the capabilities of the shell command line can help you write better shell scripts. If, after you finished reading this short introduction, you want to learn more about the command line, check out Chapter 36, "Command Line Masterclass." You can use the shell command line to perform a number of different tasks, including:

- Searching files or directories with programs using pattern matching, or *expressions*; commands include the GNU *gawk* (linked as *awk*) and the *grep* family of commands, including *egrep* and *fgrep*
- Getting data from and sending data to a file or command, known as *input and output redirection*
- Feeding or filtering a program's output to another command (called using *pipes*)

A shell can also have built-in *job-control* commands to launch the command line as a background process, suspend a running program, selectively retrieve or kill running or suspended programs, and perform other types of process control.

Multiple commands can be run on a single command line using a semicolon to separate commands:

```
$ w ; free ; df
6:02pm  up 4 days, 24 min, 1 user,  load average: 0.00, 0.00, 0.00
USER TTY FROM LOGIN IDLE JCPU PCPU WHAT
bball pts/0 shuttle.home.org 1:14pm 0.00s 0.57s 0.01s w
total used free shared buffers cached
Mem: 190684 184420 6264 76 17620 142820
```
