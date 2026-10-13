
first two bytes: 12 18

Test iteration 7

first two bytes: 12 18

first two bytes: 14 21

Test iteration 8

first two bytes: 14 21

first two bytes: 16 24

Test iteration 9

first two bytes: 16 24

first two bytes: 18 27

在用共享内存开发和运行程序时，有两个非常实用的 UNIX 工具程序是你应该使用的：`ipcs` 和 `ipcrm`。`ipcs` 工具可以打印当前分配的共享内存、信号量和消息队列的信息。`ipcrm` 工具用于释放由于程序崩溃或编写不当而未释放的系统资源。

### 总结

当你需要对大量数据进行快速性能时，使用共享内存是一项棒的技术。本章的示例忽略了多处理器计算机上两个或多个程序同时写入共享内存引起的问题。在下一章节中，你将看到如何使用信号量来协调对共享资源的访问。

## 信号量

*作者：Mark Watson*

本章内容

- 使用信号量的示例程序 288
- 运行信号量示例程序 293

### 进程间通信与网络编程
第三部分

信号量是用于协调独立进程之间动作的数据对象。信号量经常用于共享一次时间只能被一个进程使用的资源。在第 17 章“共享内存”中，你看到了两个进程之间使用共享内存的简单示例；在这个共享内存示例中，忽略了两个进程同时访问同一块共享内存的问题。你可以通过使用信号量协调对共享内存和其他系统资源的访问，从而避免这些潜在问题。

Linux 内核操作系统需要维护信号量的状态，而不是用户进程。如果你在系统中安装了 Linux 内核源码，可以检查 `sem.h` 文件以查看内核用于维护信号量状态信息的 `sem_id` 数据结构的定义。信号量是相对的数据集合；你可以单独使用集合中的每个元素。在本章中，我们使用以下三个调用来创建、使用和释放信号量：

- `semget`—返回一个由内核分配的整数信号量索引
- `semop`—对信号量集执行操作
- `semctl`—对信号量集执行控制操作

使用信号量相当简单，正如你在下一节的示例程序中所看到的。然而，尽管使用信号量的技术很简单，但有两个问题需要注意：死锁和释放释放。如果有多个受信号量控制访问的资源，可能会发生死锁。例如，如果两个进程需要访问两个不可共享的资源，一个进程可能会获取一个资源的信号量锁并等待另一个资源，因为另一个进程锁定了第二个资源并正在等待第一个资源。在使用信号量时，在终止程序之前释放信号量是非常重要的。

### 使用信号量的示例程序

示例程序 `semaphore.c` 执行了以下操作：

- 创建一个唯一键并创建一个信号量
- 检查并确保信号量创建成功
- 打印索引为 0 的信号量值（应为 1）
- 设置信号量（将索引 0 的信号量值减至 0）
- 打印索引为 0 的信号量值（应为 0）
- 取消信号量（将索引 0 的信号量值加回 1）
- 打印索引为 0 的信号量值（应为 1）
- 信号量

设置信号量的值似乎是违反直觉的。如果计数值为零，则认为信号量集中的元素被已设置（即表示某些进程正在使用关联资源）。你通过将其值增加到 1 来释放信号量（取消设置）。

图 18.1 显示了示例程序与 Linux 内核及内部数据的关系。应用程序无法直接访问用于维护信号量集的数据；相反，应用程序使用 `semget`、`semop` 和 `semctl` 调用来创建和使用信号量集。

### 图 18.1

Linux 内核负责维护信号量集的数据。

使用信号量集协调系统资源的访问

![](img/681a495129beb6adf91e7ff7f87e7dd4_305_0.png)

Linux 内核维护信号量数据。所有信号量的使用都是通过系统调用实现的，而不是直接访问系统数据。

以下代码片段创建一个信号量：

```c
// 从创建一个信号量开始：
unique_key = ftok(".", 's');
id = semget(unique_key, 1, IPC_CREAT | IPC_EXCL | 0666);
printf("semaphore id=%d\n", id);
```

`ftok` 函数根据目录路径和种子字符创建一个键值。`semget` 的第一个参数是 `ftok` 返回的唯一键。第二个参数是要创建的集合中信号量的数量；这只需要一个信号量。

### 列表 18.1 信号量示例程序

```c
/* semaphore.c
 * Copyright Mark Watson, 1988. Open Source Software License
 * */
```

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/sem.h>
#include <sys/ipc.h>
#if defined(__GNU_LIBRARY__) && defined(_SEM_SEMUN_UNDEFINED)
 * union semid 由 <sys/sem.h> 中定义 */
#else
 * 根据 X/OPEN 标准，我们必须自己定义 */
union semun {
    int val;               /* 用于 SETVAL 的值 */
    struct semid_ds *      /* 用于 IPC_STAT, IPC_SET 的缓冲区 */
    unsigned short int *array; /* 用于 GETALL, SETALL 的数组 */
    struct seminfo *buf;    /* 用于 IPC_INFO 的缓冲区 */
};
#endif
void main(){
  key_t unique_key;
  int id;
  struct sembuf lock;
  union semun options;
  int i;
  // 从创建一个信号量开始：
  unique_key = ftok("".*", 'a');
  // /* 'a' 可以是任何字符
  // 创建一个包含 1 个成员的新信号量集；注意
  // 如果你想使用另一个程序创建的信号量，
  // 请在第二个参数中使用 0 而不是 1；
  id = semget(unique_key, 1, IPC_CREATE | IPC_EXCL | 0666);
  printf("semaphore-%d\n", id);
  options.val = 1;
  semctl(id, 0, SETVAL, options);
  // 确保一切设置都正常：
  if (semctl(id, 0, GETVAL, 0) == 0) {
    printf("can not lock semaphore.\n");
    exit(1);
  }
  // 现在打印信号量的值：
  i = semctl(id, 0, GETVAL, 0);
  printf("value of semaphore at index 0 is %d\n", i);
```

```c
// 现在设置信号量：
lock.sem_num = 0; // 信号量索引
lock.sem_op = -1; // 操作
lock.sem_flg = IPC_NOWAIT; // 操作标志
if (semop(id, &lock, 1) == -1) {
    printf("can not lock semaphore.\n");
    exit(1);
}
```

```c
// 现在打印信号量的值：
i = semctl(id, 0, GETVAL, 0);
printf("value of semaphore at index %0 is %d\n", i);
```

```c
// 现在取消信号量设置：
lock.sem_num = 0;
lock.sem_op = 1;
lock.sem_flg = IPC_NOWAIT;
if (semop(id, &lock, 1) == -1) {
    printf("could not unlock semaphore.\n");
    exit(1);
}
```

```c
// 现在打印信号量的值：
i = semctl(id, 0, GETVAL, 0);
printf("value of semaphore at index %0 is %d\n", i);
```

```c
// 现在移除信号量：
semctl(id, 0, IPC_RMID, 0);
```
