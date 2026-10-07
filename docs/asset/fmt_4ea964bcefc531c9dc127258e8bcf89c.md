
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

`child_stack`参数指向子进程使用的栈。如果给定值为`0`，子进程将获得与父进程相同的栈指针。然而，一旦其中任何一个修改了栈，写时拷贝（copy-on-write）技术将确保它们获得自己的副本。

然而，如果子进程和父进程共享同一内存区域（即它们是轻量级进程或线程），则该值必须不为空。父进程必须为子栈设置内存并传递指针。（注意，栈是向下增长的，因此该指针应指向子栈的最顶地址。）

`flags`参数有多个用途。它的低字节应包含子进程死亡时发送给父进程的信号数量（例如`SIGCHLD`）。这是与以下值的任何组合进行按位或操作的结果，用于控制父子进程之间的共享内容：

### 表 13.2: `clone()` 标志

| 标志 | 已设置 | 未设置 |
|---|---|---|
| `CLONE_VM` | 父进程和子进程共享内存；一个进程对内存的写入对另一个进程以及两个进程都可见。 | 每个进程拥有自己的内存空间，受`fork()`的写时拷贝行为影响。 |
| `CLONE_FS` | 父子进程共享文件系统信息，包括根挂载点、当前工作目录、umask。注意，这意味着如果子进程执行了`chdir()`等调用，也会影响父进程！ |  |
| `CLONE_FILES` | 父子进程共享文件描述符表，该表引用每个进程中的文件。如果任何一个进程打开或关闭文件描述符，另一个将受到影响。 | 它们从相同的表开始，但随后随着打开和关闭操作可能会发生分离。 |
| `CLONE_SIGAND` | 父子进程共享相同的信号处理器。任何一个进程调用`sigaction()`都会影响另一个。另一方面，每个进程都有自己的信号掩码和挂起信号，一个进程可以阻塞或取消某个信号而不影响另一个。 | 子进程获得父进程的信号处理器，但随后的更改不会影响另一个进程。 |
| `CLONE_PID` | 子进程与父进程具有进程 ID。这只在线程中允许。 | 子进程获得新的进程 ID |
| `CLONE_TRACE` | 如果父进程正在被`ptrace()`系统调用追踪，则子进程也将追踪。 | 即使父进程正在被追踪，也不追踪子进程。 |
| `CLONE_VFORK` | 系统调用使用。如果父进程要求子进程在释放其内存区域时唤醒它。 |  |
| `CLONE_PARENT` | 克隆进程将具有克隆者相同的父进程。 |  |
| `CLONE_THREAD` | 克隆进程将具有克隆者相同的线程组。 |  |

还有其他可以使用的特殊标志：请咨询`clone()`的手册页。

因此，`fork()`系统调用的标志为`SIGCHLD`，`vfork()`的标志为`SIGCHLD | CLONE_VM | CLONE_FORK`。

### 13.5 退出

以下函数会导致进程终止：

```c
#include <unistd.h>
void _exit(int status);

#include <stdlib.h>
void exit(int status);
```

正常终止可以通过三种方式发生：

- 从`main()`返回；这等同于调用`exit()`。
- 调用`exit()`。刷新流。
- 调用`_exit()`。关闭流。

异常终止可以通过两种方式发生：

- 被未捕获的信号终止。
- 调用`abort()`。

以下函数是异常的：

```c
#include <stdlib.h>
void abort(void);
```

`on_exit()`与`atexit()`类似，但它传递参数。

也可以使用析构方法，正如我们在文中所述。

### 13.6 构造函数和析构函数

编译器允许使用特殊的构造和析构函数。

构造函数在`main()`程序之前被调用。

析构函数在调用`exit()`后被调用；如果没有显式调用`exit()`或`return()`，析构函数仍会被调用。

我们在讨论中已经见过这些方法用法，这里重复示例：

```c
/* 使用属性声明它们 */
void init_fun(void) __attribute__ ((constructor));
void exit_fun(void) __attribute__ ((destructor));
/* 定义它们 */
void init_fun(void) { ... whatever };
void exit_fun(void) { ... whatever };
```

### 13.7 等待

父进程可以等待（挂起执行）直到一个子进程死亡或停止，或者被信号中断。

```c
#include <sys/types.h>
#include <sys/wait.h>

pid_t wait(int *status);
pid_t waitpid(pid_t pid, int *status, int options);
```

`wait()`在任何子进程返回；`waitpid()`在特定的进程或进程集返回。

`status`包含进程的退出状态，除非将其设置为`NULL`。可以使用以下查询宏：

### 表 13.3: 等待状态查询宏

| 宏 | 含义 |
|---|---|
| `WIFEXITED(status)` | 如果子进程正常退出。 |
| `WEXITSTATUS(status)` | 如果`WIFEXITED`为非零，返回进程退出码。 |
| `WIFSIGNALED(status)` | 被未捕获的信号终止。 |
| `WTERMSIG(status)` | 如果`WIFSIGNALED`为非零，返回信号号。 |
| `WIFSTOPPED(status)` | 如果子进程因信号停止。 |
| `WSTOPSIG(status)` | 如果`WIFSTOPPED`为非零，返回信号号。 |

