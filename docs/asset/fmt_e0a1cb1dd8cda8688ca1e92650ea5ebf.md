
`int fd = 1;`                        /* 文件描述符：标准输出 */

`FD_ZERO(&fdset1);`                 /* 初始化 fdset1 */

`FD_SET(fd, &fdset1);`               /* 将文件描述符添加到 fdset1 */

可以使用 `FD_CLR()` 宏从集合中移除文件描述符。要从 `fdset1` 中移除 `fd`，你可以写：

```
FD_CLR(fd,&fdset1);      /* 从 fdset1 中移除 fd */
```

有时有必要测试特定的文件描述符是否是集合的成员。这是使用 `FD_ISSET()` 宏完成的。以下测试用于检查文件单元 2（标准错误）是否为 `fdset1` 的成员：

```
if ( FD_ISSET(2,&fdset1)) {
    puts("Standard error (unit 2) is part of fdset1");
} else {
    puts("Standard error (unit 2) is not in fdset1");
}
```

如果文件单元 2 是集合 `fdset1` 的成员，则调用 `FD_ISSET(2,&fdset1)` 将返回非零值。

## timeval 结构体

使用 `select(2)` 函数另一个重要元素是可以指定超时参数。这通过使用 `timeval` 结构体指定：

```
#include <sys/time.h>
struct timeval {
    long tv_sec;      /* 秒 */
    long tv_usec;     /* 微秒 */
};
```

下面的示例显示了如何定义 1.25 秒的超时值：

```
struct timeval timeout;      /* 1.25 秒超时 */
timeout.tv_sec = 1;           /* 1 秒 */
timeout.tv_usec = 250000;     /* 0.25 秒 */
```

虽然计时值建议了一个非常精确的超时值，但 UNIX 系统可能并不那么准确。实际使用的精度可能低至 .01 秒。随着 CPU 技术的提高，精度通常随之提高。

## select(2) 函数

`select(2)` 函数是你一直努力开发的。这里是它的函数提要：

```
#include <sys/types.h>
#include <sys/time.h>
#include <unistd.h>
select(int nfds,                /* 文件描述符数量 */
       fd_set *readfds,          /* 读取描述符集 */
       fd_set *writefds,         /* 写入描述符集 */
       fd_set *exceptfds,        /* 异常描述符集 */
       struct timeval *timeout);  /* 超时值 */
```

参数 `timeout` 表明 `select(2)` 何时放弃并返回 0。0 表示没有发生感兴趣的事件。如果你不需要超时，参数 `timeout` 应该是空指针。这会导致 `select(2)` 永远等待，除非捕获到信号，在这种情况下错误为 `EINTR`。

如果提供了超时时间，但成员指示出的总时间为 0 秒，则 `select(2)` 将立即返回，而不挂起程序的执行。这允许调用者在不挂起程序的情况下轮询多个文件描述符以获取感兴趣事件。

描述符 `readfds` 指定了调用进程想要读取的所有文件描述符。例如，如果你的程序期望标准输入（文件描述符 0）上的输入，并且单元 3 上有一个打开的 FIFO，那么 `readfds` 将包含描述符 0 和 3。这会命令 `select(2)` 函数阻塞你的调用进程的执行，直到这些文件描述符中的一个或多个到达输入。

当控制权返回你的进程时，你就可以测试集合 `readfds` 以查看哪些文件描述符有可用输入。例如：

```
if ( FD_ISSET(2,&fdset1)) {
    puts("Standard error (unit 2) is part of fdset1");
} else {
    puts("Standard error (unit 2) is not in fdset1");
}
```

如果文件单元 2 是集合 `fdset1` 的成员，则调用 `FD_ISSET(2,&fdset1)` 将返回非零值。

`select(2)` 的返回值是之一：
- `-1`，如果发生错误
- `0`，如果没有发生事件
- 大于 `0`，如果至少有一个文件描述符已就绪

## 异常事件

