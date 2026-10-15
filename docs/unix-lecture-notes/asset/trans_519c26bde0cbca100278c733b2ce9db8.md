

```c
#include <sys/time.h>
#include <sys/types.h>
#include <unistd.h>

int select(int nfds, fd_set *readfds, fd_set *writefds,
    fd_set *exceptfds, struct timeval *timeout);
```

参数具有以下含义：

**nfds**    感兴趣的潜在文件描述符的数量。

**readfds**    指示进程感兴趣进行*读取*的文件描述符掩码的地址。

**writefds**    指示进程感兴趣进行*写入*的文件描述符掩码的地址。

**exceptfds**    指示进程感兴趣检查*带外*数据的地址的文件描述符掩码。 （带外消息或数据应被视为与读或写描述符掩码中的任何描述符有关的异常或错误条件。）

**timeout**    包含在完成 *select()* 调用之前等待时间的 *timeval* 结构的地址。 如果 timeout 为 *NULL*，则表示无限期等待，即阻塞直到至少有一个描述符就绪。 如果为零，则表示立即返回上述集合中所有描述符的状态。 如果非零，则要么等待指定的时间，要么在指定的描述符之一就绪前返回。

*select()* 调用的返回值是就绪的描述符数量，如果出现错误则为 -1。

*fd_set* 数据类型不一定是标量。 它通常是长整型数组。 如果你稍微深入挖掘一下，你会发现一个常量 *FD_SETSIZE*，它定义了 *fd_set* 中描述符的最大数量，通常在 1024 或更多。 幸运的是，你不需要知道它是如何定义的就可以使用它，因为库中提供了用于操作 *fd_set* 对象的宏和/或函数：

这会关闭由 *fdset* 指向的掩码中描述符 *fd* 的位：

```c
void FD_CLR(int fd, fd_set *fdset);
```

这会在由 *fdset* 指向的掩码中打开描述符 *fd* 的位：

```c
void FD_SET(int fd, fd_set *fdset);
```

这会将由 *fdset* 指向的掩码中的所有位设为零：

```c
void FD_ZERO(fd_set *fdset);
```

这会检查描述符 fd 的位是否在由 fdset 指向的掩码中设置：

```c
int FD_ISSET(int fd, fd_set *set);
```

第一个参数 nfds 的值必须设置为最大文件描述符 + 1 的值，因为文件描述符数组是基于 0 的。 第一个参数是感兴趣的描述符的最大数量的原因是为了效率。 通过向内核提供此数字，可以节省内核复制描述符掩码中不需要的部分的工作。 为了让你了解此调用在简单情况下的使用方法，如果我们想从两个不同的打开文件描述符读取，我们会使用类似

```c
#include <sys/time.h>
#include <sys/types.h>

...

int     fd1, fd2, maxfd;
fd_set  readset, tempset;

fd1  = open("file1", O_RDONLY);  /* open file1 */
fd2  = open("file2", O_RDONLY);  /* open file2*/
maxfd = fd1 > fd2 ? fd1+1 : fd2+1;

FD_ZERO(&readset);        /* clear the bits in the mask  */
FD_SET(fd1, &readset);    /* set the bit for fd1 (file1) */
FD_SET(fd2, &readset);    /* set the bit for fd2 (file2) */
tempset = readset;        /* copy into tempset          */

while ( select(maxfd, &tempset, NULL, NULL, NULL) > 0 ) {
    if ( FD_ISSET(fd1, &tempset) ) {
        /* read from descriptor fd1 */
    }
    if ( FD_ISSET(fd2, &tempset) ) {
        /* read from descriptor fd2 */
    }
    tempset = readset;
}
```

## Notes.

- 虽然我们只对文件描述符 fd1 和 fd2 感兴趣，但使用 select 的正确方法是指定从 0 到 fd1 和 fd2 的最大值范围的描述符。 由于它是基于零的数组，此值为 max(fd1, fd2) + 1。
- 因为 select() 的返回值只要 fd1 或 fd2 上有数据可读就为正，所以循环将一直继续，直到两个文件都到达文件结束。

7 带外是指在单独的通信通道中传输的数据。 带外意味着数据不是与剩余数据按顺序到达，而是在并行通道中到达。 它用于传输错误或控制消息。

