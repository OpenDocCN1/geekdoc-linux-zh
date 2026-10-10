
## 微调 dhclient
不过，您可以微调 dhclient 的工作方式，以及它获取或查找 DHCP 信息的位置和方式。您可能无需付出这些额外努力；但如果需要，您可以创建并编辑一个名为 `dhclient.conf` 的文件，并将您的设置保存在 `/etc` 目录中。`dhclient.conf` 的选项包括以下几项：

- **timeout time ;**—放弃尝试前的等待时间（默认为 60 秒）
- **retry time ;**—重试前的等待时间（默认为 5 分钟）
- **select-timeout time ;**—选择 DHCP 提议前的等待时间（默认为 0 秒）
- **reboot time ;**—尝试获取先前设置的 IP 地址前的等待时间（默认为 10 秒）
- **renew date ;**—续租 IP 地址租约的时间，其中 date 的格式为 `<weekday><year><month><day><hour><minute><second>`，例如 `4 2004/1/1 22:01:01` 代表 2004 年 1 月 4 日星期四下午 10:01:01。

有关其他设置的更多信息，请参阅 `dhclient.conf` 手册页。

## DHCP 服务器
同样，在计算机上安装 DHCP 服务器最简单的方法是，在安装时包含相应的 RPM 包，或者如果您在未安装 DHCP 服务器的情况下安装了机器，可以使用 yum。如果您愿意，还可以前往互联网软件委员会（ISC）网站，自行下载并构建源代码（http://www.isc.org/）。

如果您决定从 ISC 网站下载的源代码进行安装，安装过程非常简单。只需解压您的 tar 文件，从源代码目录的根目录运行 `./configure`，运行 `make`，最后，如果没有错误，运行 `make install`。这将把 DHCP 守护进程使用的文件放到正确的位置。最好保留源代码文件，直到您确定 DHCP 运行正常；否则，您可以删除源代码树。

**注意**
无论您选择哪种安装方法，请务必确保创建了名为 `/etc/dhcpd.leases` 的文件。该文件可以为空，但 `dhcpd` 的正常启动需要该文件存在。

## 使用 DHCP 配置网络主机
使用 DHCP 配置网络可能看起来很难，但如果您的需求简单，其实很容易。如果网络更复杂，或者您希望 DHCP 执行更多任务，服务器配置可能需要更多的努力。

## DHCP 服务器配置
配置服务器需要深思熟虑和少量工作。幸运的是，这项工作只涉及编辑单个配置文件 `/etc/dhcpd.conf`。要在启动时启动服务器，请使用 `service` 命令或基于 GUI 的 `system-config-services`。

`/etc/dhcpd.conf` 文件包含运行 `dhcpd` 所需的所有信息。Fedora 在 `/usr/share/doc/dhcp*/dhcpd.conf.sample` 中包含了一个示例 `dhcpd.conf`。DHCP 服务器源代码文件也包含一个示例 `dhcpd.conf` 文件。

`/etc/dhcpd.conf` 文件可以看作是一个三部分文件。第一部分包含 DHCP 本身的配置。这些配置包括

- 设置域名—`option domain-name "example.org"`。
- 设置 DNS 服务器—`option domain-name-servers ns1.example.org, ns2.example.org`（可以替换为 IP 地址）。
- 设置默认和最大租约时间—`default-lease-time 3600` 和 `max-lease-time 14400`。

第一部分中的其他设置包括服务器是否为初级（权威）服务器以及 DHCP 应使用哪种类型的日志记录。这些设置被视为默认值，在更复杂的情况下，可以被配置中的子网和主机部分覆盖。

> `dhcpd.conf` 文件要求每个命令语句后面都加分号 (;)。如果您的配置文件有错误或运行不当，请检查这一点。

`dhcpd.conf` 的下一部分处理您的 DHCP 服务器提供的不同子网；这一部分非常简单明了。每个子网都是单独定义的，看起来可能如下所示：

```
subnet 10.5.5.0 netmask 255.255.255.224 {
range 10.5.26 10.5.5.30;
option domain-name-servers ns1.internal.example.org;
option domain-name "internal.example.org";
option routers 10.5.5.1;
option broadcast-address 10.5.5.31;
default-lease-time 600;
max-lease-time 7200;
}
```

