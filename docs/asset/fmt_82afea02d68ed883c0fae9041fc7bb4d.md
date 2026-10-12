
这里的逻辑是非常直观的：首先比较姓，然后比较名，如果两个名字相同，则使用员工 ID 号。通过对字符串使用 `strcmp()`，我们自动获得了返回所需的正确负/零/正值。

员工 ID 的比较不能仅使用减法：假设 `long` 是 64 位而 `int` 是 32 位，且两个值仅在高 32 位上不同（例如低 32 位为零）。在这种情况下，减法结果会自动转换为 `int`，从而丢弃高 32 位。

> 注意：我们本可以在比较名时就停止，在这种情况下所有姓和名相同的员工将分在一起，但没有其他的排序。

这一点非常重要：`qsort()` 不保证排序的稳定性。稳定排序是指：如果两个元素根据某些键值（values）比较相等，它们在最终排序数组中的相对顺序将保持原始顺序。例如，考虑三个同名同姓员工，编号分别为 17、42 和 81。（这意味着员工 42 的索引比员工 81 小，而员工 81 的索引又比员工 17 小）。排序后，顺序可能是 81、42 和 17。如果这是一个问题，则比较程序必须考虑所有重要的键值。（我们的程序已经考虑了。）

只需使用一个不同的函数，我们按资历对员工进行排序：

```c
int emp_seniority_compare(const void *elp, const void *e2p) {
    const struct employee *e1, *e2;
    double diff;

    e1 = (const struct employee *)elp;           // 将指针转换为正确的类型
    e2 = (const struct employee *)e2p;
    diff = difftime(e1->start_date, e2->start_date); // 比较时间
    if (diff < 0)
        return -1;
    else if (diff > 0)
        return 1;
    else
        return 0;
}
```

为了最大的可移植性，我们使用了 `difftime()`，它返回两个 `time_t` 值之间的差值。在这种情况下，如：

```c
return (int) difftime(e1->start_date, e2->start_date);
```

![](img/6425.png)

# 2 排序与搜索函数

```
$ ch06-sortemp < presdata.txt
```

按姓名排序：

```
Bush George 41 Fri Jan 20 13:00:00 1989
Bush George 43 Sat Jan 20 13:00:00 2001
Carter James 39 Thu Jan 20 13:00:00 1977
Clinton William 42 Wed Jan 20 13:00:00 1993
Reagan Ronald 40 Tue Jan 20 13:00:00 1981
```

按入职顺序排序：

```
Carter James 39 Thu Jan 20 13:00:00 1977
Reagan Ronald 40 Tue Jan 20 13:00:00 1981
Bush George 41 Fri Jan 20 13:00:00 1989
Clinton William 42 Wed Jan 20 13:00:00 1993
Bush George 43 Sat Jan 20 13:00:00 2001
```

(我们用下午 1.0 p.m. 作为所有人开始工作时间的近似值。)

有一点值得注意：`qsort()` 会重新排列数组中的数据。如果每个元素都是大型结构体，在数组排序时，会有大量数据来回复制。相反，更好的做法是建立一个独立的指针数组，每个指针指向数组中的一个元素。然后使用 `qsort()` 对指针数组进行排序，通过排序后的指针访问未排序的数据。

付出的代价是需要存储指针的额外内存，以及需要修改比较函数以在比较结构体时使用额外的间接层。获得的好处可能是显著的速度提升，因为每一步移动的是四字节或八字节的指针，而不是大型结构体。（我们的 `struct employee` 至少有 68 字节大。交换四字节指针所移动的数据量比交换结构体少 17 倍。）对于数千个内存中的结构体来说，这种差异可能是巨大的。

> 注意 如果你是 C++ 程序员，请小心！对对象数组使用 `qsort()` 可能是危险的！它执行原始内存移动，复制字节。它完全没有感知 C++ 构造，如拷贝构造函数或 `operator=()` 函数。相反，请使用 STL 排序函数之一，或使用独立的指针数组技术。

2 这里显示的输出是美国东部标准时间。如果你使用不同的时区，相同的程序和数据将得到不同的结果。

## 6.2.1.2 示例：排序目录内容

在第 5.3 节“读取目录”第 132 页，我们演示了目录项是按物理顺序返回的。大多数情况下，让目录内容按某种方式排序（例如按名称或修改时间）要有用得多。虽然 POSIX 没有规定，但有几个例程可以使用 `qsort()` 作为底层排序代理来轻松地实现这一点：

```c
#include <dirent.h>

int scandir(const char *dir, struct dirent ***namelist,
    int (*select)(const struct dirent **), int (*compar)(const struct dirent **, const struct dirent **));

int alphasort(const void *a, const void *b);
```

常用

```c
int versionsort(const void *a, const void *b);
```

GLIBC

`scandir()` 和 `alphasort()` 函数在 4.2 BSD 中可用并被广泛支持。³ `versionsort()` 是 GNU 的扩展。

`scandir()` 返回由 `dir` 命名的目录，通过 `malloc()` 创建一个结构体指针数组，并将 `*namelist` 指向该数组的开头。指针数组和所指向的结构体都是通过 `malloc()` 分配的；由调用代码负责 `free()` 以避免内存泄漏。

使用 `select` 函数指针来选择感兴趣的项。当此值为 `NULL` 时，所有有效的目录项都将包含在最终数组中。否则，会对每个项调用 `(*select())`，返回非零（真）的项将包含在数组中。

比较函数比较两个目录项。它被传递给 `qsort()` 用于排序。

`alphasort()` 按字典顺序比较文件名。它使用 `strtok()` 函数进行比较。`strcmp()` 与 `strcmp()` 类似，但它考虑了与区域相关的排序规则（参见第 13.4 节“你能帮我看看吗？”，第 521 页）。

`versionsort()` 是 GNU 的扩展，它使用 GNU `strverscmp()` 函数来比较文件名（参见 `strverscmp(3)`）。简而言之，该函数理解常见的文件名版本控制约定并进行相应的比较。

³ 一个显著异常是 Sun 的 Solaris，那里这两个函数仅于难以使用的 BSD 兼容库中。

## 6.2 排序与搜索函数

`ch06-sortdir.c` 显示了一个类似于 `ch04-catdir.c` 的程序。然而，它使用 `scandir()` 和 `alphasort()` 来完成工作。

```c
/* ch06-sortdir.c --- Demo scandir(), alphasort(). */

#include <stdio.h>    /* 用于 printf() 等. */
#include <errno.h>    /* 用于 errno * */
#include <sys/types.h> /* 用于系统类型 * */
#include <dirent.h> /* 用于目录函数 * */

char *mname;

int process(const char *dir);

/* main -- 遍历参数 */
int main(int argc, char **argv)
{
    int i;
    int errs = 0;
    mname = argv[0];
    if (argc == 1)
        errs = process("."); /* 默认到当前目录 */
    else
        for (i = 1; i < argc; i++)
            errs += process(argv[i]);
    return (errs != 0);
}

/* nodots --- 忽略点文件，供 scandir() 使用 */
int nodots(const struct dirent *dp)
{
    return (dp->d_name[0] != '.');
}

/* process --- 对目录执行某些操作，在这种情况下
 * 在标准输出上打印名称对。
 * 如果成功返回 0，否则返回 1。 */
