

## 打开和关闭管道

如图所示，数据由写入方写入管道的一端，并由读取方在另一端读取。

![](img/be588b36b489136ce784030a08a1d3d4_359_0.png)

自然，在你能够从管道读取或向管道写入数据之前，管道必须先存在。创建管道的调用是 `pipe`。它的原型在 `<unistd.h>` 中声明如下：

```c
int pipe(int filedes[2]);
```

如果 `pipe` 成功，它会打开两个文件描述符并将其值存储在整数数组 `filedes` 中。第一个描述符 `filedes[0]` 用于读取，因此 `pipe` 使用 `O_RDONLY` 标志来打开它。第二个文件描述符 `filedes[1]` 用于写入，因此 `pipe` 使用 `O_WRONLY` 标志来打开它。如果成功，`pipe` 返回 0；如果发生错误，则返回 -1，同时设置全局错误变量 `errno`。

> `open` 和 `close` 系统调用的语法在第 139 页的“打开和关闭文件”一节中有介绍。

可能的错误条件是 `EMFILE`，意味着调用进程已经打开了太多的文件描述符；`EFAULT`，意味着 `filedes` 数组无效；或者 `ENFILE`，当内核的文件表已满时发生（这绝对是个不好的信号！）。再次强调，文件描述符并不对应于磁盘文件，而是对应于内核中的一个 inode。图 15.3 说明了这一点。

![](img/be588b36b489136ce784030a08a1d3d4_359_1.png)

要关闭管道，使用 `close` 系统调用关闭其相关的文件描述符即可。

## 示例

以下示例展示了如何打开和关闭一个管道：

```c
/*
 * pipopn.c 打开和关闭一个管道
 */
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int fd[2];

    if((pipe(fd)) < 0) {
        perror ("pipe");
        exit(EXIT_FAILURE);
    }
    printf("descriptors are %d, %d\n", fd[0], fd[1]);

    close(fd[0]);
    close(fd[1]);
    exit(EXIT_SUCCESS);
}
```

该程序的输出显示 `pipe` 调用成功（描述符值在你的系统中可能不同）。程序调用 `pipe` 函数，并传入文件描述符数组 `fd`。如果 `pipe` 调用成功，程序会打印文件描述符的整数值，关闭它们，然后退出。

### 输出

```
$ ./pipopn
descriptors are 3, 8
```

## 读取和写入管道

要从管道读取和写入数据，只需使用 `read` 和 `write` 调用。记住，`read` 从 `filedes[0]` 读取，而 `write` 写入到 `filedes[1]`。

> 关于 `read` 和 `write` 系统调用的快速复习，请参阅第 141 页的“读取和写入文件”一节。

话虽如此，一个进程为自己打开管道并没有什么意义。管道用于交换数据。因为进程已经可以访问它将通过管道共享的数据，所以把自己数据共享给自己没有意义。通常，一个进程调用 `pipe`，然后调用 `fork` 生成一个子进程。由于子进程会继承父进程打开的任何文件描述符，因此已经建立了一个 IPC 通道。下一步取决于哪个进程是读取者，哪个是写入者。一般规则是：读取进程关闭管道的写入端，写入进程关闭管道的读取端。以下各项使这一过程更加清晰：

- 如果父进程正在向子进程发送数据，父进程关闭 `filedes[0]` 并写入 `filedes[1]`，而子进程关闭 `filedes[1]` 并从 `filedes[0]` 读取。
- 如果子进程向父进程返回数据，子进程关闭 `filedes[0]` 并写入 `filedes[1]`，而父进程关闭 `filedes[1]` 并从 `filedes[0]` 读取。

图 15.4 应该有助于你可视化正确的程序并记住这条规则。

> **注意**
> 试图同时读写单个管道的两端是一个严重的编程错误。如果两个进程需要全双工管道的功能，父进程必须在 fork 之前打开两个管道。

![](img/be588b36b489136ce784030a08a1d3d4_362_0.png)

图 15.4 的上半部分显示了在 `fork` 后立即出现的文件描述符状态：父进程和子进程都打开了这两个文件描述符。图 15.4 假设父进程将是写入者，子进程将是读取者。图的下半部分说明了在父进程关闭其读取描述符且子进程关闭其写入描述符后，文件描述符的状态。

