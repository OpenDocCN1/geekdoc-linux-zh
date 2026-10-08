
当 `lokkit` 打开时，你将看到图 31.2 所示的“防火墙配置”界面，它允许你在计算机上设置高安全、中安全或无防火墙。在 `lokkit` 中，你可以使用 Tab 键在选项之间导航，并按空格键进行选择。

选择“高”（High）或“中”（Medium）安全级别并点击“自定义”继续。你将看到类似于图 31.3 所示的“防火墙配置 - 自定义”菜单。

在此菜单中，你可以看到与 Red Hat 安装期间显示的“防火墙配置”菜单中相同的自定义选项。在这种情况下，网卡选项包括一个红外设备 (`irlan0`) 和一个普通以太网适配器 (`eth0`)。使用之前描述的方法进行选择，然后选择“确定”。这将你返回到图 31.2 所示的原始界面。然后你可以点击“确定”，`lokkit` 将会将你的新防火墙记录在 `/etc/sysconfig/ipchains` 文件中。

### 图 31.2：

`lokkit` 防火墙配置界面

![](img/fd2d9aa645b3d05a8fce065954a79484_745_0.png)

### 图 31.3：

自定义防火墙

![](img/fd2d9aa645b3d05a8fce065954a79484_745_1.png)

## 注意

在安装后使用 `lokkit` 时，默认的高、中安全防火墙不会开启 DHCP。

## 创建基于 Linux 的路由器

Red Hat Linux 7.1 的默认防火墙命令是 `iptchains`。针对 2.4.x 内核的新防火墙命令是 `iptables`。你可以禁用 `iptchains`，然后 `iptables` 将在你的防火墙中可用。然而，`lokkit` 实用程序不支持 `iptables` 的配置。`iptables` 的文档尚未最终确定；目前的 HOWTO 可以在 http://va.samba.org/netfilter/unreliable-guides/packet-filtering-HOWTO/index.html 找到。就绪后，请在 www.linuxdoc.org 网站上查找。

还有另一个防火墙配置实用工具 `/usr/sbin/firewall-config`。它比 `lokkit` 稍微难用一些。

你可以通过 IP 地址自定义你打开的端口。换句话说，只有具有特定 IP 地址的计算机才有向你发送特定类型数据的密钥。设置这些内容的技术超出了本书的范围。有关防火墙和网络配置的更多信息，请参阅 Robert Ziegler 写的《Linux Firewalls》（New Riders, 1999）。

在下一节中，你将使用一个基于软盘的 Linux 版本创建一个防火墙。它包含了关于伪装（masquerading）的信息，你也可以结合基于 `lokkit` 的防火墙使用。伪装会隐藏你网络内部计算机的地址。

## 创建基于 Linux 的路由器

本节将介绍使用 Linux Router Project 发行版 Linux 创建基于 Linux 的路由器的步骤。

Linux Router Project 的 Linux 发行版设计为极简 Linux 安装，对于大多数站点它可以放入单个 1.44MB 的软盘中，并提供了两个以太网局域网之间或通过 PPP 访问之间之间路由的所有组件。通过 `add-modules`，可以支持 WAN 连接的额外硬件。其他功能如 SNMP 管理也是可。

### 第 31 章 安全与 Red Hat Linux 7.1 一个廉价的路由器

使用 Linux Router Project 发行版而不是 Red Hat 等完整版 Linux 设置路由器的好处是，所有工作都为你做好了。你不需要费力识别安装什么来实现路由。此外，软件包含了一个简单的、菜单驱动的配置，允许你检查一切是否已完成。Linux Router Project 软件可以他们的网站 http://www.linuxrouter.org/ 下载。

接下来的章节提供了如何在安全和不安全网络之间配置路由器的绝佳示例。遗憾的是，生产级 Linux Router Project (LRP) 软件基于 Linux 内核 2.0 和 2.2。针对内核 2.2 的 LRP 软件包含了过时的 `ipfw` 命令，该命令存在安全漏洞。针对内核 2.2 的 LRP 软件包含了 `iptchains`，它更安全。到目前为止，还没有生产级别的 `iptables` 支持。

### 你将创建

本节演示了使用 Linux Router Project 发行版 Linux 创建基于 Linux 路由器的步骤。

