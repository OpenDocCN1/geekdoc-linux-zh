
remove two `!` characters at the beginning of the encrypted password field in the /etc/shadow file, respectively.

Yet another method commonly used to lock a user account is to change the shell specified in /etc/passwd for a user account from /bin/bash to an invalid shell such as /bin/false or /sbin/nologin. Without a valid shell, a user cannot use the system. To lock a user account this way, you can edit the /etc/passwd file and make the appropriate change, use the `-s` option to the `usermod` command, or use the `chsh` command. The following example uses the `chsh` command to change the shell to /bin/false for the user bobg:

```
[root@server1 ~]# chsh -s /bin/false bobg
Changing shell for bobg.
chsh: Warning: "/bin/false" is not listed in /etc/shells
Shell changed.
[root@server1 ~]# _
```

## Deleting User Accounts

To delete a user account, you can use the `userdel` command and specify the user name as an argument. This removes entries from the /etc/passwd and /etc/shadow files corresponding to the user account. Furthermore, you can specify the `-r` option to the `userdel` command to remove the home directory for the user and all of its contents.

When a user account is deleted, any files that were previously owned by the user become owned by a number that represents the UID of the deleted user. Any future user account that is given the same UID then becomes the owner of those files.

Suppose, for example, that the user bobg leaves the company. To delete bobg's user account and display the ownership of his old files, you can use the following commands:

```
[root@server1 ~]# userdel bobg
[root@server1 ~]# ls -la /home/bobg
total 52
drwx------  4 1002  1002  4096 Jul 17 15:37 .
drwxr-xr-x  5 root root  4096 Jul 17 15:37 ..
-rw-r--r--  1 1002  1002  24 Jul 17 15:37 .bash_logout
-rw-r--r--  1 1002  1002  191 Jul 17 15:37 .bash_profile
-rw-r--r--  1 1002  1002  124 Jul 17 15:37 .bashrc
-rw-r--r--  1 1002  1002  5542 Jul 17 15:37 .canna
-rw-r--r--  1 1002  1002  820 Jul 17 15:37 .emacs
-rw-r--r--  1 1002  1002  118 Jul 17 15:37 .gtkrc
-rw-r--r--  3  1002  1002  4096 Jul 17 15:37 .kde
drwxr-xr-x  2 1002  1002  4096 Jul 17 15:37 .xemacs
-rw-r--r--  1 1002  1002  3511 Jul 17 15:37 .zshrc
[root@server1 ~]# _
```

From the preceding output, you can see that the UID of the bobg user was 1002. Now suppose the company hires Sue—that is, the user sueb—to replace bobg. You can then assign the UID of 1002 to Sue's user account. Although she will have her own home directory (/home/sueb), she will also own all of bobg's old files within /home/bobg and otherwise. She can then copy the files that she needs to her own home directory and remove any files that she doesn't need as part of her job function.

To create the user sueb with a UID of 1002 and list the ownership of the files in bobg's home directory, you can use the following commands:

```
[root@server1 ~]# useradd -u 1002 sueb
[root@server1 ~]# ls -la /home/bobg
total 52
drwx-----   4 sueb   sueb      4096 Jul 17 15:37 .
drwxr-xr-x   5 root   root      4096 Jul 17 18:56 ..
-rw-r--r--   1 sueb   sueb        24 Jul 17 15:37 .bash_logout
-rw-r--r--   1 sueb   sueb       191 Jul 17 15:37 .bash_profile
-rw-r--r--   1 sueb   sueb       124 Jul 17 15:37 .bashrc
-rw-r--r--   1 sueb   sueb       5542 Jul 17 15:37 .canna
-rw-r--r--   1 sueb   sueb       820 Jul 17 15:37 .emacs
-rw-r--r--   1 sueb   sueb       118 Jul 17 15:37 .gtkrc
-rw-r--r--   3 sueb   sueb      4096 Jul 17 15:37 .kde
drwxr-xr-x   2 sueb   sueb      4096 Jul 17 15:37 .xemacs
-rw-r--r--   1 sueb   sueb       3511 Jul 17 15:37 .zshrc
[root@server1 ~]#
```

## Managing Groups

By far, the easiest way to add groups to a system is to edit the /etc/group file using a text editor. Another method is to use the `groupadd` command. To add a group called group1 to the system and assign it a GID of 492, you can use the following command:

```
[root@server1 ~]# groupadd -g 492 group1
[root@server1 ~]#
```

Then, you can use the `-G` option to the `usermod` command to add members to the group. To add the user mary to this group and view the addition, you can use the following `usermod` command:

