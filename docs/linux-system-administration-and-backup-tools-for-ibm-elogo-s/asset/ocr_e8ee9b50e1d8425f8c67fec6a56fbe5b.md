2. Type in the unique login name of the new user and click OK to continue, and you will see a window similar to Figure 19.

![](bbox=[0.273, 0.111, 0.726, 0.388])

Figure 19. Specifying parameters for the new user

Here you need to specify the following:

+   - Full name - this is the description of the user
- UID - this is the number by which the system knows you. It only attaches this number to file and directory ownership and uses /etc/passwd to convert this to a username when listing the attributes. Generally UID numbers are unique and the system programs will usually prevent you from creating more than one username with the same UID. This can usually be overridden by specifying options to the commands to create ID.
- GID - this is a unique number assigned to a group. Caldera OpenLinux each user has its own default group. The default GID is the next available and the GID numbers are starting at 500.
- Other groups - each user can be a member of one or more groups. You can specify these groups here. If you click the button you will see a window similar to Figure 20.

22 Linux System Administration and Backup for IBM @server xSeries and Netfinity