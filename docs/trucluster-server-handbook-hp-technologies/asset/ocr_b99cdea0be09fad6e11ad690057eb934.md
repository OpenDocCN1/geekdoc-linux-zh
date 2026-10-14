```
BEGIN_ENTRY
HOST=molari
TIME=Sat Aug 17 14:25:50 2001
CMND=shutdown now
MEMBER_SHUTDOWN_SEQUENCE=molari-ics0
END_ENTRY

BEGIN_ENTRY
HOST=molari
TIME=Sat Aug 15 15:22:47 2001
CMND=shutdown now
MEMBER_SHUTDOWN_SEQUENCE=molari-ics0
END_ENTRY
```

```
# date
Sat Aug 17 15:56:39 EDT 2001
```

# 19.2.3 File System Manipulation Commands

Other commands seem to work properly in a cluster without any special options. Consider the purpose of file manipulation commands such as showfdmn(8), mkfdmn(8), mount(8), etc. The CPS makes their actions inherently cluster-wide. Therefore you will see no special cluster options in file system oriented commands. Some commands (such as the passwd(1) command) use cluster-wide database files and thus become cluster-oriented indirectly.

Back up and restore activities in a cluster are similar to a standalone system's backup and restore, but since members share the file systems (for the most part) you only have to backup the cluster once and not once per member. CDSLs are treated as any other symbolic link would be treated.

# 19.2.4 Kill Command

The kill(1) command will work properly and signal the target process even if that process is running on another cluster member. You are probably a step ahead of me in figuring out how this could possibly work given that Process Identifiers (PIDs) are specific to a system. There has been a change in the meaning of several bits in the PID. If you ever find yourself yearning for the good old days when you could conveniently understand PIDs, the following script may help.

```
# ps -Ao pid,comm | grep init
524289 init
525353 rdgin it
```