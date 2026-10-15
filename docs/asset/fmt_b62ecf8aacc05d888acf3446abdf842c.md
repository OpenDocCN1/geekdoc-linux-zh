
## 配置数字用户线路接入

Ubuntu也支持使用数字用户线路（DSL）服务。尽管它将可用的不同类型的DSL统称为`xDSL`，该名称包括`ADSL`、`IDSL`、`SDSL`以及其他类型的DSL服务；它们都可以使用互联网连接向导进行配置。DSL服务通常提供256Kbps到24Mbps的传输速度，并通过铜质电话线将数据从中心局传输到各个用户站点（例如你的家中）。许多DSL服务提供非对称速度，其下载速度大于上传速度。

### 注意

DSL服务是一种“始终在线”类型的互联网服务，尽管你可以使用“系统”、“管理”、“网络”下的网络配置工具在Ubuntu中关闭该连接。始终在线的连接会使你的计算机暴露于破解者的恶意攻击之下，这些破解者在互联网上搜寻并试图访问其他计算机系统。除了能够关闭此类连接之外，Ubuntu还预先配置为不在任何网络端口上监听，这意味着任何试图访问你计算机的行为都将失败，因为Ubuntu会拒绝该请求。这相当于在Ubuntu中为你的计算机竖起一道12英尺高的钢制围栏。

DSL连接要求你的计算机或笔记本电脑中有一块以太网网络接口卡（有时是Linux中不易支持的USB接口）。许多用户还配置一个网关、防火墙或其他带有至少两个网络接口卡的计算机，以便与局域网共享连接。我们已经了解了硬件和

protocol issues earlier on in this chapter. Advanced configuration of a firewall or router, other than what was addressed during your initial installation of Ubuntu, is beyond the scope of this book.

### Understanding Point-to-Point Protocol over Ethernet

Establishing a DSL connection with an ISP providing a static IP address is easy. Unfortunately, many DSL providers use a type of PPP protocol named Point-to-Point Protocol over Ethernet (`PPPoE`) that provides dynamic IP address assignment and authentication by encapsulating PPP information inside Ethernet frames. Roaring Penguin’s `rp-pppoe` clients are available from the Roaring Penguin site (`www.roaringpenguin.com/penguin/pppoe/rp-pppoe-3.8.tar.gz`), and these clients make the difficult-to-configure PPPoE connection much easier to deal with. You can download and install newer versions (see the Roaring Penguin link in the “Reference” section at the end of this chapter).

> **NOTE**
>
> `ADSL` modems were frequently supplied by ISPs when they originally started to roll out `ADSL` services. Nowadays, however, these modems are optional, which is a good thing as many people choose to purchase a router with an in-built modem to create a dedicated connection. Using a router can save many headaches and will allow you to easily connect more than one computer to an Internet connection. Note that if you are using a cable connection, then they usually come with an Ethernet cable, in which case you just need a router. Check with your ISP before buying to ensure that whatever router you do end up with can be supported by them. You might find that your ISP even supplies a router as part of the package!

### Configuring a PPPoE Connection Manually

You should only need to use these steps if you are using a modem supplied by your ISP, and not a router. The basic steps involved in manually setting up a DSL connection using Ubuntu involve connecting the proper hardware, and then running a simple configuration script if you use `rp-pppoe` from Roaring Penguin.

First, connect your DSL modem to your telephone line, and then plug in your Ethernet cable from the modem to your computer’s network interface card. If you plan to share your DSL connection with the rest of your LAN, you need at least two network cards—designated `eth0` (for your LAN) and `eth1` (for the DSL connection).

The following example assumes that you have more than one computer and will share your DSL connection on a LAN.

Note that you can also use a hostname instead, if each computer has an `/etc/hosts` file with hostname and IP address entries for your LAN. To stop your connection, use the `adsl-stop` command like this:

```
#### /sbin/adsl-stop
```

### Configuring Dial-Up Internet Access

Most ISPs provide dial-up connections supporting PPP because it is a fast and efficient protocol for using TCP/IP over serial lines. PPP is designed for two-way networking; TCP/IP provides the transport protocol for data. One hurdle faced by new Ubuntu users is how to set up PPP and connect to the Internet. It is not necessary to understand the details of the PPP protocol in order to use it, and setting up a PPP connection is easy. You can configure the PPP connections manually using the command line or graphically during an X session using Ubuntu’s Network Configuration Tool. Each approach produces the same results.
