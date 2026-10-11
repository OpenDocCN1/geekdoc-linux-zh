

## 清单 7.5：protoent.c——getprotoent(3) 演示程序

```
/* protoent.c:  
   *
   * 示例 getprotoent(3) 程序：  
   */  

#include <stdio.h>  
#include <unistd.h>  
#include <stdlib.h>  
#include <errno.h>  
#include <string.h>  
#include <netdb.h>  

int  
main(int argc, char **argv) {  
    int x;  
    struct protoent *pp;  
    
    for (;;) {  
        errno = 0;  
        if ( !(pp = getprotoent()) )  
            break;  
        
        printf("%s:\n"  
            "\tProtocol: %d\n"  
            "\tAliases: ",  
            pp->p_name,  
            pp->p_proto);  
        for ( x=0; pp->p_aliases[x] != NULL; ++x )  
            printf("%s ", pp->p_aliases[x]);  
        putchar('\n');  
    }  
    if ( errno != 0  
        &&  errno != ENOENT )  /* 针对 RH-6.0 */  
        fprintf(stderr,  
            "%s: getprotoent(3) %d\n",  
            strerror(errno), errno);  
        
    return 0;  
}
```

清单 7.5 中的程序代码与清单 7.2 中的程序非常相似，因此这里只需要重复说明基本步骤。它们是：

- 调用 `getprotoent(3)` 从 `/etc/protocols` 文件中获取一个条目。
- 打印协议名称和协议号。
- 在内部循环中，如果存在别名，则打印所有的协议别名。
- 重复步骤 1，直到没有更多的协议条目为止。

清单 7.6 展示了如何编译和运行该演示程序。

## 清单 7.6：编译和运行 protoent.c 程序

```
$ make protoent
gcc -o -D.gnu_SOURCE -Wall protoent.c
gcc protoent.o -o protoent
$ ./protoent | head

ip:
	Protocol:	0
	Aliases:	IP
icmp:
	Protocol:	1
	Aliases:	ICMP

igmp:
	Protocol:	2
	Aliases:	IGMP
```

![](img/961a0296fe36074690a9847b79332eff_188_0.png)

清单 7.6 中的示例命令会话将输出管道传输到 `head` 命令，以保持列表简短。注意，第一个显示条目的协议名称为 “ip”，其唯一的大写别名是 “IP”。

## 使用 `setprotoent(3)` 函数

`getprotoent(3)` 隐式打开的文件可以通过调用 `setprotoent(3)` 函数进行重新绑定。该函数的原型如下：

```
#include <netdb.h>

void setprotoent(int stayopen);
```

此函数接受一个参数 `stayopen`，它被解释为布尔值：

- 当 `stayopen` 非零（TRUE）时，表示隐式打开的文件保持打开状态，只是将文件指针回绕到文件开头。
- 当 `stayopen` 为零（FALSE）时，表示隐式打开的文件被关闭然后重新打开，实际上等同于将文件回绕。

将 `stayopen` 设置为 TRUE 可获得最佳性能。

## 使用 `endprotoent(3)` 函数

当你的程序不再需要访问 `/etc/protocols` 文件时，可以请求关闭隐式打开的文件。这对于服务器程序尤为重要，因为文件描述符通常非常稀缺。`endprotoent(3)` 的函数原型如下：

```
#include <netdb.h>

void endprotoent(void);
```

此函数没有参数，也没有返回值或错误需要检查。

## 按名称查找协议

有时，应用程序或实用程序需要处理多种协议，必须通过名称查找协议。虽然可以使用前面的函数来实现，但 `getprotobyname(3)` 可以节省程序员的工作量。该函数的原型如下：

```
struct protoent *getprotobyname(const char *name);
```

唯一的输入参数是一个 C 字符串，包含协议名称（例如 “udp”）。返回值是指向 `protoent` 结构的指针，或者是 NULL 指针，表示未找到该协议。

> **注意**
> 
> `getprotobyname(3)` 返回的指针仅在下一次调用同一函数之前有效。

