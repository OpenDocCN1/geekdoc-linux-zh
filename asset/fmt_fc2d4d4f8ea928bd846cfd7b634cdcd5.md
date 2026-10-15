
```c
    /* 处理循环 */
    while(fgets(readbuf, 80, infile)) {
        fputs(readbuf, pipe_fp);
    }
```

```c
    /* 关闭管道 */
    fclose(infile);
    pclose(pipe_fp);
```

```c
    return(0);
}
```

# Linux 进程间通信 39

如果管道超过了单次操作的原子限制，并且有多个进程向管道写入数据，数据将出现“交织”或“分段”。换句话说，一个进程可能会在另一个进程写入之间向管道中插入数据。

# 半双工管道的注意事项

- 通过打开两个管道并在子进程中适当重新分配文件描述符，可以创建双向管道。

- `pipe()` 的调用必须在 `fork()` 之前进行，否则描述符不会被子进程继承（`open()` 也是如此）。

- 对于半双工管道，任何连接的进程必须具有共同的祖先关系。由于管道位于内核内部，任何不在管道创建者祖先链中的进程都无法对其进行标识。命名管道（FIFOs）则并非如此。

# 命名管道 (FIFOs)：先进先出

## 基本概念

管道的工作原理与普通管道非常相似，但也有一些明显的区别。

- 命名管道以特殊设备的形式存在于文件系统中。

- 不同祖先关系的进程可以通过命名管道共享数据。

- 当共享进程完成所有 I/O 操作后，命名管道仍保留在文件系统中备后之用。

## 创建 FIFO

创建命名管道有多种方法。前两种可以直接从 shell 中完成。

```
mknod MYFIFO p
mkfifo MYFIFO
```

上述两个命令执行的操作相同，但有一个例外。`mkfifo` 命令提供了一个钩子，可以在创建后直接修改 FIFO 文件的权限。而使用 `mknod`，则需要快速调用 `chmod` 命令。

在物理文件系统中，可以通过长目录列表在此此处“p”指示符来快速识别 FIFO 文件：

```
$ ls -l MYFIFO
prw-r--r-- 1 root root 0 Dec 14 22:15 MYFIFO
```

# Linux 程序员指南：第 6 章

还有紧接文件名后的竖线（“管道符号”）。这也是运行 Linux 的另一个理由，不是吗？

在 C 中创建 FIFO，我们可以利用 `mknod()` 系统调用：

```
LIBRARY FUNCTION: mknod();

PROTOTYPE: int mknod(char *pathname, mode_t mode, dev_t dev);
RETURNS: 成功时返回 0，
  错误时返回 -1: errno = EFAULT (路径无效)
    EACCES (权限被拒绝)
    ENAMETOOLONG (路径过长)
    ENOENT (路径无效)
    ENOTDIR (路径无效)
    其他信息参见 mknod 手页)
```

备注：创建一个文件系统节点（文件、设备文件或 FIFO）

我将 `mknod()` 的详细描述留给 man 页，但让我们考虑一个用 C 创建 FIFO 的简单示例：

```
mknod("/tmp/MYFIFO", S_IFIFO|0666, 0);
```

在这种情况下，文件`/tmp/MYFIFO`被创建为 FIFO 文件。请求的权限为`0666`，尽管它们受到 `umask` 设置的影响：

```
final_umask = requested_permissions & ~original_umask
```

一个常用的技巧是使用 `umask(0)` 系统调用临时清除 `umask` 值：

```c
umask(0);
mknod("/tmp/MYFIFO", S_IFIFO|0666, 0);
```

此外，`mknod()` 的第三个参数会被忽略，除非我们正在创建一个设备文件。在这种情况下，它应该指定设备文件的主号和从号。

## FIFO 操作

在 FIFO 上的 I/O 操作本质上与普通管道相同，但有一个主要的区别。应该使用`open`系统调用或库函数来物理上打开通到管道的通道。对于半双工管道，这是没有必要的，因为管道位于内核中而不是物理文件系统中。在我们的示例中，我们将管道视为一个流，使用 `fopen()` 打开它，并使用 `fclose()` 关闭它。

考虑一个简单的服务器进程：

节选自《Linux 程序员指南 - 第 6 章》

(版权)1994-1995, Scott Burkett

```c
MODULE: fifserver;

#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <unistd.h>

#include <linux/stat.h>

#define FIFO_FILE "MYFIFO"

int main(void) {
    FILE *fp;
    char readbuf[80];

    /* 如果 FIFO 不存在则创建它 */
    umask(0);
    mknod(FIFO_FILE, S_IFIFO|0666, 0);

    while(1) {
        fp = fopen(FIFO_FILE, "r");
        if (fgets(readbuf, 80, fp)) {
            printf("Received string: %s\n", readbuf);
        }
        fclose(fp);
    }
    return(0);
}
```

由于 FIFO 默认是阻塞的，请在编译后在后台运行服务器：

```
$ fifserver &
```

我们稍后会讨论 FIFO 的阻塞行为。首先，考虑以下指向我们服务器的简单客户端前端：

节选自《Linux 程序员指南 - 第 6 章》

(版权)1994-1995, Scott Burkett

```
****************************************************************************************************
MODULE: fifocient.c
****************************************************************************************************
```

# FIFO 阻塞行为

通常情况下，阻塞发生在 FIFO 上。换句话说，如果为了读取打开 FIFO，它将“阻塞”直到另一个进程写入。如果这种行为不可理想，可以在 `open(1)` 调用中使用 `O_NONBLOCK` 标志。

在我们简单的服务器示例中，我们刚刚将其放入后台，然后切换回客户端查看结果。

# 著名的 SIGPIPE 信号

最后一点，管道必须既有读者也有写者。如果进程尝试向没有读者的管道写入数据，内核将对其发送 `SIGPIPE` 信号。这在涉及多个进程时是必须的。

# System V 概念

System V 引入了三种新的 IPC 形式（消息队列、信号量和共享内存）。虽然 POSIX 委员会尚未完成这些设施的标准化，但大多数实现都是。此外，Berkeley (BSD) 使用 `socket` 作为其主要的 IPC 形式，而不是 System V 要素。我们将在后面的章节讨论 `socket`。

Linux 对 System V 的实现由 Krishna Balasubramanian 设计。

# IPC 标识符

每个 IPC 对象都关联有一个唯一的标识符。当我们说“IPC 对象”时，我们指的是单个消息队列、信号量集或共享内存段。该标识符用于在内核内部唯一标识 IPC 对象。例如，访问特定的共享内存段，你只需要分配给该段的唯一 ID 值。

# IPC 密钥

获取唯一 ID 需要使用密钥。密钥必须由客户端和服务器进程共同约定。这代表了构建应用程序客户端/服务器框架的第一步。

# 344 Linux 程序员指南：第 6 章

```
原型：key_t ftok( char *pathname, char proj );
返回值：如果成功则返回新的 IPC 值
如果失败则返回 -1，并将 errno 设置为 stat() 调用的返回值
```

`ftok()` 返回的键值通过将第一个参数中的文件索引节点（inode）和次要设备号，与第二个参数中的单字符项目标识符结合生成。这不能保证唯一性，但应用程序可以检查冲突并重试键生成。

```
key_t mykey:
mykey = ftok("/tmp/myapp", 'j');
```

在上面的代码段中，目录 `/tmp/myapp` 与单字母标识符 `a` 结合。另一个常见的例子是使用当前目录：

```
key_t mykey:
mykey = ftok("..", 'a');
```
