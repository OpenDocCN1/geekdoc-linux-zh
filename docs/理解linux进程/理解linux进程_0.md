# 理解 Linux 进程





## 关于这本书

本书受[*理解 Unix 进程*](http://www.duokan.com/book/41446)启发而作，用极简的篇幅深入学习进程知识。

*理解 Linux 进程*用 Go 重写了所有示例程序，通过循序渐进的方法介绍 Linux 进程的工作原理和一切你所需要的概念。

本书适合所有 Linux 程序员阅读。[在线阅读](http://www.linuxprocess.com)，PDF 下载](https://github.com/tobegit3hub/understand_linux_process/blob/master/understan_linux_process.pdf?raw=true)。

## 三位好朋友

阅读前介绍三位即将与大家打交道的小伙伴：Linux、Go 和 Docker。

Linux 是我们主要的研究对象，书中所有概念与程序都基于 Linux，这同样适用于所有 Unix-like 系统。

`Go`是本书所有示例程序的实现语言，当然进程的概念与原理是相通的，你也可以使用其他编程语言实现。

`Docker`为我们创造可重复的实验环境，使用`Docker`容器你可以轻易地模拟与本书一模一样的运行环境。

感谢 `Wawa Leung`

否则这本书在两年前就发布了

## 本书概述

进程的概念大家都很熟悉，但你是否能准确说出僵尸进程的含义呢？还有`COW(Copy On Write)`、`Flock(File Lock)`、`Epoll`和`Namespace`的概念又是否了解过呢？

本书汇集了进程方方面面的基础知识，加上编程实例，保证阅读后能自如地回答以上问题，在项目开发中对进程的优化也有更深的理解。

## 本书架构

本书按循序渐进的方式介绍进程的基础概念和拓展知识，主要涵盖以下几个方面：

* 进程的基础知识介绍
* 进程相关的编程实例
* 进程的进阶知识详解
* 项目 Run 的进程管理
* 使用进程的注意事项

其中项目[Run](https://github.com/runscripts/run)是`Go`实现的脚本管理工具，通过研究`Run`的源码能够加深对进程管理的理解。

## 关于勘误

本书所有内容都托管到[GitHub](https://github.com/tobegit3hub/understand_linux_process)，如果纰漏或错误请提[Issue](https://github.com/tobegit3hub/understand_linux_process/issues/new)。

### 示例程序

本书所有示例程序都基于`Go`编写，代码托管到[GitHub](https://github.com/tobegit3hub/understand_linux_process_examples)。

每章的示例都是可直接运行的`Go`源文件，例如第一章的 Hellow World 程序可以通过`go run hello_world.go`来运行并查看运行结果。

```
## go run hello_world.go
Hello World 
```

接下来介绍使用`Docker`来运行本书的示例程序。

### Docker 简介

[Docker](https://github.com/docker/docker)是一个容器运行平台，你可以将程序及其依赖打包成容器，在不同机器上运行可得到一致的运行效果。因为不同的系统环境或`Go`版本可能影响程序的运行结果，为了得到可预测、可重复的实验环境，我们引入了`Docker`容器技术。

### Docker 使用

我们不仅开源了示例代码，还创建了官方[Docker 镜像](https://registry.hub.docker.com/u/tobegit3hub/understand_linux_process_examp/)。

只要执行命令`docker run -i -t tobegit3hub/understand_linux_process_examp`，就可以马上创建本书的实验环境。进入容器后可以轻易地运行示例程序。

```
root@6a8e36a53495:/go/src# go run hello_world.go
Hello World 
```

当然你也可以在本地运行自己的`Go`示例，或者使用官方`Go`镜像`docker run -i -t golang:1.4 /bin/bash`。

## 第一章 进程基础

作为本书的第一部分，主要介绍进程的`PID`、进程状态、退出码和`POSIX`等基础概念。

网络有很多零散的资料介绍基础了，为什么还要花篇幅介绍这些呢？首先我们要保证看过这些章节的都能掌握这些概念，其次通过编写代码实例，我们还能动手验证这些概念，已经不能更赞了。

学习完这章我们应该能够准确回答出`PID`、`PPID`、进程名字、进程参数、进程状态、退出码、死锁、活锁、`POSIX`、`Nohup`等概念。

### 进程的定义

根据维基百科的[定义](http://zh.wikipedia.org/wiki/%E8%A1%8C%E7%A8%8B)，进程(`Process`)是计算机中已运行程序的实体。用户下达运行程序的命令后，就会产生进程。进程需要一些资源才能完成工作，如 CPU 使用时间、存储器、文件以及 I/O 设备，且为依序逐一进行，也就是每个 CPU 核心任何时间内仅能运行一项进程。。

我们简单总结下，进程就是代码运行的实体。这里补充一点，进程不一定都是正在运行的，也可能在等待调度或者停止，进程状态将在后续详细介绍。

### 举个例子

进程的概念应该很好理解，因为我们都在写代码，这些代码跑起来了就是一个进程，为了完整性我们介绍最简单的 Hello World 进程。

### Hello World 进程

Hello World 程序是每门编程语言的入门示例，注意这个程序还不是进程哦，它的作用是在终端输出“Hello World”然后退出。当我们运行 Hello World 程序时，系统就创建一个 World 进程。这也是最简单的进程，没有系统调用、进程间通信。

### Bash 实现

用`Bash`实现 Hello World 只需要一行代码，运行后输出“Hello World”。

```
root@8709bfcb2:/go/src# echo Hello World
```

稍微提一下`echo`是 Linux 自带的程序，可以接受一个或多个参数，反正它们输出到终端而已。这样最简单的进程就诞生了，当然也可以用`Go`重写程序。

### Go 实现

`Go`实现的源码参见`hello_world.go`。

```
package main

import (
  "fmt"
)

func main() {
  fmt.Println("Hello World")
}
```

运行后得到输出。

```
root@8709bfcb2:/go/src# go run hello_world.go
Hello World
```

发生了接下来我们将各个方面介绍。

### PID

首先来学习`PID`这个概念，PID 全称`Process ID`，是标识和区分进程的全局唯一的整数。Hello World 运行时也有一个 PID，只是它结束后释放了，我们可以通过`print_pid.go`显示当前进程。

### 示例程序

`print_pid.go`的源码如下，通过`Getpid()`函数获得当前进程。

```
package main

import (
  "fmt"
  "os"
)

func main() {
    fmt.Println(os.Getpid())
}
```

### 运行结果

```
root@8709bfcb2:/go/src# go run print_pid.go
2922
root@8709bfcb2:/go/src# go run print_pid.go
2932
```

可以看出进程运行时是由操作系统分配的，同一个程序运行两次产生两个 PID。那 PID 究竟有什么用？稍后。

### PPID

每个进程都有 PPID，也就是父进程，通过`PPID`找到父进程。为什么进程会有父进程呢？所有进程都是它衍生出来的，后面详细介绍几种方法。准确的进程号为 1，叫做进程树。

### 示例程序

要想获得 PPID，可以通过`Getppid()`函数获得，`ppid.go`代码如下。

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  fmt.Println(os.Getppid())
}
```

### 运行结果

```
root@8709bfcb2:/go/src# go run ppid.go
2892
root@8709bfcb2:/go/src# go run ppid.go
2902
```

有趣的事情是发现每次运行的进程 ID 都不一样，符合我们的预期，原来通过`go run`都会启动一个新的进程。

### 编译后运行

如果我们先生成二进制文件再执行结果怎样？

```
root@8709bfcb2:/go/src# go build ppid.go
root@8709bfcb2:/go/src# ./ppid
root@8709bfcb2:/go/src# ps aux | grep "1" | grep -v "grep"
root         1  0.0  0.3  2028  3184        Ss   07:25   0:00 /bin/bash
```

这次发现父进程都是一样的，而且通过`ps`命令可以看到父进程就是`bash`，说明通过终端执行是从`bash`衍生出各种进程。为了执行这个程序要查找、打包。

### 使用 PID

拿到 PID 后，我们就可以通过`kill`命令结束进程，也可以通过`kill -9`或其他数字向进程发送不同的信号。信号是很重要的概念，我们后面会详细介绍，那么有了进程 ID，我们也可以看看进程名字。

### 进程名字

每个进程都一定有进程名字，例如我们运行`top`，进程名就是“top”，如果是自定义的程序呢？其实进程名一般都是程序。

### Top

在命令行执行`top`后，得到类似输出，可以看到目前有三个进程，PID 分别是 1、8 和 9。

```
top -12:45:18 up 1 min,  0 users,  load average: 0.86, 0.51, 0.20
Tasks:   3,   1 running,   2 sleeping,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 st
KiB Mem:   2056748 total,   301984 used,  1754764 free,    20984 buffers
KiB Swap:  1427664 total,        0 used,  142764 free.   231376 cached Mem
PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
1 root      20   0    4312    692    612 S   0.0  0.0   0:00.23 sh
8 root      20   0   20232   3048   2756 S   0.0  0.1   0:00.03 bash
9 root      20   0   21904   2384   2060 R   0.0  0.1   0:00.00 top 
```

### PS

执行`ps aux`后输出如下，其中`aux`参数让`ps`命令显示更详细的参数。前面 PID 为 9 的进程已经退出了，取而代之的是 PID 为 11 的进程。

```
root@fa13d0439d7a:/go/src# ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.2  0.0   4312   692 ?        Ss   12:45   0:00 /bin/sh -c /bin/bash
root         8  0.0  0.1  20232  3224 ?        S    12:45   0:00 /bin/bash
root        11  0.0  0.0  17484  2000 ?        R+   12:46   0:00 ps aux 
```





```
package main

import "flag"
import "fmt"

func main() {
  wordPtr := flag.String("word", "foo", "a string")
  numbPtr := flag.Int("numb", 42, "an int")
  boolPtr := flag.Bool("fork", false, "a bool")
  var svar string
  flag.StringVar(&svar, "svar", "bar", "a string var")

  flag.Parse()

  fmt.Println("word:", *wordPtr)
  fmt.Println("numb:", *numbPtr)
  fmt.Println("fork:", *boolPtr)
  fmt.Println("svar:", svar)
  fmt.Println("tail:", flag.Args())
} 
```

运行结果如下，相比直接使用`os.Args`代码也简洁了不少。

```
 root@87096bf68cb2:/go/src# ./flag -word=opt -numb=7 -fork -svar=flag
word: opt
numb: 7
fork: true
svar: flag
tail: []
root@87096bf68cb2:/go/src# ./flag -h
Usage of ./flag:
  -fork=false: a bool
  -numb=42: an int
  -svar="bar": a string var
  -word="foo": a string 
```

使用 Go 获取进程参数是很简单的，不过一旦参数太多，最佳实践还是使用配置文件。

进程参数只有在启动进程时才能赋值，如果需要在程序运行时进行交互，就需要了解进程的输入与输出了。

## 进程输入与输出

每个进程操作系统都会分配三个文件资源，分别是标准输入(`STDIN`)、标准输出(`STDOUT`)和错误输出(`STDERR`)。通过这些输入流，我们能够轻易得从键盘获得数据，然后在显示器输出数据。

### 标准输入

来自管道(`Pipe`)的数据也是标准输入的一种，我们写了以下的实例来输出标注输入的数据。

```
package main

import (
  "fmt"
  "io/ioutil"
  "os"
)

func main() {
  bytes, err := ioutil.ReadAll(os.Stdin)
  if err != nil {
    panic(err)
  }

  fmt.Println(string(bytes))
} 
```

运行结果如下。

```
 root@87096bf68cb2:/go/src# echo string_from_stdin | go run stdin.go
string_from_stdin 
```

### 标准输出

通过`fmt.Println()`把数据输出到屏幕上，这就是标准输出了，这里不太演示了。

### 错误输出

程序的错误输出与标准输出类似，这里暂不演示。

了解完进程一些基础概念，我们马上要深入学习并发与并行的知识了。

## 并发与并行

并发(`Concurrently`)和并行(`Parallel`)是两个不同的概念。借用 Go 创始人 Rob Pike 的说法，并发不是并行，并发更好。并发是一共要处理(`deal with`)很多事情，并行是一次可以做(`do`)多少事情。

举个简单的例子，华罗庚泡茶，必须有烧水、洗杯子、拿茶叶等步骤。现在我们想尽快做完这件事，也就是“一共要处理很多事情”，有很多方法实现实现并发，例如请多个人同时做，这就是并行。并行是实现并发的一种方式，但不是唯一的方式。我们一个人也可以实现并发，例如先烧水、然后不用等水烧开就去洗杯子，所以通过调整程序运行方式也可以实现并发。

### 大神讲解

如果还不理解，建议看 Rob Pike 题为 Concurrency is not Parallelism 的[演讲 PPT](http://concur.rspace.googlecode.com/hg/talk/concur.html)和[演讲视频](http://blog.golang.org/concurrency-is-not-parallelism)。

我把演讲的 PPT 截图贴出来方便大家理解。

## 总结

总结一下，并行是实现并发的一种方式，在多核 CPU 的时代，并行是我们设计高效程序所要考虑的，那么进程是不是越多越好呢？

### 进程越多越好？

前面提到多进程的并行可以提高并发度，那么进程是越多越好？一般遇到这种问题都回答不是，事实上，很多大型项目都不会同时开太多进程。

下面以支持 100K 并发量的 Nginx 服务器为例。

### 举个例子: Nginx

Nginx 是一个高性能、高并发的 Web 服务器，也就是说它可以同时处理超过 10 万个 HTTP 请求，而它建议的启动的进程数不要超过 CPU 个数，为什么呢？

我们首先要知道 Nginx 是 Master-worker 模型，Master 进程只负责管理 Worker 进程，而 Worker 进程是负责处理真实的请求。每个 Worker 进程能够处理的请求数跟内存有关，因为在 Linux 上 Nginx 使用了`epoll`这种多路复用的 IO 接口，所以不需要多线程做并行也能实现并发。

而多进程有一个坏处就是带来了 CPU 上下文切换时间，所以一味提高进程个数反而使系统性能下降。当然如果当前进程小于 CPU 个数，就没有充分利用多核的资源，所以 Nginx 建议 Worker 数应该等于 CPU 个数。

### 特殊情况

我们想想进程数应该等于 CPU 数，但是如果进程有阻塞呢？这是是应该提高进程数增加并行数的。

在 Nginx 的例子中，如果 Nginx 主要负责静态内容的下载，而服务器内存比较小，大部分文件访问都需要读磁盘，时候进程很容易阻塞，所以建议提高下 Worker 数目。

### 绑定 CPU

一般情况下除了确保进程数等于 CPU 数，还可以绑定进程与 CPU，这就保证了最少的 CPU 上下文切换。

在 Nginx 中可以这样配置：

```
worker_processes 4;
cpu_affinity 0;
```

这是通过系统调用`sched_setaffinity()`实现了，感兴趣可以学习这方面的。

### 进程状态

根据进程的定义，知道进程是实体，可能是正在运行，也可能是停止的。网上总结进程一共 7 种状态，究竟怎么算呢，最好的方法还是看源码。

在`proc/array.c`文件中：

```
/*
* The task array is a "bitmap" of states. */
struct task_struct {
  volatile long state; /* -1 unrunnable, 0 runnable, >0 stopped */
  void *stack;
  atomic_t usage;
  unsigned int flags; /* per process flags, defined below */
  unsigned int ptrace;
};
static const char task_state[] = {
  "R (running)",        /* 0 */
  "S (sleeping)",        /* 1 */
  "D (disk sleep)",      /* 2 */
  "T (stopped)",        /* 4 */
  "t (tracing)",        /* 8 */
  "X (dead)",          /* 16 */
  "Z (zombie)",         /* 32 */
};
```

这真的是 Linux 的源码，可以看出进程一共 7 种状态，含义也清晰，注意其中`D`(`disk sleep`) 称为不可中断睡眠状态(`uninterruptible sleep`)。

### 进程状态

通过[Ptrace](https://idea.popcount.org/2012-11-linux-process-states/)、[include/linux/sched.h](https://github.com/torvalds/linux/blob/master/include/linux/sched.h):

```
struct task_struct {
  volatile long state;
...
enum {
  TASK_RUNNING = 0,
  TASK_SLEEPING = 1,
  TASK_UNINTERTIBLE = 2,
  TASK_STOPPED = 4,
  TASK_TRACING = 8,
  TASK_DEAD = 16,
  TASK_ZOMBIE = 32,
};
```

通过`ps aux`可以看到进程的状态。

O：空闲状态

S：休眠状态（sleeping）

R：运行（running）

D：不可中断睡眠（disk sleep）

T：停止（stopped）

t：跟踪状态（tracing）

Z：僵尸状态（zombie）

## 退出码

任何进程退出时，都会留下退出码，操作系统根据退出码知道进程是否正常。

退出码是 0 到 255 的整数，通常 0 表示正常退出，其他数字表示不同的。

### 示例程序

```
package main

func main() {
  panic("Call panic()")
} 
```

### 运行结果

```
 root@fa13d04397a:/go/src# go run exit_code.go
panic: Call panic()

goroutine 16 [running]:
runtime.panic(0x425900, 0xc208000010)
/usr/src/go/src/pkg/runtime/panic.c:279 +0xf5
main.main()
/go/src/exit_code.go:4 +0x61

goroutine 17 [runnable]:
runtime.MHeap_Scavenger()
/usr/src/go/src/pkg/runtime/mheap.c:507
runtime.goexit()
/usr/src/go/src/pkg/runtime/proc.c:1445

goroutine 18 [runnable]:
bgsweep()
/usr/src/go/src/pkg/runtime/mgc0.c:1976
runtime.goexit()
/usr/src/go/src/pkg/runtime/proc.c:1445
exit status 2 
```





# Concept of Livelock

Compared to deadlock, what is the concept of `Livelock`? Interestingly, Baidu Baike explains this incorrectly.

```
 如果事务 T1 封锁了数据 R,事务 T2 又请求封锁 R，于是 T2 等待。T3 也请求封锁 R，当 T1 释放了 R 上的封锁后，系统首先批准了 T3 的请求，T2 仍然等待。然后 T4 又请求封锁 R，当 T3 释放了 R 上的封锁之后，系统又批准了 T4 的请求......T2 可能永远等待。 
```

This is clearly the definition of `Starvation`. Processes entering a livelock are not blocked and continue to use the `CPU`, but the outside world sees the process making no progress.

# Livelock Instance

Take a simple example: two people are walking towards each other on a narrow plank bridge. They both step to one side to yield, so neither can pass. Then they both move to the other side, and again neither can pass. If not disturbed by other factors, they keep moving in sync, but from an outside perspective, neither moves forward. This is livelock.

Livelock can exhaust the `CPU`. The solutions are to introduce random variables, increase the number of retries, etc.

Therefore, livelock is also a possible problem in programming design, preventing processes from running while still consuming `CPU`.

Next is the most significant content of this chapter: `POSIX`.

# Introduction to POSIX

`POSIX` (Portable Operation System Interface) sounds high-end, it is simply an interface standard for operating systems. Who follows this standard? The famous `Unix` and `Linux`. Someone asked if `Mac OS` is compatible with `POSIX`; the answer is `Yes`, Apple's operating system is also `Unix-based`.

With this specification, you can call generic `APIs`. `POSIX` system calls provided by `Linux` can also execute on `Unix`, so the best way to learn `Linux` low-level interfaces is to understand the `POSIX` standard.

To add, many modern programming languages (`Go`, `Java`, `Python`, `Ruby`, etc.) are natively cross-platform, so we rarely notice system call compatibility. In fact, `POSIX` provides cross-platform semantics for these languages, and this is a source-level guarantee.

# POSIX Standard

`POSIX` consists of several `IEEE` standards, including `1003.0`, `1003.1`, `1003.1b`, and `2003`. In fact, even `Linux` does not fully comply with these definitions, but using `Linux` to learn `POSIX` is sufficient.

Given that most programmers have never seen `IEEE` documents, let's look at [IEEE 1003.1-2001](http://wenku.baidu.com/link?url=8dfQAy-mpeNdkDzX1LWCCEJia5x4_pS-Br6alnnrNweN8HxyXbHewGnxrPgFhQ3TzaAodlfHay9KiAuOmKbWvfSUr-36XyFIDgokfCldgR7).

The length is similar to a thesis. The main idea is to correct issues in the `Base` standard. This document does not add new interfaces but adds symbols, non-function definitions, and reserves more namespaces. This is a very rigorous document; interested students can read it, but for ordinary programmers, we focus on the following content.

# POSIX Processes

When we run a `Hello World` program, the operating system creates a POSIX process through the `fork` and `exec` interfaces defined by `POSIX`. This process can use generic mechanisms like `IPC` and signals.

# POSIX Threads

`POSIX` also defines standards for threads, including `APIs` for creating and controlling threads, implemented in the `Pthreads` library. Thread knowledge can be studied in depth later.

# Nohup Command

Every developer has fallen into this trap: running a background program in the command line, only to find the process exited after closing the terminal. Searching online reveals the use of `nohup`. What is the reason?

Actually, normal processes bind to a `TTY` (virtual terminal) by default. When the terminal closes, the system sends a `TERM` signal to all processes above, causing normal processes to exit. Of course, some processes do not exit; these are the daemon processes mentioned later.

The principle of `nohup` is also simple: when the terminal closes, a `SIGHUP` signal is sent to every process under that terminal. Processes run with `nohup` ignore this signal, so they do not exit when the terminal is closed.

# Example

We implement a simple `Web server` using `Go`. The code `web_server.go` is as follows:

```
 package main

import (
  "fmt"
  "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Println("Handle request")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8000", nil)
} 
```

Then run it in the terminal and test it.

```
 ➜ go build web_server.go
➜ ./web_server &
[1] 25967
➜  wget 127.0.0.1:8000
--2014-12-28 22:24:07--  http://127.0.0.1:8003/
Connecting to 127.0.0.1:8003... connected.
HTTP request sent, awaiting response... 200 OK
Length: 5 [text/plain]
Saving to: 'index.html.4'

100%[======================>] 5           --.-K/s   in 0s

2014-12-28 22:24:07 (543 KB/s) - 'index.html' saved [5/5] 
```

If the terminal is closed, the `curl` command cannot connect to our `Web server`. What if we run it with `nohup`?

```
 ➜ go build web_server.go
➜ nohup ./web_server &
[1] 25968
➜ exit
➜ wget 127.0.0.1:8003
--2014-12-28 22:24:11--  http://127.0.0.1:8003/ 
```

We find that closing the terminal has no effect on the Web server process, which is what we expected. This is the simplest way to run a daemon. In fact, standard daemons consider other factors beyond signal handling, which will be detailed in later.

# Creating Processes

The start of this chapter demonstrated the `Hello World` program, which actually created a new process. It is easy to create new processes using `Shells` like `Bash` or `zsh`, but how is the `Shell` itself implemented? Can we implement `Shell` functionality using `Go`?

# System Calls

Actually, all of this is prepared by the operating system and exposed through `API` interfaces; these are called system calls. `Linux` and other `Unix-like` systems provide interfaces like `fork()` and `exec()`. `Bash` or the programs we write can manipulate processes by calling these interfaces.

# Creating Processes in Go

`Go` has encapsulated process-related interfaces, primarily in the `os/exec` package. By using these encapsulated interfaces, we can easily call other processes in our own projects.

This chapter has introduced many concepts, and there will be practical sessions soon to use `Go` to create and run external processes in various ways.

# Chapter 2: Go Programming Instances

After learning the basics of processes, we introduce how to run external processes using `Go` through several Go programming instances.

This chapter is mainly for programming practice. After completing it, you should have a deeper understanding of process usage and how `Go` utilizes processes.

## Spawning New Processes

This is an example from `GoByExample`; the code is at https://gobyexample.com/spawning-processes.

It can execute any `Go` or non-`Go` program, wait for the result, and continue executing this program after the external process ends.

## Code Implementation

```
 package main

import "fmt"
import "io/ioutil"
import "os/exec"

func main() {
    dateCmd := exec.Command("date")
    dateOut, err := dateCmd.Output()
    if err != nil {
        panic(err)
    }
    fmt.Println("> date")
    fmt.Println(string(dateOut))

    grepCmd := exec.Command("grep", "hello")
    grepIn, _ := grepCmd.StdinPipe()
    grepOut, _ := grepCmd.StdoutPipe()
    grepCmd.Start()
    grepIn.Write([]byte("hello grep\ngoodbye grep"))
    grepIn.Close()
    grepBytes, _ := ioutil.ReadAll(grepOut)
    grepCmd.Wait()
    fmt.Println("> grep hello")
    fmt.Println(string(grepBytes))

    lsCmd := exec.Command("bash", "-c", "ls -a -l -h")
    lsOut, err := lsCmd.Output()
    if err != nil {
        panic(err)
    }
    fmt.Println("> ls -a -l -h")
    fmt.Println(string(lsOut))
} 
```

## Running Results

```
 $ go run spawning-processes.go
> date
Wed Oct 10 09:53:12 UTC 2023
> grep hello
hello
> ls -a -l -h
total 0
drwxr-xr-x 2 user group 4096 Oct 10 ..
-rw-r--r-- 1 user group 0 Oct 10 spawning-processes.go
```





```
 if (pid=fork()) {
  exit(0); // Parent process
} 
```

然后是与终端、进程组、会话（`Session`）分离。每个进程创建时都绑定一个终端，而且属于一个进程组（进程组也有`GID`，不过等同进程组长的`PID`），这些进程组在一个会话中，如果是子进程一般会从父进程继承这些信息，想要与环境分离可以使用以下的系统调用。

```
 setsid(); 
```

同样地我们会从父进程继承文件掩码`mask`），可以手动清理掩码。

```
 umask(0); 
```

如果需要我们可以改变当前工作目录，避免运行时必须使用当前所在的文件系统。

## 使用 Nohup

前面提到过`nohup` 命令，是让程序以守护进程运行的方式之一，程序运行后忽略 `SIGHUP` 信号，也就说关闭终端不会影响进程的运行。

类似的命令还有`disown`，这里不再详述。

## 进程间通信

IPC 全称`Interprocess Communication`，指进程间协作的各种方法，当然包括共享内存、信号量或`Socket`等。

## 管道(Pipe)

管道是进程间通信最简单的方式，任何进程的标准输出都可以作为其他进程的输入。

## 信号(Signal)

下面马上会介绍。

## 消息队列(Message)

和传统消息队列类似，但是在内核实现的。

## 共享内存(Shared Memory)

后面也会更详细的介绍。

## 信号量(Semaphore)

信号量本质上是一个整型计数器，调用`wait`时计数减一，减到零开始阻塞进程，从而达到进程、线程间协作的作用。

## 套接口(Socket)

也就是通过网络来通信，这也是最通用的 IPC，不要求进程在同一台服务器上。

## 信号

我们知道信号是进程间通信的其中一种方法，当然也可以内核给进程发送的消息，注意信息只是告诉进程发生了什么事件，而不会传递任何数据。

这是进程这个概念设计时就考虑到的了，因为我们希望控制进程，就像一个小孩我们想让他按我们的想法做，前提就是他能够接受信号并且理解信号的含义。

## 信号种类

Linux 中定义了很多信号，不同的 Unix-like 系统也不一样，我们可以通过下面的命令来查当前系统支持的种类。

```
 ➜ kill -l
HUP INT QUIT ILL TRAP ABRT EMT FPE KILL BUS SEGV SYS PIPE ALRM TERM URG STOP TSTP CONT CHLD TTIN TTOU IO XCPU XFSZ VTALRM PROF WINCH INFO USR1 USR2 
```

其中 1 至 31 的信号为传统 UNIX 支持的信号，是不可靠信号（非实时的），32 到 63 的信号是后来扩充的，称做可靠信号（实时信号）。不可靠信号和可靠信号的区别在于前者不支持排队，可能会造成信号丢失，而后者不会。

简单介绍几个我们最常用的，在命令行中止一个程序我们一般摁`Ctrl+c`，这就是发送`SIGINT` 信号，而使用`kill` 命令呢？默认是`SIGTERM`，加上`-9`参数才是`SIGKILL`。

## 编程实例

```
 import os/signal

siganl.Notify()
signal.Stop() 
```

这是 Go 封装的信号接口，我们可以以此实现一个简单的信号发送和处理程序。

## 系统调用

我们要启动一个进程，需要操作系统调用（`system call`）。实际上操作系统和普通进程运行在内核态（`kernel space`），开发者运行在用户态（`user space`）。这样有效了用户程序。

## 文件描述符

Linux 提供了很多文件描述符，一个重要的设计思想就是一切皆文件，网络是文件，键盘等也是文件。文件描述符（`File Descriptor`）本质上是一个正整数，在打开或新建文件时返回，开发者可以像写文件那样通过文件描述符来操作。

POSIX 已经定义了`STDIN_FILENO`、`STDOUT_FILENO`和`STDERR_FILENO`三个常量，也就是`0`、`1`、`2`。这些文件描述符是每个进程都有，也不会冲突。

## 限制

注意了，每个进程对文件描述符个数有限。使用`ulimit`进行配置，例如服务器为了同时处理成千个请求，记住文件描述符个数是有限的。

## Epoll 简介

`Epoll`是`poll`的改进版，更加高效，同时处理大量文件描述符，跟高并发有关，Nginx 充分利用了`epoll`特性。

## Poll 

`Poll`本质上是 Linux 系统调用，接口为`int poll(struct pollfd *fds, int nfds, int timeout)`，作用是监控哪些文件描述符集合。

## Epoll 

`Epoll`关注活跃的文件描述符，相比`poll`轮询整个集合，只有发生 IO 事件时才会唤醒。它提供了边缘触发（`Edge Triggered`）特性。

## Mmap

无论是`select`、`poll`还是`epoll`，他们都要把文件描述符送到用户空间，这就存在内核空间和用户空间的拷贝问题。其中`epoll`使用了`mmap`来共享内存，提高效率。

## 共享内存

对于共享内存是好是坏，学习一下。不同进程之间内存空间是独立的，也就是说进程不能访问其他进程的内存。两个进程希望通过共享内存的方式通信，可以通过`mmap()`系统调用实现。

## Go 实例

Go 也实现了`mmap()`函数支持共享内存，不过通过`cgo`来调用系统调用函数。`cgo`是什么？它是 Go 调用 C 语言模块的功能，这种调用很平台相关的，无法保证在 Windows 也能正确运行。具体代码参见[Golang 对共享内存的操作](http://studygolang.com/articles/743)，我们也写一个简单易懂的例子。

## 写时复制(Copy On Write)

一般我们运行程序都是`Fork`一个进程后马上`Exec`加载程序，而`Fork`实际上用的是父进程的堆栈空间，Linux 通过`Copy On Write`技术极大地减少了 Fork 的开销。

Copy On Write 的含义是只有真正写的时候才把数据写到子进程，Fork 时只会页表复制到子进程，这样父子进程都指向同一个内存页，只有在写子进程的时候才会把内存页的内容重新复制一份。

## Cgroups

Cgroups 全称`Control Groups`，是 Linux 内核用于资源隔离的技术。目前 Cgroups 可以控制 CPU、内存、磁盘访问。

## 使用

Cgroups 是在 Linux 2.6.24 合并到内核的，不过项目在不断完善，3.8 内核加入了对内存的控制（`kmemcg`）。要使用 Cgroups 非常简单，阅读前建议看 sysadmincasts 的视频，[`sysadmincasts.com/episodes/14-introduction-to-linux-control-groups-cgroups`](https://sysadmincasts.com/episodes/14-introduction-to-linux-control-groups-cgroups)。

我们首先在文件系统创建 Cgroups 组，然后修改这个组的属性，启动进程时指定加入的 Cgroups 组，这样进程相当于在一个受限的资源内运行了。

## 实现

Cgroups 的实现也不是特别复杂。有一个特殊的数据结构记录进程组的信息。

## Namespaces 简介

Linux Namespaces 是资源隔离技术，在 2.6.23 合并到内核，而在 3.12 内核加入对用户空间的支持。

Namespaces 是容器技术的基础，因为有了命名空间的隔离，才能限制容器之间的进程通信，像虚拟内存对于物理内存那样，开发者无需针对容器修改已有的代码。

## 使用 Namespaces

阅读以下教程前建议看看，[`blog.jtlebi.fr/2013/12/22/introduction-namespaces`](https://blog.jtlebi.fr/2013/12/22/introduction-namespaces)。





```
 package main

import (
  "fmt"
  "os"
  "syscall"
)

func main() {
    mask := syscall.Umask(0)
    defer syscall.Umask(mask)

    err := os.MkdirAll("/tmp/gotest/", 0777)
    if err != nil {
      panic(err)
    }

    fmt.Println("Mkdir /tmp/gotest/")
} 
```

### 注意事项

这并不是`Go`的`Bug`，包括 Linux 系统调用都是这样的，创建目录除了给定的权限还要加上系统的`Umask`，`Go`也是如实遵循这种约定。

如果你想达到你的预期的权限，知道`Umask`及其用法是必须的。

### 捕获 SIGKILL

`SIGKILL`是常见的 Linux 信号，我们使用`kill`命令杀掉进程也就是像向进程发送`SIGKILL`信号。

和其他信号不同，[SIGKILL](https://en.wikipedia.org/wiki/Unix_signal#SIGKILL)和`SIGSTOP`是不可被 Catch 的，因此下面的代码是能编译通过但也是无效的，更多细节可以参考[golang/go#9463](https://github.com/golang/go/issues/9463).

```
 c := make(chan os.Signal, 1)
signal.Notify(c, syscall.SIGKILL, syscall.SIGSTOP) 
```

### 注意事项

这是 Linux 内核的限制，这种限制也是为了让操作系统有可能控制进程的生命周期，理解后我们也不应该去尝试捕获`SIGKILL`。

不过还是有人这样去做，最后结果也不符合预期，这需要我们对底层有足够的理解。

### 系统调用 sendfile

[Sendfile](http://man7.org/linux/man-pages/man2/sendfile.2.html)是 Linux 实现的系统调用，可以通过避免文件在内核态和用户态的拷贝来优化文件传输的效率。

其中大名鼎鼎的分布式消息队列服务`Kafka`就使用`sendfile`来优化效率，具体用法可参见其[官方文档](http://kafka.apache.org/documentation.html)。

### 优化策略

在普通进程中，要从磁盘拷贝数据到网络，其实是需要通过系统调用，进程也会反复在用户态和内核态切换，频繁的数据传输在此有效率问题。因此我们必须意识到 Linux 给我们提供了`sendfile`这样的系统调用，可以提高进程的数据传输效率。

## 后记

最后一章列举本文参考的过的书籍和项目，欢迎大家补充和讨论更多有关进程的知识。

## 参考书籍

* [理解 Unix 进程](http://book.douban.com/subject/24298701/)
* [Unix 编程艺术](http://book.douban.com/subject/1467587/)
* [Unix 环境高级编程](http://book.douban.com/subject/1788421/)
* [Go Web 编程](http://book.douban.com/subject/24316255/)
* [Go 并发编程实战](http://book.douban.com/subject/26244729/)

## 项目学习

* [Linux](https://github.com/torvalds/linux)
* [Go](https://github.com/golang/go)
* [Docker](https://github.com/docker/docker)
* [Run](https://github.com/runscripts/run)
* [GoByExample](https://github.com/mmcgrana/gobyexample)

## 感谢阅读！

