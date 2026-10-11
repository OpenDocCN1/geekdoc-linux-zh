
`struct khttpd_threadinfo` 表示单个线程需要处理的四个队列。为了占用 1 个（Intel）缓存行，该结构进行了填充，以避免“缓存行乒乓”效应。

```c
/**
 * struct khttpd_threadinfo
 */
struct khttpd_threadinfo
{
    struct http_request* WaitForHeaderQueue;
    struct http_request* DataSendingQueue;
    struct http_request* LoggingQueue;
    struct http_request* UserSpaceQueue;
    char    dummy[16];  /* Padding for cache-lines */
};
```

kHTTPd 可以被编译为可加载模块，也可以静态链接到内核中。静态链接到内核可提供更好的性能，因为它将位于更高效且 TLB 持久的页表映射中。

## 控制 kHTTPd

kHTTPd 守护进程通过 `/proc/sys/net/khttpd` 中的系统控制项（syscls）进行控制。以下是这些系统控制项及其描述（摘自文档）：

| 控制项 | 默认值 | 描述 |
| :--- | :--- | :--- |
| serverport | 8080 | khttpd 监听端口。 |
| clientport | 80 | 用户空间 HTTP 守护进程的端口。 |
| threads | 2 | 服务器线程数。对于小型网站，应为每个 CPU 设置一个；对于大型（活跃文件无法装入 RAM）网站，应为每个 CPU 设置两个。 |
| documentroot | /var/www | 存放文档文件的目录。 |
| start | 0 | 设置为 1 以启动 kHTTPd。（这同时会将 “stop” 重置为 0。） |
| stop | 0 | 设置为 1 以停止 kHTTPd。（这同时会将 “start” 重置为 0。） |
| unload | 0 | 设置为 1 以准备卸载 kHTTPd。 |
| sloppymime | 0 | 如果设置为 1，未知的 MIME 类型将被设置为 text/html。如果设置为 0，具有未知 MIME 类型的文件将由用户空间守护进程处理。 |
| perm_required | S_IROTH | 所需的最小权限；值请参考 man 2 stat。 |
| perm_forbid | dir+sticky+execute | 包含被禁止权限的权限掩码。（值请参考 man 2 stat。） |
| dynamic | cgi-bin .. | 字符串，如果它们是 URL 的子集，则表示动态内容。 |
| maxconnect | 1000 | 最大并发连接数。 |

## 数据结构—linux/net/structure.h

```c
#ifndef _INCLUDE_GUARD_STRUCTURE_H_
#define _INCLUDE_GUARD_STRUCTURE_H_

#include <linux/time.h>
#include <linux/wait.h>

struct http_request;

struct http_request
{
    /* Linked list */
    struct http_request *Next;

    /* Network and File data */
    struct socket *sock;
    struct file   *filp;

    /* Raw data about the file */

    int   FileLength;     /* File length in bytes */
    int   Time;          /* mtime of the file, unix format */
    int   BytesSent;     /* The number of bytes already sent */
    int   IsForUserSpace; /* 1 means let User space handle this one */

    /* Wait queue */

    wait_queue_t sleep;  /* For putting in the socket's waitqueue */

    /* HTTP request information */
    char  FileName[256]; /* The requested filename */
    int   FileNameLength; /* The length of the string representing the filename */
    char  Agent[128];    /* The agent-string of the remote browser */
    char  IMS[128];      /* If-modified-since time, rfc string format */
    char  Host[128];     /* Value given by the Host: header */
    int   HTTPVER;       /* HTTP-version; 9 for 0.9, 10 for 1.0 and above */

    /* Derived data from the above fields */
    int   IMS_Time;      /* if-modified-since time, unix format */
    char  TimeS[64];     /* File mtime, rfc string representation */
    char  LengthS[14];   /* File length, string representation */
    char  *MimeType;     /* Pointer to a string with the mime-type
                           based on the filename */
    __kernel_size_t MimeLength; /* The length of this string */
};

/*
struct khttpd_threadinfo represents the four queues that 1 thread has to deal with.
It is padded to occupy 1 (Intel) cache-line, to avoid "cacheline-pingpong".
*/

struct khttpd_threadinfo
{
    struct http_request* WaitForHeaderQueue;
    struct http_request* DataSendingQueue;
    struct http_request* LoggingQueue;
    struct http_request* UserSpaceQueue;
    char dummy[16]; /* Padding for cache-lines */
};

#endif
```

