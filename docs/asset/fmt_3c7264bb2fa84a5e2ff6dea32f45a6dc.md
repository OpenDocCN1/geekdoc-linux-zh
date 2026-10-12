
# Linux Socket 编程示例

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

- 何时以及如何使用 `inetd` 守护进程并管理配置文件 `/etc/inetd.conf`。

- 服务器如何获取关于客户端的凭据信息，以及在使用本地 socket 时如何将文件描述符传递给客户端程序。

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

# 作者简介

`Warren W. Gay` 是加拿大多伦多 `Mackenzie Financial Corporation` 的监督人员。在那里，他监督一支管理 `Mackenzie` 投资管理系统 (`IMS`) 的小型程序员团队。`Warren` 也是 *《Sams 24 小时教你 Linux 编程》* 的作者。

`Warren` 自 1980 年起从事专业编程，使用过许多汇编语言、`PL/I`、`C` 和 `C++`。他自 1986 年起为 `UNIX` 编程，并于 1994 年开始为 `Linux` 编程。`Linux` 使他能够贡献软件包，如 `ftfbackup` 程序和对流行的 `wavplay` 程序的重写。这些以及他的其他 `Linux` 软件包可以在 `sunsite.unc.edu` 及其镜像 FTP 站点找到。

业余无线电是 `Warren` 的一项爱好。他持有高级业余无线电执照，偶尔使用 75 米波段，呼号为 `VE3WWG`。1991 年 8 月 3 日，使用 2 米波段，他通过 PC 和分组无线电设备与苏联 `MIR` 空间站上的 `Musa Manarov`（呼号 `U2MIR`）建立了联系。

`Warren` 与其妻子 `Jacqueline` 以及他的三个孩子 `Erin`、`Laura` 和 `Scott` 住在加拿大安大略省的圣凯瑟琳斯。

## 题词

本书献给我深爱的妻子杰基（`Jackie`）、我的女儿艾琳（`Erin`）和劳拉（`Laura`），以及我的儿子斯科特（`Scott`）。正是得益于他们共同的耐心与支持，本书才得以成书。

## 致谢

首先，感谢布莱恩·吉尔（`Brian Gill`）的热情与支持，这帮助启动了该项目。同时也感谢托德·格林（`Todd Green`）接替布莱恩担任收购编辑，以及劳拉·布彻（`Laura Bulcher`）担任开发编辑。我还要感谢威廉·雷（`William Ray`），他作为技术编辑，充满热情并付出了巨大努力。

感谢马加林美国公司（`Macmillan USA`）的那些员工，他们花费了无数小时完成出版一本书过程中所需的各项事务。正如生活中常有的那样，成就的达成离不开众人的努力。

我还要感谢麦肯齐金融公司（`Mckenzie Financial Corporation`）的员工，在我兼顾工作职责与在家写作时给予了我支持。特别是，我要感谢卡罗尔·彭哈利（`Carol Penhale`），允许我在真正需要的时候安排假期。我还要感谢亚历克斯·洛维特（`Alex Lowitt`）为麦肯齐员工租赁笔记本电脑所做的努力。我使用的那台笔记本电脑极大地推动了我的写作进程。

向达里·乌班基（`Darie Urbanky`）致以热烈的谢意，感谢他在 `Sun` 公司的 `Solaris` 系统下帮我测试了几个程序示例。对于我其他各位朋友，请接受我普遍的谢意，感谢你们的鼓励与持续支持。

## 告诉我们你的想法！

作为本书的读者，你是我们要紧的批评者和评论者。我们重视你的意见，希望了解我们哪些方面做得对，哪些方面可以做得更好，你希望我们出版哪些领域的内容，以及任何你愿意转达给我们的其他智慧之言。

作为 `Que` 的副出版人，我欢迎你的评论。你可以通过传真、电子邮件或信件告诉我你喜欢或不喜欢这本书的哪些方面——以及我们可以做什么来让我们的书更出色。

请注意，我无法帮你解决与本书主题相关的技术问题，并且由于我收到的邮件数量巨大，我可能无法回复每一封信息。

当你写信时，请务必附上本书的书名和作者，以及你的姓名和电话或传真号码。我会仔细阅读你的评论，并将其分享给参与本书工作的作者和编辑。

传真：`317-581-4666`

电子邮件：`quetechnical@macmillanusa.com`

邮寄：副出版人，编程

`Que`

`201 West 103rd Street`

`Indianapolis, IN 46290 USA`

## 引言

关于计算机网络主题已经出版了许多书籍。虽然其中许多都是高级程序员的优秀资源，但对于那些只想了解如何使用网络的初学者来说，它们往往太深了。为什么要让潜在的驾驶员理解其汽车背后的理论呢？
