
``` 
exit(1);
}

/* The Daytime service: Send current time as string to client */
/* TCPdaytime(asock); */
/* Deallocate the active socket and accept next connection */
close(asock);
/* while */

int CreatePassiveSock(char *protocol, char *portstr, int qlen)
{
/* Insert code for the function */
}

/* TCPdaytime(active socket descriptor) */
int TCPdaytime(int s)
{
int n;
time_t current_time; /* Current time in ticks */
char *str; /* Pointer to time string */
char *ctime();

/* Get the current time in terms of clock ticks from */
/* UNIX Epoch, i.e., midnight January 1, 1970 and */
/* save it in current_time. */
(void) time(&current_time);

/* Convert current time into a humanly readable string */
/* and return pointer to this string, saved in ptr */
str = ctime(&current_time);

/* Send humanly readable string to client process */
if ((n = write(s, str, strlen(str))) == -1) {
perror("write call failed");
exit(1);
}

return 0;
}
```

```
% cat daytime_client_TCP.c
#include <netdb.h>
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
```

```
#define BUFF      256

int main(int argc, char *argv[])
{
    int csock; /* Descriptor for connected socket */
    if (argc != 4) {
        printf("Usage: %s hostname port protocol\n", argv[0]);
        exit(0);
    }

    csock = CreateConnectedSock(argv[1], argv[2], argv[3]);

    /* Perform client-side of the DAYTIME service using csock,  */
    /* the client socket connected the server-side active socket */
    DaytimeClientTCP(csock);

    /* Deallocate socket and return */
    close(csock);
    return 0;
}

int CreateConnectedSock(char *ip, char *portstr, char *protocol)
{
    /* Insert code for the function */
}

/* Client side of the DAYTIME service. 'sock' is the  */
/* client socket connected to serve's active socket.  */
void DaytimeClientTCP(int sock)
{
    int n;
    char buf[BUFF];

    /* Read time string from server and display on screen */
    while ((n = read(sock, buf, BUFF)) > 0)
        write(1, buf, n);
}
```

以下是 `DAYTIME` 客户端-服务器软件的编译和示例运行。如前所述，在 Solaris 机器上，您将使用 `gcc -w -lsocket daytime_server_TCP.c -o udpdaytimes` 命令生成服务器程序的可执行代码，并使用 `gcc -w -lsocket -lnsl daytime_client_TCP.c -o udpdaytimec` 命令生成客户端程序的可执行代码。

```
% gcc46 daytime_server_TCP.c -w -o tcpdaytimes
% gcc46 daytime_client_TCP.c -w -o tcpdaytimec
```

```
% ./tcpdaytimes tcp 6001 &
[1] 6566
% ps
PID TT STAT TIME COMMAND
1291 1 Ss 0:00.66 -csh (csh)
6566 1 S 0:00.00 ./tcpdaytimes tcp 6001
6573 1 R+ 0:00.01 ps
2963 4 Is+ 0:00.42 -csh (csh)
% ./tcpdaytimec 127.0.0.1 6001 tcp
Sat Aug 15 20:58:22 2015
% kill -9 6566
%
```

## EXERCISE 20.16

在你的 UNIX 系统上重复此会话以验证其按预期工作。

## EXERCISE 20.17

在同一台机器上的不同窗口中以及在 Internet 上的不同机器上运行客户端和服务器进程。

我们已经尝试根据迄今为止讨论的三个应用程序来构建我们的软件。然而，我们仍然在客户端和服务器软件中看到代码克隆，特别是在 `CreateConnectedSock()` 和 `CreatePassiveSock()` 函数中。这意味着我们可以通过使用重构并将这些克隆制作成函数来进一步改进客户端-服务器软件的设计。我们可以通过使用额外的抽象来进一步改进我们的设计。这些函数可以归档在网络编程和系统调用的现有库之上的库中。我们将这项工作留给读者作为练习。

### 20.8.3 迭代一次性连接导向客户端-服务器模型

在此模型中，客户端和服务器进程使用基于 `TCP` 协议的连接导向式通信进行通信。服务器进程等待来自客户端进程的连接请求，接受来自客户端的连接请求，在收到客户端进程的明确请求后形成响应，将响应发送给客户端进程，然后返回等待来自另一个客户端的连接请求。图 20.18 和 20.19 显示了此客户端-服务器模型的算法、系统调用图和交互序列。

我们现在讨论 `ECHO` 服务的迭代一次性连接导向客户端-服务器模型的示例。我们的模型实现了众所周知的 `ECHO` 服务，只是它在任意端口提供服务，而不是在众所周知的端口 7。在此 `ECHO` 服务模型中，客户端进程向服务器进程发送连接请求。服务器进程接受连接请求，从客户端进程接收一些文本，将相同的文本发送回客户端进程，关闭活动套接字，然后返回

接受另一个客户端请求。客户端进程从服务器进程接收文本，将其显示在屏幕上，关闭其套接字并退出。

| Server process | Client process |
| --- | --- |
| 1. Create a socket for `SOCK_STREAM` style of communication | 1. Create a socket for `SOCK_STREAM` style of communication |
| 2. Bind the socket using the `bind()` system call | 2. Send a connection request to the server process using the `connect()` system call |
| 3. Put the socket in passive mode using the `listen()` system call | 3. Send a request to the server process using the `write()` system call |
