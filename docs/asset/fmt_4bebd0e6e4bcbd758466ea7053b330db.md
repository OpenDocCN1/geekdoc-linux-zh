
然而，在当今世界中，这种方法已不可行。POSIX 提供了一个 XSI 扩展来访问这些信息。主要函数名为 `statvfs()`。（“vfs” 部分源自底层的 SunOS 技术，后来用于 System V Release 4，被称为*虚拟文件系统*）。有两个函数：

```c
#include <sys/types.h>
#include <sys/statvfs.h>

int statvfs(const char *path, struct statvfs *buf);
int fstatvfs(int fd, struct statvfs *buf);
```

`statvfs()` 针对任意文件使用路径名；它返回关于包含该文件的文件系统信息。`fstatvfs()` 接受一个打开的文件描述符作为其第一个参数；在此处，返回的信息同样是关于包含该打开文件的文件系统。`struct statvfs` 包含以下成员：

```c
struct statvfs {
    unsigned long int f_bsize;    /* 块大小 */
    unsigned long int f_frsize;   /* 碎片大小（“基本块大小”） */
    fsblkcnt_t f_blocks;          /* 块总数 */
    fsblkcnt_t f_bfree;           /* 空闲块总数 */
    fsblkcnt_t f_bavail;         /* 可用块数量（≤ f_bfree） */
    fsfilcnt_t f_files;           /* inode 总数 */
    fsfilcnt_t f_favail;         /* 可用 inode 数量（≤ f_files） */
    unsigned long int f_fsid;     /* 文件系统 ID */
    unsigned long int f_flag;     /* 标志：ST_RDONLY 和/或 ST_NOSUID */
    unsigned long int f_namemax;  /* 文件名最大长度 */
};
```

其包含的信息足以编写 `df` 程序：

- `unsigned long int f_bsize`

块大小是执行 I/O 的推荐大小。文件系统会尝试将至少 `f_bsize` 字节的数据保持在磁盘上的连续扇区中。（扇区是磁盘上可寻址的最小数据量。通常，一个磁盘扇区为 512 字节。）

- `unsigned long int f_frsize`

某些文件系统（如 BSD Fast Filesystem）区分块和块的碎片。总大小小于一块的中小型文件将驻留在若干碎片中。这避免了浪费磁盘空间（尽管代价是内核代码复杂性增加）。碎片大小在文件系统创建时选定。

- `fsblkcnt_t f_blocks`

文件系统中块的总数（以 `f_bsize` 为单位）。

- `fsblkcnt_t f_bfree`

文件系统中空闲块的总数。

- `fsblkcnt_t f_bavail`

实际可使用的块数量。某些文件系统保留文件系统的一部分块供超级用户使用，以防文件系统被填满。现代系统保留约 5%，尽管管理员可以更改这个数字。（参见 GNU/Linux 系统上的 `tune2fs(8)`，以及 Unix 系统上的 `tuneefs(8)`。）

- `fsfilcnt_t f_files`

文件系统中 inode（“文件序列号”，按 POSIX 术语称为）的总数。该数字通常在文件系统创建时初始化并永久化。

- `fsfilcnt_t f_ffree`

空闲 inode 的总数。

- `fsfilcnt_t f_favail`

实际可使用的 inode 数量。就像块一样，一部分 inode 被保留给超级用户使用。

- `unsigned long int f_fsid`

文件系统 ID。POSIX 未指定其具体代表什么，且在 Linux 下未被使用。

- `unsigned long int f_flag`

提供有关文件系统信息的标志。POSIX 规定了两个：`ST_RDONLY`，用于只读文件系统（如 CD-ROM），以及 `ST_NOSUID`，禁止对可执行文件使用 setuid 和 setgid 权限位。GNU/Linux 系统提供额外的标志：它们列于表 8.2 中。

- `unsigned long int f_namemax`

文件名的最大长度。这指的是路径名中的每个独立组成部分；换句话说，是目录项的最大长度。

**表 8.2**

**GLIBC 中 `f_flag` 的取值**

| **标志** | **POSIX** | **含义** |
| :--- | :--- | :--- |
| `ST_MANDLOCK` | | 强制锁定（见第 14.2 节，第 531 页）。 |
| `ST_NOATIME` | | 不更新每次访问的访问时间字段。 |
| `ST_NODEV` | | 禁止通过设备文件进行访问。 |
| `ST_NODIRATIME` | | 不更新目录的访问时间字段。 |
| `ST_NOEXEC` | | 禁止执行二进制文件。 |
| `ST_NOSUID` | \| | 文件系统禁止使用 setuid 和 setgid 位。 |
| `ST_RDONLY` | \| | 文件系统为只读。 |
| `ST_SYNCHRONOUS` | | 所有写入均为同步（见第 4.6.3 节，第 110 页）。 |

`fsblkcnt_t` 和 `fsfilcnt_t` 类型定义在 `<sys/types.h>` 中。它们通常是无符号 `long`，但在现代系统中，它们甚至可能是 64 位类型，因为磁盘容量变得非常大。下面的程序 `ch08-statvfs.c` 展示了如何使用 `statvfs()`：

```c
1 /* ch08-statvfs.c -- 演示 statvfs */
2
3 /* 注意：GNU/Linux 特定！ */
4
5 #include <stdio.h>
6 #include <errno.h>
7 #include <mntent.h> /* 用于 getmntent() 等 */
8 #include <unistd.h> /* 用于 getopt() */
9 #include <sys/types.h>
10 #include <sys/statvfs.h>
11
12 void process(const char *filename);
13 void do_statvfs(const struct mntent *fs);
14
15 int errors = 0;
16 char *myname;
17
18 /* main -- 处理选项 */
19
20 int main(int argc, char *argv[])
21 {
22     int c;
23     char *file = "/etc/mtab";  /* 默认读取的文件 */
24
25     myname = argv[0];
26     while ((c = getopt(argc, argv, "f:")) != -1) {
27         switch (c) {
28             case 'f':
29                 file = optarg;
30                 break;
31             default:
32                 fprintf(stderr, "usage: %s [-f fstab-file]\n", argv[0]);
33                 exit(1);
34         }
35     }
36
37     process(file);
38     return (errors != 0);
39 }
40
41 /* process --- 从文件读取 struct mntent 结构 */
42
43 void process(const char *filename)
44 {
45     FILE *fp;
46     struct mntent *fs;
47
48     fp = setmntent(filename, "r");  /* 只读 */
49     if (fp == NULL) {
50         fprintf(stderr, "%s: %s: could not open: %s\n",
51                 myname, filename, strerror(errno));
52         exit(1);
53     }
54
55     while ((fs = getmntent(fp)) != NULL)
56         do_statvfs(fs);
57
58     endmntent(fp);
59 }
```
