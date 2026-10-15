
为了比较两个文件的正确性（函数 `newer`），使用了文件状态中的最后修改时间（函数 `mtime`）。

> * cpp : 条件拷贝命令 */

```c
#include <stdio.h>
#include <sys/file.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <dirent.h>
#include <sys/param.h>
#include <string.h>
```

```c
void cpp(char* name, char* d1,char* d2) {
    char f1[MAXPATHLEN+1], f2[MAXPATHLEN+1];
    strcpy(f1,d1); strcpy(f2,d2); strcat(f1,"/");
    strcat(f2,"/"); strcat(f1,name); strcat(f2,name);
    if ( access(f2,F_OK) == -1 || newer(f1,f2) )
        printf("copy%s,%s\n", f1, f2);
}
```

```c
* 如果 file1 的最后修改时间比 file2 新 *
int newer(char* file1,char* file2) {
    return(mtime(file1) > mtime(file2));
}

/* 获取文件的最后修改时间 */
int mtime(char* file) {
    struct stat; // 从 stb 修正而来
    if (stat(file,&stb) < 0)
        perror(""); exit(1);
    return(stb.st_mtime);
}

int main(int argc,char* argv[]) {
    short i;
    DIR *dirp;
    struct dirent *dp;
    if (argc < 3) /* 需要至少两个参数 */
        fprintf(stderr, "%s: wrong number of arguments", argv[0]);
        exit(1);
    } else if (argc > 3) /* 指定了文件 */
        for ( i = 3; i < argc; i++)
            cpp(argv[i],argv[1],argv[2]);
    return(0);
}
/* 现在恰好有两个参数 */
if ((dirp = opendir(argv[0])) == NULL) {
    fprintf(stderr, "%s: can not open", argv[0]);
    exit(1);
} 
for (dp = readdir(dirp); dp != NULL; dp = readdir(dirp))
    if (strcmp(dp->d_name, ".") != 0)
        cpp(dp->d_name,argv[1],argv[2]);
```

## 在 C 程序中的 shell 级命令

当前目录是进程的属性，程序退出后你将返回原始目录。

查看一个用 C 语言编写的 UNIX 命令完整示例可能是恰当的。我们将讨论的命令是 `cpp`，它用于将文件从一个目录拷贝到另一个目录。特定文件是否拷贝，取决于是否有需要更新。以 shell 脚本实现的 `cpp` 版本在第 7.7 和 7.16 节中讨论过。

`cpp` 命令将文件从源目录拷贝到目标目录 `dest`。其用法为

`cp source dest [file...]`

指定的文件或所有文件（但不包括目录）将从 `source` 拷贝到 `dest`，需满足以下条件：

- 1. 如果文件不在 `dest` 中，则拷贝文件。
- 2. 如果文件已经在 `dest` 中，但源中的文件较新，则拷贝该文件。
- 3. 如果文件已经在 `dest` 中，且源中的文件并不较新，则不拷贝该文件。

为了比较两个文件的正确性（函数 `newer`），使用了文件状态中的最后修改时间（函数 `mtime`）。

# 第 11 章

# UNIX 系统编程

## 11.8 进程控制

当前目录是进程的属性，程序退出后你将返回原始目录。

查看一个用 C 语言编写的 UNIX 命令完整示例可能是恰当的。我们将讨论的命令是 `cpp`，它用于将文件从一个目录拷贝到另一个目录。特定文件是否拷贝，取决于是否有需要更新。以 shell 脚本实现的 `cpp` 版本在第 7.7 和 7.16 节中讨论过。

程序通过 `ld` 的 `-s` 选项加载，或者可执行文件已通过 UNIX 的 `strip` 命令处理。

头部为 `ld` 在内存中创建进程映像提供了信息，但其本身不会被加载到可执行映像中。通常，文本段（text segment）从内存中的虚拟地址 0 开始。文本段和数据段的具体布局以及文本段是否可共享（写保护）取决于系统和魔数（magic number）的值。已初始化数据空间存储源代码中带有初始值的全局和静态变量。未初始化数据区域存储其他全局和静态变量（自动初始化为零）。

