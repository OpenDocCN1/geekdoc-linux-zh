# TABLE 2.9 Example Permissions and Their Meanings (continued)

| Permission String | Octal Code | Meaning |
| --- | --- | --- |
| rw-r----- | 640 | Read and write permissions to the owner, and read-only permission to the group. No permission to others. |
| rw------- | 600 | Read and write permissions to the owner. No permission to anybody else. |
| r------- | 400 | Read permission to the owner. No permission to anybody else. |

Execute permission makes sense for ordinary files, but it's meaningless for most other file types, such as device files. Directories, though, make use of the execute bit in another way. When a directory's execute bit is set, that means that the directory's contents may be searched. This is a highly desirable characteristic for directories, so you'll almost never find a directory on which the execute bit is not set in conjunction with the read bit.

Directories can be confusing with respect to write permission. Recall that directories are files that are interpreted in a special way. As such, if a user can write to a directory, that user can create, delete, or rename files in the directory, even if the user isn't the owner of those files and does not have permission to write to those files. The sticky bit (described shortly) can alter this behavior.

Symbolic links are unusual with respect to permissions. This file type always has 777 (rwxrwxrwx) permissions, thus granting all users full access to the file. This access applies only to the link file itself, however, not to the linked-to file. In other words, all users can read the contents of the link to discover the name of the file to which it points, but the permissions on the linked-to file determine its file access. Attempting to change the permissions on a symbolic link affects the linked-to file.

Many of the permission rules do not apply to root. The superstar can read or write any file on the computer—even files that grant access to nobody (that is, those that have 000 permissions). The superstar still needs an execute bit to be set to run a program file, but the superstar has the power to change the permissions on any file, so this limitation isn't very substantial. Some files may be inaccessible to root but only because of an underlying restriction—for instance, even root can't access a hard disk that's not installed in the computer.

A few special permission options are also supported, and they may be indicated by changes to the permission string:

Set user ID (SUID) The set user ID (SUID) option is used in conjunction with executable files, and it tells Linux to run the program with the permissions of whoever owns the file, rather than with the permissions of the user who runs the program. For instance, if a file is owned by root and has its SUID bit set, the program runs with root privileges and can