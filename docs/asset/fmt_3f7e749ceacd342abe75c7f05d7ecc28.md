
```c
#define MAXLINE 200

static bool getargs(int *argcp, char *argv[], int max, bool *eofp)
{
    static char cmd[MAXLINE];
    char *cmdp;
    int i;

    *eofp = false;
    if (fgets(cmd, sizeof(cmd), stdin) == NULL) {
        if (ferror(stdin))
            EC_FAIL
        *eofp = true;
        return false;
    }
    if (strchr(cmd, '\n') == NULL) {
        /* eat up rest of line */
        while (true) {
            switch (getchar()) {
                case '\n':
                    break;
                case EOF:
                    if (ferror(stdin))
                        EC_FAIL
                default:
                    continue;
            }
            break;
        }
    }
    printf("Line too long -- command ignored\n");
    return false;

cmdp = cmd;
for (i = 0; i < max; i++) {
    if ((argv[i] = strtok(cmdp, " \t\n")) == NULL)
        break;
    cmdp = NULL; /* tell strtok to keep going */
}
if (i >= max) {
    printf("Too many args -- command ignored\n");
    return false;
}

*argcp = i;
return true;

EC_CLEANUP_BGN
    EC_FLUSH("getargs")
    return false;
EC_CLEANUP_END
}
```

注释：

- `getargs` 如果成功解析参数则返回 `true`，否则返回 `false`。

- 它使用标准 C 函数 `fgets` 读取一行输入。如果输入了较长的行，该函数是足够安全的，因为它不会超出我们传入的缓冲区。但在这种情况下，我们不希望留下未读取的字符以便稍后读取，因为它们本身将是一个意外的、潜在破坏性的 shell 命令。因此，在这种情况下（没有换行符终止），我们在打印错误消息之前读取并丢弃该行的剩余部分。

- 然后我们使用 `strtok` 将该行分解为其参数。（我们在上一节的 `execvp2` 中也使用了 `strtok`。）

- 如果调用的库函数发生真实错误，`getargs` 使用 `EC_FLUSH` 显示其自身的错误消息；否则——例如行太长的情况——打印用户消息。

接下来，我们需要处理内置命令 `assignment` 和 `set` 的函数。这些很容易，因为我们可以使用第 5.2 节中的环境变量操作技术：

```c
extern char **environ;

void set(int argc, char *argv[])
{
    int i;

    if (argc != 1)
        printf("Extra args\n");
    else
        for (i = 0; environ[i] != NULL; i++)
            printf("%s\n", environ[i]);
}

void ass(int argc, char *argv[])
{
    char *name, *val;
    if (argc != 1)
        printf("Extra args\n");
    else {
        name = strtok(argv[0], "=");
        val = strtok(NULL, ""); /* get all that's left */
        if (name == NULL || val == NULL)
            printf("Bad command\n");
        else
            ec_neg1( setenv(name, val, true) )
    }
    return;

    EC_CLEANUP_BGN
        EC_FLUSH("asg")
    EC_CLEANUP_END
}
```

接下来，我们通过主函数完成程序，该函数打印提示符字符（我们使用 `@`），获取参数，检查命令是否是内置的，如果不是，则尝试执行它：

```c
#define MAXARG 20

int main(void)
{
    char *argv[MAXARG];
    int argc;
    bool eof;

    while (true) {
        printf("@ ");
        if (getargs(&argc, argv, MAXARG, &eof) && argc > 0) {
            if (strchr(argv[0], '=') != NULL)
                asg(argc, argv);
            else if (strcmp(argv[0], "set") == 0)
                set(argc, argv);
            else
                execute(argc, argv);
        }
        if (eof)
            exit(EXIT_SUCCESS);
    }
}

static void execute(int argc, char *argv[])
{
    execvp(argv[0], argv);
    printf("Can't execute\n");
}
```

请注意，只有当 `execvp` 失败时，我们才会循环回到打印另一个提示符。这就是为什么我们不太可能觉得这个 shell 有用的原因。无论如何，这是一个会话示例（为了节省空间，环境变量列表已省略）：

```
$ sh0
@ set
SSH_CLIENT=192.168.0.1 4971 22
USER=marc
MAIL=/var/mail/marc
EDITOR=vi
@ LASTNAME=Rochkind
@ set
SSH_CLIENT=192.168.0.1 4971 22
USER=marc
MAIL=/var/mail/marc
EDITOR=vi
LASTNAME=Rochkind
@ echo Hello World!
Hello World!
$
```

注意末尾的美元符号提示符——执行 `echo` 后，我们的 shell 已退出。实际上，退出的是 `echo`，因为它是替代 shell 的程序。显然，shell 在各自的进程中执行命令会更好，而这正是我们要去的方向。

### 5.5 fork 系统调用

`fork` 在某种程度上与 `exec` 相反：它创建一个新的进程，但不从新程序初始化它。相反，新进程的指令、用户数据和系统数据段几乎完全是旧进程的副本。

