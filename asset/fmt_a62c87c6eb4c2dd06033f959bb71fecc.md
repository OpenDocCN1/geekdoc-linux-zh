
```c
perror("Failed to allocate space for consumer");

return 1;

}

for (i = 0; i < numberconsumers; i++) { /* 初始化消费者 */

    if (error = initconsumer(tidc+i)) {

        fprintf(stderr, "Failed to create consumer %d:%s\n", i, strerror(error));

        return 1;

    }

}

for (i = 0; i < numberproducers; i++) { /* 初始化生产者 */

    if (error = initproducer(tidp+i)) {

        fprintf(stderr, "Failed to create producer %d:%s\n", i, strerror(error));

        return 1;

    }

}

sleep(sleeptime); /* 等待一段时间获取部分和 */

if (error = setdone()) {

    fprintf(stderr, "Failed to set done indicator:%s\n", strerror(error));

}

for (i = 0; i < numberproducers; i++) { /* 等待生产者 */

    if (error == pthread_join(tidp[i], NULL)) {

        fprintf(stderr, "Failed producer %d join:%s\n", i, strerror(error));

        return 1;

    }

}

for (i = 0; i < numberconsumers; i++) { /* 等待消费者 */

    if (error == pthread_join(tidc[i], NULL)) {

        fprintf(stderr, "Failed consumer %d join:%s\n", i, strerror(error));

        return 1;

    }

}

if (showresults()) {

    return 0;

}

}
```

# 程序 16.15 randpcscig.c

一个 `main` 创建程序 16.12 的生产者线程和程序 16.13 的消费者线程。线程检测用户何时输入 `SIGUSR1`。

程序 16.15 是 `main` 的一个版本，它创建了 476 页程序 13.14 的信号线程来等待 `SIGUSR1`。程序 13.14 应该链接到 `buffercond.c` 而不是 `doneflag.c`，以便它调用正确的 `setdone`。之后，`main` 使用 `pthread_join` 等待线程完成后再显示结果。

```c
pthread_t *tipd; 

if (argc != 3) {

    fprintf(stderr, "Usage: %s producers consumers\n", argv[0]);

    return 1;

}

numberproducers = atoi(argv[1]);

numberconsumers = atoi(argv[2]);

if (error = signalthreadread(SIGUSR1)) {

    perror("Failed to start signalthread");

    return 1;

}

printf(stderr, "Process %d will run until SIGUSR1 (%d) signal.\n",

    (long)getpid(), SIGUSR1);

tipd = (pthread_t *)calloc(numberproducers, sizeof(pthread_t));

if (tipd == NULL) {

    perror("malloc producer IDs");

    return 1;

}

tidc = (pthread_t *)calloc(numberconsumers, sizeof(pthread_t));

if (tidc == NULL) {

    perror("malloc consumer IDs");

    return 1;

}

for (i = 0; i < numberconsumers; i++) { /* initialize consumers */

    if (error = initconsumer(tidc + i)) {

        fprintf(stderr, "Failed to create consumer %d:%s\n",

            i, strerror(error));

        return 1;

    }

}

for (i = 0; i < numberproducers; i++) { /* initialize producers */

    if (error = initproducer(tipd + i)) {

        fprintf(stderr, "Failed to create producer %d:%s\n",

            i, strerror(error));

        return 1;

    }

}

for (i = 0; i < numberproducers; i++) { /* wait for producers */

    if (error = pthread_join(tipd[i], NULL)) {

        fprintf(stderr, "Failed producer join %d:%s\n",

            i, strerror(error));

        return 1;

    }

}

for (i = 0; i < numberconsumers; i++) { /* wait for consumers */

    if (error = pthread_join(tidc[i], NULL)) {

        fprintf(stderr, "Failed consumer join %d:%s\n",

            i, strerror(error));

        return 1;

    }

}

if (showresults()) {

    return 1;

}

return 0;
```

## 16.7 并行文件复制

本节重新回顾了第 427 页程序 12.8 中的并行文件复制。并行文件复制的简单实现是为每个文件和每个目录创建一个新线程进行复制。当处理大型目录时，这种实现会超出系统资源。本节概述了一种工作池实现，该实现可以限制任何时刻活跃线程的数量。在工作池实现中，固定数量的线程用于处理负载。工作线程在同步点（在本例中为空缓冲区）上阻塞，直到有请求到来（缓冲区中有项）时才开始工作。第 22 章比较了工作池与其他服务器线程策略的性能。

