```
chgrpmem -m $file sales
done
```

| Table 12.4 | User Account Files in AIX |  |
|---|---|---|
| File | Information stored |  |
| /etc/passwd | User information |  |
| /etc/security/user | Extended attributes by user |  |
| /etc/security/limits | Process resource limits by user |  |
| /etc/security/environ | Environment attributes by user |  |
| /etc/group | Group names, numbers, and lists |  |
| /etc/security/group | Extended attributes of groups |  |

It should be noted that this simple script will work for other flavors of UNIX. Just replace chgrpmem with the appropriate group attribute change command, and you're on your way.

> Solaris provides the commands useradd, usermod, and userdel, which perform similar functions as the AIX commands described in this section. Most UNIX flavors have non-GUI commands for account management.

passwd or pwdadm—Sets the user password.

| Table 12.5 | AIX Group Commands |  |
|---|---|---|
| Command | Definition |  |
| mkgroup | Creates a new group |  |
| chgroup | Changes attributes for groups |  |
| lsgroup | Displays group attributes |  |
| chgrpmem | Changes administrators or members of a group |  |
| setgroups | Resets a session's process group set |  |
| newgrp | Changes a user's real GID |  |