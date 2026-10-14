The following is a sample `/etc/passwd` file:

```
```text
at:x:25:25:Batch jobs daemon:/var/spool/atjobs:/bin/bash
bin:x:1:1:bin:/bin:/bin/bash
daemon:x:2:2:Daemon:/sbin:/bin/bash
ftp:x:40:49:FTP account:/srv/ftp:/bin/bash
games:x:12:100:Games account:/var/games:/bin/bash
gdm:x:50:15:Gnome Display Manager
daemon:/var/lib/gdm:/bin/bash
haldaemon:x:101:102:User for
haldaemon:/var/run/hal:/bin/false
lp:x:4:7:Printing daemon:/var/spool/lpd:/bin/bash
...
geeko:x:1000:100:Geeko Chameleon:/home/geeko:/bin/bash
```
```

Each line in the `/etc/passwd` file represents one user and contains the information shown in Figure 9-9 (separated by colons).

![](bbox=[0.106, 0.397, 0.916, 0.524])

Note the following about the fields in each line:

+   - *User-name*—This is the name a user enters to log in to the system (login name).
+   - *Password*—The x in this field means that the password is stored in the `/etc/shadow` file.
+   - *UID*—In compliance with the Linux standards, three number ranges are reserved:
+     - 0 for root
+     - 1–99 for the system itself
+     - 100–499 for special system users (such as services and programs)
+     - 1000+ for normal users
+   - *GID*—Number of the group. In compliance with the Linux standards, two number ranges are reserved:
+     - 0–99 for special system groups, including root (such as services and programs)
+     - 100+ for normal groups
+   - *Comments field*—Normally, the full name of the user is stored here. Information such as a room number or telephone number can also be stored here.