
```c
#include <sys/time.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <assert.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <fcntl.h>
#include <signal.h>
#include <setjmp.h>
#include <sys/socket.h>
#include <netdb.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <string.h>
#include <limits.h>

#include "child.h"

int debug=5;

extern char **environ;

main(int argc, char *argv[]) {
    int count;
```

继续

## 列表 11.5 续

```c
int i;
char **newargw;
int rc;
```

```c
#if 1
    /* 非常原始的示例，借用了来自*
    /* 当前进程的所有内容 */
    if(debug==5) child_print_arg_array("argv",argv);
```

```c
    fprintf(stderr,"argc=%d\n",argc);
    assert(argc >= 2);
    /* 从 argv[1] 创建一个新的 argv[] */
    count=0;
    while(1) {
        count++;
        if(argv[count]==NULL) break;
    }
    printf("count=%d\n",count);
    newargw = malloc(sizeof(void *)(count+2));
    newargw[0] = argv[1];
    for(i=1; i<count; i++) {
        newargw[i+1] = argv[i+1];
    }
```

```c
    newargw[count] = NULL;
    printf("argv[1]=%s\n",argv[1]);
    if(debug==5) child_print_arg_array("argv",newargw);
    if(debug==5) child_print_arg_array("environ",environ);
```

```c
    fprintf(stderr,"invoking program\n");
    rc=child_pipe(argv[1], newargw, environ,
    NULL, NULL, NULL);
    fprintf(stderr,"program invocation over\n");
```

```c
    fprintf(stderr,"rc=%d\n",rc);
    if(rc<0) {
        perror("child_pipeve(");
    }
```

```c
#endif
```

### 总结

Linux 操作系统提供了多种可以用于操作进程的函数。其中大多数函数被某些甚至所有的 UNIX 及兼容操作系统所共享。

## 第 12 章 访问系统信息

作者：Mark Whitis

### 本章内容

- 进程信息 217
- 通用系统信息 221
- 库与工具 227

在过去，UNIX 程序（如 `ps` 和 `uptime`）直接访问内核数据结构来获取系统信息。这需要对内核外部符号有了解，并且需要小心以确保值在访问时不被修改。这些程序需要以 root 权限运行才能访问内核数据结构；如果编写得不当，它们就会受到安全漏洞的威胁。当内核发生时，这些程序通常需要重新编译，因为数据结构的位置和布局可能会发生变化。

一些现代系统实现了 `/proc` 文件系统，其中包含特殊文件，可以通过读取这些文件来访问系统状态信息。这些文件通常是纯文本文件。Linux 通过 `/proc` 文件系统提供的信息多许多其他系统。

`/proc` 文件系统的条目可以由任何内核模块创建。实现 `/proc` 文件系统及其某些条目的代码可以在 `/usr/src/linux/fs/proc` 中找到。proc 命名空间的部分由内核函数 `proc_register()` 注册。

本章描述的 `/proc` 文件基于运行 2.2.5 内核的系统。如果你有不同的内核版本或了创建 `/proc` 条目的驱动程序，你可能会看到不同的文件。列出的许多文件在文档中并未提及，因此我必须依靠自己的知识、内核源码、与各种工具输出的对比以及偶尔的猜测来生成描述。第 5 节的 `proc` 手册页（`man 5 proc`）提供了其中许多文件的更多信息。

我预先提醒你，本章并不包含通过 `/proc` 文件系统提供的每位信息的详尽文档。本章的文档很大程度上基于对 `proc` 内容的探索、使用该文件的程序的输出、内核源码以及……

### 进程信息

`/proc` 目录为每个运行的进程都有一个条目。每个条目以进程 ID（PID）命名。在每个目录下，都有提供进程信息的文件。

`/proc/self` 目录是当前进程的符号链接。当程序在不知道自己 PID 的情况下需要访问自身信息时，这非常有用。大多数文件都是可用的。

### cmdline 文件

读取 `/proc/$pid/cmdline` 文件返回命令行，包括名称和所有参数。如果进程被交换出，命令行可能是空的。

> 提示 你可以通过以下命令快速查看系统正在运行的内容：`strings -f /proc/*/cmdline`

### environ 文件

读取 `/proc/$pid/environ` 文件返回环境变量。单个环境变量字符串由空字节分隔，环境的结束由文件结束标记。`strings` 工具比 `cat` 工具更容易读。

### fd 目录

`/proc/$fd` 目录为每个打开的文件描述符有一个指向实际文件的符号链接条目。一个索引节点（inode）包含关于文件的信息。每个索引节点包含索引节点所在的设备、锁定信息、文件类型、文件链接、所有者的用户 ID 和组 ID、文件字节数以及文件在磁盘上的块地址。

打开文件描述符条目（例如 `/proc/self/fd/1`）会打开文件本身；如果文件是终端或其他特殊设备，可能会干扰该文件。你也可以使用 `fstat()` 或 `stat()` 系统调用来获取文件信息。文件显示的权限仅对所有者开放，所有者的读写位指示了文件的打开模式。

在许多 UNIX 系统上（无论是否有 `/proc` 文件系统）都运行一个名为 `lsof` 的实用程序。在 Red Hat 系统上，它安装在 `/usr/bin/lssof`。当你想要获取有关进程正在执行的操作的信息、知道为什么无法卸载一个被占用的文件系统，或者调查可疑活动时，这个工具非常有用。`find` 命令也用于搜索特定文件。如果你使用的是旧的发行版或没有进行完整安装，可能会缺少这些工具。

## 访问系统信息

第12章

family。许多时间相关的字段似乎是以 jiffies（1/100 秒）为单位测量的。关于是否包含计数字段似乎存在一些差异。

表 12.1 stat 字段

| # | 名称 | 描述 |
|---|---|---|
| 1 | ppid | 进程 ID |
| 2 | cmd | 括号中的命令行简单基名（如果 cmdline 为空，ps 将使用它） |
| 3 | state | R=可运行, S=睡眠, D=不可中断睡眠, T=被追踪或停止, Z=僵尸, W=未驻留, N=nice |
| 4 | ppid | 父进程 ID |
| 5 | pgrp | 进程组 ID |
| 6 | session | 进程会话 ID |
| 7 | tty | 控制 tty（主设备号，从设备号） |
| 8 | tpgid | 控制 tty 的进程 ID |
| 9 | flags | 进程标志 |
| 10 | min_flt | 次页异常 |
| 11 | cmin_flt | 次页异常（累计） |
| 12 | maj_flt | 主页异常 |
| 13 | cmaj_flt | 主页异常（累计） |
| 14 | utime | 用户时间 |
| 15 | stime | 系统时间 |
| 16 | cutie | 用户时间（累计） |
| 17 | cstime | 系统时间（累计） |
| 18 | counter | 进程下一个时间切片的大小 |
| 19 | priority | 静态调度优先级 |
| 20 | nice | 正常调度算法 nice 值（动态） |
| 21 | timeout | 以 jiffies 为单位的超时值 |
| 22 | it_real_value | 下一次间隔定时器到期的 jiffies |
