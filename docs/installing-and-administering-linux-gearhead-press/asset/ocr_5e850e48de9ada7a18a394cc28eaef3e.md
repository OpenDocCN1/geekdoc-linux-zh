point out that a d in the first position indicates that the entity is a directory. If there is a hyphen ( - ) in the first position, that indicates a file.

**Field 2** is the link count. For directories, the link count indicates the number of subdirectories in that directory. Directories always have a link count of at least two (for . and ..). The link count for files indicates the number of names given to a single file. When you enter the command rm filename, for instance, you reduce the link count for a file by 1. A file is removed only when its link count reaches 0. For a discussion of linking and removing files, see Chapter 5.

**Field 3** is the username of the person who owns the entry (the file or directory). The owner is generally the person who created the entry, but ownership can be transferred.

**Field 4** is the name of the group for which group protection privileges are in effect. Groups are generally created to organize users based on job description, organizational structure, project assignment, and so on, and their privileges determine the files and directories to which the group has access. Every user belongs to at least one group. The user in Example 4.9 is assigned to the group knights01. We touch briefly upon group concepts in Chapter 6 when we discuss file and directory permissions.

**Field 5** is the character count of the entry. Note that directory space is allocated in 4096-byte increments. Thus, just looking at the output here will not necessarily give you a good idea of the number of files or subdirectories in the directory in question. Note that you do not make the directory allocation size smaller when you delete files. To decrease the size of a directory, you must move files to newer, smaller directories.

**Fields 6 and 7** indicate the date and time that the contents of the file or directory were last modified. Other ls command options display other time attributes (for example, -u displays the last access time to the file and -c displays the time the inode was modified).

**Field 8** is the name of the entry, whether a file or a directory.

# Example 4.10 Long Listings, Including inode Numbers, with ls -li

The Don will use the -li options with the ls command to display file information, including the inode number. But first, please notice that he is