设计为极简 Linux 安装的 Linux Router Project Linux 发行版对于大多数站点可以放入单个 1.44MB 的软盘中，并提供了两个以太网局域网之间或通过 PPP 访问互联网之间路由的所有组件。通过 `add-modules`，可以支持 WAN 连接的额外硬件。其他功能如 SNMP 管理也是提供的。

### 第 31 章 安全与 Red Hat Linux 7.1 一个廉价的路由器

使用 Linux Router Project 发行版而不是 Red Hat 等完整版 Linux 设置路由器的好处是，所有工作都为你做好了。你不需要费力识别需要安装什么来实现路由工作。此外，软件包含了一个简单的、菜单驱动的配置，允许你检查一切是否已完成。Linux Router Project 软件可以从他们的网站 http://www.linuxrouter.org/ 下载。

接下来的章节提供了如何在安全和不安全网络之间配置路由器的绝佳示例。遗憾的是，生产级 Linux Router Project (LRP) 软件基于 Linux 内核 2.0 和 2.2。针对内核 2.2 的 LRP 软件包含了过时的 `ipfw` 命令，该命令存在安全漏洞。针对内核 2.2 的 LRP 软件包含了 `iptchains`，它更安全。到目前为止，还没有生产级别的 `iptables` 支持。

### 你将创建

本节演示了使用 Linux Router Project 发行版 Linux 创建基于 Linux 路由器的步骤。

设计为极简 Linux 安装的 Linux Router Project Linux 发行版对于大多数站点可以放入单个 1.44MB 的软盘中，并提供了两个以太网局域网之间或通过 PPP 访问互联网之间路由的所有组件。通过 `add-modules`，可以支持 WAN 连接的额外硬件。其他功能如 SNMP 管理也是提供的。

## 注意

在安装后使用 `lokkit` 时，默认的高、中安全防火墙不会开启 DHCP。

## 创建基于 Linux 的路由器

Red Hat Linux 7.1 的默认防火墙命令是 `iptchains`。针对 2.4.x 内核的新防火墙命令是 `iptables`。你可以禁用 `iptchains`，然后 `iptables` 将在你的防火墙中自动可用。然而，`lokkit` 实用程序不支持 `iptables` 的配置。`iptables` 的文档尚未最终确定；目前的 HOWTO 可以在 http://va.samba.org/netfilter/unreliable-guides/packet-filtering-HOWTO/index.html 找到。就绪后，请在 www.linuxdoc.org 网站上查找。

另一个防火墙配置实用工具 `/usr/sbin/firewall-config` 也是提供的。它比 `lokkit` 稍微难用。

你可以通过 IP 地址自定义你打开的端口。换句话说，只有具有特定 IP 地址的计算机才有向你发送特定类型数据的密钥。设置这些内容的技术超出了本书的范围。有关防火墙和网络配置的更多信息，请参阅 Robert Ziegler 写的《Linux Firewalls》（New Riders, 1999）。

在下一节中，你将使用一个基于软盘的 Linux 版本创建一个防火墙。它包含了关于伪装（masquerading）的信息，你也可以结合基于 `lokkit` 的防火墙使用。伪装会隐藏你网络内部计算机的地址。

## 创建基于 Linux 的路由器

本节将介绍使用 Linux Router Project 发行版 Linux 创建基于 Linux 路由器的步骤。

设计为极简 Linux 安装的 Linux Router Project Linux 发行版对于大多数站点可以放入单个 1.44MB 的软盘中，并提供了两个以太网局域网之间或通过 PPP 访问互联网之间路由的所有组件。通过 `add-modules`，可以支持 WAN 连接的额外硬件。其他功能如 SNMP 管理也是提供的。

### 第 31 章 安全与 Red Hat Linux 7.1 一个廉价的路由器

使用 Linux Router Project 发行版而不是 Red Hat 等完整版 Linux 设置路由器的好处是，所有工作都为你做好了。你不需要费力识别需要安装什么来实现路由工作。此外，软件包含了一个简单的、菜单驱动的配置，允许你检查一切是否已完成。Linux Router Project 软件可以从他们的网站 http://www.linuxrouter.org/ 下载。

接下来的章节提供了如何在安全和不安全网络之间配置路由器的绝佳示例。遗憾的是，生产级 Linux Router Project (LRP) 软件基于 Linux 内核 2.0 和 2.2。针对内核 2.2 的 LRP 软件包含了过时的 `ipfw` 命令，该命令存在安全漏洞。针对内核 2.2 的 LRP 软件包含了 `iptchains`，它更安全。到目前为止，还没有生产级别的 `iptables` 支持。

