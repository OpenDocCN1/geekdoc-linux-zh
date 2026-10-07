
### 答案

输出语句虽然是由服务器执行的，但实际上位于客户端的计时循环中。服务器侧的打印语句增加了在共享设备上隐式同步线程的问题。

另一个可能影响计时的低效因素是在工作线程中使用了不必要的 `select` 语句。除非你控制超时，否则你不需要在请求-响应情况下使用 `select`。

## 练习 22.23

以下写入大小为 `BLKSIZE` 的块后紧接着读取相同大小的块的代码段存在什么问题？

```
if (r_write(commfund, buf, BLKSIZE) < 0)
    perror("Failed to write");
else if (r_read(commfund, buf, BLKSIZE) < 0)
    perror("Failed to read");
```

答案：

`r_read` 函数在循环中调用 `write` 直到整个 `BLKSIZE` 缓冲区被写入。`r_read` 函数只执行一次顺序读取，因此整个 `BLKSIZE` 响应可能没有被读取。因此，使用单个 `r_read` 调用的客户端驱动程序可能无法正确计时该请求-响应，特别是对于广域网上的大数据包。糟糕的是，当下一个客户端对连接进行请求-响应计时时，它将读取上一个请求的响应。

## 22.11.4 同步

“每个请求一个线程”的服务器不需要显式同步，因此从理论上讲，同步对于该服务器不是问题。然而，每当线程共享公共资源（如屏幕）时，每个请求一个线程可能会发生隐式同步。避免在服务器事件中使用打印语句进行调试或警告严重错误状况。调试语句应始终包含在条件编译子句中。

## 示例 22.24

以下语句在程序中被编译是因为定义了 `DEBUG`。

```
#define DEBUG 1
#ifdef DEBUG
    printf(stderr, "Sending the message...\n");
#endif
```

要消除 `printf`，请注释掉或完全删除它。

工作池的同步问题更为复杂。工作池的三种常见实现具有不同的同步特征。在最直接的实现中，每个工作线程阻塞在 `accept` 上。这种机制依赖于库提供的安全的 `accept`。POSIX 规定 `accept` 应该是线程安全的，但并不是所有的操作系统实现都提供可靠的线程安全。另一种工作池实现使用互斥锁保护 `accept`，如示例 22.25 所示。

## 示例 22.25

在以下工作池实现的伪代码中，互斥锁有效地形成了一个屏障，允许一次只有一个线程通过。

```
loop
    mutex lock (if error, output message to log, exit)
    accept (if error, release lock and continue)
    mutex unlock (if error, output message to log, exit)
    process request (if error, output message to log, continue)
```

示例 22.25 的伪代码指示了发生错误时的处理。一个常见问题发生在 `accept` 后没有正确释放锁。在这种情况下，系统会死锁，因为没有其他工作线程可以获取互斥锁。

工作池的缓冲区实现容易出现其他性能瓶颈，如果主生产者在将项目放入缓冲区时执行 `pthread_cond_broadcast` 而不是 `pthread_cond_signal`，所有等待的线程将被唤醒并竞争控制线程的互斥锁。这种实现给服务器带来了巨大的负载，即使工作线程数量适中。生产者应该避免在槽位上广播，消费者应该避免在项目上广播。

## 22.11.5 纯错误

你不能依赖运行不正确的程序的计时结果。捕获所有库函数的返回值（包括线程调用）是非常重要的。使用 `lint` 工具对源代码进行处理并注意输出。特别是，不要忽略隐式假设返回 `int` 的信息，这表明你缺少了头文件。

由于线程在父进程环境中执行，线程服务器容易出现子进程不会出现的内存泄漏。如果线程在调用 `pthread_exit` 时没有释放缓冲区或关闭其通信文件描述符，服务器在其剩余的生命周期内将承担这些遗留。

## 练习 22.26

以下代码中可能存在内存泄漏？

```
loop
    malloc space for communfd
      if malloc fails
        quit
    accept a client connection
```

```
if accept fails
continue
create a thread to handle the communication
if the thread create fails,
continue
```

答：

如果 `accept` 失败，通信文件描述符的空间就会泄漏。如果线程创建失败，服务器也会遗留一个打开的文件描述符以及分配的内存。

## 练习 22.27

在转换 `communfd` 时，以下代码 `string` 了什么假设？

```
int communfd
if ((communfd = u_accept(listenfd, client, MAX_CANON)) == -1)
return -1;
if (pthread_create(&tid, null, process_request, (void *)communfd))
return -1;
```
