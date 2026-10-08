+   s Socket
n Network special file
M Mount point

+   -links n
True if the file has n links.

+   -user uname
True if the file belongs to the user uname. If uname is numeric and does not appear as a login name in the /etc/passwd file, it is taken as a user ID. The uname operand can be preceded by a + or - to modify the comparison operation as described previously.

+   -group gname
True if the file belongs to the group gname. If gname is numeric and does not appear in the /etc/group file, it is taken as a group ID. The gname operand can be preceded by a + or - to modify the comparison operation as described previously.

+   -nouser
True if the file belongs to a user ID that is not listed in the password database. See passwd(4).

+   -nogroup
True if the file belongs to a group ID that is not listed in the group database. See group(4).

+   -size n[c]
True if the file is n blocks long. If n is followed by a c, the size is in bytes.

+   -atime n
True if the file has been accessed in n days. The access time of directories in pathname_list is changed by find itself.

+   -mtime n
True if the file has been modified in n days.

+   -ctime n
True if the file inode has been changed in n days.

+   -newer file
True if the current file has been modified more recently than the argument file.

+   -newer[tv1[tv2]] file
True if the indicated time value (tv1) of the current file is newer than the indicated time value (tv2) of file. The time values tv1 and tv2 are each selected from the set of characters:
a
The time the file was last accessed
c
The time the inode of the file was last modified
m
The time the file was last modified
If the tv2 character is omitted, it defaults to m. Note that the -newer option is equivalent to -newerm.
Syntax examples:
-newera file
-newermc file