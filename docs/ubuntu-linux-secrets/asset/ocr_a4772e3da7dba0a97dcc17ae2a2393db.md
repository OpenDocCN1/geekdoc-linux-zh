These permissions correspond to the three classes of permissions for the file or folder. You set specific access rules for each group of permissions using the drop-down boxes provided. The permissions available depend on whether the object is a file or folder. The permissions for folders are shown in Table 17-2.

# Table 17-2: Ubuntu Folder Permissions

| Permission | Description |
|---|---|
| List files only | Be able to see the files in the folder but not be able to read or write to the individual files |
| Access files | Read and write to existing files in the folder |
| Create and delete files | Full access to all files in the folder, including creating new ones |
| None | No access to view or use the files in the folder |

You can use these permissions to restrict access to a folder or allow access for other users to a folder if you want to share files on your system.
The permissions for an individual file are shown in Table 17.3.

# Table 17-3: Ubuntu File Permissions

| Permission | Description |
|---|---|
| None | No access to the file |
| Read-only | Only able to view the contents of the file |
| Read and write | Able to view and modify the contents of the file |

Read-only permission allows you to permit others to view a file but not change its contents. This restriction can come in handy when posting information that you want to control on your system.

# Summary

This chapter walked through the Ubuntu system of controlling user access. Ubuntu uses a system of user and group accounts to limit access to specific files, folders, and features of the Ubuntu workstation and server. The User Administration tool provides a graphical environment where you can create, modify, and delete user and group accounts. The chapter demonstrated how to manage user and group accounts using this tool.

The chapter also discussed how to perform user and group management using the command line programs `adduser`, `deluser`, `addgroup`, and `delgroup`. These programs provide all the access you need to manage user and group accounts from the command line.