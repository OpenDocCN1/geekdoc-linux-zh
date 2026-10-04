In addition any combination of the following flag values may also be included using the bitwise-OR (|) operator:

+   - `O_CREAT` open the file and create it if it doesn’t exist;
- `O_EXCL` force open() to fail if O_CREAT is set and file exists;
- `O_TRUNC` truncate the file to zero length on open();
- `O_APPEND` force write()s to occur on the end of the file.

There are some other flags which can be specified but they are of no use on ordinary files so we’ll cover them later when they are more relevant. The symbolic names for all these flag values can be accessed via a #include <fcntl.h>.

If you use open() to create a file, then the mode parameter is used to specify the access permission bits for the file’s owner, the file’s group and all other system users. The required combination of the following symbolic constants (defined through <sys/stat.h>) should be created with the bitwise-OR operator:

+   - `S_IRUSR` read permission bit for file’s owner;
- `S_IWUSR` write permission bit for file’s owner;
- `S_IXUSR` execute permission bit for file’s owner;
- `S_IRGRP` read permission bit for file’s group;
- `S_IWGRP` write permission bit for file’s group;
- `S_IXGRP` execute permission bit for file’s group;
- `S_IROTH` read permission bit for other file users;
- `S_IWOTH` write permission bit for other file users;
- `S_IXOTH` execute permission bit for other file users.

Three useful bitwise-OR combinations are already defined as follows:

+   - `S_IRWXU` defined as (S_IRUSR | S_IWUSR | S_IXUSR)
- `S_IRWXG` defined as (S_IRGRP | S_IWGRP | S_IXGRP)
- `S_IRWXO` defined as (S_IROTH | S_IWOTH | S_IXOTH)

In addition, it is also possible to specify that the set-uid bit and/or the set-gid bit should be set as well using the constant values:

+   - `S_ISUID` set the set-uid bit;
- `S_ISGID` set the set-gid bit.

Don’t forget, when a process creates a file on your behalf, the permission bits are modified by the value of the umask associated with the process. The process effectively uses the formula:

```
mode & (~umask)
```

to determine the permissions with which the file will actually be created. This means that you should not be surprised if the permission bits you get on a file created by one of your programs do not match the mode flags you requested in the open() call. We’ll look at how to do something about the umask value (in Section 21.1) if this security feature becomes a problem.

Examples of calls to open() using a range of parameter values might be: