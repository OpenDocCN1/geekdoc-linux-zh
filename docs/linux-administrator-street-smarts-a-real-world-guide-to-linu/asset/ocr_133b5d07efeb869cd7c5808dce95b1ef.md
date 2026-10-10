file's main owner. This is effectively the same as the `chgrp` command, which works much like `chown` but accepts a group name alone (without a dot or colon). If you omit the colon or dot and the group name, `chown` changes only the primary owner of the file or directory.

The `chown` command has several options; consult its man page for details. One of the most useful options, though, is `-R`, which performs a recursive change to a directory and all the files and subdirectories it contains:

```
# chown -R fred:users /home/project7
```

# ## Setting File and Directory Permissions

Earlier, in “Verifying the Presence of a File” in Task 1.1, I described the long form of the `ls` command (`ls -l`), which shows additional information on a file. Specifically, the output looks like this:

```
$ ls -l /usr/bin/whatis 
-rwxr-xr-x  1 root root 2409 Nov 19  2004 /usr/bin/whatis
```

The columns in this output are the permissions, the number of links to the file (described in the next task), the owner, the group, the file size in bytes, the file creation date, and the file-name. The permissions string can be perplexing at first. It consists of 10 characters. The first of these characters is a code for the file type. A dash (-) denotes a normal file, while various characters stand for special file types. Most important, `d` refers to a directory and `l` refers to a symbolic link. Other codes include `c` and `b` for character and block devices, respectively (used to access hardware via device files in /dev/).

The remaining nine characters in the permissions string represent permissions for the file's owner, group, and all other users (aka *world* permissions). Each of these three classes of users consumes three characters, which denote the presence or absence of read, write, and execute permissions. If an `r`, `w`, or `x` character is present in the respective position, the class has the relevant permission; if a dash is present, the class lacks that type of permission. Table 1.1 summarizes some possible permissions and their uses; however, as there are 512 possible permissions, Table 1.1 is incomplete. (Most of the 512 possible permissions are bizarre, though; Table 1.1 contains the most common permissions in practice.) Note that the leading character is sometimes omitted from the permission string, as it’s not really part of the permissions *per se*. Read and write permissions are fairly self-explanatory. Execute permission identifies executable files—that is, program files. Note that you can remove execute permission for some users to ensure that a program may only be run by certain users (such as the program’s owner).

**Table 1.1** Example Permissions and Their Likely Uses
| Permission String | Octal Code | Meaning | 
| :--- | :--- | :--- |
| `rwxrwxrwx` | 777 | Read, write, and execute permissions for all users. |
| `rwxr-xr-x` | 755 | Read and execute permission for all users. The file's owner also has write permission. |