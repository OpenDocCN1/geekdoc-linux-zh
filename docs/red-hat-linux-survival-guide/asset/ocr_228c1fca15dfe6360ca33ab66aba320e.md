| Octal Number | What It Represents |
|---|---|
| 3, 5, 6, 7 | Combinations of permissions. For example, the number 3 grants executable plus write permissions (1 + 2), 5 grants execute and read permissions (1 + 4), 6 grants read and write permissions (4 + 2), and 7 grants read, write, and executable permissions (4 + 2 + 1). |

Octal permission values are based on numbers containing four octal digits. Figure 8-1 shows how you can visualize the permissions as four octal digits. Here, the first octal digit is the leftmost or most significant one.

![](bbox=[0.1, 0.55, 0.9, 0.75])

Figure 8-1 A permission diagram using four octal digits.

As Figure 8-1 demonstrates, the first octal digit is used for setting special permissions, the second digit is used for setting permissions for the file owner, the third digit is used for setting permissions for the group, and the fourth digit is used for setting permissions for everyone else. Owner and group permissions are discussed in earlier sections of this chapter, and “everyone else” just means everyone other than the file’s group or owner. Special permissions are a little strange, though; choosing special permissions involves deciding whether the set-UID, set-GID, or sticky bit is necessary. Each of these concepts is explained in the following list.

+   - **set-UID (set user ID):** When an executable file with set-UID permission is run, the process runs as the file owner. In other words, if a file is set-UID and owned by the user gunchy, any time it is run, the running program enjoys the privileges of the user gunchy. So, if a file is owned by root, and is also set to be set-UID, anyone who can run the file essentially has the privileges of the superuser.