
# 列表 24.10 Condition variable 条件变量类

```cpp
// Listing 24.10 Condition variable 条件变量类
#if defined(c_cond_h)
#define c_cond_h

#include <thread.h>

#include "event.h"

class CondVar : public Event
{
public:
    CondVar();
    virtual ~CondVar();

    void Create();
    void Destroy();

    int Wait();
    int Signal();

private:
    CondVar& operator=(const CondVar&); // 不允许拷贝

    pthread_cond_t cond;
    pthread_condattr_t attr;

    pthread_mutex_t mutex;
    pthread_mutexattr_t matr;
};

#endif
```

列表 24.10 使用之前定义的 `Event` 接口定义了 `CondVar` 对象。线程将类似于互斥锁的方案使用 `CondVar` 变量作为同步原语。当线程访问数据时，它调用 `CondVar::Wait()` 成员函数。当它完成更新时，它通过调用 `Signal` 释放 `CondVar`。

> 将条件变量初始化为已信号状态是非常重要的，否则将会导致死锁条件。这种 `CondVar` 的实现始终将条件变量初始化为已信号状态。

## 合并 (Joining)

合并是一种同步原语，导致线程等待另一个线程完成。合并不被视为同步原语，因为合并的目的是等待另一个线程结束，而不是同时运行。

## 死锁

当你在多线程环境中进行编程时，多个线程正在竞争有限的资源。如果一个线程请求一个不可用的资源，该线程将进入等待状态。

理论上，线程可能会无限等待，因为它正在等待的资源被另一个等待的线程持有；这被称为死锁。死锁被定义为一个线程无限期阻塞，并与另一个线程竞争同一组资源。

必须存在以下四个条件才能构成死锁条件：

1.  **互斥性**——至少有一个锁是不可共享的。
2.  **持有并等待**——一个线程持有一个资源，并等待一个被另一个线程持有的资源。
3.  **非抢夺性**——持有的资源只能由拥有所有权的线程释放。
4.  **循环等待**——必须存在一组等待线程 {t0, t1, t2, ... t(n)}，其中 t0 正在等待 t1 持有的锁，t1 正在等待 t2 持有的锁，... t(n-1) 和 t(n) 正在等待 t0 持有的锁。

递归死锁是指线程尝试获取它已经拥有的资源的情况。

互斥死锁发生在两个线程获取了不同的锁，并阻塞等待另一个线程释放锁时。这也被称为致命拥抱（deadly embrace）。

## 系统编程

