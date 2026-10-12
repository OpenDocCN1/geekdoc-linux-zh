
> `dirent` 结构中只有一个成员的使用是移植的（即 POSIX 定义其具有可预测的行为，适用于所有符合 POSIX 的系统）：`d_name[]`。所有其他成员都是系统定义且依赖系统的，因此它们的名称和/或包含的数据类型可能因系统而异。例如，某些文件系统仍然将文件名限制为 14 个字符，而其他文件系统（如 `Linux`）则允许多达 256 个字符。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_197_0.png)

接下来的程序 `listdir` 列出命令行中传递的目录名称的内容：

```c
/*  * listdir.c - Read a directory file */
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>

void err_quit(char *msg);

int main(int argc, char *argv[])
{
    DIR *dir;
    struct dirent *mydirent;
    int i = 1;

    if(argc != 2) {
        puts("USAGE: listdir {pathname}");
        exit(EXIT_FAILURE);
    }

    if((dir = opendir(argv[1])) == NULL)
        err_quit("opendir");
    while((mydirent = readdir(dir)) != NULL)
        printf("%3d : %s\n", i++, mydirent->d_name);

    closedir(dir);
    exit(EXIT_SUCCESS);
}

void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```

`while` 循环是这段代码的核心。它反复调用 `readdir` 遍历目录流，直到其返回 `NULL` 并退出循环。在每次迭代中，它打印文件名（`mydirent->d_name`）。以下输出说明了 `listdir` 的行为：

![](img/be588b36b489136ce784030a08a1d3d4_198_0.png)

```
$ ./listdir
  1: .
  2: ..
  3: listdir
  4: Makefile
  5: chgtime.c
  6: 08cd.zip
  7: cwd.c
  8: out
  9: setext2.c
 10: deldir.c
 11: newdir.c
 12: chdir.c
 13: listdir.c
```

## I/O 多路复用

`多路复用`（Multiplexing）是一个价值五美元的词汇，意思是同时从多个文件描述符读取或写入。多路复用的例子包括打开多个网络连接以尽可能多地同时下载网页内容的 `Web` 浏览器，以及同时为数十或数百名用户提供服务的客户端/服务器应用程序。虽然从概念上理解起来很容易，但高效实现多路复用可能很困难。

幸运的是，`Linux` 提供了 `select` 调用以使多路复用更容易。`select` 是一种非资源密集型的手段，用于等待许多文件描述符的状态发生变化。其在 `<unistd.h>` 中的原型如下：

```c
int select(int n, fd_set *readfds, fd_set *writefds, 
       fd_set *exceptfds, struct timeval *timeout);
```

`select` 监视以下文件描述符集合：

- `readfds` 中的描述符集合，用于检查是否有可读字符。
- `writefds` 中的集合，用于检查是否可以写入。
- `exceptfds` 中的集合，用于检查异常情况。

自然地，如果你只对写入大量文件感兴趣，你可能并不关心那些有字符准备就绪的文件描述符集合。事实上，你的程序甚至可能根本不做任何读取。如果情况如此，你可以向该参数传递 `NULL`。例如，要忽略可读的文件描述符和具有某些异常条件（如错误）的文件描述符，你可以按以下方式调用 `select`：

```c
fd_set *writeable_fds;
select(maxfds, NULL, writefds, NULL, 10);
```

`timeout` 参数决定了 `select` 将 `阻塞`（或等待）多长时间，直到它将控制权返回给调用进程。如果 `timeout` 设置为 0，`select` 将立即返回。当 I/O 操作立即返回，而无需等待时，它被称为 `非阻塞` I/O 调用。如果你想等待直到 I/O 操作可以执行（即，直到 `readfds` 或 `writefds` 发生变化）或发生错误，请向 `timeout` 传递 `NULL` 值，使用与前面示例中显示的相同语法。

第一个参数 `n` 包含被监视的任何集合中编号最高的文件描述符加 1（示例程序展示了一种确定此值的方法）。如果发生错误，`select` 返回 -1 并将 `errno` 设置为适当的值。在发生错误时，`select` 还会使所有描述符集合和 `timeout` 无效，因此你需要在重新使用它们之前将它们重置为有效值。如果 `select` 调用成功，它返回被监视的（非 `NULL`）描述符集合中包含的描述符总数，或者 0。返回值为 0 意味着没有发生“有趣”的事情，即没有描述符在 `timeout` 过期之前改变状态。

`select` 的实现还包括四个用于操作描述符集合的例程：

```c
FD_ZERO(fd_set *set);
FD_SET(int fd, fd_set *set);
FD_CLR(int fd, fd_set *set);
FD_ISSET(int fd, fd_set *set);
```

它们的操作如下：

- `FD_ZERO` 清除集合 `set`。
- `FD_SET` 将描述符 `fd` 添加到 `set`。
- `FD_CLR` 将 `fd` 从 `set` 中移除。
- `FD_ISSET` 确定 `fd` 是否在 `set` 中。`FD_ISSET` 是在 `select` 返回后使用的例程，用于确定是否有任何事情发生需要采取行动。如果 `fd` 被设置，则表示其状态在 `select` 调用期间发生了变化（它有字节可读、可写入或发生错误）。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_200_0.png)

以下示例 `mplex` 监视两个命名管道，以获取准备读取的数据（示例程序使用管道，因为它们是在短程序中演示多路复用 I/O 的最简单方式）。

> **注**
>
> 改编自 `mplex-select.c`，最初发表于 `Linux Application Development`，作者 Michael K. Johnson 和 Erik W. Troan（Addison Wesley, 1998），第 213–214 页。
>
> - 命名管道在第 330 页的 "Understanding FIFOs" 中有详细解释。

使用 `mplex` 的最简单方法可能是使用本书网站提供的 `makefile` 来构建它，其中包含了创建管道的规则。否则，首先构建程序，然后使用以下命令创建两个命名管道（在 `mplex` 二进制文件所在的同一目录中）：

```
$ mknod pipe1 p
$ mknod pipe2 p
```

接下来，启动 `mplex`。打开另外两个终端窗口。在第一个窗口中，输入 `cat > pipe1`，在第二个窗口中，输入 `cat > pipe2`。之后你在任一窗口中输入的任何内容都将被排队等待 `mplex` 读取。代码如下：

## 示例
