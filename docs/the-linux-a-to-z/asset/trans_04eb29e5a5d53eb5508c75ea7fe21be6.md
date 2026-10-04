
2. 解决此问题的方案只需将你的 *launch* 命令设置为守护进程，使进程作为守护进程运行，然后使用 exec() 将守护进程中的程序更改为命令行给出的程序即可。这可以按如下方式完成：

```
main(int argc, char **argv)
{
    Setup process as a daemon (fork, setsid, fork etc.)
    execvp(argv[1], &argv[1]);
}
```

## 微型守护进程 – 案例研究

在了解了设置守护进程所涉及的原理之后，我们现在将回到第 18.2 节中介绍的示例套接字服务器程序，看看如何将其改造成一个适当的守护进程，使其在您注销机器后仍能继续运行并提供服务。

## 23.1 守护进程列表

以下程序展示了第 18.2 节中示例套接字服务器的完整列表，已修改为作为健壮的守护进程运行。你会注意到原始服务器代码本身做了一些更改，并且还添加了 setup_daemon() 函数。所有这些内容将在列表之后详细解释：

```
/****************************************************************
THE SOCKET SERVER DAEMON
****************************************************************/

#include <stdio.h>
#include <string.h>
#include <signal.h>
#include <fcntl.h>
#include <setjmp.h>
#include <sys/param.h>
#include "socklib.h"

/* Server's communication port number */
#define PORT 2121

/* Values for the next_action parameter to fatal() */
#define NA_EXIT 0
#define NA_RESTART 1

/* Global environment store for setjmp/longjmp */
jmp_buf env;

/****************************************************************
MAIN - A very simple file transfer daemon, which sets up a concurrent
    socket server on the host machine on port number PORT to transfer
    any files from the current directory on request.
****************************************************************/
main(void)
{
    SOCKET *sp;
    int sd;

    /* Rearrange operating environment for daemon working */
    setup_daemon();
    /* Set SIGCHLD for no zombies */
    signal(SIGCHLD, SIG_IGN);

    /* Create server's socket */
    if ((sp = sopen())==0)
        /* Exit server if this fails */
        fatal("sopen()", NA_EXIT);

    /* Setup the NA_RESTART (post error) entry point */
    setjmp(env);

    /* Repeatedly accept and service client requests */
    for (;;)
    {
        /* Connect to client or restart on failure */
        if ((sd = sserver(sp, PORT, S_DELAY))==-1)
            fatal("sserver()", NA_RESTART);

        /* Fork() a child process */
        switch (fork())
        {
        /* Deal with client request in child */
        case 0:
            do_service(sd);

        /* Deal with fork() failure */
        case -1:
            close(sd);
            /* Restart for next client */
            fatal("fork()", NA_RESTART);
        }
        /* In parent, close client and loop for next connection */
        close(sd);
    }
}

/************************************************************************
SETUP_DAEMON - This function is responsible for modifying the current
    working environment of the process to that required by a daemon.
    I.e.  it closes unnecessary file descriptors, disassociates itself
    from the current controlling terminal, session and process group
    and modifies the current file creation mask.
************************************************************************/
setup_daemon(void)
{
    int i;

    /* Close all open file descriptors */
    for (i = 0; i<NOFILE; ++i)
        close(i);

    /* 1st fork() call */
    switch (fork())
    {
    /* Error in 1st fork() */
    case -1:
        fatal("setup_daemon(), 1st fork()", NA_EXIT);

    /* Exit 1st parent */
    default:
        exit(0);

    /* Continue in 1st child (2nd parent) */
    case 0:
        /* Start new session exit() on error */
        if (setsid()==-1)
            fatal("setup_daemon(), setsid()", NA_EXIT);

        /* 2nd fork() call */
        switch (fork())
        {
        /* Error in 2nd fork() */
        case -1:
            fatal("setup_daemon(), 2nd fork()", NA_EXIT);

        /* Exit 2nd parent */
        default:
            exit(0);

        /* Continue in 2nd child */
        case 0:
            /* Reset file creation mask for ERROR.LOG */
            umask(0);
            /* and return with daemon set up */
            return;
        }
    }
}

/****************************************************************
FATAL - This routine is called when an error condition is returned to
    the daemon, usually from one of the system calls it makes. The
    function first prints the message pointed to by <text> and then
    either terminates the process or restarts it with longjmp(),
    depending on the value of the <next_action> parameter.
****************************************************************/
fatal(char *text, int next_action)
{
    FILE *fp;

    /* Open the error log file */
    if ((fp = fopen("ERROR.LOG", "a"))==0)
        /* exit() on failure here, with error unreported... */
        exit(1);

    /* Write the error message */
    fprintf(fp, "Error in %s\n", text);
    fclose(fp);

    if (next_action==NA_RESTART)
        /* Restart calling process */
        longjmp(env, 1);
    else
        /* Terminate calling process */
        exit(1);
}

/**************************************************************************
DO_SERVICE - This function is called in the child process that is
created when a client makes a successful connection. Its task is
to service the client's request and supervise the required file
transfer. The parameter <sd> is the socket descriptor to use for
the communication.
**************************************************************************/
do_service(int sd)
{
    int i, fd;
    char *name;
    char c, namlen;

    /* Get length of file name */
    if (read(sd, &namlen, 1)!=1)
        fatal("namlen read()", NA_EXIT);

    /* Space for name + " open()" */
    if ((name = (char *)malloc(namlen+8))==0)
        fatal("malloc()", NA_EXIT);

    /* Get required file name into name[] */
    for (i = 0; i<namlen; ++i)
        if (read(sd, &name[i], 1)!=1)
            fatal("file name read()", NA_EXIT);

    /* Make name[] a string */
    name[i] = '\0';

    /* Check name[] is in current directory */
    if (strchr(name, '/'))
        fatal("illegal file name", NA_EXIT);

    /* Open specified file */
    if ((fd = open(name, O_RDONLY))==-1)
        fatal(strcat(name, " open()"), NA_EXIT);

    /* Transfer contents to client */
    while ((i = read(fd, &c, 1))!=0)
        if (i==-1)
            fatal("file read()", NA_EXIT);
        else if (write(sd, &c, 1)!=1)
            fatal("write()", NA_EXIT);

    /* Terminate child and with it the connection to this client */
    exit(0);
}
```