> **注意**
> 在管道的写入端被关闭后，从该管道读取将返回 0 以表示文件结束。但是，如果读取端已被关闭，任何试图向管道写入的操作都会为写入者生成 `SIGPIPE` 信号，并且 write 调用本身将返回 -1，并将全局变量 `errno` 设置为 `EPIPE`。如果写入进程没有捕获或忽略 `SIGPIPE`，写入进程将会终止。

> 要回顾捕获和忽略信号的方法，请参阅第 102 页的“捕获信号”一节。

## 示例

以下程序 `piperw` 展示了在相关进程之间打开管道的正确步骤。

```c
/**
 * piperw.c - 正确打开管道并
 *        fork 子进程的方式。
 */
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

#include <fcntl.h>
#include <limits.h>

#define BUFSZ PIPE_BUF

void err_quit(char *msg);

int main(int argc, char *argv[])
{
  int fd[2];      /* 管道的文件描述符数组 */
  int fdin;       /* 输入文件的描述符 */
  char buf[BUFSZ];
  int pid, len;

  /* 创建管道 */
  if(pipe(fd) < 0)
    err_quit("pipe");

  /* Fork 并关闭适当的描述符 */
  if((pid = fork()) < 0)
    err_quit("Fork");
  if (pid == 0) {
    /* 子进程是读取者，关闭写入描述符 */
    close(fd[1]);
    while((len = read(fd[0], buf, BUFSZ)) > 0)
      write(STDOUT_FILENO, buf, len);
    close(fd[0]);
  } else {
    /* 父进程是写入者，关闭读取描述符 */
    close(fd[0]);
    if((fdin = open(argv[1], O_RDONLY)) < 0) {
      perror("Open");
      /* 既然无法打开输入，就发送一些内容 */
      write(fd[1], "123\n", 4);
    } else {
      while((len = read(fdin, buf, BUFSZ)) > 0)
        write(fd[1], buf, len);
      close(fdin);
    }
    /* 关闭写入描述符 */
    close(fd[1]);
  }
  /* 回收退出状态 */
  waitpid(pid, NULL, 0);

  exit(EXIT_SUCCESS);
}

void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```

`piperw` 期望一个输入文件的名称，否则它会向读取者发送 `123\n`。使用 `pipopn.c` 作为输入的示例运行产生了以下输出（为了简洁进行了截断）：

### 输出

```
$ ./piperw pipopn.c
/*
 * pipopn.c - 打开和关闭一个管道
 */
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
```

从输出可以看出，`piperw` 的行为很像 `cat` 命令，只是它使用管道而不是简单地将输入显示到 `stdout`。在 `fork` 之后，子进程关闭它继承的写入描述符，因为它只从管道读取。同样，父进程是写入者，所以它关闭其读取描述符。

如果父进程无法打开其输入文件（`argv[1]`），它不会终止程序，而是在关闭之前通过管道发送字符串 `123\n`。当父进程完成向子进程通过管道传输数据后，它会关闭其写入描述符。当子进程从管道读取到 0 个字节时，它会关闭读取描述符。最后，虽然不清楚父进程还是子进程先退出，但父进程调用 `waitpid` 来回收子进程的退出状态，以防止僵尸进程或孤儿进程的产生。

> **注意** 如果多个进程正在向同一个管道写入，每个进程的写入量必须小于 `PIPE_BUF` 字节（这是定义在 `<limits.h>` 中的一个宏），以确保原子写入；也就是说，确保一个进程写入的数据不会与另一个进程的数据混合。作为一条规则陈述，为了确保原子写入，限制每次 write 调用写入的数据量小于 `PIPE_BUF` 字节。

## 更简单的方法

`piperw` 程序做了大量工作只是为了 `cat` 一个文件：创建管道，fork，在父进程和子进程中关闭不需要的描述符，打开输入文件，向管道写入和从管道读取，关闭打开的文件和描述符，然后回收子进程的退出状态。这一系列操作非常常见，因此 ANSI/ISO C 已在标准库函数 `popen` 和 `pclose` 中对其进行了编码，它们在 `<stdio.h>` 中的原型如下：

```c
FILE *popen(const char *command, const char *mode);
int pclose(FILE *stream);
```

`popen` 创建一个管道，然后 fork 一个子进程并随后执行 `exec`，调用 `/bin/sh -c` 来执行 `command` 中包含的命令字符串。`mode` 参数必须是 `r` 或 `w` 之一，其语义与标准 I/O 库中的相同。也就是说，如果 `mode` 是 `r`，则 `FILE`

