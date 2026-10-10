
## linux-wlan

`linux-wlan` 项目 (`www.linux-wlan.org`) 开发了一组无线驱动，设计用于支持新 802.11 无线标准的 Prism 基网卡。`linux-wlan` 驱动目前未包含在 Fedora 中；现在你必须下载驱动。当前的包是 `linux-wlan-ng`。你必须解包并编译驱动。

驱动将安装 WLAN 设备，设备配置放在 `/etc/sysconfig/network-scripts` 目录下。例如，第一个 WLAN 设备的配置将在 `ifcfg-wlan0` 脚本中。通用无线选项放在 `/etc/wlan.conf` 配置文件中。

## 设置你的防火墙：system-config-firewall

要设置防火墙，请在系统上运行 `system-config-firewall`（“系统管理”窗口和菜单中的“防火墙”）。Fedora 9 使用了一个名为 `system-config-firewall` 的新系统配置工具来设置防火墙（见图 14-6）。这取代了不再使用的 `system-config-securitylevel`（SELinux 使用一个名为 `system-config-selinux` 的独立工具进行配置）。

![](img/9a8872dc6f2acaed163529fd9d421e05_462_0.png)

**图 14-6：显示防火墙信任服务的 system-config-firewall**

你可以在直接连接互联网的独立系统上运行防火墙，也可以在连接本地网络和互联网的网关系统上运行防火墙。大多数网络使用专用路由器访问互联网，这些路由器有自己的防火墙。如果你决定使用 Linux 系统作为网关，它将至少有两个网络连接：一个用于本地网络，另一个是用于互联网的连接设备。确保将防火墙应用于互联网设备，而不是本地网络。

顶部栏具有防火墙向导按钮、用于生效任何更改的应用按钮、用于恢复已保存防火墙的重新加载按钮，以及禁用和启用按钮。你可以通过启用和禁用按钮来启用或禁用你的防火墙（见图 14-6）。如果防火墙处于激活状态，则只能使用“禁用”按钮，反之亦然。

系统已有一有一个默认配置。要创建你自己的基础自定义配置，只需点击向导按钮运行向导即可。

你也可以直接对不同的防火墙组件进行更改。防火墙配置窗口将显示多个面板，从侧边栏的条目中选择。这些面板分别是信任服务（Trusted Services）、其他端口（Other Ports）、信任接口（Trusted Interfaces）、伪装（Masquerading）和自定义规则（Custom Rules）。

许多用户可能想要更改的功能是信任服务。Linux 系统通常用于为网络运行服务器。如果你正在创建一个强大的防火墙，但仍希望运行如 Web 服务器之类的服务、允许用户在互联网上进行 FTP 文件传输、允许 Samba 桌面浏览或允许如 SSH 等远程加密连接，你必须在“信任服务”面板中指定它们。Samba 桌面浏览让你能够从 GNOME 或 KDE 桌面访问你的 Samba 共享（类似于远程 Windows 文件系统）。

“其他端口”部分允许你指定可能为服务开放的端口，例如 BitTorrent（见图 14-7）。点击“添加”按钮打开对话框，你可以在其中输入端口号以及要控制的协议（`tcp` 或 `udp`）。

![](img/9a8872dc6f2acaed163529fd9d421e05_463_0.png)

**图 14-7：防火墙其他端口配置**

“信任接口”面板允许你选择那些可以信任的硬件网络连接，如网卡、调制解器或无线连接（见图 14-8）。这通常适用于连接到本地网络或直接连接到本地路由器或服务器（打印服务器）的接口。连接到互联网等更广泛网络的接口不应被信任。

![](img/9a8872dc6f2acaed163529fd9d421e05_464_0.png)

**图 14-8：防火墙信任接口**

![](img/9a8872dc6f2acaed163529fd9d421e05_464_1.png)

**图 14-9：防火墙伪装**

如果你的系统被用本地网络的互联网网关，你可以实施伪装来隐藏本地主机，防止来自互联网的外部访问（见图 14-9）。尽管如此，这还需要 IP 转发，IP 转发在你选择伪装时会自动启用。本地主机仍然能够访问互联网，但它们将伪装成你的网关系统。你应该选择连接到互联网的接口进行伪装。伪装仅适用于 IPv4 网络，不适用于 IPv6 网络。

