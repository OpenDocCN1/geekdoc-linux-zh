
图 4.31 在运行时确定 `PIPE_BUF` 和 `OPEN_MAX` 的值。

这里是指定不同文件系统的示例：

```
solaris % pipeconf /
PIPE-BUF = 5120, OPEN-MAX = 64
solaris % pipeconf /home
PIPE-BUF = 5120, OPEN-MAX = 64
solaris % pipeconf /tmp
PIPE-BUF = 5120, OPEN-MAX = 64
```
Solaris 2.6 默认值

```
alpha % pipeconf /
PIPE-BUF = 4096, OPEN-MAX = 4096
alpha % pipeconf /var
PIPE-BUF = 4096, OPEN-MAX = 4096
```
Digital Unix 4.0B 默认值

我们现在展示如何使用 Korn-Shell 在 Solaris 下更改 `OPEN_MAX` 的值。

```
solaris % limit -ns
64
solaris % limit -nx
1024
solaris % limit -ns 512
solaris % pipeconf /
PIPE-BUF = 5120, OPEN-MAX = 5120
```

```
display max #descriptors, soft limit
display max #descriptors, hard limit
set soft limit to 512
verify that change has occurred
```

虽然 FIFO 的 `PIPE_BUF` 值可能会根据存储路径的底层文件系统而变化，但这极罕见。

APUE 的第 2 节描述了 `getconf`、`pathconf` 和 `sysconf` 函数，Posix.1 定义了 12 个以 `_SC-` 开头的常量和 52 个以 `_SC_` 开头的常量。Digital Unix 4.0B 扩展了后者，增加了约 100 个可以使用 `sysconf` 查询的非标准常量。

`getconf` 命令由 Posix.2 定义，它打印这些实现的大多数的值。例如

```
alpha % getconf OPEN_MAX
4096
alpha % getconf PIPE_BUF /
4096
```

## 4.12 总结

管道和 FIFO 是许多应用程序的基础构建块。管道通常与 shell 一起使用，但也用于程序内部，通常用于将信息从子进程传回父进程。使用管道涉及的一些代码（`pipe`、`fork`、`close`、`exec` 和 `waitpid`）可以通过 `popclose` 来避免，它处理所有细节并调用 shell。

### 管道和 FIFO

FIFO 类似于管道，但它们通过 `mkfifo` 创建然后通过 `open` 打开。打开 FIFO 时必须小心，因为许多规则（图 4.21）决定了 `open` 调用是否会阻塞。

通过管道和 FIFO，我们查看了一些客户端-服务器设计：一个带有多个客户端的服务器，以及迭代式与并发服务器。迭代服务器一次处理一个客户端请求，以串行方式，这类服务器通常容易受到拒绝服务攻击。并发服务器由另一个进程或线程处理每个客户端请求。

管道和 FIFO 的一个特性是它们的数据是字节流，类似于 TCP 连接。将此字节流划分为记录是……

### 练习题

- 4.1 如果 FIFO 的 `PIPE_BUF` 值取决于存储路径的底层文件系统而变化，这极罕见。
- 4.2 APUE 的第 2 节描述了 `getconf`、`pathconf` 和 `sysconf` 函数，Posix.1 定义了 12 个以 `_SC-` 开头的常量和 52 个以 `_SC_` 开头的常量。Digital Unix 4.0B 扩展了后者，增加了约 100 个可以使用 `sysconf` 查询的非标准常量。
- 4.3 `OPEN_MAX` 的值通过调用 `pathconf` 或 `statconf` 在运行时获取。图 4.31 显示了这两个限制的示例。
- 4.4 `getconf` 命令由 Posix.2 定义，它打印这些实现的大多数的值。
- 4.5 这里是指定不同文件系统的示例……
- 4.6 Solaris 2.6 默认值……
- 4.7 Digital Unix 4.0B 默认值……
- 4.8 我们现在展示如何在 Solaris 下使用 Korn-Shell 更改 `OPEN_MAX` 的值
- 4.9 虽然 FIFO 的 `PIPE_BUF` 值可能会取决于存储路径的底层文件系统而变化，这极罕见。
- 4.10 `getconf` 命令由 Posix.2 定义……
- 4.11 管道和 FIFO 是许多应用程序的基础构建块……
- 4.12 FIFO 类似于管道，但通过 `mkfifo` 创建然后通过 `open` 打开……

