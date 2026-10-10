# Managing Groups

Groups can make managing users a lot easier. Instead of having to assign individual permissions to every user, you can use groups to grant or revoke permissions to a large number of users quickly and easily. Setting group permissions allows you to set up workspaces for collaborative working and also to control what devices can be used, such as external drives or DVD writers. This approach also represents a secure method of limiting access to system resources to only those users who need them. As an example, the sysadmin could put the users andrew, paul, scott, derek, mark, and vanessa in a new group named unleashed. Those users could each create files intended for their group work and chgrp those files to unleashed.

Now, everyone in the unleashed group—but no one else except root—can work with those files. The sysadmin would probably create a directory owned by that group so its members could have an easily accessed place to store those files. The sysadmin could also add other users such as bernie and lido to the group and remove existing users when their part of the work is done. The sysadmin could make the user andrew the group administrator so that andrew could decide how group membership should be changed. You could also put restrictions on the DVD writer so that only andrew could burn DVDs, thus protecting sensitive material from falling into the wrong hands.

Different UNIX operating systems implement the group concept in various ways. Fedora uses a scheme called UPG, the user private group, in which all users are assigned to a group with their own name by default. (The user's username and group name are identical.) All the groups are listed in `/etc/group` file. Here is a partial list of a sample `/etc/group` file:

```
# cat /etc/group
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,adm,daemon


dovecot:x:97:

...

postdrop:x:90:
postfix:x:89:
andrew:x:500:
```

In this example, there are a number of groups, mostly for services (mail, ssh, and so on) and devices (CD-ROM, disk, and so on). As previously mentioned, the system services groups enable those services to have ownership and control of their files. For example, adding postfix to the mail group, as shown previously, enables the postfix application to access mail's files in the manner that mail would decide for group access to its file. Adding a regular user to a device's group permits the regular user to use the device with permissions granted by the group owner. Adding user andrew to the group cdrom, for