
# linux-wlan

linux-wlan 项目（www.linux-wlan.org）开发了一套独立的无线驱动，为支持 802.11 无线标准的 Prism 无线卡设计。Fedora 目前没有安装 linux-wlan 驱动；你需要下载驱动。原始源码包从 linux-wlan 网站获取。目前的软件包是 `linux-wlan-ng`。你必须解压并编译驱动。驱动将安装 WLAN 设备，设备配置放置在 `/etc/sysconfig/network-scripts` 目录。例如，`ifcfg-eth0` 文件将包含设置。

第一个 WLAN 设备的配置将位于 `ifcfg-wlan0` 脚本中。通用无线选项放置在 `/etc/wlan.conf` 文件中。

## 设置防火墙：system-config-firewall

要设置防火墙，请在系统中运行 `system-config-firewall`（位于“系统管理”窗口和菜单中的“防火墙”）。Fedora 8 使用了一个名为 `system-config-firewall` 的新系统配置工具来设置防火墙（见图 14-6）。它取代了不再使用的 `system-config-securitylevel`（SELinux 使用名为 `system-config-selinux` 的独立工具进行配置）。

![](img/660de85fae8d68d8e30eb0e48a1ee77d_446_0.png)

你可以在直接连接互联网的独立系统上运行防火墙，也可以在连接本地网络与互联网的网关系统上运行。大多数网络使用专用的路由器访问互联网，这些路由器有自己的防火墙。相反，如果你决定使用 Linux 系统作为网关，它将至少有两个网络连接：一个用于本地网络，一个用于互联网的连接设备。请确保防火墙应用于互联网设备，而不是你的本地网络。

顶部按钮栏具有防火墙向导按钮、用于生效任何更改的“应用”按钮、恢复已保存防火墙的“重载”按钮以及“禁用”和“启用”按钮。你可以通过启用和禁用按钮来启用或禁用防火墙（见图 14-6）。如果防火墙处于激活状态，只能使用禁用按钮，反之亦然。

系统已有一个默认配置。要创建你自己的基础自定义配置，只需运行向导并点击向导按钮。

你还可以对不同的防火墙组件进行更改。防火墙配置窗口将显示多个面板，从侧边栏的项目中选择。这些面板分别是：信任服务（Trusted Services）、其他端口（Other Ports）、信任接口（Trusted Interfaces）、伪装（Masquerading）和自定义规则（Custom Rules）。

许多用户可能想要更改的功能是信任服务。如果你正在创建一个强大的防火墙，但仍希望运行如 Web 服务器之类的服务、允许用户在互联网上进行 FTP 文件传输、允许 Samba 桌面浏览，或允许 SSH 等远程加密连接，你必须在“信任服务”面板中指定它们。Samba 桌面浏览让你从 GNOME 或 KDE 桌面访问你的 Samba 共享（例如远程 Windows 文件）。

“其他端口”部分允许你指定可能为某些服务开放的端口，例如 BitTorrent（见图 14-7）。点击“添加”按钮打开对话框，你可以在其中输入端口号以及协议（tcp 或 udp）。

![](img/660de85fae8d68d8e30eb0e48a1ee77d_447_0.png)

图 14-7：防火墙其他端口配置

“信任接口”面板允许你选择可以信任的硬件网络连接，如网卡、调制解调器或无线连接（见图 14-8）。这通常适用于连接到本地网络或直接连接到本地路由器或服务器（如打印服务器）的接口。连接到互联网等更广网络的接口不应被信任。

![](img/660de85fae8d68d8e30eb0e48a1ee77d_448_0.png)

图 14-8：防火墙信任接口

![](img/660de85fae8d68d8e30eb0e48a1ee77d_448_1.png)

图 14-9：防火墙伪装

如果你的系统被用作本地网络的互联网网关，你可以实施伪装来隐藏本地主机免受来自的外部访问（见图 14-9）。然而，这还需要 IP 转发，该功能在你选择伪装时会自动启用。本地主机仍然能够访问互联网，但它们将伪装成你的网关系统。你应该选择连接到互联网的接口进行伪装。伪装适用于 IPv4 网络，不适用于 IPv6 网络。

