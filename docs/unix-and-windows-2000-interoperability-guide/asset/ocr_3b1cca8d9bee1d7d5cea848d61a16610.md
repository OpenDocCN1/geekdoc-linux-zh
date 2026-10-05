# Chapter 1 • What Is UNIX?

When a user logs into a system, usually one of two mechanisms authenticate that user: the password and group files (/etc/passwd and /etc/group) or the Network Information Service (NIS). Both of these mechanisms establish the user and group identifiers (UIDs and GIDs) of each authenticated user. Among other attributes, the file system stores the UID and GID of the owner of each file and directory in an on-disk structure called an inode, sometimes called file system metadata. Also stored for each file is its permissions.

Three classes of users can access files and directories: owner, group, and other. Owner is usually the person who created the file, group is several users grouped together and who share permissions, and other is all other users. For each of these classes there are three types of access permissions: read, write, and execute. These permissions mean different things, depending on whether you are talking about files or directories. Table 1–2 describes these differences.

# Table 1–2 Standard UNIX Permissions

| Permission | Means This for a Directory | Means This for a File |
|---|---|---|n| read (r) | Users can view names of files and directories in that directory. | Users can view the contents of the file. |
| write (w) | Users can create, rename, or remove files or directories contained in that directory. | Users can change the contents of the file. |
| execute (x) | Users can view the contents of files within the directory, and run commands, scripts, and programs within that directory. | Users can run the file (execute it) by typing the file name at the command prompt. |

To determine a file’s permissions, you use the `ls -l` command, which displays the following information:

+   * Whether the item is a file or directory
* The access permissions for each of the three classes of users (owner, group, and other)
* Number of links
* Name of the owner
* Name of the group
* Size in bytes
* Date and time of last modification