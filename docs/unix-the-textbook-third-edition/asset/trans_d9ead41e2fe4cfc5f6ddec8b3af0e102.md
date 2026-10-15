

我们现在讨论一个迭代连接触发的客户端-服务器模型的示例，用于以人类可读的形式提供当前时间。在此示例中，我们实现了众所周知的 DAYTIME 服务，只是我们的服务在任意端口提供，而非众所周知的端口 13。我们将讨论该应用的客户端和服务器进程的源代码。

用于 TCP 连接触发 DAYTIME 服务的客户端-服务器模型的协议与 TCP TIME 服务非常相似，只是存在两点差异。首先，客户端进程在成功与服务器进程建立连接后不会向服务器进程发送任何消息。其次，在 TIME 服务的情况下，当前时钟滴答计数在客户端侧转换为人类可读的时间形式，而在 DAYTIME 服务的情况下，转换在服务器侧进行。

客户端和服务器软件的总体结构与 TIME 服务非常相似，当然，除了在双方处理当前时间的函数之外。

以下是客户端和服务器软件的源代码：

```
% cat daytime_server_TCP.c
#include <stdio.h>
#include <time.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>

#define BUFF 256
#define QLEN 5

int main(int argc, char *argv[])
{
    int psock, asock, caddrlen;
    struct sockaddr_in caddr;

    /* Exit if program is not run with two command line arguments. */
    if (argc != 3) {
        printf("Usage: server protocol port\n");
        exit(1);
    }

    /* Create a TCP socket, bind name to it, and put it in passive mode */
    psock = CreatePassiveSock(argv[1], argv[2], QLEN);

    caddrlen = sizeof(caddr);
    while (1) {
        /* Accept actual connection from the client */
        if ((asock = accept(psock, (struct sockaddr *)&caddr, &caddrlen)) == -1) {
            perror("accept failed");
```

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

以下是 DAYTIME 客户端-服务器软件的编译和示例运行。如前所述，在 Solaris 机器上，您将使用 `gcc -w -lsocket daytime_server_TCP.c -o udpdaytimes` 命令生成服务器程序的可执行代码，并使用 `gcc -w -lsocket -lnsl daytime_client_TCP.c -o udpdaytimec` 命令生成客户端程序的可执行代码。

```
% gcc46 daytime_server_TCP.c -w -o tcpdaytimes
% gcc46 daytime_client_TCP.c -w -o tcpdaytimec
```