### 你将创建

本节演示了使用 Linux Router Project 发行版 Linux 创建基于 Linux 路由器的步骤。

设计为极简 Linux 安装的 Linux Router Project Linux 发行版对于大多数站点可以放入单个 1.44MB 的软盘中，并提供了两个以太网局域网之间或通过 PPP 访问互联网之间路由的所有组件。通过 `add-modules`，可以支持 WAN 连接的额外硬件。其他功能如 SNMP 管理也是提供的。

## 注意

在安装后使用 `lokkit` 时，默认的高、中安全防火墙不会开启 DHCP。

## 创建基于 Linux 的路由器

Red Hat Linux 7.1 的默认防火墙命令是 `iptchains`。针对 2.4.x 内核的新防火墙命令是 `iptables`。你可以禁用 `iptchains`，然后 `iptables` 将在你的防火墙中自动可用。然而，`lokkit` 实用程序不支持 `iptables` 的配置。`iptables` 的文档尚未最终确定；目前的 HOWTO 可以在 http://va.samba.org/netfilter/unreliable-guides/packet-filtering-HOWTO/index.html 找到。就绪后，请在 www.linuxdoc.org 网站上查找。

另一个防火墙配置实用工具 `/usr/sbin/firewall-config` 也是提供的。它比 `lokkit` 稍微难用。

你可以通过 IP 地址自定义你打开的端口。换句话说，只有具有特定 IP 地址的计算机才有向你发送特定类型数据的密钥。设置这些内容的技术超出了本书的范围。有关防火墙和网络配置的更多信息，请参阅 Robert Ziegler 写的《Linux Firewalls》（New Riders, 1999）。

在下一节中，你将使用一个基于软盘的 Linux 版本创建一个防火墙。它包含了关于伪装（masquerading）的信息，你也可以结合基于 `lokkit` 的防火墙使用。伪装会隐藏你网络内部计算机的地址。

### 准备工作

以下说明允许你从软盘创建 Linux Router Project。就目前为止，你可以从 http://www.linuxrouter.org 下载这些文件。

1. 下载 "iot-image" 文件并将其保存到方便的位置，例如 `/tmp/`。

2. 切换当前目录到下载文件的目录，使用命令 `cd /tmp`。

3. 解压缩存档。该镜像以 gzip 格式提供，可以使用以下命令解压：

```
gunzip idiot-image-1440KB_FAT_2.9_8_Linux_2.2.gz
```

4. 将磁盘镜像拷贝到软盘。这将擦除该磁盘上的任何数据。使用 `dd` 命令如：

```
dd if=idiot-image-1440KB_FAT_2.9_8_Linux_2.2 of=/dev/fd0
```

完成后，你就有了 Linux Router 的启动软盘。但不够。你还需要相同内核版本的网络驱动程序，在这种情况下为 2.2.16-1。

对 `2.2.16-1.tar.gz` 文件重复基本过程，从相同的下载站点可用。将此文件拷贝到 `/tmp` 目录。使用 `tar xzv 2.2.16-1.tar.gz` 命令解压并提取存档。将网络模块从解压的 `/tmp/2.2.16-1/modules/net/` 子目录拷贝到第二个软盘。备后用。

到目前，Linux Router Project 2.9.8 版本是“测试版”。换句话说，在最终确定之前，不建议在生产计算机中使用。

确保你有足够的硬件来运行路由器。虽然带有 8MB RAM 的 386SX 可以作为路由器运行，而带有 12MB RAM 的 486DX2 66MHz 表现尚可，但你真的想要运行 Pentium 100MHz 或更快的系统，并配备至少 16MB RAM。不需要硬盘，只需要用于启动的软盘。如果你想为你的 Linux Router Project 配置添加更多插件，那么软件可能会超过你的软盘的大小，在

假设考虑从硬盘或可启动的 Zip 驱动器启动，并将你的 RAM 增加到 32MB。有关如何从其他介质启动的详情，可以在 Linux Router Project 页面上找到。