```
[root@server1 ~]# usermod -G group1 mary
[root@server1 ~]# tail -1 /etc/group
group1:x:492:mary
[root@server1 ~]#
```

There also exists a `groupmod` command, which can be used to modify the group name and GID, and a `groupdel` command, which can be used to remove groups from the system.

To see a list of groups of which you are a member, simply run the `groups` command; to see the GIDs for each group, simply run the `id` command. The primary group is always listed first by each command. The following output shows sample output of these commands when executed by the root user:

```
[root@server1 ~]# groups
root bin daemon sys adm disk wheel
[root@server1 ~]# id
uid=0(root)   gid=0(root)   groups=0(root),1(bin),2(daemon),3(sys),
4(adm),6(disk),10(wheel)
[root@server1 ~]#
```

In the preceding output the primary group for the root user is the root group. This group is attached as the group owner for all files that are created by the root user, as shown in the following output:

```
[root@server1 ~]# touch samplefile1
[root@server1 ~]# ls -l samplefile1
-rw-r--r-- 1 root root 0 Aug 27 19:22 samplefile1
[root@server1 ~]# _
```

To change the primary group temporarily to another group that is listed in the output of the `groups` and `id` commands, you can use the `newgrp` command. Any new files created afterward will then have the new group owner. The following output demonstrates how changing the primary group for the root user affects file ownership:

```
[root@server1 ~]# newgrp sys
[root@server1 root]# id
uid=0 (root) gid=3 (sys) groups=0 (root), 1 (bin), 2 (daemon), 3 (sys), 4 (adm), 6 (disk), 10 (wheel)
[root@server1 ~]# touch samplefile2
[root@server1 ~]# ls -l samplefile2
-rw-r--r-- 1 root sys 0 Aug 27 19:28 samplefile2
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_483_0.png)

> If you use group passwords as described earlier in this section, you can use the `newgrp` command to change your primary group to a group of which you are not a member, provided you supply the appropriate group password when prompted.

The root user can use the `newgrp` command to change her primary group to any other group.

Although command-line utilities are commonly used to administer users and groups, you can instead use a graphical utility to create, modify, and delete user and group accounts on the system. These utilities run the appropriate command-line utility in the background. To create and manage users and groups in Fedora 20 from within a desktop environment, you can open a terminal application in the desktop environment, switch to the root user, and run the `system-config-users` command to open the User Manager utility shown in Figure 10-6.

![](img/c27875544958897d817484d558c208c8_483_1.png)

**Figure 10-6 Configuring users and groups within a desktop environment**

# Chapter Summary

- Print jobs are spooled to a print queue before being printed to a printer.
- You can configure spooling or printing for a printer by using the `cupsaccept`, `cupsreject`, `cupsenable`, and `cupsdisable` commands.
- Print jobs are created using the `lp` command, can be viewed in the print queue using the `lpstat` command, and are removed from the print queue using the `cancel` command.
- You can configure printers using the `lpadmin` command, the CUPS Web administration tool, or by modifying the `/etc/cups/printers.conf` file.
- Most log files on a Linux system are stored in the `/var/log` directory.
- System events are typically logged to files by the System Log Daemon (syslogd) or to a database by the Systemd Journal Daemon (journald).
- You can use the `journalctl` command to view the contents of the journald database.
- Log files should be cleared or rotated over time to save disk space; the logrotate utility can be used to rotate log files.
- User and group account information is typically stored in the `/etc/passwd`, `/etc/shadow`, and `/etc/group` files.
- You can use the `useradd` command to create users and the `groupadd` command to create groups.
- All users must have a valid password before logging in to a Linux system.
- Users can be modified with the `usermod`, `chage`, `chfn`, `chsh`, and `passwd` commands, and groups can be modified using the `groupmod` command.
- The `userdel` and `groupdel` commands can be used to remove users and groups from the system, respectively.

## Key Terms

| Term | Description |
| :--- | :--- |
| `/etc/cups/cupsd.conf` | A file that holds daemon configuration for the cups daemon. |
| `/etc/cups/printers.conf` | A file that holds printer configuration for the cups daemon. |
| `/etc/default/useradd` | A file that contains default values for user creation. |
| `/etc/group` | The file that contains group definitions and memberships. |
| `/etc/login.defs` | A file that contains default values for user creation. |
| `/etc/logrotate.conf` | The file used by the logrotate utility to specify rotation parameters for log files. |
| `/etc/passwd` | The file that contains user account information. |
| `/etc/syslog.conf` | The main configuration file for the System Log Daemon. |
| `/etc/shadow` | The file that contains the encrypted password as well as password and account expiry parameters for each user account. |