# 第 9 章：Linux 系统调用

本章将帮助您了解 Linux 中系统调用的动态机制。除非另有说明，当提及代码段时，我指的是 2.3.52（即将发布的 2.4）系列内核。

回顾几个广义术语：

- **内核**是运行在保护模式下的操作系统软件，并可以访问硬件的特权寄存器。
- 一些操作系统采用**微内核架构**，其中设备驱动程序和其他代码按需加载和执行，并不一定始终存在于内存中。
- 相比之下，**单片式架构**在 UNIX 实现中更为常见。诸如 BSD 的经典设计就采用了这种架构。

Linux 内核是一个主要采用单片式架构的内核：所有设备驱动程序都是内核本体的组成部分。与 BSD 不同，Linux 内核的设备驱动程序可以是可加载的，即可以通过用户命令将它们从内存中加载和卸载。内核并不是一个在系统上运行的独立进程。它是操作系统的核心，通过控制进程调度以实现多任务处理，并提供一组始终驻留在内存中的例程，供所有用户空间进程访问。

内核还包含实现用户程序与硬件设备之间接口的例程、虚拟内存的换入换出、文件管理以及系统的许多其他方面。为了实现所有这些功能，可以通过多种方式从用户空间代码调用内核例程。利用内核的一种直接方法是进程执行系统调用。共有 116 个系统调用；关于这些调用的文档可以在 man(2) 手册页中找到。

## IA32 上的系统调用与事件类别

因此，系统调用是运行中的任务向内核提出的请求，要求内核代表其提供某种服务。一般而言，由系统调用调用的内核服务构成了硬件与用户空间程序之间的抽象层，允许程序员实现操作环境，而无需将其程序过于特定地针对某一种品牌或精确的特定系统硬件组件组合进行定制。系统调用还在编程语言之间起到这种通用化作用；例如，`read` 系统调用将从文件描述符读取数据。对程序员来说，这看起来像另一个 C 函数，但实际上 `read` 的代码包含在内核中。IA32 CPU 识别两类需要处理器特别关注的事件：中断和异常。两者都会导致强制上下文切换到一个新的过程或任务。

## 中断

关于中断的详细论述，请查看第 3 章“内核基本功能”。中断可能在程序执行过程中的意外时刻发生，它们用于指示硬件需要处理器关注。当硬件设备发出中断时，中断处理程序位于内核中。IA32 识别两种中断源：可屏蔽中断，其向量由硬件确定；以及不可屏蔽中断（NMIs）。

## 异常

异常要么由处理器检测，要么由软件发出（抛出）：当过程或方法遇到其自身无法处理的异常条件（*异常条件*）时，它可能会抛出一个异常。两种类型的异常都会由放置在线程的过程或方法调用堆栈上的处理例程（*异常处理程序*）*捕获*——即调用过程或方法，或者如果该过程或方法不包含处理异常条件的代码，则是其调用过程或方法，依此类推。如果您程序中的某个线程抛出了一个异常，而没有任何过程（或方法）捕获它，那么该线程将终止。

异常向调用过程指示已经发生了一种非正常（但不一定罕见）的情况；例如，当一个方法以无效参数被调用时。当您抛出一个异常时，您正在执行一种结构化的“跳转”，从程序中检测到非正常条件的地方跳转到可以处理该条件的地方。异常处理程序应根据其能够处理的错误范围之广，部署在程序模块级别，以便尽可能减少异常处理器的数量