“自定义规则”面板允许你加载包含自定义防火墙规则的 IP-tables 文件（见图 14-10）。你不需要选择是使用 `system-config-firewall` 还是在 IP-tables 文件中创建整套规则，而是可以使用 `system-config-firewall` 自动配置标准防火墙规则，然后设置一个只包含你系统自定义规则的 IP-tables 文件。这些规则将被添加到标准规则集中。你还需要确定 IPTables 文件包含的是 IPv4 还是 IPv6 协议规则（地址类型）。你还需要选择防火墙规则适用于哪个表。有三种选择：`filter`（Netfilter 规则）、`mangle`（mangle 表）和 `nat` 表。使用“文件”条目打开浏览器以定位你想要加载的 IPTables 文件。

![](img/9a8872dc6f2acaed163529fd9d421e05_465_0.png)

## 设置 Windows 网络访问：Samba

大多数本地网络和家庭网络可能包含运行在 Microsoft Windows 上的系统以及其他运行在 Linux 上的系统。你可能需要让 Windows 计算机访问 Linux 系统，反之亦然。Windows 由于其巨大的市场存在率，往往从两者中受益。

一种解决方案是在 Linux 上启用 Samba。要允许 Windows 访问 Linux 系统以及让 Linux 访问 Windows，请使用 Samba 服务器。首先确保已安装 Samba。在“应用程序”中打开“添加/删除软件”工具。点击“浏览”面板，向下滚动选择左侧框中的“服务器”条目。然后勾选右侧框中的“文件服务器”条目。如果该项目未勾选，请勾选它。同时确保“服务器配置”也被勾选。如果尚未安装，请点击“应用”进行安装。

Samba 有两种身份验证方法：共享和用户。用户身份验证要求 Windows 和 Linux 系统都有相应的账户。它们可以具有相同的名称，尽管 Windows 用户可以映射到 Linux 账户。共享可以对任何用户开放，并作为用户存储空间的扩展。

使用 `system-config-services` 配置（系统管理 | 服务）让 Samba 自动启动（见图 14-11）。在“后台服务”面板中，勾选 `smbd` 和 `nmb` 条目的复选框。点击“保存”保存启动规范，并点击“重启”启动 Samba 服务器。

要在 Linux 系统上设置文件共享，你首先需要配置 `/etc/samba/samba.conf` 文件，或使用 `system-config-samba` 工具（系统管理 | Samba）。如果你编辑 `/etc/samba/samba.conf` 文件，你首先需要指定你的 Windows 网络名称。

### system-config-samba

`system-config-samba` 工具提供了一种配置 Samba 服务器的简单方法，添加 Samba 用户并指定 Samba 共享。它还将自动将 Linux 系统上的所有打印机配置为 Samba 共享打印机，允许从任何连接的 Windows 系统使用它们。你可以从“系统管理”菜单中的“Samba”条目启动 `system-config-samba`。`system-config-samba` 工具将列出服务器的所有共享。你可以使用顶部的按钮管理共享，添加新的共享或删除当前的共享。失去作为共享目录的状态。

## 第 14 章：网络配置

注意：作为 `system-config-samba` 的替代方案，你可以使用 SWAT，这是一种支持复杂配置的 Samba 浏览器工具。请安装 `swat` 包和 `xinetd` 包。务必同时使用 `chkconfig` 工具启用 swat。SWAT 将托管 Samba 服务器的系统的 901 端口访问。

### Samba 服务器配置

要配置你的 Samba 服务器，请从 `system-config-samba` 属性（Preferences）菜单中选择“服务器设置（Server Settings）”。这将打开一个包含两个面板的窗口：基本（Basic）和安全（Security）（见图 14-13）。在“基本”面板上，你输入 Samba 服务器组名称。这应与你的 Windows 系统使用的名称相同。Windows 提供的默认名称是 MSHOME 或 WORKGROUP。请使用已经为你的 Windows 网络指定的名称。对于家庭网络，你可以自行决定。只需确保你的所有电脑都使用相同的网络名称。检查你的 Windows 控制面板中的“系统”小部件以确认。

描述（Description）是你希望在 Windows 系统上显示的 Samba 服务器的名称。在“安全”面板上，你可以指定身份验证模式、密码加密选项、宾客账户名称以及身份验证服务器。

![](img/9a8872dc6f2acaed163529fd9d421e05_468_0.png)

图 14-13：Samba 服务器设置

默认使用用户安全（User security）。你也可以使用共享安全（share security）或服务器安全（server security），这些更加开放，但两者都已弃用，并可能在后续版本中被删除。

