

```
if (argc != 3) {
    printf("Inappropriate number of command line arguments.\n");
    exit(0);
}
newfilesize = atoi(argv[2]);
if ((fd = open(argv[1], O_WRONLY)) == -1) {
    perror("File opening");
    exit(1);
}
size_o = lseek(fd, 0, SEEK_END); /* Size of original file */
if (truncate(argv[1], newfilesize) == -1) {
    perror("Truncating file");
    exit(1);
}
size_t = lseek(fd, 0, SEEK_END); /* Size of truncated file */
printf("The size of the original file is %d bytes.\n", size_o);
printf("The size of the truncated file is %d bytes.\n", size_t);
if (close(fd) == -1) {
    perror("File closing");
    exit(1);
}
return(0);
}
```

```
% man cat > data
% ls -l data
-rw-r--r-- 1 sarwar faculty 4083 Jan 31 14:15 data
% tail data
```

## BUGS

Because of the shell language mechanism used to perform output redirection, the command "cat file1 file2 > file1" will cause the original data in file1 to be destroyed!

The cat utility does not recognize multibyte characters when the -t or -v option is in effect.

```
% gcc48 -w truncate.c
% ./a.out data 1024
The size of the original file is 4083 bytes.
The size of the truncated file is 1024 bytes.
% tail data
```

The options are as follows:

-   -b    Number the non-blank output lines, starting at 1.
-   -e    Display non-printing characters (see the -v option), and display a dollar sign ('$') at the end of each line.
-   -l    Set an exclusive advisory lock on the standard output file descri

## EXERCISE 18.12

Compile and run truncate.c. Does it work as intended?

## 18.8.7 Removing a File

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

## TABLE 18.10 Some Common Reasons for the unlink() System Call to Fail

| Reason for Failure | Value of errno |
|---|---|
| The named file is a directory. | EISDIR |
| The file specified in path does not exist. | ENOENT |
| A component in path is not a directory. | ENOTDIR |
| Search permission is denied on a component of path. | EACCES |
| Write permission does not exist on the directory containing the file/link to be removed. | EACCES |
| A component in path exceeds the file name size limit (255 characters) and the entire path exceeds the 1023 characters. | ENAMETOOLONG |
| An I/O error occurred while deleting the directory entry for the file or deallocating file's inode. | EIO |
| The file to be removed resides on a read-only file system or device. | EROFS |

```
#include <string.h>
#define HSIZE 512L
int main(int argc, char *argv[])
{
    int fd, i, n, nholes, nw, size_o, size_h;
    char *buf="Random data for creating holes.";
    /* Open the given file */
    if (argc != 3) {
        printf("Inappropriate number of command line arguments.\n");
        exit(0);
    }
    nholes = atoi(argv[2]);
    if ((fd = open(argv[1], O_WRONLY)) == -1) {
        perror("File opening");
        exit(1);
    }
    size_o = lseek(fd, 0, SEEK_END); /* Size of original file */
    for (i=0; i<nholes; i++) {
        n = lseek(fd, HSIZE, SEEK_END);
        nw = write(fd, buf, strlen(buf));
    }
    size_h = lseek(fd,0,SEEK_END); /* Size of file with holes */
    if (close(fd) == -1) {
        perror("File closing");
        exit(1);
    }
    printf("The size of the original file is %d bytes.\n", size_o);
```

