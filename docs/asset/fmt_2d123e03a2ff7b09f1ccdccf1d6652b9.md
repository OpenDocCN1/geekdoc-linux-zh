
此函数修改从 `addr` 开始的内存区域的保护属性，修改为 `prot` 中指定的属性，`prot` 是表 14.1 列出的一个或多个标志的按位或结果。成功时返回零，失败时返回 -1 并设置 `errno`。

### 锁定内存

深入了解工作原理，内存锁定意味着防止内存区域被交换到磁盘。在像 Linux 这样的多任务多用户系统中，未使用的系统内存（RAM）区域可能会临时写入磁盘（换出），以便其他用户使用这些内存。锁定内存会设置一个标记，防止其被换出。

有四个用于锁定和解锁内存的：`mlock()`、`mlockall()`、`munlock()` 和 `munlockall()`。它们的原型列如下。

```
int mlock(void *addr, size_t len);
int munlock(void *addr, size_t len);
int mlockall(int flags);
int munlockall(void);
```

要锁定或解锁的内存区域由 `addr` 指定，并指示要锁定或解锁的区域的大小。`flags` 的值可以是 `MCL_CURRENT`（请求在调用返回之前锁定所有页面）和 `MCL_FUTURE`（表示所有页面都应该被锁定）之一或两者。正如讨论 `mmap()` 时提到的，只有具有 root 权限的进程才能锁定或解锁内存区域。

### 使用 mmap() 函数

使用 `mmap()` 函数更改映射文件的大小。该函数使用以下原型：

```
void *mmap(void *old_addr, size_t old_len, size_t new_len, unsigned long flags);
```

你偶尔需要调整内存区域的大小，这就是该函数的作用。与之前讨论的 `realloc()` 类似，`mmap()` 将从 `old_addr` 开始、原始大小为 `len` 的内存区域调整大小为 `new_len`。`flags` 表示在必要时该区域是否可以在内存中移动。`MREMAP_MOVE` 允许地址改变；如果未指定，则调整大小的操作失败。`mmap()` 返回调整后区域的地址，失败时返回 `NULL`。

# 使用内存映射实现 cat(1)

列表 14.2 展示了如何使用内存映射文件。虽然这是一个原始的 `cat(1)` 实现，但它清楚地演示了内存映射文件使用方法。

## 列表 14.2 使用内存映射实现的 cat(1)

```
/*
 * 列表 14.2
 * mmcat.c 使用 mmap() 及其族实现 cat(1) 命令
 */
#include <sys/types.h>
#include <sys/mman.h>
#include <sys/stat.h>
#include <unistd.h>
#include <fcntl.h>
#include <stdlib.h>
#include <stdio.h>

void err_quit(char *msg);

int main(int argc, char *argv[])
{
    int fdin;
    char *src;
    struct stat statbuf;
    off_t len;
    /* 打开输入文件并找到 stdout */
    if(argc != 2)
        err_quit("usage: mmcat <file>");

    if((fdin = open(argv[1], O_RDONLY)) < 0)
        err_quit("open failed");

    /* mmap() 需要输入文件的大小 */
    if((fstat(fdin, &statbuf)) < 0)
        err_quit("fstat failed");

    len = statbuf.st_size;
    /* 映射输入文件 */
    if((src = mmap(0, len, PROT_READ, MAP_SHARED, fdin, 0)) == (void *)-1)
        err_quit("mmap failed");

    /* 输出内容 */
    fprintf(stdout, "%s", src);

    /* 清理 */
    close(fdin);
43 munmap(src, len);
44
45 exit(0);
46 }
47
48 void err_quit(char *msg)
49 {
50 perror(msg);
51 exit(EXIT_FAILURE);
```

该程序中有意思的代码是第 30–39 行。如注释所示，`mmap()` 调用需要输入文件的大小，这里第 30 行的 `fstat()` 调用（`fstat()` 和第 26 行的 `open()`）分别在第 9 章“I/O 例程”和第 10 章“文件操作”中讨论过。一旦我们将文件映射到内存中（第 35 行），就可以完全使用指针 `src`，就像我们用 `read()` 或 `fgets()` 填充它一样，正如我们在第 39 行的 `sprintf()` 语句中所做的那样。我们在第 43 行通过调用 `munmap()` 将内存区域返回给内核。`perror()` 用于工具函数 `err_quit()`，该函数是在第 13 章“处理错误”中引入的。

从实践角度来看，在这个示例中使用映射文件有些大材小用了，因为它在性能或代码长度上并没有带来什么好处。然而，在性能至关重要或我们正在处理时间敏感的操作时，映射文件可以是一个巨大的优势。内存映射在高安全场景下也很有价值。因为以 root 权限运行的进程可以将映射文件锁定到内存中，防止 Linux 内存管理器将其交换到磁盘，像密码文件这样的敏感数据将较不易影响。当然，在这种情况下，内存区域必须设置为 `PROT_NONE`，以便其他进程无法访问该区域。

现在你已经了解了更多关于内存映射的知识，下一节将检查帮助你调试内存问题的工具。

### 查找和修复内存问题

本节涵盖了一些帮助你定位代码中内存管理问题的工具。由于编译器假设你不会出现未初始化内存、缓冲区溢出或越界的情况，本节的工具可以弥补这些缺陷。实际上，大多数编译器接受各种开关，例如 `gcc` 有 `-g` 选项（在第 3 章“GNU”中讨论过），但列表 14.3 存在以下问题：

- 内存泄漏（第 18 行）
- 动态分配堆溢出（第 22 和 28 行）
- 缓冲区越界（第 32 行）
- 重复释放缓冲区（第 36 和 37 行）
- 访问已释放内存（第 40 和 41 行）
- 破坏静态分配栈和全局内存（分别第 48 和 44 行）

## 列表 14.3 带有 BUG 的程序

```
/*

 * 列表 14.3

 * badmem.c 展示内存工具的使用

 */

#include <stdlib.h>

#include <stdio.h>

#include <string.h>

char g_buf[5];

int main(void)

{

    char *buf;

    char *leak;

    char l_buf[5];

    /* 不释放这个 */

    leak = malloc(10);

}
```
/* 稍微溢出 buf */
buf = malloc(5);
strcpy(buf, "abcde");
printf(stdout, "LITTLE : %s", buf);
free(buf);

/* 大量溢出 buf */
buf = malloc(5);
strncpy(buf, "abcdefgh");
printf(stdout, "BIG : %s", buf);

/* 越界 buf */
*(buf - 2) = '\0';
printf(stdout, "UNDERRUN : %s", buf);
free(buf);

/* 重复释放 buf */
free(buf);
free(buf);

/* 访问已释放内存 */
strcpy(buf, "This will blow up");
printf(stdout, "FREE : %s", buf);

/* 破坏全局变量 */
strcpy(g_buf, "global boom");
printf(stdout, "GLOBAL : %s", g_buf);

/* 破坏局部变量 */
strncpy(l_buf, "local boom");
printf(stdout, "LOCAL : %s", l_buf);

exit(0);
```

这些 bug 中的一个阻止了程序的执行，而泄漏和内存破坏通常会在程序的其他地方表现为不可预测的行为。在我的系统中，输出是：

```
$ ./badmem

LITTLE : abcde

BIG : abcdefgh

UNDERRUN : abcdefgh

GLOBAL : global boom
```

在其他系统中，特别是配置了允许 core dump 的系统，示例程序可能会在第二次调用 `free()`（第 37 行）时 dump。

# 使用 mpr 和 check 定位内存问题
