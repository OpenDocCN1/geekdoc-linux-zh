


```c
    printf("release = %s\n",  info.release);
    printf("version = %s\n",  info.version);
    printf("machine = %s\n",  info.machine);
    exit(EXIT_SUCCESS);

    EC_CLEANUP_BGN
        exit(EXIT_FAILURE);
    EC_CLEANUP_END
}
```

下面是我们在四个测试系统上运行此程序得到的输出$^9$；看看你能否发现其中的规律：

```
sysname = SunOS
nodename = sol
release = 5.8
version = Generic_108529-13
machine = i86pc
```

```
sysname = Darwin
nodename = Marc-Rockhinds-Computer.local.
release = 6.6
version = Darwin Kernel Version 6.6: Thu May  1 21:48:54 PDT 2003;
    root:xnu/xnu-344_34.obj-1/RELEASE_PPC
machine = Power Macintosh
```

```
sysname = FreeBSD
nodename = bsd.MSHOME
release = 4.6-RELEASE
version = FreeBSD 4.6-RELEASE #0: Tue Jun
machine = i386
```

```
sysname = Linux
nodename = suse2
release = 2.4.18-4GB
version = #1 Wed Mar 27 13:57:05 UTC 2002
machine = i686
```

## 8.8.2 网络函数

此类别中的函数用于获取本地机器可能连接到的网络信息。首先是三个类似主机函数（例如 `gethostent`）的函数，用于扫描网络：

### setnetent—开始扫描网络数据库

```c
#include <netdb.h>
void setnetent(
    int stayopen; /* 是否保持连接打开？ */
);
```

### getnetent—获取网络数据库条目

```c
#include <netdb.h>
struct netent *getnetent(void);
/* 返回指向 netent 的指针，或在结束时返回 NULL（未定义 errno） */
```

### endnetent—结束扫描网络数据库

```c
#include <netdb.h>
void endnetent(void);
```

### struct netent—用于网络数据库函数的结构体

```c
struct netent {
   char *n_name;        /* 正式网络名称 */
   char *n_aliases;     /* 替代网络名称数组 */
   int n_addrtype;      /* 地址族（而非类型） */
   uint32_t n_net;      /* 网络号 */
};
```

这是一个示例：

```c
static void netdb(void)
{
    struct netent *n;

    setnetent(true);
    while ((n = getnetent()) != NULL)
        display_netent(n);
    endnetent();
}

static void display_netent(struct netent *n)
{
    int i;

    printf("name: %s; type: %d; number: %lu\n", n->n_name, n->n_addrtype,
           (unsigned long)n->n_net);
    for (i = 0; n->n_aliases[i] != NULL; i++)
        printf("\t%s\n", n->n_aliases[i]);
}
```

输出如下：

```
name: loopback; type: 2; number: 127
name: arpanet; type: 2; number: 10
arpa
```

几乎所有（如果不是全部的话）机器都有一个用于测试的回环网络。这台机器（运行 Solaris 系统）还拥有一个连接到它称之为“arpanet”（为了纪念其历史）的互联网网络的连接。请记住，显示的“type”实际上是地址族；事实证明，宏 `AF_INET` 定义为 2。

与主机数据库类似，也有用于通过网络号或名称查找条目的函数：

**getnetbyname**—按名称查找网络

```c
#include <netdb.h>
struct netent *getnetbyname(
          const char *name       /* 网络名称（需匹配 n_name 成员） */
);
/* 返回指向 netent 的指针，若未找到则返回 NULL（未定义 errno） */
```

**getnetbyaddr**—按网络号查找网络

```c
#include <netdb.h>
struct netent *getnetbyaddr(
        uint32_t net,           /* 网络号（需匹配 n_net 成员） */
        int type                /* 地址族（需匹配 n_addrtype 成员） */
);
/* 返回指向 netent 的指针，若未找到则返回 NULL（未定义 errno） */
```

### 8.8.3 协议函数

按照同样的模式，扫描协议数据库的函数如下：

**setprotoent**—开始扫描协议数据库

```c
#include <netdb.h>
void setprotoent(
       int stayopen          /* 是否保持连接打开？ */
);
```

**getprotoent**—获取协议数据库条目

```c
#include <netdb.h>
struct protoent *getprotoent(void);
/* 返回指向 protoent 的指针，或在结束时返回 NULL（未定义 errno） */
```

**endprotoent**—结束扫描协议数据库

```c
#include <netdb.h>
void endprotoent(void);
```

**struct protoent**—用于协议数据库函数的结构体

```c
struct protoent {
    char  *p_name;         /* 正式协议名称 */
    char **p_aliases;      /* 替代协议名称数组 */
    int   p_proto;         /* 协议号 */
};
```

在某些系统上，调用 `setsockopt` 或 `getsockopt` 时可以使用协议号作为协议级别，但这是非标准的。

如果你一直阅读到这里，示例代码应该显而易见：

