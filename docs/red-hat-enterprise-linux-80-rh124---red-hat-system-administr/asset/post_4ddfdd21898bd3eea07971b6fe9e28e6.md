
# CHAPTER 12 | Accessing Linux Filesystems

Generate a list of all block devices in the /dev directory on host:

```
[root@host]# find /dev -type b
/dev/vd1
/dev/vda
```

The -links option followed by a number looks for all files that have a certain hard link count. The number can be preceded by a + modifier to look for files with a count higher than the given hard link count. If the number is preceded with a - modifier, the search is limited to all files with a hard link count that is less than the given number.

Search for all regular files with more than one hard link on host:

```
[root@host]# find / -type f -links +1
```

> REFERENCES
locate(1), updatedb(8), and find(1) man pages

# GUIDED EXERCISE

# LOCATING FILES ON THE SYSTEM

In this exercise, you will find specific files on mounted file systems using the **find** and **locate** commands.

# OUTCOMES

You should be able to search files using the **find** and **locate** commands.

# BEFORE YOU BEGIN

Log in as the **student** user on workstation using **student** as the password.

From workstation, run the **lab fs-locate start** command. The command runs a script that determines whether the host, servera, is reachable on the network.

```
[student@workstation ~]$ lab fs-locate start
```

- 1. Use the **ssh** command to log in to **servera** as the **student** user.

```
[student@workstation ~]$ ssh student@servera
[student@servera ~]$
```

- 2. Use the **locate** command to search files on **servera**.

2.1 Even though the **locate** database is updated automatically every day, make sure that the database is up-to-date by manually starting an update on **servera**. Use the **sudo updatedb** command to update the database used by the **locate** command.

```
[student@servera ~]$ sudo updatedb
[sudo] password for student: student
[student@servera ~]$
```

2.2 Locate the **logrotate.conf** configuration file.

```
[student@servera ~]$ locate logrotate.conf
/etc/logrotate.conf
/usr/share/man/man5/logrotate.conf.5
```

2.3 Locate the **networkmanager -i networkmanager.conf** configuration file, ignoring case.

```
[student@servera ~]$ locate networkmanager.conf
/etc/NetworkManager/NetworkManager.conf
/etc/dbus-1/system/d.freedesktop.NetworkManager.conf
/usr/share/man/man5/NetworkManager.conf.5
```

- 3. Use the **find** command to perform real-time searches on servera according to the following requirements:

- Search all files in the **/var/lib** directory that are owned by the **chrony** user.
- List all files in the **/var** directory that are owned by **root** and the group owner is **mail**.
- List all files in the **/usr/bin** directory that has a file size greater than 50 KB.
- Search all files in the **/home/student** directory that have not been changed in the last 120 minutes.
- List all block device files in the **/dev** directory.

3.1. Use the **find** command to search all files in the **/var/lib** directory that are owned by chrony user. Use the **sudo** command as the files inside the **/var/lib** directory are owned by root.

```
[student@servera ~]$ sudo find /var/lib -user chrony
[sudo] password for student: student
/var/lib/chrony
/var/lib/chrony/drift
```

3.2. List all files in the **/var** directory that are owned by root and are affiliated with the **mail** group.

```
[student@servera ~]$ sudo find /var -user root -group mail
/var/spool/mail
```

3.3. List all files in the **/usr/bin** directory with a file size greater than 50 KB.

```
[student@servera ~]$ find /usr/bin -size +50k
/usr/bin/iconv
/usr/bin/locale
/usr/bin/localedef
/usr/bin/cmp
...output omitted...
```

3.4. Find all files in the **/home/student** directory that have not been changed in the last 120 minutes.

```
[student@servera ~]$ find /home/student -mmin +120
/home/student/.bash_logout
/home/student/.bash_profile
/home/student/.bashrc
...output omitted...
```

3.5. List all block device files in the **/dev** directory.

```
[student@servera ~]$ find /dev -type b
/dev/vdb
/dev/vda3
/dev/vda2
/dev/vda1
/dev/vda
```

- 4. Exit from servera.

```
[student@servera ~]$ exit
logout
Connection to servera closed.
[student@workstation]$
```

# Finish

On workstation, run the lab fs-locate finish script to complete this exercise.

```
[student@workstation ~]$ lab fs-locate finish
```

This concludes the guided exercise.

# ACCESSING LINUX FILE SYSTEMS

![](img/59afb92e10b67a9cecc358a2c65e93b5_570_0.png)

- 1. On serverb as root, identify the UUID for /dev/vdb1 and mount /dev/vdb1 by its UUID on the /mnt/freespace
- 2. Generate a disk usage report of the /usr/share directory, and save the result in the /mnt/freespace/results.txt file.
- 3. Use the locate command to find all syslog.conf configuration files and store the result in the /mnt/freespace/search1.txt file.
- 4. Store the search result of all files in the /usr/share directory that is greater than 50 MB and less than 100 MB in the /mnt/freespace/search2.txt file.
- 5. Exit from serverb.

# Evaluation

On workstation, run the lab fs-review grade script to confirm success.
