
![](img/2591af4bdf00a0f382331fc9481f785e_221_0.png)

## 图 9.1

> *额外的 servlet 被抛出来以查看是否有待处理的连接。*

同样，假设你的服务器每 60 秒创建一个新 servlet（空闲超时为 30 秒）。如果额外的 servlet 未能在规定时间内终止，你可以将创建之间的时间延迟减半，从而将频率加倍。你可以重复此过程，直到连接速率开始稳定下来。

最后，当连接开始减少时，待处理的连接（如果存在）为队列提供了绰绰有余的 servlet，服务器开始看到 servlet 的终止。当额外的 servlet 开始终止时，你可以将服务器的频率重置为正常。

```c
 /*********Chumming connections example*********/
 /**** ('servlet-chummer.c' on Web site)****/
 int delay=MAXDELAY;         /* for example, 5 seconds */
 time_t lasttime;
 void sig_child(int signum)
 {
     wait(0);                /* Acknowledge termination */
     time(&lasttime);        /* get the time stamp */
     delay = MAXDELAY;       /* reset chummer back */
 }
 void Chummer(void (*servlet)(void))
 {
     time(&lasttime);        /* Initialize timestamp */
     for (;;)
     {
         if ( !fork() )     /* first, set the chum */
         {
             servlet(); /* call the task (must have exit()) */
             sleep(delay); /* dream for a while */
         } /* if no child terminated, double frequency */
         if ( time(0) - times[1] >= delay-1 )
         {
             if ( delay > MINDELAY ) /* don't go below min */
                 delay /= 2;        /* double chum frequency */
         }
     }
 }
```

此代码片段展示了如何通过记录最后一个子进程终止的时间来跟踪 servlet 的形成并测试负载是否增加。终止操作也会重置计时器，以便当前连接可以稳定下来，并且进程可以重新启动。

### 使用智能 Select 扩展控制

使用进程来管理连接流是一种直观的任务分配方式。此外，对运行进程数量的限制和预先 fork 进程确保了连接得到所需的关注。然而，这些方法都存在一个根本问题：调度器风暴（scheduler storm）。

### 调度器风暴

调度器风暴提出了两个问题，这些问题暴露了多任务处理器的局限性以及单 CPU 系统为何会被压垮的原因。第一个问题展示了大型进程表对 servlet 的影响。第二个问题影响了预 fork（preforking）概念。

进程表可以轻松处理几百个进程。取决于内存和交换空间（swap），理论上你可以拥有更多。尽管如此，请考虑其限制：Linux 每 10 毫秒在进程之间进行切换。这尚未包括卸载旧进程上下文和加载新进程上下文的时间延迟。

例如，如果你有 200 个正在运行的 servlet，在一个每 0.01 秒切换一次任务的系统上，每个进程可能需要等待 2 秒才能获得一小片 CPU 时间。如果每个时间片（timeslice）在该小切片内能发送 1 KB 数据，你在 10 Mbps 局域网连接上可能会看到大约 200 KBps 的吞吐量（对于 TCP/IP 来说大致相当）。然而，每个连接每秒仅获得 512 字节。这是让进程表无限制增长的主要风险。

第二个问题在于预 fork 的核心：多个进程都在等待同一个连接。当连接请求到达时，你的服务器可能有 20 个处于 I/O 阻塞状态的 servlet。由于都在等待连接，内核会唤醒所有 20 个。第一个进程获取连接，而其余所有进程返回到 I/O 阻塞状态。一些程序员将此称为*调度风暴*（scheduling storm）或*惊群*（thundering herd）。在这两种情况下，这个问题都强调了最小化等待 servlet 的数量并根据连接负载进行适应的必要性。

**在内核中解决惊群问题**
撰写关于 Linux 这种不断演进的书籍的一个问题是，信息很快就会过时。Linux 2.4 通过只唤醒一个 I/O 阻塞进程解决了内核中的惊群问题。

