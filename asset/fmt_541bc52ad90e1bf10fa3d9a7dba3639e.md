
```c
dev_t      st_dev;                     /* device number */
ino_t      st_ino;                     /* inode number */
mode_t     st_mode;                    /* file type and permissions */
nlink_t    st_nlink;                   /* link count */
uid_t      st_uid;                     /* owner ID of file */
gid_t      st_gid;                /* group ID of file */
dev_t      st_rdev;    /* device numbers for device file */
off_t      st_size;                /* file size, in bytes */
time_t     st_atime;               /* time of last access */
time_t     st_mtime;               /* time of last modification */
time_t     st_ctime;               /* time of last status change */
```

此结构中 `st_mode` 字段的值的符号常量通过 `<sys/stat.h>` 定义。

此结构中的信息可使用以下三种系统调用之一恢复：`fstat()`、`stat()` 或 `lstat()`：

```c
#include <sys/stat.h>
#include <unistd.h>

int fstat(int fd, struct stat *sbuf);
int stat(char *pathname, struct stat *sbuf);
int lstat(char *pathname, struct stat *sbuf);
```

对于 `fstat()`，`fd` 参数是打开文件描述符的文件描述符，`sbuf` 是指向 `struct stat` 的指针，调用将用适当的 `status` 详细信息填充它。

`stat()` 调用与 `fstat()` 相同，只是第一个参数是文件的路径名而不是文件描述符。

`lstat()` 调用与 `stat()` 相同，只是如果文件是符号链接，`lstat()` 将给出链接文件本身的状态详细信息，而 `stat()` 将跟随链接并给出链接指向的文件的详细信息。

所有三个系统调用在成功完成时返回 `0`，在出错时返回 `-1`，并将 `errno` 设置为适当的值。

下面的代码是一个简单的程序，将与任何给定文件路径名关联的 `struct stat` 中的信息以人类可读的形式显示出来：

```c
#include <stdio.h>
#include <sys/stat.h>

#define MAJOR(a) (int)((unsigned short)(a) >> 8)
#define MINOR(a) (int)((unsigned short)(a) & 0xFF)

main(int argc, char **argv)
{
    struct stat sbuf;
    int dev_flag;

    for (; argc>1; --argc)
{
    printf("\nFile name: %s\n", argv[argc-1]);

    if (stat(argv[argc-1], &sbuf)==-1)
        fatal("obtaining status details");

    dev_flag = file_type(&sbuf);
    printf("Permission bits: %o\n", sbuf.st_mode & 07777);
    printf("File numbers: ");
    printf("major %d, ", MAJOR(sbuf.st_dev));
    printf("minor %d, ", MINOR(sbuf.st_dev));
    printf("inode %d\n", sbuf.st_ino);
    printf("Link count: %d\n", sbuf.st_nlink);

    if (dev_flag)
    {
        printf("Device numbers: ");
        printf("major %d, ", MAJOR(sbuf.st_rdev));
        printf("minor %d\n", MINOR(sbuf.st_rdev));
    }
    else
        printf("File size: %ld\n", sbuf.st_size);

    printf("File owner ID: %d\n", sbuf.st_uid);
    printf("File group ID: %d\n", sbuf.st_gid);
}
}
```

```c
file_type(struct stat *sbufp)
{
    printf("File type: ");

    switch (sbufp->st_mode & S_IFMT)
    {
    case S_IFREG:
        printf("Ordinary file\n");
        return 0;

    case S_IFDIR:
        printf("Directory\n");
        return 0;

    case S_IFIFO:
printf("Named pipe (FIFO)\n");
return 0;

case S_IFBLK:
    printf("Block device special file\n");
    return 1;

case S_IFCHR:
    printf("Character device special file\n");
    return 1;

default:
    printf("Unknown...\n");
    exit(1);
}
}
```

```c
fatal(char *mess)
{
    fprintf(stderr, "Error: %s\n", mess);
    exit(1);
}
```

请注意，该程序能够处理命令行上的多个文件名。程序的典型输出如下所示：

```
$ file_status /etc ./book.ps /dev/modem

File name: /dev/modem
File type: Character device special file
Permission bits: 660
File numbers: major 3, minor 65, inode 47638
Link count: 1
Device numbers: major 5, minor 64
File owner ID: 0
File group ID: 14

File name: ./book.ps
File type: Ordinary file
Permission bits: 644
File numbers: major 3, minor 66, inode 34876
Link count: 1
File size: 1049173
File owner ID: 500
File group ID: 500

File name: /etc
File type: Directory
Permission bits: 755
File numbers: major 3, minor 65, inode 45701
Link count: 8
File size: 2048
File owner ID: 0
File group ID: 0
```

### 15.5 更改文件属性

在你能收集到的有关文件的各种信息中，只有相对较少的一部分是可以更改的。本节将介绍你对其具有控制权的大多数内容。

#### 15.5.1 chmod 和 fchmod 系统调用

首先要查看的是文件权限位。用于更改它们的系统调用称为 `chmod()` 和 `fchmod()`。这些系统调用可以更改的位与 `chmod` 命令可以更改的位完全相同。这包括所有者、组和全局用户类别的读、写和执行位。它还包括 `setuid` 位和 `setgid` 位。`chmod()` 和 `fchmod()` 的原型如下：

```c
#include <sys/types.h>
#include <sys/stat.h>

int chmod(char *pathname, mode_t mode);
int fchmod(int fd, mode_t mode);
```
