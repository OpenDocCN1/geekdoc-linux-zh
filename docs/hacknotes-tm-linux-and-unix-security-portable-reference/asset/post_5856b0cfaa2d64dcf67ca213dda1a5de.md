
| Filename | User | Group | Permissions |
| --- | --- | --- | --- |
| `/var/log/secure*` | root | root | -rw------- |
| `/var/log/spooler*` | root | root | -rw------- |
| `/var/log/syslog*` | root | root | -rw------- |
| `/var/log/utmp*` | root | utmp | -rw-rw-r-- |
| `/var/log/wtmp*` | root | utmp | -rw-rw-r-- |
| `/var/log/xferlog` | root | root | -rw------- |
| `/var/run` | root | root | drwxr-xr-x |
| `/var/run/*.pid` | root | root | -rw-r--r-- |
| `/var/spool/cron` | root | root | drwx------ |
| `/var/spool/cron/crontabs/root` | root | root | -rw------- |
| `/var/spool/mail` | root | mail | drwxrwxr-x |
| `/var/spool/mail/*` | user | user | -rw-rw---- |
| `/var/tmp` | root | root | drwxrwxrwt |

> A few files listed in the preceding table may not be applicable to all distributions. Also, some files may exist in different directories. Use the find command to locate them: find / -type f -name filename -print 2> /dev/null.

## FILES IN /dev

Devices are represented by special files in the /dev directory, and appropriate file permissions must be set on such files. Consider /dev/hda*, which represents IDE disks in Linux. If these files are readable by the world, malicious users will have read permissions to all data on the disks! Use the mount command to find out the /dev files associated with mounted drives on a system.

In addition, ensure that proper permissions are set on other device files, such as /dev/console, /dev/tty/*, /dev/pty*, /dev/audio, and /dev/dsp*.

## DISK PARTITIONS

A malicious user may launch a denial of service attack by consuming all available disk space. Consider the following command:

```bash
cat /dev/zero > /tmp/zero^C
```

The preceding command will cause a new file, /tmp/zero, to be created. This file's size will continue to increase unless the user interrupts the command by pressing CTRL-C. The file /dev/zero is a special, never-ending file containing zeros. By letting the preceding command run for a while, a malicious user may consume all space on the disk. This may cause undesirable results, since many running programs need and depend on available disk space to function properly.

It is recommended that the following directories be mounted in separate partitions:

- /boot
- /home(s)
- /tmp
- /var

Also, consider using the no dev, no suid, and no exec options when mounting the /var and /tmp partitions.

## setuid AND setgid FILES

Check for files that have the setuid and setgid bits set, since such files are executed with the permissions of the owner. Vulnerabilities in root- or wheel-owned setuid and setgid files may lead to root compromise. If possible, consider removing the setuid and setgid bits from files.

To find setuid files, run

```bash
find / -perm -4000 -type f -print 2> /dev/null
```

To find setgid files, run

```bash
find / -perm -2000 -type f -print 2> /dev/null
```

## IMPLEMENT THE wheel GROUP

Use the wheel group to limit access to setuid programs such as su. If this group does not exist, create it with the groupadd command. Change the permissions of su so that only users in the wheel group may execute it:

```bash
chgrp wheel $(which su)
chmod u+s,o-rwx,urwx,g+rx $(which su)
```

## SUDO

Sudo is a freeware tool that allows permitted users to execute commands with root privileges. If multiple individuals need to perform privileged operations, it is a good idea to set up Sudo to provide them with specific permissions. This is better than sharing the root password. Sudo is usually bundled with most distributions, but it can also be obtained at http://www.sudo.ws/sudo/. Please see http://www.onlamp.com/pub/a/bsd/2002/08/29/Big_Scary_Daemons.html for instructions and examples on how to set up and configure Sudo.

## SUMMARY

It is important to understand and enforce proper file permissions. World-readable and -writable files must be routinely audited for, in addition to files owned by system accounts such as bin and sys. The umask value should be set to be as restrictive as possible. Important configuration files must also be audited to ensure proper permissions. Disk partitions must be created for directories such as /tmp and /var to protect against denial of service attacks. The wheel group should be used to restrict access to executables such as setuid programs whenever possible. It is also a good idea to use Sudo in order to allow users to execute files with superuser privileges. This is much better than sharing the root password.

# Chapter 9

# Logging and Patching

**IN THIS CHAPTER:**

- Logging
- Patching
- Summary

This chapter describes the most common methods of system event logging; the sections that follow cover specific log files and the information they contain. It is important for every system administrator to understand different events and where they are logged. Without this information, a system administrator will have no idea of what events and activities are taking place on the host.

In addition to logging, another important issue is that of software updates. Every day, software vulnerabilities are announced for which exploit code is released. Most often, such vulnerabilities are fixed by software vendors in the form of patches, or software updates. This chapter provides resources on where one can obtain such software patches.

## LOGGING

This section describes specific log files and the information contained in them. In addition, issues such as disk space on `/var` and log rotation are also discussed. As an administrator, be sure to understand the information presented in this section in order to detect abnormal system activities and behavior.

### Log Files

Here are some common log files and the information that is usually logged into them. It is a good idea to go through these files on a routine basis.

> Depending upon your Unix or Linux distribution, some log files may be located in different directories. Use the `find` command to locate the files if you can't find them: `find /var -name filename -print 2> /dev/null.`

### /var/audit

Most Solaris distributions come bundled with BSM (Basic Security Module), a utility that logs user action details. Since BSM audits act on the system call level, huge logs may be generated.
To enable BSM, switch to runlevel 1:

```bash
init 1
```

Next, run `bsmconv`:

```bash
cd /etc/security ; ./bsmconv
```

Configure /etc/security/audit_control to choose what events to log. See http://www.securityfocus.com/infocus/1362 for detailed instructions. Reboot for the changes to take effect.

### /var/adm/loginlog

After five unsuccessful login attempts, all further attempts are logged to this file. Each log event contains the login name, tty information, and time. This file is logged to only if it exists. Therefore, create this file if it doesn’t exist, using the touch command. Make sure this file is readable only by root.

### /var/adm/sulog

The su command is used to log in to another user’s account. For example, user joe may su to log in to jack’s account:

```bash
[joe’s_bash]$ su - jack
Password: jackpassword
[jack’s_bash]$
```

Similarly, a user may log in as root using the su command:

```bash
[joe’s_bash]$ su -
Password: rootpassword
[root’s_bash]#
```

It is important to log all su attempts. Doing so will help detect brute-force password guessing attempts by malicious local users. Edit /etc/default/su and make sure the value of SULEG points to /var/adm/sulog. You may also enable syslogd logging by setting the value of SYSLOG to yes.

### /var/log/cron

The cron daemon logs information to this file. Edit /etc/syslog.conf and make sure the following line is present:

```bash
cron.*    /var/log/cron
```

### /var/log/maillog

This file contains information logged by the host’s mail server. Details about outgoing and incoming e-mails and appropriate error messages are logged to this file. Edit /etc/syslog.conf and make sure the following line exists:

```bash
mail.*    /var/log/maillog
```