![](img/2591af4bdf00a0f382331fc9481f785e_222_0.png)

## 过载的 select()

解决这些问题的一种方法是完全避免多任务处理。在之前的一章中，你阅读过关于 I/O 多路复用系统调用：select() 和 poll()。这些系统调用可以像多个进程一样起作用。

相反让 20 个服务器进程都在等待连接，你可以提供一个进程来等待连接。当连接请求到达时，服务器将该连接（客户端通道）放入 I/O 列表中。这些系统调用等待其中任何一个发送请求或命令。系统调用将准备好的通道返回给你的服务器，你的服务器获取并处理该命令。

完全跳过多任务处理并使用这些多路复用器的诱惑可能会导致某些性能损失。当使用单个任务处理信息时，你的程序或服务器必须在进程生命周期的各个时间点等待 I/O。如果你不利用这段空闲时间，你的服务器可能会错失进行其他操作的重大机会。例如，如果你曾经编译过内核，你可能会发现，如果使用 -j make 选项强制多个任务，编译时间会更短。（如果你有内存，每个处理器两个或三个任务会显著缩短编译时间。）

## 使用智能 Select 进行折中

当你创建高性能、高需求的服务器时，你可以使用各种方式来分配负载。其中两种是多任务处理和 I/O 多路复用。然而，如果单独使用，多任务处理可能会失去对调度器的控制，并耗费宝贵的时间进行上下文切换，而 I/O 多路复用则浪费了未使用的 CPU 带宽。使用二者的结合是一个替代方案。将两者结合成一个*智能 Select*（Smart Select）可以帮助你减少各自的劣势，同时保留你的两种能力。

智能 Select 分发少数几个进程。每个进程拥有一个连接通道和一组打开的客户端通道。一个 I/O 多路复用器管理所有这些通道。以下是该进程的算法：

```c
/*** Smart Select example: each child tries to accept a 
 ***  connection.  If successful, it adds the connection 
 ***  to the select() list. 
 ***  ("smart-select.c" on Web site) 
 *****************************************************/
int sd, maxfd=0;
fd_set set;
FD_ZERO(&set);

/** Create socket and fork() processes **/

/*---In Child---*/
maxfd = sd;
FD_SET(sd, &set);
for (;;) 
{
    struct timeval timeout={2,0};                /* 2 seconds */
    /*---Wait for some action---*/
    if ( select(maxfd+1, &set, 0, 0, &timeout) > 0 )
    {
        /*---If new connection, connect and add to list---*/
        if ( FD_ISSET(sd, &set) )
        {
            int client = accept(sd, 0, 0);
            if ( maxfd < client )
                maxfd = client;
            FD_SET(client, &set);
        }
        /*---If command/request from client, process---*/
        else
        {
           /** Process client's request ***/
           /** If client just closed, remove from list ***/
        }
    }
}
```

你可以使用此算法创建少数几个进程——远少于在纯多任务服务器中可创建的数量——例如，5–10 个 servlet。每个 servlet 进而可以支持 5–10 个连接。

> **Select 冲突**
> 你可能听说过 BSD 的一个问题，称为*select 冲突*（select collision）。之前的算法假设 `select()` 可以等待多个描述符，并仅在描述符状态改变时唤醒。BSD 4.4 实现有一个限制，会导致所有阻塞在 `select()` 中的进程都唤醒。看起来 Linux 没有这个限制。

这种方法可以轻松支持数百个连接而互不干扰。任务数量和连接数量之间的平衡有助于最小化对进程表的影响。然而，拥有如此多的连接可能会带来问题，如果你需要跟踪你的协议状态。

你可以轻松地将此算法用于无状态服务器。无状态连接不记忆任何关于之前事务的信息。这需要发送到你的服务器的所有事务与其他事务或每个连接之间的单个事务没有关联。此外，如果你的服务器需要短期到中期连接，你可以使用这种方法。一些例子是 HTTP 服务器、数据库查询服务器和 Web 重定向器。

