
## 12.2.1 硬件调试探针

除了前面列出的组件外，您还应考虑某种类型的硬件辅助调试工具。这包括一个连接至主机（通常通过以太网）并通过板载调试连接器连接至目标系统的硬件探针。目前市面上有许多此类解决方案。我们将在第 14 章“内核调试技术”中详细探讨这一主题。

## 12.3 托管目标板

回顾图 12-1，您会注意到从目标嵌入式板到主机开发系统之间存在一条以太网连接。这并非绝对必要，事实上，一些较小的嵌入式设备没有以太网接口。然而，这是例外而非常态。在目标板上具备以太网连接的价值简直物超所值！

在开发内核时，您需要多次向嵌入式板编译并下载内核。许多嵌入式开发系统和引导加载程序都支持 TFTP，并假设开发者会使用它。TFTP 是一种用于在 TFTP 服务器和 TFTP 客户端之间传输文件的轻量级协议，类似于 FTP。

使用引导加载程序中的 TFTP 来加载内核将为您节省无数等待串行下载的时间，即使是在较高的串行波特率下也是如此。而且加载 ramdisk 可能花费更长的时间，因为 ramdisk 镜像根据需求可能增长到几十兆字节甚至更多。在配置和使用 TFTP 上投入的时间一定会得到回报，强烈建议采用。很少有设计在开发期间无法容纳一个以太网端口的空间，即使在生产阶段将其移除也是如此。

### 12.3.1 TFTP 服务器

在您的 Linux 开发主机上配置 TFTP 并不困难。当然，具体细节可能因您为开发工作站选择的 Linux 发行版而异。这里提供的指导方针基于 Red Hat 和 Fedora Core Linux 发行版。

TFTP 是一种 TCP/IP 服务，必须在您的工作站上启用。要启用 TFTP 服务，您必须指示服务器响应传入的 TFTP 数据包并启动您的 TFTP 服务器。在许多 Linux 发行版中，这是通过编辑 xinetd Internet 超级服务器使用的配置文件来实现的。例如，在 Red Hat 和 Fedora 桌面 Linux 发行版中，该文件为 /etc/xinetd.d/tftp。清单 12-4 包含来自 Fedora Core 2 开发工作站的 TFTP 配置，用于启用 TFTP 服务。为了适应页面排版，内容稍作重新排列。

**清单 12-4 TFTP 配置**

```
# default: off
# description: The tftp server serves files using the trivial
# file transfer protocol.  The tftp protocol is often used to
# boot diskless workstations, download configuration files to
# network-aware printers, and to start the installation process
# for some operating systems.

service tftp
{
    socket_type         = dgram
    protocol            = udp
    wait                = yes
    user                = root
    server              = /usr/sbin/in.tftpd
    server_args         = -c -s /tftpboot
    disable             = no
    per_source          = 11
    cps                 = 100 2
    flags               = IPv4
}
```

在此典型设置中，TFTP 服务已被启用（disable = no），并配置为提供位于此工作站 /tftpboot 目录中的文件。当 xinetd Internet 超级服务器接收到传入的 TFTP 请求时，它会查阅此配置并启动指定的服务器（/usr/sbin/in.tftpd）。由 *server_args* 指定的命令行参数会传递给 *in.tftpd* 进程。在这种情况下，-c 开关告知 *in.tftpd* 切换到指定目录（/tftpboot），而 -s 标志允许创建新文件。这对于从目标系统向服务器写入文件非常有用。

请查阅随您的桌面发行版提供的文档，以获取针对您环境的具体细节。

### 12.3.2 BOOTP/DHCP 服务器

在开发主机上拥有 DHCP 服务器可以简化嵌入式目标的配置管理。我们此前已说明了为什么在目标硬件上使用以太网接口是一个好主意。当 Linux 在目标板上启动时，它需要先配置以太网接口，该接口才真正有用。此外，如果您在目标板上使用 NFS 根挂载配置，Linux 需要在引导过程完成之前配置目标的以太网接口。我们在第 9 章“文件系统”中详细讨论了 NFS。

一般来说，Linux 在启动过程中可以使用两种方法来初始化其以太网/IP 接口：

- 在 Linux 内核命令行或默认配置中硬编码以太网接口参数
- 配置内核在启动时自动检测网络设置

出于显而易见的原因，后一种选择是最灵活的。DHCP 或 BOOTP 是您的目标和服务器用于实现网络设置自动检测的协议。关于 DHCP 或 BOOTP 协议的细节，请参见本章末尾的第 12.4.1 节。

