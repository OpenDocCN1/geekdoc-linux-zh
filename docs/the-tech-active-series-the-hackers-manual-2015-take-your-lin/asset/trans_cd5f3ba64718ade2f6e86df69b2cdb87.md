

## 网络：

在向你介绍了网络的构建模块和工具之后，我们将把所有这些知识整合起来，创建真实、可用的网络。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_105_0.png)

在之前的页面中，我们向你介绍了网络的不同组成部分——数据包、物理连接和逻辑寻址——以及你在 Linux 主机上检查这些组件运行情况所需的工具。这将大大帮助你有效地处理网络并诊断你遇到的问题。现在，我们想向你展示这些元素如何组合起来创建一些真实的网络。我们将从让两台计算机直接相互通信开始，然后再演示如何将 Linux 主机变成路由器。为了让你不需要很多计算机，所有这些都将在 VirtualBox 中完成，但你应该也能将同样的技术应用于物理系统。

我们的示例将使用 CentOS——它基于 Red Hat Enterprise Linux，是服务器的常见选择。如果你对 Ubuntu 或其他基于 Debian 的发行版感兴趣，（请参阅第 109 页的“基于 Debian 的发行版”框）。在开始网络方面的工作之前，我们首先需要搭建一个练习用的实验室。那么，你的第一项工作就是安装 VirtualBox。它应该位于大多数发行版的默认软件仓库中，所以只需使用你当前发行版自带的包管理器即可。完成后，下载 CentOS 最小安装光盘（www.centos.org）。然后，按照对面的分步指南在 VirtualBox 中创建两个新的虚拟机，确保添加所有必要的网络接口以使一切正常工作。然后，对第二台虚拟机重复上述步骤，确保它也连接到相同的内部网络。通过像我们这样创建具有两个网络接口的虚拟机，它们不仅可以通过默认 NAT 连接，还能通过我们添加的内部网络直接相互通信。这个内部网络相当于将两台虚拟机插入同一个交换机，或者在两者之间连接一根网线。

/etc/sysconfig/network-scripts 目录的内容看起来令人望而生畏，但如果你专注于 ifcfg-ethX 文件，你会发现这里有很多可以做的事情。

## 基础网络

两台机器都安装完成后，是时候通过默认的 NAT 网络将两者都连接到互联网了。这将让我们有机会熟悉 Red Hat 的网络配置文件，并重温我们在之前页面中介绍的一些信息。新虚拟机启动后要做的第一件事是切换到 /etc/sysconfig/network-scripts 目录。在基于 Red Hat 的发行版中，该目录包含连接到机器的每个网络设备的启动脚本和配置。如果你按照我们的分步指南操作，应该会看到两个配置文件，ifcfg-eth0 和 ifcfg-eth1（如果你使用的是不同版本的 Red Hat，你看到的可能是 ifcfg-em2 和 ifcfg-em2）。Eth0 是系统上的第一个网络设备，应该对应 VirtualBox 配置中的适配器 1——也就是 NAT 网络。

使用 Vi 编辑 ifcfg-eth0，确保以下行存在并设置为这些值：
NM_CONTROLLED="no"
BOOTPROTO="dhcp"
ONBOOT="yes"

第一行阻止 NetworkManager 控制此接口——既然我们要手动操作，它的干扰可能会把事情搞乱，所以我们将其关闭。第二行指定了它应该使用什么协议来获取 IP 地址。这里，我们指定了 DHCP，即动态。

```
root@Adam /etc/sysconfig/network-scripts
ifcfg-Auto Ethernet  ifdown-post  ifup-plug
ifcfg-Auto Ethernet-1  ifdown-ppp  ifup-ppp
ifcfg-Auto greater...  ifdown-route  ifup-route
ifcfg-Auto...  ifdown-sit  ifup-sit
ifcfg-Auto_LAN...  ifdown-tunnel  ifup-tunnel
ifcfg-Auto_netgear  ifup  ifup-aliases  ifup-wireless
ifcfg-lo  ifup-bnep  init.ipv6-global
ifdown  ifup-eth  keys-Auto...  network-functions
ifdown-bnep  ifup-ippp  keys-Auto...  net.hotplug
ifdown-ippp  ifup-ipsec  network-functions  network-functions-ipv6
ifdown-isdn  ifup-ipx  network-functions  
root@Adam network-scripts#
```

