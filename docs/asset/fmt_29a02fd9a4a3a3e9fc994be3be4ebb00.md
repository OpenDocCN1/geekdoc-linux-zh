
# 0x00487c in main () at expc.C:13

`13 throw ( 5 );`

## 6.11 线程

从内存读取然后根据大小开始使用列表。当线程 `#1` 正在读取列表时，线程 `#2` 可能会更改列表或列表的大小，导致线程 `#1` 获取的信息不一致。如果线程 `#1` 在线程 `#2` 更改列表之前读取完列表，则没有问题。同样，如果线程 `#1` 读取得足够快（在线程 `#2` 有机会实际进行更改之前），也没有问题。竞态条件通常难以重现，因为影响时机的变化（例如附加 `GDB`）可能会改变事件的顺序或持续时间，从而有效地掩盖该问题。

使用线程时，另一个具有挑战性的问题类型是多线程内存损坏。在这种情况下，一个线程在未来的某个时刻读取了内存（以及被损坏的数据）。这是一种极具挑战性的问题类型，因为该问题的症状可能与原始原因非常脱节（且很难将两者联系起来）。

观察点（`Watchpoints`）确实可以帮助处理多线程内存损坏，但遗憾的是，`GDB` 通常对线程的支持并不良好（至少在 Linux 上不是）。主要问题是 `GDB` 只能监控单个线程中的某个地址。换句话说，如果你设置了监控线程 `#1` 向某个地址写入的操作，那么当线程 `#2` 写入被监控的地址时，它不会触发。这限制了观察点在线程应用程序中的用处！

如果程序或应用程序具有某种追踪功能，那么定期或针对每个追踪点检查或转储被损坏的地址范围（如果你知道的话）可能是值得的。这样你可以将损坏内存的代码区域缩小到损坏发生时在追踪中捕获的函数。遗憾的是，由于缺乏对多线程进程的观察点支持，`GDB` 可能不是调试多线程损坏的最佳工具。无论如何，让我们探索一下 `GDB` 对多线程进程能做什么。

以下程序用于说明 `GDB` 的基本线程支持。该程序创建了一个线程，它消耗栈空间直到达到一定数量或直到线程耗尽栈：

```c
#include <unistd.h>
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
#include <sys/types.h>
void burnStackSpace( int *depth )
{
    char foo[8192];
    (*depth)--;

if ( *depth > 0 )
{
    burnStackSpace( depth );
}
else
{
    sprintf( foo, "Hit final depth!\n" ); // 实际上使用 "foo" 以
// 确保编译器保留它
    puts( foo );
    sleep( 30 );
}
}
extern "C" void useStackSpace( void *arg)
{
    int stackSpace = *(int *)arg;
    int depth = ( stackSpace/8192 ) / 2;
    burnStackSpace( &depth );
    return NULL;
}
int main(int argc, char *argv[], char *envp[])
{
    int src = 0;
    pthread_t newThread;
    int stackSpace = 1008*1024;
    pthread_attr_t attr;
    pthread_attr_init(&attr);
    pthread_attr_setstacksize(&attr, 1024*1024 );
    src = pthread_create(&newThread, &attr, useStackSpace, (void*)&stackSpace);
    pthread_join(newThread, NULL);
}
```

函数 `burnStackSpace` 是一个递归函数，旨在消耗栈空间，以展示 `GDB` 中栈空间溢出的状况。函数 `useStackSpace` 是新创建的函数调用的第一个函数。`main` 函数简单地创建一个线程并等待它完成。

### 6.11.1 编译与进程信息

这是我们将用于编译程序的命令行：

```
penguin g++ threads.C -o threads -lpthread
```

注意，我们需要包含 `-lpthread` 来引入 posix 线程库。这对于 Linux 多线程应用程序是必须的。

在检查这个多线程程序之前，值得提到 Linux 中的线程支持取决于你的 Linux 内核版本。如果我们在旧版本的 Linux 内核（2.6 版本以前）上运行此程序，根据 `ps` 列表将三个“进程”（一个原始进程和两个线程）：

```
penguin ps -fu wilding | egrep threads | egrep -v grep
widening 19151 19400 0 08:46 pts/2 00:00:00 threads
widening 19152 19151 0 08:46 pts/2 00:00:00 threads
widening 19152 19152 0 08:46 pts/2 00:00:00 threads
```

这是由于线程的原始实现（被称为 "Linux Threads"），它让每个线程看起来非常像独立的进程。同样值得注意的是，当我们预期两个线程（主线程和主线程创建的线程）时，出现了三个线程。额外的线程可能创建也可能不，这取决于系统的线程实现。

在较新的 Linux 内核（2.6+ 版本）中，你只会看到一个进程，因为线程不会像早期的 Linux 内核那样显示为进程：

```
penguin2 ps -fu wilding | egrep threads
widening 22959 22534 0 13:05 pts/10 00:00:00 threads
widening 22964 22865 0 13:05 pts/16 00:00:00 /bin/grep -E threads
```

这种较新的实现被称为 Native POSIX Thread Library (`NPTL`)，并包含在最近版本的 Linux 内核中。尽管存在差异，这两种实现在 `GDB` 中可以几乎以相同的方式处理。无论如何，让我们看看这些线程在 `GDB` 中是什么样子的。使用 `info threads` 命令：

```
(gdb) info threads
2 10274887004 (LWP 22996) 00000002a956c6d2af in __write_nocancel
```

# GNU 调试器 (GDB) 第 6 章

考虑到段错误并非由于尝试访问无效指针或其他典型原因而引起。

此外，从被捕获指令的汇编列表中，我们看到了以下内容：

```
gdb disass 0x0000000000040080a 0x0000000000040081a
Dump of assembler code from 0x40080a to 0x40081a:
0x000000000004008a <_Z1burnStackSpacePi+34>: callq 0x0007e8
0x000000000004008f <_Z1burnStackSpacePi+39>: jmp 0x004848
- <Z1burnStackSpacePi+36>
0x0000000000040090 <_Z1burnStackSpacePi+41>: mov
0xffffff(%rb), rax
0x0000000000040815 <_Z1burnStackSpacePi+45>: lea
0xffffff(%rbp), rdi
End of assembler dump.
```
