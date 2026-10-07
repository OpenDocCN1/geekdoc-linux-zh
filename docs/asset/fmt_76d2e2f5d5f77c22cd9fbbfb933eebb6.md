
进入`/path/to/xxx`目录，找到`xxx.json`。

使用`dup2()`，整个操作被保证是原子的，这意味着它永远不会被到达的信号中断。在使用原始的`(dup)`系统调用时，程序员必须在调用它之前执行一次`close()`操作。

## 6.2.3 更简单的管道方法！

如果你觉得以上所有的漫论看起来像是创建和利用管道的一种非常迂的方法，那么还有替代方案。

# LIBRARY FUNCTION: `popen()`;
PROTOTYPE: `FILE *popen(char *command, char *type);`
RETURNS: 成功时返回新的文件流

成功的`fork()`或`pipe()`调用失败返回`NULL`
NOTES: 创建管道，并使用"`command`"执行`fork/exec`操作

虽然这个库函数为你承担了大量的脏活工作，但也存在实质性的权衡。你失去了曾经通过使用`pipe()`系统调用和自己处理`fork/exec`所拥有的精细控制力。然而，由于直接使用了Bourne shell，在“命令”参数中允许进行shell元字符扩展（包括通配符）。

通过`open()`创建的管道必须用`close()`关闭。到此时，你可能已经发现`open`/`close`与标准文件流I/O函数`open()`和`fclose()`有惊相似之处。

## 库函数：`pclose()`;

返回值：`wait(4)`调用的退出状态
如果"`stream`"无效或`wait(4)`失败，则返回`-1`

说明：等待管道进程终止，然后关闭流。`pclose()`函数对`popen()`派生的进程执行`wait(4)`。当它返回时，会销毁管道和文件流。再次，它与用于普通基于流的文件I/O的`fclose()`函数同义。考虑下面这个示例，它打开了通往`sort`命令的管道，并对一个字符串数组进行排序：

****************************************************************************************************************

摘自《Linux 程序员指南 - 第 6 章》
(C)opyright 1994-1995, Scott Burk

****************************************************************************************************************

## 模块：`popen.c`

****************************************************************************************************************

```
#include <stdio.h>

#define MAXSTRS 5

int main(void) {

    int cntr;

    FILE *pipe_fp; char *strings[MAXSTRS] = { "echo", "bravo", "alpha",

        "charlie", "delta"};

    /* 使用 popen() 创建一条管道线 */

    if ((pipe_fp = popen("sort", "w")) == NULL) {

        perror("popen"); exit(1);

    }

    /* 处理循环 */

    for (cntr=0; cntr<MAXSTRS; cntr++) {

        fprintf(pipe_fp, "%s", strings[cntr]); fputc('\n', pipe_fp);

    }

    /* 关闭管道 */

    pclose(pipe_fp);

    return(0);

}
```

由于`popen()`使用shell来执行其指令，所有的shell扩展字符和元字符均可用！此外，使用`popen()`可以利用重定向、甚至输出管道等更高级的技术。考虑以下示例调用：

```
popen("ls ~scott", "r"); popen("sort > /tmp/foo", "w"); popen("sort | uniq | more", "w");
```

作为`popen()`的另一个示例，考虑这个小程序，它打开了两个管道（一个指向`ls`命令，另一个指向`sort`）：

****************************************************************************************************

# 摘自《Linux 程序员指南 - 第 6 章》
(Copyright 1994-1995, Scott Burchett)

# 模块：`popen.c`

作为`popen()`的最后一个演示，让我们创建一个通用程序，在传递的命令和文件名之间建立流水线：

# 摘自《Linux 程序员指南 - 第 6 章》

尝试这个程序，并使用以下调用：
`popen3 sort popen3.c` `cat popen3.c` `popen3 more popen3.c` `popen3 cat popen3.c | grep main`

## 6.3. 命名管道 (FIFOs - 先入先出)

## 6.2.4 管道的原子操作

为了使一个操作被认为是“原子的”，它不能因为任何原因被中断。整个操作必须一次性完成。POSIX标准在`/usr/include/posixlim.h`中规定了管道上进行原子操作的最大缓冲区大小为：

```
#define POSIX_PIPE_BUF 512
```

多达512字节可以以原子方式写入管道或从管道中读取。任何超过此阈值的内容都会被拆分，且不是原子的。在Linux下，原子操作限制定义在`linux/limits.h`中：

正如你所见，Linux满足了POSIX要求的字节数，我可以说，这相当合理。当涉及多个进程（FIFOs）时，管道操作的原子性变得非常重要。例如，如果写入管道的字节数超过了单次操作的原子限制，且有多个进程写入管道，数据将变得“交织”或“分块”。换句话说，一个进程可能会在另一个进程写入之间向流水线插入数据。

## 6.2.5 关于半双工管道的说明：

通过打开两个管道并在子进程中正确重新分配文件描述符可以创建两个管道。

