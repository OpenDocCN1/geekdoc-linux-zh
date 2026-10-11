

```c
while(connect(sock2, (struct sockaddr *)&addr1,
                sizeof(addr1))) {
    int err;

    err = Errno;
    if(err != ECONNREFUSED) {
        printf("connect FAILED: err=%d\n", Errno);
        exit(1);
    }
    SLEEP(2); // Be polite
    *per_client_refusecnt++;
    if(refusedcount++ >= econnrefuseretries) {
        printf("connect FAILED: ");
        printf("after %d ECONNREFUSED attempts\n",
                econnrefuseretries);
        exit(1);
    }
}
    return sock2;
}
```

这两段代码值得详细讨论。`listen_and_accept()` 例程的设计旨在尽可能简单地使用；它要么返回一个可用的套接字，要么打印错误信息并退出。`clientconnect()` 例程要么返回一个可用的套接字，要么打印错误信息并退出。它处理 ECONNREFUSED 错误返回，以应对因过于繁忙而无法接受套接字请求的服务器。这种情况会发生在任何 `listen` 和 `accept` 循环中，当操作系统中的请求队列长度超过默认值 5 时。例如，如果服务器发出 `listen_and_accept()`，接收到一个传入套接字，然后简单地进入睡眠状态，后续的传入请求将由操作系统排队，直到有五个这样的请求为止。第六个连接请求将被拒绝，并由发出连接请求的客户端（在我们的情况下是 `clientconnect()`）报告 ECONNREFUSED 错误。我们的代码只是睡眠 2 秒并重试。我们默认允许四次重试。可以通过编辑程序并重新编译来更改此数值。或者，添加一个新选项以便在命令行中设置该值将非常简单。

我们描述了创建套接字连接所需的操作。套接字连接的细节很少是性能问题的根源。有趣的事情发生在套接字创建之后。

## 线程

由于我们的程序使用线程并展示了线程池，我们必须描述线程的工作方式以及我们对它们的使用。我们并不声称以下任何代码都是性能最优的代码。我们声称这些代码演示了线程如何以池化和非池化的方式使用，并且代码质量相当不错。无疑，还有改进的空间。

回想之前我们对服务器 *main* 程序的描述，其中创建了一个调度器和一个清理线程，我们将展示这两个模块。还有一个我们尚未提到的第三个模块。它是监听新工作并将其排队的线程。工作是新创建的套接字，被排队的是该套接字。我们的工作线程从套接字中读取包含文件大小和块大小的文本字符串，用于执行工作。针对此代码的其他实验几乎可以用任何目的的线程替换我们的工作线程。总之，以下内容发生：

1. 监听器监听新连接并将工作（新创建的套接字）插入工作队列。
2. 线程调度器等待队列中的工作，并启动一个线程，将套接字文件描述符传递给该线程。调度器可以使用 *池化* 线程运行，或者以每个工作项创建新线程的模式运行（-*pooling* 命令行选项）。
3. 工作线程完成所有工作，最后关闭套接字。
4. 线程清理等待线程终止并清理善后工作。

工作线程周围是向客户端报告任务完成情况的设施。

线程监听器的代码如下所示：

```c
void ServerMain()
{
    SOCKTYPE sock;

    initq(&workq);
    newThread( (void(*)(void *)) threadScheduler,0, &schedulerT);
    newThread( (void(*)(void *)) threadCleanup,0, &cleanupT);
    newThread( (void(*)(void *)) threadDbg, 0, &dbgT);

    // Server waits in a listen/accept sequence and hands off
    // request to a thread. Threads are either dynamically
    // created or there is a pool.
    //
    // listen_and_accept creates sockets
    //
    for(;;) {
        listen_and_accept(&sock);
        enqueue(&workq, sock);
        vsema(&workq.sema);
    }
}
```

线程调度器从队列中读取信息。队列由同步原语保护，我们在本章稍后部分讨论了这些原语。这些保护机制允许多个线程更新队列而不会使队列元数据变得不一致。线程调度器的代码如下所示：

```c
void threadScheduler()
{
  SOCKTYPE sock;
  int rc;

  //
  // threadScheduler decrements availableThreads,
  // threadCleanup  increments availableThreads.
  //
  for(;;) {

    schedulerstate = 1;
    psema(&workq.sema);

    schedulerstate = 2;
    psema(&availableThreads);

    schedulerstate = 3;
    if (dequeue(&workq, (int *)&sock)) {
      schedulerstate = 4;
      rc = threadStart(sock); // starting a thread
      if (rc == -1) {
        printf("threadStart FAILED: maxthreads=%d\n",
               maxthreads); fflush(stdout);
        exit(1);
      }
    }
    else {
      printf("Workq Sema count wrong\n");
      exit(1);
    }
  }
}
```

