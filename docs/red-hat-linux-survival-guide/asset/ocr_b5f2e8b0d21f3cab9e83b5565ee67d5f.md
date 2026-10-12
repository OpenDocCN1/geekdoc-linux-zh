is accessible only by the new user. The user has to change the file permissions explicitly to allow someone else to see the file.

However, if your user account philosophy clashes with this kind of private group idea, you can override it by using the -g group option (where group is the name of your group). For example, the following command forces useradd to create the user kabir with the default group set to the users group:

```
useradd kabir -g users
```

![](bbox=[0.08, 0.46, 0.2, 0.55])

> You can use the groups username command to find out which user belongs to what group.

If you want to make the new user a member of additional groups on your system, use the -G comma-separated list of groups option. For example, the following command adds the user kabir to the wheel and admins groups in the /etc/group file:

```
useradd kabir -G wheel,admins
```

# Creating a new group

To create a new group, use the groupadd command. For example, the following command adds a new group called mygroup in the /etc/group file (and in the /etc/gshadow file if you are using shadow passwords):

```
groupadd mygroup
```

By default, the groupadd program creates the group with a GID above 499, because 0 through 499 are (sort of) reserved for system-level accounts such as root, bin, and mail. So if your /etc/group file has the last group GID set to 511, the new group you create with this program will have a GID of 512, and so on. If you want to set the GID of your new group specifically, use the -g GID option. Also, if you want to create a group with a GID in the 0 to 499 range, use the -r option with the -g GID option to force groupadd to create the new group as a system group. Note that if the group or GID you are trying to use with the program is already in use in /etc/group, you will get an error message and the command will fail.