## 按编号查找协议

当应用程序已知协议号，并且需要以人类可读的方式显示它时，使用 `getprotobynumber(3)` 例程。该函数的原型如下：

```
#include <netdb.h>

struct protoent *getprotobynumber(int proto);
```

此函数接受协议号作为输入参数，如果找到匹配项，则返回指向 `protoent` 结构的指针。否则，返回 NULL 指针，表示该协议未被小型数据库识别。例如，如果输入参数为 6（或 C 宏常量 `IPPROTO_TCP`），则应返回一个结构指针，其成员 `p_name` 的值为 “tcp”。

> **注意**
> 
> `getprotobyname(3)` 返回的指针仅在下一次调用同一函数之前有效。

至此，`getservent(3)` 和 `getprotoent(3)` 函数族的介绍到此结束。现在既然知道了如何查找与 Internet 相关的服务和协议，是时候编写一个基于连接的 TCP/IP 客户端程序了。

## 编写 TCP/IP 客户端程序

使用 TCP/IP 进行成对套接字的连接需要采用与上一章使用 UDP 协议时略有不同的过程。从客户端程序的角度来看，必须执行以下一般步骤：

1. 创建套接字。
2. 可选地绑定套接字（以限制将使用哪个接口，或显式指示一个通配套接字地址）。
3. 连接到远程套接字（客户端连接到服务器）。
4. 通过读写进行通信。
5. 关闭或封闭套接字。

在使用 UDP 协议时，你执行了上述所有步骤，除了步骤 3。因为你使用的是无连接协议，所以从未需要连接到任何东西。下一节将向你介绍一个新的套接字函数。

### 介绍 `connect(2)` 函数

为了建立套接字连接，你需要调用 `connect(2)` 函数。其函数原型如下：

```
#include <sys/types.h>
#include <sys/socket.h>

int connect(int sockfd, struct sockaddr *serv_addr, int addrlen);
```

此函数接受三个参数。它们是：

1. 由先前对 `socket(2)` 的调用返回的套接字文件描述符 `sockfd`。
2. 程序要连接的服务器地址 `serv_addr`。
3. 服务器地址的长度 `addrlen`（以字节为单位）。

服务器地址和服务器地址长度与如果你使用 UDP 时在调用 `sendto(2)` 函数时提供的套接字地址值相同。然而，与面向连接的协议的区别在于，你只建立一次目标地址。在此函数成功之后，所有后续的通信都将针对此处寻址的套接字。

当函数调用成功时，返回值为零。否则，返回 -1 表示发生错误，错误的性质记录在变量 *errno* 中。

## 准备编写客户端程序

为了保持客户端程序简短并让你专注于基本原理，演示程序将连接到你的系统上正在运行的现有服务。客户端程序将连接到你的 daytime 服务以获取当前的日期和时间字符串。

在展示程序之前，你应该确保该服务在你的系统中已启用并正常运行。作为第一步，执行以下操作：

![](img/961a0296fe36074690a9847b79332eff_191_0.png)

```
$ grep daytime /etc/services
daytime 13/tcp
daytime 13/udp
$
```

你应该看到你的系统识别 daytime Internet 服务，并且它通过 tcp 在端口 13 上可用。`grep` 输出的第一行证实了这一点。

## 提示

> telnet 程序通常可用于对 TCP/IP 服务器进行简单测试。但是，切记要在命令行中的 IP 号码（或主机名）后指定端口号非常重要。否则，端口号将默认为 23，这是 telnet 服务的端口！
> 
> 例如，要测试 daytime 服务，你必须在命令行中的 IP 号码后指定端口号 13。

下一步是确保其正在运行。*telnet 程序*是一个在使用 *TCP/IP* 时通常可用于简单测试的程序。要测试 daytime 服务是否正在运行，你应该能够执行以下操作：

![](img/961a0296fe36074690a9847b79332eff_191_1.png)

```
$ telnet 127.0.0.1 13
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
Tue Aug 17 17:59:30 1999
```