| 应该 (DO) | 避免 (DON'T) |
| --- | --- |
| 保护多个线程之间共享的数据，以便你的代码是重入的。 | 不要忘记在获取互斥锁后释放它。 |
| 正确初始化 LinuxThread 同步原语。 | |

## 总结

LinuxThread 库没有完全实现 POSIX 1003.1c，但它几乎完成了。主要的不合规特性是使用信号。

今天课程的前半部分涵盖了进程和线程。后半部分侧重于 IPC（进程间通信）。

## 问答

- **Q** 如何将条件变量初始化为已信号状态？**A** 这种 `CondVar` 的实现始终将条件变量初始化为已信号状态。
- **Q** 如何避免致命拥抱？**A** 互斥死锁发生在两个线程获取了不同的锁，并阻塞等待另一个线程释放锁时。

## 工作坊

工作坊提供了测试题来帮助你理解材料。

## 测验

- Q 进程的状态。
- Q 描述 FIFO 和轮询调度的区别。
- Q 二进制信号量和计数信号量的区别？
- Q 死锁的必要条件。

## 练习题

1. 使用计数信号量，如何解决启动时的竞态条件？
2. 使用条件变量实现 24.8 中的重入。

# 第四周

# 第25 天

# 进程间通信

进程间通信 (IPC) 是进程之间通信的手段。今天的课程讨论了用于进程的一些方法。

Linux 为同一系统的进程提供了多种方法。这些方法包括管道、命名管道和 System V 进程间通信。Linux 还为不同系统之间的进程提供了其他方法，例如套接字。本节重点关注同一系统的进程间通信。

## 背景

在讨论今天的主题之前，我们将从一个用于今天所有类的定义开始。列表 25.1 中定义的 `Object` 类为创建和销毁实现了一个通用接口。

## 列表 25.1 对象接口

```cpp
// Listing 25.1 Object class
#if defined(c_object_h)
#define c_object_h

class Object
{
public:
    virtual int Create() = 0;
    virtual int Destroy() = 0;
};

#endif
```

例如，如果用户拷贝了一个管道，一个管道实例会被关闭，然后另一个实例的管道句柄将失效。由于这个原因，今天课程的所有对象将拷贝构造函数定义为私有成员函数。此外，没有实现拷贝构造函数。通过不实现拷贝构造函数，其他函数无法无意中调用它；任何调用拷贝构造函数的尝试都会导致链接错误。

## 管道

管道是一种简单的方法，允许一个进程将其标准输入附加到另一个进程的标准输出上。管道是父进程和子进程之间的半双工通信通道。

Linux 提供了 `pipe()` 系统调用返回两个文件描述符作为文件描述符数组；文件描述符 0 是管道的读端，文件描述符 1 是管道的写端。`pipe` 函数原型如下：

```c
int pipe(int fd[2]);
```

文件描述符是一个用于内核引用已打开文件的整数。当进程想要从文件读取或向文件写入时，通过文件描述符来标识该文件。

> 正如你在第 24 天“系统编程”中所学到的，子进程会继承父进程打开的句柄。这包括用于管道的句柄。

管道的典型用法是父进程创建一个管道并调用 `fork()` 创建子进程。由于子进程继承了父进程的所有文件描述符，父进程和子进程现在都包含了指向彼此的文件描述符。为了完成一个允许子进程向父进程写入的半工管道设置，子进程关闭 `fd[0]`（读取文件描述符），而父进程关闭 `fd[1]`（写入文件描述符）。剩余的是子进程的文件描述符和父进程的读取文件描述符。这一系列事件创建了一个允许子进程向父进程写入的半工管道。图 25.1 显示两个进程之间管道的图。

**图 25.1** 两个进程之间的管道。

![](img/a66ce94ee9cc26e5c70f5604bcd3600c_906_0.png)

管道创建并完成必要的设置后，通过使用标准的 `read` 和 `write` 调用来实现通信。

管道默认是阻塞 IO。也就是说，如果管道执行读取操作且没有数据可读，管道将阻塞直到有可用数据。如果用户不想阻塞，可以使用 `O_NONBLOCK` 标志打开管道以禁用 IO 阻塞。

列表 25.2 定义了 `Pipe` 类。该类封装了管道系统调用。

## 列表 25.2 Pipe 类定义

```cpp
// Listing 25.2 Pipe class
#if defined(c_pipe_h)
#define c_pipe_h

#include <unistd.h>
#include <object.h>

class Pipe : public Object
{
public:
    Pipe();
    ~Pipe();

    int Create();
    int Destroy();

    void SetToRead();
    void SetToWrite();

    int ReadFromPipe(char*);
    int WriteToPipe(char*);

private:
    Pipe& operator=(const Pipe&); // disallow copy

    bool init_;
    bool read_;
    int pipe[2];
};

#endif
```

列表 25.2 中定义的 `Pipe` 类实现了本节讨论的与管道相关的程序。父进程和子进程决定哪个进程读取以及哪个进程写入，每个进程调用 `SetToRead` 或 `SetToWrite` 成员函数。在每个进程初始化其读或写管道后，它们调用 `ReadFromPipe` 或 `WriteToPipe` 成员函数来传输数据。

管道限于父/子进程。

半工管道必须由两个进程创建并设置。如果其中一个进程未准备好，即一个进程向另一个进程未为读取打开的管道写入，或从另一个进程未为写入打开的管道读取，则会返回信号 `SIGPIPE`。

半工管道使用进程文件描述符实现。由于文件描述符是进程资源，因此当进程退出时，文件描述符将返回给系统。

## 进程间通信最佳实践

| 可以的 | 不要 |
| --- | --- |
| 对具有父子关系的进程使用管道 | 除非两个进程都已设置好各自的管道端，否则不要向管道写入数据 |

## popen 和 pclose

或者，Linux 提供了另一种创建半工管道的方法：`popen()`。

```c
FILE *popen(char *command, char *type);
```

`popen` 系统调用创建一个管道，执行 `fork`，然后调用 `exec` 来运行请求的命令。向 `popen` 创建的管道读取或写入值由 `type` 参数决定。`popen` 的返回值是一个 `iostream`，必须用 `pclose` 关闭。

为了关闭由 `popen` 创建的流，用户应该调用 `pclose`。`pclose` 会终止管道并将进程资源返回给系统。

```c
FILE *popen(ls, "r");
```

## 命名管道 (FIFOs)

命名管道是一种允许独立进程进行通信的方法。在 UNIX 世界中，命名管道传统上被称为 FIFOs（先进先出）。命名管道类似于管道；它是两个进程之间的半工管道。管道与命名管道的区别在于，当进程完成命名管道的使用后，命名管道仍然留在系统中。

管道与命名管道的另一个区别是，由于命名管道是文件系统的一部分，因此必须像文件一样打开和关闭。

使用命名管道的过程与使用 `pipe` 系统调用相似。一个进程打开命名管道写入，另一个进程打开命名管道读取。一旦命名管道被双方打开，进程就可以通过命名管道相互通信。命名管道可以通过多种方式创建。可以使用 shell 命令 `mknod` 和 `mkfifo` 来创建命名管道。此外，进程可以使用 `mknod` 系统调用。

```c
int mknod(char *pathname, mode_t mode, dev_t dev);
```

![](img/a66ce94ee9cc26e5c70f5604bcd3600c_908_0.png)

注意 `mknod` 通常留给 root 用户；但任何用户都可以使用 `mkfifo` 创建命名管道。

分析 `Create` 函数被重载，以接收命名管道名称或使用默认值。管道创建后，数据通过标准的读写调用（`fopen`、`fclose`、`fread` 和 `fwrite`）进行传递。

列表 25.3 显示了我们命名管道的实现。

## 列表 25.3 NamedPipe 类定义

```cpp
// Listing 25.3 NamedPipe class
#if defined(c_pipe_h)
#define c_pipe_h

#include <sys/types.h>
#include <sys/stat.h>
#include <stdio.h>
#include <object.h>

class NamedPipe : public Object
{
public:
    NamedPipe();
    ~NamedPipe();

    int Create();
    int Create(char* name);
    int Destroy();

    int Open();
    int Close();

    int Read(char* buf, int len);
    int Write(char* buf, int len);

private:
    NamedPipe& operator=(const NamedPipe&); // disallow copy

    bool init_;
    FILE* fp_;
    char* name_;
};

#endif
```

客户端和服务器可以约定一个键，并在公共头文件中共享该键。

客户端和服务器可以约定一个路径和一个 ID，并调用系统函数 `ftok()` 生成一个键。`ftok()` 是一个系统调用，它根据输入的文件和进程 ID 创建一个键。

在列表 25.4 中，我们开发了一个管理 System V IPC 键的 C++ 类。每个 IPC 对象都必须有一个键对象才能正常工作。

## 列表 25.4 键类定义

```cpp
// Listing 25.4 Key class
#if Defined(c_key_h)
#define c_key_h

#include <object.h>
#include <sys/types.h>
#include <sys/ipc.h>

class Key
{
public:
    Key();
    ~Key();

    int Create(char* name, char id);
    int Create(Key_t key);
    void Destroy();

    key_t Get(void);

private:
    Key& operator=(const Key&); // disallow copy

    bool init_;
    key_t key_;
};

#endif
```

获取键的第一步是创建一个键对象并调用 `Create` 成员函数。`Create` 是重载的，因此你可以传递一个预定义的键，或者通过传递文件名和 ID 来创建一个键。键创建后，你可以通过调用 `Get` 成员函数获取键值。

## IPC 权限结构

每个 IPC 方法都包含一个 `ipc_perm` 结构。`ipc_perm` 结构包含了 IPC 对象的权限和所有者。列表 25.5 显示了 Linux 的 `ipc_perm` 结构。

## 列表 25.5 Linux ipc_perm 结构

```c
struct ipc_perm
{
    kernel_key_t key;
    kernel_uid_t uid;
    kernel_gid_t gid;
    kernel_uid_t cuid;
    kernel_gid_t cgid;
    kernel_mode_t mode;
    unsigned short seq;
};
```

当创建进程间通信方法时，`ipc_perm` 结构会自动填充。在 IPC 对象的生命周期内，用户可以通过 `msgget`、`semctl` 或 `shmctl` 函数修改 `uid`、`gid` 和 `mode` 字段。要更改这些字段，用户必须是 IPC 对象的创建者或超级用户。每个创建进程间通信方法的进程间调用都接受一个 `flags` 参数，用于定义该对象的权限。这些标志用于填充 `ipc_perm` 结构。

## ipcs 和 ipcrm 命令

System V 进程间通信方法实现在内核中。如果一个进程退出时没有清理其 IPC 方法，该方法将残留在内核中。`ipcs` 和 `ipcrm` 命令用于显示 IPC 方法的状态并清理任何残留资源。

`ipcs` 命令用于获取所有 IPC 对象的状态。以下是使用 `ipcs` 命令的结果——我的系统上有两个共享内存段，ID 为 78592 和 78593。

```text
------ Shared Memory Segments ------
key owner perms bytes nattch status
0x00bc614e 78592 paul 666 1024 0
0x000162e 78593 paul 666 64 0

------ Semaphore Arrays ------
key owner perms nsems status

------ Message Queues -------
key msqid owner perms used-bytes messages
```

`ipcrm` 命令用于从系统中移除 IPC 对象。在前节的示例中，我们将使用 `ipcrm` 命令移除一个共享内存段。以下演示了移除共享内存 ID 78593 的过程。

```text
resource deleted
```

现在我们已经删除了共享内存 ID 78593，我们将重新运行 `ipcs` 命令以验证共享内存方法已被移除。以下是重新运行 `ipcs` 命令的结果。
