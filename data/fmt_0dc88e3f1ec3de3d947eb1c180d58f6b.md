
```c
                break;

            }

            printf("Child: %s", buffer);

            if(strncmp(buffer, "EXIT", 4) == 0) /* 退出请求 */

            {

                unlink(path);

                puts("Bye!");

                close(soc);

                break;

            }
        }
        /* 子退出 */
        exit(0);
    }
    /* 连接到由子任务创建的服务器 socket */
    sleep(2); /* 等待设置 */
    if(connect(soc, (struct sockaddr *)&sock, sizeof(sock)) < 0)
    {
        perror("parent: connect(");
        exit(-1);
    }
    /* 将交互式用户输入的消息发送到子任务 */
    while(1)
    {
        sleep(1); /* 响应时间 */
        printf("enter a message: ");
        fflush(stdout);
        fgets(buffer, sizeof(buffer), stdin);
        if(send(soc, buffer, strlen(buffer)+1, 0) < 0)
        {
            perror("parent: send(");
            exit(-1);
        }
        if(strncmp(buffer, "EXIT", 4) == 0) /* 退出请求 */
        {
            close(soc);
            break;
        }
    }
    /* 等待子退出 */
    waitpid(pid);
    return;
}
```

这两个列表都通过键盘和屏幕与用户交互；它们都使用 `fork` 创建子任务，并且每个父进程都与其子任务进行通信。一个程序使用 `UDP`（列表 3.6），另一个使用 `TCP`（列表 3.7）。`TCP` 版本确保了子进程能够接收，但在应用程序代码层面，这种区别并不明显。`TCP` 为你做了大量工作，以保持通信链路可用，并确保父进程发送给子进程的消息按发送顺序原样到达。

尽管这些代码很简单，但它们可以作为你未来应用程序的模式。在提示处输入消息 `EXIT` 即可干净地退出这些程序。

## 网际协议地址

到目前为止，你关注的是所有运行在同一台计算机上的子任务和其他进程。然而，如果你要管理集群，就需要与网络上其他机器的进程进行通信。

网际协议或 `IP` 地址是一个 32 位数，用于唯一定义网络上的每台机器。这种地址方案被用于本章的主题进程间通信。

### 注意

在设计 `IP` 地址时，它提供的四十亿多个地址似乎是一个永远无法接近、更说超越的数量。`IP6` 的开发是为了解决这一局限性。

`IP` 地址通常以点点十进制法表示（例如 `192.168.1.1`）。每个字节代表一个 0 到 255 之间的 8 位值。

# 列表 3.8B 续

```c
perror("server: bind(*)");
close(fd);
exit(-1);
}
/* 将从客户端接收的消息回显给用户 */
while(1) {
    recvfrom(fd, buffer, sizeof(buffer), 0,
        (struct sockaddr *) &sock, &len);
    printf("Server: %s", buffer);
    if(strncmp(buffer, "EXIT", 4) == 0) /** 退出请求 */
    {
        puts("Bye!");
        close(fd);
        break;
    }
}
return(0);
```

首先启动服务器（参见列表 3.8b），然后在在另一台机器上启动客户端（参见列表 3.8a）。为了告诉客户端服务器运行的位置，请在启动客户端时在命令行中包含服务器的 `IP` 地址。

在 `IP` 为 `10.0.0.2` 的服务器上：

- `server` [注意 > 符号表示命令行提示符。]

在 `IP` 为 `10.0.0.1` 的客户端上：

- `client 10.0.0.2`

以你处理列表 3.6 或列表 3.7 时相同的方式与客户端交互。在服务器机器上查看来自服务器的响应。以下是你可能会看到的内容。如所示，在服务器或客户端列上执行第 1 到 5 步：

```
10.0.0.2
10.0.0.1
```

- 1) > server
- 2) > client 10.0.0.2
- 3) 输入消息: Hello there, server!
- 4) Server: Hello there, server!
- 5) 输入消息: （以此此类推。输入 "EXIT" 结束会话）

列表 3.8a 和 3.8b 中的程序是独立的客户端和服务器程序。它们使用 `UDP` 进行通信，就像列表 3.6 中的结合形式一样，但它们跨网络从一台机器通信到另一台。（同样，列表 3.9a 和 3.9b 是使用 `TCP` 的列表 3.7 网络对应版本）。检查这两组程序之间的差异，以及在自己的机器之外通信时需求的整体差异。如既往，我们鼓励你进行实验。对于“如果我这样做会怎么样？”最快的回答通常是：“试试看！”

### 列表 3.9A 向远程服务器发送 TCP 数据包

```c
#include <netinet/in.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <string.h>
#include <netdb.h>
#include <stdio.h>
#define PORT 4321
```

```c
main(argc, argv)
char *argv[];
int argc;
/*
** Listing3.9a.c - 向远程服务器发送 TCP 数据包
 */
{
  struct sockaddr_in sock;
  struct hostent *hp;
  int port = PORT;
  int fd;
  char buffer[80];
/* 服务器 */
if(argc < 2)
{
    printf("\n\t用法: %s <IP_Addr>\n\n", argv[0]);
    exit(-1);
}
```

```c
/* 获取远程服务器的关键信息 */
strncpy(buffer, argv[1], sizeof(buffer));
if((hp == gethostbyname(buffer)) == NULL)
{
    perror("client: gethostbyname()");
    exit(-1);
}
```

```c
/* 初始化 TCP 流套接字结构 */
if((fd = socket(AF_INET, SOCK_STREAM, 0)) < 0)
{
    perror("client: socket()");
    exit(-1);
}
```

```c
memset((char *) &sock, 0, sizeof(sock));
memcpy(&sock.sin_addr, hp->h_addr, hp->h_length);
sock.sin_family = hp->h_addrtype;
sock.sin_port = htons(port);
```

```c
/* 连接到远程服务器 */
if(connect(fd, (struct sockaddr *) &sock, sizeof(sock)) < 0)
{
    perror("client: connect()");
    exit(-1);
}
```

```c
/* 将交互式用户输入的消息发送到子子任务 */
while(1)
{
    printf("\n输入消息: ");
    fflush(stdout);
    fgets(buffer, sizeof(buffer), stdin);
    if(send(fd, buffer, strlen(buffer)+1, 0) < 0)
    {
        perror("parent: send()");
        exit(-1);
    }
```
