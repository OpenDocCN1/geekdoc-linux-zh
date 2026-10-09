
以下代码片段演示了如何检索目录索引节点：

```c
d = (struct dinode *)kindo_buf(fab0 * sizeof(struct dinode));
printf("\nlnumber %ld info:\n", inumber);
printf("\tmode = 0%o\n", d->di_mode);
printf("\tlinks = %d\n", d->di_nlink);
printf("\towner = %d\n", d->di_uid);
printf("\tmod. time = %s", ctime((time_t *)&d->di_mtime));
exit(EXIT_SUCCESS);
EC_CLEANUP_BGN

    exit(EXIT_FAILURE);
EC_CLEANUP_END
```

`sb_buf` 的复杂声明：

```c
char sb_buf[((sizeof(struct fs) / DEV_BSIZE) + 1) * DEV_BSIZE];
```

是为了将其大小向上取整到偶数扇区，因为在 FreeBSD 上读取原始磁盘设备有这一要求。

第一个 `lseek` 操作定位到 `SBLOCK * DEV_BSIZE`，即超级块的位置。`SBLOCK` 恰好为 16，而 `DEV_BSIZE` 是扇区大小，通常为 512，这对大多数磁盘都适用。超级块总是从文件系统的起始位置开始第 16 个扇区。第一组 `printf` 语句打印非常长的 `fs` 结构体中的几个字段。这是该输出：

```text
Superblock info for /dev/ad0s1g:
last time written = Mon Oct 14 15:25:25 2002
number of blocks in fs = 1731396
number of data blocks in fs = 1704331
size of basic blocks in fs = 16384
size of frag blocks in fs = 2048
name mounted on = /usr
```

接下来，程序使用一些宏（这些宏位于某个头文件中，因为 FFS 磁盘上的算术运算非常复杂）来查找作为参数提供的索引节点（`argv[1]`）。我通过 `ls` 命令的 `-i` 选项获取了文件的 i 节点号：

```text
$ ls -li x
383642 -rw-r--r-- 1 marc marc 11687 Sep 19 13:29 x
```

以下是 i 节点 383642 的其余输出：

```text
inumber 383642 info:
mode = 0100755
links = 1
owner = 1001
mod. time = Thu Sep 19 13:29:30 2002
```

我不打算再花时间讨论底层磁盘访问——我真正想做的只是说明普通文件和特殊文件之间的关系。但是如果你有 FreeBSD 系统，可能会喜欢稍作修改以显示其他信息；或者如果你有另一个 UNIX 系统，也可以尝试将其修改为适用于该系统。

## 3.2.3 statvfs 和 fstatvfs 系统调用

在块设备或原始设备上找到超级块后，使用 `read` 读取它虽然有趣，但在符合 SUS1 的系统上（参见 1.5.1 节），使用 `statvfs` 或 `fstatvfs` 系统调用是一种更好的方法：

```c
/* statvfs—通过路径获取文件系统信息 */
#include <sys/statvfs.h>
int statvfs(
    const char *path,     /* 路径名 */
    struct statvfs *buf   /* 返回的信息 */
); /* 成功时返回 0，出错时返回 -1（并设置 errno） */

/* fstatvfs—通过文件描述符获取文件系统信息 */
#include <sys/statvfs.h>
int fstatvfs(
    int fd,               /* 文件描述符 */
    struct statvfs *buf   /* 返回的信息 */
); /* 成功时返回 0，出错时返回 -1（并设置 errno） */
```

通常，你会使用 `statvfs`，它返回包含其第一个参数所给路径的文件系统信息。如果有一个已打开的文件，你可以改用 `fstatvfs`，它返回相同的信息。

标准定义了 `statvfs` 结构的字段，但实现并不要求支持所有字段。此外，大多数实现支持额外的字段以及 `f_fflag` 字段的额外标志。你需要查看你系统的手册页以获取具体细节。如果某个实现不支持某个标准字段，该字段仍然存在，但不会包含有意义的信息。

```c
/* struct statvfs—statvfs 和 fstatvfs 的结构体 */
struct statvfs {
    unsigned long f_bsize;       /* 块大小 */
    unsigned long f_fsize;       /* 基本（fblock）大小 */
    fsblkcnt_t f_blocks;         /* 总块数 */
    fsblkcnt_t f_bfree;          /* 空闲块数 */
    fsblkcnt_t f_bavail;         /* 可用 fblock 数 */
    fsfilcnt_t f_files;          /* 总 i 节点数 */
    fsfilcnt_t f_ffree;          /* 空闲 i 节点数 */
    fsfilcnt_t f_favail;         /* 可用 i 节点数 */
    unsigned long f_fsid;        /* 文件系统 ID */
    unsigned long f_flag;        /* 标志（见下文） */
    unsigned long f_namemax;     /* 文件名最大长度 */
};
```

关于此结构体的一些说明：

