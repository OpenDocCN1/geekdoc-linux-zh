
```c
/**
 * netconn.c - Connect to a TCP/IP socket
 */
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <stdlib.h>
#include <stdio.h>
#include "helper.h"

int main(int argc, char *argv[])
{
    int sockfd;              /* File descriptor for socket */
    struct sockaddr_in cli;  /* Client's socket structure */
    socklen_t socklen;       /* Size of sockaddr */

    /* Expect the IP address on the command-line */
    if(argc != 2) {
        puts("USAGE: netconn <ip address>");
        exit(EXIT_FAILURE);
    }

    /* Create a socket */
    if((sockfd = socket(PF_INET, SOCK_STREAM, 0)) < 0)
        err_quit("socket");

    /* Set up the client */
    memset(&cli, 0, sizeof(cli));
    cli.sin_family = AF_INET;
    cli.sin_port = htons(50000); /* Don't forget network byte order */
    /* This will self-destruct if the IP address is invalid */
    if(!(inet_aton(argv[1], &cli.sin_addr)))
        herr_quit("inet_aton");

    /* Connect to the socket */
    socklen = sizeof(cli);
    if(connect(sockfd, (struct sockaddr *)&cli, socklen))
        err_quit("connect");
    puts("connected to socket");

    exit(EXIT_SUCCESS);
}
```

除了处理 TCP/IP 套接字的代码外，`netconn.c` 还包含一个新函数 `herr_quit`，它定义在 `helper.c` 中，并调用了一个专用于 TCP/IP 的错误处理函数 `herror`。它的行为与 `perror` 调用完全相同。要执行 `netconn`，请传递你想连接的主机的 IP 地址（点分十进制格式），如下列列表所示（在一个窗口中运行 `netconn`，在另一个窗口中运行 `mknet`）：

![输出](img/be588b36b489136ce784030a08a1d3d4_434_0.png)

### 输出

```bash
$ ./netconn 0
connected to socket
$ ./mknet
TCP/IP socket available
port 50000
addr 0.0.0.0
new connection granted
```

再次强调，向 `netconn` 传递零会让内核使用其自行选择的地址。你可以用 `0.0.0.0` 或你系统的 IP 地址（如果有的话）来代替零。图 18.6 表明 `mknet` 能够与互联网通信。我从另一台系统使用 `telnet` 连接到运行 `mknet` 的系统，使用了指定替代端口的 `telnet` 语法（`telnet` 的默认端口是 23）。

![图 18.6](img/be588b36b489136ce784030a08a1d3d4_434_1.png)

### 输出

![输出](img/be588b36b489136ce784030a08a1d3d4_434_2.png)

## 读取和写入 TCP/IP 套接字

读取和写入 TCP/IP 套接字与读取和写入 UNIX 域套接字完全相同。再一次，Linux 的抽象机制证明了一项真正的福音。对 `wrsock` 和 `rdsock` 进行几处简单的修改，如下面的示例所列，表明这有多简单。

## 示例

![代码](img/be588b36b489136ce784030a08a1d3d4_435_0.png)

```c
/*
 * rdnet.c - Make and bind to a TCP/IP socket, then read it
 */
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <stdlib.h>
#include <stdio.h>
#include "helper.h"

int main(void)
{
    int sockfd, infd; /* File descriptors for socket */
    struct sockaddr_in srv; /* Server's socket structure */
    socklen_t socklen;

    /* Create the socket */
    if((sockfd = socket(PF_INET, SOCK_STREAM, 0)) < 0)
        err_quit("socket");

    /* Initialize and set up the server structure */
    memset(&srv, 0, sizeof(srv));
    srv.sin_family = AF_INET;
    srv.sin_port = htons(50000);

    /* Bind the socket to an address */
    socklen = sizeof(srv);
    if((bind(sockfd, (struct sockaddr *)&srv, socklen)) < 0)
        err_quit("bind");

    /* Wait for incoming connections */
    if((listen(sockfd, 5)) < 0)
        err_quit("listen");
    puts("TCP/IP socket available");
    printf("\tport %d\n", ntohs(srv.sin_port));
    printf("\taddr %s\n", inet_ntoa(srv.sin_addr));

    /* Accept the first connection that comes in */
    if((infd = accept(sockfd, (struct sockaddr *)&srv, &socklen)) >= 0)
        puts("new connection granted");

    /* Read from the socket and write to stdout */
    xfer_data(infd, fileno(stdout));

    exit(EXIT_SUCCESS);
}
```
