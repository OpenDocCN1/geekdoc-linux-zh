
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

9. 大多数现代文件系统将短的符号链接直接存储在 `i` 节点中，而不是占用数据块，但 `st_size` 字段仍然给出大小。

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

在底层，UNIX 系统几乎总是将目录实现为普通文件，只是它们的 `i-mode` 中设置了一个特殊位，并且内核不允许对其写入。在某些系统上，允许使用 `read` 读取目录，但 POSIX 和 SUS 标准并不要求这样做，它们也没有指定目录信息的内部格式。但窥探这些信息很有趣，所以我写了一个小程序来读取当前目录的前 96 个字节，并将这些字节转储为字符（如果它们是可打印的）和十六进制：

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

这是在 Linux 上得到的输出（去掉了“`ec`”跟踪内容）：

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

乍一看这似乎是一堆杂乱的混合物，但仔细一看，它开始变得有意义。可以看到六个名称：`.`、`..`、`m2`、`k`、`pcsync_sig.o` 和 `time.o`。我们知道它们的 `i` 编号也必须包含在内，为了在十六进制中找到它们，我们使用 `ls` 命令的 `-i` 选项以及 `dc`（“桌面计算器”）将十进制转换为十六进制（*斜体注释是后来添加的*）:[10]

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

- `struct dirent`—用于 `readdir` 的结构体

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

这些函数的作用正如你所期望的那样：你从 `opendir` 开始，它会给你一个指向 `DIR` 的指针（类似于调用标准 C 函数 `fopen` 获取指向 `FILE` 的指针）。然后该指针作为其他五个函数的参数使用。你在循环中调用 `readdir`，直到它返回 `NULL`，这意味着如果你没有通过 `readdir` 更改 `errno`，则你已到达末尾；如果更改了，则表示出错。（为了避免混淆，你在调用 `readdir` 之前应该将 `errno` 设置为零。）`readdir` 返回指向 `dirent` 结构体的指针，该结构体包含一个条目的 `i` 编号和名称。完成 `DIR` 的使用后，你用 `closedir` 将其关闭。

`readdir` 在 `d_ino` 字段中返回的 `i-node` 号（`i-number`）实用性不高，因为如果该条目是一个挂载点，返回的将是挂载前的 `i-node` 号，而不是反映当前目录树的 `i-node` 号。例如，在图 3.3（见第 3.3 节）中，对于目录条目 `./y/a`，`readdir` 会返回 `221`，但由于它是一个挂载点，有效的 `i-node` 实际上是 `ad0slm2`（单纯的 `2` 不够具体，因为设备 `ad0s1g` 也有 `i-node` 号 `2`）。`i-node` `221` 甚至无法访问。因此，在读取目录以遍历目录树时（正如我将在第 3.6.4 节中演示如何获取当前目录路径那样），你需要通过调用 `stat` 函数之一来获取目录条目的正确 `i-node` 号，而不是从 `d_ino` 字段中获取。

`rewinddir` 偶尔有用，用于回到目录的开头，这样你就可以在不关闭和重新打开目录的情况下再次读取它。`seekdir` 和 `telldir` 的使用频率较低。`seekdir` 的 `loc` 参数必须是你从 `telldir` 获取的值；你不能假设它是一个条目编号，也不能假设目录条目占用固定宽度的位置，正如我们之前已经看到的。

`readdir` 是那些使用单个静态分配结构体的函数之一，返回的指针指向该结构体。这非常方便，但对于多线程程序并不理想，因此存在一个 `readdir` 的无状态变体，它使用你传入的内存：

### `readdir_r`——读取目录

```c
#include <dirent.h>

int readdir_r(
        DIR *restrict dirp,      /* 来自 opendir 的 DIR 指针 */
        struct dirent *entry,     /* 用于存储条目的结构体 */
        struct dirent **result    /* 结果（指针或 NULL） */
); /* 成功返回 0，出错时返回错误编号（不设置 errno） */
```