```c
static void protodb(void)
{
    struct protoent  *p;

    setprotoent(true);
    while ((p = getprotoent()) != NULL)
        display_protoent(p);
    endprotoent();
}

static void display_protoent(struct protoent *p)
{
    int i;

    printf("name: %s; number: %d\n", p->p_name, p->p_proto);
    for (i = 0; p->p_aliases[i] != NULL; i++)
        printf("\t%s\n", p->p_aliases[i]);
}
```

但是输出结果相当有趣。在 SuSE Linux 上我得到了 135 种协议。这只是输出的一部分：

```
...  
name: mobile; number: 55
       MOBILE
name: tlsp; number: 56
       TLSP
name: sktp; number: 57
       SKIP
name: ipv6-icmp; number: 58
       IPv6-ICMP
       ICMPv6
       icmprv6
       icmpr6
name: ipv6-nonxt; number: 59
IPy6-NoNxt
name: ipv6-opts; number: 60
IPv6-Opts
name: cftp; number: 62
CFTP
name: sat-expak; number: 64
SAT-EXPAK
name: krypton; number: 65
KRYPTOLAN
...
```

还有两个更可预测的函数来完善这一组：

**getprotobyname**—按名称查找协议

```c
#include <netdb.h>
struct protoent *getprotobyname(
const char *name          /* 协议名称 */
);
/* 返回指向 protoent 的指针，若未找到则返回 NULL（未定义 errno） */
```

**getprotobynumber**—按号查找协议

```c
#include <netdb.h>
struct protoent *getprotobynumber(
int proto                 /* 协议号 */
);
/* 返回指向 protoent 的指针，若未找到则返回 NULL（未定义 errno） */
```

### 8.8.4 服务函数

还有一套扫描及按名称和编号获取的函数，这次是针对服务的。这些函数扫描本地系统的 /etc/services 文件。

**setservent**—开始扫描服务数据库

```c
#include <netdb.h>
void setservent(
int stayopen          /* 是否保持连接打开？ */
);
```

**getservent**—获取服务数据库条目

```c
#include <netdb.h>
struct servent *getservent(void);
/* 返回指向 servent 的指针，或在结束时返回 NULL（未定义 errno） */
```

**endservent**—结束扫描服务数据库

```c
#include <netdb.h>
void endservent(void);
```

**struct servent**—用于服务数据库函数的结构体

```c
struct servent {
  char *s_name;  /* 正式服务名称 */
  char **s_aliases;  /* 替代服务名称数组 */
  int s_port;  /* 端口号 */
  char *s_proto;  /* 该服务的协议名称 */
};
```

**getservbyname**—按名称查找服务

```c
#include <netdb.h>
struct servent *getservbyname(
    const char *name,  /* 服务名称 */
    const char *proto  /* 协议名称 */
);
/* 返回指向 protoent 的指针，若未找到则返回 NULL（未定义 errno） */
```

**getservbyport**—按端口查找服务

```c
#include <netdb.h>
struct servent *getservbyport(
    int port,  /* 端口 */
    const char *proto  /* 协议名称 */
);
/* 返回指向 protoent 的指针，若未找到则返回 NULL（未定义 errno） */
```

我们最后的一个此类示例如下：

```c
{
  static void servdb(void)
  {
    struct servent *s;

    setservent(true);
    while ((s = getservent()) != NULL)
      display_servent(s);
    endservent();
  }

  static void display_servent(struct servent *s)
  {
    int i;
    printf("name: %s; port: %d; protocol: %s\n", s->s_name,
           ntohs(s->s_port), s->s_proto);
    for (i = 0; s->s_aliases[i] != NULL; i++)
        printf("\t%s\n", s->s_aliases[i]);
  }
}
```

输出非常大，因为 /etc/services 文件通常很大。这是一个片段：

```
...  
name: ftp-data; port: 20; protocol: tcp  
name: ftp-data; port: 20; protocol: udp  
name: ftp; port: 21; protocol: tcp  
name: ftp; port: 21; protocol: udp  
name: ssh; port: 22; protocol: tcp  
name: ssh; port: 22; protocol: udp  
name: telnet; port: 23; protocol: tcp  
name: telnet; port: 23; protocol: udp  
name: smtp; port: 25; protocol: tcp  
mail  
name: smtp; port: 25; protocol: udp  
mail  
name: nsw-fe; port: 27; protocol: tcp  
name: nsw-fe; port: 27; protocol: udp  
name: msg-icp; port: 29; protocol: tcp  
name: msg-icp; port: 29; protocol: udp  
name: msg-auth; port: 31; protocol: tcp  
name: msg-auth; port: 31; protocol: udp  
...
```

### 8.8.5 网络接口函数

有一组函数用于获取网络接口的名称及其索引号。首先，这里有一个函数以 if_nameindex 结构体数组的形式获取它们，以及一个对应的用于释放该数组的函数：

**if_nameindex**—获取所有网络接口名称和索引

```c
#include <net/if.h>
struct if_nameindex *if_nameindex(void);
/* 返回数组，或在出错时返回 NULL（设置 errno） */
```

**if_freenameindex**—释放由 if_nameindex 分配的数组

```c
#include <net/if.h>
void if_freenameindex(
struct if_nameindex *ptr /* 指向数组的指针 */
);
```


