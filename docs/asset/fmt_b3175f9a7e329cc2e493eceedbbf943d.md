
其代价是需要额外的内存来存储指针，并且修改比较函数以便在比较结构体时使用额外的指针间接引用。带来的好处是速度可能显著提升，因为每一步移动的只是 4 或 8 字节的指针，而不是大型结构体。（我们的 `struct employee` 大小至少为 68 字节。交换 4 字节指针所移动的数据量是交换结构体数据的 1/17。）对于成千上万个内存中的结构体而言，这种差异是显著的。

> **注意** 如果你是 C++ 程序员，请小心！在对象数组中使用 `qsort()` 可能很危险！`qsort()` 执行的是原始内存移动，即复制字节。它完全 unaware C++ 构造，例如拷贝构造函数或 `operator=()` 函数。取而代之的是，使用 STL 的排序函数之一，或者使用独立的指针数组技术。

2 此处显示的输出基于美东标准时间。如果使用不同的时区，运行相同的程序和数据将得到不同的结果。

#### 6.2.1.2 示例：排序目录内容

在第 5.3 节“读取目录”（第 132 页）中，我们展示了目录项是按物理目录顺序返回的。大多数时候，以某种方式（如按名称或修改时间）对目录内容进行排序会更实用。虽然 POSIX 标准并未规定这些例程，但有几个例程使得这样做变得简单，它们使用 `qsort()` 作为底层排序机制：

```c
Common
#include <dirent.h>

int scandir(const char *dir, struct dirent **namelist,
        int (*select)(const struct dirent *),
        int (*compare)(const struct dirent **, const struct dirent **));
int alphasort(const void *a, const void *b);
```

```c
GLIBC
int versionsort(const void *a, const void *b);
```

`scandir()` 和 `alphasort()` 函数是在 4.2 BSD 中可用的，并被广泛支持。³ `versionsort()` 是 GNU 扩展。

`scandir()` 读取名为 `dir` 的目录，使用 `malloc()` 创建一个 `struct dirent` 指针数组，并设置 `*namelist` 指向该数组的开头。指针数组和被指向的 `struct dirent` 结构体都是通过 `malloc()` 分配的；调用代码需要使用 `free()` 来避免内存泄漏。

使用 `select` 函数指针来选择感兴趣的条目。当此值为 `NULL` 时，所有有效的目录条目都包含在最终数组中。否则，对每个条目都会调用 `(*select)()`，只有返回非零（真）的条目才会被包含在数组中。

`compare` 函数指针用于比较两个目录条目。它被传递给 `qsort()` 用于排序。

`alphasort()` 按字典序比较文件名。它使用 `strcoll()` 函数进行比较。`strcoll()` 类似于 `strcmp()`，但会考虑与区域设置相关的排序规则（参见第 13.4 节“请帮我拼写一下这个词好吗？”，第 521 页）。

`versionsort()` 是 GNU 扩展，它使用 GNU `strverscmp()` 函数来比较文件名（参见 `strverscmp(3)`）。简而言之，这个函数理解常见的文件名版本约定，并据此进行比较。

3 一个显著的例外是 Sun 的 Solaris，在那里这两个函数仅存在于难以使用的 BSD 兼容性库中。

`ch06-sortdir.c` 展示了一个与 `ch04-catdir.c` 类似的程序。但是，它使用 `scandir()` 和 `alphasort()` 来完成工作。

```c
/* ch06-sortdir.c --- 演示 scandir(), alphasort(). */

#include <stdio.h>          /* for printf() etc.  */
#include <errno.h>          /* for errno */
#include <sys/types.h>      /* for system types */
#include <dirent.h>         /* for directory functions */

char *myname;
int process(const char *dir);

/* main --- 遍历目录参数 */

int main(int argc, char **argv)
{
    int i;
    int errs = 0;

    myname = argv[0];

    if (argc == 1)
        errs = process(".");  /* 默认为当前目录 */
    else
        for (i = 1; i < argc; i++)
            errs += process(argv[i]);

    return (errs != 0);
}

/* nodots --- 忽略点文件，供 scandir() 使用 */

int
nodots(const struct dirent *dp)
{
    return (dp->d_name[0] != '.');
}

/*
 * process --- 对目录执行操作，在此情况下，
 *             将 inode/名称对打印到标准输出。
 *             如果一切正常返回 0，否则返回 1。
 */

int
process(const char *dir)
{
    DIR *dp;
    struct dirent **entries;
    int nents, i;

    nents = scandir(dir, &entries, nodots, alphasort);
    if (nents < 0) {
        fprintf(stderr, "%s: scandir failed: %s\n", myname,
            strerror(errno));
        return 1;
    }

    for (i = 0; i < nents; i++) {
        printf("%8ld %s\n", entries[i]->d_ino, entries[i]->d_name);
        free(entries[i]);
    }

    free(entries);

    return 0;
}
```

`main()` 程序（第 1–27 行）遵循我们之前使用的标准样板代码。`nodots()` 函数（第 31–35 行）作为 `select` 参数，仅选择不以句点开头的文件名。

`process()` 函数（第 43–65 行）相当简单，大部分工作由 `scandir()` 完成。注意每个元素都是单独通过 `free()` 释放的（第 59 行），并且整个数组也被释放了（第 62 行）。

运行该程序时，目录内容确实按排序顺序输出，且不包括 `.` 和 `..`：

```bash
$ ch06-sortdir        默认行为显示当前目录
2097176 00-preface.texi
2097187 01-intro.texi
2097330 02-cmdline.texi
2097339 03-memory.texi
2097183 03-memory.texi.save
2097335 04-fileio.texi
2097334 05-fileinfo.texi
2097332 06-general1.texi
...
```

#### 6.2.2 二进制搜索：bsearch()

线性搜索大致如其名所示：你从开头开始，遍历正在被搜索的数组，直到找到你需要的东西。对于像查找整数这样简单的事情，这通常表现为一个 `for` 循环。考虑以下函数：

```c
/* ifind --- 线性搜索，找到则返回索引，未找到则返回 -1 */
int ifind(int x, const int array[], size_t nelems)
{
    size_t i;

    for (i = 0; i < nelems; i++)
        if (array[i] == x)  /* 找到了 */
            return i;

    return -1;
}
```

线性搜索的优点是简单；第一次就能正确编写代码很容易。此外，它始终有效。即使元素被添加到数组末尾或从数组中移除，也不需要重新排序数组。

线性搜索的缺点是它速度慢。平均而言，对于包含 `nelems` 个元素的数组，线性搜索随机元素需要在找到目标元素之前进行 `nelems / 2` 次比较。当 `nelems` 变得很大时，即使在现代高性能系统上，这种开销也是不可接受的。因此，你只应在小数组上使用线性搜索。
