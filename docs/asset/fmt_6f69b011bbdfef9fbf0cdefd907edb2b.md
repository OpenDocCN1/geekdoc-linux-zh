
将变量 `pid` 转换为 `(long)` 会强制数据类型与格式说明符 `%ld` 匹配。

列表 18.1 中的过程使用了以下步骤：

- 1. 声明类型为 `pid_t` 的变量 `pid` 用于保存 `fork()` 调用返回的进程 ID（第 9 行）。
- 2. 调用函数 `fork()` 创建新进程（第 11 行）。返回的进程 ID 存储在变量 `pid` 中。
- 3. 执行测试检查 `fork()` 调用是否存在错误（第 13 行）。如果变量 `pid` 的值为 -1，则报告错误并退出程序（第 14 到 17 行）。
- 4. 执行测试检查进程 ID 是否为 0（第 18 行）。如果变量 `pid` 为 0，则该进程是父进程的副本。这表明你正在执行针对子进程的指令。在这种情况下，会报告子进程的消息（第 19 到 21 行）。注意你如何使用 `getpid()` 函数获取父进程的进程 ID。
- 5. 否则（第 22 行），你知道你正在原始父进程中执行，因为变量 `pid` 存储了来自 `fork()` 返回值的子 ID。显示父进程的消息（第 23 到 25 行）。
- 6. 调用 `sleep()` 函数暂停程序一秒（第 28 行），确保子进程不会因父进程匆忙退出而变成孤儿。如果父进程在子进程报告消息之前退出，子进程将报告 PID 1 为其父进程（init 进程）。

## 运行 fork() 示例

> 你的进程可以调用 `getppid()` 函数来获取父进程的进程 ID。该函数不接受参数且不会产生错误。这种能力对于 `fork()` 之后的子进程特别有用。子进程返回值为 0，因此子进程有必要调用 `getppid()` 来确定其父进程 ID。

在编译了列表 18.1 中的程序后，你应该能够运行它并获得类似下面的输出（你的进程 ID 值将是）：

```bash
bash $ ./a.out
PID 310: Started child PID 311.
PID 311: Child started, parent is 310.
bash$
```

会话可以总结如下：

- 1. 启动编译后的程序 `a.out`。
- 2. 父进程 ID 310 启动了一个子进程 ID 311。
- 3. 子进程 ID 311 启动并返回其父进程 ID 为 310。
- 4. 两个进程均退出。

在这个示例中，父进程首先报告其消息。然而，有时子进程可能会先报告消息。这种行为发生在子进程在创建后与其父进程竞争 CPU 资源时。

## 运行示例

如果你获取列表 18.1 中的程序并对其添加一个 `system()` 调用，你就可以更图形化地显示这些关系。查看列表 18.2。

### 列表 18.2 18ST02.c—修改后的示例

```c
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <errno.h>
#include <sys/types.h>
#include <stdlib.h>
int main(int argc,char **argv) {
    pid_t pid;               /* 子进程进程 ID */
    pid = fork();            /* 创建一个新的子进程 */
    if (pid == -1) {
      fprintf(stderr,
               "%s: Failed to fork()\n",
               strerror(errno));
      exit(13);
    } else if (pid == 0 ) {
      printf("PID %ld: Child started, parent is %ld.\n",
               (long)getpid(),    /* 我们的 PID */
               (long)getppid());  /* 父进程 PID */
    } else {
      printf("PID %ld: Started child PID %ld.\n",
               (long)getpid(),    /* 我们的 PID */
               (long)pid);         /* 子进程的 PID */
    }
    sleep(1);               /* 稍留一下 */
    system("ps");
}
```

## 分叉进程

列表 18.1 中的过程使用了以下步骤：

- 1. 声明类型为 `pid_t` 的变量 `pid` 用于保存 `fork()` 调用返回的进程 ID（第 9 行）。
- 2. 调用函数 `fork()` 创建新进程（第 11 行）。返回的进程 ID 存储在变量 `pid` 中。
- 3. 执行测试检查 `fork()` 调用是否存在错误（第 13 行）。如果变量 `pid` 的值为 -1，则报告错误并退出程序（第 14 到 17 行）。
- 4. 执行测试检查进程 ID 是否为 0（第 18 行）。如果变量 `pid` 为 0，则该进程是父进程的副本。这表明你正在执行针对子进程的指令。在这种情况下，会报告子进程的消息（第 19 到 21 行）。注意你如何使用 `getpid()` 函数获取父进程的进程 ID。
- 5. 否则（第 22 行），你知道你正在原始父进程中执行，因为变量 `pid` 存储了来自 `fork()` 返回值的子 ID。显示父进程的消息（第 23 到 25 行）。
- 6. 调用 `sleep()` 函数暂停程序一秒（第 28 行），确保子进程不会因父进程匆忙退出而变成孤儿。如果父进程在子进程报告消息之前退出，子进程将报告 PID 1 为其父进程（init 进程）。

