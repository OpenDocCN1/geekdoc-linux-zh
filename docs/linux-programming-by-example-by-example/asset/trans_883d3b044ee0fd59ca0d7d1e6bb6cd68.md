

```c
int fd;
void *map;
struct stat statbuf;

/* Open the file to map */
if (argc != 2) {
    puts ("USAGE: mkmap [file]");
    exit(EXIT_FAILURE);
}
if ((fd = open (argv[1], O_RDONLY)) < 0)
    err_quit ("open");

/* Get the file's length for mmap */
fstat (fd, &statbuf);

/* Map the input file */
if ((map = mmap (0, statbuf.st_size, PROT_READ,
        MAP_SHARED, fd, 0)) == MAP_FAILED)
    err_quit ("mmap");
printf ("map created at %p\n", &map);

/* Close and unmap the file */
close (fd);
munmap (map, statbuf.st_size);
exit (EXIT_SUCCESS);
}

void err_quit (char *msg)
{
    perror (msg);
    exit (EXIT_FAILURE);
}
```

`mkmap` 的唯一输出是映射文件的起始地址。虽然这个程序没有实际功能，但它应明确地展示如何映射和取消映射文件。`fstat` 调用使得确定文件大小变得容易，该尺寸随后被作为 `mmap` 调用的长度参数传入。

## 使用映射文件

当然，映射和取消映射文件是一回事，但核心思想是*使用*并操作该文件。本节讨论的调用——`msync`、`mprotect`、`mlock` 系列以及 `mremap`——能够使你完成这些操作。

## 将映射写入磁盘

`msync` 函数将映射文件写入磁盘。其原型如下：

```c
int msync(const void *start, size_t length, int flags);
```

`msync` 将映射中从内存地址 `start` 开始的数据刷新 `length` 字节到磁盘。`flags` 参数是以下一项或多项标志的按位或运算结果：

- `MS_ASYNC` — 安排写入并返回
- `MS_SYNC` — 在 `msync()` 返回前写入数据
- `MS_INVALIDATE` — 使同一文件的其他映射失效，以便它们用新数据更新

## 更改映射保护

`mprotect` 函数修改内存映射的保护标志。其原型如下：

```c
int mprotect(const void *addr, size_t len, int prot);
```

`mprotect` 设置或更改从 `addr` 开始区域的保护级别为 `prot` 中指定的保护级别。`prot` 可以是表 8.1 中列出的一个或多个标志的按位或运算结果。成功时返回 0。如果失败，`mprotect` 返回 −1 并设置 `errno`。

## 锁定映射内存

*内存锁定*是指防止内存区域被交换到磁盘。在 Linux 这样的多任务、多用户系统中，未活跃使用的系统内存（RAM）区域可能会被临时写入磁盘（交换出），以便内存可用于其他用途。锁定内存会设置一个标志，防止其被交换出。有四个函数用于锁定和解锁内存：`mlock`、`mlockall`、`munlock` 和 `munlockall`。它们的原型如下列出：

```c
int mlock(const void *addr, size_t len);
int munlock(void *addr, size_t len);
int mlockall(int flags);
int munlockall(void);
```

要锁定或解锁的内存区域的起始位置由 `addr` 指定。`len` 指示要锁定或解锁该区域的多少部分。`flags` 的值可以是以下一个或两个：

- `MCL_CURRENT` 请求在调用返回前锁定所有页面。
- `MCL_FUTURE` 请求锁定后续添加到进程地址空间的所有页面。

正如在 `mmap` 讨论中提到的，只有具有 root 权限的进程才能锁定或解锁内存区域。

## 调整映射文件大小

你偶尔需要调整内存区域的大小。使用 `mremap` 函数来实现。其原型如下：

```c
void *mremap(void *old_addr, size_t old_len, size_t new_len,
       unsigned long flags);
```

作为 `realloc` 库调用的类似物，`mremap` 将起始于 `old_addr` 的内存区域（原始大小为 `old_len`）调整为 `new_len`。`flags` 指示如果需要，该区域是否可以在内存中移动。`MREMAP_MAYMOVE` 允许地址改变；如果未指定，调整大小操作将失败。`mremap` 返回调整大小后的区域的地址，失败时返回 `NULL`。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_210_0.png)

## 示例

下面的程序 `mmcat` 使用内存映射实现了 `cat` 程序。尽管这是一个朴素的实现，但它清楚地展示了如何使用内存映射文件执行文件 I/O。

```c
/*
 * mmcat.c cat(1) implemented with memory maps
 */

#include <sys/types.h>
#include <sys/mman.h>
#include <sys/stat.h>
#include <unistd.h>
#include <fcntl.h>
#include <stdlib.h>
#include <stdio.h>

void err_quit(char *msg);
```

