
## File Creation

A user goes to create a file and permission is denied. First check the directory permissions. If all is well there, consider the following items:

- **Are quotas enforced on this partition?** The user may have hit a quota limit. Check the partition's `/etc/fstab` record for either `usrquota` or `grpquota` to see if quotas are enabled on this filesystem (covered in Chapter 10) or use the `repquota` utility. If quotas are enabled, check the user's (or group's) quota usage using the `quota` command. If the user has exceeded quota limits and the grace period has passed, turn off quotas with `quotaoff`, extend the user's quotas, or have the user delete unneeded files.
- **Has the disk run out of space?** The `df` command (covered in Chapter 20) can help you quickly determine if the partition on which the user is attempting to create a file has run out of space. If you are out of space, take the appropriate action (also covered in Chapter 20).
- **Has the partition run out of inodes?** *Inode exhaustion* is an unusual situation, but it does happen. An inode number (covered in Chapter 3, "Managing Files, Directories, and Text") is a file's associated index number. If a filesystem runs out of inodes, no additional files can be created on it. Check if this is the problem by employing the `df -i` command, which shows each filesystem's inode use.

If inodes are exhausted, you cannot extend them after filesystem creation. Instead, look for directories that have a large amount of small unnecessary files, such as a temporary directory, and remove what you can. A good practice is to put applications that create many small files on their own large partitions formatted to provide higher amounts of inode numbers. At filesystem creation, increase inode counts above their defaults by using utility options like the `mke2fs -i` command.

- **What is the user's *umask* setting?** The `umask` setting (covered in Chapter 15) subtracts permissions from the default file and directory permission settings. Thus, when a user is creating files and/or directories, the permissions set on them are affected by this setting. Have the user enter `umask` at the command line (or check the user's environment file) to determine its setting. If it is set too high (for example, removing needed write permissions for created subdirectories), you have found the cause of the problem.

Just as with access issues, check your Linux kernel security module (SELinux or AppArmor) in situations where a user cannot create or delete files. Peruse the appropriate policy violation log files (/var/log/messages or /var/log/audit/audit.log) using the appropriate tools.

After you have found the policy violation concerning the file or directory in question, determine if the file/directory was mislabeled, the policy is incorrect, or possibly the wrong security context was used. Take appropriate actions to remedy the situation.

## Exploring Environment and Shell Issues

When dealing with user problems, a potential issue is the user account’s default shell. Check it using the getent command, as shown on an Ubuntu distribution in Listing 22.14.

**Listing 22.14:** Determining an account’s default shell with the getent command

```
$ getent passwd BSisko
BSisko:x:1007:1007::/home/BSisko:/bin/sh
$
$ readlink -f /bin/sh
/bin/dash
$ 
```

Notice that instead of the /bin/bash shell as the default shell, the /bin/sh shell is used. On this system, the /bin/sh file is linked to the /bin/dash shell. If this is not desired, you can change the user’s default shell via the usermod command (see Chapter 10).

Incorrect or improperly set environment variables can cause various user difficulties. Review a user's environment file (covered in Chapter 10), such as the ~/.profile file. While you're at it, check the system's global environment variable settings using the set, env, or printenv command.

Ensure that environment variables are exported so that they are available in subshells (a subshell may occur when a shell script is executed.) An example of this problem is shown in Listing 22.15.

**Listing 22.15:** Demonstrating what happens when variables are not exported

```
$ EDITOR='nano'
$ echo $EDITOR
nano
$
$ bash
$
$ echo $EDITOR
$
$ exit
exit
$
```

The user sets the environment variable EDITOR so that their default text editor is now nano. However, when a new subshell is created via the bash command, the setting is lost. To keep the setting persistent, it needs to be exported as well as stored in a user's environment file. An example of exporting the variable is shown in Listing 22.16.

**Listing 22.16:** Demonstrating the export command

```
$ export EDITOR='nano'
$
$ echo $EDITOR
nano
$
$ bash
$
$ echo $EDITOR
nano
$
```

It is also important to make sure you have environment variables in the correct file, global or per user. Also, you must understand what type of login the user conducts in order to set these variables in the right file (see Chapter 10).

## Summary

User issue troubleshooting is tricky. Many components are involved in access, authentication, file management, and the user's shell and environment. Understanding common problems will assist in fixing an issue.

## Exam Essentials

- **Summarize user access problems/solutions.** For impeded local access, research corrupted terminal files, improperly configured GUI components, and expired passwords/accounts. Remote access problems are often caused by misconfigured OpenSSH components or remote desktop applications. Other issues can involve layered authentication software such as PAM or a system's kernel security module, such as SELinux or AppArmor.
- **Describe various file problems/solutions.** File access and management requires understanding of basic file and directory permissions as well as ownership and group membership. Additional system items to review include filesystem quotas, disk space, inode use, and umask settings. Check the kernel security module log files for policy violations as well. If a user cannot delete a file, look for the immutable bit set on the file.
- **Explain user environment and shell issues.** Improperly configured environment variables or ones that are not exported will cause user problems. Examine the various environment files, both global and user, for issues. Difficulties may also arise from the user account's default shell setting.

## Review Questions

1. Lamar, a contractor, claims he cannot log into his account locally. He was able to do so yesterday. No one else seems to be having problems accessing the system. What should you check first?
    A. Check if GUI services are running using the `systemctl` command.
    B. Look at the OpenSSH server configuration files.
    C. Determine if his account has expired by using the `chage` command.
    D. See if the account is locked using the `faillock` utility.
    E. Check for policy violations in the SELinux log files.

2. Irene normally logs into the system locally via the `tty4` terminal but cannot today. She tries her authentication at the `tty3` terminal and logs in successfully. What should you check first?
    A. Determine if getty services are running using the `systemctl` command.
    B. Review access rules in the `/etc/security/access.conf` file.
    C. See if the account is locked using the `passwd -S` command.
    D. Use the `last` command to see when she last logged in.
    E. Check if the `tty4` device file is corrupted using the `ls -l` command.

3. Vincent is attempting to remotely log into the system using OpenSSH without success. He asks you what he can do to help troubleshoot this problem. What should you recommend first?
    A. Check the `/etc/ssh/sshd_config` configuration file.
    B. Add the `-vvv` option on to Vincent's `ssh` command.
    C. Add the `-X` option onto Vincent's `ssh` command.
    D. Confirm that Vincent's public key is stored in the `~/.ssh/authorized_keys` file.
    E. Check the `~/.ssh/config` configuration file.

4. Anton is struggling to determine why a particular user cannot log into a Rocky Linux system, where SELinux is disabled and `auditd` is not used. Which of the following are the best log files to pursue? (Choose two.)
    A. `/var/log/audit/audit.log`
    B. `/var/log/messages`
    C. `/var/log/auth`
    D. `/var/log/secure`
    E. `/var/log/lastlog`
