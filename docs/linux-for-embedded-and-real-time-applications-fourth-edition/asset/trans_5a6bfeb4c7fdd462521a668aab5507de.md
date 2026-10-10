

以 root 用户身份，将 `/mnt/iso/arm-gcc-4.9.4.tar.bz2` 复制到 `/usr/local`，并按如下所示解包：

```
cp /mnt/iso/arm-gcc-4.9.4.tar.bz2 /usr/local
cd /usr/local
tar -xf arm-gcc-4.9.4.tar.bz2
```

在本书中，你会进行大量“解包”操作，即上面列表中的第三个命令。因此，当你看到解包特定文件的说明时，这就是你要使用的命令。

工具链安装在 `arm-unknown-linux-gnueabif` 中。你需要将 `/usr/local/arm-unknown-linux-gnueabif/bin` 添加到你的 PATH（shell 搜索可执行文件的目录列表）中。在 CentOS 中，定义 PATH 的文件是 `.bash_profile`。在 Ubuntu/Debian 安装环境中，它只是 `.profile`。从这里开始，我们将进行大量的编辑。如果你有喜欢的 Linux 编辑器，尽管使用它。就个人而言，我拒绝使用 vi 或 emacs。² 我最喜欢的 K 桌面环境（KDE）编辑器是 Kwrite。在文件管理器窗口中双击文本文件，它会自动在 Kwrite 中打开。

在 `.bash_profile`（或 `.profile`）中，你会找到一行以 `PATH=$PATH:` 开头的行；后面通常跟着 `$HOME/bin`。在那一行的末尾添加 `:/usr/local/arm-unknown-linux-gnueabif/bin`。保存文件并关闭编辑器。新的路径在你注销并重新登录之前不会生效。不用着急。距离我们开始构建程序还有一段时间。

### 终端仿真器 minicom

minicom 是一个相当简单的 Linux 应用程序，它通过串行端口模拟一个笨拙的 RS-232 终端。这就是我们将用来与目标板通信的工具。

最近的 Linux 发行版默认不安装 minicom。安装它很容易。

以 root 用户身份（再次，使用 `su` 或 `sudo`）执行：

```
yum install minicom        在 CentOS 中
apt-get install minicom    在 Ubuntu 或 Debian 中
```

这两个命令基本上做的是同样的事情。它们会去互联网上查找指定的软件包，解决依赖项，下载软件包，并安装它们。

一旦 minicom 安装完毕，我们需要更改一些配置选项以方便与目标板通信。

² 虽然我被迫尝试过 vim，但它也不坏。

在 shell 窗口中，再次以 root 用户身份，输入命令 `minicom -s`。如果你第一次运行 minicom，你可能会看到以下警告消息：

```
WARNING: Configuration file not found. Using defaults
```

你将看到一个配置菜单。选择 **Serial port setup**（图 4.1）。默认情况下，minicom 通过调制解调器设备 `/dev/modem` 通信。我们需要将其更改为直接通过串行端口通信。我们的目标板在其 USB 接口上模拟了一个串行端口。输入 “A” 并将 “modem” 一词替换为 “/ttyACM0。”

![](img/f03d6fa2c5faefc793771df52bbb2ef9_72_0.png)

图 4.1 Minicom 串行端口设置菜单。

输入 “E” 然后输入 “T” 以选择 115200 波特率。确保硬件和软件流控制都设置为 “no”。这些是切换开关。输入 “F” 或 “G” 会将相应的值在 “yes” 和 “no” 之间切换。图 4.1 显示了最终的串行端口配置。

按 <Enter> 退出 Serial port setup，然后选择 **Modem and dialing**。在这里，我们要删除调制解调器的 Init string 和 Reset string，因为它们在直接串行连接中只是碍事。输入 “A” 并退格删除整个 Init string。输入 “B”，并对 Reset string 执行相同操作。此菜单中的其他字符串无关紧要，因为它们永远不会被调用。

按 <Enter> 退出 Modem and dialing，然后选择 **Screen and keyboard**。输入一次 “B” 将 Backspace 键从 BS 更改为 DEL。

按 <Enter> 退出 Screen and keyboard。选择 **Save setup as dfl (default)**。然后选择 **Exit**。

此时，`/dev/ttyACM0` 尚不存在，因为你还没有给目标板供电。但如果它存在，你会发现只有所有者和组对该设备有访问权限。为了获得对该端口的访问权限，你必须成为 dialout 组的成员。

过去有一个漂亮的图形对话框，可以从开始菜单下的 Administration > Users and Groups 访问，使这个过程非常简单。现在没有那种对话框了。现在你必须编辑 `/etc` 下的相应文件，在这种情况下是 `group`。以 root 用户身份，在编辑器中打开 `/etc/group`。找到以 “dialout:” 开头的行，并在该行末尾添加 “:<your_user_name>”。保存文件并关闭编辑器。

