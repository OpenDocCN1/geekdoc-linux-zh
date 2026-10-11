# ## Accelerated Review

+   - Ownership defines which user and group owns a particular file or directory in the file system.
+   - You can use the ls -l command to view ownership.
+   - You can use the chown utility to configure user and group ownership of a file or directory.
+   - You can use the chgrp utility to change group ownership.
+   - You must be logged in as root to change user ownership.
+   - You must be logged in as root or as the file/directory owner to change group ownership.
+   - Permissions are used to define what users may or may not do with files or directories in the file system.
+   - Linux uses the read, write, and execute permissions for files and directories.
+   - Linux permissions are assigned to Owner, Group, and Others.
+   - Linux permissions are additive.
+   - The permissions assigned to Owner, Group, and Others constitute the file or directory's mode.
+   - Permissions can be represented numerically: read=4, write=2, and execute=1.
+   - Summing up all permissions assigned to an entity, such as Owner, allows you to represent all assigned permissions with a single number.
+   - You use the chmod utility to modify permissions.
+   - Linux assigns rw-rw-rw- permissions by default to new files and rwxrwxrwx permissions to new directories.
+   - These permissions are too relaxed for most situations, so the umask variable is used to subtract specific permissions from the defaults.
+   - The default value of umask is 022, which subtracts the write permission (2) from Group and Others.
+   - You can modify the value of umask to change the default permissions assigned upon creation.
+   - Linux also includes three default special permissions: Sticky Bit, SUID, and SGID.
+   - You assign special permissions with chmod by adding an additional digit before the Owner digit in the command.
+   - You can use the quota package to implement disk quotas in the file system.
+   - Quotas prevent users from consuming too much disk space.
+   - You can set quotas for the number of blocks a user is allowed to consume (disk space) and the number of inodes a user may consume (number of files).