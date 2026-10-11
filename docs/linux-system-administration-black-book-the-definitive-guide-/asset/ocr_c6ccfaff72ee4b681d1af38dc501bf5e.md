# Immediate Solutions

# Activating And Deactivating The Shadow Suite

The shadow suite has two major components: passwords and groups. Although shadow passwords are generally active by default on a Red Hat installation, if you have them deactivated, you can turn them on with the command `pwconv`. To remove them, use the command `pwunconv`.

Shadow groups are typically not already active. To turn them on, use the command `grpconv`. To remove the group shadow feature, use `grpunconv`.

# Shutting Off Unnecessary Daemons And Background Processes

To stop unnecessary daemons and other processes from starting automatically in Red Hat Linux, do the following:

+   1. Log in as root.

+   2. Type `ps aux | more` to show the list of all running processes without the beginning scrolling off the top of the screen.

+   3. Look through the processes. Some of these are things you need, and some are started from the assumption that you might need them.

TIP: *Utilize the man system if you cannot tell whether you want a particular item. Type "man process" to learn what it does.*

+   4. Type `cd /etc/rc.d` to change to the parent directory that contains all the runlevel boot directories. Red Hat's runlevels are laid out in Table 9.9.

+   5. Type `ls rc#.d`, where # stands for the runlevel whose boot information you want to edit.

+   6. Type `ls S*` and press Enter. Everything you see here is a daemon that starts when you enter this runlevel. The number after each S corresponds to when the daemon starts. The lower the number, the sooner it starts.