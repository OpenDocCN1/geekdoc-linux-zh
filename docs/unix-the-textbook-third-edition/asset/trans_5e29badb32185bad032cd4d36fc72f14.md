
```
/* Create a TCP socket, bind name to it, and put it in passive mode */
psock = CreatePassiveSock(argv[1], argv[2], QLEN);

while (1) {
    /* Accept actual connection from the client */
    if ((asock = accept(psock, (struct sockaddr *)&caddr,
&caddrlen)) == -1) {
        perror("accept failed");
        exit(1);
    }
    /* Create a slave process and have it server the client  */
    /* The parent process closes the newly created active  */
    /* socket and goes back to accept the next client request */
    pid = fork();
    if (pid == -1) {
        perror("fork failed");
        exit(1);
    }
    if (pid == 0) { /* Child process */
        close(psock); /* Deallocate passive socket */
        /* The Daytime service: Send current time as string */
        /* to client using active socket */
        (void) TCPdaytime(asock);
        exit(0);
    }
    else /* Parent process: Deallocate the active socket */
        close(asock);
} /* while */

int CreatePassiveSock(char *protocol, char *portstr, int qlen)
{
    /* Insert code for the function */
}

int TCPdaytime(int s)
{
    /* Insert code for the function */
}
```

以下是源代码的编译、 resultant 可执行代码的运行，以及使用第 20.8.2 节中开发的 DAYTIME 客户端对其进行测试的汇总。各种命令的输出不言自明。该会话表明，你可以使用回环地址与客户端命令一起使用，而无需显式指定客户端和服务器进程运行的主机的 IP 地址。

```
% gcc46 daytime_concurrent_server_TCP.c -w -o tcpdaytimecons tcp 6001 &
[1] 18738
```

```
% /tcpdaytime 202.147.169.196 6001 tcp
Sat Aug 15 22:56:46 2015
```

```
% ps
PID TT STAT TIME COMMAND
1291 1 Is+ 0:00.73 -csh (csh)
16351 2 Ss 0:00.46 -csh (csh)
18738 2 S 0:00.00 ./tcpdaytimecons tcp 6001
18822 2 Z 0:00.00 <defunct>
18827 2 R+ 0:00.01 ps
16380 3 Is+ 0:00.16 -csh (csh)
```

```
% /tcpdaytime 127.0.0.1 6001 tcp
Sat Aug 15 22:56:55 2015
```

```
% ps
PID TT STAT TIME COMMAND
1291 1 Is+ 0:00.73 -csh (csh)
16351 2 Ss 0:00.47 -csh (csh)
18738 2 S 0:00.00 ./tcpdaytimecons tcp 6001
18822 2 Z 0:00.00 <defunct>
18840 2 Z 0:00.00 <defunct>
18849 2 R+ 0:00.01 ps
16380 3 Is+ 0:00.16 -csh (csh)
```

```
% kill -9 18738 18822 18840
```

## EXERCISE 20.22

在你的 UNIX 系统上重复此会话，以验证其按预期工作。显示在 Solaris 机器上为客户端和服务器程序生成可执行代码的编译器命令。

## EXERCISE 20.23

在同一台机器的不同窗口上以及互联网上不同机器上运行客户端和服务器进程。验证并发服务器在多个同时客户端下的工作情况。

请注意，ps 命令的输出显示，当子/从属进程终止时，它们会变成僵尸。这是因为其父进程在它终止时没有等待。看起来解决此问题的明显方法是在使用 wait()（或此调用的变体）在父代码的 close(sock) 语句之前。 然而，这将使父进程等待子（从属）进程终止，从而使模型变为迭代。解决此问题的真正方法是让子进程成为僵尸，然后立即将其从系统中移除。这可以通过使用信号处理来实现，如第 20.5 节所述。回想一下，当子进程终止时，UNIX 内核会生成 SIGCHLD 信号。你可以在服务器进程中插入几行代码来拦截此信号并运行 wait3() 系统调用以从系统中移除相关的僵尸。我们将在第 21.12 节详细讨论这个问题。现在，你可以手动使用 kill 命令删除僵尸，或者使用第 21.12 节中给出的代码段在僵尸进程创建时清理它。现在，我们使用 kill 命令从系统中删除僵尸进程。

该模型中服务器进程的结构可以通过让每个从属进程使用来自 exec() 家族的调用用另一个可执行文件覆盖自身来扩展。可执行文件对应于为给定客户端请求提供的服务。这种服务器进程的图形视图如图 20.27 所示。

![](img/02e070097d401d3bf7de4bf1c470b267_978_0.png)

FIGURE 20.27 Concurrent connection-oriented server process using fork() and exec().

## 20.9 SYNCHRONOUS VERSUS ASYNCHRONOUS I/O: THE SELECT() SYSTEM CALL

UNIX 系统调用如 read()、write()、recvfrom()、sendto() 和 accept() 如果与之关联的套接字描述符未准备好执行输入、输出或连接建立 [在 accept() 的情况下] 则会阻塞。一旦与这些调用关联的套接字描述符准备好进行 I/O 或连接建立，调用就会解除阻塞并执行其指定的操作。

基于信号的 I/O 也以类似的方式工作。一旦信号发生，相关的信号处理代码就会执行。基于阻塞调用和信号的 I/O 被称为同步 I/O。两者都与计算机系统中的中断处理类似工作。

