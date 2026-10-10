
如果一切正常，你可以通过启用 `dhcpd` 服务，让 DHCP 服务器在每次计算机启动时自动启动，方法如下：

```
# chkconfig dhcpd on
```

有几种方法可以验证你的 DHCP 服务器是否正在工作：

- 检查 `/var/log/messages` 文件。如果 DHCP 服务启动出现问题，你会在此文件中看到指示问题的消息。

- 检查 `/var/lib/dhcpd/dhcpd.leases` 文件。如果客户端已成功从 DHCP 服务器分配了地址，该文件中应出现一条租约行。对于每个已租约 IP 地址的客户端，应有一组信息，外观如下：

```
lease 10.0.0.225 {
	starts 2 2006/05/04 03:48:12;
	ends 2 2006/05/04 15:48:12;
	hardware ethernet 00:50:ba:d8:03:9e;
	client-hostname "pine";
}
```

- 启动 Wireshark（在终端窗口中输入 `wireshark&`）并开始捕获数据（以混杂模式）。重新启动 DHCP 服务器并重启网络接口。

客户端。您应该能看到一系列 DHCP 数据包，显示如下序列：DHCP Discover、DHCP Offer、DHCP Request 和 DHCP ACK。

在客户端计算机上，您应该能够开始在网络上传输通信。如果客户端是 Linux 系统，请输入 `ifconfig -a` 命令。您的以太网接口（很可能是 `eth0`）应该会出现，且 IP 地址设置为 DHCP 服务器分配的地址。如果客户端是 Windows 系统，请打开命令提示符并输入 `ipconfig /all`。您将看到所有网络接口的配置信息。

当服务器正常运行时，您可以继续向网络添加 DHCP 客户端，以利用您分配的地址池。

## 配置 DHCP 客户端

大多数客户端计算机（Windows、Linux 或 Mac）默认配置为使用 DHCP 启动以连接到网络。然而，当情况并非如此时，您可能需要手动指定使用 DHCP。

配置网络客户端从您的 DHCP 服务器获取地址相当简单。然而，不同类型的操作系统使用 DHCP 的方式不同。以下是设置 Windows 和 Linux DHCP 客户端的示例。

### Windows (Vista)

1. 从 Windows Vista 中，选择 开始 → 控制面板 → 网络和 Internet → 网络和共享中心 → 管理网络连接。

2. 选择 本地连接。

3. 选择 属性。属性窗口将出现。

4. 选择 Internet 协议版本 4 并点击 属性。

5. 在 常规 选项卡上，确保已选中“自动获取 IP 地址”按钮。

### Windows (95, 98, 2000)

1. 从大多数较旧的 Windows 操作系统（Windows 95、98 和 2000）中，您通过 控制面板（开始 → 设置 → 控制面板）打开 网络 窗口。对于 Windows XP 系统，选择 开始 → 控制面板 → 网络连接 → 网络连接，然后选择您的 本地连接 并选择 属性。

2. 从 配置 选项卡（或在 Windows XP 中为 常规 选项卡），点击与您的以太网卡关联的 TCP/IP 接口（例如 TCP/IP → 3Com EtherLink III）。

3. 点击 属性。属性窗口将出现。

4. 点击 IP 地址 选项卡（或在 Windows XP 中为 常规 选项卡），然后选中“自动获取 IP 地址”复选框。

5. 点击 确定 并重启计算机，以便客户端可以使用新的 IP 地址。

### Fedora/RHEL

1. 在您最初安装 Linux 时，在 网络配置 屏幕上点击 使用 DHCP 进行配置。您的网络客户端在启动时应自动从您的 DHCP 服务器获取其 IP 地址。

2. 要在安装后设置 DHCP，请打开 网络配置 窗口（选择 系统 → 管理 → 网络 或运行 `neat` 命令）。

