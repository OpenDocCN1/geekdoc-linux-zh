# Managing Groups

By far, the easiest method to add groups to a system is to edit the /etc/group file using a text editor. Another method is to use the groupadd command. To add a group called group1 to the system and assign it a GID of 492, you can use the following command:

```
[root@server1 root]# groupadd -g 492 group1
[root@server1 root]# _
```

Then, you can use the -G option to the usermod command to add members to the group. To add the user mary to this group and view the addition, you can use the following usermod command:

```
[root@server1 root]# usermod -G group1 mary
[root@server1 root]# tail -1 /etc/group
group1:x:492:mary
[root@server1 root]# _
```

There also exists a groupmod command that can be used to modify the group name and GID, as well as a groupdel command, which can be used to remove groups from the system.

To see a list of groups of which you are a member, simply run the groups command; to see the GIDs for each group, simply run the id command. The primary group is always listed first by each command. The following output shows the output of these commands when executed by the root user:

```
[root@server1 root]# groups
root bin daemon sys adm disk wheel
[root@server1 root]# id
uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel)
[root@server1 root]# _
```

You can see from the preceding output that the primary group for the root user is the root group. This group is attached as the group owner for all files that are created by the root user, as shown in the following output:

```
[root@server1 root]# touch samplefile1
[root@server1 root]# ls -1 samplefile1
-rw-r--r--    1 root     root       0 Jul 17 19:22 samplefile1
[root@server1 root]# _
```

To change the primary group temporarily to another group that is listed in the output of the groups and id commands, you can use the newgrp command. Any new files created afterward will then have the new group owner. The following output demonstrates how changing the primary group for the root user affects file ownership:

```
[root@server1 root]# newgrp sys
[root@server1 root]# id
uid=0(root)  gid=3(sys)
```