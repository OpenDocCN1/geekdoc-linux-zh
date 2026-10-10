program to match that of the file, thus transferring permissions of the file to the directory. This gives the program user permissions that he or she does not normally have. The set-GID works in a similar fashion, but is used to transfer a user's permissions to the program. The set-GID bit is set to 2000. When this bit is on in a similar fashion, but is used to transfer a user's permissions to the program. The set-GID bit is set to 2000. When this bit is on in a similar fashion, but is used to transfer a user's permissions to the program. The set-GID bit is set to 2000. When this bit is on in a similar fashion, but is used to transfer a user's permissions to the program. The set-GID bit is set to 2000. When this bit is on in a similar fashion, but is used to transfer a user's permissions to the program. The set-GID bit is set to 2000. When this bit is on in a similar fashion, but is used to transfer a user's permissions to the program. The set-GID bit is set to 2000. When this bit is on in a similar fashion, but is used to transfer a user's permissions to the program. The set-GID bit is set to 2000. When this bit is on in a similar fashion, but is used to transfer a user's permissions to the program. The set-GID bit is set to 2000. When this bit is on in a similar fashion, but is used to transfer a user's permissions to the program.

The sticky, setUID, and setGID switches can be set from the `chmod` command. They respectively require 1000, 2000, and 4000 to be added to the number. The other bits will be switched off if you do not add the appropriate values to the `chmod` command, as they will all be set to zero. If we take the earlier `chmod` example and modify it to set the sticky bit as well, this command would result:

```
chmod 1640 textdoc
```

Again, it is much easier to use the Permissions window of KFM, which makes it easy to see the current settings as well as making it easier to alter settings. Of course, whether you use KFM or the command line to alter permissions settings, it is only possible if you have the authority to do so. Without this authority, you can see the KFM Permissions window if you can get into the directory containing the file, but no changes can be made.

# Adding a group

If you wish to change the user group for a file, this can be accomplished using the KFM Permissions window. The bottom section of the window shows the group ID of the current window and has a menu of installed groups to choose from. If you need to assign a file to a new group, the group must be added first. Since it can be generated from the KFM Permissions window, a group can be added to the command line using the `newgroup` command. Suppose you wish to add a group called “newgroup.” This command could be used:

```
groupadd -g 1000 newgroup
```

You have to supply a group ID number that the system is not already using, but you should use a fairly high number. If you use a number in the range 1000 to 6000, there should be no problem. The maximum permissible number is 65535, but any number from 600 to 6000 should do. The maximum permissible number is 65535, but any number from 600 to 6000 should do. The maximum permissible number is 65535, but any number from 600 to 6000 should do. The maximum permissible number is 65535, but any number from 600 to 6000 should do. The maximum permissible number is 65535, but any number from 600 to 6000 should do. The maximum permissible number is 65535, but any number from 600 to 6000 should do.

Having made a new group, it can be assigned to one or more users before it can be used. It can be made a default group for a user to assign to the “Permissions window, because group “Fred” and “users” possible” will be listed. You can check a user belongs to the `groups` command at the command line. Using this command would check which groups “Fred” belongs to:

```
groups Fred
This would return this answer:

Fred : Fred users
```

“Fred” is the primary group for “Fred.” the user, and “users” is the only secondary group. Suppose we wished to remove “users” and assign “Fred” to “newgroup” instead.

These two commands would do the job:
`usermod -d /home/Fred Fred`
`usermod -g newgroup Fred`

The first command directs the system towards the correct directory and then sets the secondary and primary groups for that user. If more than one secondary group is required, use the `usermod -G` option.

To include all files with a secondary group is named with a unique (but no-space) name such as “fred” for instance, between the two commands, use the `usermod -G` option. The group “newgroup” and “users” as secondary groups for “Fred” with Fred still as the primary group.

![](bbox=[0.5, 0.6, 0.95, 0.8])

```
usermod -g newgroup users Fred
```