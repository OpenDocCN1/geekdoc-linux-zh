+   •  **Group**	This is the group that has been assigned ownership of the file or directory. Permissions assigned to the group apply to all user accounts that are members of that group.

+   •  **Others**	This entry refers to all other users who have successfully authenticated to the system. Permissions assigned to this entity apply to these user accounts.

Be aware that permissions are additive. That means it is possible for one user account to receive permissions assigned to more than one entity. For example, suppose I assign the read and write permissions to a file to Owner and the execute permission to Group. If klanders is the file Owner, users is the Group, and klanders is a member of users, then klanders receives both the permissions assigned to Owner and Group. Her effective permissions would be rwx!

Also, be very careful about what permissions you assign to Others. Basically, every user on the system belongs to Others; therefore, any permission you grant to Others gets assigned to anyone who successfully authenticates to the system. In some cases, this can be very useful. However, in others, it can get you in a lot of trouble! Just ask yourself before assigning permissions, “Do I really want everyone to have this kind of access to this file or directory?”

You can use the ls -l command to view the permissions assigned to each of these entities for any file or directory in the file system. Consider the example shown in Figure 11-2.

The first column displayed is the mode for each file and directory. The first character is either a d or a --. This simply indicates whether or not the associated entry is a directory or a file. As you can see, contacts.odt is a file while Desktop is a directory.

![](bbox=[0.25, 0.55, 0.9, 0.83])

**Figure 11-2**	Viewing the file mode with ls -l