### 16.7.1 并行文件复制生产者

通过创建一个生产者线程函数，该函数接收一个大小为 2 的数组参数，包含目录路径。对于第一个目录中的每个普通文件，生产者打开该文件进行读取，并在第二个目录中打开同名文件进行写入。如果目标目录中已存在同名文件，则应打开并截断它。如果在打开任一文件时发生错误，则关闭两个文件并向标准输出发送一条信息消息。将两个文件描述符和文件名放入缓冲区。使用 `bufferconddone` 实现，以便线程能够优雅地退出。`buffer.h` 包含了 `buffer_t` 的定义，即缓冲区条目的的类型。在此项目中使用以下定义。

```c
typedef struct {
int infd;
int outfd;
char filename[PATH_MAX];
} buffer_t;
```

此版本的程序仅复制普通文件。`filename` 成员应仅包含文件名，不包含路径规格。使用第 152 页第 5.2 节描述的 `opendir` 和 `readdir` 函数来访问源目录。这些函数不是线程安全的，但只有一个生产者线程，且该调用将执行它们。使用第 155 页第 5.2.1 节描述的 `lstat` 函数来确定文件是否为普通文件。如果将 `S_ISREG` 宏应用于 `stat` 结构体的 `st_mode` 字段时返回 `true`，则该文件为普通文件。程序 16.16 显示了一个函数，当 `filename` 代表普通文件时它返回 `true`，否则返回 `false`。

这是一个生产者驱动的边界缓冲区问题。当生产者用来自给定目录的文件名填充缓冲区时，它调用程序 16.11 中的 `setdone` 并退出。

#### 程序 16.16 irregular.c

一个当 `filename` 参数为普通文件时返回 `true` 的函数。

```c
#include <sys/stat.h>
#include <sys/types.h>
int isregular(const char *filename) {
  struct stat buf;
  if (lstat(filename, buf) == -1)
    return 0;
  return S_ISREG(buf.st_mode);
}
```

### 16.7.2 并行文件复制消费者

每个消费者线程从缓冲区读取一个项，将文件从源描述符复制到目标描述符，关闭文件，并向标准输出写入一条消息，给出文件名和复制的完成状态。

注意，生产者和多个消费者都在写入标准输出，这是一个必须保护的临界区域。设计一种原子地写入这些消息的方法。

消费者在检测到完成标志位被设置且缓冲区中没有剩余项时终止，如程序 16.13。

### 16.7.3 并行文件复制主程序

主程序应接收消费者数量以及源目录目录作为命令行参数。应用程序只有一个生产者线程。

主程序应启动线程并使用 `pthread_join` 等待线程完成，如程序 16.15。使用 `gettimeofday` 获取创建第一个线程之前和最后一个连接之后的时间。

尝试不同的缓冲区大小和消费者数量。哪种组合效果最好？注意不要超过文件描述符的进程限制。打开描述符的数量由缓冲区的大小和消费者的数量决定。

### 16.7.4 并行复制

在描述的程序运行正常后，添加以下增强：

- 复制子目录。
- 复制 FIFO。
- 递归复制子目录。
- 统计复制的文件数量和类型。
- 跟踪总字节数。
- 跟踪最短和最长的复制时间。
- 添加一个信号线程，当进程接收到 `SIGUSR1` 时输出已积累的统计数据。

## 16.8 多线程打印服务器

本节开发了一个基于生产者-消费者同步的项目，该项目使用无界缓冲区而非固定大小缓冲区。

大多数系统的 `lp` 命令并不将文件发送到指定的打印机。相反，`lp` 将请求发送到一个称为打印服务器或打印守护进程的进程。打印服务器将请求放入队列并为用户提供一个标识符，以便用户决定取消打印作业。当打印机空闲时，打印服务器开始将文件复制到打印机。

相对于进程执行时间，打印机是慢设备，一个打印服务器进程可以处理许多打印机。类似于处理多个描述符的问题，打印服务问题适用于多线程。图 16.3 显示了多线程打印服务器的示意结构。服务器使用一个专用线程从输入源读取用户请求。请求线程为请求分配空间并将其加入缓冲区。

### 示例 16.11

以下 UNIX 命令将 `file.ps` 输出到名为 `nps` 的打印机。

```
lp -d nps myfile.ps
```

`lp` 命令可能会返回类似下面的请求号。

```
Request nps-358 queued
```

在取消命令中使用 `nps-358` 来删除打印作业。

