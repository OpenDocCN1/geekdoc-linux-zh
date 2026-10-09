
有意义的。正如我在第 3.5 节中所述，它们在设备 ID 中的编码方式并未标准化，但通常将最右边的 8 位作为次号（minor number）是可行的：

```c
static void print_size(const struct stat *statp)
{
    switch (statp->st_mode & S_IFMT) {
    case S_IFCHR:
    case S_IFBLK:
        printf("%4u,%4u", (unsigned)(statp->st_rdev >> 8),
                (unsigned)(statp->st_rdev & 0xff));
        break;
    default:
        printf("%9lu", (unsigned long)statp->st_size);
    }
}
```

接下来是文件数据修改日期和时间，使用标准 C 函数 `strftime` 来完成繁重的工作。函数 `time` 和 `diff_time` 也在标准 C 中。（参见第 1.7.1 节了解这三个函数。）我们通常不打印年份，除非时间相隔 6 个月，在这种情况下，我们会跳过时间以腾出空间:^8

```c
static void print_date(const struct stat *statp)
{
    time_t now;
    double diff;
    char buf[100], *fmt;

    if (time(&now) == -1) {
        printf(" ??????????????");
        return;
    }

    diff = diff_time(now, statp->st_mtime);
    if (diff < 0 || diff > 60 * 60 * 24 * 182.5) /* 大约 6 个月 */
        fmt = "%b %e %Y";
    else
        fmt = "%b %e %H:%M";
    strftime(buf, sizeof(buf), fmt, localtime(&statp->st_mtime));
    printf(" %s", buf);
}
```

我们最后想要打印的是文件名，它当然不在 stat 结构体中，因为它不在 i 节点中。然而，这一点有点棘手，因为如果名称是符号链接，我们既要打印它，也要打印其内容：

8. 通常，我们的策略是检查所有错误，除了格式化（打印）和打印本身。`diff_time` 是个例外——它是那些没有错误返回值的函数之一。

```c
static void print_name(const struct stat *statp, const char *name)
{
    if (S_ISLNK(statp->st_mode)) {
        char *contents = malloc(statp->st_size + 1);
        ssize_t n;

        if (contents != NULL && (n = readlink(name, contents,
                statp->st_size)) != -1) {
            contents[n] = '\0'; /* 不能假设以 NUL 结尾 */
            printf(" %s -> %s", name, contents);
        }
        else
            printf(" %s -> [can't read link]", name);
        free(contents);
    }
    else
        printf(" %s", name);
}
```

回想一下在第 3.3.3 节中我介绍 `readlink` 时，我指出我们需要知道最长路径名的长度以确定缓冲区的大小。这个函数展示了一种更直接的方法，因为路径的精确大小（不包括 NUL 字节）在符号链接的 `st_size` 字段中.^9 注意，我分配的内存比 `st_size` 多一个字节，但传递给 `readlink` 的是 `st_size`，以确保为 NUL 字节留出空间，以防 `readlink` 不提供该字节，因为它并没有要求这样做。

现在，是大家等待已久的将所有打印功能组合在一起的程序：

```c
int main(int argc, char *argv[])
{
    int i;
    struct stat statbuf;

    for (i = 1; i < argc; i++) {
        ec_neg1( stat(argv[i], &statbuf))
        ls_long(&statbuf, argv[i]);
    }
    exit(EXIT_SUCCESS);

EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
EC_CLEANUP_END
}
```

9. 大多数现代文件系统将短的符号链接直接存储在 i 节点中，而不是占用数据块，但 `st_size` 字段仍然给出大小。

158   第 3 章：高级文件 I/O

```c
static void ls_long(const struct stat *statp, const char *name)
{
    print_mode(statp);
    print_numlinks(statp);
    print_owner(statp);
    print_group(statp);
    print_size(statp);
    print_date(statp);
    print_name(statp, name);
    putchar('\n');
}
```

以下是我们简化的 `ls` 命令的运行效果：

```text
$ auple /dev/tty
crw-rw-rw-  1 root    root      5,    0 Mar 23  2002 /dev/tty
$ auple a.tmp a.out util
lrwxrwxrwx  1 marc    sysadmin  5 Jul 29 13:30 a.tmp -> b.tmp
-rwxr-xr-x  1 marc    sysadmin 8392 Aug  1  2001 a.out
drw-xr-x    3 marc    sysadmin  512 Aug 28 12:26 util
```

注意最后一行，它不知道如何列出一个目录——它只列出作为参数给出的名称。要添加该功能，我们需要了解如何读取目录以获取其链接。这就来了。

## 3.6 目录

本节涵盖读取和删除目录、更改当前目录以及遍历目录树。

### 3.6.1 读取目录

在底层，UNIX 系统几乎总是将目录实现为普通文件，只是它们的 i-mode 中设置了一个特殊位，并且内核不允许对其写入。在某些系统上，允许使用 `read` 读取目录，但 POSIX 和 SUS 标准并不要求这样做，它们也没有指定目录信息的内部格式。但窥探这些信息很有趣，所以我写了一个小程序来读取当前目录的前 96 个字节，并将这些字节转储为字符（如果它们是可打印的）和十六进制：

