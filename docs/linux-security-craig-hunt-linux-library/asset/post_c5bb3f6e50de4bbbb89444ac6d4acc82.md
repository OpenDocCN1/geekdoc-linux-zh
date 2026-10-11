
```
daemon:*:11223:0:99999:7:::
adm:*:11223:0:99999:7:::
lp:*:11223:0:99999:7:::
sync:*:11223:0:99999:7:::
shutdown:*:11223:0:99999:7:::
halt:*:11223:0:99999:7:::
mail:*:11223:0:99999:7:::
operator:*:11223:0:99999:7:::
ftp:*:11223:0:99999:7:::
nobody:*:11223:0:99999:7:::
ramon:$aag10.pAvX2uA:11223:0:99999:7:
```

The next section of this chapter discusses the **sudo** utility, a useful tool to minimize the exposure of the root password to your Linux server.

## The sudo Utility

During the normal course of administering my Linux systems, I often go several weeks before actually logging on as the root user. In fact, there have been times when I have come close to forgetting the root password. The **sudo** utility affords me this luxury, and I recommend that you install this tool on every system that you administer. By allowing the system administrator to predefine root access for regular users, **sudo** can be used to execute commands with root privileges in lieu of actually logging in as root, and exposing the root password on the network. In general, the less often the root password is actually typed, the more secure it will be.

## Installing sudo

You can download sudo in both RPM and source format. I recommend that you use the RPM package system to install it, since the default compilation parameters are typically rational, and there is very little need for customization.

Let's start the installation by ensuring that **sudo** is not already present:

```
[root]# rpm -q sudo
sudo-1.5.9p4-1
```

In this case, you do have a previous installation of **sudo**, but it's out of date, so delete it and install a more current version using the following commands:

```
[root]# rpm -e sudo
[root]# rpm -i ./sudo-1.6.3p5-1rh62.1386.rpm
[root]# rpm -q sudo
sudo-1.6.3p5-1
```

You now have installed the sudo utility. Make sure you take a look through /usr/doc for the documentation that comes with the source package before you start using the tool.

## The sudoers file

As with any Linux utility, sudo comes with a configuration file where you can customize its operation. This file is in /etc/sudoers by default, and contains, among other things, the list of users who should be allowed to run the sudo command, along with the set of commands that each sudo user is allowed to execute.

The general format used to add users to this file is as follows:

```
userhost(s)=command(s)[run_as_user(s)]
```

For example, if you’d like to grant user alice permission to run the shutdown command, you specify the following:

```
alice ALL = /etc/shutdown
```

Note that the ALL directive can be used as a wildcard for any fields in the sudoers file. Let’s consider another example where user bob is given access to all root commands, as any user:

```
bob ALL = ALL
```

And finally, let’s consider the case where you’d like user charlie to be allowed to run su to become user operator:

```
charlie ALL = /bin/su operator
```

> **WARNING** If you’re using sudo to grant a user root access to a limited set of commands, make sure that none of these commands allow an "escape" to a Linux shell, because that would give the user unrestricted root access to all system commands. Note that some Linux editors (e.g., vi) include this shell escape feature.

## Using sudo

The basic usage of the sudo command is as follows:

```
sudo [command line options] [username] [command]
```

Table 2.2 contains a summary of the most important sudo command-line options.

**Table 2.2** sudo command-line options

| Option | Parameter | Purpose |
| :--- | :--- | :--- |
| -v | N/A | Prints out the current version. |
| -l | N/A | Lists the allowed and forbidden commands for this user. |
| -h | N/A | Prints usage message. |
| -b | N/A | Runs command in the background. |
| -u | username | Runs the command as the specified username (default is root). |

For example, to show the contents of the shadow password directory, simply use:

```
sudo cat /etc/shadow
```

To edit a file in a user's directory preserving his or her permissions:

```
sudo -u fred vi /export/home/fred/.forward
```

I recommend that you use the sudo command strictly to log the root activity of users who are fully trusted to execute any root command on your Linux server (including yourself), rather than using it to allow certain users the execution of a small set of system utilities. It is relatively easy for a user to maliciously extend the privilege of a given command by executing an escape command to the root shell.

The following section describes sudo's logging features, as well as the format of the sudo log file.

## The sudo.log file

