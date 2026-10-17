
我们的信号量结构包含两个描述符，一个用于读取，一个用于写入。为了相似性，我们将两个描述符都存储在一个两个元素的数组中，第一个描述符用于读取，第二个用于写入。`sem_magic`成员一旦该结构初始化，将包含`SEM_MAGIC`。每个函数都会检查这个值。

### sem_t 类型

我们的信号量结构包含两个描述符，一个用于读取，一个用于写入。为了相似性，我们将两个描述符都存储在一个两个元素的数组中，第一个描述符用于读取，第二个用于写入。`sem_magic`成员一旦该结构初始化，将包含`SEM_MAGIC`。每个函数都会检查这个值。

### sem_open 函数

描述，“父进程中打开的任何信号量在子进程中也应该是打开的”。这意味着以下代码是可以允许的：

```c
sem_t *mutex; /* 跨 fork 拷贝的全局指针 */
/* 父进程创建命名信号量 */
mutex = sem_open(Fk_ipc_name(NAME), O_CREATE | O_EXCL, FILE_MODE, 0);

if ((childpid = fork()) == 0) {
    /* 子进程 */
    sem_wait(mutex);
    ...
}
/* 父进程 post */
sem_post(mutex);
```

我们之所以必须小心处理何时可以和不能在不同进程间共享信号量，是因为信号量的状态可能包含在`sem_t`类型本身中，但也可能使用其他信息（例如文件描述符）。我们将在下一章看到，进程描述 System V 信号量的唯一句是`semget`返回的整数标识符。任何知道该标识符的进程都可以访问信号量。System V 信号量的所有状态信息都包含内核，整数标识符仅告诉内核引用的是哪一个信号量。

## 10.13 信号量限制

Posix 定义了两个信号量常量：

- `SEM_NS_MAX`：进程可以同时打开的信号量最大数（Posix 要求至少为 256），
- `SEM_VALUE_MAX`：信号量的最大值（Posix 要求至少为 32767）。

这两个常量通常在`<unistd.h>`中定义，也可以像我们接下来所示的，通过调用`semysconf`函数在运行时获取。

示例：`semysconf`程序

图 10.35 中的程序调用了`semysconf`并打印了信号量的两个由实现定义的限制。

```c
1 include "unipc.h"
2 int
3 main(int argc, char *argv) {
4 printf("SEM_NS_MAX = %d, SEM_VALUE_MAX = %d\n",
5 semysconf(_SC_NS_MAX), semysconf(_SC_VALUE_MAX));
6 exit(0);
7 }
```

> `pxsem/semysconf.c`

如果我们执行这个程序，将得到`semysconf`输出：

```
alpha % semysconf
SEM_NS_MAX = 2147483647, SEM_VALUE_MAX = 2147483647
SEM_NS_MAX = 256, SEM_VALUE_MAX = 32767
```

## 10.14 使用 FIFO 的实现

我们现在提供一种使用 FIFO 的 Posix 命名信号量实现。每个命名信号量都实现为相同名称的 FIFO。FIFO 中的非负字节数是信号量的当前值。`sem_post`函数向 FIFO 写入 1 字节。

本节和本章的其余部分包含一些你可能在第一次阅读时想要跳过的高级主题。我们首先在图 10.36 中展示我们的`semaphore.h`，它定义了基本的`sem_t`类型。

```c
1 /* 基础类型 */
2 typedef struct {
3     int fds[2];      /* 两个 fd：一个用于读，一个用于写 */
4     int sem_magic;   /* 打开时的魔数 */
5 } sem_t;
```
