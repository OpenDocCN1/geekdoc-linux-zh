
`-m` 选项按修改时间排序，`-s` 按大小排序，`-l` 开启长列表格式。下面的程序清单省略了 ls 之前版本中已经展示过的辅助函数，也几乎省略了所有注释。

```
Listing ls_fts.c
#include <sys/types.h>
#include <err.h>
#include <errno.h>
#include <fnmatch.h>
#include <fts.h>
#include <string.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/stat.h>
#include <pwd.h>
#include <grp.h>
#include "utils.h"

#define BYTIME 1
#define BYNAME 2
#define BYSIZE 3
#define HERE " "
#define TRUE 1
#define FALSE 0

int entcmp(const FTSENT **a, const FTSENT **b)
{
    return strcoll((*a)->fts_name, (*b)->fts_name);
}

int mtimecmp(const FTSENT **s1, const FTSENT **s2)
{
    return (int) (((*s1)->fts_statp)->st_mtime - ((*s2)->fts_statp)->st_mtime);
}

int szcmp(const FTSENT **s1, const FTSENT **s2)
{
    return (int) (((*s1)->fts_statp)->st_size - ((*s2)->fts_statp)->st_size);
}

void ls ( char dir[], int do_longlisting, int sortflag )
{
    FTS *tree;
    FTSENT *f;
    char *argv[] = { dir, NULL };

    switch ( sortflag ) {
    case BYTIME:
        tree = fts_open(argv, FTS_LOGICAL , mtimecmp);
        break;
    case BYNAME:
        tree = fts_open(argv, FTS_LOGICAL , entcmp);
        break;
```

```
case BYSIZE:
    tree = fts_open(argv, FTS_LOGICAL, szcmp);
    break;
}

if (tree == NULL)
    perror("fts_open");

f = fts_read(tree);
if ( NULL == f ) {
    perror("fts_read");
    return;
}

f = fts_children(tree, 0);
if ( NULL == f )
    if ( errno != 0 )
        perror("fts_children");
    else
        fprintf(stderr, "empty directory\n");

while ( f != NULL ) {
    switch (f->fts_info) {
    case FTS_DNR:  /* Cannot read directory */
        fprintf(stderr, "Could not read %s\n", f->fts_path);
        continue;
    case FTS_ERR:  /* Miscellaneous error */
        fprintf(stderr, "Error on %s\n", f->fts_path);
        continue;
    case FTS_NS:  /* stat() error */
        fprintf(stderr, "Could not stat %s\n", f->fts_path);
        continue;
    case FTS_DP:
        /* Returned to directory for second time as part of
           post-order visit to directory, so skip it. */
        continue;
    }
    if ( do_longlisting )
        print_file_status(f->fts_name, f->fts_statp);
    else
        printf("%s\n", f->fts_name);

    f = f->fts_link;
}
if (errno != 0)
    perror("fts_read");

if (fts_close(tree) < 0)
    perror("fts_close");
}

/*********************  Main Program *********************************/
int main(int argc, char* argv[])
```

```
{
    int longlisting = 0;
    int howtosort  = BYNAME;
    int ch;
    char options[] = ":lms";
    opterr = 0;

    while (TRUE) {
        ch = getopt(argc, argv, options);
        if ( -1 == ch )
            break;
        switch ( ch ) {
        case 'l':
            longlisting = 1;
            break;
        case 'm':
            if ( howtosort != BYSIZE )
                howtosort = BYTIME;
            else {
                printf("usage: %s [-l] [-m|-s] [files]\n", argv[0]);
                return 1;
            }
            break;
        case 's':
            if ( howtosort != BYTIME )
                howtosort = BYSIZE;
            else {
                printf("usage: %s [-l] [-m|-s] [files]\n", argv[0]);
                return 1;
            }
            break;

        case '?':
            printf("Illegal option ignored.\n");
            break;
        default:
            printf("??? getopt returned character code 0%o ??\n", ch);
            break;
        }
    }

    if ( optind == argc )    /* no arguments; use . */
        ls( HERE, longlisting, howtosort );
    else
        /* for each command line argument, display file */
        while ( optind < argc ) {
            ls( argv[optind], longlisting, howtosort );
            optind++;
        }
    return 0;
}
```

## 说明

- 主程序负责解析选项，并阻止用户同时按大小和修改时间排序，因为同时按这两种方式排序意味着必须对 `fts_children()` 返回的链表重新排序。
- 主程序对每个命令行参数调用一次 `ls()`，而不是把它们组装成一个字符串数组，因为 `ls()` 被设计为只显示单个目录的内容。
- `mtimecmp()` 和 `szcmp()` 函数使用算术运算而不是条件判断。这样运行速度更快，但在非 POSIX 系统上，时间相减可能不起作用。两者都通过访问 `FTSENT` 结构的 `fts_statp` 成员所指向的 `stat` 结构来实现。没有检查该成员是否为 `NULL`。
- `ls()` 首先调用 `fts_open()`。然后调用 `fts_read()`，以便目录对象成为由 `fts_read()` 调用最后读取到的对象，从而确保如果目录非空，`fts_children()` 将返回指向该目录子项列表的指针。
- 与之前的程序不同，这个程序不会反复调用 `fts_read()`。它遍历 `FTSENT` 结构组成的链表，直到到达一个 `NULL` 链接，然后结束。

以上只是对 `fts` 函数的简要概述。它没有展示如何使用 `FTSENT` 结构内部提供给应用程序的钩子。

## 练习

一个不错的练习是使用 fts 实现 `du` 命令，利用 `FTSENT` 结构中可供应用程序使用的成员以及父指针。