栈占用了用户地址空间中最高的区域：从 `0xffffffff` 向下增长。栈根据需要动态扩展。系统保留一个指向当前栈顶的栈指针。数据段的当前上限被称为断点（breakpoint）。在程序执行期间，该断点保持固定，除非使用 `brk` 系统调用来更改它。断点和栈指针之间的虚拟内存地址不属于进程地址空间（图 11.6）。通常，虚拟地址空间的上部分留给 UNIX 内核，当进程在用户模式下运行时，该部分受到保护。当进程执行系统调用时，它进入内核模式。虽然每个进程都有自己的用户地址空间，但所有进程通常共享同一个内核。

除了这些用户区域外，每个进程还有一个名为 `u_area` 的内核数据栈区域，它包含特定进程的额外信息：

- 所有打开的文件描述符
- 打开的文件表
- 当前工作目录和根目录

## 图 11.6 进程的内存布局

| 段 | 地址 |
| :--- | :--- |
| 文本段 | 0x0 |
| 静态数据 |  |
| 动态数据 | 断点 |
| 未使用 |  |
| 栈 | 0x7ffffff |
| 内核 | 0x80000000 0xffffffff |

存储在 `u_area` 中的数据只能由进程执行 I/O、中断处理和上下文切换等操作系统功能时进行访问和操作。

### 进程表

UNIX 内核维护着一个全系统的进程表以控制所有进程。每个存在的进程都有一个表项。每个进程项包含以下信息：

| 字段 | 描述 |
| :--- | :--- |
| PID | 唯一的整数进程 ID |
| UID | 执行进程的用户的真实和有效用户 ID 及组 ID |
| State | 当前进程状态 |
| Event | 进程可能等待（睡眠）的任何事件 |
| Size | 进程的大小（内存需求） |
| Locations | 指向 `u_area` 的指针，以及指向进程特定区域的指针，该区域包含进程文本、数据和栈区域的指针 |
| Priority | 进程调度的参数 |
| Signals | 进程接收但尚未处理的信号 |
| Accounting | 计时信息，如执行时间、空闲时间、内核利用率等；用于调度和计费 |

## 11.9 ps 命令

你可以从 Shell 层级获取关于进程的各种信息。UNIX 命令 `ps`（显示状态）显示有关现有进程的信息。由于 UNIX 是多用户系统，且许多系统进程在执行各种任务以维持 UNIX 的运行，因此在任何时刻都有大量的进程。`ps` 命令尝试显示一组可能你感兴趣的合理进程。你可以给出选项来控制显示哪些进程子集。除非给出 `-a`（全部）选项，否则 `ps` 只显示你的进程的信息。同样，除非给出 `-l`（详细）选项，否则 `ps` 以短格式显示。

### ps 命令

`ps` 以长格式显示所有进程。选项 `-g`（Berkeley UNIX）或 `-d`（System V）强制显示包含某些进程。例如：

```
ps -al
ps -ag
```

如果你想包含后台进程，请添加 `-x` 选项。为每个进程提供的信息包括：

- PID: 进程 ID
- PPID: 父进程 ID
- STAT: 状态
- TIME: 使用的时间
- COMMAND: 命令

进程状态由四个字母表示。第一个字母表示可运行性：

- R: 可运行（Runnable）
- T: 已停止（Stopped）
- D: 不可中断的睡眠（磁盘 I/O）
- S: 睡眠中（Sleeping）
- Z: 僵尸进程（Zombie）

第二个字母表示优先级：

- N: 低优先级
- L: 普通优先级
- I: 空闲

第三个字母表示调度：

- P: 优先级
- <: 低
- >: 高

第四个字母表示内存状态：

- W: 已交换出内存（Swapped out）
- E: 在内存中
- : 正常

## 11.10 进程创建

C 程序内部使用 `fork` 调用来创建另一个进程。调用 `fork` 的进程称为父进程，新创建的进程称为子进程。`fork` 调用后，父子进程并发运行。图 11.7 显示了这种关系。在父进程中，它返回子进程的 PID，而在子进程中返回 0。如果 fork 失败，则不会创建子进程并返回 -1。以下是使用 fork 的模板：

