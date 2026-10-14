
networking protocols that do not play well with passwords longer than eight characters. For example, only the first eight characters are significant in NIS+ passwords because the underlying secure-RPC protocol uses DES.

Consider the following suggestions when choosing a password-hashing algorithm for your system:

- When using DES, set the minimum password length to be at least six; use an eight-character password for root.
- If all interconnected systems support MD5, use MD5 as the password-hashing algorithm and set the minimum password length to be at least six.
- Consider using Blowfish for all system accounts that require a password. (However, this means you need to switch the password-hashing method from the current setting to Blowfish, change the password, and restore the setting. An alternative is to install the Blowfish-aware version of Perl—the version included with SLES 9 supports only DES and MD5—so you can use a simple script to first generate the hashed value using Perl and then set the password using `usermod -p hashed_value`.)

### TIP

You can find the RPM for a version of Perl that supports Blowfish at http://rpmfind.net/linux/RPM/contrib/libc6/i386/perl-Crypt-Blowfish-2.09-1.i386.html and at http://rpmfind.net/linux/RPM/suse/8.2/i386/suse/i586/perl-Crypt-Blowfish-2.09-188.i586.html. The Perl crypt home page is at http://www.cpan.org/modules/Crypt.

In most cases, MD5 provides the best balance between performance and security.

## Auditing Default Accounts

As mentioned earlier, a number of system accounts exist to allow programs to be run as the UID associated with that account; they are not direct login accounts. FTP, named (for DNS), mail, and news are some examples of such system accounts. Make sure such accounts are prevented from a terminal login by setting their shell to `/bin/false` or similar.

If the services for these accounts are not in use, uninstall them and remove the accounts—or at the very least, disable unused services (see Chapter 8 for more information). Periodically, you should check the contents of `/etc/passwd` and `/etc/shadow` to ensure that the removed system accounts didn’t “spontaneously resurrect” themselves or new system accounts were not added without your knowledge, and nonlogin system accounts don’t “suddenly” get assigned valid password hashes and shells.

## The Root Account

The root account is the key to your entire server kingdom (and to your entire network if the server in question serves as the central authentication server). Nothing is more important than the password to the root account in the Linux/Unix world. For this reason, you will not want to make your root password known to anyone else but yourself. Well, this is often easier said than done.

As you may already have found out, many of the administrative tasks, such as resetting a user's forgotten password, changing system configuration, and so on, require you to be root. If you’re the lone ranger who looks after the system(s) at your organization, keeping the root password safe is relatively easy. Follow the recommendations given earlier in this chapter about selecting strong passwords, change it often, never write it down, and so on. However, it is not uncommon in a company for system administration tasks to be shared by two or more people. In such cases, how do you safeguard the root password effectively? The more people who know it, the higher the likelihood it will be leaked to someone who shouldn’t know about it!

### TIP

> If you are the sole system administrator at your organization, it might be a good idea to record the root password in a sealed envelope and keep it in a secure location where only trusted company officers (such as the accountant or CTO) have access to it; a bank safety deposit box is a good choice. The idea here is that although you would want to keep the root password secret from others, you need to provide a way for “continuity” should you be unavailable, due to illness or any other reasons.

There are a number of ways to address the multiple administrator requirements, and we discuss two of them here:

- **Setting up multiple root users**—Instead of providing the root password to the people who need access, you can set up multiple root accounts. Suppose, for example, both Tasha and Carol require administrative access as part of their job. One way to track their root activities is to set up two separate accounts, say tasha-root for Tasha and carol-root for Carol, each with a unique (strong) password and each with a UID of 0. Whenever Tasha needs root privileges, she would log in as tasha-root or su as `tasha-root`. Carol would do so as `carol-root`. This method has the advantage of having an audit trail in the form of process accounting and system logging for each administrator and without having to share the root password. The disadvantage is that each duplicate UID 0 account is another potential vulnerability.

Because adding another UID 0 account is also a common hacker practice, you should review `/etc/passwd` frequently to check for illegal UID 0 accounts. You can also use Bastille (see Chapter 13) to automatically detect unauthorized duplicate root accounts.

### CAUTION

You should not name the root-equivalent accounts with “-root” as that makes it easy for the hackers to zero in on accounts to attack.

- **Using sudo**—The best way of granting multiple users root access is via the sudo (superuser do) utility. sudo allows you to grant certain users (or groups of users) the ability to run some (or all) commands as root while logging all commands and arguments used, regardless of whether the command was successful. All sudo commands are logged in the log file `/var/log/messages`, which can be very helpful in determining how user error may have contributed to a problem. All the sudo log entries have the word sudo in them, so you can easily get a thread of commands used by using the grep command to selectively filter the output accordingly. sudo operates on a per-command basis, and it is not a replacement for the shell.

### NOTE

Further discussion about sudo can be found in Chapter 5.

Running as root *all the time* is not a very good idea. Because it grants you all-powerful, unlimited access to the server and its files, one little mistake may render the whole system useless. For example, before you execute `rm -r` (or even just `rm *`), make very sure you are in the right directory! In general, think twice before you perform certain actions as root. Here are some tips regarding using the root account:

- Become root only when absolutely necessary.
- Gain root access only through `su` or `sudo`.
- Restrict from which terminal console(s) root can log in. (See man security and refer to the “Authentication Using PAM” section in Chapter 5 for more information.)
- Exercise extreme care when executing potentially destructive commands (such as rm -f while being root).
- Use absolute pathnames when invoking commands. This helps to eliminate executing a Trojan Horse program that may have been installed in one of the nonsystem directories that is pointed to by the PATH environment variable.

### TIP

When setting up root's environment, do not put user-writable directories in root's PATH. This reduces the chance of running a Trojan Horse program placed (knowingly or not) by a user.

- Whenever you need to remotely administer a system as root, use SSH (discussed in the “Securing Network Services” section in Chapter 13) and sudo.

## User in Too Many Groups?

Linux and most other recent Unix systems support at least 32 groups per user. However, because the NFS protocol supports only 16 groups, most of them (SUSE included) have imposed a soft limit of 16 groups per user. There are very rarely circumstances that require more than 16 groups, but it is usually possible to use more if the system will not be exporting or using NFS-mounted filesystems; NFS has a hard-coded limit of 16 groups in its underlying RPC protocol. The first 16 groups are passed to the NFS server for permission checking, while the others are ignored. In other words, a user might appear to belong to a group, but if the 16-group limit is exceeded, the user might not have the access privileges of that group.

## Summary

This chapter provided information on how users and groups are identified in Linux and how you can effectively manage user and group information using
