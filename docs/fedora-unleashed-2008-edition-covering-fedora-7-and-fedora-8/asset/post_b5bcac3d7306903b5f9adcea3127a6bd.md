
## NOTE

Other files that might have suid or guid permissions include at, rcp, rlogin, rsh, chage, chsh, ssh, crontab, sudo, sendmail, ping, mount, and several UNIX-to-UNIX Copy (UUCP) utilities. Many programs (such as games) might also have this type of permission to access a sound device.

Files or programs that have suid or guid permissions can sometimes present security holes because they bypass normal permissions. This problem is especially compounded if the permission extends to an executable binary (a command) with an inherent security flaw because it could lead to any user or intruder gaining root access. In past exploits, this typically happened when a user fed a vulnerable command with unexpected input (such as a long pathname or option); the command would bomb out, and the user would be presented a root prompt. Although Linux developers are constantly on the lookout for poor programming practices, new exploits are found all the time, and can crop up unexpectedly, especially in newer software packages that haven't had the benefit of peer developer review.

Savvy Linux system administrators keep the number of suid or guid files present on a system to a minimum. The `find` command can be used to display all such files on your system:

```bash
# find / -type f -perm +6000 -exec ls -l {} \
```

## NOTE

The `find` command is quite helpful and can be used for many purposes, such as before or during backup operations. See the section “Using Backup Software” in Chapter 13, “Backing Up.”

Note that the programs do not necessarily have to be removed from your system. If your users really do not need to use the program, you can remove execute permission of the program for anyone. You have to decide, as the root operator, whether your users are allowed to, for example, mount and unmount CD-ROMs or other media on your system. Although Linux-based operating systems can be set up to accommodate ease of use and convenience, allowing programs such as `mount` to be suid might not be the best security policy. Other candidates for suid permission change could include the chsh, at, and chage commands.

## Managing Passwords

Passwords are an integral part of Linux security, and they are the most visible part to the user. In this section, you learn how to establish a minimal password policy for your system, where the passwords are stored, and how to manage passwords for your users.

An effective password policy is a fundamental part of a good system administration plan. The policy should cover the following:

- Allowed and forbidden passwords
- Frequency of mandated password changes
- Retrieval or replacement of lost or forgotten passwords
- Password handling by users

### The Password File

The password file is `/etc/passwd`, and it is the database file for all users on the system. The format of each line is as follows:

```
username:password:uid:gid:gecos:home dir:shell
```

The fields are self-explanatory except for the `gecos` field. This field is for miscellaneous information about the user, such as the user's full name, his office location, office and home phone numbers, and possibly a brief text message. For security and privacy reasons, this field is little used nowadays, but the system administrator should be aware of its existence because the `gecos` field is used by traditional UNIX programs such as `finger` and `mail`. For that reason, it is commonly referred to as the *finger information field*. The data in this field is comma delimited; the `gecos` field can be changed with the `chg` (change finger) command.

Note that a colon separates all fields in the `/etc/passwd` file. If no information is available for a field, that field is empty, but all the colons remain.

If an asterisk appears in the password field, that user is not permitted to log on. Why does this feature exist? So that a user can be easily disabled and (possibly) reinstated later without having to be created all over again. The system administrator manually edits this field, which is the traditional UNIX way of accomplishing this task. Fedora provides improved functionality with the `passwd` `-l` command mentioned earlier.

Several services run as pseudo-users, usually with root permissions. These are the system, or logical, users mentioned previously. You would not want these accounts available for general login for security reasons, so they are assigned `/sbin/nologin` as their shell, which prohibits any logins from those “users.”

A listing of `/etc/passwd` reveals the following:

```
# cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
gdm:x:42:42::/var/gdm:/sbin/nologin
named:x:25:25:Named:/var/named:/sbin/nologin
dovecot:x:97:97:dovecot:/usr/libexec/dovecot:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
andrew:x:500:500:Andrew Hudson:/home/andrew:/bin/bash
```

Note that the password fields do not show a password, but contain an x because they are shadow passwords, a useful security enhancement to Linux, discussed in the following section.

### Shadow Passwords

It is considered a security risk to keep any password on `/etc/passwd` because anyone with read access can run a cracking program on the file and obtain the passwords with little trouble. To avoid this risk, shadow passwords are used so that only an x appears in the password field of `/etc/passwd`; the real passwords are kept in `/etc/shadow`, a file that can be read by only the sysadmin (and PAM, the Pluggable Authentication Modules authentication manager; see the “PAM Explained” sidebar for an explanation of PAM).

Special versions of the traditional password and login programs must be used to enable shadow passwords. Shadow passwords are automatically enabled during the installation phase of the operating system on Fedora systems.

Let's examine a listing of the shadow companion to `/etc/passwd`, the `/etc/shadow` file:

```
# cat /etc/shadow
root:::13121::0:99999::7:::
daemon:*::13121::0:99999::7:::
bin:*::13121::0:99999::7:::
sys:*::13121::0:99999::7:::
sync:*::13121::0:99999::7:::
games:*::13121::0:99999::7:::
man:*::13121::0:99999::7:::
...
andrew:$1$z/9LTBHLs0mt70dYk.KJL7rwB1M0511::13121::0:99999::7:::
```

The fields are separated by colons and are, in order, the following:

1. The user's login name.
2. The encrypted password for the user.
3. When the password was last changed, measured in the number of days since January 1, 1970. This date is known in UNIX circles as the epoch. Just so you know, the billionth second since the epoch occurred was in September 2001; that was the UNIX version of Y2K— not much happened because of it.
4. The number of days before the password can be changed (prevents changing a password and then changing it back to the old password right away— a dangerous security practice).
5. The number of days after which the password must be changed. This can be set to force the change of a newly issued password known to the system administrator.
6. The number of days before password expiration that the user is warned it will expire.
7. The number of days after the password expires that the account is disabled (for security).
8. The number of days since January 1, 1970 that the account has been disabled.
9. The final field is a “reserved” field and is not currently allocated for any use.

Note that password expiration dates and warnings are disabled by default in Fedora. These features are not used on home systems and usually not used for small offices. It is the sysadmin’s responsibility to establish and enforce password expiration policies.

The permissions on the `/etc/shadow` file should be set so that it is not writable or readable by regular users: The permissions should be 600.

### PAM Explained

Pluggable Authentication Modules (PAM) is a system of libraries that handle the tasks of authentication on your computer. It uses four management groups: account management, authentication management, password management, and session management. This allows the system administrator to choose how individual applications will authenticate users. Fedora has preinstalled and preconfigured all the necessary PAM files for you.

The configuration files in Fedora are found in `/etc/pam.d`. These files are named for the service they control, and the format is as follows:

```
type control module-path module-arguments
```

The type field is the management group to which the rule corresponds. The control field tells PAM what to do if authentication fails. The final two items deal with the PAM module used and any arguments it needs. Programs that use PAM typically come packaged with appropriate entries for the `/etc/pam.d` directory. To achieve greater security, the system administrator can modify the default entries. Misconfiguration can have unpredictable results, so back up the configuration files before you modify them. The defaults provided by Fedora are adequate for home and small office users.