## 运行 fork() 示例

在编译了列表 18.1 中的程序后，你应该能够运行它并获得类似下面的输出（你的进程 ID 值将是）：

```bash
bash $ ./a.out
PID 310: Started child PID 311.
PID 311: Child started, parent is 310.
bash$
```

会话可以总结如下：

- 1. 启动编译后的程序 `a.out`。
- 2. 父进程 ID 310 启动了一个子进程 ID 311。
- 3. 子进程 ID 311 启动并返回其父进程 ID 为 310。
- 4. 两个进程均退出。

在这个示例中，父进程首先报告其消息。然而，有时子进程可能会先报告消息。这种行为发生在子进程在创建后与其父进程竞争 CPU 资源时。

## 运行示例

如果你获取列表 18.1 中的程序并对其添加一个 `system()` 调用，你就可以更图形化地显示这些关系。查看列表 18.2。

### 列表 18.2 18ST02.c—修改后的示例

```c
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <errno.h>
#include <sys/types.h>
#include <stdlib.h>
int main(int argc,char **argv) {
    pid_t pid;               /* 子进程进程 ID */
    pid = fork();            /* 创建一个新的子进程 */
    if (pid == -1) {
      fprintf(stderr,
               "%s: Failed to fork()\n",
               strerror(errno));
      exit(13);
    } else if (pid == 0 ) {
      printf("PID %ld: Child started, parent is %ld.\n",
               (long)getpid(),    /* 我们的 PID */
               (long)getppid());  /* 父进程 PID */
    } else {
      printf("PID %ld: Started child PID %ld.\n",
               (long)getpid(),    /* 我们的 PID */
               (long)pid);         /* 子进程的 PID */
    }
    sleep(1);               /* 稍留一下 */
    system("ps");
}
```

## 分叉进程

列表 18.1 中的过程使用了以下步骤：

- 1. 声明类型为 `pid_t` 的变量 `pid` 用于保存 `fork()` 调用返回的进程 ID（第 9 行）。
- 2. 调用函数 `fork()` 创建新进程（第 11 行）。返回的进程 ID 存储在变量 `pid` 中。
- 3. 执行测试检查 `fork()` 调用是否存在错误（第 13 行）。如果变量 `pid` 的值为 -1，则报告错误并退出程序（第 14 到 17 行）。
- 4. 执行测试检查进程 ID 是否为 0（第 18 行）。如果变量 `pid` 为 0，则该进程是父进程的副本。这表明你正在执行针对子进程的指令。在这种情况下，会报告子进程的消息（第 19 到 21 行）。注意你如何使用 `getpid()` 函数获取父进程的进程 ID。
- 5. 否则（第 22 行），你知道你正在原始父进程中执行，因为变量 `pid` 存储了来自 `fork()` 返回值的子 ID。显示父进程的消息（第 23 到 25 行）。
- 6. 调用 `sleep()` 函数暂停程序一秒（第 28 行），确保子进程不会因父进程匆忙退出而变成孤儿。如果父进程在子进程报告消息之前退出，子进程将报告 PID 1 为其父进程（init 进程）。

## wait() 系列函数

`wait()` 系列允许父进程查询其子进程。这些函数对 Linux 内核来说同样重要，因为它们允许内核知道退出状态何时不再需要。当子进程终止时，退出状态会保存在该进程的进程表中，尽管大部分资源已释放。该进程表目通过其进程 ID 标识，进程的终止状态存储在进程表目中。

## 理解 wait() 的重要性

`wait()` 系列允许父进程查询其子进程。这些函数对 Linux 内核来说同样重要，因为它们允许内核知道退出状态何时不再需要。

## 理解僵尸进程

僵尸进程是由于某种原因已终止，但其父进程继续执行而不查询其命运的子进程。`wait()` 函数由父进程调用，允许内核从系统中移除这些僵尸进程。

在父进程获取这些信息之前，该表条目必须留在 Linux 内核中。处于这种状态的进程被称为僵尸进程（zombie）。以下示例会话，其中子进程已经退出，但父进程尚未查询其终止状态：

