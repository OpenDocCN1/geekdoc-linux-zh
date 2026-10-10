
```
1: #include <stdio.h>
2: #include <unistd.h>
3: #include <string.h>
4: #include <wait.h>

5: #define MAX_LINE 80

6: int main() {
7: {
8: int thePipe[2], ret;
9: char buf[MAX_LINE+1];
10: const char *testbuf="a test string.";

11: if ( pipe(thePipe) == 0) {

12: if (fork()) == 0) {

13: ret = read(thePipe[0], buf, MAX_LINE);
14: buf[ret] = 0;
15: printf("Child read %s\n", buf);

16: } else {

17: ret = write(thePipe[1], testbuf, strlen(testbuf));
18: ret = wait(NULL);

19: }
20: }
21: }

22: return 0;
23: }
```

到目前为止，这些简单的程序还没有讨论关闭管道，因为在进程结束后，与管道相关的资源会自动释放。尽管如此，良好的编程习惯仍然是使用 `close` 调用来关闭管道的描述符，如下所示：

```
ret = pipe( myPipe );
...
close( myPipe[0] );
close( myPipe[1] );
```

# 第 12 章 管道编程 179

如果管道的写端关闭且进程尝试从管道读取，则将返回 0。这表示管道不再被使用且已关闭。如果管道的读端关闭且进程尝试向其写入，则会产生一个信号。该信号（在第 13 章“套接字编程简介”中将讨论）向管道写入数据的应用程序通常包含一个信号处理器来捕获这种情况。

## dup 和 dup2

`dup` 和 `dup2` 调用是非常实用的函数，提供了复制文件描述符的能力。它们最常用于重定向进程的 stdin、stdout 或 stderr。`dup` 和 `dup2` 的函数原型如下：

```
#include <unistd.h>
int dup(int oldfd);
dup2(int oldfd, int targetfd);
```

`dup` 函数允许你复制一个描述符，并返回一个与第一个描述符完全相同的新描述符。这意味着两个描述符共享相同的内部结构。例如，如果你对一个文件描述符执行了 `lseek`（在文件中寻），那么第二个描述符的文件位置也是相同的。`dup` 函数的使用在下面的代码段所示：

```
int fd1, fd2;
...
fd2 = dup(fd1);
```

在 `fork` 调用之前创建描述符的效果与调用 `dup` 相同。子进程会接收到一个复制的描述符，就像在调用 `dup` 后一样。

`dup2` 函数与 `dup` 类似，但它允许调用者指定一个活跃的描述符和一个目标描述符的 ID。在 `dup2` 成功返回后，新的目标描述符是第一个的副本（targetfd = oldfd）。现在来看一个阐明 `dup2` 的简短代码段：

```
int oldfd;
oldfd = open("app_log", (O_RDWR | O_CREATE, 0644);
dup2(oldfd, 1);
close(oldfd);
```

在这个示例中，你打开了一个名为 app_log 的新文件，并接收了一个名为 fd1 的文件描述符。你使用 `oldfd` 和 `1` 调用了 `dup2`，其效果是将标识为 1 (stdout) 的描述符替换为 `oldfd`（新打开的文件）。任何写入到 stdout 的内容都将写入文件名 app_log 中。请注意，我们在复制它之后直接关闭了 `oldfd`。这不会关闭你新打开的文件，因为描述符 1 指向它。

现在来看一个更复杂的例子。回想在本章前面，你将 `ls` 管道化到你管道的输入。现在在 C 应用程序的背景下探索这个示例（参见列表 12.3）。

**列表 12.3** C 语言管道化（位于 CD-ROM 的 `./source/ch12/dup.c` 中）

```
1: #include <stdio.h>
2: #include <stdlib.h>
3: #include <unistd.h>

4: int main()
5: {
6: int pfds[2];

7: if (pipe(pfds) == 0) {

8: if (fork() == 0) {

9: close(1);
10: dup2(pfds[1], 1);
11: close(pfds[0]);
12: execcl("ls", "ls", NULL);

13:    } else {

14:    close(0);
15:    dup2(pfds[0], 0);
16:    close(pfds[1]);
17:    execcl("wc", "wc", NULL);

18:    }
19:    return 0;
20: }
```

在这个应用程序中，重要的是子进程将其输出重定向到管道的输入。

## mkfifo

`mkfifo` 函数用于在文件系统中创建一个提供 FIFO 功能（也称为命名管道）的文件。本章为止的管道都是匿名管道。它们专门用于进程及其子进程之间。命名管道在系统中可见，因此可以被任何（相关的相关的）进程使用。`mkfifo` 的函数原型如下：

```
#include <sys/types.h>
#include <sys/stat.h>
int mkfifo(const char *pathname, mode_t mode);
```

`mkfifo` 命令需要两个参数。第一个（pathname）是要创建的文件的路径。第二个（mode）代表 FIFO 的权限。`mkfifo` 命令成功时返回 0，失败时返回 -1（并设置 errno）。来看一个使用 `mkfifo` 函数创建文件的示例：

```
int ret;
...
ret = mkfifo("/tmp/cmd_pipe", S_IFIFO | 0666);
if (ret == 0) {
    // 命名管道创建成功
} else {
    // 创建命名管道失败
}
```

## 系统命令

现在是时候查看与 IPC 管道模型相关的系统命令了。`mkfifo` 命令和 `mkfifo` API 函数一样，允许你从命令行创建命名管道。

命名管道 `cmd_pipe` 在当前子目录下创建（类型为 `p` 表示命名管道）。

## 总结

本章对匿名管道和命名管道进行了快速回顾。你回顾了创建管道的应用程序方法和命令行方法，还回顾了通过它们进行通信的典型 I/O 机制。你还回顾了使用 `dup` 和 `dup2` 命令重定向 I/O 的能力。这些命令对管道非常有用，但在许多其他场景中同样有用（任何使用文件描述符的地方，例如套接字或文件）。

# 管道编程 API

```
#include <unistd.h>
int pipe( int filedes[2] );
int dup( int oldfd );
int dup2( int oldfd, int targetfd );
int mkfifo( const char *pathname, mode_t mode );
```

# 13 Socket 编程简介

+ 本章内容

- 理解 Socket 编程范式

- 学习 BSD4.4 Socket API

- 查看 TCP/IP 服务器和客户端的示例源码

- 探索 Socket 的各种功能（控制、I/O、通知）

- 研究说明 Socket API 使用的 Socket 模式

- 探索 SCTP 等其他传输协议

- 查看其他语言中的 Socket 编程

## 引言

本章将快速概览 Socket 编程。它讨论了 Socket 编程范式、Socket 应用程序的元素以及 Socket API。Socket API 允许你开发在网络上通信的应用程序。网络可以是本地私有网络，可以是公共互联网。关于 Socket 编程一个重要的一点是，它既不是特定操作系统的，也不是特定语言的。Socket 应用可以在 GNU/Linux 主机上用 Ruby 脚本语言编写，也可以在嵌入式控制器上用 C 语言编写。这种自由性和灵活性是 BSD4.4 Socket API 如此流行的原因。

层次结构的顶端是主机（Host）。它是网络上的源或目的节点，数据包从这里发送或向这里接收。（从技术上说，你会将接口 视为源或目的，因为主机可能提供多个接口，但本章将保持简单。）主机实现了一套协议。这些协议定义了通信发生的方式。每个协议内部有一组端口（Port）。每个端口定义了一个端点（最终的源或目的）。参见表 13.1 的这些元素列表（图 13.2 为这些关系的图形化视图）。

# 表 13.1 Socket 编程元素层次结构

| 元素 | 描述 |
| --- | --- |
