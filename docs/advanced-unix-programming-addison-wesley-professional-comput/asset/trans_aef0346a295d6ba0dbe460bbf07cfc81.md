

3. 在子进程中，关闭管道的写端，并进行其他必要的准备。（我们将在后续示例中看到这些内容。）
4. 在子进程中，执行子程序。
5. 在父进程中，关闭管道的读端。
6. 如果有第二个子进程要写入管道，则创建该子进程，进行必要的准备，并执行其程序。如果是由父进程写入，那就直接进行写入。

我们关于单向管道的所有示例都将遵循此范式。

现在我们可以看到为什么 `fork` 和 `exec` 是独立的系统调用。为什么不用一个系统调用来完成这两项工作，从而节省 `fork` 的开销呢？将它们分开是为了让我们能够执行上述步骤 3。我们已经发现需要在 `fork` 和 `exec` 之间做一些工作（关闭 `pfd[1]`），并且在本章的后续部分我们将看到更多。我们不能在 `fork` 之前做这些工作，因为我们不希望它影响父进程（父进程必须不关闭管道的写端）。我们不希望子程序来做这项工作，因为我们希望程序对它们是如何被调用以及它们的输入和输出是如何连接的毫无感知（这是 UNIX 哲学的一个基石）。因此，我们在完美的位置执行这些工作：在子进程中，执行从父进程克隆的代码。一个额外的优点是连接代码被局部化，使其更容易调试和修改。

进一步思考：既然进程连接的方式通常只有几种，为什么不设置一个带有各种进程间连接选项的单一 `fork-exec` 系统调用呢？毕竟，还有其他许多带有大量选项的系统调用，这里为什么不行？答案很简单：UNIX 的原始设计者 Thompson 和 Ritchie 希望最小化系统调用的数量。`fork` 和 `exec` 很简单，但它们允许调用者安排各种自定义连接。那么我们为什么要搞出另一个复杂的系统调用³？

读取程序 `pipe` 是专门设计用来读取传入的文件描述符的。这是一个奇怪的程序——没有标准的 UNIX 命令那样工作。许多程序可以读取特定的文件描述符，它们假定该描述符已经打开，但该文件描述符固定为 0（标准输入，`STDIN_FILENO`）。它不需要作为参数传入。类似地，许多程序被设计用来写入文件描述符 1（标准输出，`STDOUT_FILENO`）。为了像 shell 那样连接命令，我们需要某种方式迫使 `pipe` 在 `pfd` 数组中返回特定的文件描述符：读端为 0，写端为 1。可惜，`pipe` 不提供这样的功能。我们可以尝试在调用 `pipe` 之前关闭 0 和 1，以使它们可用，但这并不安全，因为标准并未说明哪一端是哪一端，而且，我们通常不能为了创建管道而牺牲我们的标准输入和标准输出。那么，我们如何完成这个小技巧呢？我们使用 `dup` 或 `dup2`。

## 6.3 dup 和 dup2 系统调用

**dup**——复制文件描述符

```c
#include <unistd.h>
int dup(
        int fd;            /* 要复制的文件描述符 */
);
/* 返回新的文件描述符，出错时返回 -1（设置 errno） */
```

**dup2**——复制文件描述符

```c
#include <unistd.h>
int dup2(
        int fd,            /* 要复制的文件描述符 */
        int fd2;           /* 要使用的文件描述符 */
);
/* 返回新的文件描述符，出错时返回 -1（设置 errno） */
```

`dup` 复制现有的文件描述符，返回一个新的文件描述符，该描述符打开到同一文件（或管道等）。两者共享同一个文件描述（参见第 2.2 节），就像继承的文件描述符与其父进程中对应的文件描述符共享文件描述符一样。如果参数无效（未打开）或没有可用的文件描述符，该调用将失败。

`dup` 采用编号最小的可用文件描述符，因此如果您知道哪些文件描述符已打开，您可以控制它返回什么。不过，使用 `dup2` 更容易，它允许您通过 `fd2` 参数指定要返回的文件描述符。为了使 `fd2` 可用，如果需要，`dup2` 会关闭它。

`dup`(`fd`) 等价于：

```c
fcntl(fd, F_DUPFD, 0)
```

而 `dup2`(`fd`, `fd2`) 等价于：

```c
close(fd2);
fcntl(fd, F_DUPFD, fd2);
```

不同之处在于 dup2 是原子操作——如果复制过程中出现问题，fd2 不会被关闭。我们将使用 dup2 而不是 dup 作为我们所有示例中的选择，因为它更容易使用。

由于文件描述是共享的，拥有第二个文件描述符只有一个好处：它的编号不同，可能更适合调用者的目的。假设我们创建一个管道，然后使用 dup2 使 STDIN_FILENO（文件描述符 0）成为管道读端（其文件描述符可能是 3、4、27 或任何数字）的副本。如果我们随后执行一个设计为读取 STDIN_FILENO 的程序（有很多这样的程序！），它就会被“欺骗”去读取管道。可以使用类似的算法来强制 STDOUT_FILENO 成为管道的写端。

