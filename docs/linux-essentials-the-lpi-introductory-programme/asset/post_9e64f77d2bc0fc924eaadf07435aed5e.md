
## 14.2.2 Specifying File Permissions—`chmod`

```
chmod [⟨options⟩] ⟨permissions⟩ ⟨name⟩ ..
```

You can give as many file or directory names as desired. The most important options include:

-   **-R** If a directory name is given, the permissions of files and directories inside this directory will also be changed (and so on all the way down the tree).

-   **--reference=⟨name⟩** Uses the access permissions of file ⟨name⟩. In this case no ⟨permissions⟩ must be given with the command.

💡 You may also specify a file's access mode “numerically” instead of “symbolically” (what we just discussed). In practice this is very common for setting all permissions of a file or directory at once, and works like this: The three permission triples are represented as a three-digit octal number—the first digit describes the owner's rights, the second those of the file's group, and the third those that apply to “others”. Each of these digits derives from the sum of the individual permissions, where read permission has value 4, write permission 2, and execute permission 1. Here are a few examples for common access modes in “`ls -l`” and octal form:

```
rwxr-xr-x    644
r-x------    400
rwxr-xr-x    755
```

💡 Using numerical access modes, you can only set all permissions at once—there is no way of setting or removing individual rights while leaving the others alone, like you can do with the “`+`” and “`-`” operators of the symbolic representation. Hence, the command

```
$ chmod 644 file
```

is equivalent to the symbolic

```
$ chmod u=rw,go=r file
```

### 14.2.3 Specifying File Owners and Groups—`chown` and `chgrp`

The `chown` command lets you set the owner and group of a file or directory. This command takes the desired owner's user name and/or group name and the file or directory name the change should apply to. It is called like

```
chown ⟨user name⟩[:⟨group name⟩] ⟨name⟩ ..
chown :⟨group name⟩ ⟨name⟩ ..
```

If both a user and group name are given, both are changed; if just a user name is given, the group remains as it was; if a user name followed by a colon is given, then the file is assigned to the user's primary group. If just a group name is given (with the colon in front), the owner remains unchanged. For example:

```
# chown joe:devel letter.txt
# chown www-data foo.html              new user www-data
# chown :devel /home/devel              new group devel
```

💡 `chown` also supports an obsolete syntax where a dot is used in place of the colon.

To “give away” files to other users or arbitrary groups you need to be **root**. The main reason for this is that normal users could otherwise annoy one another if the system uses quotas (i.e., every user can only use a certain amount of storage space).

Using the `chgrp` command, you can change a file’s group even as a normal user—as long as you own the file and are a member of the *new group*:

```
chgrp ⟨group name⟩ ⟨name⟩
```

💡 Changing a file’s owner or group does not change the access permissions for the various categories.

`chown` and `chgrp` also support the `-R` option to apply changes recursively to part of the directory hierarchy.

💡 Of course you can also change a file’s permissions, group, and owner using most of the popular file browsers (such as Konqueror or Nautilus).

# Exercises

-   **14.1 [2]** Create a new file. What is that file’s group? Use `chgrp` to assign the file to one of your secondary groups. What happens if you try to assign the file to a group that you are not a member of?

-   **14.2 [4]** Compare the mechanisms that various file browsers (like Konqueror, Nautilus, ...) offer for setting a file’s permissions, owner, group, ... Are there notable differences?

# 14.3 Process Ownership

Linux considers not only the data on a storage medium as objects that can be owned. The processes on the system have owners, too.

Many commands create a process in the system’s memory. During normal use, there are always several processes that the system protects from each other. Every process together with all data within its virtual address space is assigned to a user, its owner. This is most often the user who started the process—but processes created using administrator privileges may change their ownership, and the SUID mechanism (Section 14.4) can also have a hand in this.

The owners of processes are displayed by the `ps` program if it is invoked using the `-u` option.

```
# ps -u
USER  PID %CPU %MEM SIZE    RSS TTY STAT START TIME COMMAND
bin   89  0.0  1.0 788     328 ?   S    13:27  0:00 rpc.portmap
test1 190 0.0  2.0 1100    28  3   S    13:27  0:00 bash
test1 613 0.0  1.3 968     24  3   S    15:05  0:00 vi XF86.tex
nobody 167 0.0  1.4 932    44  ?   S    13:27  0:00 httpd
root  1   0.0  1.0 776     16  ?   S    13:27  0:03 init [3]
root  2   0.0  0.0 0       0   ?   SW   13:27  0:00 (kflushd)
```

