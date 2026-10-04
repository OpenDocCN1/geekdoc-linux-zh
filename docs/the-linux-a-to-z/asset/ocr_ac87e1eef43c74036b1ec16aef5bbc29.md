# Table 1.1 The main directory list

| Path | Description |
|---|---|
| /bin | Binary executable commands |
| /dev | Device special files |
| /etc | System admin. and config. files |
| /home | Base for user home directories |
| /lib | Standard programming libraries |
| /sbin | System admin. commands |
| /tmp | General store for temporary files |
| /usr/X11 | X windows system files |
| /usr/adm | System admin. data files |
| /usr/bin | More executable commands |
| /usr/lib | Libraries and package config. files |
| /usr/local/bin | Locally added commands |
| /usr/local/lib | Locally added libraries |
| /usr/local/src | Local command source files |
| /usr/man | System online manual pages |
| /usr/src/linux | Linux kernel source files |
| /var | Overflow for some large files |

all the users and which shell program they will use when they login. The password file is also responsible for holding user passwords, giving a system identity number to each user and for placing sets of users into groups if they need to co-operate on joint project work.

The password file itself is just an ordinary text file which any user is allowed to read. It is stored in:

```
/etc/passwd
```

The contents of this file can be listed most simply by typing the command line:

```
$ cat /etc/passwd
```

The cat command is just being used to list the file contents here. Its full use will be covered in the next chapter (Section 2.3).

Each separate line in the password file is a record of information about a single user login name. Each record in the file is divided up into seven fields with colons (:) between them. The records have the format:

```
name:password:uid:gid:comment:home:shell
```

From left to right, the seven fields are used as follows:

**name** This field contains the users login name. It appears exactly as the user must type it to login.