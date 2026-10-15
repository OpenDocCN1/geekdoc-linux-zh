
# 遍历目录结构

## 搜索目录

通常需要搜索目录以确定该目录包含哪些条目。例如，备份工具在备份时需要访问所有文件和子目录。为此目的，提供了一组从 `opendir(3)` 开始的函数：

```c
/* readdir.c */

#include <stdio.h>

#include <errno.h>

#include <sys/types.h>

#include <dirent.h>

int main(int argc, char *argv[]) {
    DIR dirp = 0;           /* 打开目录 */
    struct dirent *dp;      /* 目录条目 */

    if (argc < 2) {
        fputs("A pathname is required.\n", stderr);
        return 1;
    }

    dirp = opendir(argv[1]); /* 打开目录 */

    if (!dirp) { /* errors? */
        perror("opendir");
        return 2;
    }

    errno = 0; /* 为 readdir(3) 清除 errno */

    while ((dp = readdir(dirp)) != NULL) {
        printf("%s\n", dp->d_name);
        errno = 0;
    }

    if (errno != 0) { /* EOF 还是错误? */
        perror("readdir");
    }

    if (closedir(dirp) == -1) { /* 关闭目录 */
        perror("closedir");
    }

    return 0;
}
```

该程序需要作为一个命令行参数提供一个目录名。示例展示了 FreeBSD 系统上目录 `/etc/ppp` 的列出情况。

## 回到目录开头

为了允许对目录进行多次搜索，必须对打开的目录进行重置。这正是 `rewinddir(3)` 函数实现的功能。

```c
#include <sys/types.h>

#include <dirent.h>

void rewinddir(DIR *dirp);
```

当使用 `opendir(3)` 初始打开目录时，它被隐式地定位在目录的开头。当调用 `rewinddir(3)` 时，打开的目录将重新定位到开头。输入参数 `dir` 只是指向 `opendir(3)` 返回的已打开 `DIR` 结构的指针。`rewinddir(3)` 没有返回值，且该调用没有记录的错误。

以下显示了如何调用该函数：

```c
DIR *dirp;                /* 打开的 DIR 指针 */

rewinddir(dirp);
```

## 在目录内保存位置

可以使用 `telldir(3)` 函数保存目录内的某个位置。该函数的签名概要如下：

```c
#include <sys/types.h>

#include <dirent.h>

long telldir(const DIR *dirp);
```

给定输入 `dirp`（指向 `opendir(3)` 返回的已打开 `DIR` 结构），此函数返回一个目录偏移量，供后续 `seekdir(3)` 使用。如果成功，返回的偏移量大于等于零。如果失败，返回 -1，错误代码位于 `errno` 中。

### 注意

某些 UNIX 平台上 `telldir(3)` 的类型定义可能略有不同。例如，SGI IRIX 6.5 将 `telldir(3)` 定义如下：

```c
off_t telldir (DIR *dirp);
```

注意，返回的偏移量类型为 `off_t`，且输入参数缺少 `const` 关键字。

## 恢复目录内位置

为了根据从之前调用 `telldir(3)` 保存的信息随机定位目录，必须使用 `seekdir(3)` 函数来恢复目录位置。该函数的签名概要如下：

```c
#include <sys/types.h>

#include <dirent.h>

void seekdir(DIR *dirp, long loc);
```

`seekdir(3)` 函数仅接受指向已打开 `DIR` 结构的指针和一个用于恢复目录位置的偏移量 `loc`。此调用不返回成功或错误指示。

示例展示了如何结合使用 `telldir(3)` 和 `seekdir(3)`：

```c
DIR *dirp;                /* 打开的 DIR 指针 */

long dirpos;              /* 目录偏移量 */

dirpos = telldir(dirp);   /* 获取目录中的偏移量 */

seekdir(dirpos);          /* 恢复目录位置 */
```

### 注意

注意某些 UNIX 平台（如 SGI 的 IRIX 6.5）可能使用略不同的 `seekdir(3)` 定义：

