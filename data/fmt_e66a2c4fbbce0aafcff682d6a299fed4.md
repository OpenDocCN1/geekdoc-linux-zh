
```c
/* daytime.c:
 *
 * Example daytime client, modified
 * to accept different port numbers:
 */

#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <errno.h>
#include <string.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <netdb.h>

/* This function reports the error and
 * exits back to the shell:
 */
static void
bail(const char *on_what) {
    if (errno != 0) {
        fputs(strerror(errno), stderr);
        fputs(": ", stderr);
    }
    fputs(on_what, stderr);
    fputc('\n', stderr);
    exit(1);
}

int
main(int argc, char **argv) {
    int z;
    char *srvr_addr = NULL;
    char *srvr_port = "9009";
    struct sockaddr_in adr_srvr; /* AF_INET */
    int len_inet;                /* length */
    int s;                       /* Socket */
    char dtbuf[128];             /* Date/Time info */

/*
 * Use a server address from the command
 * line, if one has been provided.
 * Otherwise, this program will default
 * to using the arbitrary address
 * 127.0.0.1:
```

## 接下来是什么

在本章中，你查看了服务器所扮演的角色。你看到了它与客户端有何不同，因为它必须调用 `listen(2)` 和 `accept(2)` 函数。

下一章将讨论主机名查找。截至本书此阶段，你一直将互联网地址限制为特定的 IP 号码。下一章将向你展示如何除了 IP 号码之外还使用主机名。

## 主机名和网络名称查找

现在是正午时分，你上午的会议和问题的战斗暂时平息了。隔板的寂静被你带来的棕色纸袋午餐的噼啪声所破坏。你的 `Netscape` 浏览器在一整个上午处于最小化状态待命后，重新活跃起来。你敲了几下键盘 `http://206.43.198.67` 并按下了 `ENTER`。嗯？

这张图有什么问题？它是 IP 号码 `206.43.198.67`，不是吗？毕竟，那是哪个网站？你很可能知道这是 `www.lwn.net` 网站，在那里你可以获取 Linux 周刊（至少在写作本书时是这样）。

你在工作中的同事不会让你从 `ftp` 站点 `152.2.254.81` 获取一些源代码，对吧？相反，他会让你从 `sunsite.unc.edu` 进行 `ftp` 传输。你知道，IP 号码并不容易记住。在本章中，你将学习：

- 如何确定你的本地主机名
- 如何将主机名解析为 IP 号码
- 如何将 IP 号码解析为主机名

完成本章后，你将能够在客户端和服务器程序中使用主机名或 IP 号码。

## 理解对名称的需求

人类更喜欢使用和记忆名称，而不是 IP 号码。名称实际上为我们解决了网络世界中的许多问题：

- 它们为站点提供了对人类友好的引用。
- 它们允许 IP 号码改变，而名称保持不变。
- 它们允许为同一主机或服务提供多个 IP 号码作为可能性。

你已经理解，名称提供了对 IP 号码更简单的引用。然而，第二点是，名称可以保持固定，但允许主机的 IP 号码改变。由于网络变化、`ISP` 变化、设备变化等原因，IP 号码经常改变。只要你记住互联网站点的名称，你就不必担心带你到达那里的实际 IP 号码是什么。

最后一点很容易被忽视。查找 `ftp.redhat.com`（在写作时）产生了两个 IP 号码：

- `208.178.165.228`
- `206.132.41.212`

无论这两个 IP 号码是指向同一个 `ftp` 主机还是为了负载均衡目的的两个不同的镜像站点都无关紧要。事实是，通过使用这两个 IP 号码中的任意一个，你都可以获取你想要的文件。

这个引言引导你进入本章的主题：名称解析。首先，你将学习如何查询本地系统以获取有关其本身的信息。然后，你将学习如何使用远程主机名称，查找它们，并将它们转换为 IP 号码。

## 使用 uname(2) 函数

一个有用的函数是 `uname(2)` 函数。此函数告诉你的程序一些关于其执行所在系统的信息。此函数的函数原型如下：

```c
#include <sys/utsname.h>
```

```c
int uname(struct utsname *buf);
```

该函数将信息返回到结构 `buf` 中。成功时返回的值为零，报告错误时返回 -1。外部变量 `errno` 将包含错误的原因。

结构 `struct utsname` 定义如下：

```c
#include <sys/utsname.h> /* defines the following structure */

struct utsname {
    char    sysname[SYS_NMLN];
    char    nodename[SYS_NMLN];
    char    release[SYS_NMLN];
    char    version[SYS_NMLN];
    char    machine[SYS_NMLN];
    char    domainname[SYS_NMLN];
};
```

结构成员在表 9.1 中进行了详细说明。

**表 9.1: utsname 结构成员**

| 成员 | 描述 |
| :--- | :--- |
| `sysname` | 这表示正在使用的操作系统。对于 Linux，该值是 C 字符串 "Linux"。 |
| `nodename` | 这表示机器的网络节点主机名。 |
| `release` | 操作系统发行版。例如，对于内核发行版 2.2.10，返回 C 字符串 "2.2.10"。 |
| `version` | 操作系统版本。对于 Linux，这代表内核构建的版本号、日期和时间戳。 |
| `machine` | 这表示主机的硬件类型。例如，"i686" 代表 `Pentium` CPU。 |
| `domainname` | 这返回主机的 `NIS/YP` 域名。 |

**注意**

`NIS/YP`（网络信息服务）超出了本书的范围。`NIS` 为网络中的一组主机提供集中式信息管理。例如，它允许集中管理用户、组和密码。

列表 9.1 中显示了一个简单的程序，允许你测试 `uname(2)` 返回的值。此程序调用 `uname(2)`，然后显示结构 `utsname` 中返回的信息内容。

**列表 9.1: uname.c—用于 uname(2) 的简单测试程序**