宏`WIFSTOPPED()`和`WSTOPSIG()`只有在给出`WUNTRACED`标志时才有意义。

`pid`可以取以下值：

### 表 13.4：`pid`值及等待对象

| 值 | 含义 |
|---|---|
| `pid < -1` | 等待进程组 ID 等于`pid`的任何子进程 |
| `pid = -1` | 等待任何子进程。（与使用`wait()`相同） |
| `pid = 0` | 等待进程组 ID 与调用进程相同的任何子进程 |
| `pid > 0` | 等待 ID 等于`pid`的子进程 |

`options`标志用于修改行为，它是`0`与以下一个或多个（或两者）的逻辑或（OR）结果：

### 表 13.5：等待选项标志

| 标志 | 含义 |
|---|---|
| `WNOHANG` | 如果没有子进程退出，则立即返回 |
| `WTRACED` | 为状态尚未报告的停止状态子进程返回 |

这些函数在成功时返回退出的子进程的`pid`，失败时返回`-1`（并设置`errno`）。可能的错误返回值为：

### 表 13.6：Wait 函数错误返回值

| 值 | 含义 |
|---|---|
| `EINVAL` | `options`参数无效 |
| `ECHILD` | `pid`不存在或它不是调用进程的子进程 |
| `ERESTARSYS` | 未设置`WNOHANG`且捕获了未阻塞的信号或`SIGCHLD`。在这种情况下可能会实际返回`EINTR` |

### 13.8 守护进程 (Daemon Processes)

守护进程在后台运行，不直接受用户控制。按照惯例，守护进程的名称通常以字母`d`结尾；例如`klogd`、`cupsd`、`nfsd`、`xinetd`等。

创建守护进程的基本步骤是`fork()`出一个子进程并终止父进程；然后子进程将由进程 ID 为`1`的`init`进程接纳。

还会采取其他步骤，包括：

- 关闭所有文件描述符，然后将`stdin`、`stdout`和`stderr`重定向到`/dev/null`，从而切断与与控制终端的任何关联。
- 成为会话组和进程组组长。
- 将根目录设置为`/`。这使得进程可能会卸载其启动时所在的文件系统，同时也避免了依赖于进程启动位置的安全或其他错误。

人们可以手动构建这一切，但为了方便，可以使用该函数：

```c
#include <unistd.h>
int daemon (int nochdir, int noclose);
```

如果`nochdir`不为零，则根目录不会重置为`/`。

如果`noclose`不为零，则标准输入、输出和错误将不会重定向到`/dev/null`。

### 13.9 实验

### 实验 1：Fork

编写一个简单的`fork`示例：

父进程和子进程必须能够识别自己是谁。

父进程应该等待子进程终止。

### 实验 2：僵尸 (Zombie Limescale)

修改之前的`fork`程序，使子进程快速终止，而父进程使用`sleep()`休眠一段时间。

在一个终端窗口中运行该进程（或使用`&`在后台运行），同时使用`ps ux`监控你的活动进程，注意子进程的状态。当父进程退出时，子进程应该消失。

### 实验 3：更多的 Fork 和等待

修改上一节中的`ls`，使得对于发现的子目录（可以使用`stat()`和`S_ISDIR()`检测目录），都会`fork()`出一个子进程来处理该子目录（你可能想跳过`.`和`..`）。

如果输出变得太混乱，可以让父进程`wait()`等待每个子进程完成。

`108`第`13`节 进程 - II

创建过多的进程可能会导致机器挂起。查看`help ulimit`并输入`ulimit -a`获取当前限制。将最大进程数设置为合理的值。

### 实验 4：克隆 (Cloning)

编写一个短程序，使用`clone()`系统调用创建共享所有内存资源的主线程和从线程。

设置一个全局变量，并证明任何一个线程都可以修改它，另一个线程可以看到该值。

创建从线程栈指针时要小心，使其指向栈顶，因为栈是向下增长的。

如果从线程在主线程之前死亡会发生什么？

注意，你可以将此作为你自己不使用标准线程库的多线程编程方法的核心。你也可以尝试共享文件描述符或等。

### 实验 5：退出 (Exiting)

让程序使用`aexit()`（或`on_exit()`），或使用构造/析构方法来处理退出。

注册至少两个在退出期间处理的句程序。

你能让发生的情况取决于你的主例程返回的退出代码吗？

### 实验 6：内存映射 (Memory Mapping)

编写一个使用匿名内存映射进行父子通信的程序。

让子进程写入内存映射区域，并让父进程从中读取。

### 实验 7：守护进程 (Daemons)

编写一个启动守护进程的简单程序。它可以简单到只需调用`pause()`休睡眠直到接收到信号。