# 14.4 Special Permissions for Executable Files

When listing files using the “`ls -l`” command, you may sometimes encounter permission sets that differ from the usual `rwx`, such as

```
-rwsr-xr-x  1 root shadow  32916 Dec 11  20:47 /usr/bin/passwd
```

What does that mean? We have to digress here for a bit:
Assume that the *passwd* program carries the usual access mode:

```
-rwxr-xr-x  1 root shadow  32916 Dec 11 20:47 /usr/bin/passwd
```

A normal (unprivileged) user, say *Joe*, wants to change his password and invokes the *passwd* program. Next, he receives the message "permission denied." What is the reason? The *passwd* process (which uses *Joe*'s privileges) tries to open the */etc/shadow* file for writing and fails, since only *root* may write to that file—this cannot be different since otherwise, everybody would be able to manipulate passwords arbitrarily and, for example, change the *root* password.

![](img/44bdd771e9c9b1353d2401c2892b2459_191_0.png)

By means of the **set-UID bit** (frequently called "SUID bit", for short) a program can be caused to run not with the invoker’s privileges but those of the file owner—here, *root*. In the case of *passwd*, the *process* executing *passwd* has write permission to */etc/shadow*, even though the invoking user, not being a system administrator, generally doesn’t. It is the responsibility of the author of the *passwd* program to ensure that no monkey business goes on, e.g., by exploiting programming errors to change arbitrary files except */etc/shadow*, or entries in */etc/shadow* except the password field for the invoking user. On Linux, by the way, the set-UID mechanism works only for binary programs, not shell or other interpreter scripts.

![](img/44bdd771e9c9b1353d2401c2892b2459_191_1.png)

> Bell Labs used to hold a patent on the SUID mechanism, which was invented by Dennis Ritchie [SUID]. Originally, AT&T distributed Unix with the caveat that license fees would be levied after the patent had been granted; however, due to the logistical difficulties of charging hundreds of Unix installations small amounts of money retroactively, the patent was released into the public domain.

![](img/44bdd771e9c9b1353d2401c2892b2459_191_2.png)

By analogy to the set-UID bit there is a **SGID bit**, which causes a process to be executed with the program file’s group and the corresponding privileges (usually to access other files assigned to that group) rather than the invoker’s group setting.

![](img/44bdd771e9c9b1353d2401c2892b2459_191_3.png)

The SUID and SGID modes, like all other access modes, can be changed using the *chmod* program, by giving symbolic permissions such as *u+s* (sets the SUID bit) or *g-s* (deletes the SGID bit). You can also set these bits in octal access modes by adding a fourth digit at the very left: The SUID bit has the value 4, the SGID bit the value 2—thus you can assign the access mode 4755 to a file to make it readable and executable to all users (the owner may also write to it) and to set the SUID bit.

![](img/44bdd771e9c9b1353d2401c2892b2459_191_4.png)

You can recognise set-UID and set-GID programs in the output of “*ls -l* ” by the symbolic abbreviations “*s*” in place of “*x*” for executable files.

# 14.5 Special Permissions for Directories

There is another exception from the principle of assigning file ownership according to the identity of its creator: a directory’s owner can decree that files created in that directory should belong to the same group as the directory itself. This can be specified by setting the SGID bit on the directory. (As directories cannot be executed, the SGID bit is available to be used for such things.)

![](img/44bdd771e9c9b1353d2401c2892b2459_191_5.png)

A directory’s access permissions are not changed via the SGID bit. To create a file in such a directory, a user must have write permission in the category (*owner*, *group*, *others*) that applies to him. If, for example, a user is neither the owner of a directory nor a member of the directory’s *group*, the directory must be writable for “*others*” for him to be able to create files there. A file created in a SGID directory then belongs to that directory’s *group*, even if the user is not a member of that group at all.

![](img/44bdd771e9c9b1353d2401c2892b2459_191_6.png)

> The typical application for the SGID bit on a directory is a directory that is used as file storage for a “project group”. (Only) the members of the project group are supposed to be able to read and write all files in the directory, and
