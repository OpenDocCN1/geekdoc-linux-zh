
/var/spool/cron and /etc/cron.d directories and the /etc/crontab file, and executes commands specified by these configuration files if the time matches the time listed in the files.

There are two types of cron jobs: system cron jobs and user cron jobs. System cron jobs are run as root and perform system-wide maintenance tasks. By default, most Linux distributions include system cron jobs that clean out old files from /tmp, perform log rotation (as described earlier, in “Rotating Log Files”), and so on. You can add to this repertoire, as described shortly. Ordinary users can create user cron jobs, which might run some user program on a regular basis. You can also create a user cron job as root, which might be handy if you need to perform some task at a time not supported by the system cron jobs, which are scheduled rather rigidly.

One of the critical points to remember about cron jobs is that they run unsupervised. Therefore, you shouldn't call any program in a cron job if that program requires user input. For instance, you wouldn't run a text editor in a cron job; but you might run a script that automatically manipulates text files, such as log files.

## Creating System cron Jobs

The /etc/crontab file controls system cron jobs. This file normally begins with several lines that set environment variables, such as SPATH and SMAILTO (the former sets the path, and the latter is the address to which programs' output is mailed). The file then contains several lines that resemble the following:

```
02 4 * * * root run-parts /etc/cron.daily
```

This line begins with five fields that specify the time. The fields are, in order, the minute (0–59), the hour (0–23), the day of the month (1–31), the month (1–12), and the day of the week (0–7; both 0 and 7 correspond to Sunday). For the month and day of the week values, you can use the first three letters of the name rather than a number, if you like.

In all cases, you can specify multiple values in several ways:

- 1. An asterisk (*) matches all possible values.
- 2. A list separated by commas (such as 0,6,12,18) matches any of the specified values.
- 3. Two values separated by a dash (–) indicate a range, inclusive of the end points. For instance, 9–17 in the hour field specifies a time of from 9:00 a.m. to 5:00 p.m.
- 4. A slash, when used in conjunction with some other multi-value option, specifies stepped values—a range in which some members are skipped. For instance, */10 in the minute field indicates a job that's run every 10 minutes.

After the first five fields, /etc/crontab entries continue with the account name to be used when executing the program (root in the preceding example) and the command to be run (run-parts /etc/cron.daily in this example). The default /etc/crontab entries generally use run-parts, cronloop, or a similar utility that runs any executable scripts within a directory. Thus, the preceding example runs all the scripts in /etc/cron.daily at 4:02 a.m. every day. Most distributions include monthly, daily, weekly, and hourly system cron jobs, each corresponding to scripts in a directory called /etc/cron.interval, where interval is a word associated with the run frequency. Others place these scripts in /etc/cron.d/interval directories.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_427_0.png)

> The exact times chosen for system cron jobs to execute vary from one distribution to another. Normally, though, daily and longer-interval cron jobs run early in the morning—between midnight and 6:00 a.m. Check your /etc/crontab file to determine when your system cron jobs run.

To create a new system cron job, you may create a script to perform the task you want performed (as described in Chapter 9, “Writing Scripts, Configuring E-Mail, and Using Databases”) and copy that script to the appropriate /etc/cron.interval directory. When the runtime next rolls around, cron will run the script.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_427_1.png)

> Before submitting a script as a cron job, test it thoroughly. This is particularly important if the cron job will run when you’re not around. You don’t want a bug in your cron job script to cause problems by filling the hard disk with useless files or producing thousands of e-mail messages when you’re not present to quickly correct the problem.

If you need to run a cron job at a time or interval that’s not supported by the standard /etc/crontab, you can either modify that file to change or add the cron job runtime or create a user cron job, as described shortly. If you choose to modify the system cron job facility, model your changes after an existing entry, changing the times and script storage directory as required.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_427_2.png)

> System cron job storage directories should be owned by root, and only root should be able to write to them. If ordinary users can write to a system cron job directory, unscrupulous users can write scripts to give themselves superuser privileges and place them in the system cron directory. The next time cron runs those scripts, the users will have full administrative access to the system.

## Creating User cron Jobs

To create a user cron job, you use the crontab utility, not to be confused with the /etc/crontab configuration file. The syntax for crontab is as follows:

```
crontab [-u user] [-l | -e | -r] [file]
```

If given without the -u user parameter, crontab modifies the cron job associated with the current user. (User cron jobs are often called crontabs; but because the word is already used in reference to the system-wide configuration file and the utility itself, this usage can be perplexing.) The crontab utility can become confused by the use of su to change the current user identity, so if you use this command, it’s safest to also use **-u *user***, even when you’re modifying your own *cron* job.

If you want to work directly on a *cron* job, use the `-l`, `-r`, or `-e` option. The `-l` option causes *crontab* to display the current *cron* job; `-r` removes the current *cron* job; and `-e` opens an editor so that you can edit the current *cron* job. (*Vi* is the default editor, but you can change this by setting the *VISUAL* or *EDITOR* environment variable, as described in Chapter 1.)

Alternatively, you can create a *cron* job configuration file and pass the filename to *crontab* using the *file* parameter. For instance, *crontab* -u **tbaker** **my-cron** causes *crontab* to use **my-cron** for *tbaker*’s *cron* jobs.

Whether you create the *cron* job and submit it via the *file* parameter or edit it via `-e`, the format of the *cron* file is similar to that described earlier. You can set environment variables by using the form *VARIABLE*=***value***, or you can specify a command preceded by five numbers or wildcards to indicate when the job is to run. In a user *cron* job, you do *not* specify the *username* used to execute the job, as you do with system *cron* jobs. That information is derived from the owner of the *cron* job. Listing 7.2 shows a sample *cron* job file. This file runs two programs at different intervals: The **fetchmail** program runs *every* 30 minutes (on the hour and half hour), and **clean-adouble** runs on Mondays at 2:00 a.m. Both programs are specified via complete paths, but you can include a *PATH* environment variable and omit the complete path specifications.

### Listing 7.2: A Sample User *cron* Job File

```
SHELL=/bin/bash
MAILTO=tbaker
HOME=/home/tbaker
0,30 * * * * /usr/bin/fetchmail -s
0 2 * * mon /usr/local/bin/clean-adouble $HOME
```

Ultimately, user *cron* job files are stored in the */var/spool/cron*, */var/spool/cron/tabs*, or */var/spool/cron/crontabs* directory. Each file in this directory is named after the user under whose name it runs; for example, *tbaker*’s file might be called */var/spool/cron/tabs/tbaker*. You shouldn’t directly edit the files in this directory; instead, use *crontab* to make changes.

Access to the *cron* facility may be restricted in several ways:

- **Executable permissions** The permissions on the *cron* and *crontab* programs may be restricted using standard Linux permissions mechanisms, as described in Chapter 4. Not all distributions configure themselves in this way, but for those that do, users who should be able to schedule jobs using *cron* should be added to the appropriate group. This group is often called **cron**, but you should check the group owner and permissions on the */usr/sbin/cron* and */usr/bin/crontab* program files to be sure.
- **Allowed users list** The */etc/cron.allow* file contains a list of users who should be permitted access to *cron*. If this file is present, only users whose names appear in the file may use *cron*; all others are denied access. If this file isn’t present, anybody may use *cron*, assuming access isn’t restricted by executable permissions or a disallowed users list.
