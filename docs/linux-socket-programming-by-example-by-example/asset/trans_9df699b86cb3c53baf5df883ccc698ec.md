

# Linux Socket 编程

## 实例详解

```c
in = fopen(pathname, "r");
if (in == NULL) {
    fprintf(stderr,
    "%s: opening %s for read",
    progname, pathname);
    exit(1);
}
#include <sys/utsname.h>
#include <sys/socket.h>

int accept(int s, struct sockaddr *addr,
           int *len);
int inet_aton(const char *cp, struct in_addr *addr);
unsigned long inet_network(const char *cp);
unsigned long inet_lshiftb(const char *cp, int lsb);
unsigned long inet_makenetmask(int hostmask, int subnet);
unsigned long inet_netof(unsigned long x);
unsigned long inet_hostmask(unsigned long x);
unsigned long inet_lshiftb(unsigned long x, int n);
struct in_addr *inet_lshiftb(const char *cp, int n);
struct in_addr *inet_makeadr(const char *cp,
                              int hostmask, int subnet);
```

![](img/961a0296fe36074690a9847b79332eff_0_0.png)

![](img/961a0296fe36074690a9847b79332eff_0_1.png)

![](img/961a0296fe36074690a9847b79332eff_0_2.png)

![](img/961a0296fe36074690a9847b79332eff_0_3.png)

## 我们对你所做的假设

一本关于 Linux socket 编程的书并不是一本纯粹的网络理论书。为了能让你在 socket 编程领域学到最多的知识，我们紧扣主题，旨在为你提供最陡峭的学习曲线，同时不浪费你的时间和金钱。

### 我们假设你知道什么

- C 编程语言以及如何在 Linux 下链接这些程序。
- 关于在 Linux（或 UNIX）下进行编程的一些知识——例如 `open(2)`、`read(2)` 和 `write(2)` 等。
- 对捕获和处理 Linux 下信号的基本理解。一些演示程序中使用了 `signal(2)` 函数。
- 关于 TCP/IP 网络的基本概念。

### 我们期望你学到什么

- 如何使用 `socketpair(2)` 和 `shutdown(2)` 函数，并介绍如何在 socket 上执行 I/O。
- 地址族以及如何构建和初始化 socket 地址结构。
- 如何使用无连接模式与 UDP 数据报通信。涵盖了优缺点，并附有执行数据报 I/O 的示例。
- 通过讨论内核监听队列来使用 `listen(2)` 和 `accept(2)` 函数。图表和示例程序还将向你展示服务器设计的相关知识。
- 如何处理为多个客户端连接提供服务的挑战。你将学会使用 `fork(2)` 和 `select(2)` 方法作为解决方案。
- 何时以及如何使用 inetd 守护进程并管理配置文件 `/etc/inetd.conf`。
- 服务器如何获取关于客户端的凭据信息，以及在使用本地 socket 时如何将文件描述符传递给客户端程序。

# Linux Socket 编程

## 实例详解

Que
201 West 103rd Street
Indianapolis, Indiana 46290

Warren W. Gay

# Linux Socket 编程 实例详解

版权所有 © 2000 Que®
保留所有权利。未经出版商书面许可，不得以任何形式（包括电子、机械、复印、录音或其他形式）复制、存储在本检索系统中或传输本书的任何部分。对于本书所含信息的使用，不承担专利责任。尽管在本书的编写过程中已采取了所有预防措施，但出版商和作者不对错误或遗漏承担责任。亦不承担因使用本书所含信息而导致的任何损害赔偿的责任。

- 国际标准书号：0-7897-2241-0
- 美国国会图书馆图书分类号：99-66454
- 美国印刷
- 第一次印刷：2000年4月

## 商标

本书中提到的所有已知商标或服务商标均已适当大写。Que 无法保证此信息的准确性。本书中术语的使用不应被视为影响任何商标或服务商标的有效性。

Linux® 是 Linus Torvalds 的注册商标。Red Hat® Linux™ 是 Red Hat Software 的注册商标。

## 警告与免责声明

我们已尽力使本书尽可能完整和准确，但不暗示任何保证或适用性。所提供的信息基于“原样”基础。作者和出版商对于因使用本书所含信息而导致的任何损失或损害，对任何个人或实体均不承担任何责任。

| 角色 | 姓名 |
| :--- | :--- |
| **副出版人** | Tracy Dunkelberger |
| **收购编辑** | Todd Green |
| **开发编辑** | Laura Bulcher |
| **主管编辑** | Thomas F. Haynes |
| **项目编辑** | Karen S. Shields |
| **文字编辑** | Victoria Elzey |
| **索引编辑** | Amir Burki |
| **校对员** | Jeanne Clark |
| **技术编辑** | William Ray |
| **团队协调员** | Cindy Teeters |
| **媒体开发人员** | Jay Payne |
| **内部设计师** | Karen Ruggles |
| **封面设计师** | Rader Design |
| **版权** | Eric Børgert |
| **制作** | Lisa England<br>Steve Geiselman<br>Liz Johnston |