异常事件由一组单独的文件描述符集合选择。异常事件包括：

- 在套字上接收到带外数据（out-of-band data）
- 伪终端发生某些条件
- 在套字上接收到辅助错误数据

所有这些条件都不在本章的范围内。这些特殊事件不归类为读或写事件。

## 使用 select(2) 函数

列表 16.2 中的程序创建了一个管道到两个 shell 进程，这两个进程将列出目录。一个进程的输出被转换为大写，另一个被转换为小写，以便于区分。由于一个或两个进程可能都有输出准备好供当前进程处理，`select(2)` 函数可以提供帮助。

列表 16.2 `select.c`—一个使用 `select(2)` 的程序

```c
/* select.c */
#include <stdio.h>
#include <stdlib.h>
#include <stdarg.h>
#include <unistd.h>
#include <fcntl.h>
#include <errno.h>
#include <string.h>
#include <sys/types.h>
#include <sys/time.h>
#include <sys/stat.h>

static void
quit(int rc,const char *fmt,...) {
va_list ap;
if ( errno != 0 ) /* Report错误 */
fprintf(stderr,"%s",strerror(errno));
va_start(ap,fmt); /* 化错误消息 */
vprintf(stderr,fmt,ap);
va_end(ap);
fputc('\n',stderr);
exit(rc); /* 用返回码退出 */
}

int
main(int argc,char **argv) {
int z; /* 普通状态码 */
int f1; /* 打开 fifo 1 */
int f2; /* 打开 fifo 2 */
fd_set rxset; /* fd 集合 */
int nfds; /* 文件描述符数量 */
struct timeval tv; /* 超时 */
char buf[200+1]; /* I/O 缓冲区 */
FILE *p1, *p2; /* 来自 popen(3) 的管道 */

/*
* 管道 :
*/
if (!p1 = popen('ls -l|tr '[a-z]' '[A-Z]','r')) {
    quit(1,'popen(3) p1 失败');
}
if (! (p2 = popen('ls -l|tr '[A-Z]' '[a-z]' & sleep 8,'r'))) {
    quit(1,'popen(3) p2 失败');
}
/*
* 获取底层文件描述符 :
*/
f1 = fileno(p1);
f2 = fileno(p2);
printf("BEGIN: f1=%d,f2=%d\n",f1,f2);
/*
* 进入 select 循环 :
*/
do {
    FD_ZERO(&rxset);      /* 清空集合 */
    if (f1 > 0) {
        FD_SET(f1,&rxset);   /* 检查 f1 */
    if (f2 > 0) {
        FD_SET(f2,&rxset);   /* 检查 f2 */
    }
    nfds = f1 > f2 ? f1 : f2 + 1;
    tv.tv_sec = 3;          /* 3 秒 */
    tv.tv_usec = 500000;    /* 0.5 秒 */
    do {
        z = select(nfds,&rxset,0,0,tv);
    } while (z == -1 && errno == EINTR);
    if (z == -1) {/* 错误? */
        quit(13,'select(2)');
    }
    if (z == 0) {
        printf("TIMEOUT: f1=%d,f2=%d\n",f1,f2);
        continue;
    }
    /*
    * 如果 f1 或 f2 有数据可读
    * 控制权在这里。
    */
    if ( f1 >= 0 && FD_ISSET(f1,rxset)) {
        z = read(f1,buf,sizeof buf-1);
        if (z == -1)
            quit(6,"read(2) of f1.");
        if (z > 0)
            printf("%d bytes from f1\n",z);
        else
            puts("READ EOF");
    }
    if (f2 >= 0 && FD_ISSET(f2,rxset)) {
        z = read(f2,buf,sizeof buf-1);
        if (z == -1)
            quit(6,"read(2) of f2.");
        if (z > 0)
            printf("%d bytes from f2\n",z);
        else
            puts("READ EOF");
    }
} while (f1 >= 0 || f2 >= 0);
puts("select.");
return 0;
}
```
