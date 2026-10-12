```
enabled 1
failure 1
pid 634
rate_limit 0
backlog_limit 8192
lost 0
backlog 0
enabled 1
failure 1
pid 634
rate_limit 0
backlog_limit 8192
lost 0
backlog 1
```

For more information on the Audit rules and the augenrules script, see the `audit.rules(8)` and `augenrules(8)` man pages.

# ### 6.6. UNDERSTANDING AUDIT LOG FILES

By default, the Audit system stores log entries in the `/var/log/audit/audit.log` file; if log rotation is enabled, rotated `audit.log` files are stored in the same directory.

The following Audit rule logs every attempt to read or modify the `/etc/ssh/sshd_config` file:

```
-w /etc/ssh/sshd_config -p wexec -k sshd_config
```

If the `auditd` daemon is running, for example, using the following command creates a new event in the Audit log file:

```
-[J]$ cat /etc/ssh/sshd_config
```

This event in the `audit.log` file looks as follows:

```
type=SYSCALL msg=audit(1364481363.243:24287): arch=c000003e syscall=2
success=no exit=-13 a0=7fff d19c5592 a1=0 a2=7fffd19c4b50 a3=a items=1
ppid=2686 pid=3538 audit=1000 uid=1000 gid=1000 euid=1000 suid=1000
fsuid=1000 fegid=1000 fgid=1000 fsgid=1000 ttype=pts0 ses=1 comm="cat"
exe="/bin/cat" subj=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
key="sshd_config"
type=CWD msg=audit(1364481363.243:24287): cwd="/home/shadowman"
type=PATH msg=audit(1364481363.243:24287): item=0
name="/etc/ssh/sshd_config" inode=4090248 dev=fd:00 mode=0100600 ouid=0
gooid=0 rdev=00:00 obj=system_u:object_r:etc_t:s0 objtype=NORMAL
cap_fp=none cap_fi=none cap_fe=0 cap_fver=0
type=PROCTITLE msg=audit(1364481363.243:24287): 
proctitle=636174002f6574632f7373682f737368645f636f6e66
```

The above event consists of four records, which share the same time stamp and serial number. Records always start with the `type=` keyword. Each record consists of several `name=value` pairs separated by a white space or a comma. A detailed analysis of the above event follows:

# #### First Record