
```c
int main(int argc, char *argv[])
{
     struct stat statbuf;
 
     /* 检查是否提供了文件名 */
     if (argc < 2) {
         printf("specify a file to test\n");
         return 1;
     }
     /* 获取文件的 stat 信息 */
     if (stat(argv[1],&statbuf) == -1 ) {
         printf("Can't stat file\n");
         return 1;
 }
```

# 第 19 章 高级文件处理

```c
    }
 
    printf("%s ", argv[1]);
 
    /* 从 stat st_mode 确定文件类型 */
    if (S_ISDIR(statbuf.st_mode)) {
        printf("is a directory\n");
    } else if (S_ISCHR(statbuf.st_mode)) {
        printf("is a character special file\n");
    } else if (S_ISBLCK(statbuf.st_mode)) {
        printf("is a block special file\n");
    } else if (S_ISREG(statbuf.st_mode)) {
        printf("is a regular file\n");
    } else if (S_ISFIFO(statbuf.st_mode)) {
        printf("is a FIFO special file\n");
    } else if (S_ISSOCK(statbuf.st_mode)) {
        printf("is a socket\n");
    } else {
        printf("is unknown\n");
    }
 
    return 0;
 }
```

通过以下方式使用多种类型演示了该应用程序的使用：

+   $ ./ftype .

.. is a directory

$    ./ftype /dev/mem

/dev/mem is a character special file

$    ./ftype /dev/fd0

a block special file

$    ./ftype /etc/resolv.conf

/etc/resolv.conf is a regular file

$

`stat` 命令提供的信息比 `st_mode` 字段要多。下一节将查看通过 `stat` 返回的其他属性。

# 362 GNU/Linux 编程

## 其他 stat 信息

`stat` 命令提供了关于文件的丰富信息，包括其大小、所有者、组、最后修改时间以及访问时间。列表 19.2 提供了一个简单的程序，该程序实现了上述数据元素的输出，并利用了其他辅助函数将原始数据转换为人类可读的字符串。特别是，`stat` 函数接收一个时间结构（标准时间格式）并将其转换为字符串。该函数提供了大量的选项和输出格式。

列表 19.2 使用 `stat` 命令获取文件数据（位于 CD-ROM 的 `../software/ch19/ftime2.c`）

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <pwd.h>
#include <grp.h>
#include <time.h>
#include <langinfo.h>

int main(int argc, char *argv[])
{
    struct stat statbuf;
    struct passwd *pwd;
    struct group *grp;
    struct tm *tm;
    char tmstr[257];

    /* 检查是否提供了文件名 */
    if (argc < 2) {
        printf("specify a file to test\n");
        return 1;
    }

    /* 获取文件的 stat 信息 */
    if (stat(argv[1], &statbuf) == -1) {
        printf("Can't stat file\n");
        return 1;
    }

    printf("File Size : %-d\n", statbuf.st_size);
    pwd = getpwuid(statbuf.st_uid);
32:   if (pwd) printf("File Owner: %s\n", pwd->pw_name);
33:
34:   grp = getgrgid(statbuf.st_gid);
35:   if (grp) printf("File Group: %s\n", grp->gr_name);
36:
37:   tm = localtime(&statbuf.st_mtime);
38:   strftime(tmstr, sizeof(tmstr), nl_langinfo(D_T_FMT), tm);
39:   printf("File Date: %s\n", tmstr);
40:
41:   return 0;
42:   }
```

执行 `stat` 应用程序（称为 `ftype2`）对 `passwd` 文件产生如下结果：

```bash
$ ./ftype /etc/passwd
File Size : 1337
File Owner : root
File Group: root
File Date : Sun Jan 6 19:44:50 2008
$
```

同样可以使用 `fstat` 命令检索相同的信息，尽管该命令操作于文件描述符而不是文件名。

## 确定当前工作目录

你可以通过 `getcwd` 命令学习当前工作目录的名称，包括完整路径。另一个函数 `pathconf` 允许你确定传递给 `getcwd` 的缓冲区 own。这一过程在列表 19.3 中进行了演示。在知道最大路径长度后，使用 `malloc` 分配缓冲区，然后将其传递给 `getcwd` 以返回当前工作目录。在将其输出到标准输出后，释放该缓冲区。

## 列表 19.3 使用 `getcwd` 获取当前工作目录（位于 CD-ROM 的 `/software/ch19/getcwd.c`）

```c
1:   #include <stdio.h>
2:   #include <unistd.h>
3:   #include <stdlib.h>
4:
5:   int main()
6:   {
7:   char *pathname;
8:   long maxbuffersize;
9:
10:  maxbuffersize = pathconf(".", _PC_PATH_MAX);
11:  if (maxbuffersize == -1) return 1;
12:
13:  pathname = (char *)malloc(maxbuffersize);
14:
15:  (void)getcwd(pathname, (size_t)maxbuffersize);
16:
17:  printf("%s\n", pathname);
18:
19:  free(pathname);
20:
21:  return 0;
22:  }
```

## 枚举目录

GNU/Linux 提供了用于枚举目录或整个系统的函数。与操作文件类似，必须打开目录然后读取其内容。在这种情况下，目录的内容是文件本身（可以是目录）。

要打开目录，使用 `opendir` 函数。它返回一个目录流（`DIR` 类型）。流打开后，可以使用 `readdir` 函数读取。每次调用 `readdir` 返回一个目录项，在枚举完成后返回 `NULL`。当不再需要目录流时，应用 `closedir` 关闭。

下面的简单应用程序（列表 19.4）说明了用过的 API 函数：`opendir`、`readdir` 和 `closedir`。在此示例中，枚举命令行指定的目录并仅输出指向普通文件的目录项。

## 列表 19.4 使用 `readdir` 枚举目录（位于 CD-ROM 的 `../software/ch19/dirlist.c`）
