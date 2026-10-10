What does that mean? We have to digress here for a bit:  
Assume that the *passwd* program carries the usual access mode:

```
-rwkr-xr-x  1 root shadow  32916 Dec 11 20:47 /usr/bin/passwd
```

A normal (unprivileged) user, say *Joe*, wants to change his password and invokes the *passwd* program. Next, he receives the message "permission denied." What is the reason? The *passwd* process (which uses *Joe*'s privileges) tries to open the */etc/shadow* file for writing and fails, since only *root* may write to that file—this cannot be different since otherwise, everybody would be able to manipulate passwords arbitrarily and, for example, change the *root* password.

![](bbox=[0.24, 0.2, 0.29, 0.23])

By means of the **set-UID bit** (frequently called "SUID bit", for short) a program can be caused to run not with the invoker’s privileges but those of the file owner—here, *root*. In the case of *passwd*, the *process* executing *passwd* has write permission to */etc/shadow*, even though the invoking user, not being a system administrator, generally doesn’t. It is the responsibility of the author of the *passwd* program to ensure that no monkey business goes on, e.g., by exploiting programming errors to change arbitrary files except */etc/shadow*, or entries in */etc/shadow* except the password field for the invoking user. On Linux, by the way, the set-UID mechanism works only for binary programs, not shell or other interpreter scripts.

![](bbox=[0.3, 0.33, 0.34, 0.35])

> Bell Labs used to hold a patent on the SUID mechanism, which was invented by Dennis Ritchie [SUID]. Originally, AT&T distributed Unix with the caveat that license fees would be levied after the patent had been granted; however, due to the logistical difficulties of charging hundreds of Unix installa-tions small amounts of money retroactively, the patent was released into the public domain.

![](bbox=[0.24, 0.45, 0.29, 0.47])

By analogy to the set-UID bit there is a **SGID bit**, which causes a process to be executed with the program file’s group and the corresponding privileges (usually to access other files assigned to that group) rather than the invoker’s group setting.

![](bbox=[0.22, 0.5, 0.29, 0.53])

The SUID and SGID modes, like all other access modes, can be changed using the *chmod* program, by giving symbolic permissions such as *u+s* (sets the SUID bit) or *g-s* (deletes the SGID bit). You can also set these bits in octal access modes by adding a fourth digit at the very left: The SUID bit has the value 4, the SGID bit the value 2—thus you can assign the access mode 4755 to a file to make it readable and executable to all users (the owner may also write to it) and to set the SUID bit.

![](bbox=[0.25, 0.58, 0.29, 0.6])

You can recognise set-UID and set-GID programs in the output of “*ls -l* ” by the symbolic abbreviations “*s*” in place of “*x*” for executable files.

# 14.5  Special Permissions for Directories

There is another exception from the principle of assigning file ownership according to the identity of its creator: a directory’s owner can decree that files created in that directory should belong to the same group as the directory itself. This can be specified by setting the SGID bit on the directory. (As directories cannot be executed, the SGID bit is available to be used for such things.)

![](bbox=[0.18, 0.7, 0.29, 0.72])

A directory’s access permissions are not changed via the SGID bit. To create a file in such a directory, a user must have write permission in the category (*owner*, *group*, *others*) that applies to him. If, for example, a user is neither the owner of a directory nor a member of the directory’s *group*, the directory must be writable for “*others*” for him to be able to create files there. A file created in a SGID directory then belongs to that directory’s *group*, even if the user is not a member of that group at all.

![](bbox=[0.3, 0.87, 0.34, 0.89])

> The typical application for the SGID bit on a directory is a directory that is used as file storage for a “project group”. (Only) the members of the project group are supposed to be able to read and write all files in the directory, and