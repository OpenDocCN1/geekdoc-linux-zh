
运行带有 PID 整数参数的命令将列出所有用户进程的统计信息。若要运行程序并获取其页面的总数，请使用 `/usr/bin/time` 命令。（这可能需要你通过 `sudo apt-get install time` 安装 time 包。你需要知道完整路径，因为 `time` 也是一个内置命令）。现在使用 `/usr/bin/time ls` 查看输出如何报告页异常数量。

注意，Linux 区分了次要异常（minor faults）——页面已驻留但未映射到此进程中（例如多个进程间共享的代码段），以及主异常（major faults）——操作系统需要访问持久性存储设备并从文件中读取数据。

例如，考虑下方的 C 代码。它创建了一个多页数组并访问每个页中的一个字节。随着程序在带有较大尺寸的数组（通过命令行参数增加尺寸）时执行，次要页异常的数量会增加。尝试使用参数 `64000`（256MB 大尺寸的数组）运行它。如果内存不足，程序将终止。

![](img/17ca5177da1b1e15b2169f9c7932e5b6_165_0.png)

```c
#include <stdlib.h>
/* 假设页大小为 4KB */
#define PAGES 1024*4

int main(int argc, char **argv) {
    char *p = 0;
    int i = 0, j = 0;
    /* n 是页的数 {}
    int n = 100;
    if (argc >= 2) {
        n = atoi(argv[1]);
    }
    p = (char *)malloc(PAGES*n);
    for (i=0; i<PAGES; i++) {
        for (j=0;j<PAGES*(n-1); j+=PAGES) {
            p[i+j] = 42;
        }
    }
    return 0;
}
```

现在考虑一个类似的程序，但它使用了内存映射文件，因此操作系统必须从备份存储获取数据。获取一个测试文件，例如：

```
curl -o alice.txt http://www.gutenberg.org/files/11/11-0.txt
```

并编译所示代码。

### 6.5.2 产生大量页异常的程序

```c
#include <assert.h>
#include <fcntl.h>
#include <stdio.h>
#include <sys/mman.h>
#include <sys/stat.h>
#include <unistd.h>

size_t get_size(const char * filename) {
    struct stat st;
    stat(filename, &st);
    return st.st_size;
}

int main(int argc, char **argv) {
    int total = 0;
    size_t filesize = get_size(argv[1]);
    int fd = open(argv[1], O_RDONLY);
    char *data;
    assert(fd != -1);
    posix_fadvise(NULL, 0, filesize, POSIX_DONTNEED);
    data = mmap(NULL, filesize, PROT_READ, MAP_PRIVATE, fd, 0);
    assert(data != MAP_FAILED);
    for (i=0; i<filesize; i+=1024)
        total += data[i];
    printf("total=%d\n", total);
    int rc = munmap(data, filesize);
    assert(rc==0);
    close(fd);
}
```

第一次使用以下命令运行此程序：

`usr/bin/time -v ../out alice.txt 2>&1 | grep Major`

注意，当文件被读入内存时，至少有一个主异常。然而，如果你紧接着再次运行它，将不再有主异常；文件数据已缓存在内存中，因此程序只会引起次要异常。

### 6.5.3 工作集大小

进程的工作集（working set）衡量了该进程为了取得有效进展（即避免频繁交换内存）而必须驻留的页面数量。

有多种文件可以跟踪进程的内存消耗。例如，对于带有 PID 的进程，`/proc/PID/statm` 文件报告了页内存使用情况。第一列显示 `vsize`（虚拟地址空间中分配的页数），第二列显示驻集大小（该进程在物理内存中驻留的页数）。

树莓派上的 Linux 操作系统基础
