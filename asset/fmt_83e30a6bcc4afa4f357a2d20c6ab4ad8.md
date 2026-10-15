
### 硬件规格
- Dual Intel Xeon 2.4 GHz 533 FSB
- 512 MB DDR ECC Max: 12GB
- 36 GB 10K rpm SCSI
- 3 Hot-Swap SCSI Drive Bays
- CD, Floppy
- Dual Gig, VGA onboard
- Raid optional

### ASA Colocation
$50 per month for
- 1U Rack - 20 GB/month

### ASA Colocation Special
First month of colocation free.*

### Storage Solutions
- IDE, SCSI, Fiber RAID solutions
- TB storage options
- 3Ware, Promise, Adaptec, ICP-Vortex, LSI, CMD, Chaparral, Mylex controllers
- JMR, Kingston/Storcase solutions

### Clusters
- Rackmount and Desktop nodes
- HP, Intel, 3Com, Cisco switches
- KVM or Cyclades Terminal Server
- APC or Generic racks
- All systems installed and tested with user’s choice of Linux distribution [free]. ASA Colocation—$50 per month

## ASA Computers, Inc.
- 1-800-REAL-PCS
- 2354 Calle Del Mundo, Santa Clara, CA 95054
- TEL: (408) 654-2900 • FAX: (408) 654-2910
- E-MAIL: sales@asacomputers.com
- Free delivery in Silicon Valley*
- Open on Sat. too—10 to 1

![](img/3e9d313887e2c1cabeb5043769cbf08f_54_5.png)

## www.asacomputers.com
www.b2bforsale.com

## 使用 `ioctl` 控制硬件

一旦你学会 `ioctl` 系统调用，你就能检查以太网链路灯的状态以及关于硬件的其他各种但重要的事实。

**作者 LISA CORSETTI**

几年前的某段时间，我有一台在工作和家里都使用的笔记本电脑。为了简化网络配置并且不必根据所在位置手动更改，我决定在两个地方都使用 `DHCP`。它在工作场所是标准配置，所以我在家里实现了一个 `DHCP` 服务器。这工作得很好，除了在不插入任何网络的情况下启动系统时。当我这样做时，笔记本电脑在继续启动过程的其余部分之前花费了大量时间尝试寻找 `DHCP` 服务器而未成功。

我得出结论，这个延迟时间的理想解决方案是让系统以以太网接口关闭状态启动，并且只有在电缆连接到集线器时才启动，即当以太网接口上有链路灯时。实现这一目标的最佳方式似乎是让 shell 脚本调用一个程序，其返回码指示特定网络接口上是否建立了链路。就此开始了我寻找确定我的 `10/100Base-T` 接口链路状态的方法的探索。

由于没有做过太多低级 Linux 编程，花了我一些时间才发现这种与设备驱动程序的大多数交互通常是通过 `ioctl` 库调用完成的（I/O 控制的缩写），原型在 `sys/ioctl.h` 中：

```
int ioctl(int, int, ...)
```

第一个参数是文件描述符。由于 Linux 中的所有设备都像文件一样访问，通常使用的文件描述符是使用要交互的设备作为目标打开的文件描述符。在以太网接口的情况下，`fd` 只是打开的套接字。显然，没有必要将此套接字绑定到相关接口。

`ioctl.h` 中的第二个参数是一个整数，表示对 `ioctl` 的特定请求的标识号。请求本质上必须因设备而异。例如，你可以设置串行设备的速度，但不能设置打印机设备。当然，网络接口有一组特定的命令。

附加参数是可选的，并且可能因设备上的 `ioctl` 实现而异。据我所知，第三个参数始终存在，我还没有找到超过第三个参数的情况。这个第三个参数通常似乎是指向结构的指针。这允许在两个方向传递任意数量的数据，数据由指针所指的结构定义，只需传递指针即可。

`ioctl` 工作方式的基本示例显示在以下简单的程序中，该程序检查串行端口上的一个信号状态：

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

此程序打开一个 `tty`（串行端口），然后调用 `ioctl`，参数为串行端口的 `fd`、命令 `TIOCMGET`（列为获取调制解调器位的状态）和一个指向结果返回的整数的指针。

然后检查 `ioctl` 结果，以查看请求处理过程中是否出错。如果没有问题，我们通过与 `TIOCM_DTR` 进行与运算来检查返回的值。此步骤产生 `true` 或 `false`，分别是非零或零。

使用 `ioctl` 用于以太网驱动程序的过程类似。`ioctl` 调用中用于套接字 `ioctl` 调用（其中 `fd` 是套接字句柄）的第三个参数通常是指向 `ifreq`（接口请求）结构的指针。`ifreq` 结构的 `type` 声明可以在 `net/if.h` 中找到。

不幸的是，许多 `ioctl` 接口的文档很难找到，并且至少有三种不同的 `API` 用于访问网络接口。我最初使用 `MII`（媒体独立接口）方法编写了此程序。

## 即时验证 Web 服务，使用 Parasoft SOAPtest.

![](img/3e9d313887e2c1cabeb5043769cbf08f_56_0.png)

![](img/3e9d313887e2c1cabeb5043769cbf08f_56_1.png)

![](img/3e9d313887e2c1cabeb5043769cbf08f_56_2.png)

## （就像 1-2-3 一样简单。）

`Parasoft SOAPtest` 是第一个也是唯一一个能够让你即时验证 Web 服务是否正常工作的测试工具。

只需将 `SOAPtest` 指向你的 Web 服务 `WSDL` 文件。它会自动创建测试套件并运行对 Web 服务功能和负载能力的全面测试。

## 用于 SOAP 客户端开发的服务器仿真。

如果你正在开发客户端应用程序并且需要验证诸如信用卡处理之类的功能，通常 Web 服务服务器正在使用中或以其他方式无法用于测试。`Parasoft SOAPtest` 通过让你在几秒钟内仿真服务器响应并验证客户端功能来解决这个问题。

`SOAPtest` 还能让你快速创建用 `Java,™` `JavaScript,` 和 `Python` 编写的模板。

下载请访问 `www.parasoft.com/ij_11`。或致电 888-305-0041。

现支持 `WS-I` `Basic` `Profile` `1.0`

## 兼容性：
- 与任何 `SOAP` 兼容的实现兼容，包括 `Microsoft` 和 `IBM`
- `Windows` `2000/XP`
- `Linux`
- `Solaris`

`Parasoft` `Automated` `Error` `Prevention` `(AEP)` 解决方案和服务的一部分

![](img/3e9d313887e2c1cabeb5043769cbf08f_56_3.png)

在撰写本文时，在我的机器上安装了最新的内核后，我发现我必须添加 `ETHTOOL` 方法。

在添加 `ETHTOOL` 后，我随后修改了程序并将每个接口方法写成子例程。修改后的程序尝试一种方法，如果失败则尝试另一种方法。第三种方法早于 `MII` `API`，我还没有遇到需要它的机器，所以代码未包含在内。
