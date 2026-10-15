
# 章总结

DNS 将域名映射到 IP 地址，反之亦然。它作为一种分层的、分布式且复制的数据库实现。你可以通过在 `chroot` 环境运行以及使用事务签名（`TSIG`）来提高 `BIND` 的安全性。

当本地系统上的程序需要查找对应的 IP 地址时，它会调用解析器。解析器查询本地 DNS 缓存（可用），查询局域网或互联网上的 DNS 服务器。查询有两种类型：迭代和递归。当服务器响应迭代查询时，它返回所拥有的信息；不查询其他服务器。递归查询会导致服务器在必要时查询其他服务器以给出答案。

有三种服务器：
- 主服务器，持有区域的主副本，对区域具有权威性。
- 从服务器也具有权威性并从主服务器或其他服务器复制数据。
- DNS 缓存不是权威的，要么从缓存回答，要么转发到其他服务器。

DNS 数据库持有资源记录。存在许多类型的记录，包括 `A`（地址）、`MX`（邮件交换）、`NS`（名称服务器）、`PTR`（用于反向名称解析）和 `SOA`（描述区域的起始）。

## 练习题

1. 哪种服务器响应递归查询？该服务器是如何工作的？
2. 当 浏览器尝试解析 URI 的域名部分时，可能会返回什么类型的 DNS 记录？
3. `MX` 资源记录用于什么？
4. 如何从命令行查找 `example.com` 的 IP 地址？
5. 如何指示 Linux 系统使用局域网 DNS 缓存（地址为 `192.168.1.254`）或 ISP 缓存（地址为 `1.2.3.4`），如果局域网服务器不可用？
6. 如何指示 DNS 服务器仅响应来自 `137.44.*` IP 范围的查询？
7. 解析器如何尝试查找 域名的 IP 地址？

## 进阶练习

- 8. 你将如何设置一个不包含任何官方 InterNIC 分配域名的私有域名层次结构？
- 9. DNS 的哪部分最容易受到恶意用户的攻击？为什么？
- 10. 当更改 DNS 条目时，通常需要等待 DNS 记录在全球范围内更新，这很令人烦恼。你可以通过将 TTL 设置为较小来防止这种延迟。为什么将 TTL 设置为较小是一个坏主意？
- 11. 概述一种利用 DNS 支持加密的方法。

# 第 25 章 firestarter、gufw 和 iptables：设置防火墙

## 本章内容介绍

- `firestarter` 简介....... 864
- `firestarter`：设置和维护防火墙....... 866
- `ufw`：简单的防火墙（Uncomplicated Firewall）....... 874
- `gufw`：`ufw` 的图形化界面
- 规则、匹配项、目标和链....... 880
- `iptables` 命令的解析....... 884
- 使用 `iptables` 构建规则集....... 885
- 使用 NAT 共享互联网连接....... 883

`gufw` 和 `firestarter` 工具是 `iptables` 的用户友好型图形化前端；`iptables` 在 Linux 内核中构建并操作网络包过滤（第 1164 页）规则。你可以使用 `firestarter` 或直接使用 `iptables` 创建一个保护系统免受恶意用户的防火墙，并设置 `NAT`（网络地址转换，第 1161 页）（基于第 1164 页）以允许多个系统共享单个互联网连接。事实上，`firestarter` 还可以控制 DHCP 服务器。

`iptables` 工具灵活且具有可扩展性，允许你建立简单和复杂的网络过滤解决方案。它提供了连接跟踪（状态数据包过滤），允许你根据连接状态处理数据包。例如，你可以设置规则来拒绝尝试建立新连接的入站数据包，并接受对本地发起连接响应的入站数据包。许多未包含在基础 `iptables` 包中的功能可以通过 `patch-o-matic` 程序以补丁的形式提供。

## 第 25 章 firestarter、gufw 和 iptables：设置防火墙

由于 `firestarter` 具有用户友好的特性，它通常足以保护单个系统或小型局域网（LAN），但它没有提供访问 `iptables` 全部复杂性和强大的功能。对于熟悉基础网络的人来说，涉及 `firestarter` 的大多数概念都是熟悉的或易于学习的。完全理解 `iptables` 所需的某些概念超出了本书的范围。虽然你可以在不同级别使用 `iptables`，但本章仅介绍基础知识。本章的某些章节深入了可能需要额外理解或解释的领域。如果某个概念不清楚，请参阅第 883 页“更多信息”中的资源。