DHCP 服务器控制其已配置管理的 IP 子网的 IP 地址分配，以及已配置参与该过程的 DHCP 或 BOOTP 客户端。DHCP 服务器监听来自 DHCP 客户端（如您的目标板）的请求，并在引导过程中将地址及其他相关信息分配给客户端。典型的 DHCP 交互过程（见清单 12-5）可以通过启动带有 -d 调试开关的 DHCP 服务器，并在目标机器请求配置时观察输出来进行检查。

**清单 12-5 典型的 DHCP 交互过程**

```
tgt> DHCPDISCOVER from 00:09:5b:65:1d:d5 via eth0
srv> DHCPOFFER on 192.168.0.9 to 00:09:5b:65:1d:d5 via eth0
tgt> DHCPREQUEST for 192.168.0.9 (192.168.0.1) from 00:09:5b:65:1d:d5 via eth0
srv> DHCPACK on 192.168.0.9 to 00:09:5b:65:1d:d5 via eth0
```

该序列以客户端（目标）传输广播帧尝试发现 DHCP 服务器开始。这就是所显示的 DHCPDISCOVER 消息所表示的内容。如果服务器已如此配置并启用，它将通过向客户端提供 IP 地址来响应。这由 DHCPOFFER 消息所证明。然后客户端通过本地测试该 IP 地址来响应。测试包括向 DHCP 服务器发送 DHCPREQUEST 数据包，如图所示。最后，服务器通过确认将 IP 地址分配给客户端来响应，从而完成目标的自动配置。

值得注意的是，正确配置的客户端会记住由 DHCP 服务器分配的最后一个地址。下次启动时，它将跳过 DHCPDISCOVER 阶段并直接进入 DHCPREQUEST 阶段，假设它可以复用服务器先前分配的相同 IP 地址。启动中的 Linux 内核不具备这种能力，每次启动时都会发出相同的序列。

配置主机的 DHCP 服务器并不困难。通常，我们的建议是查阅随您的桌面 Linux 发行版提供的文档。在 Red Hat 或 Fedora Core 发行版中，单个目标的配置条目可能如清单 12-6 所示。

**清单 12-6 DHCP 服务器配置示例**

```
# Example DHCP Server configuration
allow bootp;

subnet 192.168.1.0 netmask 255.255.255.0 {
  default-lease-time 1209600;   # two weeks
  option routers 192.168.1.1;
  option domain-name-servers 1.2.3.4;
  group {
    host pdnal {
      hardware ethernet 00:30:bd:2a:26:1f;
      fixed-address 192.168.1.68;
      filename "uImage-pdna";
      option root-path "/home/chris/sandbox/pdna-target";
    }
  }
}
```

这是一个简单的示例，仅用于展示您可以传递给目标系统的信息类型。目标的 MAC 地址与其分配的 IP 地址之间存在一对一的映射。除了固定的 IP 地址外，您还可以向目标传递其他信息。在此示例中，将默认路由器和 DNS 服务器地址传递给目标，以及一个您选择文件的文件名，和一个用于内核挂载 NFS 根的文件系统路径。该文件名可能被您的引导加载程序用于从 TFTP 服务器加载内核镜像。您还可以配置 DHCP 服务器从预定义范围分配 IP 地址，但使用如清单 12-6 中所示的固定地址非常方便。

您必须在 Linux 开发工作站上启用 DHCP 服务器。这通常通过主菜单或命令行完成。请查阅您自己的 Linux 发行版的文档，以获取适合您环境的细节。例如，要在 Fedora Core 2 Linux 发行版上启用 DHCP 服务器，只需在根命令提示符下键入以下命令：

```
/etc/init.d/dhcpd start (or restart)
```

每次启动开发工作站时都必须执行此操作，除非您配置为自动启动。

安装 DHCP 服务器涉及许多细微之处，因此除非您的服务器位于私有网络上，否则建议在与自己的服务器上线之前先与系统管理员沟通。如果您与企业局域网共存，很有可能会干扰其自身的 DHCP 服务。

### 12.3.3 NFS 服务器

为您的目标板使用 NFS 根挂载是一种非常强大的开发工具。这种配置在开发过程中的一些优势包括：

- 您的根文件系统不受板卡自身有限资源（如闪存）的大小限制。
- 开发过程中对应用程序文件所做的更改可立即供目标系统使用。
- 您可以在开发和调试根文件系统之前调试和启动内核。