- 身份验证模式指定访问级别，可以是用户（user）、共享（share）、服务器（server）、ADS 或域（domain）。用户级访问通过用户密码限制访问，而共享级则允许任何宾客访问。
- 通常，你会选择加密密码，而不是以明文形式通过网络传输密码。
- 宾客用户（Guest user）是允许访问你想要向任何用户开放共享或打印机的账户名称，无需提供密码。弹出菜单将列出你当前的所有用户，默认选择“无宾客账户（No Guest Account）”。除非你想让所有人访问共享，否则你不需要宾客账户。

### 添加 Samba 用户

对于用户身份验证，你必须将 Windows 用户与特定的 Samba 用户关联。Samba 为用户维护其自有的密码列表。要使用 Samba 访问，你需要将用户注册为 Samba 用户。从属性菜单中选择“Samba 用户（Samba Users）”打开 Samba 用户窗口，点击“添加用户（Add User）”按钮。在这里输入 Unix 用户名（Unix Username）、Windows 用户名（Windows Username）和 Samba 密码（Samba Password）。还有一个框用于 Samba 密码。Unix 用户名是一个弹出窗口，列出了你 Samba 服务器上的所有用户。

在 `system-config-samba` 属性菜单中选择“Samba 用户”。这将打开列出所有当前 Samba 用户的 Samba 用户窗口。这些对应于系统中已设置的用户账户。要添加 Samba 用户，点击右侧的“添加用户”按钮。这将打开一个带有四个条目的“创建 Samba 用户（Create Samba User）”窗口（见图 14-14）。在这里输入 Unix 用户名、Windows 用户名和 Samba 密码。还有一个框用于 Samba 密码。Unix 用户名是一个弹出窗口，列出了托管你 Samba 服务器的 Linux 系统上的所有用户。

![](img/9a8872dc6f2acaed163529fd9d421e05_469_0.png)

图 14-14：添加 Samba 用户

从 Unix 用户名下拉菜单中选择一个 Linux 用户，然后输入对应的 Windows 用户名。Windows 用户名可以与 Linux 账户（Linux用户名）不同。然后输入 Windows 用户访问 Linux 时使用的密码。这就是该用户的 Samba 密码。Samba 维护自己的密码集，用户访问 Samba 共享时需要这些密码。当 Windows 用户想要访问 Samba 共享时，他们需要他们的 Samba 密码。

一旦你创建了 Samba 用户，其名称将出现在 Samba 窗口的 Samba 用户列表中。要稍后修改或删除 Samba 用户，使用相同的 Samba 用户窗口，从列表中选择用户，并点击“编辑用户（Edit User）”按钮更改密码等条目，或点击“删除用户（Delete User）”按钮移除 Samba 用户。

![](img/9a8872dc6f2acaed163529fd9d421e05_470_0.png)

图 14-15：创建 Samba 共享

### 在 Linux 系统上添加 Samba 共享

要设置简单共享，点击“添加共享（Add Share）”，这将打开“创建 Samba（Create Samba）”窗口。在“基本”面板上，选择要共享的 Linux 目录（点击“浏览”查找），然后指定它是否可写且可见。你还为共享提供一个名称以及你想要的任何描述（见图 14-15）。

在“访问（Access）”面板上，你可以限制某些用户访问或允许所有用户访问。系统上的所有 Samba 用户将列在复选框中，你可以从中选择想要获得权限的用户（见图 14-16）。

一旦创建，共享将出现在主 `system-config-samba` 窗口。将显示共享的目录、共享名称、可见性、读/写权限和描述。要稍后修改共享，点击其条目，然后点击“属性（Properties）”菜单。这将打开“编辑 Samba 共享”窗口，具有与你创建共享时相同的“基本”和“访问”面板。

![](img/9a8872dc6f2acaed163529fd9d421e05_471_0.png)

图 14-16：创建 Samba 共享：访问

### 访问 Samba 共享

对于大多数网络，使用专用路由器建立网络，提供域名服务（DNS）、防火墙和地址解析。你可以使用 Linux 来提供这些服务，但通常只有当你需要自定义配置或想直接控制防火墙、DNS 和地址解析时才需要。

## 附录：获取 Fedora

Fedora Linux 发行版安装了专业级且稳定的 Linux 系统，带有 KDE 和 GNOME 图形界面、灵活且易用的系统配置工具、丰富的互联网服务器、各种多媒体应用以及数千种 Linux 应用。你可以在 `redhat.org` 找到关于 Red Hat Fedora 项目的最新条目。

### 下载镜像

要获取 Fedora 9，只需访问 Fedora 项目网站并点击“Get Fedora”链接。在这里你将看到 btorrent 或用于不同 Fedora 安装 DVD 和 Live 版本的直接下载链接。直接下载链接指向当前可用的镜像站点。