`ufw` 和 `gufw`：Ubuntu 在其安全区域添加了 `ufw`（简单防火墙）及其图形化界面 `gufw`。随着这些产品的趋成熟，你可能想要考虑尝试并使用它们来替代 `firestarter`。更多信息请参阅第 874 页（`ufw`）和第 876 页（`gufw`）。

### 路由器具有防火墙

许多系统已经受到位于路由器中的防火墙的保护。如果你使用带有防火墙的路由器，那么除了在 Ubuntu 系统上由你设置的任何防火墙上开启端口外，你可能还需要在路由器防火墙上开启端口。

### firestarter 简介

`firestarter` 工具是一个用于构建和维护防火墙的复杂图形化工具。尽管它与 GTK 配合并设计为在 GNOME 下运行，但在 KDE 下也同样适用。该工具允许你与局域网上的其他系统共享互联网连接。你还可以设置和控制 DHCP（第 470 页）服务器。它提供了入侵和其他事件的实时视图，并允许你调整 `ICMP`（第 1153 页）参数以帮助阻止 Dos 攻击（第 1146 页）。在安装后，`firestarter` 允许出站连接，并显示源自系统或其所保护的局域网外部的入站连接（即源自互联网的连接）。当你查看这些事件时，可以设置规则允许它们通过，从而方便 `firestarter` 的自定义。

`firestarter` 工具可以保护它运行的系统（防火墙主机），也可以保护它运行的系统，作为其所在的局域网上的所有其他客户端（这些客户端通过防火墙主机连接到互联网）。图 25-1 显示了一个典型的设置，所有进出局域网的网络流量都必须通过防火墙，使防火墙能够控制互联网与局域网之间的访问（包括防火墙主机）。在这种设置下，防火墙主机充当路由器（第 377 页）。

#### 笔记

**术语** 本节解释了用于解释 `firestarter` 的词在语境中的含义。`firewall` 和 `firestarter` 词被通用使用。

- （防火墙）主机（系统）——运行其上的系统。

#### firestarter 简介

![](img/c8ae2cd4d550a81142a3ed64b0f61f6a_915_0.png)

图 25-1 典型的设置

- 客户端系统——与防火墙主机处于同一局域网，且与其外部系统（特别是互联网）的流量通过防火墙。
- **策略**——防火墙适用的规则集。
- **规则**——指定防火墙操作的语句。
- **连接**——在 TCP 下，系统交换数据的路径。客户端通过 SYN（同步）包开启连接，服务器返回 ACK（确认）包，客户端通过 FIN 关闭连接。虽然 UDP 工作方式不同，没有连接的概念，但对于本文讨论来说是合适的。
- **入站连接**——源自互联网并以防火墙主机为目标的连接。
- **出站连接**——源自防火墙主机并以互联网为目标的连接。

**默认策略** 默认情况下，`firestarter` 实现了一种保护主机和客户端系统的用户友好策略。通常情况下，它允许出站流量，并阻止对出站流量响应的入站流量。具体而言，默认 `firestarter`

- 阻止来自互联网指向防火墙的新连接。
- 允许对防火墙主机或客户端发起的连接进行响应的入站包。
- 允许防火墙主机建立连接。

### 设置和维护防火墙

在使用防火墙向导使用 `firestarter` 后，你可以根据需要修改默认策略。虽然 `firestarter` 是 `iptables` 的前端，但它并不像 `iptables` 那样存储规则（使用 `iptables-save` [第 891 页]）。相反，它以自己的格式将配置存在 `/etc/firestarter` 目录中。

#### 更多信息

Web `www.fs-security.com`

#### 设置维护防火墙

本节介绍了如何使用 `firestarter` 防墙向导设置防火墙，以及在设置后如何维护防火墙。

##### 前提条件

安装以下包：

- `firestarter`
- `dhcp3-server`（仅在你希望 `firestarter` 运行在 DHCP 时需要；第 472 页）

