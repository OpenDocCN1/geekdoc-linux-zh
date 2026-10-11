
```c
if (strncmp(buffer, "EXIT", 4) == 0)    /* 退出请求 */
{
    close(fd);
    break;
}
}
close(fd);
return(0);
```
### 列表 3.9B 从远程客户端打印 TCP 数据包

```c
#include <netinet/in.h>
#include <sys/socket.h>
#include <netdb.h>
#include <stdio.h>
#define PORT 4321
```

```c
main(void)
/*
** Listing3.9b.c - 从远程客户端打印 TCP 数据包
 */
{
    struct sockaddr_in sock;
    int len=sizeof(sock);
    struct hostent *hp;
    int port = PORT;
    int acc, soc;
    char buffer[80];
    /* 创建服务器套接字以接受连接 */
    if((acc = socket(AF_INET, SOCK_STREAM, 0)) < 0)
    {
        perror("server: socket()");
        exit(-1);
    }
```

### 列表 3.9B 续

```c
memset((char *)sock, 0, sizeof(sock));
sock.sin_addr.s_addr = htonl(INADDR_ANY);
sock.sin_port = htons(port);
sock.sin_family = AF_INET;
if(bind(acc, (struct sockaddr *) &sock, sizeof(sock)) < 0)
{
    perror("server: bind()");
    exit(-1);
}
/* 监听 */
if(listen(acc, 5) < 0)
{
    perror("server: listen()");
    exit(-1);
}
/* 接受连接 */
if((soc = accept(acc, (struct sockaddr *) &sock, &len)) < 0)
{
    perror("server: accept()");
    exit(-1);
}
/* 将从客户端接收的消息回显给用户 */
while(1) {
    recvfrom(fd, buffer, sizeof(buffer), 0,
        (struct sockaddr *) &sock, &len);
    printf("Server: %s", buffer);
    if(strncmp(buffer, "EXIT", 4) == 0) /* 退出请求 */
    {
        puts("Bye!");
        close(fd);
        break;
    }
}
close(fd);
return(0);
```

### 列表 3.9C 继续

```c
log = fopen("/tmp/log", "w");
/* echo messages received from client into log file */
while(1) {
    read(0, buffer, sizeof(buffer));
    printf(log, "Service: %s", buffer);
    if(strncmp(buffer, "EXIT", 4) == 0) { /* exit request */
        puts("Bye!");
        break;
    }
}
close(log);
return(0);
}
```

当然，便利也是有代价的：你必须更改两个 inet 配置文件。这些文件归 `root` 所有，因此你必须拥有 `root` 身份才能修改它们。

请将以下行添加到 `/etc/services` 文件的末尾，按端口号的顺序排列：

| tcpsvc | 4321/tcp | # Linux 集群架构 TCP 服务示例 |
| udpsvc | 5678/tcp | # Linux 集群架构 UDP 服务示例 |

当你检查 `/etc/services` 文件的内容时，可能会发现较低的端口号与常用的远程服务相关联。如果没有约定的端口号，Telnet 和 FTP 服务将无法供公众使用。这些被称为“周知端口”。一些较高的数字（例如用于商业服务器软件包、Web 服务器和数据库服务器）会发布它们的端口号以保留供自己使用。通常情况下，使用 4096 以上的空闲端口号是安全的。

同样，请将以下部分添加到 `/etc/inetd.conf` 文件中：

```text
#
## Linux 集群架构 TCP 和 UDP 服务示例
#
tcspsvc stream tcp nowait nobody
/home/user/bin/Listing.3.9c Listing.3.9c
```

## 自动启动远程服务器

`udpsvc stream udp nowait nobody`
➜`home/user/bin/Listing3.8c Listing3.8c`

# 现在输入

> `killall -HUP inetd`

以 `root` 身份运行，并执行与你在测试列表 3.8a、3.8b 以及列表 3.9a 和 3.9b 中的程序时使用的相同的客户端命令。

然而，你不会在远程服务器的屏幕上看到消息回显，因为标准输出流被 `inetd` 重置，以表示返回客户端的通信路径。你发送的消息保存在 `/tmp/log` 日志文件中，可以列出该文件以确保一切符合预期。

- > `cat /tmp/log`

`cat` 命令是 `concatenate`（在本例中指到输出流）的缩写，用于在屏幕上列出文件内容。

> 提示
如果你没有 `/etc/inetd.conf` 文件，你的 Linux 版本可能在使用 `xinetd` 而不是传统的 `inetd`。在这种情况下，请编辑每个文件中输入的两行，并以 `root` 身份在 `/etc/rc.d/init.d/` 下创建两个小文件，分别命名为服务 `Listing3.8c` 和 `Listing3.9c`。例如，在 `/etc/rc.d/init.d/Listing3.9c` 文件中：

```text
service Listing3.9c
{
    port        = 4321
    socket_type = stream
    protocol    = tcp
    wait        = no
    user        = nobody
    server      = /home/user/bin/Listing3.9c
    only_from   = 10.0.0.0
    disable     = no
}
```
