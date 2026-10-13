/etc/gshadow. Before we look at that, however, just observe that the first group—root—is group ID=0, and has one member: account root. The second, group bin, has three members, adm has four, and so on.

3. A user can be moved from one default group to another by changing the number associated with his default group in the /etc/passwd file, as you might expect.

Adding a user to additional groups is most efficiently done by editing the group file itself. On Linux, there's a simple tool vigr (vi group) that enables you to safely edit the /etc/group file without worrying about another sysadmin making changes underfoot. Otherwise, you can directly edit the file with the editor of your choice and if you're the only admin, you should be safe.

To demonstrate, I'm going to add user taylor to the administrative group wheel by simply appending the login ID taylor to the line.

Before the change, wheel looks like this:

```
# grep wheel /etc/group
wheel:x:10:root
```

and after the change:

```
# grep wheel /etc/group
wheel:x:10:root,taylor
```

Now, when user taylor logs in, the id command reports something slightly different:

```
$ id
uid=502(taylor) gid=502(coders) groups=502(coders),4(adm),10(wheel)
```

Voila! Now taylor is a member of three groups.

![](bbox=[0.22, 0.71, 0.3, 0.8])

> The wheel group is an interesting one: On most Unices, only users who are part of the group wheel can use the su command to switch user accounts without logging out.

Users can temporarily join a group with the newgrp command, though they'll need to know the group password if one has been set. (Groups have random, impossible-to-guess passwords by default, by the way.)

A good philosophy to follow is to create mnemonic groups for the teams in your organization, and add and delete members of the group to reflect the current membership. Then, the group members are free to create directories and allow limited access to programs and files without worries about unauthorized access.