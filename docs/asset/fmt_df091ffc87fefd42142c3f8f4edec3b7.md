
## 进程间通信

`mmap` 的第五个参数是一个文件句柄；在这种情况下，`ff` 的值被设置为调用共享内存设备 (`/dev/mem`) 返回的返回值。`mmap` 的第六个参数是共享内存块的物理地址；在例中，表达式 `(63*1000000)` 结果为 63 兆，这是 Linux 启动后预留的共享内存区域的起始位置（回想我们对 `/etc/lilo.conf` 的修改）。

图 17.1 显示了程序访问同一块共享内存。

![](img/66f6e6c242a0e6a79aeee4012c6ff547_283_0.png)

以下代码每两秒读写共享内存的前两个字节：

```c
for (i=0; i<10; i++) {
  printf("Test iteration %d\n", i);
  printf("first two bytes: %d\n",
    mem_pointer[0] = 2); // 写入共享内存
  mem_pointer[1] = 3; // 写入共享内存
  printf("first two bytes: %d\n",
    mem_pointer[0], mem_pointer[1]); // 从共享内存读取
  sleep(2); // 等待 2 秒
}
```

此示例使用系统调用 `sleep` 来暂停程序执行两秒，而不浪费 CPU 周期。当你完成共享内存的使用后，使用 `munmap` 函数释放该块：

```c
munmap(mem_pointer, 8192);
```

此示例（由源文件 `shared_mem.c` 构建）必须以 root 身份或具有管理员权限的账户运行。如果你在两个独立的终端窗口中运行此程序（并间隔几秒启动它们），你将看到两个程序读写两个字节共享内存的效果。共享内存是程序之间进行高效共享数据的极佳方法。然而，`shared_mem.c` 文件中的简单示例忽略了不同执行程序同时访问共享内存的问题。

## 共享内存

第 17 章

确保对共享内存进行原子读写的最佳方法是使用信号量（参见第 18 章，“信号量”），以防止多个程序在同一时间读取或写入时访问共享内存。问题是，写入共享内存的进程可能会被内核中断，另一个读取共享内存的程序可能会被执行并读取到部分写入的数据。对于某些应用程序，可能只需使用一个字节的共享内存作为标志，指示该进程正在使用共享内存。如果一个写入共享内存的进程将此标志置为非零值，并在更新（写入）共享内存之前被中断，那么运行的任何其他进程都可以检查该标志字节并发现共享内存正在使用中。然后，它可以在尝试访问共享内存之前睡眠一会儿。

## 运行共享内存程序示例

在运行 `shared_mem.c` 示例程序之前，你已经遵循了本章第一部分的共享内存配置说明。切换目录到 `IPC/SHARED` 并按照以下命令构建示例：

```bash
make
```

然后，执行 `su root` 获取 root 权限并运行 `shared_mem` 示例程序；你应该看到以下输出：

```bash
markw@Colossus:/home/markw/MyDocs/LinuxBook/src/IPC/SHARED > make
cc -o shared_mem shared_mem.c
markw@Colossus:/home/markw/MyDocs/LinuxBook/src/IPC/SHARED > su
Password:
colossus:/home/markw/MyDocs/LinuxBook/src/IPC/SHARED # ./shared_mem
Test iteration 0
first two bytes: 0 0
first two bytes: 0 0
Test iteration 1
first two bytes: 0 0
first two bytes: 2 3
Test iteration 2
first two bytes: 2 3
first two bytes: 4 6
Test iteration 3
first two bytes: 4 6
first two bytes: 6 9
Test iteration 4
first two bytes: 6 9
first two bytes: 8 12
Test iteration 5
first two bytes: 8 12
```

![](img/66f6e6c242a0e6a79aeee4012c6ff547_284_0.png)

```text
first two bytes: 10 15
Test iteration 6
first two bytes: 10 15
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
```

当你开发和运行使用共享内存的程序时，有两个非常有用的 UNIX 实用程序是你应该使用的：`ipcs` 和 `ipcrm`。`ipcs` 工具打印当前分配的共享内存、信号量和消息队列的信息。`ipcrm` 工具用于释放那些因程序崩溃或编写不当而未释放的系统资源。

### 总结

当你需要共享大量数据以获得最高性能时，使用共享内存是一项 Great 技术。然而，章中的简单示例忽略了不同执行程序同时访问共享内存的问题。确保对共享内存进行原子读写的最佳方法是使用信号量（参见第 18 章，“信号量”），以防止多个程序在同一时间读取或写入时访问共享内存。问题是，写入共享内存的进程可能会被内核中断，另一个读取共享内存的程序可能会被执行并读取到部分写入的数据。对于某些应用程序，可能只需使用一个字节的共享内存作为标志，指示该进程正在使用共享内存。如果一个写入共享内存的进程将此标志置为非零值，并在更新（写入）共享内存之前被中断，那么运行的任何其他进程都可以检查该标志字节并发现共享内存正在使用中。然后，它可以在尝试访问共享内存之前睡眠一会儿。

## 信号量

第 18 章

示例程序 `semaphore.c` 执行以下操作：

- 创建唯一密钥并创建信号量
- 确保信号量已创建
- 打印索引 0 的信号量值（应为 1）
- 设置信号量（索引 0 的值减 1）
- 打印索引 0 的信号量值（应为 0）
- 取消设置信号量（索引 0 的值加 1）
- 打印索引 0 的信号量值（应为 1）
- 信号量

设置信号量的值似乎违背直觉。如果信号量集中某个元素的计数值为零，则被认为已设置（即指示某些进程正在使用关联资源）。你通过将其值增加到 1 来释放信号量（取消设置）。

Linux 内核维护信号量数据。所有信号量使用都是通过系统调用进行的，而不是直接访问系统数据。以下代码片段创建了一个信号量：

```c
// 开始创建一个信号量：
unique_key = ftok(".", 's');
id = semget(unique_key, 1, IPC_CREAT | IPC_EXCL | 0666);
printf("semaphore id=%d\n", id);
```

## 进程间通信与网络编程

第三部分

`ftok` 函数根据目录路径和字符创建一个键值。`semget` 的第一个参数是 `ftok` 返回的唯一键。第二个参数是要创建的信号量集合中的信号量数量；本例中只需要一个信号量。第三个参数指定创建信号量，并且如果信号量已经存在则创建失败。标志位（第三个参数）与调用 `open` 文件时使用的标志位类似，区别是将 "O" 替换为 "IPC_"。

以下代码展示了如何设置信号量的一个成员：

```c
union semid options;
options.val = 1; // 指定值
semctl(id, 0, GETVAL, options); // 对索引为0的信号量进行操作

// 确保所有设置都已完成：
if (semctl(id, 0, GETVAL) == 0) {
    printf("can not lock semaphore.\n");
    exit(1);
}
```

`union semid` 定义在头文件 `sys/sem.h`（或 `sys/sem.h` 包含的另一个头文件中），其值如下：

```c
union semid {
    int val;               /* 用于 SETVAL 的值 */
    struct semid_ds *buf;  /* 用于 IPC_STAT & IPC_SET 的缓冲区 */
    ushort *array;         /* 用于 GETALL & SETALL 的数组 */
    struct seminfo *_buf;   /* 用于 IPC_INFO 的缓冲区 */
    void *pad;
};
```
