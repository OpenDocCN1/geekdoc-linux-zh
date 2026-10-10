To see the contents of the at job listed in the previous output alongside the shell environment at the time the at job was scheduled, you can use the -c option to the at command and specify the appropriate at job ID:

```
```
[root@server1 ~]# at -c 1
#!/bin/sh
# atrun uid=0 gid=0
# mail     root 0
umask 22
XDG_VTNR=2; export XDG_VTNR
XDG_SESSION_ID=1; export XDG_SESSION_ID
HOSTNAME=server1; export HOSTNAME
SHELL=/bin/bash; export SHELL
HISTSIZE=1000; export HISTSIZE
QT_GRAPHICSSYSTEM_CHECKED=1; export QT_GRAPHICSSYSTEM_CHECKED
USER=root; export USER
MAIL=/var/spool/mail/root; export MAIL
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin; export PATH
PWD=/root; export PWD
LANG=en_US.UTF-8; export LANG
KDEDIRS=/usr; export KDEDIRS
HISTCONTROL=ignoredups; export HISTCONTROL
SHLVL=1; export SHLVL
XDG_SEAT=seat0; export XDG_SEAT
HOME=/root; export HOME
LOGNAME=root; export LOGNAME
LESSOPEN=|/usr/bin/lesspipe.sh %s; export LESSOPEN
XDG_RUNTIME_DIR=/run/user/0; export XDG_RUNTIME_DIR
cd /root || {
    echo 'Execution directory inaccessible' >&2
    exit 1
}
${SHELL:-/bin/sh} << 'marcinDELIMITER2b2a920e'
date >/root/atfile
root >>/root/atfile
marcinDELIMITER2b2a920e
[root@server1 ~]# _
```
```

To remove the at job used in the preceding example, simply specify the -d option to the at command, followed by the appropriate at job ID, as shown in the following output:

```
```
[root@server1 ~]# at -d 1
[root@server1 ~]# at -l
[root@server1 ~]# _
```
```

![](bbox=[0.17, 0.9, 0.3, 0.97])

Alternatively, you can use the atrm 1 command to remove the first at job. The atrm command is simply a shortcut to the at -d command.