By default, sudo logs all its activity to the file /var/log/sudo.log. The format of entries into this file is as follows:

```
date:user:HOST=hostname:TTY=terminal:PWD=dir:USER=user:COMMAND=cmd
```

Each of these fields has the following meaning:

- **date**: the timestamp of the log entry
- **user**: the username that executed sudo
- **hostname**: the host address on which the sudo command was executed
- **terminal**: controlling terminal from which sudo was invoked
- **dir**: current directory from which the command was invoked
- **user**: username that the command was run as
- **command**: the command that was executed through sudo

For example, Listing 2.2 illustrates a typical sudo_log file showing six entries, all executed by username ramon, invoking commands to be run as root.

### Listing 2.2 Contents of the sudo_log file

```
Sep 23 14:41:37 : ramon : HOST=redhat ; TTY=pts/0 ; PWD=/home/ramon
 ; USER=root ; COMMAND=/bin/more /etc/shadow
Sep 23 14:43:42 : ramon : HOST=redhat ; TTY=pts/0 ; PWD=/home/ramon
 ; USER=root ; COMMAND=/usr/sbin/pwconv
Sep 23 14:43:51 : ramon : HOST=redhat ; TTY=pts/0 ; PWD=/home/ramon
 ; USER=root ; COMMAND=/bin/more /etc/shadow
Sep 23 14:55:30 : ramon : HOST=redhat ; TTY=pts/0 ; PWD=/home/ramon
 ; USER=root ; COMMAND=/bin/cat /etc/security
Sep 23 15:12:27 : ramon : HOST=redhat ; TTY=pts/1 ; PWD=/home/ramon
 ; USER=root ; COMMAND=/bin/linxconf
Sep 23 15:23:37 : ramon : HOST=redhat ; TTY=pts/0 ; PWD=/home/ramon
 ; USER=root ; COMMAND=/usr/sbin/pwconv
```

## File and Directory Permissions

Perhaps one of the most difficult aspects of Linux administration, file permissions are a vital aspect of system security, and as such, an entire section of this book is devoted to their discussion. Linux (like all Unix variants) treats most resources as files, whether they’re directories, disk devices, pipes, or terminals. While this makes for straightforward software architecture, it also introduces a fundamental challenge to the Linux administrator charged with ensuring the security of these resources.

Permissions on files and directories have a direct effect on the security of your system. Make the permissions too tight and you limit users’ ability to get their work done. Make permissions too lax and you invite unauthorized use of other users’ files and general system resources.

The next subsection of this book examines the specifics of suid and sgid permissions on the Linux operating system.

### suid and sgid

Linux supports device and file permissions for three distinct groups of users, each of which is represented by three bits of information in the permissions mask, in addition to two special-purpose high-order bits, for a total of 12 bits:

```
AAA BBB CCC DDD
```

Each of these bits has the following meaning:

- **AAA**: setuid, setgid, sticky-bit
- **BBB**: user (read, write, execute)
- **CCC**: group (read, write, execute)
- **DDD**: other (read, write, execute)

Thus, if we have a new executable file called `report` that we want read, written, and executed only by the file’s owner, but read and executed by everybody else, we would set its permissions to the appropriate bit-mask value as follows:

```bash
[ramon]$ chmod 0755 report
[ramon]$ ls -1 report
-rwxr-xr-x 1 ramon users 19032 Sep 25 19:48 report
```

Note that 7 is the octal representation of the binary number 111. The permissions displayed include only three bits per portion (user, group, other), while in reality, Linux allows you to specify four bits for each of the groups. This is addressed by overloading the representation of the third bit with the following values:

- **x**: execute
- **s**: execute + [setuid or setgid] (applicable only to the user and group portions)
- **S**: [setuid or setgid] (applicable only to the user and group portions)
- **t**: execute + sticky (applicable only to the other portion)
- **T**: sticky (applicable only to the other portion)

Now consider the case where you’d like this file to be executed with root permissions because it has to read and write to privileged areas of the file system, but you would like nonprivileged users to be able to execute it. You can achieve this by setting the very first bit of the permissions mask as follows:

```bash
[ramon]$ sudo chown root:root report
[ramon]$ sudo chmod 4755 report
[ramon]$ ls -1 report
-rwsr-xr-x 1 root root 19032 Sep 25 20:30 report
```
