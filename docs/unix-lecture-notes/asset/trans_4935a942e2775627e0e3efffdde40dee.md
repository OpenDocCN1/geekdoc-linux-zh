

children, and it remains in its loop as long as there is a zombie to be collected. The WNOHANG flag is used to prevent it from blocking in the waitpid() code. This way, if multiple SIGCHLD signals arrive while it is in the handler, the children whose deaths caused them will be collected. (Remember that signals may not be reliably handled on all systems, and even though in a POSIX compliant system, each SIGCHLD will be delivered if we set SA_NODEFER, it is safer to collect them in this loop.)

```
void on_sigchld( int signo )
{
    pid_t pid;
    int status;

    while ( (pid = waitpid(-1, &status, WNOHANG) ) > 0 )
        fprintf(upcaselog_fp, "Child process %d terminated.\n", pid);
    fflush(upcaselog_fp);
    return;
}
```

```
void on_sigpipe( int signo )
{
    fprintf(stderr, "Client is not reading the pipe.\n");
}
```

```
void on_signal( int sig )
{
    close(publicfifo);
    close(dummyfifo);
    if ( clientreadfifo != -1 )
        close(clientreadfifo);
    if ( clientwritefifo != -1 )
        close(clientwritefifo);
    if ( getpid() == server_pid )
        unlink(PUBLIC);
    fclose(upcaselog);
    exit(0);
}
```

## Comments.

- 所有工作都由子进程执行。每个子进程开始时都会尝试打开客户端的 raw_text FIFO 以进行读取。如果成功，它会进入一个循环，反复读取、将文本转换为大写、打开客户端的 converted_text FIFO、将转换后的文本写入其中，然后关闭它。
- 由于客户端可能因各种原因无法打开 converted_text 进行读取——它可能已被终止——子进程会在放弃之前尝试固定次数的 open()。它使用与迭代服务器相同的方法，使用非阻塞 open()。
- 当子进程成功打开 FIFO 后，它仍会检查 write() 是否失败，因为中间可能发生任何事情，如果失败，子进程就会退出。否则，它会写入

数据，关闭其 FIFO 的一端并等待从客户端读取更多文本。当它收到文件结束时，它会退出。

- 你可能会想知道为什么服务器要反复打开和关闭客户端 converted_text FIFO 的写端。这是客户端在其 read() 中接收到 EOF 的唯一方式。如果客户端没有收到 EOF，那么它将阻塞在对 converted_text FIFO 的读取中，并且无法向服务器发送更多数据。这将使客户端和该服务器子进程陷入死锁，因为该进程会返回到对客户端 raw_text FIFO 的 read() 并阻塞等待来自客户端的数据，而数据永远不会到达。因此，虽然每次都打开和关闭此 FIFO 看起来效率低下，但它是防止死锁的最简单方法。

- 信号处理程序会检查父进程是否正在执行它。如果父进程收到信号，则应删除公共 FIFO，否则不应删除。我们不希望子进程删除此 FIFO！

- 如果你对套接字有一定了解，你可能会注意到此服务器的设计很容易转换为使用套接字的服务器。我们在学习套接字时会再次参考此示例。

## 8.5 Daemon Processes

如前所述，守护进程是一个在后台运行、没有控制终端的进程。此外，守护进程会将其工作目录设置为 "/"。通常守护进程由系统初始化脚本在启动时启动。如果你编写了一个服务器并想将其转变为完整的守护进程，仅将其放到后台是不够的。这只会告诉 shell 不要等待它；它仍然拥有控制终端，并且仍会被该终端发出的任何信号杀死。

一些守护进程由其他程序启动。例如，一些网络守护进程由 inetd 或 xinetd 超级服务器启动。一些由 crond 守护进程等程序启动，后者运行计划任务。一些在用户终端上调用。例如，有时打印机守护进程会在终端上由超级用户停止并重新启动。

由于守护进程没有控制终端，它们无法向标准输出或标准错误写入消息。相反，它们可以使用名为 syslog() 的系统日志函数，它是一个与 syslogd 守护进程通信的客户端，后者将消息写入特定的日志文件。glibc 版本的此函数是 klogctl()。稍后我们将查看如何使用它的示例。服务器应设计为使自身成为守护进程。换句话说，当服务器运行时，它应采取所有必要的步骤成为守护进程，其中包括：

- 1. 将自身放到后台。它通过 fork 一个新进程并以子进程执行其代码，而父进程执行 exit() 来实现。当父进程退出时，启动它的 shell 会收集其退出状态并认为已调用的程序已终止（确实如此）。子进程，即现在是服务器的进程，不再在前台，但它仍受终端控制。
- 2. 使自身成为会话领导者。回想一下，一个进程可以通过成为会话领导者来与终端分离，但只有既不是会话领导者也不是进程