```c
int pid;
if ((pid = fork()) == 0)
{
    /*在此处放置子进程的代码 */
```

图 11.7 进程创建

(img/ff919c7814d14d82e360c4f712d54e86_373_0.png)

```c
if (pid < 0)
{
    /* fork 失败，在此处放置错误处理 */
}
/* fork 成功，在此处放置父进程剩余的代码 */
```

```c
int main() {
    int pid, i, ans;
    int arr[DIM]={1,2,3,4,5,6,7,8};
    pid = fork(); /* child code begin */
    {
        ans = 0;
        for (i = 0; i < DIM ; i++) {
            ans = ans + arr[i];
            printf("Child: sum = %d\n", ans);
        }
        exit(0);
    } /* child code end */
    if (pid < 0) {
        fprintf(stderr,"fork failed\n");
        exit(1);
    }
    ans = 1;
    for (i = 0; i < DIM ; i++) {
        ans = ans * arr[i];
        printf("Parent: product = %d\n", ans);
    }
}
```

父进程和子进程都可以访问自己的数组 `arr`、变量 `ans` 等副本。两个进程同时向 `ans` 赋值这一事实并不重要，因为程序运行在不同的地址空间中。以下是该程序的一种可能的输出：

Parent: product = 1

Child: sum = 1

Parent: product = 2

Child: sum = 3

Child: sum = 6

Parent: product = 6

Child: sum = 10

Parent: product = 24

Parent: product = 120

Child: sum = 15

Parent: product = 720

Child: sum = 21

Child: sum = 28

Parent: product = 5040

Child: sum = 36

Parent: product = 40320

取决于执行相对速度和其他系统负载因素，父进程和子进程的输出行可能会以不同的方式交错出现。

## 程序执行：exec 例程

子进程并不限于执行父进程中的语句子集。它还可以通过用一个可执行文件覆盖自身来执行另一个程序。目标可执行文件被读取到正在执行进程的地址空间之上，覆盖内存中的内容，并从文件中定义的入口点继续执行。结果是子进程开始执行一个新程序，其执行环境与现在被替换的旧进程相同。

这种程序覆盖可以由任何 `exec` 例程启动，包括库函数 `exec`、`execve`、`execcl` 等几个，它们都是基本 `exec` 系统调用的变体。然而，为了避免混淆，我们在讨论这些例程的通用特性时将使用共同前缀 `exec`。

对于调用程序来说，`exec` 是一个永返回的调用。`exec` 调用结合 `fork` 可以产生运行另一个程序的新进程：

- 1. 进程 A（父进程）调用 `fork` 产生子进程 B。
- 2. 进程 B 立即调用 `exec` 运行新程序。

`exec` 将调用进程转换为新进程。新进程由一个可执行文件构建。可执行文件可以是一个 `.out` 文件，或者是解释器（一个可执行文件）的命令文件。可执行对象（a.out）的格式刚刚讨论过。可执行文本文件以如下形式的行开头：

```
#!interpreter
```

要运行可执行文本文件，由第一个系统 `exec` 指定解释器，将文件作为第一个参数传递它，随后是原始的其他参数。例如，一个 csh 脚本可能以该行开头：

```
#!/bin/csh
```

而一个 sh 脚本则以

```
#!/bin/sh
```

如第 7 章所述。

在执行 `exec` 调用后，以下属性保持不变：

- 进程 ID (PID)、父进程 ID 和进程组 ID
- 进程所有者 ID（除非是 set-userid 程序）
- 访问组 ID（除非是 set-groupid 程序）
- 工作目录和根目录
- 会话 ID 和控制终端
- 资源使用情况
- 间隔定时器
- 资源限制
- 文件创建权限掩码 (umask)
- 信号掩码
- 环境变量值

此外，在调用进程中打开的描述符通常在新进程中仍然保持打开。被忽略的信号在 *exec* 过程中保持被忽略，被捕获的信号将重置为默认值。信号处理在第 11.15 节讨论。

各种 *exec* 例程的区别在于它们接受的参数类型和数量。`execv`(char *filename, char *argv[]) 字符串数组