![](img/74e4d4cf6f07ca029fcde95b6b423fe7_673_0.png)

图 16.3 显示的打印服务器具有处理其打印机的专用线程。每个打印机线程从请求缓冲区中移除一个请求，并将请求中指定的文件复制到打印机。当复制完成后，打印机线程会释放该请求并处理另一个请求。

打印服务器内部的线程需要与单个生产者（请求线程）和多个消费者（打印机线程）进行生产者-消费者同步。缓冲区本身必须受到保护，以确保项以一致的方式被移除和添加。消费者必须对缓冲区中可用的请求进行同步，以防止它们尝试移除不在内存中的请求。请求缓冲区不是无界的，因为请求线程会根据请求的到来动态地为请求分配空间。请求线程可以使用高水位（high-water mark）来限制在阻塞之前所缓存的请求数量。在这种更复杂的情况下，请求线程在缓冲器的预测性索引上进行同步。

为了本次练习，打印服务器的几个方面被简化了。真实的服务器可能从网络端口或通过过程调用接受输入。打印机并不要求完全相同，且真实的请求允许用户通过多种选项来指定打印方式。系统管理员可以安装默认过滤器，作用于特定类型的文件。打印服务器可以分析请求并将它们定向到最适合该任务的打印机。打印请求可能有优先级或其他特征，影响它们的打印方式。各个打印机线程应该响应来自打印机驱动程序的错误条件和状态报告。

本次练习描述了图 16.3 所示示意表示的打印服务器。将待处理请求保留在名为 `items` 的请求缓冲区变量中，方式类似于标准的生产者-消费者问题。本次练习不需要用于 `slots` 的条件变量，因为请求缓冲区可以增长到任意大。用字符串表示打印请求，该字符串由一个整数、一个空格以及指定要打印文件完整路径的字符串组成。

### 16.8.1 请求缓冲区

使用类型为 `prcmd_t` 的节点链表表示请求缓冲区。以下是一个示例定义。

```c
typedef struct pr_struct {
    int owner;
    char filename[PATH_MAX];
    struct pr_struct *nextprcmd;
} prcmd_t;

static prcmd_t *prhead = NULL;
static prcmd_t *prtail = NULL;
static int pending = 0;
static pthread_mutex_t prcmd_mutex = PTHREAD_MUTEX_INITIALIZER;
```

将请求缓冲区数据结构放在单独的文件中，并仅通过以下函数访问。

```c
int add(prcmd_t *node);
```

向请求缓冲区添加一个节点。`add` 函数增加 `pending` 并将节点插入到请求缓冲区的末尾。如果成功，`add` 返回 0。如果失败，`add` 返回 -1 并设置 `errno`。

```c
int remove(prcmd_t **node);
```

从请求缓冲区中移除一个节点。如果缓冲区为空，`remove` 函数将阻塞。如果缓冲区不为空，`remove` 函数递减 `pending` 并从请求缓冲区移除第一个节点。它将 `*node` 指向被移除的节点。如果 `remove` 成功移除了一个节点，它返回 0。如果失败，`remove` 返回 -1 并设置 `errno`。

```c
int getnumber(void);
```

返回请求缓冲区的大小，即 `pending` 的值。

使用程序 16.11 的同步策略，但消除控制槽位数量条件。

### 16.8.2 生产者线程

生产者线程 `getrequests` 将输入请求插入缓冲区。

```c
void *getrequests(void *arg);
```

参数 `arg` 指向一个打开的文件描述符，指定了读取请求的位置。`getrequests` 函数读取要打印文件的用户 ID 和文件名，创建一个 `prcmd_t` 来承载这些信息，并调用 `add` 将其加到打印机列表请求中。如果 `getrequests` 未能分配空间或检测到文件结束（EOF），它将在设置全局错误标志后返回。否则，它将继续监控打开的文件描述符以获取下一个请求。

编写一个主程序来测试 `getrequests`。主程序使用 `STDIN_FILENO` 作为输入创建 `getrequests` 线程。它进入一个循环，等待 `pending` 变为非零。主线程从缓冲区移除下一个请求，并将用户 ID 和文件名写入输出。通过从键盘输入请求来运行该程序。使用从文件重定向的标准输入来测试该程序。

### 16.8.3 消费者线程

每个消费者线程 `printer` 从打印机请求缓冲区中移除一个请求并“打印”它。`printer` 的原型如下：

```c
void *printer(void *arg);
```