```
fork—create new process

#include <unistd.h>
pid_t fork(void);
/* Returns child process-ID and 0 on success or -1 on error (sets errno) */
```

在 `fork` 返回后，*两个* 进程（父进程和子进程）都会收到返回。然而，返回值不同，这一点至关重要，因为这允许它们后续的行为不同。通常，子进程执行一个 `exec`，而父进程要么等待子进程终止，要么去做其他事情。

子进程从 `fork` 接收到 0 的返回值；父进程接收到子进程的进程 ID。如往常一样，返回 −1 表示错误，但由于 `fork` 没有

对于参数而言，调用者不可能做错任何事。错误的原因只能是资源耗尽，例如交换空间不足或已运行的进程过多。父进程可能不希望直接放弃，而是稍等片刻（例如使用 `sleep`）再重试，尽管这通常不是 shell 的做法——它们会打印一条消息并重新提示。

回想一下，由 `exec` 系统调用启动的程序保留了许多属性，因为系统数据段几乎未被改动。同样，由 `fork` 创建子进程会继承父进程的大部分属性，因为它的系统数据段是从父进程复制而来的。正是这种继承机制，使得用户能够 shell 中设置某些属性（如当前目录、有效用户 ID 和优先级），这些属性随后将应用于后续调用的每个命令。可以想象这些属性属于“直系家庭”，尽管这不是一个正式定义的 UNIX 术语。

只有少数几个属性不被继承：

- 显然，子进程的进程 ID 和父进程 ID 是不同的，因为它是另一个进程。

- 如果父进程正在运行多个线程（第 5.17 节），只有执行了 `fork` 的那个线程存在于子进程中。然而，所有线程在父进程中保持完好。

- 子进程获得父进程打开文件描述符的副本。每个副本都指向同一个文件，且文件指针具有相同的值。如果打开的文件描述（第 2.2.3 节）共享，因此文件偏移量也是共享的。如果子进程通过 `lseek` 修改了它，那么父进程的下一次读或写将发生在新的位置。然而，文件描述符本身是独立的：如果子进程关闭了它，父进程的副本不会受到影响。

- 子进程的累计执行时间被重置为零，因为它处于生命周期的开始阶段。

（这些是主要的属性——完整列表请参见附录 A。）

下面是一个简单的例子，展示了 `fork` 的效果：

```c
void forktest(void)
{
 int pid;

 printf("Start of test\n");
 pid = fork();
 printf("Returned %d\n", pid);
}
```

输出结果：

```
$ forktest
Start of test
Returned 98657
Returned 0
$
```

在这种情况下，父进程在子进程之前执行了其 `printf`，但一般来说，你不能依赖哪一个先执行，因为进程是独立调度的。如果顺序很重要，你需要像第 9.2.3 节解释的那样自己同步这两个进程。正如那里所示，你可以用管道来做到这一点，或者较难地用信号来实现。

让我们再次运行 `forktest`，但这次将标准输出重定向到一个文件：

```
$ forktest >tmp
$ cat tmp
Start of test
Returned 56807
Start of test
Returned 0
$
```

这次 "Start of test" 被写了两次！你能想通为什么吗？（下一段会有剧透。）

发生的情况是，`printf` 缓冲了其输出（如第 2.12 节所述），而子进程继承了未刷新的缓冲区以及所有内容。当子进程退出时，它刷新了缓冲区，父进程也刷新了缓冲区。之前，当输出未被重定向时，`printf` 没有缓冲，因为它知道标准输出是一个终端设备，应该更具交互性地行为。我将在第 5.7 节讨论如何控制退出的副作用。

`fork` 和 `exec` 是完美搭档，因为由 `fork` 创建的子进程，作为父进程的近似克隆，通常并不实用。但它非常适合被新程序覆盖，而这正是 `exec` 所做的。我们将在下一节中随着改进我们的 shell 来看到这一点。

`fork` 的开销可能非常大。它费尽周折去克隆父进程，或许复制了一个庞大的数据段（指令段通常是只读的，可以共享），结果只执行了几百条指令就重新初始化了代码段和数据段。这看起来很浪费，事实也是如此。在虚拟内存版本的 UNIX 中，复制特别昂贵，使用了一种巧妙的解决方案，称为写时复制（copy-on-write）。其工作原理如下：在 `fork` 时，父进程和子进程共享数据段，它由一组页面组成。只要页面保持未修改，这种捷径就能正常工作。然后，一旦父进程或子进程试图写入某个页面，仅该页面就会被复制，使每个进程拥有自己的版本。在拥有适当类型的动态地址转换硬件的情况下，这是透明且高效的，几乎所有现代计算机都有这种硬件。由于在几乎所有情况下 `exec` 紧随其后，因此很少有页面需要被复制。但即使所有页面都需要复制，我们也不会更差——事实上，我们情况更好，因为我们能够更早地开始运行子进程。请记住，写时复制方案是内核内部的，它不改变 `fork` 的语义，除了性能提升外，用户对此并不知情。

