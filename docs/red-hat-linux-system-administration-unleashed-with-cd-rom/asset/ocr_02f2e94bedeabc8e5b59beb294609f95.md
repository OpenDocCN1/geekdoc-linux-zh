# The newgrp Command

Having membership in different groups is a good thing, but having to use chgrp to change the group ownership of your files all the time is tedious. If you are working with other users and need to share files using your common group ownership, it would be nice to be able to create files owned by the shared group by default instead of using chgrp constantly. You can do this with the newgrp and sg commands.

# newgrp

newgrp allows you to temporarily change your default group to another group that you are a member of or for which you have the password. newgrp does not go through login or change the current directory when switching groups. You can either type exit to return to your previous group, or you can run the newgrp command with no arguments to accomplish the same thing. The syntax is:

```
newgrp <new_group_name>
```

Obviously, <new group name> is the group name to which to switch. If this is left blank, the user's default group from /etc/passwd will be used.

# Other System Commands Related to Users and Groups

# chage

All the date calculations for the /etc/shadow file can be somewhat tedious, so if you are forced to do this without the use of a menu or GUI tool, hopefully you will have the chage function at your disposal. The sole purpose of chage is to manipulate the settings in /etc/shadow. The chage command has several options:

+   -m <min_change>
+   Modify the min_change field.
+   
+   -M <max_change>
+   Modify the max_change field.
+   
+   -d change_days
+   Modify the change_days field. Can be specified as YYYY-MM-DD.
+   
+   -I <inactive>