“自定义规则”面板允许你加载包含自定义规则的 IP-tables 文件（你无需选择是使用 `system-config-firewall` 还是在 IP-tables 文件中创建一组规则，而是可以使用 `system-config-firewall` 自动配置标准防火墙规则，并设置一个仅包含你系统自定义规则的 IP-tables 文件。这将被添加到由 `system-config-firewall` 实现的标准集中。当你加载文件时，还必须确定 IPTables 文件包含的是 IPv4 还是 IPv6 协议规则（地址类型）。你还需要选择防火墙规则适用于何处。三个选择：filter（Netfilter 规则）、mangle（mangle 表）和 nat 表。使用“文件”条目打开浏览器以定位你想要加载的 IPTables 文件。

![](img/660de85fae8d68d8e30eb0e48a1ee77d_449_0.png)

图 14-10：防火墙自定义规则

## 设置 Windows 网络访问：Samba

大多数本地和家庭网络可能包含一些运行在 Microsoft Windows 上的系统以及运行在 Linux 上的系统。你可能需要让 Windows 访问 Linux 系统，或反之。Windows 由于其特殊性，倾向于需要特定的网络配置。要在 Linux 系统上设置简单的文件共享，你首先需要配置你的 Samba 服务器。你可以通过直接编辑 `/etc/samba/samba.conf` 文件或使用 `system-config-samba` 配置工具（系统管理 | Samba）。

`system-config-samba` 工具提供了配置 Samba 服务器的简单方法，用于添加 Samba 用户和指定 Samba 共享。它还会自动将你 Linux 系统上的所有打印机配置为 Samba 共享打印机，允许你从任何连接的 Windows 系统使用它们。你可以从系统管理菜单中的 Samba 启动 `system-config-samba`（见图 14-12）。`system-config-samba` 工具将列出服务器的所有共享。你可以使用顶部的按钮来管理共享，添加新的或删除当前的。如果你删除了，实际的目录不会被删除；它们只是失去了共享目录的状态。

### Samba 服务器配置

要配置你的 Samba 服务器，请从 system-config-samba 选项菜单中选择服务器设置（Server Settings）。这将打开一个有两个面板的窗口：基础（Basic）和安全（Security）（见图 14-13）。在基础面板上，你输入 Samba 服务器组名称。这将与你的 Windows 系统使用的名称相同。Windows 提供的默认名称为 HOME 或 WORKGROUP。请使用已经赋予 Windows 网络的名称。对于家庭网络，你可以自行决定。只需确保所有计算机都使用相同的网络名称即可。检查 Windows 控制面板的系统（System）选项卡以确保。

描述（Description）是你希望在 Windows 系统上显示的 Samba 服务器名称。在安全（Security）面板上，你可以指定身份验证模式、密码加密选项、来宾账户名称以及身份验证服务器。

![](img/660de85fae8d68d8e30eb0e48a1ee77d_452_0.png)

图 14-13：Samba 服务器设置

默认使用用户安全（User）。你也可以使用共享（share）或服务器（server）安全，这些更加开放，但两者都已弃用，可能会在后续版本中被删除。

- 身份验证模式指定访问级别，可以是用户（user）、共享（share）、服务器（server）、ADS 或域（domain）。用户级访问通过用户密码限制访问，而共享则对任何用户开放访问。
- 通常，你会选择加密密码，而不是以明文形式在网络上传输密码。
- 来宾用户（Guest user）是允许访问你想打开的共享或打印机的账户名称，无需提供密码。弹出菜单将列出所有当前用户，并选择“来宾账户（Guest Account）”。除非你为所有人提供访问，否则将没有来宾账户。

### 添加用户

对于用户身份验证，你必须将特定的 Windows 用户与 Samba 用户关联。Samba 维护自己的用户密码列表。要提供 Samba 访问，你需要注册用户为 Samba 用户。从偏好（Preferences）菜单选择 system-config-samba。这将打开列出所有当前用户的 Samba 用户（Users）窗口。点击右侧的添加用户（Add User）按钮。这将打开 Samba 用户窗口（见图 14-14）。在这里输入 Unix 用户名、Windows 用户名。有一个额外的框用于确认 Samba 密码。Unix 用户名（Username）是一个弹出窗口，列出托管 Samba 服务器的所有用户。

![](img/660de85fae8d68d8e30eb0e48a1ee77d_453_0.png)

图 14-14：添加用户

