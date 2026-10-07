
`controldriver`进程可以每个进程维护一个事件列表，也可以在单个链列表中存储连接信息。

## 22.5.1 另一种多客户端设计

另一种设计将所有参数放在控制程序中。`multipleclientdriver`程序接收单个命令行参数：与控制驱动程序通信的端口号。建立连接后，控制驱动程序将其命令行参数发送给每个`multipleclientdriver`。由于需要通信（主机名）和数据（所有内容），需要为这些信息指定格式。由于所有机器都是基于 ASCII 字符的，可以发送一个客户端逐字符读取的字符串。另一种方案是通过发送服务器的 IP 地址而不是其名称，以数值形式（网络字节序整数）发送所有数据。

## 22.6 每个请求线程与每个请求进程的实现

本节规定了在磁盘 I/O 不是考虑因素的情况下，用于比较*每个请求线程*（thread-per-request）和*每个请求进程*（process-per-request）服务器实现的程序。编写两个程序，`thread_per_request`和`process_per_request`，并在相同的负载下进行测试。

`thread_per_request`服务器将接收连接的端口号作为命令行参数。主线程监听连接请求，并创建一个分离线程（detached thread）来处理通信文件描述符和线程编号。分离线程调用第 22.4.2 节中的`handle_request`然后退出。

实现一个使用子进程而不是线程来处理请求的程序。`process_per_request`程序与`thread_per_request`左，但主程序会等待子进程执行完成（例如示例 3.13）。在等待时务必使用`WNOHANG`选项，以便服务器能够处理并发的子进程。以负载为函数比较这两种方法的性能。用图表和文字讨论展示你的结果。

## 22.7 线程池策略

线程池策略在执行开始时创建固定数量的工作线程，而不是在每次建立连接时创建一个新线程。与每个请求线程的实现相比，线程池实现具有以下几个优势：

- 创建工作线程的成本仅在启动时产生，且不会随着请求数量的增加而增长。
- 每个请求线程实现不限制并发活动请求的数量，如果请求接连涌入，服务器可能会耗尽文件描述符。线程池实现根据工作线程的数量限制了打开的文件描述符的数量。
- 由于线程池实现对并发活动请求的数量施加了自然限制，因此当大量请求涌入时，它们不太可能导致服务器过载。

编写一个`thread_worker_pool`服务器，将监听端口号和工作线程数量作为命令行参数。在接受任何连接之前创建指定数量的工作线程。每个工作线程均调用`u_accept`并直接处理连接。

尽管 POSIX 规定`accept`应该是线程安全的，但某些系统尚未遵守这一要求。处理此问题的方法之一是自己进行同步。使用单个静态初始化的互斥锁（`mutex`）来保护对`u_accept`的调用。每个线程在调用`u_accept`之前锁定互斥锁，在`u_accept`返回时解锁。这样，同一时间最多只有一个线程在等待连接请求。一旦请求到达，工作线程就会解锁互斥锁，另一个线程就可以开始等待。

## 22.8 带界限缓冲器的线程池

本节描述了一种线程池的实现，该实现在包含客户端通信文件描述符的界限缓冲区上同步（例如，参见第 16.5 节）。服务器是一个生产者，将通信描述符放入环形缓冲区中。工作线程是消费者，等待缓冲区中的通信描述符变得可用。

编写一个`worker_pool_buffer`服务器，它接受三个命令行参数：监听端口号、界限缓冲区的大小以及池中工作线程的数量。工作线程调用`handle_request`函数来处理通信。设计并运行实验以回答以下问题：

1. 连接时间如何取决于界限缓冲区的大小？哪些因素影响结果？
2. 工作线程的数量如何影响服务器的响应字节率？
3. 整体性能对工作线程的数量有多敏感？
4. 线程池何时何时性能优于每个请求线程？

在运行实验之前，写一段讨论，说明不同的实验参数可能如何影响每情况的结果。

## 22.9 进程池

实现一个进程池，其中每个工作进程在`accept`上阻塞。服务器接受两个命令行参数：监听端口号和要派生（fork）的进程进程数量。

比较进程池与第 22.7 节中线程池的连接时间。以负载为函数探索性能。探索混合设计，即线程工作线程池在`accept`上阻塞。每个线程进程都维护一个如第 22.7 节所示的工作线程池。

## 练习题 22.14

你如何确定由`listen`设置的 backlog 值是否影响服务器性能？

答案：

`backlog`在 UICI 中被设置为程序 C.2 中`uici.c`顶部定义的`MAXBACKLOG`常量值。选择让服务器处于中等负载的参数，并使用不同的 backlog 值重新编译。如果没有定义`MAXBACKLOG`，UICI 使用默认值 50。你可以在编译行上使用`-D`选项来定义`MAXBACKLOG`。从该值开始，然后修改它，看看较小或较大的值是否会影响服务器的性能。

## 22.10 磁盘 I/O 的影响

