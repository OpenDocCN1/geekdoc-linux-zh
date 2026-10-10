
# Administering Users and Groups

```text
boot.log-20150808
boot.log-20150818
boot.log-20150823
btmp
ConsoleKit
cron
cron-20150808
cron-20150818
cron-20150823
cups
[root@server1 ~]# _

maillog-20150823
messages
messages-20150808
messages-20150818
messages-20150823
mysqld.log
news
npm
pm-powersave.log
pm-suspend.log

speech-dispatcher
spooler
spooler-20150808
spooler-20150818
spooler-20150823
squid
sssd
tallylog
wtmp
Xorg.0.log
```

Given the preceding output, the most recent events for the cron daemon are recorded in the cron.log file, followed by the cron-20150823 file, followed by the cron-20150818 file and the cron-20150808 file.

You must log in to a Linux system with a valid user name and password before a BASH shell is granted. This process is called authentication because the user name and password are authenticated against a system database that contains all user account information. Authenticated users are then granted access to files, directories, and other resources on the system based on their user account.

The system database that contains user account information typically consists of two files: `/etc/passwd` and `/etc/shadow`. Every user typically has a line that describes the user account in `/etc/passwd` and a line that contains the encrypted password and expiration information in `/etc/shadow`.

Older Linux systems stored the encrypted password in the `/etc/passwd` file and did not use an `/etc/shadow` file at all. This is considered poor security today because processes often require access to the user information in `/etc/passwd`. Storing the encrypted password in a separate file that cannot be accessed by processes prevents a process from obtaining all user account information. By default, Fedora 13 configures passwords using an `/etc/shadow` file. However, you can use the `pwconv` command to revert to using an `/etc/passwd` file only. Also, you can use the `pwconv` command to configure the system again using an `/etc/shadow` file for password storage.

Each line of the `/etc/passwd` file has the following colon-delimited format:

`name:password:UID:GID:GECOS:homeDirectory:shell`

The name in the preceding output refers to the name of the user. If an `/etc/shadow` is not used, the password field contains the encrypted password for the user; otherwise, it just contains an `x` character as a placeholder for the password stored in `/etc/shadow`.

The User Identifier (UID) specifies the unique User ID that is assigned to each user. Typically, UIDs that are less than 500 refer to user accounts that are used by daemons when logging in to the system. The root user always has a UID of zero.

The Group Identifier (GID) is the primary Group ID for the user. Each user can be a member of several groups, but only one of those groups can be the primary group. The primary group of a user is the group that is made the group owner of any file or directory that the user creates. Similarly, when a user creates a file or directory, that user becomes the owner of that file or directory. GECOS represents a text description of the user and is typically left blank; this information was originally used in the General Electric Comprehensive Operating System (GECOS). The last two fields represent the absolute pathname to the user’s home directory and the shell, respectively.

An example of an `/etc/passwd` file is shown next:

```bash
[root@server1 ~]# cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody::/:/sbin/nologin
dbus:x:81:81:System message bus::/:/sbin/nologin
usbmuxd:x:113:113:usbmuxd user::/:/sbin/nologin
avahi-autoipd:x:499:499:avahi-autoipd:/var/lib/avahi-autoipd:/sbin/nologin
rpc:x:32:32:RPCbind Daemon:/var/lib/rpcbind:/sbin/nologin
ruserx:x:29:496:RPC Service User:/var/lib/nfs:/sbin/nologin
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
named:x:25:25:Named:/var/named:/sbin/nologin
apache:x:48:486:Apache:/var/www:/sbin/nologin
gdm:x:42:468::/var/lib/gdm:/sbin/nologin
hsqldb:x:96:96::/var/lib/hsqldb:/sbin/nologin
jetty:x:487:467::/usr/share/jetty:/bin/sh
user1:x:1000:1000:sample user one:/home/user1:/bin/bash
[root@server1 ~]# _
```

The root user is usually listed at the top of the `/etc/passwd` file, as just shown, followed by user accounts used by daemons when logging in to the system, followed by regular user accounts. The final line of the preceding output indicates that the user `user1` has a UID of 1000, a primary GID of 1000, a GECOS of "sample user one," the home directory `/home/user1`, and uses the BASH shell.

Like `/etc/passwd`, the `/etc/shadow` file is colon-delimited yet has the following format:

`name:password:lastchange:min:max:warn:disable1:disable2`

