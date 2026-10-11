
`popen` 返回的流指针以只读方式打开，这意味着该流连接到命令的标准输出；从该流读取数据等同于读取命令的标准输出。同样地，如果 `mode` 为 `w`，则该流连接到命令的标准输入，因此向该流写入数据就如同向命令的标准输入写入一样。如果 `popen` 调用失败，它会返回 `NULL`。导致失败的错误条件会被设置在错误变量 `errno` 中。

要关闭该流，必须使用 `pclose` 而非标准的 `fclose` 调用。`pclose` 会关闭 I/O 流，等待命令执行完毕，并将退出状态返回给调用进程。如果 `pclose` 调用失败，则返回 -1。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_366_0.png)

以下程序将 `piperw` 重写为使用 `popen` 和 `pclose`：

```c
/*
 * piperw.c – The correct way to open a pipe and fork
 *           a child process.
 */
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <limits.h>

#define BUFSZ PIPE_BUF

void err_quit(char *msg);

int main(void)
{
  FILE *fp;                    /* FILE stream for popen */
  char *cmdstring = "cat piperw.c";
  char buf[BUFSZ];             /* Buffer for "input" */

  /* Create the pipe */
  if((fp = popen(cmdstring, "r")) == NULL)
    err_quit("popen");
  /* Read cmdstring's output */
  while((fgets(buf, BUFSZ, fp)) != NULL)
    printf("%s", buf);

  /* Close and reap the exit status */
  pclose(fp);
  exit(EXIT_SUCCESS);
}

void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```

正如代码清单所示，`popen` 和 `pclose` 使得管道操作所需的代码量大大减少。代价是放弃了一定程度的控制权。例如，你被迫使用 C 流库而不是低级别的 read 和 write I/O 调用。此外，`popen` 强制你的程序执行 exec，而你可能并不一定想要或需要这样做。最后，用于回收子进程退出状态的函数调用 `pclose` 可能不符合你的程序要求。尽管存在这种灵活性上的损失，`popen` 本身节省了 10–15 行代码；而处理读写操作的代码相比 `piperw` 的代码也显著简化了。输出结果（部分如下所示）保持不变。模式语义可能看起来有些奇怪，所以请记住 `r` 表示你从 `stdout` 读取，而 `w` 表示你向 `stdin` 写入。

![](img/be588b36b489136ce784030a08a1d3d4_367_0.png)

## 输出

```text
$ ./newrw
/*
 * pipopn.c - Open and close a pipe
 */
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
...
```

## FIFO

如前所述，FIFO 也称为命名管道，因为它们具有持久性，即存在于文件系统中。FIFO 特别有用，因为它们允许互不相关的进程交换数据。

## 理解 FIFO

使用 shell 命令的一个简单示例可以帮助你理解 FIFO。`mkfifo(1)` 命令用于创建 FIFO：

```text
mkfifo [option] name [ . . . ]
```

该命令创建一个名为 `name` 的 FIFO。`option` 通常是 `-m mode`，其中 `mode` 指示新创建的 FIFO 的八进制模式，该模式会受到 umask 的修改。创建 FIFO 后，你可以像使用常规 shell 管道的一部分一样使用它。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_368_0.png)

下面的示例将 `newrw` 的输出通过一个富有想象力的名为 `fifo1` 的 FIFO 传递，该 FIFO 进而将其输出通过 `cut` 命令传递。

首先，使用以下命令创建 FIFO：

```shell
$ mkfifo -m 600 fifo1
```

接下来，执行以下两个命令：

```shell
$ cat < fifo1 | cut -c1-5 &
$ ./newrw > fifo1
```

这些 shell 命令的输出如下：

![](img/be588b36b489136ce784030a08a1d3d4_368_1.png)

## 输出

```c
/*
 * piperw.c
 */
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    int ...
    if((...
        per ...
    Exit ...
    }
    fpri ...
    clos ...
    exit
}
```

在后台运行的 `cat` 命令从 FIFO（`fifo1`）读取输入。`cat` 的输入是 `cut` 命令的输出，而 `cut` 命令会修剪掉每一行输入中除前五个字符以外的所有字符。`cut` 的输入，最终来自 `newrw` 程序的输出。

这些 shell 命令的实际输出是看似奇怪、被截断的代码，以完成代码清单。如果 `fifo1` 是常规文件，结果将是一个填充了 `newrw` 输出的常规文件。

> **提示**
>
> `ls` 命令的输出确认 `mkfifo` 创建了所请求的 FIFO。它在文件模式的设备类型字段中显示为 `p`（代表 pipe），并且由于 `-F` 开关，它在文件名末尾显示为 `|`。

## 创建 FIFO

创建 FIFO 的函数调用名称与 shell 接口相同，即 `mkfifo`。其语法类似于 `open`：

