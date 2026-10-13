
## 选择服务菜单和修改选项

- 4. 选择“Service”（服务）菜单和“Modify”（修改）选项。图 11.22 显示了“Modify Service Options”（修改服务选项）窗口。

![](img/b8864f367e279929da7f8395589b04dd_260_1.png)

图 11.22 DHCP 修改服务选项窗口。

- 5. 勾选“Update DNS Host Information Upon Client Request”（客户端请求时更新 DNS 主机信息）复框。这将配置 DHCP 服务器向 DNS 服务器更新新分配的客户端信息。15 秒的默认超时值是可以接受的，但如果需要，也可以更改。

- 6. 确保也勾选“Restart Server”（重启服务器）框。

- 7. 点击 OK（确定）按钮应用更改。

- 8. 退出。

## 考试备习

### 问题 1

哪两个命令可以用于向 DHCP 服务器添加主机名？

A. `dhcpconfig`

B. `in.named`

C. `dhcmgr`

D. `dhcpagent`

E. `pntadm`

答案 A 和 C 是正确的，因为 `dhcpconfig` 是一个命令行工具，`dhcmgr` 是一个（图形）工具。答案 B 是错误的，因为 `in.named` 是一个进程。答案 D 是错误的，因为这是一个文件。答案 E 是错误的。

### 问题 2

使用哪个文件可以启用带主机名的 DHCP？

A. `/etc/default/dhcpagent`

B. `/etc/hostname.hme0`

C. `/etc/hostname`

D. `/etc/inet/cpsvc`

答案 B 是正确的，因为 `/etc/hostname.hme0` 用于标识系统主机名。答案 A 是错误的，因为 `/etc/default/dhcpagent` 是该文件。答案 C 是错误的，因为 `/etc/hostname` 会指定主机名，但不会使用 DHCP。答案 D 是错误的，因为这是一个配置文件。

### 问题 3

你将使用哪个命令来添加要管理的 IP 地址？

A. `pntadm`

B. `dhtadm`

C. `dhcpconfig`

D. `in.dhd`

答案 A 是正确的，因为 `pntadm` 用于管理。答案 B 是错误的，因为 `dhtadm` 是文件。答案 C 是错误的，因为 `dhcpconfig` 是命令行工具。答案 D 是错误的，因为 `in.dhd` 是进程。

### 问题 4

使用二进制文件管理 `192.168.45.0` 网络的 DHCP 服务器。文件名应该是？

A. `SUNWfiles_192.168.45.0`

B. `SUNWfiles1_192.168.45.0`

C. `192.168.45.0_SUNfiles1`

D. `dhcpab`

答案 B 是正确的，文件名由数据类型（`SUNWfiles1`）和 IP 地址组成。答案 A 是错误的，这表示 ASCII 文件。答案 C 是错误的，语法错误。答案 D 是错误的，因为 `dhcpab` 包含服务信息。

### 问题 5

你有一个使用 DHCP 获取 IP 地址的客户端。该客户端有一个 `hme0` 网络接口，并将指定一个特定的主机名——`ultra99`。为了实现这一目标，会在 `/etc/hostname.hme0` 文件中添加以下哪个项？

A. `ultra99`

B. `dhcp ultra99`

C. `hostname ultra99`

D. `inet ultra99`

答案 D 是正确的，因为 `/etc/hostname.hme0` 文件将添加 `inet ultra99` 项以请求使用主机名 `ultra99`。答案 A 是错误的，因为 `ultra99` 项会指定主机名但不会通过 DHCP 配置接口。答案 B 和 C 是错误的。

### 问题 6

`dhcpconfig` 命令的哪个选项用于初始化配置 DHCP 服务器？

A. `-D`

B. `-N`

C. `-U`

D. `-C`

答案 A 是正确的，因为 `-d` 用于在服务器上初始化配置 DHCP 服务。答案 B 是错误的，因为 `-N` 选项定义网络。答案 C 是错误的，因为 `-u` 用于取消配置服务器。答案 D 是错误的，因为 `-c` 用于转换现有的数据存储。

### 问题 7

当 DHCP 客户端启动时，它会发送一条消息来寻找 DHCP 服务器并请求 IP 地址。在以下消息类型中，哪一个是由 DHCP 服务器发送的、包含可租用 IP 地址详细信息的？