`pipe()`调用必须在调用`fork()`**之前**执行，否则描述符将不会被子进程继承！（`popen()`也是如此）。

对于半双工管道，任何连接的进程必须共享相关的祖先关系。由于管道位于内核限制范围内，任何不在管道创建者祖先关系中的进程都没有方法对其进行引用。命名管道（FIFOs）则并非如此。

## 6.3 命名管道 (FIFOs) - 先入先出

### 6.3.1 基本概念

命名管道的工作与普通管道类似，但有一些明显的区别。

- 命名管道作为设备特种文件存在于文件系统中。
- 不同祖先关系的进程可以通过命名管道共享数据。
- 当所有共享进程完成I/O操作后，命名管道仍留在文件系统中供日后使用。

### 6.3.2 创建 FIFO

有多种方法创建命名管道。第一种可以通过shell直接完成：

```bash
mkfifo MYFIFO
```

`mkfifo`命令提供了修改FIFO权限的钩。FIFO文件可以通过目录列表中的“p”指示符快速识别：

```
$ ls -l MYFIFO
prw-r--r-- 1 ...
```

`mkfifo`命令在创建后执行相同的操作，但有一个例外。为了在C中创建FIFO，我们可以使用`mknod()`系统调用：

## 库函数：`mknod()`;

```
原型：int mknod(char *pathname, mode_t mode, dev_t dev);
返回值：成功时返回 0，
失败时设置 errno =
EFAULT (路径无效)
EACCES (拒绝访问)
ENAMOOLONG (路径过长)
ENOENT (路径不存在)
ENOTDIR (不是目录)
(其他见 man mknod)
说明：创建一个文件系统节点（设备文件、FIFO）
```

我会将`mknod()`的详细讨论留给手册页，但让我们考虑一个简单的FIFO创建示例：

在这种情况下，文件`/tmp/MYFIFO`作为一个FIFO文件。请求的权限为`066`，尽管它们受到如下`umask`设置的影响：

```
final_umask = requested_permissions & ~umask
```

一种常用的技巧是使用`umask()`调用临时清除`umask`值：
`umask(0);`

此外，`mknod()`的第三个参数会被忽略，除非我们正在创建设备文件。例如，它应该指定设备文件的主、次设备号。

### 6.3.3 FIFO 操作

FIFO的I/O操作与普通管道基本相同，只有一个主要的例外。应该使用`open`系统调用或库函数来物理打开通往管道的通道。对于半双工管道，这是必要的，因为管道位于内核而非物理文件系统中。在我们的示例中，我们将管道视为流，使用`fopen()`打开，并使用`fclose()`关闭。考虑一个简单的服务器进程：

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <unistd.h>
#define FIFO_FILE "MYFIFO"
int main(void) {
    FILE *fp; char readbuf[80];
    /* 如果 FIFO 不存在则创建它 */
    umask(0); mkfifo(FIFO_FILE, S_IFIFO|0666, 0);
    while(1) { 
        fp = fopen(FIFO_FILE, "r"); 
        fgets(readbuf, 80, fp); 
        printf("Received string:%s\n", readbuf); 
        fclose(fp);
    }
    return(0);
}
```

由于FIFO默认是阻塞的，请在编译后在后台运行服务器：
`$ fifoserver&`

我们稍后会讨论FIFO的阻塞行为。首先，考虑下面作为服务器的简单客户端前端：

# (C)版权 1994-1995, Scott Burkett

# 模块：`fifocient.c`

```
#include <stdio.h>
#include <stdlib.h>
#define FIFO_FILE "MYFIFO"
int main(int argc, char *argv[])
{
    FILE *fp;
    if (argc != 2) {
        printf("USAGE: fifo [client]\n"); exit(1);
    }
    if ((fp = fopen(FIFO_FILE, "w")) == NULL) {
        perror("fopen"); exit(1);
    }
    fputs(argv[1], fp);
    fclose(fp); return(0);
}
```

## 6.3.4 FIFO 上的阻塞操作

通常，FIFO会发生阻塞。换句话说，如果以读模式打开FIFO，进程将“阻塞”，直到另一个进程以写模式打开它。这种行为反之亦然。如果这种行为不可接受，可以在`open()`调用中使用`O_NONBLOCK`标志来禁用默认的阻塞操作。

在我们的服务器中，我们只是将其推到后台运行，让它在那里进行阻塞。另一种方法是跳转到另一个虚拟控制台并运行客户端，来回切换以查看结果的操作。

## 6.3.5 臭名昭著的 SIGPIPE 信号

最后一点，管道必须有一个读取者和一个写入者。如果一个进程尝试向一个没有读取者的管道写入数据，它将收到内核发送的`SIGPIPE`信号。当流水线涉及两个以上以上进程时，这一点至关重要。

## 6.4 System V IPC

### 6.4.1 基本概念

通过System V，AT&T引入了三种新形式的IPC设施（消息队列、信号量和共享内存）。虽然POSIX委员会尚未完成这些设施的标准化，但大多数实现都支持这些。此外，Berkeley (BSD)使用`sockets`作为其主要的IPC形式，而不是System V元素。Linux有能力同时使用这两种IPC形式（BSD和System V），尽管我们将在后面的章节中才会讨论`sockets`。

Linux的System V IPC实现由Krishna Balasubramanian编写，邮箱为`balasub@cis.ohio-state.edu`。

## IPC 标识符

每个IPC对象都有一个与其相关的唯一IPC标识符。当我们说“IPC对象”时，我们指的是单个消息队列、信号量集或共享内存段。

该标识符在内核内部用于唯一地标识一个IPC对象。例如，要访问特定的共享内存段，你只需要分配给该段的唯一ID值。标识符的唯一性与所涉及的对象类型有关。为了说明这一点，假设有一个数字标识符为"`12345`"。虽然永远不存在两个相同标识符的消息队列，但完全存在一个消息队列和一个（比如）共享内存具有相同的数字标识符。

## IPC 密钥

为了获取唯一ID，必须使用密钥（key）。密钥必须在客户端和服务器进程之间达成一致。这代表了构建应用程序客户端/服务器框架的第一步。当你用电话给打电话时，你必须知道对方的号码。此外，电话公司必须知道如何将你的拨号转接到最终目的地。一旦对方接听电话响应，连接就建立了。

在System V IPC设施的情况下，“电话”直接与所使用的对象类型相关。“电话公司”或路由方法可以与IPC密钥直接关联。

通过在应用程序中硬编码密钥值，密钥每次可以是相同的值。它的缺点是密钥可能已被占用。通常，使用`ftok()`函数为客户端和服务器生成密钥值。

## 库函数：`ftok()`

```
原型: key_t ftok ( char *pathname, char proj ); 返回: 如果成功则返回新的 IPC
  key 值
  如果失败则返回 -1，errno 设置 stat() 调用的返回值
