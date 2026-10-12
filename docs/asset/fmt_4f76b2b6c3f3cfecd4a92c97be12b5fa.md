
第 15 行使用 `getpid()` 获取初始进程的 PID。第 17–20 行获取子进程 PID，并检查是否有错误返回。

第 21–24 行由子进程执行：第 22 行获取 `PPID`。第 23 行使进程暂停两秒（参见第 10.8.1 节，“闹钟：`sleep()`, `alarm()`, and `SIGALRM`”，第 382 页获取关于 `sleep()` 的信息），然后第 24 行再次获取 `PPID`。

第 25–27 行在父进程中运行。第 26 行让父进程延迟一秒，给子进程留出足够的时间调用 `getpid()`。第 27 行父进程退出。

第 31–34 行打印值。注意，在 `fork` 之前设置的变量 `parent` 在子进程仍然保持其值。`fork` 之后，两个进程拥有其地址空间完全相同但独立的副本。以下是程序运行时发生的情况：

```bash
$ ch09-reparent

$ Original parent: 6582

Child: 6583

Child's old parent: 6582

Child's new parent: 1

Parent's PID: 6582

Child's PID: 6583
```

`test1` 的第一个可执行部分从标准输入读取一行，从而改变文件的偏移量。`test1` 的第二行在子 shell 中运行括号中的命令。这是一个独立的进程——正如你所想的——它是通过 `fork()` 创建的。子 shell 继承了父进程的标准输入，包括当前文件。该进程读取一行并更新文件中的共享偏移量。当回到父进程 shell 的第三行再次读取文件时，它将从子进程停止的地方开始。

| PID | 动作 | 结果 |
| :--- | :--- | :--- |
| 6582 | Original parent | 6582 |
| 6583 | Child | 6583 |
| 6583 | Child's old parent | 6582 |
| 6583 | Child's new parent | 1 |
| 6582 | Parent's PID | 6582 |
| 6583 | Child's PID | 6583 |

图 9.2 `ch09-reparent.c` 的进程流程

`test1` 的第一个可执行部分从标准输入读取一行，从而改变文件的偏移量。`test1` 的第二行在子 shell 中运行括号中的命令。这是一个独立的进程——正如你所想的——它是通过 `fork()` 创建的。子 shell 继承了父进程的标准输入，包括当前文件。该进程读取一行并更新文件中的共享偏移量。当回到父进程 shell 的第三行再次读取文件时，它将从子进程停止的地方继续。

### 9.1.3 设置进程优先级：`nice()`

随着进程运行，内核会动态调整。设计一个良好的内核调度器是一门艺术；具体的细节超出了本书的范围。然而，进程可以通过其 `nice` 值来影响内核的优先级分配。

`nice` 值是进程对其他进程有多“友好”的指标。因此，较高的 `nice` 值表示进程越耐心；即对其他进程越友好，降低其相对于其他进程的优先级。

负的 `nice` 值则表示进程希望对其他进程“不友好”。这样的进程更自私，想要更多的 CPU 时间。幸运的是，虽然用户可以增加自己的 `nice` 值（变得友好），但只有 `root` 可以降低 `nice` 值（变得不友好）。

要更改 `nice` 值，请使用 `nice()` 系统调用：

```c
#include <unistd.h>

int nice(int inc);
```

默认的 `nice` 值为 0。允许的 `nice` 值范围是 -20 到 19。这需要一些适应。值越负，优先级越高：-20 是最高优先级（不友好），19 是最低优先级（最友好）。

`inc` 参数是更改 `nice` 值的增量。使用 `nice(0)` 在不改变值的情况下获取值。如果 `current_nice_value + inc` 的结果超出了 -20 到 19 的范围，系统将强制结果处于范围之内。

## 9.1 进程创建与管理

返回值是新的 `nice` 值，如果发生错误则返回 -1。由于 -1 也是一个有效的 `nice` 值，在调用 `nice()` 时，必须显式地将 `errno` 设置为零，然后再检查它以是否存在问题：

```c
int niceval;
int inc = /* whatever */;

errno = 0;
if ((niceval = nice(inc)) < 0 && errno != 0) {
    printf(stderr, "%d failed: %s\n", inc, strerror(errno));
    /* 其他恢复措施 */;
}
```

如果 `inc` 为负值且进程没有以 `root` 身份运行，此示例可能会失败。

### 9.1.3.1 POSIX 与现实

Linux 使用的从 -20 到 19 的 `nice` 值具有历史性的；它至少可以追溯到 `V7` 版本。`POSIX` 使用更间接的语言来描述这种情况，这在保持历史兼容性的同时允许了实现上的灵活性。这也使得标准变得更难阅读和理解，不过，这正是你读这本书的原因。以下是 `POSIX` 对它的描述：

首先，由系统维护的进程 `nice` 值范围从 0 到 `'2 * NICE - 1'`。常量 `NICE` 定义在 `<limits.h>` 中，且至少为 20。这给了我们 0–39 的范围。

其次，正如我们描述的，当前 `nice` 值与增量 `incr` 之和被强制限制在这个范围内。

最后，`nice()` 的返回值是进程 `nice` 值减去 `NICE`。当 `NICE` 值为 20 时，这给了我们最初描述的 -20 到 19 的范围。

结论是，`nice()` 的返回值范围实际上是 `'-NICE'` 到 `'NICE-1'`，最好使用符号常量编写代码。然而，从实践来说，你不太可能找到 `NICE` 不为 20 的系统。

### 9.1.4 启动新程序：`exec()` 族

一旦新进程运行（通过 `fork()`），下一步是在进程中启动一个不同的程序。有多个函数提供不同的用途：

```c
#include <unistd.h>

int execve(const char *filename, char *const argv[], char *const envp[]);

int execcl(const char *path, const char *arg, ...);
int exepl(const char *file, const char *arg, ...);
int execle(const char *path, const char *arg, ..., char *const envp[]);
int execv(const char *path, char *const argv[]);
int execvp(const char *file, char *const argv[]);
```

`POSIX` | 系统调用 | 封装函数

我们将这些函数称为“`exec()` 族”。并没有一个名为 `exec()` 的函数；相反，我们使用这个名称来指代上述列出的任何一个函数。与 `fork()` 一样，“`exec`”在 Unix 术语中作为动词使用，意味着执行（运行）程序，也可以作为名词。

### 9.1.4.1 `exec()` 系统调用

最容易解释的函数是 `execve()`。它也是底层的系统调用。其他的是封装函数，稍后会解释。

```c
int execve(const char *filename, char *const argv[], char *const envp[]);
```
