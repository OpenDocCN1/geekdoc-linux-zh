
# Managing Users and Groups

![](img/35f616c7eba4e79e12bfd762129c5d27_397_0.png)

The /etc/shadow file is normally stored with very restrictive permissions, such as rw------- (600), with ownership by root. (Precise permissions vary from one distribution to another, though.) This fact is critical to the shadow system's utility because it keeps non-root users from reading the file and obtaining the password list, even in an encrypted format. By contrast, /etc/passwd is readable by ordinary users and usually has rw-r--r-- (644) permissions. If you manually modify /etc/shadow make sure it has the correct permissions when you're done.

# Real World Scenario

# Network Account Databases

Many employees employ network account databases. These systems include the Network Information System (NIS), an update to this system called NIS+, the Lightweight Directory Access Protocol (LDAP), Kerberos, Windows NT 4.0 domains, and Active Directory (AD) domains. All of these systems account database management unto a single centralized computer (often with one or more backup systems). The advantage of this approach to account maintenance is that users and administrators do not deal with maintaining accounts independently on multiple computers. A single account database can handle accounts on dozens (or hundreds or thousands) of different computers, greatly simplifying day-to-day administrative tasks and simplifying users' lives. Using such a system means that most users don't appear in /etc/passwd and /etc/shadow, and groups may not appear in /etc/group. (These files will still hold information on local system accounts and groups, though.)

Linux can participate in these systems. In fact, some distributions provide options to enable support at OS installation. Typically, you must know the name or IP address of the server that hosts the network account database, and you must know what protocol the server uses. You may also need a password or some other protocol-specific information, and the server may need to be configured to access the Linux system you're configuring.

Activating such network account databases after installing Linux is a complex topic. It involves installing appropriate software, modifying the /etc/passwd.conf file, and modifying the Pluggable Authentication Module (PAM) configuration files in /etc/pam.d. Such systems often alter the behavior of tools such as passwd and usermod in subtle or not-subtle ways. If you need to use such a system, you'll have to consult documentation specific to the service you intend to use. My book Linux in a Windows World (O'Reilly, 2005) covers this topic for Windows NT 4. domains, LDAP, and Kerberos; and Mark Minasi and Dan York's Linux for Windows Administrators (Sysex, 2002) covers this topic for Windows NT 4.0 domains and NIS.

# Deleting Accounts

On the surface, deleting user accounts is easy. You may use the userdel command to get the job of removing a user's entries from /etc/passwd and, if the system uses shadow passwords, /etc/shadow. The userdel command takes three parameters:

- Remove User Files: The -r or --remove parameter causes the system to remove all files from the user's mail spool and home directory, as well as the home directory.
- Force Deletion: You can force deletion of the account while a user is logged in by using the -f or --force option in conjunction with -r. This option also forces removal of the mail spool even if it is owned by another user and forces removal of the home directory even if another user uses the same home directory.
- Get Help: The -h or --help option summarizes userdel options.

As an example, removing the sally account is easily accomplished with the following command:

```bash
# userdel -r sally
```

You may omit the -r parameter if you want to preserve the user's files. Be aware of potential complication: Users may create files outside their home directories. For instance, many programs use the /tmp directory as "scratch space," so user files open until deleting. These files are deleted automatically after a certain period, but you may have other directories in which users store files. To locate all such, you can use the find command with -uid parameter (or -user, if you find before deleting the account). For instance, if sally is UID 1029, you can use the following command to delete all her files:

```bash
# find / -uid 1029
```

A result is a list of files by UID 1029 (formerly sally). You can go through this list and decide what to do with the files—change their ownership to somebody else, delete them, back up to CD-R, or what you have. It's wise to do something with these files, or may be assigned ownership to another user if Sally's UID is reused. This can become awkward if the file exceeds the new user's disk quota or if they contain data that the new user should not—such as a person may be mistakenly accused of indiscretions or even crimes.

A few notably Samba--keep their own of files. If you run a server, it's best to remove the user's entry from that user list when you remove the user's main account. In the case of Samba, this is normally done by manually editing the smbpasswd file (usually located in /etc,/etc/samba, or /etc/samba.d) and deleting the line corresponding to the user in question or by using the smbpasswd command and its -x option, as in smbpasswd -x sally to delete the sally account from Samba's database.

# Configuring Groups

Linux provides group configuration files that parallel those for accounts in many ways. Groups are not accounts, however, many features differ. Likewise, you can create or modify groups by directly editing the configuration files.

# Managing Users and Groups

Their layout is similar to that for account files, but the utilities and configuration files differ.

# Adding Groups

Linux uses the groupadd command to add a new group. This utility is similar to useradd but has fewer options. The groupadd syntax is as follows:

```bash
groupadd [-g GID [-o]] [-r] [-f] groupname
```

The parameters to command enable you to adjust its operation:

- Specify a GID: You can provide a specific GID with the -g parameter. If you omit this parameter, groupadd uses the next available GID. Normally, the GID you specify must be unused by other groups, but the -o parameter overrides this behavior, enabling you to create multiple groups that share one GID.
- Create a System Group: The -r parameter instructs groupadd to create a group with a GID of less than SYS_MIN, as defined in /etc/login.defs. Groups with GIDs in this range are considered system groups, which are used by tools or help control access to system resources, such hardware device files. Not all distributions support this option; it was added by Red Hat and has been used for groups of 500 and greater for user private groups (that is, groups named after individuals), which is the reason for the -r parameter.
- Force Creation: Normally, if you try to create a group that already exists, groupadd returns an error message. The -f parameter suppresses that error message. Not all versions of groupadd support this parameter.

In most cases, you will create groups without specifying any parameters except for the group name itself:

```bash
# groupadd project3
```

This command creates the project3 group, giving it whatever GID the system finds convenient—usually the highest GID. Once you've done this, you can add users to the group, as described in the next section.

# Modifying Group Information

Group information, like user account information, may be edited by using utility programs or by directly editing the underlying configuration file, /etc/group. There are fewer options for modifying groups than for accounts, and the utilities and configuration files are similar. In fact, usermod is one of the tools that's used to modify groups.

**Using groupmod and usermod**
The groupmod command modifies an existing group's settings. Its syntax is as follows:

```bash
groupmod [-g GID [-o]] [-n newgroupname] oldgroupname
```
