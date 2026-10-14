
```c
void show_info(struct utmp *utbufp) {
    if (utbufp->ut_type != USER_PROCESS ) {
        return;
    }
    printf("%-8.8s", utbufp->ut_name); /* 用户名 */
    printf("%s"); /* 空格 */
    printf("%-8.8s", utbufp->ut_line); /* tty */
    printf("%s"); /* 空格 */
    showtime(utbufp->ut_time); /* 显示时间 */
}
```

```c
#ifdef SHOWHOST
    if (utbufp->ut_host[0] != '\0') {
        printf("%s", utbufp->ut_host); /* 主机 */
    }
#endif
```

```c
    printf("\n"); /* 换行 */
```

```c
void showtime(long time) {
    /* 显示适合人类阅读的时间
       使用 ctime 构建字符串，然后从中提取部分
       注意：%12.12s 打印一个宽度为 12 字符的字符串并限制
       其为 12 个字符 */

    char *cp; /* 用于存储时间的地址 */
    cp = ctime(&time); /* 将时间转换为字符串
    /* 格式如下
    /* Mon Feb 4 00:06:40 EST 1991
    /* 0123456789012 */

    printf("%12.12s", cp+4); /* 从位置 4 提取 12 个字符 */
}
```

## 测试 who2.c

我们编译并运行 `who2.c`。为了方便，我们关闭了 `SHOWHOST` 设置。运行系统的 `who` 并比较输出：

```bash
$ cc who2.c -o who2
$ who2
root     tty0         Jun 30 21:49
user     tty1         Jun 30 21:50
```

## 2.6 项目二：编写 cp (读与写) 53

图 2.4 显示了参与者和数据流：

![](img/99837708330d437de319a559cfa6cda7_73_0.png)

文件位于磁盘上，原始文件在左侧，副本在右侧。进程运行在用户空间中。缓冲区（`buffer`）是进程内部的一块内存。进程有两个文件描述符。字节从原始文件读取到缓冲区，然后从缓冲区写入副本文件文件中。

最后，这里是实现该图示的代码：

```c
/* cpl.c
* cp 的版本 1 - 使用带有可调缓冲区大小的 read 和 write
*
* 用法: cpl 源 目的
 */
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>

#define BUFFERSIZE 4096
#define COPYMODE 0644

void oops(char *, char *);

main(int ac, char *av[]) {
    int in_fd, out_fd, n_chars;
    char buf[BUFFERSIZE];    /* check args */
    if (ac != 3) {
        printf(stderr, "usage: %s source destination\n", *av);
        exit(1);
    }
    /* 打开文件 */
    if ((in_fd=open(av[1], O_RDONLY)) == -1) {
        oops("Cannot open *", av[1]);
    }
    if ((out_fd=creat(av[2], COPYMODE)) == -1) {
        oops("Cannot create *", av[2]);
    }
    /* 拷贝文件 */
```

```c
while ( ( n_chars = read(in_fd , buf, BUFFERSIZE)) > 0 )
    if ( write(out_fd, buf, n_chars ) != n_chars )
        oops("Write error to *", av[2]);
    if ( n_chars == -1)
        oops("Read error from *", av[1]);

    /* 关闭文件 */

    if ( close(in_fd) == -1 || close(out_fd) == -1 )
        oops("Error closing files,"");

void oops(char *s1, char *s2)
{
    fprintf(stderr,"Error: %s *", s1);
    perror(s2);
    exit(1);
}
```

编译并测试程序：

```
$ cc cpl.c -o cpl
$ cpl cpl copy.of.cpl
$ ls -l copy.of.cpl
-rw-r--r-- 1 bruce bruce 37419 Jul 23 03:12 copy.of.cpl
-rwxr-xr-x 1 bruce bruce 37419 Jul 23 03:08 cpl
$ cpl cpl copy.of.cpl
$
```

这看起来工作得良好。`cmp` 工具比较两个文件并报告差异。这些文件之间没有差异，所以报告没有显示任何内容。

我们的程序对错误的响应如何？首先，我们尝试拷贝一个不存在的文件，然后尝试写入一个目录。结果如下：

```
$ cpl xxx123 file1
Error: Cannot open xxx123: No such file or directory
$ cpl cpl /tmp
Error: Cannot create /tmp: Is a directory
```

测试其他错误情况。阅读系统调用的手册页（`manpages`），查看可能会出现哪些错误，并尝试生成它们。确保你不会覆盖任何你想要保留的文件。

## 2.6.4 Unix 编程看起来相当简单

`who` 是一个从文件读取并格式化数据的程序。`cp` 是一个从一个文件读取并写入另一个文件的程序。两个程序都使用相同的系统调用来连接并传输文件中的出的数据。

## 2.7 更高效的 I/O：缓冲 55

手册和头文件提供了我们理解和编写这些程序所需的所有事实。这种 Unix 编程似乎并不难。我们遗漏了一些问题吗？伴随着学习 Unix 时提出的三个问题，Unix 编程还有另一个问题：我该如何让它运行得更好？

### 2.7 更高效的 I/O：缓冲

`cpl` 包含 `BUFFERSIZE`，它是存储字节从源文件传输到副本文件的数组大小。该值为 4096。我们提出了一个重要的问题：缓冲区的大小重要吗？

### 2.7.1 缓冲区的大小重要吗？

很重要。如果你使用缓冲区将数据从一个地方传输到另一个地方，较大的缓冲区需要更少的传输和更短的时间。考虑一个 2500 字节长度的文件。以下是一些事实：

文件大小 = 2500 字节

如果缓冲区 = 100 字节，则拷贝需要 25 次读写调用

如果缓冲区 = 1000 字节，则拷贝需要 3 次读写调用

将缓冲区大小从 100 更改为 1000 使读写调用次数从25 次减少到 3 次。这重要吗？下表显示了 `cp` 在不同 `BUFFERSIZE` 值下拷贝 5 兆字节文件的执行时间：

| 缓冲区大小 | 执行时间（秒） |
| :--- | :--- |
| 1 | 50.2 |
| 4 | 12.8 |
| 16 | 3.28 |
| 64 | 0.96 |
| 128 | 0.56 |
| 256 | 0.37 |
| 512 | 0.27 |
| 1024 | 0.22 |
| 2048 | 0.19 |
| 4096 | 0.18 |
| 8192 | 0.18 |
| 16384 | 0.18 |

### 2.7.2 为什么系统调用是耗时的

如果你使用缓冲区将数据从一个地方传输到另一个地方，较大的缓冲区需要更少的传输和更短的时间。考虑一个 2500 字节长度的文件。以下是一些事实：

文件大小 = 2500 字节

如果缓冲区 = 100 字节，则拷贝需要 25 次读写调用

如果缓冲区 = 1000 字节，则拷贝需要 3 次读写调用

将缓冲区大小从 100 更改为 1000 使读写调用次数从25 次减少到 3 次。这重要吗？下表显示了 `cp` 在不同 `BUFFERSIZE` 值下拷贝 5 兆字节文件的执行时间：

| 缓冲区大小 | 执行时间（秒） |
| :--- | :--- |
| 1 | 50.2 |
| 4 | 12.8 |
| 16 | 3.28 |
