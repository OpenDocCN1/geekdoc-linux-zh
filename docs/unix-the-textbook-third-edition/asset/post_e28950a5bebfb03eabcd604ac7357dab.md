
## 23.9.2 Access Control: Discretionary (DAC), Mandatory (MAC), and Role-Based (RBAC)

Access control policies determine what access right is granted to what object, under what circumstances (discretionary, mandatory, or role-based) and by what subject. Discretionary access enables an entity (like a user) to grant another entity access rights. Mandatory access will not allow an entity to grant another entity access rights. Rather than use the user ID to determine what access rights users and groups have on the system, the role-based access control (RBAC) paradigm grants access based on the role or roles that a user assumes. In ZFS, for example, when you execute the zfs command, your action is checked to see that the entity issuing the command has the role privilege, even if the user is root. In Solaris, the roleadd command and its options and arguments define roles on the system. Not only does the system administrator need to allocate login and resource use restrictions and privileges on the system, they must control all file and data access in the traditional UNIX system via the chmod command. Ordinarily this is done by root. On PC-BSD, you can by default use the sudo command as well to assume the role of root to issue the chmod, chown, or chgrp for files.

### 23.9.2.1 sudo

On Solaris and PC-BSD systems, programs, commands, and files are traditionally accessed through user and group permissions. Each user has a unique identifier, given either as a username or UID. Users belong to unique groups, given either as a group name or a GID. Specific users and groups have permission to access available programs, commands, and files.

The su command allows a user to switch roles and become the superuser on the system without logging off from their own account. You must know the password of the root account if you want to assume the role of root.

The sudo program allows a single command to be run as root, or even as some other user. The system administrator utilizes a policy listing file (named sudoers) that contains commands that each user can execute. When any user needs to run a command that requires root permissions, that user types sudo command in a console terminal, allowing them to run command. Then, sudo consults its permissions list in the policy listing file. If the user has permission to run that command, it runs the command. If the user does not have permission to run the command, sudo denies execution. Running sudo does not require knowing root’s password, but by default requires the user’s own password to execute successfully.

There are two aspects to sudo: the sudo program itself, and the sudoers policy file that the program uses. The sudoers policy file can only be edited by root. The sudo program includes a special tool, visudo, just for editing and validating the sudoers policy file. On Solaris, the path to the executable program visudo is /usr/sbin, and on PC-BSD the path to visudo is /usr/local/sbin.

The sudoers policy file must only be edited with visudo, because that special editing tool has safeguards built into it. On Solaris and PC-BSD visudo launches the vi text editor to allow editing of the sudoers file. On Solaris, the sudoers file itself is found in /etc. In PC-BSD, the sudoers file is found in /usr/local/etc. At this point, you should use the more command to examine the contents of the sudoers file on your system.

The sudoers file recognizes seven types of user specification lists. They are usernames, group names (such as wheel on PC-BSD), aliases defined within the sudoers file itself, UID numbers, GID numbers, netgroups, and non-UNIX groups. See the following examples for applications of some of these seven specification lists.

The sudoers file is composed of two types of entries: aliases (basically variables) and user specifications that specify who may run what. When multiple entries match a user, they are applied in order. Where there are multiple matches, the last match is used (which is not necessarily the most specific match). A user specification determines which commands a user may run (and as what user) on specified hosts. By default, commands are run as root, but this can be changed on a per-command basis.

The user specifications in the sudoers file contain policy rules, one rule per line. Every rule uses the general format as follows:

```
who where = (as_whom) what
```

where:
who is the user that this rule applies to. who can also be a user specification list—for example, a group name that has been defined as shown for Solaris in Section 23.3.3.7, "Adding Group Accounts," and for PC-BSD in Section 23.3.2, "Adding/Deleting and Maintaining Users and Groups in a GUI-Based Interface on PC-BSD."
where is the hostname of the system this rule applies to.
= separates the where from (as_whom) and what.
(as_whom) designates the user specification list sudo will run the what.
what lists the full path to each command this policy rule applies to.
You must specify full pathnames to command.

Some sudoers file examples follow:
In the following rule, bob can run any command:

```
bob ALL = ALL
```

The following rule from a Solaris sudoers file allows user sarwar to run the visudo program:

```
sarwar ALL = /usr/sbin/visudo
```

The following command run on a Solaris system, uses the -l option to sudo to allow you to list the permissions currently defined as policy in the sudoers file. We see that user sarwar can run all commands as root, all commands as the user admin, and visudo as root.

```
$ sudo -l
```
