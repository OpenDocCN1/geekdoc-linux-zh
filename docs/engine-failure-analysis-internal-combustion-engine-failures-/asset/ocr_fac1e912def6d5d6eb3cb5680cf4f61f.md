# EXAMPLES (CONT.)

| This Command | Does the Following |
| :--- | :--- |
| `chmod u=rw,go=r info.txt` | Sets the permissions of the specified file (info.txt) so that the file owner (user) may read and write, but group owners and others are restricted to reading the file. |
| `chmod a=rw *.doc` | Sets the permissions of all the files that conform to the specified shell pattern (see Chapter 4) so that all users may read and write to the file. |
| `chmod -R u+rw *` | Increases the permissions of all files in the specified directory and, if necessary, in all of its associated subdirectories so that the user has both read and write privileges. |
| `chmod u+s ballistic` | Adds the set user ID special permission to the specified executable (ballistic). |
| `chmod u-s ballistic` | Removes the set user ID special permission from the specified executable (ballistic). |
| `chmod o+t ballistic` | Saves a copy of the program on the swap device so that it loads more quickly. |

# chown

```
`chown [ option | user [.group] ] file`
```

Change the ownership of the specified file to the specified user. To change the group ownership, type a period after the user name and type the group name or ID with no intervening spaces. To specify owners or groups, you can supply user or group names or ID numbers. This command requires superuser status (see su in Chapter 1).

See also chgrp.