```c
void seekdir(DIR *dirp, off_t loc);
```

此定义使用数据类型 `off_t` 作为目录偏移量。

## 扫描目录

虽然从 `opendir(3)` 开始的一系列程序（参见 `directory(3)`）实现了程序员可能需要的的功能，但如果频繁使用，编写代码会有些繁琐。`scandir(3)` 和 `alphasort(3)` 程序的有助于减少程序员的工作量：

```c
#include <sys/types.h>

#include <dirent.h>

scandir(
    const char *dirname,
    struct dirent **namelist,
    int (*select)(struct dirent *),
    int (*compare)(const void *, const void *);

int alphasort(const void *di, const void *d2);
```

`scandir(3)` 函数看起来可能有点人生畏。然而，一旦你花时间研究它，就会发现它很好用。参数 `dirname` 是你想要扫描的目录。参数 `namelist` 指向一个 `struct dirent **` 指针，以便返回目录条目列表。如果你想选择所有目录名，参数 `select` 可以留空（null）。当参数 `compare` 给出空指针时，返回的目录条目是无序的。

成功返回后，`scandir(3)` 返回 `namelist` 数组中的条目数量（可能包含值 0）。发生错误时返回 -1（`errno` 似乎没有被完全记录）。

`alphasort(3)` 函数可以作为参数 `compare` 提供，如果你需要 `namelist` 按照字母顺序排序。

### 注意

`namelist` 数组是动态分配的，当你的程序不再需要它时必须释放。你必须先对数组中的每个条目调用 `free(3)`，然后通过调用 `free(3)` 释放数组本身。

## 为 scandir(3) 声明自己的 select 函数

为 `select` 参数提供的函数指针将接收一个指向 `dirent` 结构的指针。基于此，如果该条目要包含在最终的条目列表中（选中），则函数必须返回非零（真）。如果此函数返回 0（假），则该条目将被排除。以下展示了一个仅选择以 `n` 开头的条目的示例函数。

```c
/*
 * 仅选择以 'h' 开头的目录条目
 */

int
my_select(struct dirent *dp) {
    if (dp->d_name[0] != 'h') {
        return 0;
    } /* 不包含此条目 */
```

`my_select` 会为 `scandir(3)` 找到的每个条目被调用。如果此函数返回 0，则该条目将被排除。

## 为 scandir(3) 声明自己的 compare 函数

为 `compare` 参数提供的函数指针接收两个指向 `dirent` 结构的指针。基于此，如果该条目要包含在最终的条目列表中（选中），则函数必须返回非零（真）。如果此函数返回 0（假），则该条目将被排除。FreeBSD 手页并未清晰地说明了如何解释这些参数。

`seekdir(3)` 函数仅接受指向已打开 `DIR` 结构的指针和一个用于恢复目录位置的偏移量 `loc`。此调用不返回成功或错误指示。

以下示例展示了 `telldir(3)` 和 `seekdir(3)` 如何结合使用：

```c
/*
 * 比较函数示例
 */
int my_compare(const void *d1, const void *d2) {
    struct dirent *dir1 = *(struct dirent **)d1;
    struct dirent *dir2 = *(struct dirent **)d2;
    return strcmp(dir1->d_name, dir2->d_name);
}
```

## SysV 变体

你会发现某些 UNIX 平台以不同的方式定义 `compare` 和 `alphasort(3)`。`seekdir(3)` 如下：

```c
seekdir(DIR *dirp, off_t loc);
```

这里的不同在于 `compare` 指针定义为 `dirent **` 而不是 `void *`。在这种情况下，你应该如下方式定义 `my_compare()`：

```c
int
my_compare(struct dirent **d1, struct dirent **d2) {
    struct dirent *dir1 = *d1;
    struct dirent *dir2 = *d2;
    return strcmp(dir1->d_name, dir2->d_name);
}
```

## scandir(3) 示例

