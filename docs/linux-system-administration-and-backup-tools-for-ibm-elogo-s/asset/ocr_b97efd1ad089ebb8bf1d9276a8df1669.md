# 4.4.3 Group administration using YaST

To administer users, select System Administration -> Group administration from the YaST main menu. Alternatively, start YaST from the command line using the following parameters:

```
yast --mask group --autobexit
```

This will get you directly to the group administration window:

![](bbox=[0.149, 0.198, 0.85, 0.493])

Each user has a unique name and ID. The default group for normal users is users. To create a new group, enter the name of the group and Tab to advance to the next entry field. If you entered a new group name, YaST will automatically assign the next available group ID to this group. You can accept it or modify to your needs. If it is not intended to be a primary (default) user group, you can protect it with a password as well. All users that should be members of this group can be entered in the **List of members of that group** (comma-separated). You can press F3 to select them from the user list, or you can add them manually. Press F4 to create this group, F10 or Esc to leave this window.

If you want to delete a group, select the group with F3 or enter it manually and press F5 to delete it. Please note that this will not delete the user accounts belonging to this group! It will only remove the group