你需要向 `readdir_r` 传递一个指向 `dirent` 结构体的指针，该指针的大小必须足以容纳至少 `NAME_MAX` + `1` 个元素的名称。你可以通过调用 `pathconf` 或 `fpathconf`，并传入目录作为参数来获取 `NAME_MAX` 的值，类似于我们在第 3.4 节中获取最大路径长度值所做的事情。`readdir_r` 通过 `result` 参数返回结果；其解释与 `readdir` 的返回值完全相同，但这次你不需要检查 `errno`——错误编号（或零）是函数的返回值。你可以使用 `ec_rv` 宏（第 1.4.2 节）来检查它，就像我在下面这个示例中所做的那样，该示例列出了当前目录中的名称和 `i-node` 号。

```c
static void readdir_r_test(void)
{
    bool ok = false;
    long name_max;
    DIR *dir = NULL;
    struct dirent *entry = NULL, *result;

    errno = 0;
    /* 当 errno == 0 时失败意味着值未找到 */
    ec_negil(name_max = pathconf(".", __PC_NAME_MAX) )
    ec_null( entry = malloc(offsetof(struct dirent, d_name) +
            name_max + 1) )
    ec_null( dir = opendir(".") )
    while (true) {
        ec_rw( readdir_r(dir, entry, &result) )
        if (result == NULL)
            break;
        printf("name: %s; i-number: %ld\n", result->d_name,
                (long)result->d_ino);
    }
    ok = true;
    EC_CLEANUP
    EC_CLEANUP_BGN
        if (dir != NULL)
            (void)closedir(dir);
        free(entry);
        if (!ok)
            EC_FLUSH("*readdir_r_test*");
    EC_CLEANUP_END
}
```

关于这段代码的一些注释：

- `pathconf` 返回 `-1` 且 `errno` 为零意味着目录中名称没有长度限制，但这是不可能的。但我们希望代码能处理这种情况，所以采取了一种简化的方法，将 `errno` 设置为零，然后将所有 `-1` 的返回值视为错误。注释是为了那些实际遇到 `errno` 值为零的错误消息的人准备的。我们的理念是确保代码能够处理不可能的情况，而无需以过于复杂的方式处理它们，反正我们也无法为不可能发生的情况创建测试用例。

- 使用 `malloc` 进行分配很棘手。关于 `dirent` 结构体，我们唯一确定的是 `d_ino` 字段位于其本地位置（可能存在其他非标准字段），并且 `d_name` 位于最后。因此，`d_name` 的偏移量加上我们所需的容量是计算总大小的唯一安全方式，同时考虑了结构体中的空洞（标准 C 允许）和隐藏字段。

- `EC_CLEANUP` 跳转到清理代码，如第 1.4.2 节所述。布尔变量 `ok` 告诉我们是否发生了错误。

真麻烦！使用 `readdir` 要简单得多，如果你不使用多线程，或者能确保每次只有一个线程读取目录，这样做是没问题的：

```c
static void readdir_test(void)
{
    DIR *dir = NULL;
    struct dirent *entry;

    ec_null(dir = opendir("."))
    while (errno = 0, (entry = readdir(dir)) != NULL)
        printf("name: %s; i-number: %ld\n", entry->d_name,
               (long)entry->d_ino);
    ec_nzero(errno)
    EC_CLEANUP

    EC_CLEANUP_BGN
        if (dir != NULL)
            (void)closedir(dir);
        EC_FLUSH("readdir_test");
    EC_CLEANUP_END
}
```

这里的一个棘手之处在于将 `readdir` 的调用塞进 `while` 条件中：逗号表达式的第一部分将 `errno` 置零，第二部分确定整个表达式的值，而 `while` 正是测试这个值。你可能希望有一个密度较低的版本，这也没问题，但不要这样做：

```c
errno = 0;
while ((entry = readdir(dir)) != NULL) { /* 错误 */
    /* 处理条目 */
}
```

因为 `errno` 可能在处理条目的过程中被重置。每次调用 `readdir` 时，你都应该将 `errno` 设置为零。[11]

不管怎样，这里是输出（来自任一示例）的前几行：

`name: . ; i-number: 383072`

`name: .. ; i-number: 383062`

`name: m2 ; i-number: 383074`

`name: k ; i-number: 383097`

> 11. 我知道你在想什么：UNIX 编程难度的一半在于处理 `errno`。你说得对！但别怪我，我只负责传话：参见附录 B 了解一种更简单的方法。

既然我们可以读取目录，让我们将 `readdir` 循环与出现在第 3.5.3 节末尾的 `ls_long` 函数结合起来，以获得一个可以列出目录的 `ls` 命令：
