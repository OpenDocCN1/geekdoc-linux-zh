single option (although options to fine-tune its behavior are also available): a time. This time can take any of several forms:

**Time of day** You can specify the time of day as *HH:MM*, optionally followed by **AM** or **PM** if you use a 12-hour format. If the specified time has already passed, the operation is scheduled for the next occurrence of that time—that is, for the next day.

**noon, midnight, or teatime** These three keywords stand for what you’d expect (*teatime* is 4:00 *p.m.*).

**Day specification** To schedule an at job more than 24 hours in advance, you must add a day specification after the time-of-day specification. This can be done in numeric form, using the format *M/D/YYYY*, *M/D/YY* or *DD.MM.YY*. Alternatively, you can specify the date as *month-name day* or *month-name day year*.

**A specified period in the future** You can specify a time using the keyword *now*, a plus sign (+), and a time period, as in *now + 2 hours* to run a job in two hours.

![](bbox=[0.14, 0.4, 0.22, 0.44])

The at command relies on a daemon, *atd*, to be running. If your system doesn’t start *atd* automatically, you may need to configure a SysV startup script to do so.

When you run *at* and give it a time specification, the program responds with its own prompt, *at>*, which you can treat much like your normal bash or other common shell prompt. When you’re done typing commands, press Ctrl+D to terminate input. Alternatively, you can pass a file with commands by using the -f parameter to *at*, as in *at -f commands.sh* to use the contents of *commands.sh* as the commands you want to run at *noon*.

The *at* command has several support tools. The most important of these is *atd*, the atd daemon. This program must be running for at to do its work. If it’s not, check for its presence using *ps*. If it’s not running, look for a SysV startup script and ensure that it’s enabled, as described in Chapter 5.

Other at support programs include *atq*, which lists pending at jobs; *atrm*, which removes an at job from the queue; and *batch*, which works much like at but executes jobs when the system load level drops below 0.8. These utilities are all fairly simple. To use *atq*, simply type its name. (The program does support a couple of options, but chances are you won’t need them; consult *atq*’s man page for details.) To use *atrm*, type the program name and the number of the at job, as returned by *atq*. For instance, you might type *atrm 12* to remove at job number 12.

The at facility supports access restrictions similar to those of *cron*. Specifically, the */etc/at.allow* and */etc/at.deny* files work analogously to the */etc/cron.allow* and */etc/cron.deny* files. There are a few wrinkles with at, though. Specifically, if neither *at.allow* nor *at.deny* exists, only root may use at. If *at.allow* exists, the users it lists are granted access to at; if *at.deny* exists, everybody *except* those mentioned in this file is granted access to at. This differs from *cron*, in which everybody is granted access if neither access-control file is present. This tighter default security on at means that the program is seldom installed with restrictive execute permissions, but of course you can use program file permissions to deny ordinary users the ability to run at if you want an extra layer of security.