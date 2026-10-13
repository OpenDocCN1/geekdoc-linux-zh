
通常情况下，每个服务有两个条目，因为大多数服务可以使用 TCP 或 UDP 进行传输。通常在初始配置 `/etc/services` 后，你将不需要更改它。

## 更改命名服务后使用 `/etc/nsswitch.conf`

此文件最初由 Sun Microsystems 开发，用于指定系统访问信息的顺序。（此处省略原文中大量重复的句子，以保持翻译逻辑一致性）。

# 第 18 章 网络连接性

## 图形化配置工具

如前所述，如果你是网络新手或尚未精通命令行，图形化配置工具是你在配置 Fedora 新硬件的最佳方法。与大多数图形工具一样，`system-config-network` 允许你填写内容；点击按钮，由工具修改所需的文件。记住，必须以 root 身份运行 `system-config-network`。

启动 `system-config-network` 有两种方法：从 X11 终端窗口的命令行输入 `system-config-network`；使用面板的运行应用程序；或点击 GNOME 或 KDE 桌面面板的系统设置中的网络项目。（在任何情况下，都会提示输入 root 密码。）

启动后，`system-config-network` 可能会询问你是否创建一个新设备。然而，如果你在带有网卡的计算机上安装了 Fedora，启动 `system-config-network` 后会显示图 18.1 所示屏幕。

![](img/d4ad9a7c85702c925b4288f587284a4f_515_0.png)

图 18.1 使用初始 `system-config-network` 开始配置网络客户端主机

点击 DNS 标签页配置系统的 DNS 设置、主机名或 DNS 搜索路径。点击 Hosts 标签页，然后点击 New 或 Edit 按钮（选择主机后）来创建或编辑系统 `/etc/hosts` 文件中的条目，例如添加

# 第 18 章 网络连接

你网络上主机的 IP 地址、主机名和别名。请参图 18.2 查看编辑主机条目的示例。

![](img/d4ad9a7c85702c925b4288f587284a4f_516_0.png)

图 18.2 亮显示条目，然后点击“编辑 (Edit)”按钮以更改“网络配置”屏幕中“主机”选项卡中的 `/etc/hosts` 条目。

点击“设备 (Devices)”选项卡，然后点击“新建 (New)”或选择一个以太网设备来自动或手动设置以太网设备。图 18.3 显示了“添加设备类型 (Add Device Type)”对话框，其中已准备好用于静态（或固定）IP 地址分配的所有必要信息。选择你的网卡如何获取配置：是手动从动态主机配置协议（DHCP，见下一节）还是从 Bootp 获取。根据需要填写空白处。

![](img/d4ad9a7c85702c925b4288f587284a4f_516_1.png)

图 18.3 在“添加新设备类型”对话框的“配置网络设置”屏幕中配置以太网设备。

## 动态主机配置协议

> 注意
> Bootp 是 DHCP 构建的初始协议，它已大部分被 DHCP 取代。

当你配置网卡（NIC）或为网卡编辑 IP 地址或分配方案时，请使用“文件 (File)”菜单下的“保存 (Save)”项保存更改。请注意，你也可以使用“配置 (Profile)”菜单（如之前的图 18.1 所示）为你的网卡创建不同的网络配置和 IP 地址分配。如果你想在运行 Fedora 的笔记本电脑上创建（例如）为家里或工作创建不同的网络设置，这非常方便。

# 动态主机配置协议

顾如其名，动态主机配置协议 (`DHCP`) 用于配置主机连接到你的网络。`DHCP` 允许网络管理员在网卡连接到网络激活时，为每个主机配置所有的 TCP/IP 参数。这些参数包括自动为网卡分配 IP 地址、在 `/etc/resolv.conf` 中设置名称服务器条目以及为主机配置默认网关信息。本节首先描述如何通过 `DHCP` 获取网卡的 IP 分配，以及如何使用 Fedora 正确设置并启动 `DHCP` 服务器。

> 注意
> 你可以通过阅读 RFC2131 “动态主机配置协议”了解更多关于 `DHCP` 的信息。
> 访问 http://www.ietf.org/rfc/rfc2131.txt。

## DHCP 如何工作

`DHCP` 通过持有每个可能连接到网络的客户端的信息来提供网络参数的持久化存储。最常见的三个参数是：
- 子网掩码
- 默认网关
- DNS 服务器

