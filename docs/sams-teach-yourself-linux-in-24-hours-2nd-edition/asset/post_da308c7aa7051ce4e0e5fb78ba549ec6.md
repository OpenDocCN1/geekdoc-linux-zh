
As you can see, this is why the at command depends on the cron command: the cron command runs the atrun command, found under the /usr/sbin directory, each minute your system is up. The atrun command, in turn, searches the /var/spool/atjobs directory to look for jobs to run. For example, if the root operator creates a job at 14:46 for that day (2:46 p.m.), you see the following:

```
# at 14:46
at> echo Hello
at> <EOT>
warning: commands will be executed using /bin/sh
job 11 at 1998-12-14 14:46
```

```
# ls -l /var/spool/atjobs
total 1
-rwx------ 1 root root 842 Dec 14 14:43 a000b00e85b62
```

To create an at command, use the word at, followed by a time. After you press Enter, the at > prompt appears. You can then enter a command and press Enter. To quit entering commands and save your job, press Ctrl+D. The at command then tells you the job number and the date and time the command executes. As you can see in the atjobs directory listing after entering the command, there is a job waiting for the root operator.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_549_0.png)

> You can get more specific information about waiting at jobs with the atq command. If you're the root operator, you see all the jobs your users have scheduled, instead of just the ones you've scheduled.

## Controlling the batch and at Commands

Now that you know how the at facilities run, how do you control how at works, and for whom, on your system? One way to control how at works on your OpenLinux system is to use the atrun command's -l (load average) option. This option controls any jobs submitted by users using the batch command (discussed in Hour 18 with the at command). You can limit when batch jobs are run by specifying a number lower than 1.5 (the default), which tells atrun to run batch jobs only when the system load average is low. The load average is determined by a value in the /proc/loadavg file while the system is running.

You can see the current load average with the following:

```
# cat /proc/loadavg
0.20 0.11 0.03 2/50 1228
```

This shows the load average for the last 5, 10, and 15 minutes. You can also get the load average by using the uptime command, for example:

```
# uptime
7:40pm up 2:44, 3 users, load average: 0.13, 0.08, 0.02
```

To enable your users to use batch nearly any time, change the value of the -l option in the atrun command entry in your system's /etc/crontab file to a number higher than the default 1.5 value.

How do you control whether users are enabled to use the at command on your system? By default, after you install OpenLinux, anyone on your system can use the at command. There are four ways to control who can use the at command. Look in your /etc directory, and find a file called at.deny.

For security reasons, the at.deny file contains a list of OpenLinux users, including daemons or other processes, who are not enabled to use at. However, everyone else can use the at command to schedule jobs. If you want to prevent a user from using the at command, put the user's username in /etc/at.deny. If you don't want anyone on your system to use the at command (of course, this doesn't apply to you because you're the root operator), either create an empty at.allow file or delete the at.deny file from your /etc directory. If you want to enable only certain users to use the at command, create a file called at.allow in the /etc directory, and put the user's username in the file. If the at.allow and at.deny files are removed from the /etc directory, only the root operator can use the at command.

As a final, desperate measure to control at jobs as the root operator, list all at jobs scheduled on your system with the atq command, and if you see too many jobs scheduled, delete them with the atrm command, for example:

```
# atq
Date Owner Queue Job#
20:00:00 11/26/97 bball c 12
20:10:00 11/26/97 bball c 13
20:15:00 11/26/97 bball c 14
20:30:00 11/26/97 bball c 15
...
# atrm 12 13 14 15 ...
```

Here, I'm assuming you see a long, long list of job numbers, and delete them. This is an abrupt, rude way to handle enthusiastic users. A better method might be to email the user to find out if there are tasks being run that can be automated during off-hour or off-peak times.

As the system administrator, you have complete control of scheduling commands for the users of your OpenLinux system. Think about tasks you should run hourly, daily, weekly, and monthly. With a little imagination, you can soon automate any custom tools, command lines, and reports you've created to help you manage your system. You can end up with more disk space, a better running system, and happier users.

## Summary

This hour introduced you to a valuable skill required of all system administrators—the capability to schedule and automate complex tasks at any required date or time. This is one of the secrets to becoming a successful system administrator—to initially spend the time crafting a general-purpose approach or tool for system maintenance that can be used over and over again.

## Q&A

Q I'd like to have my computer automatically connect to the Internet during the early morning hours and then download the day's news and email the news to me. Is this possible?

A Yes. Use the name of a shell script in your system's crontab file to initiate the connection, temporarily sleep, wake up, and then download and mail the news. For example, the lynx browser's dump option can be used with the mail command like this:

```
lynx http://some.newsource.com/news.html -dump ; mail
 -s 'news' root
```

## Exercises