程序运行后，输入`ps 1x`以验证它是否在后台运行以及其进程是否为`init`。

向守护进程发送信号以中断休眠；例如，可以使用`kill -SIGUSR1 <pid>`。该进程应该消失。

## 第 14 章

## 管道 (Pipes) 和命名管道 (Fifos)

我们将学习更通用地创建和使用命名管道 (`FIFOs`)。我们还将学习`splice()`、`vmsice()`和`tee()`。

- `14.1`管道和进程间通信 ...... `109`
- `14.2` `popen()`和`pclose()` ...... `110`
- `14.3` `pipe()` ...... `111`
- `14.4`命名管道 (`FIFOs`) ...... `113`
- `14.5` `splice()`, `vmsice()` and `tee()` ...... `114`
- `14.6`实验 ...... `116`

### 14.1 管道和进程间通信

管道允许进程交换数据，而不只是信号。这些进程可以是相互独立的，也可以是父子关系。

进程也可以使用管道从命令接收输入或直接输出到命令。

人们经常通过`|`符号从命令行调用管道；例如：

`133`第`14`章 管道和命名管道

`$ ls -l | sort | tail -20`

三个独立的进程（`ls`、`sort`和`tail`）将同时运行，并通过管道传递数据，无需临时文件。

在下文中，我们将关注能够高效实现此点的编程接口。

### 14.2 popen() 和 pclose()

这些函数使用标准 I/O 库打开和关闭管道：

```c
#include <stdio.h>

FILE *popen(const char *command, const char *mode);
int pclose(FILE *stream);
```

`popen()`通过创建管道、`fork`和调用`shell`（使用`system()`调用）来启动进程。

`mode`参数与`popen`相同。但它只能取`"r"`或`"w"`。不允许`"r+"`或`"w+"`以及追加模式。

`command`参数指向一个非终止字符串，该字符串包含传递给`/bin/sh`的命令行（使用`-c`标志读取但不进行任何解释）。

- 向流写入写入命令的`stdin`；命令的`stdout`与调用`popen()`的进程相同。
- 同样，从流读取的是命令的`stdout`，而命令的`stdin`与调用`popen()`的进程相同。

`popen()`返回正常的 I/O，但必须使用`pclose()`而不是`fclose()`关闭。如果底层的`pipe()`或`fork`调用或内存无法分配，将返回`NULL`且不设置`errno`。如果参数无效，`errno`将设置为`EINVAL`。

`pclose()`等待关联进程终止并返回命令的退出状态。如果检测到错误，则返回`-1`。

例如：

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main ( {
    FILE *fp;
    int nbytes, BSIZE=getpagesize();
```

# PIPE()

```
char *buffer = malloc(BSIZE);
fp = open("finger", "r");
while ((bytes = read(buffer, 1, BSIZE, fp)) > 0) {
    fwrite(buffer, bytes, stdout);
}
printf("EOF = %d and Error = %d\n", feof(fp), ferror(fp));
close(fp);
exit(EXIT_SUCCESS);
```

### 14.3 pipe

低级函数`pipe()`在两个进程之间传递数据，而无需经过调用`shell`的开销，并提供了更多的控制：

```c
#include <unistd.h>
```

```c
int pipe(int filefds[2]);
```

父进程和子进程可以建立连接，甚至一个进程可以连接到自己。

管道有一个读端和一个写端；任何写入`filefds[1]`的数据都可以从`filefds[0]`回。数据按照先入先出（FIFO）的原则处理。

`filefds`是文件描述符；因此必须使用`read()`和`write()`，而不是`read()`和`write()`。

这些管道的具体工作方式在不同的 Unix 变体之间略有不同。在 System V 中，管道是全双工的；两个描述符都可以读和写。在 Posix 标准中，每个进程在用另一端之前必须关闭管道的一端。在 Linux 下，每个管道的通信仅是单向的，不需要执行关闭操作。在编写代码时请记住这些考虑。

成功时返回`0`，出错时返回`-1`（并设置`errno`）。可能的错误返回值为：

### 表 14.1：`pipe()`错误返回值

| own | 含义 |
|---|---|
| `ENFILE` | 进程使用的文件描述符过多，或系统文件表已满。 |
| `EFAULT` | `filefds`无效。 |

一个简单的`pipe()`示例：

```c
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
```

```c
int main ()
{
    int rc, filep[2], length;
    char *in_data = "data";
    char *out_data;
    length = strlen(in_data) + 1;
    out_data = malloc(length);
    memset(out_data, 0, length);

    if (pipe(filep) == 0) {
        rc = write(filep[1], in_data, 4);
        printf("wrote %d bytes\n", rc);
        rc = read(filep[0], out_data, 4);
        printf("read %d bytes which were %s\n", rc, out_data);
        exit (EXIT_SUCCESS);
    }
    exit (EXIT_FAILURE);
}
```

子进程和父进程之间的简单管道示例：

```c
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <errno.h>
#include <sys/wait.h>
```
