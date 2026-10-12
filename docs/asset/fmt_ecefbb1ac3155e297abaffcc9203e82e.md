
你可以通过使用`fcntl(fd, F_DUPFD, 0)`来模拟`dup()`返回最低可用文件描述符的行为。如果你记得文件描述符只是内部表格的索引，那么理解这个函数的原理就显而易见了。第三个参数仅提供了内核搜索空闲文件描述符的起始索引。

### 9.4.3.3 文件状态标志和访问模式的操纵

在 4.6.3 节`open()`，第 110 页，我们提供了`open()`接受的`o_xx`标志完整列表。POSIX 按功能对它们进行了分类，如表 9.4 所示。

## 4 文件描述符管理 333

除了模式本身，`O_ACMODE`符号常量是一个掩码，你可以用它从返回值获取文件模式：

```c
fd_flags = fcntl(fd, F_GETFL);

switch (fd_flags & O_ACCESS) {
  case O_RDONLY:
    ... 只读操作...
    break;

  case O_WRONLY:
    ... 只写操作...
    break;

  case O_RDWR:
    ... 读写操作...
    break;
}
```

POSIX 要求`O_RDONLY`、`O_RDWR`和`O_WRONLY`在位位上是相互不同的；如上所示的代码保证有效，并且是确定任意文件描述符模式的简单方法。

通过使用`F_SETFL`你也可以更改这些模式，尽管权限检查仍然有效。根据 GNU/Linux`fcntl(2)`手册，如果文件在打开时已使用了`O_APPEND`，则无法将其清除。

## 9.4.3.4 管道和 FIFOs 的非阻塞 I/O

之前，我们使用了两个人洗碗和干碗的隐喻，用一个水架来描述管道的工作原理：水架满了，洗碗机停止；当它排空时，洗碗机重新开始。这就是阻塞行为：生产者或消费者在`write()`或`read()`调用中阻塞，等待管道有更多空间或等待有更多数据进入。

在现实世界中，等待水架排空或填满的人并不会只是站在那里。相反，空闲的人会去寻找其他厨房任务要做（例如扫掉地板上孩子们掉落的碎屑），直到水架再次就绪。

在 Unix/POSIX 术语中，这种概念被称为非阻塞 I/O。也就是说，I/O 请求完成或返回一个错误值，表示无数据（对于读取者）或无空间（对于写入者）。非阻塞 I/O 适用于管道和 FIFOs，而不适用于普通磁盘文件。它也可以适用于某些设备（如终端）以及网络连接，这两者都超出了本书的范围。

`O_NONBLOCK`标志可以配合`open()`用于指定非阻塞 I/O，并可以通过`fcntl()`设置或清除。对于`open()`和`read()`，非阻塞 I/O 是直观的。

设置或未设置`O_NONBLOCK`打开 FIFO 会显示出以下行为：

- `open("/fifo/file", O_RDONLY, mode)`
  阻塞直到 FIFO 以写入方式打开。

- `open("/fifo/file", O_RDONLY|O_NONBLOCK, mode)`
  打开文件并立即返回。

- `open("/fifo/file", O_WRONLY, mode)`
  阻塞直到 FIFO 以读取方式打开。

- `open("/fifo/file", O_WRONLY|O_NONBLOCK, mode)`
  如果 FIFO 已经以读取方式打开，则打开 FIFO 并立即返回。否则，返回错误（返回 -1 且`errno`设置为`ENXIO`）。

正如普通管道所示，对不再以写入方式打开的 FIFO 进行`read()`将返回文件结束（返回值为 0）。在这种情况下，`O_NONBLOCK`标志是无关。对于空管道或 FIFO，情况变得更有趣：一个仍处于打开状态但内部没有数据的管道：

```c
read(fd, buf, count)，且未设置 O_NONBLOCK

read() 会阻塞直到有更多数据进入管道或 FIFO。
```

```c
read(fd, buf, count)，且设置了 O_NONBLOCK

read() 立即返回 -1，并将 `errno` 设置为 `EAGAIN`
```

