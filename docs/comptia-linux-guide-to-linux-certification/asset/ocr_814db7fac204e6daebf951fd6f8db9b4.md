has read and write permissions to the file. The group owner of *file6* is the sys group; thus, any members of the sys group have read permission to the file. Finally, everyone on the sys-tem receives read permission to the file via the other category. Regardless of the mode, the root user receives all permissions to this file.

# Interpreting Permissions

After you understand how to identify the permissions that are applied to user, group, and other on a certain file or directory, you can then interpret the function of those permissions. Permissions for files are interpreted differently from those for directories. Also, if a user has a certain permission on a directory, that user does not have the same permission for all files or subdirectories within that directory; file and directory permissions are treated separately by the Linux system. Table 4-4 shows a summary of the different permissions and their definitions.

The implications of the permission definitions described in Table 4-4 are important to understand. If a user has the read permission to a text file, that user can use, among others, the cat, more, head, tail, less, strings, and od commands to view its contents. That same user can also open that file with a text editor such as vi; however, the user does not have the ability to save any changes to the document unless that user has the write permission to the file as well.

Recall from earlier that some text files contain instructions for the shell to execute and are called shell scripts. Shell scripts can be executed in much the same way that binary compiled programs are; the user who executes the shell script must then have execute permission to that file to execute it as a program.

![](bbox=[0.12, 0.54, 0.26, 0.61])

It is important to avoid giving execute permission to files that are not programs or shell scripts. This ensures that these files will not be executed accidentally, causing the shell to interpret the contents.

Remember that directories are simply special files that have an inode and a data section but what the data section contains is a list of that directory’s contents. If you want to read that list (using the ls command for example), then you require the read permission to the directory. To modify that list, by adding or removing files, you require the write permission to the directory. Thus, if you want to create a new file in a directory with a text editor such as vi, you must have the write permission to that directory. Similarly, when a source file is copied to a target directory with the cp command, a new file is created in the target

| Permission | Definition for Files | Definition for Directories |
|---|---|---|
| Read | Allows a user to open and read the contents of a file | Allows a user to list the contents of the directory (if she has also been given execute permission) |
| Write | Allows a user to open, read, and edit the contents of a file | Allows a user to add or remove files to and from the directory (if she has also been given execute permission) |
| Execute | Allows a user to execute the file in memory (if it is a program file or script) | Allows a user to enter the directory and work with directory contents |

# **Table 4-4** Linux permissions