## 第 5.2 节

我们在第 2.2 节中描述了关于名称参数的规则。`oflag` 参数是 `O_RDONLY`、`O_WRONLY` 和 `O_RDWR` 之一，并且可以是位组合的：例如 `O_RDWR` 与 `O_CREAT`、`O_EXCL` 和 `O_NONBLOCK`。我们在第 2.3 节中描述所有这些标志。

当创建一个新队列时（指定了 `O_CREAT` 且消息队列不存在），需要 `mode` 和 `attr` 参数。我们在图 2.4 中描述了所使用的 `mode` 值。`attr` 参数允许我们为队列指定某些属性。如果这是一个空指针，则应用默认属性。我们在第 5.3 节中讨论了这些属性。

`mq_open` 的返回值被称为消息队列描述符，但它不需要（也并不是）像文件描述符或套接字描述符那样的小整数。该值用作后续消息队列函数的第一个参数。

Solaris 的 `mq_close_t` 是 `void*`，而 Unix 4.08 将其定义为 `int`。在第 5.8 节的示例实现中，这些描述符是指结构结构的指针。调用错误的数据类型是一个不幸的错误。

消息队列通过 `mq_close` 关闭。

```c
#include <mqueue.h>
int mq_close(mqd_t mqdes);
```
如果成功则返回 0，出错时返回 -1

该功能与打开文件类似：调用进程无法再使用该描述符，但消息队列并不会从系统中移除。当进程终止时，所有打开的消息队列都会被关闭，就像调用了 `mq_close` 一样。

要从系统中移除用作 `mq_close` 参数的名称，必须调用 `mq_unlink`。

```c
#include <mqueue.h>
int mq_unlink(const char *name);
```
如果成功则返回 0，出错时返回 -1

消息队列有一个引用计数，表示它们当前被打开的次数（类似于文件），该函数的作用类似于文件的 `unlink` 函数：在引用计数大于 0 时，名称可以从系统中移除，但队列的销毁（而非从系统中移除其名称）直到最后一次 `mq_close` 发生才会进行。

POSIX 消息队列至少具有内核持久性（回想第 1.3 节）。也就是说，即使没有进程打开该队列，它们也会与写入队列的任何消息一起存在，直到调用 `mq_unlink` 且队列引用计数达到 0 为止。

我们将看到，如果这些消息队列使用内存映射文件（5.2）实现，那么它们就可以具有文件系统持久性，但这并不是强制要求的，且无法依赖它。

### mqcreate1 程序

由于 Posix 消息队列具有内核持久性，我们可以编写一组小型程序来管理这些队列，提供一种易于对其进行实验的方法。图 5.2 中的程序创建了一个消息队列，其名称指定为命令行参数。

```c
1 #include "unipc.h"
2 int
3 main(int argc
```

> 图 5.2 使用指定的独占创建标志创建一个消息队列。

我们允许使用 `-e` 选项来指定独占名称。（我们将在图 5.5 节中详细介绍关于 `getopt` 包装函数的内容。）返回时，`getopt` 存储下一个要处理参数的索引。
我们为来自行的 IPC 消息调用 `mq_open`，而不调用我们的 `px_ipc_name` 函数（第 2.2 节）。这让我们看到实现是如何处理这些 IPC 消息的。（我们在本书中范围内通过我们的简单的测试程序这样做。）

以下是 Solaris 6 上的输出：

```
solaris % mqcreate /tmp.1234               first create
solaris % ls -l /tmp/.1234
-rw-rw-rw- 1 rstevens other 132632 Oct 23 17:08 /tmp/.1234
-rw-rw-rw- 1 rstevens other1 0 Oct 23 17:08 /tmp/.1234.tmp
```