### 网络

主机网络配置需要做一些更改。

#### 网络地址

你的工作站很可能配置为通过 DHCP（动态主机配置协议）获取网络地址。但在这种情况下，为了简化问题，我们将为工作站和目标指定固定的 IP 地址。

CentOS 用于更改网络参数的图形菜单通过 Settings -> System Settings 访问。³ 选择 Network Settings 以及 Wired 或 Wireless 选项卡，具体取决于你的网络连接类型。对于虚拟机，即使是无线接口在客户端操作系统中看起来也像有线接口。

选择网络接口并单击 Edit... 你的网络接口可能命名为类似 `enp0s8` 的名称，这意味着它是一个连接到 PCI 总线段 0 的插槽 8 上的以太网设备 (en)。将 Method 从 DHCP 更改为 Manual。现在输入固定的 IP 地址。网络地址 `192.168.1` 是一个很好的选择，因为它是为局域网保留的一组网络地址之一。为你的工作站选择节点 `2`。子网掩码会自动填充。图 4.2 显示了最终结果。如果你连接到互联网，可能还想设置默认网关地址和 DNS 节点。

![](img/f03d6fa2c5faefc793771df52bbb2ef9_74_0.png)

图 4.2 编辑网络设备对话框。

当你退出 *Edit Network Connections* 对话框时，会出现一个关于 KDE Wallet 系统的对话框，要求你选择一种加密方法。说实话，我从未理解 KDE Wallet 系统是怎么回事，也从未使用过它，所以我只需在此处单击 Cancel。

或者，你可以直接进入并直接编辑网络设备参数文件。网络配置参数位于 `/etc/sysconfig/network-scripts/` 中，在那里你应该找到一个名为类似 `ifcfg-enpo8` 的文件，其中包含网络适配器 `enpo8` 的参数。你可能想复制一份此文件并将其命名为类似 `dhcp-ifcfg-enpo8` 的名称。这样，如果需要，你将拥有一个用于未来使用的 DHCP 配置文件。现在，以 root 用户身份使用编辑器打开原始文件。它应该看起来像清单 4.1A 中的样子。此处显示的各行的顺序可能不同，并且可能与其他行穿插。

将行 `BOOTPROTO=dhcp` 更改为 `BOOTPROTO=none`，并添加清单 4.1B 中显示的两个新行。删除关于 PEERDNS 和 PEERROUTES 的行。

| TYPE=Ethernet
BOOTPROTO=dhcp
DEFROUTE=yes
IPV4_FAILURE_FATAL=yes
IPV6INIT=no
NAME=enp0s8
UUID=27db13eb-6a1d-41e5-88bc-de3a6aa0895
ONBOOT=yes
PEERDNS=yes
PEERROUTES=yes |

| TYPE=Ethernet
BOOTPROTO=none
DEFROUTE=yes
IPV4_FAILURE_FATAL=yes
IPV6INIT=no
NAME=enp0s8
UUID=27db13eb-6a1d-41e5-88bc-de3a6aa0895
ONBOOT=yes
IPADDR=192.168.1.2
PREFIX=24 |

清单 4.1: (A) ifcfg-eth0; (B) 修订后的 ifcfg-eth0。

### 无线网如何？

就个人而言，我在 Linux 中直接配置无线网络端口时从未成功过。但无线端口在虚拟机环境中工作正常，因为虚拟机管理器虚拟化网络接口，使其在客户机中看起来像其他东西。例如，VirtualBox 将任何物理网络接口转换为 Intel 82540EM 千兆以太网接口。

拥有两个接口可能非常有用。例如，你可以让无线端口保持连接到你的网络并通过 DHCP 获取 IP 地址，然后按照上述方法重新配置以太网端口，以便专门用于与目标板的连接。例如，我的网络是 `192.168.1`。我将目标板插入交换机。路由器中的 DHCP 服务器分配节点地址，范围从 100 到 199。我笔记本电脑上的 Windows 主机操作系统从 DHCP 获取其 IP 地址。Linux 客户机的地址由此处描述的过程固定，一切都运行良好。

### 网络文件系统

我们使用 NFS（网络文件系统）来挂载目标板的根文件系统。⁴ 这样做的原因在我们从第 7 章“访问硬件”开始开发应用程序时将变得明显。这意味着我们必须“导出”工作站上的一个或多个目录，以便它们在网络上可见。

⁴ Ubuntu 发行版默认未安装 NFS。执行 `sudo apt-get install nfs-kernel-server` 来安装它。