## 23.2 套接字服务器新增内容

程序中最明显的变化是添加了 setup_daemon() 函数，该函数作为 main() 的第一条语句被调用。关于该函数的作用没有令人惊讶之处，但其编码方式与我们之前看到的概念方法不同。

首先要做的任务是关闭所有文件描述符。无论它们是否打开都会执行此操作。然后，接下来有一个部分将守护进程与其控制终端、会话和进程组分离，并阻止其将来重新获取另一个终端。这是通过通常的 fork()、setsid()、fork() 序列完成的，但嵌入在一对 switch() 结构中，以便更容易处理 fork() 调用可能出现的任何错误。请记住 fork() 返回三个不同的值：出错时为 -1，子进程为 0，非零值由 default: case 处理，返回给父进程。最后，在第二个子进程中，会调用 umask() 将文件创建掩码设置为 0。这是因为如果出现任何严重错误，守护进程可能需要创建文件 ERROR.LOG，而如果不进行此调用，当前的 umask() 值可能不合适。

## 23.3 套接字服务器更改

原始示例套接字服务器的所有其他更改都直接与使守护进程能够处理系统和库调用返回的错误有关。这是通过在适当的情况下重新启动守护进程的主循环来实现的，而不是在出现任何错误时就终止守护进程。这一想法的实现是通过为 fatal() 函数添加一个额外的参数来指定的，以指定在打印出错误消息后其 next_action 应该是什么。选项有：NA_EXIT，在这种情况下调用进程终止；或 NA_RESTART，此时使用 setjmp() 和 longjmp() 库例程导致非局部跳转回到主服务器循环的开始。事实上，此重启功能仅用于在父进程的主循环中检测到的错误。如果在为客户端服务的子进程中检测到任何错误，则该进程将被允许像以前一样终止。
