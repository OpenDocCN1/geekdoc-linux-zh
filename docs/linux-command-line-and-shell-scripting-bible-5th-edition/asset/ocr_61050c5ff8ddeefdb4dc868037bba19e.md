# TABLE 7.6  **The chmod SUID, SGID, and Sticky Bit Octal Values**

| Binary | Octal | Description |
| :--- | :---: | :--- |
| 000 | 0 | All bits are cleared. |
| 001 | 1 | The sticky bit is set. |
| 010 | 2 | The SGID bit is set. |
| 011 | 3 | The SGID and sticky bits are set. |
| 100 | 4 | The SUID bit is set. |
| 101 | 5 | The SUID and sticky bits are set. |
| 110 | 6 | The SUID and SGID bits are set. |
| 111 | 7 | All bits are set. |

So, to create a shared directory that always sets the directory group for all new files, all you need to do is set the SGID bit for the directory:

```
$ mkdir testdir
$ ls -1
drwxrwxr-x   2 rich     rich      4096 Sep 20 23:12 testdir/
$ chgrp shared testdir
$ chmod g+s testdir
$ ls -1
drwxrswr-x   2 rich     shared    4096 Sep 20 23:12 testdir/
$ umask 002
$ cd testdir
$ touch testfile
$ ls -1
total 0
-rw-rw-r--   1 rich     shared          0 Sep 20 23:13 testfile
$
```

The first step is to create a directory that you want to share using the `mkdir` command. Next, you use the `chgrp` command to change the default group for the directory to a group that contains the members who need to share files. Finally, you set the SGID bit for the directory to ensure that any files created in the directory use the shared group name as the default group.

For this environment to work properly, all of the group members need to have their `umask` values set to make files writable by group members. In the preceding example, the `umask` is changed to `002` so that the files are writable by the group.

After all that’s done, any member of the group can go to the shared directory and create a new file. As expected, the new file uses the default group of the directory, not the user account’s default group. Now any user in the shared group can access this file.