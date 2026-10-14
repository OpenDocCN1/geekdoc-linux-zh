
To better understand the nature of groups, suppose you have created a new user account called “chrislee.” Because your system employs User Private Groups, the primary group for this user is the group named chrislee. User chrislee is also assigned to the following groups: projectleads, salesteam, and hrcommittee. (See Figure 4-2.) Now suppose you want to give all members of the sales team access to a particular directory or group of files. You can just make salesteam the group assigned to the directory or files and grant group permissions according to the access that group members should have.

![](img/43f64015de86d989e30eff5bb284fb96_186_0.png)

Figure 4-2 A user as a member of multiple groups

## User and Group Files

User account information is stored in the file /etc/passwd. In earlier releases of Linux, password information for each user was also stored in this file, hence the file’s name. Because of security problems in the past, password information is no longer stored in this file. Other information about each user is contained in the file, however. A sample /etc/passwd file from a new Red Hat Linux installation is shown on the next page, followed by a description of each of the file’s colon-separated fields.

> NOTE
> The exact list of users created on a new Linux system depends on which version of Linux you are using and which features you have selected to install or activate.

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
news:x:9:13:news:/var/spool/news:
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/sbin/nologin
vcsa:x:69:69:virtual console memory owner:/dev:/sbin/nologin
mailnull:x:47:47:/var/spool/mqueue:/dev/null
rpm:x:37:37::/var/lib/rpm:/bin/bash
ntp:x:38:38::/etc/ntp:/sbin/nologin
rpc:x:32:32:Portmapper RPC user::/sbin/nologin
xfs:x:43:43:X Font Server:/etc/X11/fs:/bin/false
gdm:x:42:42::/var/gdm:/sbin/nologin
rpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologin
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
nscd:x:28:28:NSCD Daemon::/bin/false
ident:x:98:98:pident user::/sbin/nologin
radvd:x:75:75:radvd user::/bin/false
apache:x:48:48:Apache:/var/www:/bin/false
squid:x:23:23::/var/spool/squid:/dev/null
johnl:x:500:500:John Lim:/home/johnl:/bin/bash
```

The following list describes the fields in each line of the output above. The last line of the file (the user johnl) is a regular user account that is used as an example.

- User account name (johnl): The name used by a person to log in to Linux. This field cannot contain uppercase letters or spaces.
- Password (x): The encrypted password for each user was formerly stored in this field. An x in this field indicates that the Shadow Password Suite is in use, in which case the encrypted password is stored in /etc/shadow. You will learn more about shadow passwords later in this section.
- User ID number, or UID (the first 500): A number from 0 to 65,535 that uniquely identifies this user on this Linux system. The number is arbitrary and normally is automatically assigned by the utility used to create a new user account. Numbers from 0 to 100 are reserved for special system uses (root always has a UID of 0). New regular user accounts commonly start with 500.
- Group ID number, or GID (the second 500): A number from 0 to 65,535 that uniquely identifies the primary group for this user account. The GID must correspond to a group defined in the /etc/group file (described shortly).
- The user's real name (John Lim): A complete name for the user. In the documentation, this is formally called the comment field. Spaces are permitted in this field. If the user account was created for a certain role in the organization, other text can be placed here instead, such as "Database Administrator."
- Home directory (/home/johnl): The location in the Linux file system that is used as the current working directory when the user first logs in. Whenever the user uses a tilde (~) on the command line, this directory is used. (For example, cd ~ changes your current directory to your home directory.)
- Default shell (/bin/bash): The program that runs automatically when the user logs in. The default setting for this field is /bin/bash, which runs the bash shell. If a user prefers a different shell (such as the Korn shell or C shell), this field can be changed to accommodate that. This field can also be used to start a nonshell program to restrict the user's actions.

Although you can edit the /etc/passwd file directly in a text editor, this is not a good idea if more than one system administrator might be working on the file over the network. In addition, small typing errors can make one or more user accounts inaccessible. Instead of a text editor, use the programs described in the following sections to update /etc/passwd. If you need to use a text editor to correct a problem in the file, use the special editing command vipw.

Groups on a Linux system are defined in the /etc/group file. You can edit this file if necessary using the command vigr. A part of the file in Red Hat Linux is shown here, with the fields in the file (again separated by colons on each line) described in the following list.

```
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,adm,daemon
tty:x:5
disk:x:6:root
lp:x:7:daemon,lp
...
ident:x:98:
radvd:x:75:
apache:x:48:
squid:x:23:
wine:x:66:
nwells:x:500:
rsolomon:x:501:
authors:x:502:rsolomon,nwells
```

- The name of the group: This field cannot contain uppercase letters or spaces. As with user names, shorter is often better; avoid names more than 10 or 12 letters long.
- Group password: This field is either blank or contains *x* (meaning the password is stored in another location). Group passwords allow a person who knows that group's password to temporarily assume that group's access rights using the *newgrp* command; this feature is rarely used.
- Group ID (GID) number: This number uniquely identifies the group. Group numbers are automatically assigned when you create a new group, though you can specify a number if you prefer.
- Members of the group: This field identifies members of the group. Note in the sample file that many groups do not have member users defined. A program may be able to assume the permissions of the group using system calls (programming instructions), but no user is part of the group by virtue of logging in. Some of the groups (such as sys and adm) have a comma-separated list of users as the last field. In addition to the two User Private Group items (for nwells and rsolomon in this sample file), a group named authors has been added to this default installation.

![](img/43f64015de86d989e30eff5bb284fb96_189_0.png)

> Some UNIX systems employ a special group called wheel, which has special administrative powers; it is essentially a reduced version of the root account. On some systems a user must be a member of the wheel group in order to use the su command to change to the root account permissions. Although Linux includes a wheel group by default (with root as the only member), no special features or privileges apply to the wheel group in Linux.

## Shadow Passwords

All programs and users may need to access the list of users stored in /etc/passwd. Each user's password used to be stored in this file as well, in an encrypted form. But if everyone could read the user names in the file, then everyone could also read the encrypted passwords. Having these passwords, even in this encrypted form, was a serious security breach that might have permitted unauthorized use of an account.

To protect against this problem, encrypted passwords are rarely stored in the /etc/passwd file. Instead, they are commonly stored in a file called /etc/shadow. Systems that use this file rely on the Shadow Password Suite, a collection of password-related programs that have been modified to recognize the /etc/shadow file. This file can only be read by the root user and certain utilities such as the login program.