安装 `firestarter` 包后，必须运行防火墙向导 `firestarter` 才能启动（见下文的启动部分）。配置完成后，`firestarter` 会每次启动系统时运行。虽然有一个 `firestarter` 初始化文件，但你不需要手动运行它；使用 `firestarter` GUI 开启或关闭防火墙不允许网络流量进入或离开。当你启动系统时，`firestarter` 将处于你关闭系统时的状态。无论是否显示 GUI，`firestarter` 都会运行。

![](img/c8ae2cd4d550a81142a3ed64b0f61f6a_916_0.png)

图 25-2 防火墙向导：Firestarter 欢迎界面

#### 快速上手：使用 firestarter 防墙向导配置防火墙

防火墙向导和 Firestarter 窗口（第 86 页图 25-2 和 25-6）允许你设置和控制 `firestarter`。要显示此窗口，请选择主菜单：`System⇒Administration⇒firestarter`，或者从终端模拟器或运行应用程序窗口（`Alt+F2`）输入命令 `gksudo`。

当你第一次运行 `firestarter` 时，它会打开防火墙向导（图 25-2），帮助你配置 `firestarter`。你可以随时通过选择 Firestarter 菜单：`Firewall⇒Run Wizard` 重新运行此向导。向导的最后一步允许你启动防火墙并显示 Firestarter。

第一个屏幕欢迎你使用 `firestarter`；点击向前开始。防火墙向导显示网络设备设置（图 25-3）。在此屏幕中选择连接到 Internet 的设备。你还可以指定在拨号拨出系统时启动防火墙（如果你正在使用调制解器连接到 Internet），和/或指定 `firestarter` 使用 DHCP（第 470 页）为客户端系统分配 IP 地址并提供其他网络配置信息。

从标记为 Detected device(s) 的下拉列表中，选择连接到 Internet 的设备。如果本地系统作为路由器运行，请确保选择连接到 Internet 的设备，而不是连接到局域网（LAN）的设备。如果本地系统仅使用调制解器连接 Internet，请勾选 Start the firewall on dial-out 复选框。

如果你想运行 DHCP，请勾选 IP address is assigned via DHCP 的复选框。（你也可以通过 Firestarter 菜单：`Edit⇒Preferences` 配置 DHCP。）如果 `firestarter` 将控制 DHCP，你必须安装 DHCP 软件包（第 866 页）。点击向前。

## 图 25-4 Internet 连接共享设置屏幕

`NAT`（连接）Internet 连接共享设置屏幕（图 25-4）允许你设置共享 `NAT`（第 1161 页），以便局域网上的系统可以共享单个 Internet 连接。只有当你在至少具有两个网络连接的机器上安装防火墙时，此窗口才会出现。如果防火墙主机作为路由器运行（图 25-1，第 865 页）并共享 Internet 连接，请勾选 Enable Internet connection sharing 复选框；否则跳过此屏幕。当你勾选此复选框时，`firestarter` 允许你选择连接到局域网的设备（未连接到 Internet 的设备）。勾选 Enable DHCP for local network 复选框会导致 `firestarter` 运行 DHCP。当你勾选此复选框时，点击 DHCP server details 附近的加号，以选择保留现有的 DHCP 配置还是创建一个新的。Server name 可以 DHCP 服务器的 IP 地址或名称。如果你将名称设置为 `<dynamic>`，`firestarter` 将在运行时确定 DHCP 服务器的 IP 地址，这对于服务器使用 DHCP 分配 IP 地址的情况可能非常有用。点击向前。

启动防火墙。在 Ready to start your firewall（图 25-5）中，你可以选择启动防火墙。防火墙以安全模式启动，这可以保护 LAN，但可能可能会给某些用户带来问题，并且不允许 Internet 上的系统访问防火墙后的服务器。如果你从远程系统配置防火墙，一旦启动防火墙，你将无法操作 `firestarter`。如果你想立即启动防火墙，请勾选 Start firewall now 复选框。点击保存。

#### 使用 firestarter 维护防火墙

配置 `firestarter` 后，你可以通过 Firestarter 窗口更改策略。运行防火墙向导后，`firestarter` 会显示此窗口。你可以按照第 867 页中快速上手部分的说明随时显示此窗口。无论 Firestarter 窗口是否显示，防火墙都会运行。当你启动系统时，防火墙将恢复你关机时的状态（运行、停止或锁定）。