最后，`write()`的行为更为复杂。为了讨论它，我们必须首先引入原子写的概念。原子写是指所有请求的数据都一起写入，而不会与其他写入者的数据交织在一起。POSIX 在`<unistd.h>`中定义了常量`PIPE_BUF`。根据我们稍后将涉及的细节，向管道或 FIFO 写入小于或等于`PIPE_BUF`字节的数据要么成功，要么阻塞。`PIPE_BUF`的最小值为`_POSIX_PIPE_BUF`，即 512。`PIPE_BUF`本身可以更大；当前的 GLIBC 系统将其定义为 4096。

在任何情况下，你都应该使用符号常量，而不是期望`PIPE_BUF`在不同系统上具有相同的值。

在所有情况下，对于管道和 FIFOs，`write()`会将数据追加到管道末尾。这是由于管道没有偏移量：它们是不可寻址的。

此外，在所有情况下，如所述，最多`PIPE_BUF`的写入是原子的：数据不会与其他写入的数据交织。大于`PIPE_BUF`字节的写入数据可以在任意边界处与其他写入的数据交织。这意味着你不能期望大量数据中的每个`PIPE_BUF`块都是原子写入的。`O_NONBLOCK`的设置不影响此规则。

与`read()`类似，当未设置`O_NONBLOCK`时，`write()`会阻塞直到所有数据写入完毕。

设置了`O_NONBLOCK`后情况最复杂。对于管道或 FIFO，其行为如下：

| 空间 ≥ nbytes | 空间 < nbytes |
|---|---|
| nbytes ≤ PIPE_BUF | write() 成功 | 返回 -1/EAGAIN |
| 空间 > 0 | 空间 = 0 |
| nbytes > PIPE_BUF | write() 写入能写的 | 返回 -1/EAGAIN |

*(注：源文件中的 OCR 表格存在损坏行，已根据非阻塞管道行为进行重建)*

在任何情况下，当设置了`O_NONBLOCK`时，行为如下：

### 9.4.3.5 fcntl() 总结

`fcntl()`系统调用总结如表 9.5 所示。

| 命令 | 参数 | 返回 |
|---|---|---|
| F_DUPFD | 最新的描述符 | 描述符的副本 |
| F_GETFD | | 获取描述符 |
| F_SETFD | 新值 | 设置描述符 |
| F_GETFL | | 获取文件标志 |
| F_SETFL | 新值 | 设置文件标志 |

复制文件描述符时，创建、状态和访问标志会被复制。执行标志则不会。

## 9.5 示例：gawk 中的双向管道

双向管道双向连接两个进程。通常，对于至少一个进程，标准输入和输出通过管道设置。K shell (`ksh`) 在语言层面引入了双向管道，并称之为协进程（coprocess）：

```bash
database engine command and arguments |&
print -p "database command"
read -p db_response
```

在这里，`database engine`代表任何由前端驱动的后端程序，在本例中为 `ksh` 脚本。`database engine`的标准输入和输出通过两个独立的单向管道与 shell 连接¹。这如图 9.7 所示。

![](img/6452567e31ac7030110673e83f993f4a_372_0.png)

**图 9.7** Korn shell 协进程

在普通的 awk 中，进程管道是单向的：没有方法向程序发送数据并读取响应——你必须使用临时文件。GNU awk (`gawk`) 借用了 `ksh` 的`&`符号来扩展 awk 语言：

```awk
print "a command" | & "database engine"
dabase engine & getline db_response
```

gawk 还将`|&`符号用于 TCP/IP 套接字和 BSD 端口，这些在书中未涵盖。以下来自 gawk 3.1.3 分布中`io.c`的代码

> ³ 同时只有一个带有`read -p`和`print -p`的默认协进程。脚本可以使用`exec`命令配合特殊重定向将协进程的文件描述符移动到特定的数字。一旦完成，就可以启动另一个协进程。

# 338 第 9 章 • 进程管理与管道

这是`two_way_open()`函数中用于设置简单协进程的部分：它创建了两个管道，派生子进程，并处理了所有的文件描述符操作。我们省略了一些无关的代码片段（这个函数比它应该的要大）：

```
1561   static int
1562 two_way_open(const char *str, struct redirect *rp)
1563 {
1827     /* case 3: 通向子进程的双向管道 */
1828     {
```
