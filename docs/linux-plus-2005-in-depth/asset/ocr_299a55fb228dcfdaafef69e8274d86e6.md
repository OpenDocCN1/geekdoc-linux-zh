```
LOGNAME=root; export LOGNAME
LESSOPEN=\!/usr/bin/lesspipe.sh %s; export LESSOPEN
G_BROKEN_FILENAMES=1; export G_BROKEN_FILENAMES
COLORTERM=gnome-terminal; export COLORTERM
XAUTHORITY=/root/.Xauthority; export XAUTHORITY
cd /root || {
echo 'Execution directory inaccessible' >&2
exit 1
}
$ (SHELL=:/bin/sh) << `(dd if=/dev/urandom count=200 bs=1 2>/dev/null|LC_ALL=C tr -d -c '[ :alnum:]')`
date > /root/atfile
who >> /root/atfile
[root@server1 root]# _
```

To remove the at job used in the preceding example, simply specify the -d option to the at command, followed by the appropriate at Job ID, as shown in the following output:

```
[root@server1 root]# at -d 1
[root@server1 root]# at -l
[root@server1 root]# _
```

![](bbox=[0.05, 0.55, 0.95, 0.6])

Alternatively, you can use the atrm 1 command to remove the first at job; the atrm command is simply a shortcut to the at -d command.

If there are many commands to be scheduled using the at daemon, you can choose to place these commands in a shell script and schedule the shell script to execute at a later time using the -f option to the at command. An example of scheduling a shell script called myscript using the at command is shown next:

```
[root@server1 root]# cat myscript
#This is a sample shell script
date > /root/atfile
who >> /root/atfile
[root@server1 root]# at 10:15pm July 16 -f myscript
job 2 at 2004-07-26 22:15
[root@server1 root]# _
```

If the /etc/at.allow and /etc/at.deny files do not exist, only the root user is allowed to schedule tasks using the at daemon. To give this ability to other users, simply create an /etc/at.allow file and add the names of users allowed to use the at daemon, one per line. Conversely, you can