| PID | TTY | STAT | TIME | COMMAND |
| :--- | :--- | :--- | :--- | :--- |
| 722 | a | S | 0:03 | -bash |
| 379 | a | S | 0:00 | ./a.out |
| 380 | a | Z | 0:00 | (a.out <zombie>) |
| 381 | a | R | 0:00 | ps f |

此 `ps` 命令显示 PID 为 380 的子进程已退出，且 `ps` 命令将其标记为僵尸进程。然而，父进程（PID 379）仍在运行。因此你知道它尚未查询其子进程。出于这个原因，Linux 内核保留了进程表，以便 PID 380 的进程终止状态不会丢失。

## 使用 wait() 函数

父进程可以使用 `wait()` 函数查询其子进程。该函数的原型定义如下：

```c
#include <sys/types.h>
#include <sys/wait.h>
```

```c
pid_t wait(int *status)
```

该函数接受一个参数，该参数必须指向整数数据类型的指针，用于接收返回的状态信息。函数的返回值数据类型为 `pid_t`。该返回值指示哪个进程被该调用回收（reaped）（某些父进程可能有多个待处理的进程）。

列表 18.3 显示的程序与列表 18.1 中的原始程序相似。然而，在这个程序中，`sleep()` 调用被 `wait()` 调用所取代了。

## 18.3 18BLST03.c—使用 wait() 函数的示例

```c
1:   #include <stdio.h>
2:   #include <unistd.h>
3:   #include <string.h>
4:   #include <errno.h>
5:   #include <sys/types.h>
6:   #include <sys/wait.h>
7:   int
8:   int
```

### 列表 18.3 续

```c
9:  main(int argc, char **argv) {
10:     pid_t pid;                /* 子进程的进程 ID */
11:     pid_t wpid;               /* wait() 返回的进程 ID */
12:     int status;               /* wait() 返回的退出状态 */
13:
14:     pid = fork();             /* 创建一个新的子进程 */
15:
16:     if (pid == -1) {
17:         fprintf(stderr,
18:             "%s: Failed to fork()\n",
19:             strerror(errno));
20:         exit(13);
21:     } else if (pid == 0) {
22:         printf("PID %ld: Child started, parent is %ld.\n",
23:             (long)getpid(),           /* 我们的 PID */
24:             (long)getppid());         /* 父进程 PID */
25:     } else {
26:         printf("PID %ld: Started child PID %ld.\n",
27:             (long)getpid(),           /* 我们的 PID */
28:             (long)pid);
29:         wpid = wait(&status);      /* 子进程的退出状态 */
30:         if (wpid == -1) {
31:             fprintf(stderr, "%s: wait()\n",
32:                 strerror(errno));
33:             return 1;
34:         } else if (wpid == pid) {
35:             abort(1);                /* 在此程序中不应发生 */
36:         } else {
37:             printf("Child PID %ld exited status 0x%04X\n",
38:                 (long)pid,               /* 子进程 PID */
39:                 status);                /* 退出状态 */
40:         }
41: }
42:     return 0;
43: }
```

为了得到列表 18.3 中的程序，对列表 18.1 了以下更改：

- 1. 声明了类型为 `pid_t` 的变量 `wpid`（第 11 行）。
- 2. 声明了一个变量 `status` 来接收子进程退出状态（第 12 行）。
- 3. 删除了 `sleep(1)`。父进程和子进程都没有调用 `sleep()`。
- 4. 父进程调用了函数 `wait()`（第 29 行）。返回值放在 `wpid` 中。子进程的状态由 `wait()` 调用存储在变量 `status` 中。
- 5. 执行了测试以检查 `wpid == -1` 的值。这表示函数执行失败（第 30 行）。如果发生错误，则报告错误（第 31 行到 33 行）。

## 分叉进程

- 6. 执行了测试以检查 `wpid` 是否匹配变量 `pid`（第 34 行）。在此程序中它们永远不应该一致，因此如果不一致，你编写了对 `abort()` 调用。
- 7. 报告了退出状态。由于该值包含子字段，退出状态以十六进制形式报告（第 37 行到 39 行）。

如果你编译并从 shell 调用列表 18.3 中的程序，你应该得到：

```bash
bash$../a.out
PID 421: Started child PID 422.
PID 422: Child started, parent is 421.
Child PID 422 exited status 0x0000
bash$
```
