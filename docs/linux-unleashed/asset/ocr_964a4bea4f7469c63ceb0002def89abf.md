position, and permission to execute is shown by an x in the third position. If a particular permission is absent, its space is filled by -. 

In the case of myfile, the owner has rw-, which means read and write permissions. This file cannot be executed by typing myfile at the Linux prompt since there is no execute permission. The group permissions are r--, which means that members of the group users can read the file but cannot change it or execute it. Likewise, the permissions for all others are r--, or read-only.

# # UMASK Settings

When you create a file (such as with redirection), how does Linux know which file permissions to assign? The answer is that a variable called the UMASK (user file creation mask) contains the instructions for every file you create. The system administrator can set the UMASK setting for any user or for the entire set of users on the whole system. You can change your own UMASK setting, but not that of others (unless you are logged in as root).

The value of UMASK can be shown at any time by typing the command umask (lower-case to distinguish it from the environment variable UMASK) at the shell prompt:

```
$ umask
022
```

You may have four numbers instead of three, but the first one doesn't mean anything so simply ignore it. What do the numbers mean? They are a set of octal numbers which indicate the user, group, and other permissions. The valid set of numbers in the umask command are shown in Table 9.1.

# **TABLE 9.1. OCTAL VALUES USED BY UMASK AND THEIR MEANINGS.**

| Octal number | Permissions granted |
| :--- | :--- |
| 0 | Read and write (and execute for directories) |
| 1 | Read and write |
| 2 | Read (and execute for directories) |
| 3 | Read |
| 4 | Write (and execute for directories) |
| 5 | Write |
| 6 | Execute for directories only |
| 7 | No permissions |