
如果找不到匹配输入参数的服务条目，该函数返回一个 `NULL` 指针。否则，返回指向包含信息（例如服务名称）的结构指针。

> **注意**
>
> `getservbyport(3)` 返回的指针仅在下次调用同一函数之前有效。

### 查阅 /etc/protocols 文件

早先，在表 7.1 中，曾提到那里使用的协议必须出现在 `protocols(5)` 表中。文本文件 `/etc/protocols` 充当各种定义的 Internet 协议值的迷你数据库。有一组函数，其工作方式与刚刚介绍的服务条目函数非常相似。如果你需要的话，这些可以作为便利函数使用。事实上，这些函数非常相似，以至于不需要详细讨论。`getprotoent(3)` 的函数原型如下：

```c
#include <netdb.h>

struct protoent *getprotoent(void);
```

`getprotoent(3)` 函数每次调用返回一个 `/etc/protocols` 条目。当遇到文件末尾或错误时，返回一个 `NULL` 指针。清单 7.4 显示了由该函数调用返回的 `protoent` 结构。

> **注意**
>
> `getprotoent(3)` 返回的指针仅在下次调用同一函数之前有效。

![](img/961a0296fe36074690a9847b79332eff_186_0.png)

### 清单 7.4：struct protoent 结构

```c
struct protoent {
  char    *p_name; /* official protocol name */
  char    **p_aliases;   /* alias list */
  int     p_proto;   /* protocol number */
}
```

结构成员更完整的描述如下：

- 结构成员 `p_name` 包含指向 C 字符串的指针，该字符串为协议命名（例如“tcp”）。

- 成员 `p_aliases` 是 C 字符串指针数组的指针，其中最后一个条目是 `NULL` 指针。如果 `pp` 指向此结构，则 `pp->p_aliases[0]` 包含第一个 C 字符串（或者在没有别名时为 `NULL`）。别名的一个例子可能是“TCP”（协议的大写名称通常被指定为别名）。

- 成员 `p_proto` 包含协议号。例如，`/etc/protocols` 中条目“tcp”找到的协议号应与 C 宏常量 `IPPROTO_TCP` 一致。如果你查看 `/usr/include/netinet/in.h` 和 `/etc/protocols` 中的值，你会发现它们确实都具有值 6。

> **注意**
>
> 在 Linux 下，`getprotoent(3)` 函数存在与 `getservent(3)` 函数相同的缺陷。即使在调用 `getprotoent(3)` 之前将 `errno` 的值置零，当到达文件末尾并由 `NULL` 返回指针指示时，Red Hat Linux 6.0 的 `errno` 值为 `ENOENT`。
>
> 在其他 UNIX 操作系统中，如 HP-UX 10.2 和 Sun Solaris 5.5.1，当返回文件末尾时，`errno` 值保持为零。这使作者推测此行为是一个 bug，可能会在 Linux 的后续版本中得到修复。

当到达文件末尾或遇到错误时，`getprotoent(3)` 函数返回 `NULL` 指针。

清单 7.5 显示了一个演示程序，它遍历 `/etc/protocols` 数据库的所有条目。

### 清单 7.5：protoent.c——getprotoent(3) 演示程序

```c
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

### 清单 7.6：编译和运行 protoent.c 程序

```bash
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

```c
#include <netdb.h>

void setprotoent(int stayopen);
```

此函数接受一个参数 `stayopen`，它被解释为布尔值：

- 当 `stayopen` 非零（TRUE）时，表示隐式打开的文件保持打开状态，只是将文件指针回绕到文件开头。
- 当 `stayopen` 为零（FALSE）时，表示隐式打开的文件被关闭然后重新打开，实际上等同于将文件回绕。

将 `stayopen` 设置为 TRUE 可获得最佳性能。

## 使用 `endprotoent(3)` 函数

当你的程序不再需要访问 `/etc/protocols` 文件时，可以请求关闭隐式打开的文件。这对于服务器程序尤为重要，因为文件描述符通常非常稀缺。`endprotoent(3)` 的函数原型如下：

```c
#include <netdb.h>

void endprotoent(void);
```

此函数没有参数，也没有返回值或错误需要检查。

## 按名称查找协议

有时，应用程序或实用程序需要处理多种协议，必须通过名称查找协议。虽然可以使用前面的函数来实现，但 `getprotobyname(3)` 可以节省程序员的工作量。该函数的原型如下：

```c
struct protoent *getprotobyname(const char *name);
```

唯一的输入参数是一个 C 字符串，包含协议名称（例如 “udp”）。返回值是指向 `protoent` 结构的指针，或者是 `NULL` 指针，表示未找到该协议。

> **注意**
>
> `getprotobyname(3)` 返回的指针仅在下一次调用同一函数之前有效。

## 按编号查找协议

当应用程序已知协议号，并且需要以人类可读的方式显示它时，使用 `getprotobynumber(3)` 例程。该函数的原型如下：