```c
int main(int argc, char *argv[])
{
    int fd;
    char *src;
    struct stat statbuf;

    /* Open the source file */
    if (argc != 2) {
        puts("USAGE: mmcat (file)");
        exit(EXIT_FAILURE);
    }
    if ((fd = open(argv[1], O_RDONLY)) < 0)
        err_quit("open");

    /* Get the file length for mmap */
    fstat(fd, &statbuf);

    /* map the input file */
    if ((src = mmap(0, statbuf.st_size, PROT_READ,
            MAP_SHARED, fd, 0)) == MAP_FAILED)
        err_quit("mmap");

    /* write it out */
    write(STDOUT_FILENO, src, statbuf.st_size);

    /* clean up */
    close(fd);
    munmap(src, statbuf.st_size);

    exit(0);
}

void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```

文件映射到内存后，`mmcat` 在 `write` 调用中使用字符指针 `src`，就像它是由 `read` 或 `fgets` 填充的一样。我们通过调用 `mmap` 回到内核的内存区域。

> **提示**
> 从实际角度看，在这个例子中使用内存映射文件有些大材小用，因为它在性能或代码长度方面提供的益处很少。然而，在性能至关重要或处理时间敏感操作的情况下，内存映射文件可能是一个明显的优势。内存映射在高度安全的环境下也很有价值。以 root 权限运行的进程可以将映射文件锁定在内存中，防止它们被 Linux 的内存管理器交换到磁盘。结果是，敏感数据（如密码文件或工资数据）就不太容易被扫描程序检测到。当然，在这种情况下，必须将该内存区域设置为 `PROT_NONE`，以便其他进程无法读取该区域。

# 文件锁

文件锁是一种方法，使多个进程能够以安全、合理且可预测的方式同时访问同一个文件。每个锁定文件的进程这样做是为了防止其他进程在它处理文件时修改数据。没有固有的理由阻止两个进程同时从同一文件读取，但想象一下，如果两个进程同时向同一文件写入会发生什么混乱。它们很可能会覆盖彼此的数据，或者在某些情况下完全损坏文件。

如果你想要访问已锁定的文件，一般程序如下列出：

1. 检查锁。
2. 如果文件未锁定，建立你自己的锁。
3. 打开文件。
4. 根据需要处理文件。
5. 关闭文件。
6. 解锁文件。

注意，进程在开始任何 I/O 之前锁定文件，并在解锁文件之前完成所有处理。这种程序确保你的程序执行的所有处理不会受到其他进程的干扰。如果你在建立锁之前打开文件，或者在读取锁之后关闭文件，另一个进程可能会在锁定/解锁操作与打开/关闭操作之间流逝的短暂时间内访问该文件。

如果文件已锁定，你必须做出决定。许多文件 I/O 操作最多只需几秒钟。你可以等待几秒钟——也许使用 `sleep` 调用——然后再试一次，或者放弃并报告给你正在运行该程序的用户，由于另一个进程正在使用该文件，因此无法打开它。

文件锁有两种形式：建议性锁和强制性锁。**建议性锁**，也称为协作性锁，依赖于一种约定，即每个使用锁定文件的进程都会检查锁的存在并尊重该锁。内核或整个系统都不强制实施建议性锁；它们依赖程序员遵守约定。另一方面，**强制性锁*由内核强制执行。内核会阻止对已加写锁文件的读或写访问，直到加锁进程释放锁。然而，强制性锁所付出的代价是显著的性能惩罚，因为每个读或写操作都必须检查锁的存在。

正如文件锁有两种类型，其实现也有两种：锁文件和记录锁定。

## 锁文件

锁文件是长度为零的文件，形式为 `filename.lck`，其中 `.lck` 附加到文件末尾，通常创建在与进程想要打开的文件名相同的目录中。它们很容易实现。为此，你需要一个类似于以下伪代码片段的代码块：

```text
使用 O_EXCL 标志打开锁文件
如果打开失败且 errno == EEXIST
  另一个进程已锁定该文件
否则
  你已锁定该文件
  打开文件本身
  执行额外处理
  关闭文件
  删除（unlink）锁文件
结束 if
```

在打开锁文件时使用 `O_EXCL` 保证 `open` 调用是*原子的*，即 `open` 调用不会在内核中被中断。这很重要，因为当两个进程试图打开同一文件时存在潜在的竞态条件。第二个进程可能会在第一个进程的 `open` 调用被内核中断时打开该文件。使用 `O_EXCL` 可以避免这种情况。如前所述，按照惯例，锁文件命名为 `somefile.lck`，其中 `somefile` 是你正在锁定的文件的名称。