A. `DHCPPREREQUEST`

B. `DHCPPACK`

C. `DHCPOFFER`

D. `DHCPDISCOVER`

答案 C 是正确的，因为 `DHCPOFFER` 消息类型是由 DHCP 服务器返回的，用于提供供客户端租用的 IP 地址。答案 A 是错误的，因为 `DHCPREQUEST` 消息类型是由 DHCP 客户端在响应 `DHCPOFFER` 服务器时发送的。该请求接受了 DHCP 服务器做出的提议。答案 B 是错误的，因为 `DHCPPACK` 消息类型是由 DHCP 服务器在确认客户端对提议的接受时发送的。答案 D 是错误的，因为 `DHCPDISCOVER` 消息类型是由正在启动的 DHCP 客户端发送的，用于寻找 DHCP 服务器并请求 IP 地址。

## 想要了解更多？

Sun Microsystems，技术白皮书，“DHCP。”可在网站 www.sun.com/software/whitepapers/solaris9/dhcp.pdf 访问。

Sun Microsystems，Solaris 9 系统管理员合集—系统管理指南：IP 服务。提供纸质版、可在网站 http://docs.sun.com 获取，以及通过 Solaris 9 操作系统提供的在线文档获取。

Sun Microsystems，系统参考手册，第 1M 节—系统管理命令。提供纸质版、可在网站 http://docs.sun.com 获取，以及通过 Solaris 9 操作系统提供的在线文档获取。

# 高级动态主机配置协议 (DHCP)

你需要理解的术语：

- `add_install_client`

- 调试模式 (`Debug mode`)

- DHCP 服务器宏定义

- DHCP 服务器符号

- 主机名获取

- JumpStart 客户端

你需要掌握的概念：

- 解释如何配置 DHCP 服务器以支持 JumpStart 客户端。

- 给定的 DHCP 调试输出，推导出解析策略。

## 第 12 章

JumpStart 是 Solaris OE 提供的一项功能，允许在许多主机上自动安装操作系统环境。本书没有讨论 JumpStart 过程，因为它是 Solaris 9 系统管理员认证的一部分，而该认证是本书涵盖考试的先决条件。因此，假设读者已经熟悉了 JumpStart。本章描述了如何执行高级 DHCP 功能，例如配置 DHCP 服务器以支持 JumpStart 客户端，以及对 DHCP 服务器和客户端进行故障排除。

# JumpStart 和 DHCP

可以配置 DHCP 服务器，使 JumpStart 客户端启动时可以使用 DHCP 而不是使用 RARP 的传统 JumpStart 机制。使用 DHCP 方法是有优势的，因为 DHCP 数据包可以通过路由器，消除了要求客户端在同一子网上存在 JumpStart 服务器的需求——在标准 JumpStart 流程下，客户端要求在启动子网内有服务器，因为客户端使用的 RARP 协议无法通过路由器。

> 带有 DHCP 的 JumpStart 目前仅在 Intel 和 Ultra 工作站上支持。在 Ultra 工作站上，启动 PROM 版本必须至少为 3.25。如果不满足这些要求，客户端将无法执行 DHCP 启动。通常有一道考试题询问最低要求。

# 符号和宏

随 Solaris OE 提供的 `add_install_client` 脚本用于在 JumpStart 配置服务器上注册 JumpStart 客户端。该脚本的 `-d` 选项指定客户端为 DHCP 客户端。在运行脚本时，你的 JumpStart 服务器应该已经配置好，但在 DHCP 服务器支持 JumpStart 客户端之前，有许多需要配置的符号。以下示例使用主机 `ultra10` 作为 JumpStart 服务器，并为 `SUNW.Ultra5_10` 添加支持。

```
ultra10# ./add_install_client -d s ultra10:/export/install -c ultra10:\n/export/jumpstart -p ultra10:/export/install SUNW.Ultra5_10 sun4u
copying reboot to /tftboot
```

要在 DHCP 服务器中启用 `SUNW.Ultra5_10`，请向服务器添加包含以下数据的项：

- 安装服务器 (`SintNM`) : `ultra10`

安装服务器 IP (`SintIP4`) : `192.168.28.28`

安装服务器路径 (`SinstPTH`): `/export/install`

根服务器名称 (`SrootNM`): `ultra10`
