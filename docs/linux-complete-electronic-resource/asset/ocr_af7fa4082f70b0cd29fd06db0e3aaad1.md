chmod. In this case, newly-created directories would have 744 permissions, obtained by subtracting 053 from 777. Newly-created files using the 053 umask would have permissions of 644.

If you are using Red Hat, and adhere to their user and group ID creation scheme (User Private Groups), it is only necessary to use 002 for a umask. This is due to the fact that the default configuration is one user per group.

# File Permissions

It's important to ensure that your system files are not open for casual editing by users and groups who shouldn't be doing such system maintenance.

Unix separates access control on files and directories according to three characteristics: owner, group, and other. There is always exactly one owner, any number of members of the group, and everyone else.

A quick explanation of Unix permissions:

+   - **Ownership**—Which user(s) and group(s) retain(s) control of the permission settings of the node and parent of the node

+   - **Permissions**—Bits capable of being set or reset to allow certain types of access to it. Permissions for directories may have a different meaning than the same set of permissions on files.

+   - **Read**
+   
+     - To be able to view contents of a file
+     - To be able to read a directory

+   - **Write**
+   
+     - To be able to add to or change a file
+     - To be able to delete or move files in a directory

+   - **Execute**
+   
+     - To be able to run a binary program or shell script
+     - To be able to search in a directory, combined with read permission

+   - **Save Text Attribute (For directories)** The *sticky bit* also has a different meaning when applied to directories than when applied to files. If the sticky bit is set on a directory, then a user