
了解您的系统硬件对于做出有关系统使用的未来决策非常重要。随着时间的推移，您可能会选择向特定 Linux 服务器添加服务，该服务器具有足够的硬件来充分支持软件。或者，您可能会选择在添加服务之前升级 Linux 服务器的硬件。

使用 YaST 的硬件信息模块查看您的系统硬件配置文件。保存或打印结果以供以后使用。

## YaST 模块

为了有效地管理 Linux 系统，您应该熟悉 YaST 中用于系统配置的各种模块。使用 `yast --list` 命令查看系统上可用的 YaST 模块。直接使用 `yast` 命令启动每个模块并注意其用途。

## 了解 SuSEconfig

`SuSEconfig` 实用程序通过配置 YaST 在 `/etc/sysconfig` 中保存的信息为 YaST 提供后端。检查 `/etc/sysconfig` 目录的内容并查看其中的一些文件。使用 Internet 和本地文档，检查 `SuSEconfig` 实用程序的目的。最后，在您的系统上运行 `SuSEconfig`。

![](img/9129877170834ca9d5fdac5319bf5f12_118_0.png)

![](img/9129877170834ca9d5fdac5319bf5f12_120_0.png)

## 第 5 节

## 管理网络配置

在本节中，您将了解 YaST 网络卡模块以及其他网络相关主题。这些包括用于测试网络的命令行工具、SUSE 防火墙和远程访问。

### 目标

- 目标 1—从 YaST 管理网络配置信息
- 目标 2—使用命令行工具测试网络连接
- 目标 3—使用 SuSEfirewall2
- 目标 4—使用 NetworkManager 配置网络
- 目标 5—提供远程访问

### 目标 1—从 YaST 管理网络配置信息

用于配置网络卡和网络连接的 YaST 模块可以从 YaST 控制中心访问。参见图 5-1。

要激活网络配置模块，请选择 `网络设备 > 网络卡`。

![](img/9129877170834ca9d5fdac5319bf5f12_121_0.png)

**图 5-1**

YaST 首先想知道网络设置方法：

- *由 NetworkManager 控制的用户*—普通用户可以使用桌面小程序管理所有网络接口的连接。这在笔记本电脑在有线和无线连接之间切换时特别有用。
- *使用 ifup 的传统方法*—传统方法使用 `ifup` 命令。您会在服务器上或在不太可能更改网络连接的桌面上使用此方法。

The next dialog is independent of the method you choose. It lists the detected network cards. See Figure 5-2.

![](img/9129877170834ca9d5fdac5319bf5f12_122_0.png)

图 5-2

Usually the cards are autodetected by YaST, and the correct kernel module is used. Select the card you want to configure; then select Edit. The dialog that appears is shown in Figure 5-4.

If the card is not recognized by YaST, the required module must be entered manually. Select Add. A Manual Network Card Configuration dialog appears. See Figure 5-3.

From this dialog, you can configure the following:

- *Network Configuration*—Specify the network Device Type (Ethernet, Bluetooth, Wireless, etc.) and the Configuration Name (0, 1, etc.).
- *Kernel Module*—If your network card is a PCMCIA or USB device, select the corresponding check boxes and confirm by selecting Next. Otherwise, select Select from List and select your network card from the list. YaST automatically adds the appropriate driver for the selected card to the Module Name drop-down list, as well as any options to the Options text box. Confirm by selecting OK.

![](img/9129877170834ca9d5fdac5319bf5f12_123_0.png)

图 5-3

After selecting Next, the dialog shown in Figure 5-4 appears.

It is the same dialog you see when selecting an existing network card entry in the YaST Network Card Configuration Overview and selecting Edit.

The Address tab offers the following configuration options:

- *None Address Setup*—Select this if you do not want an IP address for this interface.
- *Automatic Address Setup (via DHCP)*—If your network has a DHCP server, you can set up your network address automatically. You should also use this option if you are using a DSL line with no static IP address assigned by the ISP.

If you decide to use DHCP, you can configure the details after selecting DHCP Options from the Advanced drop-down list. Specify whether the DHCP server should always broadcast its responses (in this case, select Request Broadcast Response) and any identifier to use.

By default, DHCP servers use the network card’s hardware address to identify an interface. If you have a virtual host setup where different hosts communicate through the same interface, an identifier is necessary to distinguish them.

![](img/9129877170834ca9d5fdac5319bf5f12_124_0.png)

图 5-4

- *Static Address Setup*—If you have a static address, select the corresponding check box.
- *IP Address*—Each computer accessible in the network has at least one address for each network interface, which must be unique in the entire network. According to the currently valid standard (IPv4), this address consists of a sequence of four bytes, separated by dots (such as 10.10.0.69).