如果 dup2 的参数相等，它仅返回该文件描述符，而不关闭或复制任何内容。这在某些情况下很有帮助，例如，管道的读端碰巧已经等于 STDIN_FILENO 时。

为了说明 dup2，这里有一个示例，该示例创建一个管道，创建一个子进程来读取它，安排子进程的 STDIN_FILENO 为管道的读端，然后调用 cat 命令来读取管道。既然我们可以使用 STDIN_FILENO，我们就不需要像上一节示例中的 pipe_read 那样的特殊程序了。

```c
void pipewrite2(void) /* 有一个 bug */
{
  int pfd[2];
  pid_t pid;

  ec_neg1( pipe(pfd) )
  switch (pid = fork()) {
  case -1:
    EC_FAIL
  case 0: /* 子进程 */
    ec_neg1( dup2(pfd[0], STDIN_FILENO) )
    ec_neg1( close(pfd[0]) )
    ec_neg1( close(pfd[1]) )
    exec1p("cat", "cat", (char *)NULL);
    EC_FAIL
  default: /* 父进程 */
    ec_neg1( close(pfd[0]) )
    ec_neg1( write(pfd[1], "hello", 6) )
    ec_neg1( waitpid(pid, NULL, 0) )
  }
  return;

EC_CLEANUP_BGN
  EC_FLUSH("pipewrite2");
EC_CLEANUP_END
}
```

我们得到了这个不出所料的结果：

```
hello
```

请注意，在子进程中，我们在复制其中一个文件描述符之后关闭了从 `pipe` 获得的两个文件描述符。管道的读端仍然打开，但现在它的文件描述符是 `STDIN_FILENO`。父进程关闭了 `pfd[0]`（读端），因为它不需要它。对 `waitpid` 的调用等待 `cat` 终止；我们在上一节的 `pipe` 读示例中省略了这一点。

不幸的是，在显示 "hello" 之后，程序挂起了，我们必须通过 Ctrl-c 终止它才能得到 shell 提示符。你知道原因吗？（下一段会有剧透。）

程序挂起是因为 `cat` 一直读取直到遇到文件结束符（EOF），但它没有遇到，所以它没有终止。回想一下，只有当 *所有* 打开到管道的写文件描述符都被关闭时，`read` 才会返回 0，而在调用 `waitpid` 时，`pfd[1]` 仍然处于打开状态。因此，父进程和子进程形成了死锁。解决方案是在写入数据后关闭写端：

```c
default: /* 父进程 */
    ec_neg1( close(pfd[0]) )
    ec_neg1( write(pfd[1], "Hello", 6) )
    ec_neg1( close(pfd[1]) )
    ec_neg1( waitpid(pid, NULL, 0) )
```

我们不必局限于从父进程向子进程进行管道传输。下一个示例实现了与 shell 命令行等价的操作：

`$ who | wc`

以查看有多少用户登录。

```c
void who_wc(void)
{
    int pfd[2];
    pid_t pid1, pid2;

    ec_neg1( pipe(pfd) )
    switch (pid1 = fork()) {
    case -1:
        EC_FAIL
    case 0: /* 第一个子进程 */
        ec_neg1( dup2(pfd[1], STDOUT_FILENO) )
        ec_neg1( close(pfd[0]) )
        ec_neg1( close(pfd[1]) )
        execlp("who", "who", (char *)NULL);
        EC_FAIL
    }
    /* 父进程 */
    switch (pid2 = fork()) {
    case -1:
        EC_FAIL
    case 0: /* 第二个子进程 */
        ec_neg1( dup2(pfd[0], STDIN_FILENO) )
        ec_neg1( close(pfd[0]) )
        ec_neg1( close(pfd[1]) )
        execlp("wc", "wc", "-l", (char *)NULL);
        EC_FAIL
    }
    /* 仍然是父进程 */
    ec_neg1( close(pfd[0]) )
    ec_neg1( close(pfd[1]) )
    ec_neg1( waitpid(pid1, NULL, 0) )
    ec_neg1( waitpid(pid2, NULL, 0) )
    return;
}
EC_CLEANUP_BGN
EC_FLUSH("who_wc");
EC_CLEANUP_END
```

这是输出：

```
1
```

**who** 和 **wc** 不必都是同一个父进程的子进程；wc 也可以是 who 的子进程，设置起来同样容易：

```c
void who_wc2(void)
{
    int pfd[2];
    pid_t pid1, pid2;

    ec_neg1( pipe(pfd) )
    switch (pid1 = fork()) {
    case -1:
        EC_FAIL
```