线程清理的代码如下所示：

```c
void threadCleanup()
{
  int j = 0;

  //
  // For pooled threads, this loop will last forever.
  //
  for(;;) {
    cleanupstate = 1;
    psema(&ActiveT);
    cleanupstate = 2;

    for(j = 0; j < maxthreads; j++) {
      if(threads[j].exists) {
        threadWait(&threads[j].thrd);
        threads[j].exists = 0;
        threads[j].active = 0;
        nexists--;
        vsema(&availableThreads);
      }
    }
  }
}
```

这三个模块需要一些背景讨论。监听器模块简单地接受新套接字并将其排队。它很简单，唯一需要考虑的是它必须一致地排队工作；因此，它使用 enqueue() 例程。线程调度器必须创建线程或分配现有的（池化）线程。线程通过 pthread_create() 调用创建。由于我们的程序希望启动一个已经创建（池化线程）或新建的线程，我们选择使用 threadStart() 例程抽象线程启动过程。threadStart() 使用池化全局变量来确定是使用池化线程还是简单地启动新线程。池化全局变量默认不池化，并且是一个命令行选项。

命令行告诉服务器和客户端使用多少个线程。默认值是 1。服务器一次运行的线程数不超过命令行指定的线程数。客户端以相同的方式工作。每个服务器线程执行其工作并结束。池化线程通过将自己标记为非活动并在锁上阻塞来结束。非池化线程简单地返回，从而销毁线程。对于非池化线程，如果系统要防止耗尽资源，清理例程是必不可少的。清理例程将非池化线程使用的资源返回给系统。

我们对线程代码再加一点观察。使用池化线程调度工作的线程代码编写并非易事。确定问题原因可能非常耗时。我们在下面演示一种简化调试任务的方法。我们的线程管理例程（调度和清理）每个都有一个全局状态变量。状态变量表示例程的当前状态，并且可以从程序中的所有线程访问。在任何可能阻塞的函数调用之前，这些变量会发生变化。通过打印这两个状态变量，我们可以准确确定调度和清理线程当前在代码中何处被阻塞。我们编写了一个简单的调试线程，可以打印这些状态变量的值，与状态变量一起，调试任务显著加速。

## 同步

调度器使用同步原语（信号量）在无事可做时进行阻塞。信号量用作同步计数机制，如果有待办事项，待办事项的数量反映在信号量的值中。如果计数大于零，psema() 例程将计数减一并返回给调用程序。如果信号量的值为零，psema() 例程阻塞。vsema() 操作增加信号量且从不阻塞。我们的 psema() 和 vsema() 例程基于手册第 3 节中定义的 semaphores(3) 接口。我们的接口采用了一个名称，使我们能够更清晰地调试它们——我们可以通过插入适当的打印语句来打印正在检查的信号量名称。我们使用一个信号量来计算可用线程的数量（池化或非池化），一个来计算任务（作业、工作项或任何我们想要的名称）的数量，一个来计算活动线程的数量。

信号量接口定义如下所示：

```c
void initsema(PVSEMA *s, int initvalue, int hi, char *name)
{
 if(sem_init(&s->pv,0,initvalue) == -1) {
 printf("sem_init() FAILED: sema=<%s> err=%d\n",name,Errno);
 exit(1);
 }
 s->name = name;
}
void psema(PVSEMA *s) // decrements or blocks if s==0
{
 sem_wait(&s->pv);
}
void vsema(PVSEMA *s) // increments
{
 int rc;

 rc = sem_post(&s->pv);
 if(rc == -1) {
 printf("sem_post(<%s>) FAILED: err=%d\n",name,Errno);
 exit(1);
 }
}
```

最后，还有队列操作。它们的作用是保护描述传入作业队列的数据结构。队列通过 enqueue() 和 dequeue() 操作进行操作。为了支持数据的排队和出队，lock 和 unlock 实现对指定对象（在本例中是工作队列）的加锁。我们将展示 enqueue 例程和相关的 dequeue 例程。

你可能会问为什么有两种计数机制。信号量计数机制专门用于计数。因为线程数量（活动和可用）是严格的数字，我们唯一需要的机制就是计数。队列例程是为更通用的排队编写的，其中对象可以被排队。在这种情况下，它们需要的不仅仅是一个简单的计数。对于我们这里的特定演示，它们已被调整为仅对整数（套接字文件描述符）进行排队；因此，它们在功能上与信号量操作相似。