##### 标签卡

Firestarter 窗口的 Status 标签卡（图 25-6）显示防火墙的概述。此标签卡可以显示到防火墙的活动连接。工具栏允许你更改 `firestarter` 的状态并指定偏好。Firestarter 窗口中的大型圆形图标指示防火墙的状态：

- **Disabled**—防火墙已关闭——即未安装 `firestarter`。
- **Active**—防火墙已运行并执行你设置的策略（或默认策略）。
- **Locked**—防火墙正在运行并拦截所有数据包。没有数据可以通过 `firestarter` 控制的网络接口进入或离开防火墙。

点击工具栏上的相应图标更改防火墙状态。

当防火墙根据规则拦截数据包时，会发生事件。Firewall 列表中的列显示防火墙拦截的入站和出站事件数量，并指示其中有多少是严重性质。如果事件可能是恶意用户尝试访问系统的尝试，则被视为严重事件。

Network 帧显示每个系统连接的活动。当你点击 Active connections 左侧的加号时，`firestarter` 会显示一个可滚的活动连接列表。点击列表中的一个进行选择，然后选择 Hostnames 以更改 Source 和 Destination 列中的值。Port 列显示连接使用的目标主机上的端口。Service 列指示与端口关联的服务。Program 列显示如果是本地运行的程序名称。

##### 事件 标签卡

Firestarter 窗口 Events 标签卡（图 25-7）是修改默认防火墙策略的关键。它显示被拦截的连接列表。列表中的每行指定一个防火墙根据规则拦截的事件。黑色显示的事件是尝试连接到随机端口，通常不需要担心。灰色的事件是无害的，主要由广播流量组成。红色事件是尝试访问未提供的服务，可能表明恶意用户正尝试访问主机或客户端系统。你可以通过以下方式进行修改：

- 要显示主机名而不是 IP 地址，突出显示要更改的项，右键点击并选择 Hostnames（图 25-7）。
- 默认情况下，Blocked Connections 列表不包含冗余项。取消勾选 Firestarter 菜单：`Edit-Preferences-Events-Skip redundant entries` 中的复选框。
- 你可以通过 Firestarter：`Events-Show Column` 菜单（图 25-8）指定 `firestarter` 在 Blocked Connections 列表中包含的列。

如图所示，右键菜单还允许你更改突出显示的系统和端口（服务）的规则。入站和出站连接显示不同的菜单。入站菜单包含以下选择：

- **Allow Connections from Source**—允许被拦截的 Internet 源系统向客户端系统或防火墙主机建立任何类型的连接。仅在你信任源系统时才设置此规则。
- **Allow Inbound Service for Everyone**—允许 Internet 上的任何系统连接到被拦截的服务（端口）。设置此规则以允许访问防火墙之前的服务器。
- **Allow Inbound Service for Source**—允许被拦截的 Internet 源系统连接到被拦截的服务（端口）。受此规则保护的端口被称为隐身端口，因为它对指定系统外的 Internet 上的所有系统都是不可见的。

##### 第 25 章 firestarter, gufw 和 iptables：设置防火墙

**策略标签页 (POLICY TAB)**

出站菜单包含以下选项：

- **允许连接到目标 (Allow Connections to Destination)**——允许防火墙主机和客户端系统与被高亮事件拦截的目标系统建立连接。
- **所有人允许出站服务 (Allow Outbound Service for Everyone)**——允许防火墙主机和客户端系统连接到被高亮事件拦截的服务（端口）。
- **源允许出站服务 (Allow Outbound Service for Source)**——允许防火墙主机或被拦截的特定客户端连接到被高亮事件拦截的服务。

此外，两个菜单都包含两个选项：

- **禁用源事件 (Disable Events from Source)**——阻止互联网上的高亮源系统连接到客户端或防火墙主机。
- **禁用端口事件 (Disable Events on Port)**——阻止互联网上的任何系统连接到被高亮事件拦截的服务（端口）。

### 事件标签页 (Events tab)：易用性

> 提示 从事件标签页设置规则并在策略标签页中查看非常方便。但是，你无法从事件标签页设置某些规则（例如转发规则）。此外，你无法从事件标签页编辑规则。