```

`ftok()`的返回值是通过将第一个参数中的文件索引节点号（inode number）和次要设备号，与第二个参数中的单字符项目标识符结合生成的。这不能保证唯一性，但应用程序可以检查冲突并重试密钥生成。

```
key_t mykey;
mykey = ftok("/tmp/myapp", 'a');
```

在上面的代码段中，目录`/tmp/myapp`与单标识符`'a'`结合。另一个常见的例子是使用当前目录：

```key
key_t mykey; mykey = ftok("", 'a');
```

使用的密钥生成算法完全取决于应用程序程序员的决定。只要采取了措施防止竞态条件、死锁等，任何方法都是可行的。为了演示目的，我们将使用`ftok()`方法。如果我们假设每个客户端进程都从一个唯一的“家”目录运行，那么生成的密钥应该足够我们使用。

然而，无论如何获取密钥值，它都被用于后续IPC系统调用创建或访问IPC对象。

## `ipcs` 命令

可以使用`ipcs`命令获取所有System V IPC对象的状态。该工具的Linux版本也由Krishna Balasubramanian编写。

| `ipcs -q`: | 仅显示消息队列 |
| :--- | :--- |
| `ipcs -s`: | 仅显示信号量 |
| `ipcs -m`: | 仅显示共享内存 |

| `ipcs -h`: | 显示帮助 |
| `ipcs -a`: | 显示所有 |
| `ipcs -p`: | 显示非共享段 |
| `ipcs -i`: | 显示 ID 的信息 |
| `ipcs -u`: | 显示当前系统状态 |
| `ipcs -c`: | 显示 IPC 统计数据 |
| `ipcs -t`: | 按类型显示表 |

（注：由于原始文本包含大量OCR识别重复，上述译文已根据逻辑流进行了去重和清理。）

# `msgtype`

这是消息类型，在用户结构`msgbuf`中分配。

# `msgspot`

指向消息体起始位置的指针。

# `msgts`

消息文本或正体的长度。

## 内核 `msqids` 结构

三种类型的IPC对象中的每种都有一个由内核维护的内部数据结构。对于消息队列，这就是`msqids`结构。内核为系统中每个每个消息队列创建、存储并维护该结构的实例。它定义在`linux/msg.h`中：

```c
/* 系统中每个队列有一个 msqid 结构 */
struct msqid_ds {
    ipc_perm msg_perm;
    struct msg *msg_first; /* 队列中的第一个消息 */
    struct msg *msg_last; /* 队列中的最后一个消息 */
    time_t msg_stime; /* 上次 msgsnd 时间 */
    time_t msg_rime; /* 上次 msgrcv 时间 */
    time_t msg_ctime; /* 上次修改时间 */
    struct wait_queue *wait;
    struct wait_queue *rwait;
    ushort msg_cbytes;
    ushort msg_qnum;
    ushort msg_qbytes; /* 队列上的最大字节数 */
    ushort msg_lspid; /* 上次 msgsnd 的 pid */
    ushort msg_lrpid; /* 上次接收的 pid */
};
```