比写时复制效率更高，但透明度较差的是 `fork` 的一种变体，称为 `vfork`：

```
vfork—创建新进程；共享内存（已废弃）

#include <unistd.h>
pid_t vfork(void);
/* 成功时返回子进程 ID 和 0，错误时返回 -1（设置 errno） */
```

`vfork` 在创建子进程方面表现得与 `fork` 完全相同，但父进程和子进程共享同一个数据段。没有写时复制——它们都读写相同的变量，除非子进程立即退出或执行 `exec`，否则就会引发混乱，而这通常是正常发生的情况（参见下一节中的示例函数 `execute2`）。在早期版本的 BSD UNIX 中，`vfork` 很重要；然而，它相对于 `fork` 的性能优势已不再显著，且使用它是危险的，因此你不应该使用它，这就是为什么在函数概要中标注为“已废弃”。

为了提高 `fork` 和 `exec` 的效率，最近的一次尝试是 `posix_spawn`，它是 1999 年 POSIX 更新的一部分。由于其最终结果是运行不同程序的子进程，它避免了 `vfork` 的问题。它不提供单独的 `fork` 和 `exec` 的所有灵活性，但它确实处理了最常见的情形（例如，复制文件描述符）。`posix_spawn` 的真正目的是在实时系统中提供一种高效的方式来作为子进程调用程序，此时交换过于缓慢且硬件缺乏动态地址转换。有可能将 `posix_spawn` 实现为一个使用 `fork` 和 `exec` 的库函数（练习 5.8），但在设计者设想的那类实时系统中，`posix_spawn` 必须作为系统调用实现。

现在是时候提一下标准 C 函数 `system` 了：

```
system—运行命令

#include <stdlib.h>

int system( const char *command /* 命令 */
); /* 返回退出状态，错误时返回 -1（设置 errno） */
```

此函数执行一次 `fork`，然后执行 shell 的 `exec`，将命令参数作为 shell 命令行传递。它是一种从程序内部执行命令行的便捷方式，但它不提供单独的 `fork` 后接 `exec` 或 `posix_spawn` 的效率（shell 始终被调用）或灵活性。

### 5.6 实现 Shell（版本 2）

现在让我们把 `fork` 和 `execvp` 结合起来，使上一节中的 shell 变得更加有用——它在运行完一个命令后不会直接退出，而是实际上会提示输入另一个命令！我们用 `execute2` 替换函数 `execute`：

```c
static void execute2(int argc, char *argv[])  {
    pid_t pid;

    switch (pid = fork()) {
    case -1:  /* 父进程（错误） */
    EC_PFAIL
    case 0:  /* 子进程 */
    execvp(argv[0], argv);
    EC_PFAIL
    default:  /* 父进程 */
    ec_neg1( wait(NULL) )
    }
    return;

EC_CLEANUP_BGN
    EC_FLUSH("execute2*")
    if (pid == 0)
       _exit(EXIT_FAILURE);
EC_CLEANUP_END
}
```

我将在第 5.8 节详细介绍 `wait`；目前，你只需要知道它会等待子进程终止后再返回。

此函数对来自 `fork` 和 `wait` 的错误与来自 `execvp` 的错误处理方式不同。如果 `fork` 或 `wait` 返回 -1，我们在父进程中，因此只需打印错误信息（使用 `EC_FLUSH`）并返回。调用者（上一节的 `main`）随后会再次提示用户，这是我们所期望的——shell 不应该因为出错而终止。但如果 `execvp` 返回，我们在子进程中，而不是父进程中，最好应该退出。否则，子进程将继续运行，我们将有两个 shell 在提示输入命令。如果我们真的尝试输入命令，两个进程会争夺字符，每个进程都会读取其中的一部分，因为单个字符只能被读取一次。如果我们例如输入 `rm t*`，而其中一个 shell 读取了 `rm *`，另一个读取了 `t`，这可能会产生严重后果。

我们使用 `_exit` 而不是 `exit`，原因我将在下面解释。

### 5.7 exit 系统调用和进程终止

进程终止正好有四种方式：

- 1. 调用 `exit`。从 `main` 返回一个值等同于调用 `exit` 并将该值作为参数，不带值返回等同于返回 0。

- 2. 调用 `_exit` 或其等价物 `_Exit`，这是两种即将解释的 `exit` 变体。

- 3. 接收到终止信号。

- 4. 系统崩溃，原因可能从电力故障到操作系统 bug 都有可能。本节关注前两种情况，第 9 章讨论信号，而对于崩溃，实际上没什么可说的，进程只是停止而已。 6

> 5. 两个进程并发地读写相同的变量与线程类似，具有类似的潜在危险。第 5.17 节有更多内容。

> 6. 某些计算机在电力故障时会向进程发送信号，但这只是将其变为第三种情况。

三种 `_exit` 变体之间的区别如下：
