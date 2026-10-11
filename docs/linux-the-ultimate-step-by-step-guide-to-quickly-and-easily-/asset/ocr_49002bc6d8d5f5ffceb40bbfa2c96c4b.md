cache.

| /var/cache/man/index.<br>(bt|db|dir|pag) | An FHS compliant<br>global index<br>database cache. |

# Examples

```
man man
```

View the man page for the man command.

```
man -nh -nj man
```

# Chapter Seven: LINUX DIRECTORY COMMAND

Linux or UNIX-like systems use the ls command to list files and directories. However, ls does not have an option to list only directories. You can use combination of ls and grep to list directory names only. You can use the find command too. In this quick tutorial, you will learn how to list only directories in Linux or UNIX.

List all directories in Unix

Type the following command:

```
$ ls -l | grep `^d*`<br>ls -l | egrep `^d*`
```

Try the following ls command to list directories in the current directory:

```
$ ls -d */
```

![](bbox=[0.065, 0.705, 0.59, 0.92])

sample outputs