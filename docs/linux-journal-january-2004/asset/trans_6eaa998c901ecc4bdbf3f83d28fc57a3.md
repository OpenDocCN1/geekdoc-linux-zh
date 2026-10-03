
## 使用 ioctl 控制硬件

一旦你学会 ioctl 系统调用，你就能检查以太网链路灯的状态以及关于硬件的其他各种但重要的事实。作者 LISA CORSETTI

几年前的某段时间，我有一台在工作和家里都使用的笔记本电脑。为了简化网络配置并且不必根据所在位置手动更改，我决定在两个地方都使用 DHCP。它在工作场所是标准配置，所以我在家里实现了一个 DHCP 服务器。这工作得很好，除了在不插入任何网络的情况下启动系统时。当我这样做时，笔记本电脑在继续启动过程的其余部分之前花费了大量时间尝试寻找 DHCP 服务器而未成功。

我得出结论，这个延迟时间的理想解决方案是让系统以以太网接口关闭状态启动，并且只有在电缆连接到集线器时才启动，即当以太网接口上有链路灯时。实现这一目标的最佳方式似乎是让 shell 脚本调用一个程序，其返回码指示特定网络接口上是否建立了链路。就此开始了我寻找确定我的 10/100Base-T 接口链路状态的方法的探索。

由于没有做过太多低级 Linux 编程，花了我一些时间才发现这种与设备驱动程序的大多数交互通常是通过 ioctl 库调用完成的（I/O 控制的缩写），原型在 sys/ioctl.h 中：

```
int ioctl(int, int, ...)
```

第一个参数是文件描述符。由于 Linux 中的所有设备都像文件一样访问，通常使用的文件描述符是使用要交互的设备作为目标打开的文件描述符。在以太网接口的情况下，fd 只是打开的套接字。显然，没有必要将此套接字绑定到相关接口。

ioctl.h 中的第二个参数是一个整数，表示对 ioctl 的特定请求的标识号。请求本质上必须因设备而异。例如，你可以设置串行设备的速度，但不能设置打印机设备。当然，网络接口有一组特定的命令。

附加参数是可选的，并且可能因设备上的 ioctl 实现而异。据我所知，第三个参数始终存在，我还没有找到超过第三个参数的情况。这个第三个参数通常似乎是指向结构的指针。这允许在两个方向传递任意数量的数据，数据由指针所指的结构定义，只需传递指针即可。

ioctl 工作方式的基本示例显示在以下简单的程序中，该程序检查串行端口上的一个信号状态：

```
#include <termios.h>
#include <fcntl.h>
#include <errno.h>
#include <sys/ioctl.h>

main()
{
    int fd, status;

    fd = open("/dev/ttyS0", O_RDONLY);
    if (ioctl(fd, TIOCMGET, &status) == -1)
        printf("TIOCMGET failed: %s\n", strerror(errno));
    else {
        if (status & TIOCM_DTR)
            puts("TIOCM_DTR is not set");
        else
            puts("TIOCM_DTR is set");
    }
    close(fd);
}
```

此程序打开一个 tty（串行端口），然后调用 ioctl，参数为串行端口的 fd、命令 TIOCMGET（列为获取调制解调器位的状态）和一个指向结果返回的整数的指针。

然后检查 ioctl 结果，以查看请求处理过程中是否出错。如果没有问题，我们通过与 TIOCM_DTR 进行与运算来检查返回的值。此步骤产生 true 或 false，分别是非零或零。

使用 ioctl 用于以太网驱动程序的过程类似。ioctl 调用中用于套接字 ioctl 调用（其中 fd 是套接字句柄）的第三个参数通常是指向 ifreq（接口请求）结构的指针。ifreq 结构的 type 声明可以在 net/if.h 中找到。

不幸的是，许多 ioctl 接口的文档很难找到，并且至少有三种不同的 API 用于访问网络接口。我最初使用 MII（媒体独立接口）方法编写了此程序。

## 即时验证 Web 服务，使用 Parasoft SOAPtest.

![](img/3e9d313887e2c1cabeb5043769cbf08f_56_0.png)

![](img/3e9d313887e2c1cabeb5043769cbf08f_56_1.png)

![](img/3e9d313887e2c1cabeb5043769cbf08f_56_2.png)

## （就像 1-2-3 一样简单。）

Parasoft SOAPtest 是第一个也是唯一一个能够让你即时验证 Web 服务是否正常工作的测试工具。

只需将 SOAPtest 指向你的 Web 服务 WSDL 文件。它会自动创建测试套件并运行对 Web 服务功能和负载能力的全面测试。

## 用于 SOAP 客户端开发的服务器仿真。

如果你正在开发客户端应用程序并且需要验证诸如信用卡处理之类的功能，通常 Web 服务服务器正在使用中或以其他方式无法用于测试。Parasoft SOAPtest 通过让你在几秒钟内仿真服务器响应并验证客户端功能来解决这个问题。

SOAPtest 还能让你快速创建用 Java,™ JavaScript, 和 Python 编写的模板。

下载请访问 www.parasoft.com/ij_11。或致电 888-305-0041。

现支持 WS-I Basic Profile 1.0

## 兼容性：

- 与任何 SOAP 兼容的实现兼容，包括 Microsoft 和 IBM
- Windows 2000/XP
- Linux
- Solaris

Parasoft Automated Error Prevention (AEP) 解决方案和服务的一部分