```c
static void dir_read_test(void)
{
    int fd;
    unsigned char buf[96];
    ssize_t nread;

    ec_neg1( fd = open(".", O_RDONLY) )
    ec_neg1( nread = read(fd, buf, sizeof(buf)) )
    dump(buf, nread);
    return;

    EC_CLEANUP_BGN
    EC_FLUSH("dir_read_test");
    EC_CLEANUP_END
}

static void dump(const unsigned char *buf, ssize_t n)
{
    int i, j;

    for (i = 0; i < n; i += 16) {
        printf("%4d ", i);
        for (j = i; j < n && j < i + 16; j++)
            printf(" %c", isprint((int)buf[j]) ? buf[j] : '.');
        printf("\n ");
        for (j = i; j < n && j < i + 16; j++)
            printf(" %.2x", buf[j]);
        printf("\n\n");
    }
    printf("\n");
}
```

这是在 Linux 上得到的输出（去掉了“ec”跟踪内容）：

```text
*** BISSDIR (21: "Is a directory") ***
```

所以，那里没有运气。但是，在 FreeBSD（和 Solaris）上，有收获：

```text
0     .               .   V
60 d8 05 00 0c 00 04 01 2e 00 00 00 56 d8 05 00
16  .     .   b
0c 00 04 02 2e 2e 00 00 62 d8 05 00 0c 00 08 02
32  m 2   y   k   C
6d 32 00 c0 79 d8 05 00 0c 00 08 01 6b 00 43 c6
48          P c y n c - s
b3 da 05 00 18 00 08 0c 70 63 73 79 6e 63 5f 73
64  i g . o
69 67 2e 6f 00 00 00 00 e3 e3 05 00 10 00 08 06
80  t i m e . o   r
74 69 6d 65 2e 6f 00 c6 72 d8 05 00 0c 00 08 02
```

乍一看这似乎是一堆杂乱的混合物，但仔细一看，它开始变得有意义。可以看到六个名称：`.`、`..`、`m2`、`k`、`pcsync_sig.o` 和 `time.o`。我们知道它们的 i 编号也必须包含在内，为了在十六进制中找到它们，我们使用 `ls` 命令的 `-i` 选项以及 `dc`（“桌面计算器”）将十进制转换为十六进制（斜体注释是后来添加的）:^10

```text
$ ls -ldi . .. m2 k
383072 drwxr-xr-x 2 marc marc 2560 Oct 18 11:02 .
383062 drwxr-xr-x 9 marc marc  512 Oct 14 18:05 ..
383074 -rwxrwxrwx 1 marc marc   55 Jul 25 11:14 m2
383097 -rw-r--r-- 1 marc marc  138 Sep 19 13:28 k
$ dc
160          使输出基数变为 16
383072p     将 i 编号推入栈中并打印它
5D860       dc 以十六进制（基数 16）打印 i 编号
383062p     ... 同上 ...
5D856
q           退出
```

果然，数字 `5D860` 和 `5D856` 出现在转储的第二行（第一个十六进制行）上。每个条目那里还有一些其他数字，例如用于字符串大小等，但我们真的不想挖掘得更深。有一种更好的、标准化的方法来读取目录，使用专门为此目的设计的系统调用：

- `opendir`—打开目录
```c
#include <dirent.h>
DIR *opendir(
    const char *path /* 目录路径名 */
);
/* 返回 DIR 指针，出错时返回 NULL（设置 errno） */
```

- `closedir`—关闭目录
```c
#include <dirent.h>
int closedir(
    DIR *dirp
); /* 来自 opendir 的 DIR 指针 */
/* 成功时返回 0，出错时返回 -1（设置 errno） */
```

- `readdir`—读取目录
```c
#include <dirent.h>
struct dirent *readdir(
    DIR *dirp            /* 来自 opendir 的 DIR 指针 */
);
/* 返回结构体，EOF 或出错时返回 NULL（设置 errno） */
```

- `struct dirent`—用于 readdir 的结构体
```c
struct dirent {
    ino_t d_ino;         /* i 编号 */
    char d_name[];       /* 名称 */
};
```

- `rewinddir`—将目录指针回溯到开头
```c
#include <dirent.h>
void rewinddir(
    DIR *dirp            /* 来自 opendir 的 DIR 指针 */
);
```

- `seekdir`—在目录中定位
```c
#include <dirent.h>
void seekdir(
    DIR *dirp,                 /* 来自 opendir 的 DIR 指针 */
    long loc                  /* 位置 */
);
```

- `telldir`—获取目录位置
```c
#include <dirent.h>
long telldir(
    DIR *dirp                  /* 来自 opendir 的 DIR 指针 */
);
/* 返回位置（无错误返回） */
```

这些函数的作用正如你所期望的那样：你从 `opendir` 开始，它会给你一个指向 `DIR` 的指针（类似于调用标准 C 函数 `fopen` 获取指向 `FILE` 的指针）。然后该指针作为其他五个函数的参数使用。你在循环中调用 `readdir`，直到它返回 `NULL`，这意味着如果你没有通过 `readdir` 更改 `errno`，则你已到达末尾；如果更改了，则表示出错。（为了避免混淆，你在调用 `readdir` 之前应该将 `errno` 设置为零。）`readdir` 返回指向 `dirent` 结构体的指针，该结构体包含一个条目的 i 编号和名称。完成 DIR 的使用后，你用 `closedir` 将其关闭。

