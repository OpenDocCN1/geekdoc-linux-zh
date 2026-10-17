
不过，您可以微调 `dhclient` 的工作方式，以及它在哪里以及如何获取或查找 DHCP 信息。您可能不需要花费额外的精力；但如果您需要，您可以创建并编辑一个名为 `dhclient.conf` 的文件，并将其与您的设置一起保存在 `/etc` 目录中。`dhclient.conf` 的一些选项包括：

- `timeout time ;` — 在放弃尝试之前等待多久（默认值为 60 秒）
- `retry time ;` — 在重试之前等待多久（默认值为 5 分钟）
- `select-timeout time ;` — 在选择 DHCP 提议之前等待多久（默认值为 0 秒）
- `reboot time ;` — 在尝试获取之前设置的 IP 之前等待多久（默认值为 10 秒）
- `renew date ;` — 何时续订 IP 租约，其中 `date` 的格式为 `<weekday><year>/<month>/<day> <hour>:<minute>:<second>`，例如 `4 2004/1/1 22:01:01` 表示 2004 年 1 月 4 日星期四下午 10:01。

有关其他设置的更多信息，请参见 `dhclient.conf` man 手册页。

## DHCP 服务器

再次强调，在您的计算机上安装 DHCP 服务器最简单的方法是在安装时包含 RPM 软件包，或者如果您在没有安装 DHCP 服务器 RPM 软件包的情况下安装了机器，则使用 RPM 软件包。如果您愿意，您可以前往互联网软件联盟（ISC）网站并自行下载和构建源代码（[http://www.isc.org](http://www.isc.org)）。

如果您选择从从 ISC 网站下载的源代码进行安装，安装过程非常简单。只需解包 tar 文件，在源代码目录的根目录下运行 `./configure`，然后运行 `make`，最后，如果没有错误，请运行 `make install`。这将把 DHCP 守护进程使用的所有文件放在正确的位置。如果您有足够的磁盘空间，最好保留源文件，直到您确定 DHCP 正常运行；否则，您可以删除源代码树。

> **注意**
>
> 无论您选择哪种安装方法，请确保创建了一个名为 `/etc/dhcpd.leases` 的文件。该文件可以为空，但它必须存在，`dhcpd` 才能正常启动。

## 使用 DHCP 配置网络主机

使用 DHCP 配置网络可能看起来很困难，但如果您的需求简单，实际上很容易。如果您的网络更复杂并且取决于您希望 DHCP 承担多少工作，服务器配置可能需要多花一点功夫。

## DHCP 服务器配置

配置服务器需要一些思考和工作。幸运的是，这项工作仅涉及编辑单个配置文件，`/etc/dhcpd.conf`。要在启动时启动服务器，请使用 `service`、`ntsysv` 或 `system-config-services` 命令。

`/etc/dhcpd.conf` 文件包含运行 `dhcpd` 所需的所有信息。Fedora 在 `/usr/share/doc/dhcp*/dhcpd.conf.sample` 中附带了一个 `dhcpd.conf` 示例。DHCP 服务器源代码文件也包含一个 `dhcpd.conf` 示例文件。

可以将从 `/etc/dhcpd.conf` 文件视为一个三部分组成文件。第一部分包含 DHCP 本身的配置。配置包括

- **设置域名**——`option domain-name "example.org"`。
- **设置 DNS 服务器**——`option domain-name-servers ns1.example.org, ns2.example.org`（可以替换为 IP 地址。）
- **设置默认和最大租约时间**——`default-lease-time 3600` 和 `max-lease-time 14400`。

第一部分中的其他设置包括服务器是否为主要（权威）服务器以及 DHCP 应使用哪种类型的日志记录。这些设置被视为默认值，在更复杂的情况下，可以通过配置中的子网和主机部分进行覆盖。

> **注意**
>
> `dhcpd.conf` 文件要求在每个命令语句后加分号 (`;`)。如果配置文件有错误或运行不正确，请检查这一点。

`dhcpd.conf` 的下一部分处理您的 DHCP 服务器服务不同的子网；这部分相当简单明了。每个子网单独定义，可以如下所示：

```
subnet 10.5.5.0 netmask 255.255.255.224 {
  range 10.5.5.26 10.5.5.30;
  option domain-name-servers ns1.internal.example.org;
  option domain-name "internal.example.org";
  option routers 10.5.5.1;
  option broadcast-address 10.5.5.31;
  default-lease-time 600;
  max-lease-time 7200;
}
```

这定义了 10.5.5.0 子网的 IP 编址。它定义了 IP 地址范围从 10.5.5.26 到 10.5.5.30，以便动态分配给驻留在该子网的主机。此示例表明，TCP/IP 的任何选项都可以在配置文件子网部分中设置。它显示了子网将连接到哪个 DNS 服务器，这对于 DNS 服务器负载均衡可能很好，或者也可以用于限制可通过 DNS 到达的主机。它定义了域名，因此您可以在网络上拥有多个域。它还可以更改默认和最大租约时间。

如果您希望服务器忽略特定子网，可以使用以下条目来实现：

```
subnet 10.152.187.0 netmask 255.255.255.0 { }
```

这为 10.152.187.0 子网未定义任何选项；因此，DHCP 服务器忽略它。

`dhcp.conf` 的最后一部分用于定义主机。如果您希望网络中的某台计算机拥有特定的 IP 地址或特定于该主机的其他信息，这很有用。完成主机部分的关键在于知道主机的硬件地址。正如您在本章前面“用于网络硬件设备”中所学到的，硬件地址用于区分主机以进行配置。您可以按照前述描述使用 `ifconfig` 命令获取您的硬件地址。硬件地址位于标记为 “Hwaddr” 的 eth0 行上：

```
host fantasia {
  hardware ethernet 08:00:07:26:c0:a5;
  fixed-address fantasia.fugue.com;
}
```

此示例获取具有硬件地址 08:00:07:26:c0:a5 的主机，并执行 DNS 查找，以将 `fantasia.fugue.com` 的 IP 地址分配给该主机。

DHCP 还可以像这样为无盘客户机定义和配置引导：

```
host passacaglia {
  hardware ethernet 0:0:c0:5d:bd:95;
  filename "vmlinx.passacaglia";
  server-name "toccata.fugue.com";
}
```

无盘主机 *passacaglia* 将从服务器 *toccata.fugue.com* 获取引导信息，并使用 *vmlinx.passacaglia* 内核。还可以包含所有其他 TCP/IP 配置。

> **警告**
>
> 请记住，为避免出现问题，本地网络中只能存在一个 DHCP 服务器。在运行过时遗留操作系统的网络中，您的 DHCP 可能无法正常工作。通常 Windows NT 服务器会默认安装 Windows DHCP 服务器。由于没有可供 NT 筛选的配置文件，如果两台机器在同一局域网中，该 DHCP 服务器将在 Linux 服务器之前配置您的主机。检查您的 NT 服务器是否存在这种情况，并禁用 NT 服务器上的 DHCP；之后，您其他启用 DHCP 的主机应能正确配置。此外，如果您使用电缆或 DSL 调制解调器、无线接入点 (WAP) 或其他可以提供 DHCP 的智能路由器，请检查是否存在冲突，并确保您的局域网中没有此类设备。

### DHCP 的其他用途

在 `dhcpd.conf` 中可以使用大量选项：整个书籍都致力于介绍 DHCP。最全面的书籍是 ***The DHCP Handbook***，可在 http://www.dhcp-handbook.com/ 获得。您可以定义 NIS 域、配置 NETBIOS、设置子网掩码、定义时间服务器，或许多其他类型的服务器——举几个例子即可说明您可以使用的 DHCP 选项。前面的示例可以让您的 DHCP 服务器和客户端运行起来。

DHCP 服务器发行版中包含一个 `dhcpd.conf` 文件的示例，您可以将其用作网络的模板。该文件显示了一个基本配置，其中包含对所使用选项的解释，可帮助您入门。

## 无线联网

正如前文所述，自 20 世纪 90 年代初开发第一个标准以来，Linux 就支持无线联网。随着计算机变得越来越小，无线联网的用途越来越多；与此同时，传输速度一直在提高。创建无线联网有多种不同的方法。以下部分将向您介绍您可以在 Fedora 系统上用于初始化、配置和管理无线联网的多个 Linux 命令。

## Fedora 对无线联网的支持
