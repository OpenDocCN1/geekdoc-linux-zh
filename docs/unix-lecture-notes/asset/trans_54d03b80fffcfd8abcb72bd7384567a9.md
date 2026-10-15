

(e) 关闭私有 FIFO 的写端。

它将无限循环，因为它永远不会在管道上收到文件结束，因为它自己保持写端打开。它是通过发送信号来终止的。代码如下。

## Listing 8.14: upcased1.c

```
#include "upcase1.h"

#define WARNING "\nNOTE: SERVER ** NEVER ** accessed private FIFO\n"
#define MAXTRIES 5

int dummyfifo;    /* file descriptor to write-end of PUBLIC */
int privatefifo;  /* file descriptor to write-end of PRIVATE */
int publicfifo;   /* file descriptor to read-end of PUBLIC */

void on_sigpipe( int signo )
{
    fprintf(stderr, "Client is not reading the pipe.\n");
}

void on_signal( int sig )
{
    close(publicfifo);
    close(dummyfifo);
    if ( privatefifo != -1 )
        close(privatefifo);
    unlink(PUBLIC);
    exit(0);
}

/********************************************************************************/
/*                              Main Program                                    */
/********************************************************************************/

int main( int argc, char *argv[] )
{
    int tries;          /* num tries to open private FIFO */
    int nbytes;         /* number of bytes read from popen() */
    int i;
    int done;           /* flag to stop loop */
    struct message msg; /* stores private fifo name and command */
    struct sigaction handler;   /* sigaction for registering handlers */

    /* Register the signal handler */
    handler.sa_handler = on_signal;
    handler.sa_flags = SA_RESTART;
    if ( ((sigaction(SIGINT, &handler, NULL)) == -1 ) ||
         ((sigaction(SIGHUP, &handler, NULL)) == -1 ) ||
         ((sigaction(SIGQUIT, &handler, NULL)) == -1 ) ||
         ((sigaction(SIGTERM, &handler, NULL)) == -1 )
    ) {
        perror("sigaction");
```

```
exit(1);
}

handler.sa_handler = on_sigpipe;
if ( sigaction(SIGPIPE, &handler, NULL) == -1 ) {
    perror("sigaction");
    exit(1);
}

/* Create public FIFO */
if ( mkfifo(PUBLIC, 0666) < 0 ) {
    if ( errno != EEXIST )
        perror(PUBLIC);
    else
        fprintf(stderr, "%s already exists. Delete it and restart.\n", PUBLIC);
    exit(1);
}

/* Open public FIFO for reading and writing so that it does not get an EOF on the read-end while waiting for a client to send data.
To prevent it from hanging on the open, the write-end is opened in non-blocking mode. It never writes to it.
*/
if ( ( publicfifo = open(PUBLIC, O_RDONLY) ) == -1 ||
     ( dummyfifo = open(PUBLIC, O_WRONLY | O_NDELAY) ) == -1 ) {
    perror(PUBLIC);
    exit(1);
}

/* Block waiting for a msg struct from a client */
while ( read( publicfifo, (char*)&msg, sizeof(msg)) > 0 ) {
    /* A msg arrived, so start trying to open write end of private FIFO */
    tries = done = 0;
    privatefifo = -1;
    do {
        if ( ( privatefifo = open(msg.fifo_name,
                                 O_WRONLY | O_NDELAY)) == -1 )
            sleep(1);   /* sleep if failed to open */
        else {
            /* Convert the text to uppercase */
            nbytes = strlen(msg.text);
            for ( i = 0; i < nbytes; i++ )
                if ( islower(msg.text[i]) )
                    msg.text[i] = toupper(msg.text[i]);

            /* Send converted text to client */
            if ( -1 == write(privatefifo, msg.text, nbytes) ) {
                if ( errno == EPIPE )
                    done = 1;
            }
            close(privatefifo);  /* close write-end of private FIFO */
            done = 1;            /* terminate loop */
```

```
}
} while (++tries < MAXTRIES && !done);

if (!done)
    /* Failed to open client private FIFO for writing */
    write(fileno(stderr), WARNING, sizeof(WARNING));
}
return 0;
}
```

## Comments.

该服务器通过关闭已打开的任何描述符、删除公共 FIFO 并退出来处理所有用户发起的终止信号。它在每次循环开始时将 privatefifo 设置为 -1，如果它成功打开私有 FIFO，则 privatefifo 不再为 -1。这样，在信号处理程序中，它可以确定是否已为写入打开私有 FIFO 并需要关闭它。

如果它因 SIGPIPE 而收到信号，因为客户端在服务器写回转换后的字符串之前立即关闭了其私有 FIFO 的读端，它会通过继续监听新消息并放弃对该管道的写入来处理 SIGPIPE。

## 8.4.4 Concurrent Servers

前面的服务器是一个迭代服务器；它一次处理一个客户端请求。如果某些客户端请求可能非常耗时，那么服务器就会忙于为一个客户端服务，而排除所有其他客户端，其他客户端会遇到延迟。这可以通过允许服务器同时处理多个客户端来避免。可以同时处理多个客户端请求的服务器称为并发服务器。

创建并发服务器最简单的方法是为每个客户端 fork 一个子进程。然后服务器的角色就只剩下“监听”公共管道以获取传入请求、为新请求 fork 一个子进程来处理客户端请求，以及等待其子进程完成。等待必须通过 SIGCHLD 处理程序来完成，因为与 shell 风格的应用程序不同，此进程必须立即返回到读取公共管道的任务。因此，服务器程序主进程的基本轮廓大致如下：

- 1. 它注册其信号处理程序。
- 2. 它创建公共 FIFO。如果发现它已存在，则显示消息并退出。
- 3. 它以读写方式打开公共 FIFO，即使它只会从中读取。
- 4. 它进入其主循环，其中重复执行
- (a) 在公共 FIFO 上执行阻塞 read()，
- (b) 在从 read() 接收到消息后，fork 一个子进程来处理客户端请求。

5 当我们介绍线程时，你会看到线程是实现此目的的另一种手段。

