
```sh
#!/bin/sh
###### Configure the frad hardware and the DLCI parameters
/sbin/fradcqf /etc/frad/router.conf || exit 1
/sbin/dlcicfg file /etc/frad/router.conf

###### Bring up the FRAD device
ifconfig sda10 up

###### Configure the DLCI encapsulation interfaces and routing
ifconfig dlic100 192.168.10.1 pointopoint 192.168.10.2 up
route add -net 192.168.10.0 netmask 255.255.255.0 dlic100

ifconfig dlic101 192.168.11.1 pointopoint 192.168.11.2 up
route add -net 192.168.11.0 netmask 255.255.255.0 dlic100

route add default dev dlic100
```

![](img/a3584dae761d2e3abed8bf40d7637389_298_0.png)

### IPX (AF_IPX)

IPX 协议最常用于 Novell NetWare(tm) 局域网环境。Linux 包含对该协议的支持，并可以被配置为网络端点，或者作为 IPX 的路由器。

#### 内核编译选项

```text
Networking options --->
[*] The IPX protocol
[ ] Full internal IPX network
```

IPX 协议和 NCPFS 在 IPX-HOWTO（参见 `IPX-HOWTO.html`）中有更深入的讲解。

### NetRom (AF_NETROM)

NetRom 设备名称为 "`nr0`"`、`"nr1"` 等。

#### 内核编译选项

```text
Networking options --->
[*] Amateur Radio AX.25 Level 2
[ ] Amateur Radio NET/ROM
```

AX25、Netrom 和 Rose 协议在 AX25-HOWTO（参见 `http://metalab.unc.edu/LDP/`）中有介绍。这些协议被世界各地的业余无线电操作员用于分组无线电实验。

这些协议的大部分实现工作由 Jonathon Naylor `<jsn@cs.nott.ac.uk>` 完成。

### Rose 协议 (AF_ROSE)

在 2.1.* 内核中，Rose 设备名称为 "`rs0`"`、`"rs1"` 等。Rose 在 2.1.* 内核中可用。

#### 内核编译选项

```text
Networking options --->
[*] Amateur Radio AX.25 Level 2
<*> Amateur Radio X.25 PLP (Rose)
```

AX25、Netrom 和 Rose 协议在 AX25-HOWTO（参见 `http://metalab.unc.edu/LDP/`）中有介绍。这些协议被世界各地的业余无线电操作员用于分组无线电实验。

这些协议的大部分实现工作由 Jonathon Naylor `<jsn@cs.nott.ac.uk>` 完成。

### SAMBA——“NetBEUI”、“NetBios” 支持

SAMBA 是会话管理块协议（Session Management Block protocol）的一种实现。Samba 允许 Microsoft 及其他系统挂载和使用您的磁盘和打印机。

SAMBA 及其配置在 SMB-HOWTO（参见 `http://metalab.unc.edu/LDP/`）中有详细讲解。

### STRIP 支持 (Star MODE RADIO IP)

STRIP 设备名称为 `st0`、`st1` 等。

#### 内核编译选项

```text
Network device support -->
  [*] Network device support

 ....

 [*] Radio network interfaces
  < > STRIP (MetriCom starmode radio IP)
```

STRIP 是一种专门为一系列 Metricom 无线电调制解调器设计的协议，用于斯坦福大学正在进行的一个名为 MosquitoNet 项目的研究（参见 `http://mosquitonet.Stanford.EDU/mosquitonet.html`）。这里有很多有趣的阅读材料，即使您对该项目没有直接兴趣。

Metricom 无线电连接到串行端口，采用扩频技术，通常能够支持约 100kbps。Metricom 无线电的信息可以从 Metricom Web 服务器获取（参见 `http://www.metricom.com/`）。

目前，标准的网络工具不支持 STRIP 驱动程序，因此您必须从 MosquitoNet Web 服务器下载一些定制的工具。关于您需要哪些软件的详细信息可以在 MosquitoNet STRIP 页面（参见 `http://mosquitonet .Stanford.EDU/strip.html`）上找到。

配置摘要如下：您使用修改过的 `slattach` 程序将串行 tty 设备的线路规程设置为 STRIP，然后像配置 Ethernet 一样配置生成的 `st [0-9]` 设备，有一个重要的例外：由于技术原因，STRIP 不支持 ARP 协议，因此您必须为子网上的每台主机手动配置 ARP 条目。这应该不会太麻烦。

### 第三部分

### 令牌环

令牌环设备名称为 `tr0`、`tr1` 等。令牌环是 IBM 标准局域网协议，它通过提供一种机制来避免冲突，该机制允许局域网上的任何一次只有一个工作站拥有发送权。令牌由一个工作站在某时刻持有，持有令牌的工作站是唯一允许发送的工作站。当它发送完数据后，它将令牌传递给下一个工作站。令牌在所有活动工作站之间循环——因此得名“令牌环”。

#### 内核编译选项

```text
Network device support  ---
[*] Network device support
*
[*] Token Ring driver support
< > IBM Tropic chipset based adaptor support
```

令牌环的配置与以太网完全相同，除了要配置的网络设备名称。

### X.25

X.25 是由 C.C.I.T.T.（一个被世界大多数地区电信公司认可的标准机构）定义的基于电路的分组交换协议。X.25 和 LAPB 的实现正在开发中，最近的 `2.1.*` 内核包含正在进行的工作。

Jonathan Naylor `<jsn@cs.nott.ac.uk>` 正在领导开发，并且已经建立了一个邮件列表来讨论 Linux X.25 相关事项。要订阅，请发送一条消息给 `majordomo@vger.rutgers.edu`，消息正文中包含文本 `subscribe linux-x25`。

可以从 Jonathan 的 FTP 站点 `ftp.cs.nott.ac.uk`（参见 `ftp://ftp.cs.nott.ac.uk/jsn/`）获取配置工具的早期版本。

### WaveLAN

WaveLAN 设备名称为 "`eth0`"`、`"eth1"` 等。

#### 内核编译选项

```text
Network device support -->
[*] Network device support
...
[*] Radio network interfaces
...
<> WaveLAN support
```

WaveLAN 卡是一种扩频无线局域网卡。实际上，该卡看起来非常像以太网卡，配置方式也大体相同。

您可以从 Wavelan.com（参见 `http://www.wavelan.com/`）获取有关 WaveLAN 卡的信息。

### 电缆和布线

善于使用焊烙铁的人可能想自己制作电缆来互连两台 Linux 机器。以下布线说明将对此提供帮助。

#### 串行 Null Modem 电缆

并非所有的 Null Modem 电缆都一样。许多 null modem 电缆所做的只不过欺骗您的计算机认为所有适当的信号都存在，并交换发送和接收数据。这可以工作，但意味着您必须使用软件流量控制（XON/XOFF），其效率低于硬件流量控制。以下电缆提供了机器之间尽可能最佳的信号传输，并允许您使用硬件（RTS/CTS）流量控制。

| 引脚名称 | 引脚 | 连接 | 引脚 |
| :--- | :--- | :--- | :--- |
| Tx Data | 2 | -------- | 3 |
| Rx Data | 3 | -------- | 2 |
| RTS | 4 | -------- | 5 |
