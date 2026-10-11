

如果您以 root 以外的用户身份运行此命令，则必须输入该命令的绝对路径（`sbin/ip`）。

3-12 严禁复制本手册的全部或部分内容，或分发此类副本。如需报告涉嫌复制行为，请致电 1-800-PIRATES。第 1 版

### 练习 3-1 通过 YaST 管理网络配置信息

到目前为止，您的系统已通过 DHCP 获取了所有网络配置信息。在此练习中，您将把所有重要信息更改为静态值。

您可以在练习册中找到此练习。

*（练习结束）*

虽然使用 YaST 时，网络配置的几乎所有步骤都会自动为您完成，但手动配置网络设置有时仍很有用。对于测试和故障排除而言，从命令行更改网络设置往往速度更快。

在本节中，您将学习如何手动配置网络设备。您还将学习如何使用命令行工具配置路由，以及如何将网络设置保存到配置文件中。

- 使用 ip 工具设置网络接口
- 使用 ip 工具设置路由

## 使用 ip 工具设置网络接口

通常，您在安装期间或安装后使用 YaST 配置网卡。您可以使用工具 **ip** 从命令行快速更改网络接口配置。

命令 **ip** 在 RHEL 以及 SUSE Linux Enterprise Server 10 上均可用。

在命令行更改网络接口配置对于测试目的特别有用；如果您希望配置永久生效，必须将其保存在配置文件中。当您使用 YaST 设置网卡时，这些配置文件会自动生成。

您可以使用 **ip** 执行以下任务：

- 显示当前网络配置
- 更改当前网络配置

> 您可以以普通用户身份输入 `/sbin/ip` 来仅显示当前网络设置。若要更改网络设置，必须以 root 身份登录。

由于通过 `ip` 所做的更改会在下次重启时丢失，因此您还必须了解如何：

- 将设备设置保存到配置文件

## 显示当前网络配置

使用 `ip` 工具，您可以显示以下信息：

- IP 地址设置
- 设备属性
- 设备统计信息

### IP 地址设置

要显示所有接口的 IP 地址设置，请输入 `ip address show`。根据您的网络设置，您可能会看到类似以下信息：

```
da2:~ # ip address show
1: lo: <LOOPBACK,UP> mtu 16436 qdisc noqueue
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 brd 127.255.255.255 scope host lo
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,NOARP> mtu 1500 qdisc pfifo_fast qlen 1000
    link/ether 00:30:05:4b:98:85 brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.2/24 brd 10.0.0.255 scope global eth0
    inet6 fe80::230:5ff:fe4b:9885/64 scope link
       valid_lft forever preferred_lft forever
3: sit0: <NOARP> mtu 1480 qdisc noqueue
    link/sit 0.0.0.0 brd 0.0.0.0
```

信息按网络接口分组。每个接口条目以数字开头，称为*接口索引*，接口名称显示在接口索引之后。

在上面的示例中，有 3 个接口：

