# JUST A MINUTE

> On many System V-based systems, the output of ls -l always shows user and group. The -g flag actually turns off this display!

Both owners and groups vary for each of the files and directories in this small listing. Notice that files can have different owners while having the same group. (There are two examples here: sh145 and the shakes directory, and snd.17 and so12.)

+   2. Directories that have a wide variety of owners are the directories above your own home directory and the tmp directory, as you can see in instruction 1. Examine both on your system and identify the owner and group of all files. For in the same group you are in (with the id command, can find which group or groups you are) not owned by you, you'll need to check which of the three permission values to identify your access privileges

# SUMMARY

Files and directories have both owners and groups, although the group is ultimately less than the owner, particularly where permissions and access are involved.

# Task 5.8: Change the Owner of a File or Directory

# DESCRIPTION

Now that you can ascertain the ownership of a file or directory, it's time to learn about the chown command. This command lets you change the ownership of whatever you specify.

# CAUTION

> Before you go any further, however, a stern warning: once you've changed the ownership of a file, you cannot restore it to yourself. The owner of a file can give away its ownership, so don't use the chown command unless you're absolutely positive you want to!

# ACTION

+   1. The format for changing the ownership of a file is to specify the new owner and list the files or directory you are giving away:

```
% ls -l test
-rw-rw-rw- 1 taylor 0 Oct 12 15:17 mytest
% chown root test
% ls -l test
-rw-r--r-- 1 root 0 Oct 12 15:17 mytest
```

This would change the ownership of the file test from me to the user root on the system.