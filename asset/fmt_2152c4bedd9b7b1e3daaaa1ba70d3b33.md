
```c
1: /* af_x25.c:
2:  *
3:  * X.25 Socket Address Example:
4:  *
5:  */
6: #include <stdio.h>
7: #include <unistd.h>
8: #include <stdlib.h>
9: #include <errno.h>
10: #include <string.h>
11: #include <sys/types.h>
12: #include <sys/socket.h>
13: #include <linux/x25.h>
14:
15: /*
16:  * This function reports the error and
17:  * exits back to the shell:
18: */
19: static void
20: bail(const char *on_what) {
21:     perror(on_what);
22:     exit(1);
23: }
24:
25: int
26: main(int argc, char **argv, char **envp) {
27:     int z;              /* Status return code */
28:     int sock_x25;      /* Socket */
29:     struct sockaddr_x25 adr_x25;  /* AF_X25 */
30:     int len_x25;       /* length */
31:     const char x25_host[]  /* X.121 addr */
32:         = "79400090";
33:
34:     /* Create an AF_X25 socket */
35:     sock_x25 = socket(AF_X25, SOCK_SEQPACKET, 0);
36:
37:     if ( sock_x25 == -1 )
38:         bail("socket()");
39:
40:     /* Form an AF_X25 Address */
41:     adr_x25.sx25_family = AF_X25;
42:     strcpy(adr_x25.sx25_addr.x25_addr, x25_host);
43:     len_x25 = sizeof adr_x25;
44:
45:     /* Bind the address to the socket */
46:     z = bind(sock_x25,
```

要编译列表 2.11 中的程序，请执行以下操作：

```
$ make af_x25
```

> **注意**

> 如果您的内核未编译 X.25 支持，运行列表 2.11 中的程序将不会成功。如果您想对该协议进行实验，请务必启用 X.25 支持。要启用 X.25 支持，您必须配置并重新编译您的 Linux 内核。

建立地址的代码包含以下基本步骤：

1.  在第 29 行中使用 `sockaddr_x25` 结构体定义 `adr_x25`。在第 30 行中，长度变量 `len_x25` 被定义为 `int`。

2.  在第 31 和 32 行中，定义了字符数组常量 `x25_host[]`，作为要建立连接的目标 X.25 地址。

3.  在第 41 行中，地址族被指定为 `AF_X25`。

4.  在第 42 行中，主机地址编号被复制到地址结构中，并以空字节（null byte）结尾。

5.  在第 43 行中，`sockaddr_x25` 结构的长度是适用于当前 Linux 实现的正确长度。

请注意，这次程序没有调用 `netstat(1)`。这是因为 `netstat(1)` 目前不报告 `AF_X25` 套接字。相反，示例程序使用 `cat(1)` 将 `/proc/net/x25` 的内容复制到标准输出。然而，要成功执行此操作，您必须在内核中编译了 `proc` 文件系统支持（这已是标准做法）。

> **注意**

> 通常，具有可变元素的套接字地址（如 `AF_UNIX` 地址族）需要计算变量的长度。但是，Linux 的 `AF_X25` 套接字地址实现只需要 `sizeof(sockaddr_x25)` 的固定长度。主机编号必须在 `sockaddr_x25` 结构内部以空字符结尾。

运行程序 `af_x25` 将产生如下所示的结果，详见列表 2.12。

### 列表 2.12：`af_x25` 程序的输出

```
$ ./af_x25
X.25 SOCKETS :
dest_addr  src_addr  dev lci  st vs vr  va   t  t2  t21  t22 t23 Snd-Rcv-Q inode
         79400900 7?? 000 0    0  0   0 3 200  180  180     0 0 @14172
$ 
```

在列表 2.12 的程序输出中，您可以看到主机编号 `79400900` 列在 `src_addr` 列标题下。

## 指定其他地址族

本书的范围不允许全面涵盖 Linux 支持的所有地址族。支持的协议列表每年都在变长。如果您正在寻找 TCP/IP 编程的快速入门路径，您可以跳过此部分并直接进入下一节。

在本节中，您将简要阅读几个可能对您感兴趣的其他协议。本节旨在作为通往其他感兴趣领域的路线图，如果您想进行一些探索的话。

Linux 至少还可以支持另外三个地址族。它们是：

- `AF_INET6`——IPv6，目前仍在开发中

- `AF_AX25`——业余无线电 AX.25 协议

- `AF_APPLETALK`——Linux AppleTalk 协议实现

这些协议中的每一个都要求您在内核中编译相应的支持。其中一些协议可能不是完整的实现——程序员请谨慎！不完整或实验性的协议可能会有 bug，有时甚至会导致您的系统崩溃。

> **提示**

> `AF_APPLETALK` 地址族在 `ddp(4)` 手册页中有文档说明。

列表 2.13 展示了这些其他套接字地址族的一些重要 C 结构体。这些结构体将帮助您可视化在为所选协议创建地址时必须初始化的地址组件。

### 列表 2.13：其他地址族结构体

```
/*
 * IPv6 Address (AF_INET6):
 */

struct sockaddr_in6 {
    sa_family_t sin6_family;
    uint16_t sin6_port; /* port */
    uint32_t sin6_flowinfo; /* flow info */
    struct in6_addr sin6_addr; /* IPv6 address */
};

struct in6_addr {
    union {
        uint8_t u6_addr8[16];
        uint16_t u6_addr16[8];
        uint32_t u6_addr32[4];
    } in6_u;
};

/*
* Amateur Radio AX.25 Address (AF_AX25):
*/
struct full_sockaddr_ax25 {
    struct sockaddr_ax25 fsa_ax25;
    ax25_address fsa_digipeater[AX25_MAX_DIGIS];
};

struct sockaddr_ax25 {
    sa_family_t sax25_family;
    ax25_address sax25_call;
    int sax25_ndigis;
};

typedef struct { /* 6 call + SSDI (shifted ascii) */
    char ax25_call[7];
} ax25_address;

#define sax25_uid sax25_ndigis

/*
* AppleTalk Address (AF_APPLETALK):
*/
struct sockaddr_atalk {
    sa_family_t sat_family; /* addr family */
    u_char sat_port; /* port */
    struct at_addr sat_addr; /* net/node */
};

struct at_addr {
    u_short s_net;
    u_char s_node;
};
```

完全解决初始化这些不同协议的步骤需要对底层协议本身有一定的了解。这超出了本书此时您想要完成的目标范围。

但是，如果您想进一步实验 `AF_AX25` 族，源文件 `af_ax25.c` 中还有一个可用于此目的的程序。使用本书相关网站提供的 `Makefile`，您可以按如下方式编译它：

```
$ make af_ax25
gcc -c -D_GNU_SOURCE -Wall af_ax25.c
gcc af_ax25.o -o af_ax25
$
```

> **注意**
