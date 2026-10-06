# Controlling Access to Files

Read and write permissions for the owner. Read-only permission for all others.

Read and write permissions for the owner, and read-only permission for the group. No permission for others.

Read and write permissions for the owner. No permission for anybody else.

Read permission for the owner. No permission for anybody else.

Execution permissions makes sense for ordinary files, but it's meaningless for most other file types, directories, though, the execute bit another way. When a directory's execute bit is set, it means that the directory's contents may be searched. This is a highly desirable characteristic for directories, so you'll almost never find a directory on which the execute bit is set in conjunction with the read bit.

Directories can be confusing with respect to permission. Recall that directories are are interpreted in a special way. As such, if a user can write to a directory, they can create, delete, or rename files in the directory, even if the user isn't the owner of those files and does not have permission to write to those files. You can use the sticky bit (described shortly, in "Special Permissions") to alter this behavior.

Symbolic links are unusual with respect to permissions. This file type always has 777 (rwxrwxrwx) permissions, granting all users access to it. This access applies only to the link itself, not to the linked-file. In other words, all users can read the contents of the link to discover the name of the file to which it points, but the permissions on the linked-file determine its access. Changing the permissions on a symbolic link affects the linked-file.

Many of the permissions don't apply to root. The superuser can read or write any file on the computer—even files that grant access to nobody (that is, those that have 000 permissions). The superuser still needs execute bit to run a program file, but the superuser has the power to change the permissions on any file, so this limitation is not very substantial. Some files may be inaccessible to root, but only because of an underlying restriction—even root can't access a disk that isn't installed in the computer.

# Special Permission Bits

A few permission options are also supported, and they may be indicated by changes to the permission string:

Set User ID (SUID) The set user ID (SUID) option is used in conjunction with executable files, and it lets Linux to run the program with the permissions of whoever owns the file rather than with the permissions of the user who runs the program. For instance, if a file is owned by root and has its UID bit set, the program runs with root privileges and can read any file on the computer. Some servers and other system programs run this,