这定义了 10.5.5.0 子网的 IP 寻址。它定义将 10.5.5.26 到 10.5.5.30 的 IP 地址范围动态分配给位于该子网上的主机。此示例表明，TCP/IP 的任何选项都可以在配置文件的子网部分进行设置。它显示了子网将连接到哪个 DNS 服务器，这对于 DNS 服务器负载均衡很有用，或者可用于限制可以通过 DNS 到达的主机。它定义了域名，因此您可以在网络上拥有多个域。还可以更改默认和最大租约时间。

如果您希望服务器忽略特定的子网，可以使用以下条目来实现：

```
subnet 10.152.187.0 netmask 255.255.255.0 {
}
```

这为 10.152.187.0 子网没有定义任何选项；因此，DHCP 服务器将忽略它。

您的 `dhcp.conf` 的最后一部分用于定义主机。如果您希望网络上的计算机具有特定的 IP 地址或该主机特有的其他信息，这将很有用。完成主机部分的关键是知道主机的硬件地址。硬件地址用于区分以进行配置的主机。您可以按照前面描述的方法，使用 `ifconfig` 命令获取硬件地址。硬件地址位于标记为 “HWaddr” 的 `eth0` 行上。

```
host fantasia {
    hardware ethernet 00:00:07:26:c0:a5;
    fixed-address fantasia.fugue.com;
}
```

此示例获取硬件地址为 00:00:07:26:c0:a5 的主机，并执行 DNS 查找，将 `fantasia.fugue.com` 的 IP 地址分配给该主机。

DHCP 还可以像这样定义和配置无盘客户端的启动：

```
host passacaglia {
    hardware ethernet 0:0:c0:5d:bd:95;
    filename “vmunix.passacaglia”;
    server-name “toccata.fugue.com”;
}
```

无盘主机 `passacaglia` 从服务器 `toccata.fugue.com` 获取其启动信息，并使用 `vmunix.passacaglia` 内核。还可以包含所有其他 TCP/IP 配置。

## **注意**
请记住，为了避免问题，本地网络上应该只有一个 DHCP 服务器。如果您的 LAN 上有主机运行过时的遗留操作系统，您的 DHCP 可能无法正常工作。通常 Windows NT 服务器默认安装了 Windows DHCP 服务器。由于没有配置文件供 NT 梳理，如果两台机器在同一 LAN 上，该 DHCP 服务器会在 Linux 服务器之前配置您的主机。检查您的 Windows NT 服务器是否存在这种情况，并禁用 Windows NT 服务器上的 DHCP；之后，您的其他启用 DHCP 的主机应该能正确配置。此外，如果您在 LAN 上使用可以提供 DHCP 的电缆或 DSL 调制解调器、无线接入点 (WAP) 或其他智能路由器，请务必确保没有冲突。

## DHCP 的其他用途
*dhcpd.conf* 中可以使用各种选项；有整整的书专门介绍 DHCP。最全面的书是 *The DHCP Handbook*，可在 http://www.dhcp-handbook.com/ 获取。您可以定义 NIS 域、配置 NETBIOS、设置子网掩码，并定义时间服务器或许多其他类型的服务器——仅列举您可以使用的 DHCP 选项中的几个。前面的示例将帮助您的 DHCP 服务器和客户端启动并运行。

DHCP 服务器发行版包含一个 *dhcpd.conf* 文件示例，您可以将其用作网络的模板。该文件展示了基本配置，并附带对所使用选项的解释，帮助您入门。

## 在 Fedora 中使用 IP 伪装
三个 IP 地址块保留用于内部网络和未直接连接到互联网的主机。地址范围是从 10.0.0.0 到 10.255.255.255，即 1 个 A 类网络；从 172.16.0.0 到 172.31.255.255，即 16 个 B 类网络；以及从 192.168.0.0 到 192.168.255.255，即 256 个 C 类网络。在为企业或家庭构建 LAN 时，请使用这些 IP 地址。您选择哪一类可能取决于网络上的主机数量。

您的内部网络的 Internet 访问可以由运行 Fedora 或其他宽带或拨号路由器的 PC 提供。该主机或设备连接到 Internet，并用作 Internet 网关，将信息转发到您的 LAN 以及从您的 LAN 传出。该主机还应用作防火墙，在作为 Internet 网关的同时保护您的网络免受恶意数据和用户的侵害。

以这种方式使用的 PC 通常至少有两个网络接口。一个连接到 Internet，另一个连接到 LAN 上的计算机（通过集线器或交换机）。一些宽带设备还集成了四个或更多交换网络接口。然后使用*网络地址转换*或 NAT（在 Linux 圈子中更常被称为 IP 伪装）在 LAN 和 Internet 之间传递数据。有关更多信息，请参阅第 30 章“保护您的机器”。