# 内容一览

简介 ......................................... 1

**第 1 部分：基础 Socket 概念** .................................................... 5

- 1. 介绍 Socket ..................................... 7
- 2. 域和地址族 .......................... 35
- 3. 地址转换函数 ........................... 65
- 4. Socket 类型和协议 ............................. 93
- 5. 将地址绑定到 Socket ......................... 115
- 6. 无连接导向协议 ..................... 133
- 7. 面向连接的客户端协议 ............ 159
- 8. 面向连接的服务器协议 ............ 183
- 9. 主机名和网络名查找 .................. 203

**第 2 部分：高级 Socket 编程** .................................... 227

- 10. 在 Socket 上使用标准 I/O ........................ 229
- 11. 并发客户端服务器 ............................ 269
- 12. Socket 选项 ....................................... 305
- 13. 使用 UDP 广播 ................................ 329
- 14. 带外数据 ..................................... 349
- 15. 使用 inetd 守护进程 .............................. 379
- 16. 网络安全编程 ......................... 393
- 17. 传递凭据和文件描述符 ............... 427
- 18. 一个实用的网络项目 .......................... 473

**附录** .................................................... 505

- A. Socket 函数快速参考 ..................... 507
- B. Socket 相关结构参考 .................. 519
- C. 有用的网络表格 ............................... 525

术语表 ................................................. 529

索引 ...................................................... 537

# 目录

- 简介 1
- **第 1 部分 基础 Socket 概念** 5
  - 1   介绍 Socket  7
    - 简略的历史介绍 8
    - 理解 Socket 9
    - 定义 Socket 9
    - 使用 Socket 10
    - 引用 Socket 11
    - Socket 与管道的比较 12
    - 创建 Socket 13
    - 示例中使用 socketpair(2) 14
    - 运行演示程序 16
    - 在 Socket 上执行 I/O 17
    - 关闭 Socket 21
    - shutdown(2) 函数 22
    - 关闭 Socket 的写入 22
    - 处理重复的 Socket 23
    - 关闭 Socket 的读取 24
    - 了解何时不使用 shutdown(2) 24
    - 编写一个客户端/服务器示例 24
  - 2   域和地址族 35
    - 无名 Socket 36
    - 匿名调用 36
    - 生成地址 36
    - 理解域 36
    - 构建 Socket 地址 37
    - 检查通用 Socket 地址 37
    - 构建本地地址 38
    - 构建传统本地地址 39
    - 构建抽象本地地址 44
    - 构建互联网 (IPv4) Socket 地址 47
    - 理解网络字节序 49
    - 执行字节序转换 50
    - 初始化通配互联网地址 ... 51
    - 初始化特定互联网地址 ... 52
    - 指定 X.25 地址 ... 55
    - 指定其他地址族 ... 58
    - AF_UNSPEC 地址族 ... 61
  - 3   地址转换函数 ... 65
    - 互联网 IP 编号 ... 66
    - 互联网地址类别 ... 66
    - 理解子网掩码值 ... 67
    - 分配 IP 地址 ... 72
    - 私有 IP 编号 ... 72
    - 保留 IP 编号 ... 73
    - 操作 IP 编号 ... 73
    - 使用 inet_addr(3) 函数 ... 73
    - inet_aton(3) 函数 ... 77
    - 使用 inet_ntoa(3) 函数 ... 80
    - 使用 inet_network(3) ... 83
    - 使用 inet_inaddr(3) 函数 ... 85
    - 使用 inet_netof(3) 函数 ... 86
    - 使用 inet_makeadr(3) 函数 ... 87
  - 4   Socket 类型和协议 ... 93
    - 指定 Socket 的域 ... 94
    - 选择 PF_INET 或 AF_INET ... 94
    - 使用 PF_LOCAL 和 AF_LOCAL 宏 ... 95
    - 使用 socket(2) 函数 ... 96
    - 选择 Socket 类型 ... 96
    - 理解 SOCK_STREAM Socket 类型 ... 97
    - 理解 SOCK_DGRAM Socket 类型 ... 99
    - 理解 SOCK_SETPACKET Socket 类型 ... 100
    - 选择协议 ... 101
    - 使用 PF_LOCAL 和 SOCK_STREAM ... 102
    - 使用 PF_LOCAL 和 SOCK_DGRAM ... 103
    - 使用 PF_INET 和 SOCK_STREAM ... 103
    - 使用 PF_INET 和 SOCK_DGRAM ... 105
    - Socket 域和类型摘要 ... 106
    - 其他 Linux 支持的协议 ... 107
    - 研究其他协议 ... 109