Although the first two fields in the `/etc/shadow` file are the same as those in `/etc/passwd`, the contents of the password field are different; the password field in the `/etc/shadow` file contains the encrypted password, whereas the password field in `/etc/passwd` contains an `x` character because it is not used.

The `lastchange` field represents the date of the most recent password change; it is measured in the number of days since January 1, 1970. For example, the number 10957 represents January 1, 2000, because January 1, 2000, is 10957 days after January 1, 1970.

![](img/c27875544958897d817484d558c208c8_474_0.png)

To prevent unauthorized access to a Linux system, it is good form to change passwords for user accounts regularly. To ensure that passwords are changed, you can set them to expire at certain intervals. The next three fields of the `/etc/shadow` file indicate information about password expiration: `min` represents the number of days a user must wait before he changes his password after receiving a new one, `max` represents the number of days a user can use the same password without changing it, and `warn` represents the number of days before a password would expire that a user is warned to change his password.

By default on Red Hat Fedora Linux systems, `min` is equal to zero days, `max` is equal to 99999 days, and `warn` is equal to seven days. This means you can change your password immediately after receiving a new one, your password expires in 99999 days, and you are warned seven days before your password needs to be changed.

When a password has expired, the user is still allowed to log in to the system for a certain period of time, after which point the user is disabled from logging in. The number of days after a password expires that a user account is disabled is represented by the `disable1` field in `/etc/shadow`. In addition, you can choose to disable a user from logging in at a certain date, such as the end of an employment contract. The `disable2` field in `/etc/shadow` represents the number of days since January 1, 1970 that a user account will be disabled.

An example `/etc/shadow` file is shown next:

```bash
[root@server1 ~]# cat /etc/shadow
root:$6$VIoletCT$ESaz6q.5UTH/SriWflph9.0gHMFvH3h3R515uyxyl9p-jezZbmn8WgPpKIwvfUatNZoW3tiaXULbqDyQEeBTk2.:14841:0:99999:7:::
bin::14715:0:99999:7:::
daemon::*:14715:0:99999:7:::
adm::*:14715:0:99999:7:::
lp::*:14715:0:99999:7:::
sync::14715:0:99999:7:::
shutdown:*:14715:0:99999:7:::
halt::*:14715:0:99999:7:::
mail:*:14715:0:99999:7:::
uucp:*:14715:0:99999:7:::
operator:*:14715:0:99999:7:::
games:*:14715:0:99999:7:::
gopher:*:14715:0:99999:7:::
ftp:*:14715:0:99999:7:::
nobody::*:14715:0:99999:7:::
dbus:!!:14823::::::
usbmuxd:!!:14823::::::
avahi-autoipd:!!:14823::::::
rpc:!!:14823:0:99999:7:::
rpcuser:!!:14823::::::
nfsnobody:!!:14823::::::
named:!!:14823::::::
apache:!!:14823::::::
gdm:!!:14823::::::
hsqldb:!!:14823::::::
jetty:!!:14823::::::
user1:56$SFvyl5FBXS$nK5DUvCFTaFXOU3_h38n_docg5C842YzuINXdbjQ/nEURBQP1pqr23xqFg3eW1S84fYtJoDPvUDucmCt_dNiWFI:16342:0:99999:7:::
[root@server1 ~]# _
```

Note from the preceding output that most user accounts used by daemons do not receive an encrypted password.

Although every user must have a primary group listed in the `/etc/passwd` file, each user can be a member of multiple groups. All groups and their members are listed in the `/etc/group` file. The `/etc/group` file has the following colon-delimited fields:

`name:password:GID:members`

The first field is the name of the group, followed by a group password.

![](img/c27875544958897d817484d558c208c8_475_0.png)

The password field usually contains an `x`, because group passwords are rarely used. If group passwords are used on your system, you need to specify a password to change your primary group membership using the `newgrp` command discussed later in this chapter. These passwords are set using the `gpasswd` command and can be stored in the `/etc/gshadow` file for added security. Refer to the `gpasswd` manual or info page for more information.

The GID represents the unique Group ID for the group, and the members field indicates the list of group members. An example `/etc/group` file is shown next:

```bash
[root@server1 ~]# cat /etc/group

root:x:0:root

bin:x:1:root,bin,daemon

daemon:x:2:root,bin,daemon

sys:x:3:root,bin,adm

adm:x:4:root,adm,daemon

tty:x:5:

disk:x:6:root

lp:x:7:daemon,lp

mem:x:8:

kmem:x:9:

wheel:x:10:root

mail:x:12:mail

uucp:x:14:uucp
```