```c
int mkfifo(const char *pathname, mode_t mode);
```

要使用此函数，请在你的程序中包括 `<sys/types.h>` 和 `<sys/stat.h>`。`mkfifo` 创建一个名为 `pathname` 的 FIFO，其权限位由 `mode` 指定（以八进制表示）。通常，`mode` 中的值会受到进程 `umask` 的修改。

> **注意**
>
> `umask` 影响大多数创建具有特定权限的文件或目录的调用。要提前确定文件或目录在经 `umask` 修改后的模式，只需将你要使用的模式与 `umask` 值的按位补数进行按位与运算即可。在代码中，这看起来像这样：
>
> mode_t mode = 0666;
> mode & ~umask;
>
> 因此，给定 `umask` 为 `022`，`mode & ~umask` 返回 `0644`。

如果成功，`mkfifo` 返回 0；否则，它将错误变量 `errno` 的值设置好并返回 -1 给调用者。潜在的包括 `EACCES`、`EEXIST`、`ENAMETOOLONG`、`ENOENT`、`ENOSPC`、`ENOTDIR` 和 `EROFS`。

- **表 6.1** “系统调用错误代码”（第 125 页）列出了系统调用生成的返回代码。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_371_0.png)

以下程序在当前目录中创建一个 FIFO：

```c
/*
 * newfifo.c – Create a FIFO
 */
#include <sys/types.h>
#include <sys/stat.h>
#include <errno.h>
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[])
{
	mode_t mode = 0666;

	if (argc != 2) {
		puts("USAGE: newfifo <name>");
		exit(EXIT_FAILURE);
	}
	if ((mkfifo(argv[1], mode)) < 0) {
		perror("mkfifo");
		exit(EXIT_FAILURE);
	}
	exit(EXIT_SUCCESS);
}
```

该程序的几次示例运行产生了以下输出：

![](img/be588b36b489136ce784030a08a1d3d4_371_1.png)

## 输出

```text
$ ./newfifo
USAGE: newfifo <name>
$ ./newfifo fifo1
$ ./newfifo fifo1
mkfifo: File exists
```

第一次运行时，`newfifo` 发出警告，因为它没有被正确调用；它期望将 FIFO 的名称作为唯一的参数传递。第二次运行提供了文件名，`newfifo` 默默地创建了它。由于文件已经存在，第三次运行中的 `mkfifo` 调用失败，`errno` 被设置为 `EEXIST`。`EEXIST` 的设置对应于 `perror` 打印的字符串：`File exists`。

## 打开和关闭 FIFO

打开、关闭、删除、读取和写入 FIFO 的过程分别使用你之前已经见过的 open、close、unlink、read 和 write 系统调用——这是 Linux “一切皆文件” 抽象的一个优点。由于打开和关闭 FIFO 与打开和关闭管道相同，你可能需要回顾本章前面列出的“打开和关闭管道”中的程序。

然而，在读取和写入 FIFO 时，你必须牢记一些细微之处。首先，FIFO 的两端都必须打开后才能使用。其次，更重要的是，如果 FIFO 使用 O_NONBLOCK 标志打开时的行为。回想一下，O_WRONLY 或 O_RDONLY 标志可以逻辑或与 O_NONBLOCK。如果 FIFO 使用 O_NONBLOCK 和 O_RDONLY 打开，调用会立即返回；但如果它使用 O_NONBLOCK 和 O_WRONLY 打开，如果该 FIFO 尚未同时被打开用于读取，则 open 返回错误并将 errno 设置为 ENXIO。

另一方面，如果 open 的标志中没有指定 O_NONBLOCK，O_RDONLY 会导致 open 阻塞（不返回），直到另一个进程以写模式打开该 FIFO。同样，O_WRONLY 会阻塞，直到该 FIFO 被打开用于读取。

与管道一样，向未打开用于读取的 FIFO 写入数据会向写入进程发送 SIGPIPE，并将 errno 设置为 EPIPE。在最后一个写入者关闭 FIFO 后，读取进程在其下一次读取时会检测到文件末尾。如前关于管道所述，为了确保多个进程向单个 FIFO 写入时的原子性写入，每个进程的写入大小必须小于 PIPE_BUF 字节。

## 读取和写入 FIFO

在考虑了上一节末尾讨论的事项后，读取和写入 FIFO 与读取和写入管道及常规文件类似。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_372_0.png)

此示例稍显复杂。一个程序 `rdfifo` 创建并打开一个 FIFO 用于读取，并将 FIFO 的输出显示到 stdout。另一个程序 `wrffifo` 打开该 FIFO 用于写入。特别有趣的是运行多个写入者实例在不同窗口中，并在运行读取者的窗口中观察它们的输出的过程。

```c
/*  rdfifo.c  Create a FIFO and read from it */
#include <sys/types.h>
```