-   大多数文件系统为文件分配相当大的块，由 `f_fsize` 字段给出，以加快访问速度，但随后使用较小的碎片块来结束文件，以避免浪费空间。碎片块大小被称为*基本*块大小，由 `f_fsize` 字段给出；我们简称为 *fblock*。类型为 `fsblkcnt_t` 的字段以块为单位，因此，要获取总字节空间，需将 `f_blocks` 乘以 `f_fsize`。
-   类型 `fsblkcnt_t` 和 `fsfilcnt_t` 是无符号的，但具体由实现定义。它们通常是 long 或 long long。如果需要显示其中一个且你有 C99 编译器，请将其强制转换为 `uintmax_t` 并使用 `printf` 格式 `%ju`；否则，将其强制转换为 `unsigned long long` 并使用格式 `%llu`。
-   SUS 标准为 `f_flag` 字段仅定义了两个标志，指示文件系统的挂载方式：
    -   如果是只读，则设置 `ST_RDONLY`，
    -   如果可执行文件应忽略设置用户 ID 在执行时和设置组 ID 在执行时位（一种安全措施），则设置 `ST_NOSUID`。
-   适用于 `f_bavail` 和 `f_favail` 字段的术语“可用”意味着“对非超级用户进程可用”。它可能小于对应的“空闲”字段，以便在空闲空间变紧时性能会受到影响上，预留最小量的空闲空间。

FreeBSD 由于早于 SUS，不支持 `statvfs` 或 `fstatvfs` 函数，但它有一个类似名为 `statfs` 的函数，其结构体名称不同且大多数字段也不同。对于基本信息，可以通过编写同时适用于 `statvfs` 和 `statfs` 的代码来实现，如下所示程序所示。

# 磁盘特殊文件和文件系统

```c
#if _XOPEN_SOURCE >= 4
#include <sys/statvfs.h>
#define FCN_NAME statvfs
#define STATVFS 1

#elif defined(FREEBSD)
#include <sys/param.h>
#include <sys/mount.h>
#define FCN_NAME statfs

#else
#error "Need statvfs or nonstandard substitute"
#endif

void print_statvfs(const char *path)
{
  struct FCN_NAME buf;

  if (path == NULL)
    path = ".";
  ec_neg1( FCN_NAME(path, &buf) )
#ifdef STATVFS
  printf("block size = %lu\n", buf.f_bsize);
  printf("fundamental block (fblock) size = %lu\n", buf.f_fsize);
#else
  printf("block size = %lu\n", buf.f_iosize);
  printf("fundamental block (fblock) size = %lu\n", buf.f_bsize);
#endif
  printf("total number of fblocks = %llu\n",
         (unsigned long long)buf.f_blocks);
  printf("number of free fblocks = %llu\n",
         (unsigned long long)buf.f_bfree);
  printf("number of avail. fblocks = %llu\n",
         (unsigned long long)buf.f_bavail);
  printf("total number of i-numbers = %llu\n",
         (unsigned long long)buf.f_files);
  printf("number of free i-numbers = %llu\n",
         (unsigned long long)buf.f_ffree);
#ifdef STATVFS
  printf("number of avail. i-numbers = %llu\n",
         (unsigned long long)buf.f_favail);
  printf("file-system ID = %lu\n", buf.f_fsid);
  printf("Read-only = %s\n",
         (buf.f_flag & ST_RDONLY) == ST_RDONLY ? "yes" : "no");
  printf("No setuid/setgid = %s\n",
         (buf.f_flag & ST_NOSUID) == ST_NOSUID ? "yes" : "no");
  printf("max length of filename = %lu\n", buf.f_namemax);
#else
  printf("Read-only = %s\n",
         (buf.f_flags & MNT_RDONLY) == MNT_RDONLY ? "yes" : "no");
  printf("No setuid/setgid = %s\n",
         (buf.f_flags & MNT_NOSUID) ? "yes" : "no");
#endif
  printf("\nFree space = %.0f%%\n",
         (double)buf.f_bfree * 100 / buf.f_blocks);
  return;

EC_CLEANUP_BGN
EC_FLUSH("print_statvfs");
EC_CLEANUP_END
}
```

这是我们在包含目录 `/home/marc/aup` 的文件系统上在 Solaris 上获得的输出（Linux 产生类似的输出）：

```text
block size = 8192
fundamental block (fblock) size = 1024
total number of fblocks = 4473046
number of free fblocks = 3683675
number of avail. fblocks = 3638945
total number of i-numbers = 566912
number of free i-numbers = 565782
number of avail. i-numbers = 565782
file-system ID = 26738695
Read-only = no
No setuid/setgid = no
Max length of filename = 255

Free space = 82%
```

在 FreeBSD 上，对于 `/usr/home/marc/aup`，这是其输出：

```text
block size = 16384
fundamental block size = 2048
total number of fblocks = 1704331
number of free fblocks = 1209974
number of avail. fblocks = 1073628
total number of i-numbers = 428030
number of free i-numbers = 310266
Read-only = no
No setuid/setgid = no

Free space = 71%
```

`statvfs`（或 `statfs`）系统调用是著名的 `df`（“磁盘空闲”）命令的核心（参见练习 3.2）。以下是它在 FreeBSD 上报告的内容：

