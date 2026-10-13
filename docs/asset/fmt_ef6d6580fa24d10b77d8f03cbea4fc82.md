
`dup()` 和 `dup2()` 系统调用复制文件描述符。`dup()` 返回一个新的描述符（最小使用的描述符）。`dup2()` 允许指定要返回的描述符值，必要时关闭 `newfd`；这通常用于重新打开或重定向文件描述符。

```c
#include <unistd.h>
```

```c
int dup(int oldfd)
dup2(int oldfd, int newfd);
```

`dup()` 和 `dup2()` 返回新描述符，或返回 -1 并设置 `errno`。新旧描述符共享文件偏移量（位置）、标志和锁，但不共享 close-on-exec 标志。

## 系统编程

第 II 部分

### 列表 9.1 续

```c
print_line(int n)
{
    char buf[32];
    printf(buf,sizeof(buf), "Line #%d\n",n);
    write(1,buf, strlen(buf));
}

main(){
        int fd;

    print_line(1);
    print_line(2);
    print_line(3);

    /* 将 stdout 重定向到文件 junk.out */
    fd=open("junk.out", O_WRONLY|O_CREAT,0666);
    assert(fd!=0);
    dup2(fd,1);

    print_line(4);
    print_line(5);
    print_line(6);

    close(fd);
    close(1);
}
```

### 列表 9.2 `dup.c` 的示例运行

```
$ ./dup
Line #1
Line #2
Line #3
$ cat junk.out
Line #4
Line #5
Line #6
$
```

### `select()` 调用

`select()` 函数调用允许进程同时等待多个文件描述符，并带有可选的超时时间。只要可以对任何一个指定的文件描述符执行操作，`select()` 调用就会立即返回。这允许进程能够

## I/O 例程

第 9 章

在不派生另一个进程或启动另一个读取的情况下，执行一些基础的多任务处理。该函数及其宏的描述如下。

```c
#include <sys/time.h>
#include <sys/types.h>
#include <unistd.h>
```

```c
int select(int n, fd_set *readfds, fd_set *writefds,
fd_set *exceptfds, struct timeval *timeout);
```

```c
FD_CLR(int fd, fd_set *set);
FD_ISSET(int fd, fd_set *set);
FD_SET(int fd, fd_set *set);
FD_ZERO(int fd, fd_set *set);
```

`select()` 是可用的最复杂的系统调用之一。你可能不需要经常使用它，但当需要使用时，你可以对各种文件描述符发出大量的非阻塞读或写，但那种编程方式是 DOS 和 Windows 应用程序糟糕的原因之一；即使在没有可用的工作要做时，任务仍在运行并消耗 CPU 周期。

第一个参数是文件描述符集中文件描述符的数量（这样内核就不必浪费时间检查许多未使用的位）。第二、第三和第四个参数是文件描述符集的指针（每个文件描述符占一个位），分别指示你想要读取、写入或接收异常通知的文件描述符。最后一个参数是超时值。但所有第一个参数都可以为 NULL。返回的文件描述符集将被修改以指示已就绪，尽管对于 Linux 之外的大多数系统并非如此。返回值本身将指示描述符集中包含多少个描述符。如果为零，表示超时。如果返回值为 -1，将设置 `errno` 以指示错误（如果捕获了信号，可能包括 `EINTR`）。

宏 `FD_ZERO()`、`FD_SET()`、`FD_CLR` 和 `FD_ISSET()` 通过擦除值、设置与文件描述符对应的位、清除位或查询位来帮助操作描述符集。但所有的 `FD_ZERO()` 都将文件描述符作为第一个参数。每个宏的剩余参数都是指向文件描述符的指针。

列表 9.3 有一个粗略的终端程序，说明了 `select()` 的用法。程序没有禁用键盘的本地回显或行缓冲，没有设置串口波特率，没有锁定串口，也没有进行除两个设备之间移动字符之外的操作。如果定义了 `BADCODE` 并编译，它将在输入输出操作上旋转并占用 CPU。否则，程序将使用 `select()` 休眠直到可以执行某些 I/O。它会每十秒唤醒一次，没有任何正当理由。它限于单字符缓冲区，因此对于每个字符都会进行一次系统调用，或者在可能一次性处理多个字符时进行处理。我的 `manyterm` 程序也说明了 `select()` 的用法。

### 列表 9.3 基于 select 的终端程序
