
回想第 10 章中介绍的，我们可以通过 `fcntl()` 系统调用指定一个文件为非阻塞的。当一个慢文件是非阻塞的时，`read()` 总是立即返回。如果没有可用数据，它只需返回 0。非阻塞 I/O 通过防止文件操作发生阻塞，为复用提供了一个简单的解决方案。

这里是 `mpx-blocks` 的一个修改版本，它利用非阻塞 I/O 在 `p1` 和 `p2` 之间更平滑地切换。

```c
1: /* mpx-block.c -- 使用非阻塞 I/O 从管道 p1, p2 读取输入
2:    nonblocking input */
3:
4:     #include <fcntl.h>
5:     #include <stdio.h>
6:     #include <unistd.h>
7:
8:     int main(void) {
9:         char buf[4096];
10:        int i;
11:        int fd;
12:
13:
14:        /* 以非阻塞模式打开两个管道 */
15:        if ((fds[0] = open("p1", O_RDONLY | O_NONBLOCK)) < 0) {
16:            perror("open p1");
17:            return 1;
18:        }
19:
20:        if ((fds[1] = open("p2", O_RDONLY | O_NONBLOCK)) < 0) {
21:            perror("open p2");
22:            return 1;
23:        }
24:
25:        fd = 0;
26:        while (1) {
27:    * 如果有可用数据，则读取并显示 */
28:    i = read(fds[fd], buf, sizeof(buf) - 1);
29:    if (i < 0) {
30:        perror("read");
31:        return 1;
32:    } else if (i) {
33:        buf[i] = '\0';
34:        printf("read: %s", buf);
35:    }
36:
37:    * 从另一个文件描述符读取 */
38:    fd = (fd + 1) % 2;
39:
40: }
```

`mpx-nonblock` 和 `mpx-blocks` 之间一个重要的区别是，当其中一个管道正在读取或已关闭时，`mpx-nonblock` 不退出。不幸的是，管道的文件结束（EOF）是通过 `read()` 返回 0 字节来指示，这与空管道上非阻塞 I/O 的结果是相同的！

### 12.1.2 使用 select() 进行复用

为了实现高效复用，Unix 提供了 `select()` 系统调用，它允许进程同时在多个文件描述符上阻塞。进程不再不断检查它感兴趣的每个描述符，而是通过单次系统调用来指定进程想要读取或写入哪些文件描述符。当一个或多个文件有可用数据可读，或者可以接受写入它们的数据时，`select()` 返回，应用程序就可以对这些文件描述符进行读写，而无需担心阻塞。一旦处理完了这些文件，进程就会再次调用 `select()`，该调用将一直阻塞直到某个文件准备好接受更多关注。以下是 `select()` 系统调用的样子：

```c
#include <sys/time.h>
#include <sys/types.h>
#include <unistd.h>
```

```c
int select(int numfds, fd_set * readfds, fd_set * writefds,
    fd_set * exceptfds, struct timeval * timeout);
```

中间三个参数 `readfds`、`writefds` 和 `exceptfds` 指定了应该被监控的文件描述符。每个参数都是指向 `fd_set` 的指针，这是一种允许进程指定任意数量描述符的数据结构。它通过以下宏进行操作：

- `FD_ZERO(fd_set * fds)`: 清空 `fds`——集合中不包含任何文件描述符。该宏用于初始化 `fd_set` 结构。
- `FD_SET(int fd, fd_set * fds)`: 将 `fd` 添加到集合中。
- `FD_CLR(int fd, fd_set * fds)`: 从集合中移除 `fd`。
- `FD_ISSET(int fd, fd_set * fds)`: 如果 `fd` 在集合中，则返回真。

## 12.1 输入输出多路用

已关闭。检查它们后，我们再次对打开的管道执行 `select()`。

以下是 `mpx-select` 示例。