- 1. Create personal crontab settings to remind you several days in advance of important dates, such as anniversaries or birthdays. What do you think is the best way to have OpenLinux notify you?
- 2. Draw up a list of some important tasks to automate. How can you do this? When do you run the tasks?

## INDEX

### Symbols

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_552_0.png)

% operator, 133
? option, 76
$EDITOR
environment, 403
variable, 320, 403
$HOME environment variable, 139
$PATH
environment variable, 128
variable, 127
$SPRINTER, 355
$PS1 environment variable, 129
$REMOTE_IP
string, 232
variable, 232
$TERMCAP variable, 129
'/ol bit bucket, 139
+rv (reverse video) option, 162
+x option, 494

--bpp (bits per pixel) option, 179
--bpp 16 option, 146
--bpp 16 startx option, 374
-9 option, 464
-9 signal, 463
-a limit option, 462
-a option, 79, 334, 462
-atime option, 74
-b (backup) option, 99, 101
-b option, 99, 333, 456
-bd option, 162
-bg option, 161
-boardSize small option, 442
-bpp 16 option, 145
-bpp option, 145
--bytes option, 456
-C (color) option, 278
-C cls2 option, 219
-C command-line option, 389
-c option, 245, 253, 453, 459, 487

-calendar option, 406
-clear option, 394
-color option, 80
-COLUMN option, 339
-component-bar option, 301
-d (decompress) option, 82, 91, 114
-d (delete) option, 139
-d (directory) option, 492
-d option, 141, 253, 331
-digital option, 175
-display command, 400
-e (empty) option, 139
-e (erase) option, 501
-e (uninstall) option, 499
-E option, 110, 159, 342, 403, 413, 526
-exec option, 459
-f (flood) option, 245
-f (script file) option, 332
-F option, 79-80, 96, 109, 112, 333, 401
-fetchmailrc option, 252
-fg option, 161

-fr option, 96-97
-full-time option, 94
-fullscreen option, 169
-grab option, 445
-gray option, 394
-h (halt) option, 38
-h (help) option, 139
-h option, 275, 499
-Ha option, 462
-help option, 76, 84, 301, 369
-i (extract) option, 517
-i (install) option, 499-500
-i (interactive) option, 95, 99-101, 130, 134
-inroot option, 172
-k (keep) option, 252
-K option, 78, 456
-kilobytes option, 456
-l (list shells) option, 472
-l (list) option, 114, 139, 333, 405
-l (load average) option, 528
-l (long) format listing, 330
-l mode, 333
-l option, 213, 333, 340, 487, 491, 501
usage, 464
-lock option, 171
-M command-line option, 88
-m option, 79, 487
-mail option, 260
-modem option, 201
-mono option, 394
-mtime option, 74, 517
-n 2 option, 89
-n option, 84, 91, 273
-news option, 282
-nosplash option, 369
-nw (no-window) option, 316
-nw option, 409

-o (create) option, 517
-O option, 342
-out option, 167
-p (package file) option, 487, 500
-p (parent) option, 97
-p option, 98, 102, 252
-pkg option, 503
-pointsize option, 394
-popup option, 407
-q (query) option, 89, 499-500
-qi option, 505
-r (reboot) option, 38
-r (recursive) option, 95-96, 101, 457
-r (remove) option, 405
-r (restart) option, 475
-r option, 50, 82, 219, 273, 342
-remove-files option, 111
-rpn option, 383
-rv (reverse video) option, 162
-s (squeeze) option, 330
-s command, 461
-s option, 103, 118, 255, 453
-size option, 442
-sound option, 445
-speed option, 445
-stipple option, 383
-summarize option, 456
-T media option, 518
-t option, 114, 342, 345, 455, 457, 475, 518
-test option, 501
-topbottom option, 368
-tv option, 114
-tvtvm option, 394
-U (upgrade) option, 499, 501
-u option, 252, 319, 475, 525
-update 1 option, 175

-user option, 517
-useradm option, 469
-v (verbose mode) option, 517
-V (verify) option, 499
-v option, 112, 219, 517
-w 60 option, 342
-w option, 149, 204
-x (extract) option, 79, 112
-x option, 457
-xdev option, 75
-xrm option, 162
-z option, 110
.GIF, 360
.GIF format, 298, 368
.GIF graphics, 374
.html files, 377
.JPG, 360
file, 375
graphics file creating, 367
.PCX, 360
.pdf documents, 377
.pdf files, 377, 416
.ppm format, 368
.TIF, 360
.tiff file, creating, 368
.xpm format, 367
/boot directory, 50
/dev/modem, creating, 201
lisa command usage, 201
/etc/fstab, 482
/JOIN command, 305
/LEAVE command, 305
/LIST command, 305
/proc directory, 483
/QUIT command, 305
0x224, 13
0x382, 13
3Com Palm Pilot Professional, 12
3Com/U.S. Robotics, 224
3D graphics, 391, 393
generation, 391
