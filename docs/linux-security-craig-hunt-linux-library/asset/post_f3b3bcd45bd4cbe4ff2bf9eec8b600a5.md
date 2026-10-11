
As discussed earlier, `s` in the user portion of the permissions mask denotes that the `setuid` and `execute` bits are set for the user (file owner). This means that the file will execute with the user permissions of the file owner (root) instead of the executing user (ramon). In addition, you can set the `setgid` bit in order to have the file execute with the group permissions of root, as follows:

```
[ramon]$ sudo chmod 6755 report
[ramon]$ ls -1 report
-rwsr-sr-x  1 root      root        19032 Sep 25 20:30 report
```

The third bit in the permissions mask is often referred to as the *sticky bit*, and is used in directories to signal the Linux kernel that it should not allow a user to delete another user’s files, even if the directory is world-writable. This is most often used in the `/tmp` directory, which has wide-open permissions:

```
[ramon]$ ls -1d /tmp
drwxrwxrwt  7 root      root        1024 Sep 25 21:05 /tmp
```

Note the final `t` in the mask. This prevents you from deleting your fellow user’s files in that directory unless they explicitly allow you to do so by setting write permissions for others.

In general, use of `setuid` and `setgid` should be restricted to those partitions that are only writeable by root. I recommend that you explicitly disallow use of `setuid`/`setgid` on the `/home` directory, by specifying the `nosuid` option in the `/etc/fstab` file, as shown in Listing 2.3.

### Listing 2.3 Contents of the `/etc/fstab` file

```
[ramon]$ cat /etc/fstab
/dev/sda8            /                    ext2        defaults            1  1
/dev/sda1            /boot                ext2        defaults            1  2
/dev/sda6            /home                ext2        exec,nodev,nosuid,rw 1  2
/dev/sda5            /usr                 ext2        defaults            1  2
/dev/sda7            /var                 ext2        defaults            1  2
/dev/sda9            swap                 swap        defaults            0  0
/dev/fd0             /mnt/floppy          ext2        noauto              0  0
/dev/cdrom           /mnt/cdrom           iso9660     noauto,ro           0  0
none                 /proc                proc        defaults            0  0
none                 /dev/pts            devpts      mode=0622           0  0
```

Figure 2.7 illustrates how this option can be specified from Red Hat’s `linuxconf` utility.

### Figure 2.7 Setting the nosuid option on a local filesystem with linuxconf

![](img/3258bbaf790525f8c4eb25fabff7844a_73_0.png)

Also, note that the No Special Device File Support option (option nodev in /etc/fstab) is selected. This effectively prevents a user from creating a block device in the /home filesystem, which would be considered a highly suspect action by a nonprivileged user.

Having taken these precautions, you still need to be vigilant of the setuid/setgid present on your Linux server. I suggest that you run this command in cron, piping its output to an e-mail report to your mailbox every morning, as follows:

```
find / -type f \( -perm -04000 -o -perm -02000 \) -exec ls -l { } \;
```

This command should report on all the scripts that have either the setuid or the setgid bit set in the permissions mask. Compare the current report with the previous day’s report, and ensure that any new files have been created by the administration staff. At the very least, you should have the output of this command written to a separate file within /var/log.

> **NOTE** The Linux kernel allows you to use setuid/setgid permissions only on binary executables, not on shell scripts. This restriction protects against malicious tampering with shell scripts, a common occurrence that can result in a serious compromise of root.

# The umask setting

The default permissions for new files created on your server can have a profound impact on its overall security. Users who create world-writable files by default are effectively poking tiny holes in your system security. Linux uses the umask configuration setting to control default file permissions. Its usage is

```
umask AAA
```

where AAA is the octal complement of a default permissions mask of 666 (777 for directories). For instance, a umask of 022 would yield a default permission of 644 for files (the result of subtracting 022 from 666). Let's look at an example in Listing 2.4.

### Listing 2.4 umask configuration examples

```
console
[ramon]$ umask 000
[ramon]$ touch example1
[ramon]$ ls -l example1
-rw-rw-rw- 1 ramon users 0 Sep 25 22:08 example1
[ramon]$ umask 022
[ramon]$ touch example2
[ramon]$ ls -l example2
-rw-r--r-- 1 ramon users 0 Sep 25 22:08 example2
[ramon]$ umask 66
[ramon]$ touch example3
[ramon]$ ls -l example3
-rw------- 1 ramon users 0 Sep 25 22:08 example3
```

I recommend that you edit your /etc/profile file to assign a mask of 066 to the root user and assign a mask of 022 to your regular users. This ensures that root-created files have no permissions for group and others, while any other files are created with world-read permissions only.

# Limiting Core Dump Size

A common means for a local user to gain root privileges is to force a setuid/setgid program to dump a core file (upon crashing) in a specific location within the filesystem. By using this method to overwrite arbitrary files anywhere on the server, including /etc/passwd, /etc/hosts.equiv, or .rhosts, intruders can effectively create for themselves a user with root privileges. With today's servers having gigabytes of physical memory available, these core files could potentially fill an entire disk, which would result in a denial of service (DoS) attack for other users relying on the same filesystem.

There is an effective way to keep core files under control. Using the ulimit command, you can control the resource utilization limits of any user, including the maximum size of a core dump file. You should simply set this size to 0, using the following command:

```
 ulimit -c 0
```

You can include this command in the global /etc/profile configuration file also.

# syslog Security

One of the most significant skills of sophisticated intruders is their ability to clean up all evidence that an attack has taken place. This is the electronic equivalent of a criminal using gloves at the scene of the crime, and it’s a constant source of frustration for those who make a living out of tracking down the actions of these intruders.

You should go to whatever lengths are necessary to make sure that you can safeguard some evidence that your system was tampered with. The problem is that it’s very difficult to guarantee that your log files are correct when attackers could be modifying them with their root privileges. You should take advantage of the syslog program’s ability to send a copy of all log events to a remote server.

For example, in order to send all your kernel, mail, and news messages to a remote syslog server (hostname “zurich”), add the following line to your /etc/syslog.conf configuration file:

```
kern.*, mail.*, news.*[TAB]@zurich
```

(Don’t forget that the syntax of this file calls for a tab character to be inserted between fields.)

After making this modification, you must send the -HUP (hang-up) signal to the syslog daemon to force it to read its configuration:

```
[ramon]$ sudo killall -HUP syslogd
```

Keep in mind, however, that some services may not be configured or able to log events via syslog. You should use cron to move those services’ log files to a remote server several times throughout the day—the more often the better.

# Filesystem Encryption

However strong your physical and system security measures are, you need to be ready for the time when a user gains access to some other user’s files. Cryptography is your last line of defense. By encrypting the contents of sensitive directories, users can protect the privacy of their data even after an intrusion has succeeded.

This section describes two different ways to do this, both of which are based on secret-key technology using standard encryption algorithms. Let’s take a look at each of them in more detail.
