Each file (and directory) can belong to only one user and one group. In the previous example, the name of the file owner (geeko) is shown in the ls output next to the file permissions. The name of the owning group (users) is shown next to the file owner.

You can also view the permissions, owner, and group from the Nautilus file manager. In Nautilus, right-click the icon of the file you want to look at, select **Properties** from the menu, and select the **Permissions** tab. See Figure 9-11.

![](bbox=[0.103, 0.204, 0.515, 0.649])

Figure 9-11

From this dialog, you can change the Read and Write permissions for Owner, Group, and Others by selecting the appropriate option.

You can modify the group ownership of the file or directory to other groups you are a member of by selecting the group from the **File group** drop-down list. Only root can change the owner of a file or change the owning group beyond the groups a user is a member of.

# Change File Permissions with chmod

You can use the chmod command to add (“+”) or remove (“−”) permissions. Both the owner of a file and root can use this command.

The following options can be used to change the permissions:

+   - *u*—Change permissions for the owner (user).
+   - *g*—Change permissions for the group.