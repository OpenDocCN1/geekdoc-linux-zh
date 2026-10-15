The options are as follows:

+   -b    Number the non-blank output lines, starting at 1.
+   -e    Display non-printing characters (see the -v option), and display a dollar sign ('$') at the end of each line.
+   -l    Set an exclusive advisory lock on the standard output file descri

# EXERCISE 18.12

Compile and run truncate.c. Does it work as intended?

# 18.8.7 Removing a File

You can use the unlink() system call to remove a file from the file system structure. The following is a brief description of the call.

```
#include <unistd.h>
int unlink(const char *path);
Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

This system call essentially decrements by one the hard link count for the file stored in its inode. If the resultant link count becomes zero and no process has the file open, the file is removed from the file system. If link count becomes zero but one or more processes have the file open, the removal of the file is delayed until the reference count for the file becomes zero. If the link count is not zero, the file remains in the file system structure and its directory entry is removed. Once a file has been removed from the file system, its directory entry, inode, and all other kernel resources associated with the file are returned to the system for recycling.

On successful completion, unlink() returns 0. It returns -1 on failure and errno is set to indicate the reason for failure. Table 18.10 shows some common reasons for the unlink() call to fail for regular files.

The create_holes_delete.c program shown in the following is an updated version of the create_holes.c program discussed in Section 18.8.5. The program saves the size of the original file, creates holes in it, displays the sizes of the original file and the file with holes, and then removes the file with holes. The program determines the sizes of the original and new file (with holes) by using the lseek() system call. The sample run shows the sizes of original file and the file with holes. The ls -l data command shows that the program did remove the file with holes.

```
% cat create_holes_delete.c
#include <fcntl.h>
#include <unistd.h>
```