从菜单中选择 Linux 用户，然后输入用户名。Windows 用户名可以不同。Samba 维护访问 Linux 共享的用户密码。当 Windows 用户想要访问 Samba 共享时，需要密码。一旦创建了 Samba 用户，它将出现在 Samba 用户的列表中。要修改或删除 Samba 用户，使用 Samba 用户窗口，从列表中选择 Samba 用户，点击删除用户（Delete User）按钮。

![](img/660de85fae8d68d8e30eb0e48a1ee77d_454_0.png)

图 14-15：创建共享

### 在 Linux 上添加 Samba 共享

要设置简单的共享，点击添加共享（Add Share），这将打开窗口。在基础（Basic）面板上，你选择 Linux 目录，并指定它是否可写以及可见。你还要为 Samba 共享一个名称（见图 14-16）。在访问（Access）面板上，你可以限制某些用户或允许所有用户访问。系统上的所有 Samba 用户将列出。

![](img/660de85fae8d68d8e30eb0e48a1ee77d_455_0.png)

图 14-16：创建共享：访问

一旦创建，共享将出现在 system-config-samba 窗口中。共享名称、可见性、读写权限和描述将显示。要稍后修改共享，打开我的位置（My Places）并通过“添加网络位置（Add a network place）”来添加共享条目，或者查看 Windows 网络上的计算机。选择 Samba 服务器将显示 Samba 共享。

### 访问 Samba 共享

当 Windows 用户想要访问 Linux 系统上的共享时，“添加网络位置（Add a network place）”来添加共享条目，或者查看 Windows 网络上的计算机。选择 Samba 服务器将显示 Samba 共享。要访问共享，用户需要输入用户名和密码。在 Linux 系统上，使用服务（Services）工具重启 nmb 和 smb（System | Administration | Services）。确保 Windows 系统上的防火墙没有拦截 Samba。运行防火墙配置（System | Administration | Firewall）并选择信任（Trusted）面板。确保 Samba 服务已勾选，允许 Samba 在你的系统上运行。

> **注意**：fuse-smb 工具让你浏览整个网络。

## 配置局域网

对于大多数网络，使用专用路由器来设置域名解析服务（DNS）、防火墙和网络地址。你可以使用 Linux 提供这些功能，但通常在需要唯一自定义的网络时才需要。如果你的网络连接到子网，你可能需要配置代理服务。

![](img/660de85fae8d68d8e30eb0e48a1ee77d_458.png)

# 附录 A：获取 Fedora

Fedora Linux 发行版安装了专业级且稳定的 Linux，带有 KDE 和 GNOME 图形界面、灵活易用的系统配置工具、大量的互联网服务器、各种多媒体应用以及数种 Linux 应用程序。你可以在 fedaproject.org 找到关于红帽 Fedora 项目的最新信息。

大多数 Fedora 软件都可以从 Fedora 仓库下载。Fedora 发行策略还包括较小的桌面安装或较大的服务器安装。你可以使用 Live CD 安装 Fedora。Fedora 发行版依赖于带有精选软件的安装磁盘，以后可以从仓库中大量的软件进行更新和增强。这意味着初始安装中的软件集合可能较小。Fedora 仓库中的软件也在不断更新，因此任何安装都可能需要从仓库进行大量的更新。

## 下载镜像

要获取 Fedora 8，只需访问 Fedora 项目网站并点击 Get Fedora 链接。在这里你将看到针对不同 Fedora 安装 DVD 和 Fedora Live 版本的 torrent 或直接下载链接。直接下载链接指向当前可用的镜像站点。

```
http://fedoraproject.org/get-fedora
```

你可以通过输入以下 URL 直接访问 Fedora 镜像站点。然后你需要导航到 releases（版本）和 8 目录，找到存放 Fedora 安装和 Live iso 镜像的目录。

```
download.fedoraproject.org
```

你也可以通过以下 URL 访问特定的镜像站点。这里将列出 Fedora 镜像站及其地址。

```
mirrors.fedoraproject.org
```

在以下 URL 可以找到所有 Fedora 下载选项的详细说明，包括你需要的所有 ISO 光盘以及指向镜像站的链接。请访问此网站获取最新的下载程序。

```
http://fedoraproject.org/wiki/Distribution/Download
```