磁盘访问可能比内存访问慢百万倍。本节探讨了磁盘 I/O 对服务器性能的影响。

为了测量这种性能，修改各种服务器以访问磁盘而非内存缓冲区来满足请求。如果你的服务器是从较少数的请求文件中选择，你的测量结果可能是不准确的，因为操作系统会对 I/O 进行缓冲，大多数请求可能从内存而非磁盘得到满足。

一种可能性是创建大量以数字命名的文件，例如 0, 1, 2 等。当请求到达时，服务器可以随机选择其中一个并进行访问。某些用户可能没有足够的磁盘空间。

另一种可能性是使用已存在的系统文件。想法是创建一个这些文件的列表。当请求来临时时，服务器随机选择一个足够满足该请求的文件。必须确保选择过程不会给服务器带来显著负担。

程序 22.1 阐述了一种仔细选择的方法。为了方便访问，程序根据大小的对数创建了不同大小的列表。每个列表包含至少给定大小的文件，但小于该大小的十倍。第一个列表包含至少 10 字节的文件，第二个包含至少 100 字节，以此此类推。每个列表的大小是前一个的十倍。如果服务器接收到 1234 字节的请求，它应该从至少 1000 字节的列表中选择一个文件并从该文件中传输所需的字节数。由于每个文件都是数组而不是链表，服务器使用随机索引直接访问文件名。

程序 22.1 创建了`NUMRANGES`个列表。当`NUMRANGES`等于 5 时，列表包含至少为 10、100、1000、10000 和 100000 字节的文件，makefile 可以安全地满足高达 100,000 字节的请求。makefile 程序收集每个文件的全路径和大小存储在`filename`类型中。只有全路径最多为`MAXPATH`的文件才会被插入列表。`MAXPATH`取值 100 可以选取大多数系统上的几乎所有文件。我们避免使用系统值`PATH_MAX`（该值可能是 1024 或更大），因为这种选择似乎成本太高。

`insertfile`函数首先通过检查`info`参数`FTW_F`来判断传入的是文件而非目录。它还会验证路径是否在列表中，并根据`stat`信息进行检查，以确保文件是一个普通文件。如果满足所有这些条件，`insertfile`会尝试对文件进行非阻塞打开，以确保当前进程对其有访问权限。非阻塞打开保证了尝试操作不会阻塞。如果所有操作均成功，`insertfile`将等待以确定应该将文件放入哪个列表文件中。每个大小为`list`的列表都存储在`filecounts`数组中，该函数会跟踪这些等于列表最大的条目数量。

创建文件后，`makefileinfo`会显示一个计数列表，然后调用`showfiles`显示其中文件的大小和名称。在确认程序运行正常后，注释掉对`showfiles`的调用。

修改程序 22.1，使其供你的服务器使用。用`create_lists`函数替换`main`函数，该函数接受两个参数——其值与程序 22.1 的命令行参数相同。该函数负责创建列表。编写一个额外的函数`openfile`，它接受一个大小作为参数。`openfile`选择一个大小至少等于该参数的文件，打开该文件进行读取并返回文件描述符。如果发生错误，`openfile`返回 -1 并设置`errno`。

修改第 22.6、22.7、22.8 或 22.9 节中的其中一个服务器，使其满足来自磁盘的请求（disk-based requests）。该服务器可能像程序 22.1 那样具有两个额外的命令行参数，并在接受任何连接请求之前创建列表。服务器在创建列表后应该显示一条消息，以便你判断何时启动客户端。将结果与未进行磁盘访问操作的对应服务器的结果进行比较。

# 程序 22.1 makefileinfo.c

该程序通过遍历目录树创建一个文件列表。

```c
#include <fcntl.h>
#include <ftw.h>
#include <limits.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys.h>
#define MAXPATH 100
#define NUMRANGES 5
typedef struct {
    off_t filesize;
    char path[MAXPATH+1];
} fileinfo;
static int filecounts[NUMRANGES];
static fileinfo *files[NUMRANGES];
static int maxnum;
```

```c
static int wichlist(off_t size) {
  int base = 10;
  int limit;
  int lnum;
  if (size < base)
    return -1;
  for (lnum = 0, limit = base*base;
       lnum < NUMRANGES - 1;
       lnum++, limit *= 10)
    if (size < limit)
      break;
  return lnum;
}
```

```c
static int insertfile(const char *path, const struct stat *statbuf) {
  int info;
  int fd;
  int lnum;
  static int numfull = 0;
  if (info != FTW_F)
    return 0;
  if (strlen(path) > MAXPATH)
    return 0;
  if ((statbuf->st_mode & S_IFREG) == 0)
    return 0;
  if ((fd = open(path, O_RDONLY | O_NONBLOCK)) == -1)
    return 0;
  if (close(fd) == -1)
    return 0;
  lnum = wichlist(statbuf->st_size);
  if (lnum < 0)
    return 0;
  if (filecounts[lnum] == maxnum)
    return 0;
  strcpy(files[lnum][filecounts[lnum]].path, path);
  files[lnum][filecounts[lnum]].filesize = statbuf->st_size;
  filecounts[lnum]++;
  if (filecounts[lnum] == maxnum) numfull++;
  if (numfull == NUMRANGES)
    return 1;
  return 0;
}
```

