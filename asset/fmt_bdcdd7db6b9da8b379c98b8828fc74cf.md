
```c
    for (addrs = hostinfo->h_addr_list; *addrs != NULL; addrs++) {
        printf("* %s\n", inet_ntoa(*(struct in_addr *)addrs));
    }
    exit(0);
}
```

该程序调用`gethostname`从主机提取信息。它打印主机名、别名以及它拥有的 IP 地址。

```
$ getname tilde
results for host tilde:
Name: tilde
* 192.168.1.1
```

```
$ getname localhost
results for host localhost
Name: localhost
* 127.0.0.1
```

记住，如果你使用的计算机具有相同的原生字节序和网络字节序，你将看不到任何区别。始终使用转换函数仍然非常重要，以便允许与不同架构计算机上的客户端和服务器进行正确操作。

# 套接字

如果你有权限这样做，可以将你的服务器添加到`/etc/services`的已知服务列表中，这会为端口号分配一个名称，客户端可以使用符号化服务而不是数字。

同样，给定计算机的名称，你可以调用解析地址的主机数据库函数来确定 IP 地址。你通过查阅网络配置文件（如`/etc/hosts`）或网络信息服务（如 NIS（网络信息服务，以前称为黄页）和 DNS（域名系统））来实现。

主机数据库函数在接口头文件`netdb.h`中声明。

```c
## <netdb.h>
struct hostent *gethostbyaddr(const void *addr, size_t len, int type);
struct hostent *gethostbyname(const char *name);
```

这些函数返回的结构体必须包含这些成员：

```c
struct hostent {
  char *h_name;          /* 主机名称 */
  char **h_aliases;      /* 别名列表（昵称） */
  int h_addrtype;        /* 地址类型 */
  int h_length;          /* 地址的字节长度 */
  char **h_addr_list;    /* 地址列表（网络字节序） */
};
```

如果指定的主机或地址没有数据库条目，信息函数将返回一个空指针。

同样，有关服务和相关端口号的信息可以通过某些服务函数获取。

```c
#include <netdb.h>
struct server *getservbyname(const char *name, const char *proto);
struct server *getservbyport(int port, const char *proto);
```

`proto`参数指定用于连接到服务的协议，对于`SOCK_STREAM` TCP 连接使用 "tcp"，或者对于`SOCK_GRAM` UDP 数据报使用 "udp"。

`server`结构体包含这些成员：

```c
struct server {
  char *s_name;          /* 服务名称 */
  char **s_aliases;      /* 别名列表（备用名称） */
  int s_port;            /* IP 端口号 */
  char *s_proto;         /* 服务类型，通常为 "tcp" 或 "udp" */
};
```

你可以通过调用`gethostbyname`并打印结果获取关于计算机的主机数据库信息。注意，地址列表需要转换为适当的地址类型，并使用`inet_ntoa`转换从网络序转换为可打印字符串，其定义如下：

# 连接到标准服务

服务器也通过使用`INADDR_ANY`被修改为允许来自任何 IP 地址的连接。
现在，当你运行`server3`和`client3`时，你会看到本地连接所使用的正确端口。

注意地址列表需要转换为适当的地址类型，并使用`inet_ntoa`转换从网络序转换为可打印字符串，其定义如下：

```c
#include <arpa/inet.h>
char *inet_ntoa(struct in_addr in)
```

该函数将 Internet 主机地址转换为点分四位格式的字符串。在出错时返回 -1，但 POSIX 没有定义任何错误。你使用的另一个新函数是`gethostname`。

```c
#include <unistd.h>
int gethostname(char *name, int namlength);
```

此函数将当前主机的名称写入由`name`给出的字符串。主机名将以空字符终止。参数`namlength`表示字符串的长度，如果主机名太长，它将被截断。

# 第 15 章

我们现在可以修改客户端连接到任何命名的主机。而不是连接到示例服务器，我们将连接到一个标准服务，这样我们也可以演示端口号。大多数 UNIX 和某些 Linux 系统通过名为`daytime`的标准服务提供系统日期。客户端连接到此服务以发现服务器的时间和日期。这里有一个`getdate.c`程序就是执行这一点。

# 尝试——连接到标准服务

1. 使用通常的包含文件和声明。

```c
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>
#include <stdio.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
    char *host;
    int sockfd;
    int len, result;
    struct sockaddr_in address;
    struct hostent *hostinfo;
    struct servent *servinfo;
    char buffer[128];

    if (argc == 1)
        host = "localhost";
    else
        host = argv[1];
```

2. 将主机设置为参数，或者默认为`localhost`。

```c
    gethostname(myname, 256);
    host = myname;
```

3. 查找主机地址，如果没有找到则报告错误。

```c
    hostinfo = gethostbyname(host);
    if(!hostinfo) {
        fprintf(stderr, "no host: %s\n", host);
        exit(1);
    }
```

4. 检查主机上是否存在`daytime`服务。

```c
    servinfo = getservbyname("daytime", "tcp");
    if(!servinfo) {
        fprintf(stderr, "no daytime service\n");
        exit(1);
    }
    printf("daytime port is %d\n", ntohs(servinfo->s_port));
```

# 套接 (Sockets)

## 4. 创建套接。

```c
sockfd = socket(AF_INET, SOCK_STREAM, 0);
```

## 5. 构造用于`connect`的地址结构。

```c
address.sin_family = AF_INET;
address.sin_port = s_port;
address.sin_addr = *(struct in_addr *)hostinfo->h_addr_list;
len = sizeof(address);
```

## 6. 然后进行连接并获取信息。

```c
result = connect(sockfd, (struct sockaddr *)&address, len);
if(result == -1) {
    perror("oops: getdate");
    exit(1);
}

result = read(sockfd, buffer, sizeof(buffer));
buffer[result] = '\0';
printf("read %d bytes: %s", result, buffer);
close(sockfd);
exit(0);
```

你可以使用`getdate`获取任何已知主机当天的时间。

```
$ getdate localhost
daytime port is 13
```
