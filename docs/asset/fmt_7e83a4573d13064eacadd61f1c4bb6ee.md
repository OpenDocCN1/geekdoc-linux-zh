
# 第 7 章 进程间的通信

修复后的时序如图 7-3 所示。我将详细查看 POSIX API，但这个示例对于信号量来说是最简单了。

![](img/9c04dc9e840dfb086a38289961386a14_432_0.png)

图 7-3 列表 7-13 时序：信号充当交通警察

## 7.8 信号量

### 7.8.1 使用 POSIX API 的信号量

你在列表 7-13 中看到了父子进程之间信号量的示例。POSIX 信号量的名称在整个系统中是可见的。信号量从创建开始一直存在到它被删除或系统重启为止，如列表 7-14 中的程序所示。

#### 列表 7-14 posix_sem.c：简单的 POSIX 程序

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <assert.h>
#include <errno.h>
#include <unistd.h>
#include <sys/file.h>
#include <sys/stat.h>
#include <semaphore.h>

int main(int argc, char *argv[]) {
    const char *semname = "/mysem";

    // 创建信号量，并将计数初始化为 0。
    // 因为我们使用了 O_EXCL，如果信号量
    // 存在（EEXIST），将失败。
    sem_t *sem = sem_open(semname, O_CREAT | O_EXCL, 0664, 0);

    if (sem != SEM_FAILED) {
        printf("创建新信号量\n");
    }
    else if (errno == EEXIST) {
        // 信号量存在，因此不带 O_EXCL 打开
        printf("信号量存在\n");
        sem = sem_open(semname, 0);
    }

    assert(sem != SEM_FAILED);
    int op = 0;
    // 用户参数：零、正或负
    if (argc > 1) {
        op = atoi(argv[1]);
    }

    if (op > 0) {
        printf("正在增加信号量\n");
        sem_post(sem);
    }
    else if (op < 0) {
        printf("正在减信号信号量\n");
        sem_wait(sem);
    }
    else {
        printf("未修改信号量\n");
    }
    int val;
    sem_getvalue(sem, &val);
    printf("信号量值为 %d\n", val);
    return 0;
}
```

当程序第一次运行时，它会使用 `sem_open` 函数创建信号量。`sem_open` 的前三个参数与 `open(2)` 系统调用相同。第四个参数仅在创建信号量时使用，它包含信号量的计数。其原型如下：

```c
sem_t *sem_open(const char *name, int oflag, ...);
```

我使用了 `O_EXCL` 标志来强制在信号量存在时让 `sem_open` 失败。这并不是必要的，我本可以不写它。设置该标志的作用是为了让你在创建信号量时可以打印出不同的消息。

该程序根据用户参数执行单个信号量操作。用户可以使用正整数作为参数来增加信号量，或者使用负数来减小信号量。例如：

```bash
$ cc -o posix_sem posix_sem.c -lrt
$ ./posix_sem 1
创建新信号量
正在增加信号量
信号量值为 1
```

> 创建并增加信号量。

```bash
$ ./posix_sem 1
信号量存在
正在增加信号量
信号量值为 2
```

> 增加信号量。
> 信号量的值反映了 `sem_post` 调用的次数。

```bash
$ ./posix_sem -1
信号量存在
正在减信号量
信号量值为 1
```

> 现在是减法。

```bash
$ ./posix_sem 0
信号量存在
未修改信号量
信号量值为 1
```

> 无操作
> Value = 2 * x_sem_post - 1 * x_sem_wait

```bash
$ ./posix_sem -1
信号量存在
正在减信号量
信号量值为 0
```

> 信号量阻塞了！

列表 7-14 使用了命名信号量。在这个示例中，我疏忽了没有调用 `sem_close`，正如你所预期的那样，这会释放信号量消耗的用户空间资源。同样，还有一个 `sem_unlink` 函数，它可以从系统中移除信号量并释放该信号量所消耗的所有资源。

POSIX API 还允许使用无名信号量，但要注意：Linux 中的无名信号量仅在线程间有效。无名信号量的定义没有使用需要名称的 `sem_open`。相反，应用程序调用的是 `sem_init`，其原型如下：

```c
int sem_init(sem_t *sem, int pshared, int value);
```

POSIX 规定非零的 `pshared` 参数表示该信号量可以在进程之间共享。Linux 并没有实现这一点，这意味着无名信号量只能在进程内的线程之间使用。一种初始化无名信号量的模式如下所示：

```c
sem_t mysem;
int r = sem_init(&sem, 0, 0);
...
sem_destroy(&sem);
```

用户定义的存储
初始化为零 `pshared=0`
用于回收存储。

请注意，在回收存储之前需要调用 `sem_destroy`；否则可能会导致内存损坏。如果你使用无名信号量，最安全的办法是为应用程序的生命周期为它们分配内存，而不是将它们放在栈或堆上。

### 7.8.2 使用 System V API 的信号量

System V 信号量 API 与用于共享内存和消息队列的 API 一致——即应用程序定义键（key），系统在信号量创建时分配一个标识（ID）。列表 7-14 的等效示例显示在列表 7-15 中。

#### 列表 7-15 sysv_sem.c：使用 System V 信号量

```c
1 #include <stdio.h>
2 #include <string.h>
3 #include <stdlib.h>
4 #include <assert.h>
5 #include <errno.h>
6 #include <unistd.h>
7 #include <sys/stat.h>
8 #include <sys/sem.h>
9
10 int main(int argc, char *argv[])
11 {
12     // 使用 ftok 创建一个键
13     key_t semkey = ftok("/tmp", "a");
14
15     // 创建信号量 - 一个长度为 1 的“数组”。
16     // 由于我们 IPC_EXCL，如果信号量
17     // 存在，这将失败。
18     int semid = semget(semkey, 1, IPC_CREAT | IPC_EXCL, S_IRUSR | S_IWUSR);
19
20     if (semid != -1) {
21         printf("创建新信号量\n");
22     } else if (errno == EEXIST) {
23         // 信号量存在，因此不带 O_EXCL 打开
24         printf("信号量存在\n");
25         semid = semget(semkey, 0);
26     }
27
28     assert(semid != -1);
29     int op = 0;
30     // 用户参数：零、正或负
31     if (argc > 1) {
32         op = atoi(argv[1]);
33     }
34
35     if (op > 0) {
36         printf("正在增加信号量\n");
37         // 准备操作结构体
38         struct sem_buf sb = {0, 1, 0}; // 增加信号量
39         semop(semid, &sb, 1);
40     } else if (op < 0) {
41         printf("正在减信号量\n");
42         struct sem_buf sb = {0, -1, 0}; // 减少信号量
43         semop(semid, &sb, 1);
44     } else {
45         printf("未修改信号量\n");
46     }
47     int val;
```
