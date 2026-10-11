
# 接下来是什么

在本章中，你查看了服务器所扮演的角色。你看到了它与客户端有何不同，因为它必须调用 `listen(2)` 和 `accept(2)` 函数。

下一章将讨论主机名查找。截至本书此阶段，你一直将互联网地址限制为特定的 IP 号码。下一章将向你展示如何除了 IP 号码之外还使用主机名。

# 主机名和网络名称查找

现在是正午时分，你上午的会议和问题的战斗暂时平息了。隔板的寂静被你带来的棕色纸袋午餐的噼啪声所破坏。你的 Netscape 浏览器在一整个上午处于最小化状态待命后，重新活跃起来。你敲了几下键盘 `http://206.43.198.67` 并按下了 ENTER。嗯？

这张图有什么问题？它是 IP 号码 206.43.198.67，不是吗？毕竟，那是哪个网站？你很可能知道这是 `www.lwn.net` 网站，在那里你可以获取 Linux 周刊（至少在写作本书时是这样）。

你在工作中的同事不会让你从 `ftp` 站点 152.2.254.81 获取一些源代码，对吧？相反，他会让你从 `sunsite.unc.edu` 进行 `ftp` 传输。你知道，IP 号码并不容易记住。在本章中，你将学习：

- 如何确定你的本地主机名
- 如何将主机名解析为 IP 号码
- 如何将 IP 号码解析为主机名

完成本章后，你将能够在客户端和服务器程序中使用主机名或 IP 号码。

# 理解对名称的需求

人类更喜欢使用和记忆名称，而不是 IP 号码。名称实际上为我们解决了网络世界中的许多问题：

- 它们为站点提供了对人类友好的引用。
- 它们允许 IP 号码改变，而名称保持不变。
- 它们允许为同一主机或服务提供多个 IP 号码作为可能性。

你已经理解，名称提供了对 IP 号码更简单的引用。然而，第二点是，名称可以保持固定，但允许主机的 IP 号码改变。由于网络变化、ISP 变化、设备变化等原因，IP 号码经常改变。只要你记住互联网站点的名称，你就不必担心带你到达那里的实际 IP 号码是什么。

最后一点很容易被忽视。查找 `ftp.redhat.com`（在写作时）产生了两个 IP 号码：

- 208.178.165.228
- 206.132.41.212

无论这两个 IP 号码是指向同一个 `ftp` 主机还是为了负载均衡目的的两个不同的镜像站点都无关紧要。事实是，通过使用这两个 IP 号码中的任意一个，你都可以获取你想要的文件。

这个引言引导你进入本章的主题：名称解析。首先，你将学习如何查询本地系统以获取有关其本身的信息。然后，你将学习如何使用远程主机名称，查找它们，并将它们转换为 IP 号码。

# 使用 uname(2) 函数

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
| sysname | 这表示正在使用的操作系统。对于 Linux，该值是 C 字符串 "Linux"。 |
| nodename | 这表示机器的网络节点主机名。 |
| release | 操作系统发行版。例如，对于内核发行版 2.2.10，返回 C 字符串 "2.2.10"。 |
| version | 操作系统版本。对于 Linux，这代表内核构建的版本号、日期和时间戳。 |
| machine | 这表示主机的硬件类型。例如，"i686" 代表 Pentium CPU。 |
| domainname | 这返回主机的 NIS/YP 域名。 |

**注意**

NIS/YP（网络信息服务）超出了本书的范围。NIS 为网络中的一组主机提供集中式信息管理。例如，它允许集中管理用户、组和密码。

列表 9.1 中显示了一个简单的程序，允许你测试 `uname(2)` 返回的值。此程序调用 `uname(2)`，然后显示结构 `utsname` 中返回的信息内容。

**列表 9.1: uname.c—用于 uname(2) 的简单测试程序**

```c
/* uname.c:
 *
 * Example of uname(2):
 */

#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <errno.h>
#include <string.h>
#include <sys/utsname.h>

int
main(int argc, char **argv) {
    int z;
    struct utsname u_name;
    
    z = uname(&u_name);
    
    if ( z == -1 ) {
        fprintf(stderr, "%s: uname(2)\n",
                strerror(errno));
        exit(1);
    }
    
    printf( " sysname[] = '%s'\n",
            u_name.sysname);
    printf( " nodename[] = '%s'\n",
            u_name.nodename);
    printf( " release[] = '%s'\n",
            u_name.release);
    printf( " version[] = '%s'\n",
            u_name.version);
    printf( " machine[] = '%s'\n",
            u_name.machine);
    printf( " domainname[] = '%s'\n",
            u_name.domainname);
    
    return 0;
}
```

列表 9.1 中使用的步骤如下：

- 分配结构 `u_name` 以接收来自 `uname(2)` 的数据（第 15 行）。
- 在第 17 行调用 `uname(2)`。
- 检查并报告错误（第 19 行到第 23 行）。
- 报告返回的值（第 25 行到第 36 行）。

以下会话输出展示了如何编译和运行该程序。示例系统 lux 上程序的输出也作为一个示例包含在内（注意该系统未配置为使用 NIS）：

```sh
@lux
$ make uname
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type uname.c
gcc uname.o -o uname
```

![](img/961a0296fe36074690a9847b79332eff_217_0.png)

对程序进行的小改动是：

- 该程序现在接受命令行上的可选端口号作为第二个参数（第 60 行和第 61 行）。
- 移除了对 `getservbyname(3)` 的调用，因为端口号现在默认为 9999 或在命令行上明确给出。

以下会话展示了如何编译和测试客户端程序，针对一个宽泛地址的服务器：

```sh
@pepper
$ make daytime
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type daytime.c
gcc daytime.o -o daytime
@pepper
$ ./daytime 127.0.0.1 9999
Date & Time is: Sunday Aug 22 22:02:19 1999

@pepper
$ ./daytime 192.168.0.1 9999
Date & Time is: Sunday Aug 22 22:02:30 1999

@pepper
$
```

该会话演示了客户端程序如何成功从主机 pepper 上两个可能的 IP 地址调用同一个服务器。如果你的网络中有远程主机，请务必远程尝试该程序。