使用 `scandir(3)` 函数的示例位于列表 7.2 中。

### 列表 7.2 scandir.c — 使用 scandir(3) 的程序

```c
#include <stdio.h>

#include <stdlib.h>

#include <unistd.h>

#include <errno.h>

#include <sys/types.h>

#include <dirent.h>

extern int scandir(const char *dirname, struct dirent **namelist,
                   int (*select)(struct dirent *),
                   int (*compare)(const void *, const void *));

extern int alphasort(const void *di, const void *d2);

/*
 * 仅选择以 'h' 开头的目录条目
 * 以演示选择能力：
 */
static int
my_select(struct dirent *dp) {
    if (dp->d_name[0] != 'h') /* 不包含此条目 */
        return 0;
    /* 否则包含此条目 */
    return 1;
}

/*
 * 为了演示目的反序排序
 * 条目：
 */
static int
my_compare(const void *d1, const void *d2) {
    struct dirent *dir1 = *(struct dirent **)d1;
    struct dirent *dir2 = *(struct dirent **)d2;
    return strcmp(dir2->d_name, dir1->d_name);
}

/*
 * 一个很好的测试目录是 /etc：
 */
int main(int argc, char **argv) { /* 工作索引 */
    int x;
    int n;                       /* namelist[n] */
    struct dirent **namelist;    /* List of names */

    if (argc < 2) {
        fprintf(stderr, "A argument is required.\n");
        fprintf(stderr, "Try /etc for the directory.\n");
        return 1;
    }

    /*
     * Scan the directory given :
     * n = scandir(argv[1], &namelist, my_select, my_compare);
     */

    /*
     * Report the directory entries :
     */
    printf("%d entries for %s:\n", n, argv[1]);
    for (int x = 0; x < n; x++) {
        printf("%s\n", namelist[x]->d_name);
    }

    if (n > 0) {
        for (int x = 0; x < n; x++) {
            free(namelist[x]);   /* Release entry */
        }
        free(namelist);         /* Release the array */
    }
    return 0;
}
```

列表 7.2 中的主程序非常直观。第 60 行调用了 `scandir(3)` 函数，用于扫描目录。目录条目列表将返回给指针 `namelist`，该指针在第 49 行声明。`scandir(3)`的条目数量存储在变量 `n` 中，该变量在第 48 行声明。

你之前见过 `my_select()` 函数，例如在第 140 页。`my_compare()` 函数对第 141 页所示的示例进行了微调，以便反向排序条目（第 30–40 行）。

最后，注意 `main()` 程序中第 69–73 行是如何释放分配的存储空间的。所有的数组元素都被释放（第 71 行），然后是数组本身（第 72 行）。

编译并运行程序将得到以下结果：

```bash
$ make scandir
cc -D_POSIX_C_SOURCE=199309L -D_POSIX_C_SOURCE -Wall scandir.c
scandir -o scandir
./scandir

5 entries for /etc:
0: hosts.lpd
1: hosts.equiv
2: hosts.allow
3: hosts
4: hosts.conf
```

使用 `/etc` 目录，你可以看到确实只选中了以 `h` 开头的文件名。得益于自定义排序函数 `my_compare()`，条目也按字母表的反序顺序进行了排序。

# 遍历目录结构

某些 UNIX 平台提供了 `ftw(3)` 函数和更新的 `nftw(3)`，以便更简单地执行文件系统的树遍历。这些函数在 FreeBSD 系统上并不出现，因此这里将提供它们的简要描述。HPXUS-11 的 `ftw(3)` 页面提供了该函数的概要：

```c
#include <ftw.h>

int ftw(const char *path,
    int (*fn)(const char *obj_path,
        const struct stat *obj_stat,
        int obj_flags),
    int depth);

nftw(const char *path,
    int (*fn)(const char *obj_path,
        const struct stat *obj_stat,
        int obj_flags,
        struct FTW *ftw,
    int depth,
    int flags);
```