`DHCP` 客户端通过以下步骤工作：
1. 获取 `DHCP` 发现 (`Discovery`) 报
2. 获取 `DHCP` 提供 (`Offer`) 报
3. 获取 `DHCP` 请求 (`Request`) 报
4. 获取 `DHCP` 确认 (`Acknowledgment`) 报

本节首先描述如何通过 `DHCP` 为你的网卡获取 IP 分配，以及如何使用 Fedora 正确设置并启动 `DHCP` 服务器。

- `timeout time`；超时时间；放弃尝试之前等待多久（默认为 60 秒）
- `retry time`；重试时间；重试之前等待多久（默认为 5 分钟）
- `select-timeout time`；选择超时；在选择 `DHCP` 议之前等待多久（默认为 0 秒）
- `reboot time`；重启时间；重新获取之前设置的 IP 之前等待多久（默认为 10 秒）
- `renew date`；更新日期；何时租约 IP 许可，日期格式为 `<星期> <年份>/<月份>|<日>:<分钟>:<秒>`，例如 `4 2004/1/1 22:01:00` 代表 2004年1月4日星期四

有关更多设置的信息，请参阅 `dhclient.conf` 手页。

## DHCP 服务器

再次，在计算机上安装 `DHCP` 服务器最简单的方法是在安装时包含 RPM 包，或者在安装机器时没有安装 `DHCP` 服务器 RPM 包的情况下使用 RPM 包。如果你在线，可以前往互联网软件联盟 (`ISC`) 网站并自行编译源码 (http://www.isc.org/)。

如果你决定从 `ISC` 网站下载源码进行安装，安装过程非常简单。解压你的 tar 文件，在源码目录根目录下运行 `./configure`，运行 `make`，最后如果没有错误，运行 `install`。这会将 `DHCP` 守护进程使用的所有文件放在正确的位置。如果你有磁盘空间，最好在确定 `DHCP` 运行正常之前将源码文件留在原处；否则，你可以删除源码树。

> 注意
> 无论你选择何种安装方法，请确保创建了 `/etc/dhcpd.leases` 文件。该文件可以是空的，但它必须存在，以便 `dhcpd` 正常启动。

## 使用 DHCP 配置网络主机

使用 `DHCP` 配置网络可能看起来很困难，但如果你的需求简单，实际上非常容易。如果你的网络更复杂，并且取决于你想让 `DHCP` 执行多少工作，服务器配置可能需要花费更多精力。

## DHCP 服务器配置

配置服务器需要一些思考和一点运气。这项工作仅涉及编辑一个配置文件 `/etc/dhcpd.conf`。若要在系统启动时启动服务器，请使用 `service`、`ntsysv` 或 `system-config-services` 命令。

# 动态主机配置协议 485

`/etc/dhcpd.conf` 文件包含了运行 `dhcpd` 需要的所有信息。Fedora 在 `/usr/share/doc/dhcpd/dhcpd.conf.sample` 中包含了一个示例 `dhcpd.conf`。`DHCP` 服务器文件也包含一个示例 `dhcpd.conf` 文件。

`/etc/dhcpd.conf` 文件可以看作由三部分组成。第一部分包含 `DHCP` 自身的配置。配置包括：

- 设置域名—`option domain-name "example.org"`
- 设置 DNS 服务器—`option domain-name-servers ns1.example.org, ns2.example.org`（可以使用 IP 地址替换）
- 设置默认和最大租约时间—`default-lease-time 3600` 和 `max-lease-time 14400`

第一部分中的其他设置还包括服务器是否为主服务器（权威服务器）以及 `DHCP` 使用什么种类型的日志。这些设置被视为默认值，在更复杂的情况下，可以通过配置中的子网和主机部分进行覆盖。

> 注意
> `dhcpd.conf` 文件在每个命令语句后都需要加分号 (`;`)。如果你的配置失败出现错误或运行不正常，请检查此项。

`dhcpd.conf` 的下一部分处理你的 `DHCP` 服务器所服务的不同子网；这部分非常直观。每个子网单独定义，其格式如下：

```
10.5.5.0 netmask 255.255.255.224 {

  range 10.5.5.26 10.5.5.30;

  option domain-servers ns1.internal.example.org;

  option domain-name "internal.example.org";

  option routers 10.5.5.1;

  option broadcast-address 10.5.5.31;

  default-lease-time 600;
```
