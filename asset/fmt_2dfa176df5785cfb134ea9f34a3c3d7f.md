
```c
int main(int argc, char **argv) {
    int fd, nloop;
    int *ptr;
    sem_t *mutex;
    if (argc != 2)
        err_quit("usage: incr_map_anon <loops>");
    nloop = atoi(argv[1]);
    /* 映射到内存 */
    ptr = mmap(NULL, sizeof(int), PRO_READ | PRO_WRITE,
               MAP_SHARED | MAP_ANON, -1, 0);
```

图 12.14 4.4BSD 内存映射。自动变量 `fd` 为零，因为命令行参数指定了创建的文件。我们不再打开文件。`mmap` 调用中指定了 `MAP_ANON` 标志，第五个参数（描述符）为 -1。

## 12.5 SVR4 /dev/zero 内存映射

图 12.15 显示了当我们映射 `/dev/zero` 时，图 12.10 中变化的部分。

```c
int main(int argc, char **argv) {
    int fd, nloop;
    int *ptr;
    sem_t *mutex;
    if (argc != 2)
        err_quit("usage: incr_dev_zero <loops>");
    nloop = atoi(argv[1]);
    /* 打开 /dev/zero, 映射到内存 */
    fd = open("/dev/zero", O_RDWR);
    ptr = mmap(NULL, sizeof(int), PRO_READ | PRO_WRITE, MAP_SHARED, fd, 0);
    close(fd);
```

图 12.15 SVR4 对 `/dev/zero` 的内存映射。

## 引用内存映射对象

自动变量 `fd` 消失了，因为命令行参数指定了创建的文件。我们打开 `/dev/zero` 并在 `map` 调用中使用描述符。我们保证内存映射区域初始化为 0。

当映射普通文件时，内存中的映射大小（`map` 的第二个参数）等于文件的大小。例如，在图 12.12 中，文件大小通过 `write` 设置，而该值也是内存的大小。但这两者——文件大小和映射大小——可能会不同。我们将使用图 12.16 中的程序详细探索 `mmap` 函数。

```c
#include <unistd.h>

int main(int argc, char **argv) {
    int fd;
    char *ptr;
    size_t filesize, mmsize, pagesize;

    if (argc != 4) {
        fprintf(stderr, "usage: %s <filename> <filesize> <mmapsize>\n", argv[0]);
        exit(EXIT_FAILURE);
    }

    /* 打开文件：创建或截断；设置大小 */
    fd = open(argv[1], O_RDWR | O_CREAT | O_TRUNC, FILE_MODE);
    lseek(fd, filesize, SEEK_SET);
    write(fd, "", 1);

    ptr = mmap(NULL, mmsize, PRO_READ | PRO_WRITE, MAP_SHARED, fd, 0);

    pagesize = sysconf(_SC_PAGESIZE);
    printf("pages: %lu\n", pagesize);

    for (size_t i = 0; i < mmsize; i += pagesize) {
        printf("ptr[%lu] = %p\n", i, ptr[i]);
        ptr[i] = 0x1;
        printf("ptr[%lu] = %p\n", i + pagesize, ptr[i + pagesize]);
    }

    printf("ptr[%lu] = %p\n", i);

    exit(0);
}
```

![](img/1541bd224d292c30573e864db3959d59_326_0.png)

## 命令行参数

- 11 命令行参数指定将创建并映射的文件路径、该文件的大小以及内存映射的大小。创建、打开、截断文件：设置大小。
- 12 如果文件不存在则创建，如果已存在则截断为 0。然后通过跳转到大小减一并写入 1 字节将文件大小设置为指定的大小。

## 映射文件

- 16 使用命令行参数映射文件。然后关闭描述符。

## 读取并存储内存映射区域

- 20 读取内存映射区域（页的第一个和最后一个字节）并打印值。我们期望值全为 0。我们将页的第一个和最后一个字节设置为 1。我们期望其中一个引用会产生信号并终止程序。当 `for` 循环结束时（假设程序没有失败），打印页的第一个字节。我们展示种场景是文件大小等于映射大小，但该大小不是页大小的倍数。

```
solaris % l -1 foo
foo: Such file or directory
solaris % test foo 5000 5000
PAGES = 4096
ptr[0] = 0
ptr[4095] = 0
ptr[8191] = 2
Segmentation fault (core)
solaris % l -1 foo
IW-r- 1 returns foo 5000 Mar 20 17:18
000000 001 000 000 000 000 000 000 000 000 000
000016 000 000 000 000 000 000 000 000 000 000
000480 000 000 000 000 000 000 000 000 000 000 001
000496 001 000 000 000 000 000 000 000 000 000 000
000412 110 000 000 000 000 000 000 000 000
```

页大小为 4096 字节，我们能够读取整个第二页（索引 4096 到 8191），但对第三页（索引 8192）的引用会产生 SIGSEGV，这将导致

shell 打印“Segmentation Fault.” 尽管我们将 `p.ptr[8191]` 赋值为 1，但此值并没有被写入文件，文件大小保持为 5000。内核允许我们写入最终页中超出映射范围的区域（因为内核的内存保护是以页为单位工作的），但我们写入该扩展部分的任何内容都不会被写入文件。我们写入索引 0、4095 和 4096 的其他 3 个字节被写回文件，我们通过 `od` 命令对此进行了验证。（`-b` 选项表示以八进制格式打印字节，而 `-A d` 选项表示以十进制打印地址。）图 12.17 描述了这个示例。

![](img/1541bd224d292c30573e864db3959d59_328_0.png)

**图 12.17** `mmap` 大小等于文件大时的内存映射。

如果在 Digital Unix 下运行我们的示例，我们会看到类似的结果，但页大小为 8192。

```
alpha % ls -1 foo
foo: not found
alpha % test1 foo 5000 5000
PAGESIZE = 8192
ptr[0] = 0
ptr[8191] = 0
Memory fault (coredump)
alpha % ls -1 foo
1 retevanes operator 5000
--rw-r--r Mar 21 08:04 00
```

我们仍然能够引用内存映射区域的末尾，但在该内存页内部（索引 5000 到 8191）。正如我们预期的，引用 `ptr[8192]` 会产生 SIGSEGV。

在接下来的 12.17 示例中，我们指定的内存映射大小（15000 字节）大于文件大小（5000 字节）。

```
solaris % rm foo
solaris % test1 foo 5000 15000
PAGESIZE = 4096
ptr[0] = 0
ptr[4095] = 0
ptr[4096] = 0
```

# 共享内存介绍

```
ptr[8191] = 0
Bus Error(coredump)
solaris * 1m -1 foo
-IW-R--R-- 1 stevens other 5000 Mar 20 17:37 foo
```
