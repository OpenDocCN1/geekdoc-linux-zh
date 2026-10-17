
```c
/*************************************************************************/
/*** Creating a set of child-servers to await connection ***/
/*** ("Preforking-servlets.c" on Web site)   ***/
/*************************************************************************/
int ChildCount=0;
void sig_child(int sig)
{
    wait(0);
    ChildCount--;
}
...
main()
{
    /*** Attach signal; create & bind socket ***/
    for (; ;)
    {
        if ( ChildCount < MAXPROCESSES )
        {
            if ( (pid = fork()) == 0 )     /*---CHILD----*/
                for (; ;)
                {
                    int client = accept(sd, 0, 0);
                    Child(client);  /*---Serve new client---*/
                }
            else if ( pid > 0 )           /*---PARENT----*/
                ChildCount++;
            else                          /*---ERROR----*/
                perror( "fork( ) failed");
        }
        else
            sched_yield();                /*--- OR, sleep(1)---*/
    }
}
```

这反转了`accept()`和`fork()`的顺序：不是在连接后创建进程，而是该算法在创建子进程后等待连接。

这个代码片段可能创建例如 10 个进程。所有子进程进入无限循环，等待并处理连接。假设没有等待的连接，所有 10 个进程都处于 I/O 阻塞（睡眠）状态。当连接到达时，所有进程都会唤醒，但只有一个获得连接。剩下的九个回去睡觉。这个循环无限期地继续。

如果一个子进程崩溃或终止会发生什么？这就是为什么父进程永远不进行`accept()`系统调用的原因。父进程的主要角色是确保始终有正确数量的子进程可用。

最初，父进程创建子进程的配额。当子进程终止时，信号处理程序获取通知并将配额减一。当父进程恢复时，它创建一个新子进程。如果父进程不需要创建更多子进程，它将时间片让给其他任务。

## 适应不同的负载级别

父进程的主要责任是确保有足够的子进程可用，以处理传入的连接。这一责任必须与计算机的资源负载保持平衡。如果你不仔细，客户端可能会因超时而开始掉线，因为你的服务器没有足够的监听器来处理连接。

使用固定数量的监听器（`servlets`）对活跃连接的数量设置了限制。这是预派生 servlets 的主要限制。然而，限制程序创建和销毁进程数量的想法是一个好主意。它减轻了进程表和系统资源的混乱。有什么好方法可以在满足连接客户端需求的同时最小化创建和销毁吗？

你可以使 servlet 算法适应系统的需求。你的服务器必须应对两个不同的挑战：知道何时创建更多的 servlets，以及知道何时终止多余的。第二个挑战很简单：如果 servlet 空闲了一段时间，它会自行终止。

第一个挑战，知道何时创建更多的 servlets，并不那么直接。你可能记得每个 TCP 服务器都有一个监听队列（这就是`listen()`系统调用的功能）。网络子系统将每个连接请求入队，而`accept()`系统调用确认并创建到客户端的专用通道。如果客户端在队列中停留时间过长，它可能只等几分钟就会放弃。

能够看到队列中有多少待处理连接以及最长的等待请求可能是多少，可能有助于服务器调优。你可以使用这些信息来监控系统对请求的响应能力。随着队列填满，服务器可以创建更多的 servlets。如果连接延迟变得太长，你可能只需调整 servlet 的自终止延迟。不幸的是，这不是 API 调用提供的功能。如果你想要 servlet 的适应性，你必须使用另一种方法。

一种创建新 servlet 以应对大量请求的方法类似于撒诱饵捕鱼。在合法的情况下，渔民撒出不同种类的诱饵样本。鱼吃的诱饵就是渔民使用的诱饵。鱼的反应还指示了鱼群有多大。

像撒诱饵一样，服务器偶尔会多派生一个 servlet。只要终止的多余 servlet 数量与创建的数量相同（因为无事可做），服务器就继续这个过程。当 servlet 停止终止时，你的服务器增加创建的多余 servlet 数量，直到数量再次稳定。

预派生的目的是最小化创建和清理 servlet 的时间。随意创建和终止 servlet 会将你带回为每个新连接进行派生的做法。你必须仔细规划以避免这种结果。此外，你的算法必须运行最少数量的 servlet 才能使此方法生效。

这就是统计数据有点帮助的地方。适应性算法必须面对三种可能性：连接数量是稳定的，正在增加，或正在减少。如果连接数量是稳定的，服务器会看到在给定时间段内终止的 servlet 数量与创建的数量相同。例如，如果你的服务器每 60 秒创建一个 servlet（带有 30 秒的空闲超时），你可能会在图 9.1 的示意图中看到第一种模式。

**图 9.1.** 抛出额外的 servlet 以查看是否有待处理的连接。

`img/03334662da8fdfb8d95a02f270c522f6_156_0.png`

`img/03334662da8fdfb8d95a02f270c522f6_156_1.png`

如果连接数量正在增加，则被终止的连接少于被创建连接。如果你的服务器在规定的时间间隔内未观察到连接终止，你可以假设它正在处理一个连接。此时，你的服务器会将 Servlet 创建速率加倍（参见 **图 9.1** 中的第二个模式）。这一过程持续进行，直到 Servlet 数量达到上限，或者你的服务器达到最大创建频率（例如，每隔 5 秒一次）。

再次假设，你的服务器每 60 秒创建一个新 Servlet（空闲超时为 30 秒）。如果额外的 Servlet 未在规定时间内终止，你可以将创建之间的时间延迟减半，从而将频率加倍。你可以重复这一过程，直到连接速率开始稳定下来。

最后，当连接开始减少时，待处理的连接（如果存在）拥有的 Servlet 远多于队列所需，服务器开始观察到 Servlet 的终止。当多余的 Servlet 开始终止时，你可以将服务器的频率重置为正常水平。

```c
/***************************************************/
/*** Chumming connections example	***
/*** ("servlet-chummer.c" on Web site)	***
/***************************************************/
int delay=MAXDELAY;		/* for example, 5 seconds */
time_t lasttime;
void sig_child(int signum)
{
	wait(0);			/* Acknowledge termination */
	time(&lasttime);		/* get the time stamp */
	delay = MAXDELAY;		/* reset chummer back */
}
void Chummer(void (*servlet) (void))
{
	time(&lasttime);		/* Initialize timestamp */
	for (;;) {
		if ( !fork() )		/* first, set the chum */
			servlet();	/* call the task (must have exit()) */
		sleep(delay);		/* dream for a while */
		/* If no child terminated, double frequency */
		if ( time(0) - times[1] >= delay-1 )
		if ( delay > MINDELAY )	/* don’t go below min */
			delay /= 2;	/* double chum frequency */
	}
}
```