策略标签页（图 25-9）显示防火墙规则，并允许你添加、删除和编辑规则。标记为编辑（Editing）的下拉列表允许你选择 `firestarter` 显示（你可以选择）入站或出站规则。

策略标签页显示了入站和出站规则组的三个框架。在框架中使用鼠标指针右键点击可显示包含以下选项的上下文菜单：添加规则 (`Add Rule`)、删除规则 (`Remove Rule`) 和编辑规则 (`Edit Rule`)。要使用后两个选项，必须在右键点击之前高亮一条规则。

#### firestarter：设置和维护防火墙

**应用更改** 默认情况下，在您点击窗口顶部的“应用策略 (`Apply Policy`)”之前，`firestarter` 不会应用你在此标签页中所做的更改。你可以通过选择 Firestarter 菜单：编辑：首选项：策略并勾选“立即应用策略更改 (`Apply policy changes immediately`)”复选框，让 `firestarter` 立即应用更改。

### 入站策略 (INBOUND POLICY)

默认的入站策略是阻止所有入站连接，但响应出站连接的连接除外。当你选择入站流量策略（Inbound traffic policy）时，`firestarter` 会显示三个框架，允许你处理作为默认策略异常的规则：

- **允许来自主机的连接 (Allow connections from host)**——指定 `firestarter` 接受任何传入连接的主机或网络。请确保你完全信任此系统或网络。
- **允许服务 (Allow service)**——指定 `firestarter` 接受入站连接的服务（端口）。你可以指定 `firestarter` 接受来自任何人、所有客户端或互联网上特定主机或网络在指定端口上入的入站连接。
- **转发服务 (Forward service)**——指定 `firestarter` 接受入站连接的服务（端口）。`firestarter` 防火墙会将这些连接转发到你指定的客户端，并使用指定的端口。如果你在客户端系统上运行服务器，并希望互联网上的系统能够连接到服务器，则转发服务是合适的。

### 出站策略 (OUTBOUND POLICY)

当你选择出站流量策略（Outbound traffic policy）时，`firestarter` 会显示两个单选按钮，允许你设置默认出站策略：

- **默认许可，黑名单流量 (Permissive by default, blacklist traffic)**——默认出站策略。允许所有源自防火墙主机或客户端的出站连接。你必须设置特定的策略（黑名单）来阻止特定服务的出站请求和/或来自特定系统的请求。
- **默认限制，白名单流量 (Restrictive by default, whitelist traffic)**——阻止所有出站流量，除非你设置了规则允许的连接（白名单）。

**默认许可 (Permissive by default)** 使用“默认许可”的默认策略时，`firestarter` 会显示三个框架，允许你拒绝连接和/或服务：

- **拒绝到主机的连接 (Deny connections to host)**——指定防火墙主机和所有客户端系统不允许连接的互联网系统。
- **拒绝到局域网主机的连接 (Deny connections to LAN host)**——不允许客户端系统连接到互联网上的任何系统。
- **拒绝服务 (Deny service)**——指定 `firestarter` 阻止出站连接的服务和/或端口。你可以指定 `firestarter` 阻止来自任何人、客户端、防火墙主机或互联网上特定主机或网络在指定端口上的出站连接。

**默认限制 (Restrictive by default)** 使用“默认限制”策略时，`firestarter` 会显示三个框架，允许你允许连接和服务：

- **允许到主机的连接 (Allow connections to host)**——指定防火墙主机和所有客户端允许连接的互联网系统。
- **允许来自局域网主机的连接 (Allow connections from LAN host)**——允许客户端系统连接到互联网上的任何系统。
- **允许服务 (Allow service)**——指定 `firestarter` 允许你进行出站连接的服务和/或端口。你可以指定来自任何人、客户端、防火墙主机或互联网上特定主机或网络的指定端口。

## ufw：简单的防火墙

`ufw` (uncomplicated firewall) 工具是 `iptables` 的一个简单、易于使用的命令行界面。它是作为基础系统的一部分安装的。`gufw`（`ufw.tuxymarket.org`；第 876 页）是 `ufw` 的图形化界面，包含在 `gufw` 包中。

安装后，`ufw` 是关闭的。`status` 命令报告 `ufw` 处于活动状态（inactive）：

```