```c
void showfiles(int which) {
  int i;
  fprintf(stderr, "list %d contains %d entry\n", which, filecounts[which]);
  for (i = 0; i < filecounts[which]; i++)
    fprintf(stderr, "%*s:%s\n", i + 6, files[which][i].filesize, files[which][i].path);
}
```

```c
int main(int argc, char *argv[]) {
  int depth = 10;
  int flags = FTW_PHYS;
  int i;
  if (argc != 3) {
    fprintf(stderr, "Usage: %s directory maxnum\n", argv[0]);
    return 1;
  }
  maxnum = atoi(argv[2]);
  for (i = 0; i < NUMRANGES; i++) {
    filecounts[i] = 0;
    files[i] = (fileinfo*)calloc(maxnum, sizeof(fileinfo));
    if (files[i] == NULL) {
        fprintf(stderr, "Failed to allocate memory for list %d\n", i);
        return 1;
    }
  }
  if (nftw(argv[1], insertfile, depth, flags) == -1) {
    perror("Failed to execute nftw");
    return 1;
  }
  printf(stderr, "Max number for range is %d\n", maxnum);
  for (i = 0; i < NUMRANGES; i++) {
    showfiles(i);
  }
  return 0;
}
```

我们测量了在执行单次

```
fprintf(stderr, "this is a test");
```

在练习 22.15 描述的系统中以无缓冲形式显示到屏幕的时间。单次 `fprintf` 大约花费了 `.25 ms`，而输出五个双精度浮数值的 `fprintf` 大约花费了 `.4 ms`。然而，我们发现执行第一个打印语句 10,000 次所需的时间波动很大，范围从 1 到 10 秒不等。请为这种波动性给出可能的解释。

### 答案：

尽管从用户的角度来看，标准错误输出是没有缓冲的，但实际的屏幕设备驱动程序的输出速度会匹配输出设备的速度，随着缓冲区的填充和清空，从 `fprintf` 返回的时间会有显著差异。

考虑到系统处理 1 K 数据包的请求-响应周期大约为 1 ms，而我们正在测量由线程引入的额外开销，因此执行额外的打印语句所需的时间可能是巨大的。`sprintf` 语句在格式化字符串时可能会产生巨大的开销。为了进行精确的测量，你应该避免在计时循环中进行所有打印操作。接下来的两个示例展示了常见的计时循环错误。

## 练习 22.19

在以下测量服务器连接和响应时间的伪代码中，存在了哪些计时错误？如果省略了最后一个赋值语句，会发生什么？

```
get time1
connect to the server
get time2
output time2 - time1
loop
    write request to the server
    read response from the server
    get time3
    output time3 - time2
time2 = time3
```

### 答案：

`time3 - time2` 的输出发生在两个连续 `time3` 值测量之间，该语句位于计时循环中。程序不应该在 `connect` 和第一次 `write` 之间输出 `time2-time1`。更好的方法是将时间保存在一个数组中，并在测量完成后输出它们。如果你省略了 `time2 = time3` 语句，则所有时间都将从会话开始处开始测量。请求-响应周期的估值将没有任何意义。如果你想测量总响应时间，请将获取结束时间的语句移动到循环之外。

## 练习 22.20

在计时期间输出到磁盘是输出到屏幕更好还是更差？

### 答案：

结果有点难预测，无论哪种都不可能好。磁盘访问时间在 10 ms 数量级。然而，磁盘写入并没有直接进入磁盘，而是通常经过缓冲或缓存。如果磁盘不是本地的，而是通过 NFS 挂载的，输出将引入网络流量以及延迟。对于在这种环境中必须在测量期间完成的 I/O，最好使用 `/tmp`，因为它可能位于本地磁盘上。

## 练习 22.21

分别测量请求的发送和响应的接收（如下所示）存在什么问题？

```
get time1
write request
get time2
read response
get time3
sendtime = time2 - time1
receivetime = time3 - time2
```

### 答案：

`sendtime` 并不是消息到达其目的地的时间，而是信息从用户变量拷贝到系统缓冲区的时间，以便网络子系统可以发送它。在客户端-服务器性能的背景下，其拷贝时间通常没有意义。

打印计时循环也可能发生在服务器中，正如下一个示例中的伪代码所示。线程直接向屏幕输出具有在每个请求-响应期间同步所有线程的效果（当线程很多时，效果更糟），从而消除了并行性。使用标志和条件编译来处理调试语句。

## 练习 22.22

为什么以下使用“每个请求一个线程”的服务器线程伪代码在计时测量中存在问题？

```
loop until error:
read request
write response
output a message summarizing the response
close connection
```