3. 在 网络配置 窗口中：

   - a. 点击 设备 选项卡（默认开启）。
   - b. 点击您的以太网设备（很可能是 `eth0`）。
   - c. 点击 编辑。
   - d. 点击 常规 选项卡。
   - e. 点击“自动获取 IP 地址设置”并选择 `dhcp`。
   - f. 点击 确定。
   - g. 点击 激活。

4. 然后，从终端窗口输入：

```bash
# service network restart
```

默认情况下，Fedora 或 RHEL 客户端不会接受从 DHCP 服务器传递给它的所有信息。Fedora 或 RHEL 客户端处理 DHCP 服务器输入的方式基于 `/etc/sysconfig/network-scripts/ifup` 脚本中的设置。如果客户端已开启 DHCP，当系统启动网络时，`ifup` 脚本将运行 `dhclient` 命令。您可以通过创建 `/etc/dhclient.conf` 文件来调整 `dhclient` 的行为。（输入 `man dhclient.conf` 以了解如何设置您的 `dhclient.conf` 文件。）

## 摘要

DHCP 提供了一种集中管理网络中计算机的机制，并可以提供帮助客户端计算机快速在网络上线的信息。DHCP 用于向网络中的 Windows、Linux、Mac 或其他客户端计算机提供关于您网络的信息。IP 地址可以动态分配，这意味着它们从一个 IP 地址池中分配。或者，可以基于特定的以太网硬件地址将特定地址分配给客户端。

# 第 24 章

## 设置 MySQL 数据库服务器

### 本章内容

- 查找 MySQL 软件包
- 配置 MySQL 服务器
- 操作 MySQL 数据库
- 显示 MySQL 数据库
- 修改表和记录
- 添加和删除用户访问权限
- 检查和修复数据库

MySQL 是一个流行的结构化查询语言 `SQL` 数据库服务器。与其他 SQL 服务器一样，MySQL 提供了访问和管理 SQL 数据库的手段。然而，MySQL 还提供了用于创建数据库结构的工具，以及用于向这些结构添加、修改和删除数据的工具。由于 MySQL 是一个关系数据库，数据可以存储在小而可管理的表中。这些表可以组合使用以创建灵活且复杂的数据结构。

一家名为 MySQL AB 的瑞典公司负责开发 MySQL (`www.mysql.com`)。MySQL AB 已以开源产品的形式发布 MySQL，通过提供多种 MySQL 支持包、商业许可证和 MySQL 品牌特许经营产品来获取收入。该公司还支持多种应用程序接口 `API`，以帮助应用程序开发人员和 Web 内容创建者访问 MySQL 内容。

由于 MySQL 是一个开源产品，它已被移植到几种不同的操作系统上（主要是 UNIX 和 Linux 系统，尽管也有 Windows 版本，甚至现在还有 Mac OS X 版本）。如您所猜测的那样，这些包括运行在 Fedora 和 RHEL 上的 MySQL 二进制版本。本章包含对 Fedora 和 RHEL 发行版中包含的 MySQL 版本的描述和操作步骤。

随此 Fedora 发行版一起提供的 MySQL 版本是 5.0.45。由于 Red Hat 认为许可问题阻碍其自由分发后续版本，因此在许多发行版中，Fedora 和 RHEL 都停留在 MySQL 3.23 版本。

## 查找 MySQL 软件包

您需要至少安装 `mysql` 和 `mysql-server` 软件包才能按照本章描述的操作设置 MySQL。以下是 Fedora 和 RHEL 发行版附带的用于入门的 MySQL 软件包：

- `mysql` — 此软件包包含许多 MySQL 客户端程序（位于 `/usr/bin`）、多个客户端共享库、默认的 MySQL 配置文件（`/etc/my.cnf`）、一些示例配置文件、支持不同语言的文件以及文档。

- `mysql-server` — 此软件包包含 MySQL 服务器守护进程（`mysqld`）和 `mysqld` 启动脚本（`/etc/init.d/mysqld`）。该软件包还创建设置 MySQL 数据库所需的各種管理文件和目录。

- `mysql-devel` — 此软件包包含开发 MySQL 应用程序所需的库和头文件。