如果你使用的是基于 Intel 类型 386 或 486 的计算机，最佳可用选项是基于 2.0.36 内核的过时 `ipfwadm` 命令的“idiot-images”。按照上述相同步骤，使用 `idiot-image_14400KB_FAT_2.9_8_Linux2.0.gz` 镜像文件和 `2.0.36pre15-1.tar.gz` 内核模块文件。

Slackware 有其 Linux 发行版的变体，设计用于放入 Zip 驱动器。更多信息请查看 http://www.Slackware/zipslack。

PC 需要两个以太网卡。一个用于连接到不安全的网络，另一个将连接到安全网络。

# 运行环境

在启动 Linux 路由器软件之前，让我们定义路由器运行的环境，以便你执行的配置具有合理性。

首先，你需要确定 IP 地址。你的不安全网络将使用从 200.200.200.0 到 200.200.255.255 的地址，子掩码为 255.255.255.0。连接网络到世界的路由器位于 200.200.200.1，而你正在构建的路由器在不安全侧的 IP 地址为 200.200.200.254。这些是真实的 IP 地址，在互联网上是唯一的。如果你的路由器允许，互联网上的机器可以直接与不安全局域网中的任何机器通信。

你的安全网络将使用从 10.10.10.0 到 10.10.10.255 的地址，子掩码为 255.255.255.0。路由器将在安全侧使用 IP 地址 10.10.10.1。这些是私有的或不可路由的 IP 地址。世界其他部分不知道内部网络主机的存在，且无法与你的路由器进行直接通信；它的防火墙向世界其他部分（包括你的不安全网络）隐藏了安全网络的存在。

# 第31章 安全与红帽 Linux 7 廉价路由器

在你构建的路由器中，设备 `eth0` 将连接到不安全局域网（IP 地址 200.200.200.254），设备 `eth1` 将连接到安全局域网（IP 地址 10.10.10.1）。

你将只允许来自安全局域网的出站连接——不允许入连接。此外，你将使用 Linux 内核中称为 IP 伪装（IP masquerading）的功能来实现网络地址转换。路由器不仅处理数据进出安全局域网的工作，安全局域网内部通过路由器连接的机器还会隐藏该机器的 IP 地址，并将其转换为不安全局域网上的地址。通过这种方式，连接无法追溯到主机的真实 IP 地址，帮助隐藏世界其他部分主机的存在。

由于安全网络使用不可路由的 IP 地址，你不安全网络上的主机不知道该网络主机的存在，并且无法尝试与它们通信。同样，连接你的不安全网络到互联网的路由器不知道内部安全网络的存在，并且永远不会将数据包直接路由到内部网络的主机。

# 启动 Linux 路由器

要将计算机作为基于 Linux 的路由器启动，只需插入之前创建的启动磁盘并重启计算机。你的计算机应该从软盘启动。随后软件将创建一个 RAM 磁盘并将启动磁盘的内容加载到 RAM 磁盘中。整个路由器从 RAM 运行。你所做的任何配置更改都可以保存到启动磁盘，这样在下次启动时，你的配置就会被保留。

在你提示以 root 用户身份登录且无需密码后，Linux 路由器启动，并向你显示图 31.5 所示的配置菜单。让我们按照之前的描述通过以下步骤运行一个最小网络：

- 1. 网卡模块：取出你创建的第二张软盘。假设你将其挂载到 `/mnt/floppy` 目录，从 `/mnt/floppy` 目录将你每张已安装网卡所需的所需的模块 `copy`（复制）到 `/lib/modules` 目录。

- 2. 基本设置：配置两个以太网卡的 IP 地址、网络掩码和路由。

- 3. 基本安全：配置实现网络地址转换所需的网络安全设置。

- 4. 进一步配置：配置额外的网络参数，例如名称服务器（DNS）和主机表。

# 图 31.5：Linux Router Project 主菜单

![](img/fd2d9aa64b3d05a8fce65954a79484_752_0.png)

菜单完全是数字化的，通过输入数字并按回车键访问。例如，在主配置菜单上为网络设置（Network Settings）输入 1 将显示网络设置子菜单。在子菜单上选择一个项目将在简单的编辑器中打开文件进行编辑（用于配置）。为了有效使用编辑器，你真的需要知道如何保存（按 `Ctrl+W` 然后按回车确认文件名）和退出（按 `Ctrl+C`）。如果你不记得这些命令，在编辑器中按 F1。

# 安装网卡模块
