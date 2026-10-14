+   - The user can be a member of a group granted permission on the file
+   - The user is neither the owner nor a member of the group

Each of these roles may have Read, Write, or Execute permissions, or a combination thereof.

Read permissions on a file or folder, allow you to see (read) its contents.

Write permissions on a file or folder, allow you to change its contents. In the case of folders, it might mean that you have permissions to add files to the directory.

Execute permissions are special. When set on a file, it indicates that the file is a program. If your role has Execute permissions, you are able to run the program. On directories, the Execute permissions also controls who can navigate into the directory. If you intend to copy files into a directory, your role must have Execute permissions on the directory.

![](bbox=[0.22, 0.49, 0.32, 0.57])

# Understanding the Permissions Panel.

In the preceding figure of the Permissions Panel, the user (owner of the file) has Read and Write permissions; members of the group assigned to the file have Read and Write permissions; and other users are able to read the file but are not able to modify it because they lack write permissions.

A permission setting is enabled if it is checked. Permissions can only be assigned by the owner of the file or the superuser (root).

Don’t change permissions on a file or folder unless you know what you are doing. For example, if you remove the Change Into settings (Execute permissions) for a folder, you will make it impossible for any user to navigate or open files in that folder.

+   Previous | Table of Contents | Next