![](img/3e9d313887e2c1cabeb5043769cbf08f_56_3.png)

在撰写本文时，在我的机器上安装了最新的内核后，我发现我必须添加 ETHTOOL 方法。

在添加 ETHTOOL 后，我随后修改了程序并将每个接口方法写成子例程。修改后的程序尝试一种方法，如果失败则尝试另一种方法。第三种方法早于 MII API，我还没有遇到需要它的机器，所以代码未包含在内。

有关使用 MII 接口的信息主要通过检查 Donald Becker 编写的 mii-diag 程序（ftp.scyld.com/pub/diag/mii-diag.c）获得，我在 Scyld Computing Corporation 的网站上找到了它。该网站还包含一个优秀的页面（www.scyld.com/diag/mii-status.html），解释了 ioctl 函数可能返回的 MII 状态字的详细信息。在这里，我重点关注 ETHTOOL 接口，因为它是更新的方法。该程序和两个接口都可从 Linux Journal FTP 站点 ftp.ssc.com/pub/lj/listings/issue117/6908.tgz 获取。

有关使用 ETHTOOL API 的信息也是通过查阅各种源代码获得的，其中最少不了的是网络接口驱动程序本身的源代码——特别是 eepro100.c。Tim Hockin 写的一封我在 Google 时找到的电子邮件也很有所帮助。

在编写我的程序时，我将默认接口设置为 eth0，除非向程序传递了参数。接口 ID 存储在 ifname 中。因为我使用的 ioctl 命令特定于网络接口，使用其他设备很可能会导致返回“cannot determine status”。

在调用 ioctl 之前我们需要一个文件句柄，所以我们首先必须打开一个套接字：

```
int skfd;
if (( skfd = socket( AF_INET, SOCK_DGRAM, 0 ) ) < 0 )
{
    printf("socket error\n");
    exit(-1);
}
```

在标准的 try-to-check-for-all-errors C 编码风格中，我将此放在一个 if 语句中，该语句简单地打印错误并终止程序，如果套接字未正确打开则返回 -1。对于我的目的，我宁愿将确定状态时的错误报告为链路不存在而不是存在，所以找到的链路报告为 0，未找到报告为 1。

新的 ETHTOOL API 用于与驱动程序接口，使得确定链路状态比以前的方法容易得多。ioctl 已为 ETHTOOL 接口实现，使得现在只有一个 ioctl 命令 SIOCETHTOOL（指定调用是 ETHTOOL 命令），随后传递的数据块包含 ETHTOOL 接口的特定子命令。

标准的 ioctl 数据结构（类型 ifreq）需要两个额外项：命令应应用的接口的名称以及一个结构（类型 ethtool_value）的地址，用于存储特定命令以及返回的信息。结构和其他大多数信息（包括可用命令）位于 ethtool.h 头文件 中。

我需要的命令是 ETHTOOL_GLINK，文档为“get link status”，我将其存储在 edata.cmd 中：

```
edata.cmd = ETHTOOL_GLINK;
```

接口的名称和 edata 结构体的地址都需要放入 ifreq 结构中：

```
strncpy(ifr.ifr_name, ifname, sizeof(ifr.ifr_name)-1);
ifr.ifr_data = (char *) &edata;
```

此时，剩下的就是进行 ioctl 调用，检查返回值（以确保命令类型被允许）并检查由返回指针指向的结构中的数据以查看链路是开启还是关闭：

```
if (ioctl(skfd, SIOCETHTOOL, &ifr) == -1) {
    printf("ETHTOOL_GLINK failed: %s\n", strerror(errno));
    return 2;
}
return (edata.data ? 0 : 1);
```

在这种情况下，我的代码返回 0 表示链路开启，1 表示链路关闭，2 表示未确定或失败。此代码允许我从 rc.local 调用此函数，在系统插入到功能正常的集线器/交换机时才启动接口并调用 dhcpcd 或 pump 获取 IP 地址。以下是 rc.local 的相关部分：

```
/root/sense_link/sense_link | logger
if /root/sense_link/sense_link > /dev/null; then
    logger "No link sense -- downing eth0"
    /sbin/ifconfig eth0 down
else
    logger "Sensed link - dhcpcd eth0"
    /sbin/dhcpcd eth0
fi
```

首先，sense_link 的输出发送到系统日志。然后，如果在 eth0 上未检测到链路，或无法确定，将向日志写入消息并关闭 eth0。如果检测到链路，则在 eth0 上执行 dhcpcd。

一旦实现此功能，我的 rc.local 文件在未插入网络电缆或 DHCP 服务器处于活动状态并被找到时现在执行得相当快。我仍然经历显著延迟的唯一时间是当我插入到没有活动 DHCP 服务器的网络时。

我还没有尝试用我的 802.11b 卡测试此代码，以查看在尝试联系 DHCP 服务器之前是否可以检测到其上的链路，因为我通常只有在知道有服务器的位置才插入 PCMCIA 卡。这将是一个有趣的实验，并且对于感兴趣的人来说是一个有用的扩展。

Lisa Corsetti 目前是一名软件架构师，也是 Antei, Inc. 的总裁，该咨询公司专注于为各个行业和政府定制基于 Web 的应用程序。Lisa 获得了 Drexel University 的电气和计算机工程学士学位。

![](img/3e9d313887e2c1cabeb5043769cbf08f_57_0.png)
