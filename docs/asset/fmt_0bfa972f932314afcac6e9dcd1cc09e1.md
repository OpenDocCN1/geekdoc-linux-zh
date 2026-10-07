
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/select.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

#define SIZE 1024
#define STDIN 0
#define ECHO_PORT 2013

int main(int argc, char *argv[]) {
    int sockfd;
    int nread;
    int len;
    struct sockaddr_in serv_addr;
    struct sctp_sinfo sinfo;
    fd_set fd_set;
    char buf[SIZE];

    if (argc != 2) {
        fprintf(stderr, "usage: %s\n", argv[0]);
        exit(1);
    }
    /* 创建套接字 */
    sockfd = socket(AF_INET, SOCK_STREAM, IPPROTO_SCTP);
    if (sockfd < 0) {
        perror("socket");
        exit(1);
    }
    /* 连接服务器 */
    serv_addr.sin_family = AF_INET;
    serv_addr.sin_addr.s_addr = inet_addr(argv[1]);
    serv_addr.sin_port = htons(ECHO_PORT);

    if (connect(sockfd, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) < 0) {
        perror("connect to server");
        exit(1);
    }
    printf("连接到 %s\n", argv[1]);
    while (1) { /* 等待消息和控制台 */
        FD_ZERO(&fd_set);
        FD_SET(STDIN, &fd_set);
        FD_SET(sockfd, &fd_set);
        printf("等待中...\n");
        select(-1, &fd_set, NULL, NULL, NULL);
        if (FD_ISSET(sockfd, &fd_set)) {
            printf("从服务器读取的消息:\n");
            nread = read(sockfd, buf, SIZE);
            if (nread < 0) {
                perror("read");
            } else if (nread == 0) {
                close(sockfd);
                exit(0);
            } else {
                printf("%s\n", buf);
            }
        }
        if (FD_ISSET(STDIN, &fd_set)) {
            printf("从用户读取:\n");
            nread = read(STDIN, buf, SIZE);
            if (nread < 0) {
                perror("read");
            } else {
                write(sockfd, buf, nread);
            }
        }
    }
}
```

## 深度解析

## 2. chat_server.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <strings.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>

#include <netinet/tcp.h>

#define BUF_SIZE 1024
char buf[BUF_SIZE];
#define CHAT_PORT 2013

int main(int argc, char *argv[]) {
    int sockfd, client_fd;
    int read, len;
    struct sockaddr_in serv_addr, client_addr;
    struct sctp_scrdvinfo info;
    int flags;
    struct sctp_event_subscribe events;
    sctp_assoc_t assoc_id = {0};

    /* 创建端点 */
    sockfd = socket(AF_INET, SOCK_PACKET, IPPROTO_SCTP);

    if (sockfd < 0) {
        perror(NULL);
        exit(2);
    }

    /* 绑定地址 */
    serv_addr.sin_family = AF_INET;
    serv_addr.sin_addr.s_addr = htonl(INADDR_ANY);
    serv_addr.sin_port = htons(CHAT_PORT);
    if (bind(sockfd, (struct sockaddr *)&serv_addr, sizeof(serv_addr))) {
        perror("bind\n");
        exit(1);
    }

    /* 监听 */
    listen(sockfd, 5);
    printf("Listening\n");

    for (;;) {
        len = sizeof(client_addr);
        read = sctp_recvmsg(sockfd, (struct sockaddr *)&client_addr, &len, &flags);
        if (read > 0) {
            printf("Got a read of %d bytes\n", read);
            write(1, buf, read);
            /* 发回给所有关联 */
            bzero(&info, sizeof(info));
            info.info_flags = SCTP_SENDALL;
            sctp_send(sockfd, buf, read, (struct sockaddr *)&client_addr, 1, &info, 0);
        }
    }
}

// (注：OCR文本在 main 之前包含碎片代码)
// bzero(&events, sizeof(events));
// events_scp_data_in_event = 1;
// if (setsockopt(sockfd, IPPROTO_TCP, SCTP_EVENTS, &events, sizeof(events))) {
//     perror("set sockopt\n");
// }

`MPI`（消息传递接口，www.mpi-forum.org） 是分布式系统中并行程序进程间通信的事实标准（维基百科）。它没有规定应该使用哪种传输协议，尽管 `SCPTP` 在过去很常见。

Humaima Kaimal 在他的硕士论文中使用 `SCPTP` 作为传输协议，并由于 `SCPTP` 基于消息的特性以及在关联内对流的使用，获得了可靠的结果。这些示例表明，`SCTP` 被用于各种对可靠性敏感的场景，以获得优于 `TCP` 和 `UDP` 传输的优势。

## 结论

本系列涵盖了 `SCPTP` 的基础知识。有很多选项可以详细控制 `SCPTP` 栈的行为。

目前正在进行将安全模型绑定到 `SCPTP` 的工作，例如，可以运行 `SCPTP`。此外正在进行不同语言的 `SCPTP` 绑定工作，例如 Java 实现。`SCTP` 不会让 `TCP` 和 `UDP` 消失，但这些文章表明它具有可以使应用程序更可靠、更安全的特征。

当然，`SCTP` 并不是唯一的协议。与其他协议的比较可以参考“除 `SCPTP` 以外的传输协议调查”，http://www.mpi-forum.org/Public_Comm_Docs/Documents/2005/draft-gftdr-survey.pdf。这表明 `SCPTP` 与许多可能的替代方案并肩齐，因此你可能想在下一个网络项目中考虑它！

Jan Hemingway 是蒙特利尔大学的高级研究员。他一直在使用 Linux 内核 0.98。他撰写过许多论文，并在许多技术主题上进行过，过去六年来一直专注于网络编程。他的网站是 jan.home

78 | 2007年11月 | www.linuxjournal.com

## LISA'07
第21届大型安装系统管理会议

查看系统管理领域正在发生什么！

LISA '07 提供目前最深入、最实用的系统管理培训！

- 由领域专家进行 6 天培训，包括：
- Tom Lemoncelli：关于系统管理员的时间管理
- Steve VanDevender：关于高容量电子邮件系统设计
- Eleen Frisch：关于在生产环境环境中管理 Linux
- Faisal N. Jawdat：关于 Ruby、Rails 和 Capistano 介绍

- 为期 3 天的技术课程，包括：
由 John Strassner（摩托罗达 Fellow、摩托罗达研究实验室自动网络与通信副总裁）主的主旨演讲：自动管理：HAL 9000 遇上 Gene Donnenberry
行业领袖受邀演讲将讨论重要且及时的话题，包括：
- Bruce Moxon, NetApp，“一种面向服务的数据网格：超越可扩展的存储虚拟化”
- Erik Nygren, Akamai Technologies，“在 Akamai 进行可扩展网络操作的经验”
- Kenneth C. Brill, Uptime Institute，“摩尔定律的经济崩溃”

审稿论文、快速上手轨道、Guru 会议、供应商展览、工作研讨会、BoFs、WiPs 等！

2007年11月11-16日

达拉斯

由 USENIK & [sage] 赞助 | 10月19日前注册可节省费用！www.usenik.org/lisa07/lj

# 罗马法则与多核 CPU 的快速处理

### 利用多核心和发现同步问题的某些实用方法。

ROMAN SHAPOSHNIK

计算机运行得像冷冬天的糖糖一样慢，而且多年来一直这样。硬件行业正在改进工作，但除非软件行业跟进并采取行动，否则计算机将不会变得更快。处理能力不再仅仅取决于 GHZ（主频），而更多取决于这些系统需要适应的多个核心。

我将大胆地假设我自己的多核趋势法则：芯片上的核心数量每三年将翻一倍。这一预测是否能像戈登·摩尔那样准确还有待观察，但目前看起来很不错。随着 Intel 和 AMD 引入更多核心，以及 Sun 推得更远，软件行业必须问的首要问题是：所有这些执行对我们有用吗？我的坚定观点是，我们还没有准备好。需要发明一种新的范式，而我们并不真正知道它长什么样。我们知道的是自面向对象（OO）瓶颈出现以来软件开发最大的变化，而现在就是并发。

硬件并行的第一层是渗透你操作系统的内核。而且，我只知道如何应对挑战：Solaris 和 Linux。如果你有任何 OS X——或者像日子那样的 Windows——那么我有两个词可以形容：“256 处理器”和“工厂调度器”。现在，一个能够高效管理大量进程的内核，取决于你拥有大量进程的能力。对于本文的其余部分，我假设你拥有一台运行 Linux 2.6 的双核系统，并安装了 Sun Studio 且已添加到 PATH 中如下：

`PATH=/opt/sun/studio12/bin:$PATH`

我的目标是解释你可以采取哪些实践来教授多核心技巧。有一些基础策略可以迭代以添加并行性：

1. 识别并行性。
2. 表达并行性。
3. 测量和观察。

而且，尽管前两步看起来是常识，但我无法不强调第三步的重要性。并行编程非常困难且充满了意外之外的性能问题，除了用数据证明，没有其他方法可以验证你的代码是否变快了。消息是事实并非完全如此。如果你主要为 Intel 系统开发，可以使用与 FFMEM 相同的 `START_TIMER`/`STOP_TIMER` 进行微基准测试。

```c
START_TIMER
do_starting();
STOP_TIMER(do_starting, "stop_tag")
```

此外，还有 Sun Studio Analyzer 用于观察行为。你可以使用像 Vftune 这样的工具，但确保性能回归测试包含在运行流程中。识别应用程序中的并行性通常从寻找具有数据并行特征的地方开始，并配置调度模型将两者结合起来。这在处理大型太阳或静态数据集（如音频、视频和图像处理、游戏引擎和渲染软件）时同样有用。相反，任务并行性最适用于发生分界计算的情况（例如国际象棋士兵

# 广告商索引

当一组任务被要求进行计算时，如果其中一个找到了解决方案，就不需要等待其他任务。

一旦你确定了应用程序中所有潜在的并行源，你就需要决定使用什么编程语言来表达它。对于使用 C 或 C++ 编写的应用程序，最常用的方法是使用 POSIX 线程（POSIX threads）进行显式并行化。这种方法被认为适用于那些重视简单性的资深程序员。然而，考虑到它的复杂性以及它已不再是唯一的选择，我将跳过它。

让我们来看这段示例代码，它是一个计算 2 到 N 之间有多少个质数的非常简单的例例程：

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <omp.h>
/* plflag(v) == 1 且仅当 v 是质数时成立 */
char *plag;
int is_prime(int n) {
    int i;
    int bound = floor(sqrt(n)) + 1;
    for (i = 2; i < bound; i++) {
        if (v % i == 0) {
            plag[v] = 0;
        }
    }
    return 0; /* v 不是质数 */
}
main(int argc, char **argv) {
    int i;
    int total = 0;
    int n = atoi(argv[1]);
    int *primes; /* 质数数组 */
    plag=(char*)malloc(n);
    for (i = 2; i < n; i++) {
        if (is_prime(i)) { /* 测试开始！ */
            primes[i] = 1;
            total++;
        }
    }
    printf("number of prime numbers between 2 and %d: %d\n", n, total);
    return 0;
}
```