- **lo.** 回环设备，在每个 Linux 系统上都可用，即使没有安装网络适配器也是如此。（如前所述，在网络配置的上下文中，“设备”和“接口”通常互换使用。）使用此虚拟设备，同一机器上的应用程序可以通过网络相互通信。
  - 例如，您可以通过在网页浏览器的地址栏中输入 [http://127.0.0.1](http://127.0.0.1) 来访问本地安装的 web 服务器，使用回环设备的 IP 地址。
- **eth0.** 此示例中计算机的第一个以太网适配器。以太网设备通常命名为 eth0、eth1、eth2，依此类推。
- **sit0.** 这是一种特殊的虚拟设备，可用于将 IPv4 封装到 IPv6 数据包中。在普通的 IPv4 网络中不使用此设备。

回环设备和 sit 设备的条目始终存在。根据您的硬件设置，`ip` 输出中可能有更多的以太网设备。

每个网络接口都会显示多行信息，例如前一个示例中的 `eth0`：

```
2: eth0: <BROADCAST,MULTICAST,NOTRAILERS,UP> mtu 1500 qdisc pfifo_fast qlen 1000
```

本示例中行中最重要的信息是接口索引（2）和接口名称（eth0）。

其他信息显示为该设备设置的其他属性，例如以太网适配器的硬件地址（00:30:05:4b:98:85）：

```
link/ether 00:30:05:4b:98:85 brd ff:ff:ff:ff:ff:ff
```

在下一行中，显示该设备的 IPv4 设置：

```
inet 10.0.0.2/24 brd 10.0.0.255 scope global eth0
```

IP 地址（10.0.0.2）跟在 `inet` 之后，广播地址（10.0.0.255）跟在 `brd` 之后。网络掩码的长度显示在 IP 地址之后，由 `/` 分隔。长度以位为单位显示（24）。

接下来的几行显示该设备的 IPv6 配置：

```
inet6 fe80::230:5ff:fe4b:9885/64 scope link
   valid_lft forever preferred_lft forever
```

此处显示的地址是自动分配的，即使与设备连接的网络不使用 IPv6。该地址是根据设备的硬件地址生成的。

根据设备类型的不同，信息可能会有所不同。但是，最重要的信息（如已分配的 IP 地址）始终会显示。

### 设备属性

如果您只对设备属性感兴趣，而对 IP 地址设置不感兴趣，您可以输入 `ip link show`：

```
da2:~ # ip link show
1: lo: <LOOPBACK,UP> mtu 16436 qdisc noqueue
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,NOTRAILERS,UP> mtu 1500 qdisc pfifo_fast qlen 1000
   link/ether 00:30:05:4b:98:85 brd ff:ff:ff:ff:ff:ff
3: sit0: <NOARP> mtu 1480 qdisc noqueue
   link/sit 0.0.0.0 brd 0.0.0.0
```

信息与输入 **ip address show** 时所见的类似，但缺少关于地址设置的信息。设备属性显示在设备名称后的括号内。

以下是可能的属性及其含义的列表：

- **UP**。设备已开启。它已准备好接收数据包进行传输，并准备从网络接收数据包。
- **LOOPBACK**。设备是回环设备。
- **BROADCAST**。设备可以发送数据包到共享同一网络的所有主机。
- **POINTTOPOINT**。设备仅连接到另一个设备。所有数据包都发送给另一个设备并从其接收。
- **MULTICAST**。设备可以同时发送数据包到一组其他系统。
- **PROMISC**。设备监听网络上的所有数据包，而不仅仅是发送到该设备硬件地址的数据包。这通常用于网络监控。

### 设备统计信息

您可以使用选项 **-s** 与命令 **ip** 一起使用，以显示有关设备的额外统计信息。命令如下所示：

```
ip -s link show eth0
```

通过在命令行末尾给出设备名称，输出限制为特定的一个设备。这也可以用于显示地址设置或设备属性。

以下是针对设备 `eth0` 显示的信息示例：

```
da2: # ip -s link show eth0
2: eth0: <BROADCAST,MULTICAST,NOTRAILERS,UP> mtu 1500 qdisc pfifo_fast qlen 1000
    link/ether 00:30:05:4b:98:85 brd ff:ff:ff:ff:ff:ff
RX:  bytes packets errors dropped overrun mcast
     849172787 9304150 0 0 0 0
TX:  bytes packets errors dropped carrier collisions
     875278145 1125639 0 0 0 0
```

每个设备都会显示两个包含信息的额外部分。每个部分都有一个标题，描述所显示的信息。

以 `RX` 开头的部分显示关于接收到的数据包的信息，以 `TX` 开头的部分显示关于发送的数据包的信息。

这些部分显示以下信息：

- **Bytes（字节数）**。设备接收或传输的字节总数。
- **Packets（数据包数）**。设备接收或传输的数据包总数。
- **Errors（错误）**。接收器或发送器的错误总数。
- **Dropped（丢弃）**。因资源不足而丢弃的数据包总数。
- **Overrun（溢出）**。导致数据包丢弃的接收器溢出总数。
  - 通常，如果设备溢出，意味着 Linux 内核存在严重问题，或者您的计算机对于该设备来说太慢了。
- **Mcast（组播）**。接收到的组播数据包的总数。此选项仅被少数设备支持。

