
# 定义区域设置的语句

图 12-24：`named.conf` 中的各种声明。

# DNS 资源记录

DNS 资源记录定义了区域的参数。它包含五个部分：完全限定域名、TTL、记录类、记录类型和记录数据。资源记录的格式由请求注释（`RFC`）定义。资源记录中的记录数据取决于记录类型。

各种 DNS 记录及其使用的格式如表所示。

# CompTIA Linux+ 由 LPI 驱动

| DNS 记录 | 说明 |
| --- | --- |
| SOA | 权威起始起点 (SOA) 记录用于在字段字符串中指定有关区域的信息。SOA 记录告诉服务器对该区域具有权威性。每个区域仅包含一个 SOA 记录。SOA 记录的格式为：<br>`@ IN SOA primary nameserver`<br>`{hostmaster email}`<br>`(serial number)`<br>`(time to refresh)`<br>`(time to retry)`<br>`(time to expire)`<br>`(minimum TTL)` |
| NS | 名称服务器 (NS) 记录用于定义特定区域的权威名称服务器。NS 记录的格式为 `IN NS {nameserver}`。名称服务器可以是 FDN。它可以是主服务器或从用服务器 |
| A | 地址记录（A 记录）用于为名称分配 IP 地址。A 记录的格式为 `{hostname} {IP address}`。IP 地址不应以句号 (`.`) 结尾。如果省略了主机名，A 记录将指向命名空间顶部的默认 IP 地址 |
| PTR | 指针 (PTR) 记录用于反向域名解析映射。它用于反向域名区域文件，将 IP 地址映射到名称。PTR 记录的格式为 `(last IP digit) IN PTR {FQDN of system}`。`(last IP digit)` 指定 IP 地址中的最后一个数字，它应该指向特定服务器的域名。PTR 记录应以句号结束。例如，`253 IN PTR svrA.example.com` |
| MX | 邮件交换器 (MX) 记录用于指定区域内对邮件服务器的偏好设置。MX 记录的格式为 `IN MX {priority value} {mail server name}`。最高优先级值为 0，分配给接收邮件的主机。两个主机具有相同的优先级，以便在它们之间平均分配。对于一个域，可以定义任意数量的 MX 记录 |
| CNAME | 规范名称 (CNAME) 记录用于将别名映射到真实名称。CNAME 记录也称为别名记录。CNAME 记录的格式为 `{alias name} IN CNAME {real name}`。CNAME 记录通常用于指向另一个域名 |
| TXT | 文本记录 (TXT 记录) 用于将文本与主机名映射。它用于验证来自域的真实邮件源 |

第 12 课：配置网络服务 507

# 如何配置客户端网络服务

## 过程参考：配置 DHCP 客户端

配置 DHCP 客户端并从 DHCP 服务器获取 IP 地址：

1. 在 CLI 中以 `root` 身份登录。
2. 打开设备文件，输入 `vi /etc/sysconfig/network-scripts/ifcfg-eth0` 设备名称。
3. 验证 `BOOTPROTO=dhcp`。
4. 保存并退出。
5. 要应用设置，输入 `service network restart`。
6. 要验证系统是否已接收 IP 地址，输入 `ifconfig`。

`dhclient` 是一个实用，允许你使用 DHCP 协议配置一个或多个网络服务。如果协议失败，`dhclient` 将分配静态地址。

## 过程参考：配置 DNS 服务

在你的系统上配置 DNS 服务：

1. 以 `root` 身份登录。
2. 使用 `named.cachingnameserver.conf` 文件作为模板，输入 `cp /etc/named.caching-nameserver.conf /etc/named.conf`。
3. 配置 DNS。
   a. 指定全局配置选项。
   b. 为根、回环域以及正向和反向区域添加区域语句。
   c. 创建正向和反向区域文件。
4. 要检查 `named` 语法，输入 `named-checkconf -f /etc/named.conf`。
5. 启动 `named` 服务。
   a. 要启动 `named` 守护进程，输入 `service named start`。
   b. 如果服务已经在运行，要重新加载 `named` 守护进程，输入 `service named reload`。
   c. 要重新加载区域文件，输入 `rndc reload`。
   d. 要在系统启动时启动 `named` 服务，输入 `chkconfig named on`。

# 活动 12-3
配置 DHCP 客户端服务

开始之前：

1. `srvA` 已重启，并显示 GUI 登录界面。
2. 切换到 CLI 的第一个终端。
3. 以 `root` 身份登录。
4. 要安装 DHCP 软件包，在命令行中输入 `yum localinstall /resource/Server/dhcp*`。
5. 要继续安装，输入 `y`。
6. 清除终端屏幕。

开始之前：

1. 切换到标记为 `srvB` 的系统。
2. 你已以 `root` 身份登录 GUI，并显示终端窗口。

场景：

你的 IT 经理为你们组织的新分机构 OGC Systems 规划了网络布局。网络将包括两个 Linux 服务器（`srvA` 和 `srvB`）和 150 台工作站。DHCP 服务安装在 `srvA` 上，手动配置了 IP 地址 `192.168.0.1`。你需要配置 DHCP，以便 `srvB` 和工作站从 `srvA` 动态接收 IP 地址。根据网络策略文档，你发现要分配的 IP 地址范围可以从 `192.168.0.25` 到 `192.168.0.200`。

1. 修改网络设备设置从 DHCP 获取地址。
   a. 要打开网络设备设置，输入 `ifconfig`。
   b. 要编辑设备设置，输入 `vi /etc/sysconfig/network-scripts/ifcfg-eth0`。
   c. 将 `BOOTPROTO` 修改为 `dhcp`。
   d. 保存并退出。
   e. 要应用设置，输入 `service network restart`。
   f. 要验证系统已接收 IP 地址，输入 `ifconfig`。

2. 检查系统是否接收了 IP 地址。
   a. 要检查 `named`，输入 `ifconfig`。
   b. 观察 `192.168.0.25` 已分配。
   c. 要检查 DHCP，输入 `ifconfig`。
   d. 清除终端屏幕。

# 活动 12-4
配置 DNS 服务

开始之前：

1. 你已以 `root` 身份登录 GUI，并显示终端窗口。

场景：

你的 IT 经理为你们组织的新分机构 OGC Systems 规划了网络布局。网络将包括两个 Linux 服务器（`srvA` 和 `srvB`）和 150 台工作站。DHCP 服务安装在 `srvA` 上，手动配置了 IP 地址 `192.168.0.1`。你需要配置 DHCP，以便 `srvB` 和工作站从 `srvA` 动态接收 IP 地址。根据网络策略文档，你发现要分配的 IP 地址范围可以从 `192.168.0.25` 到 `192.168.0.200`。

1. 配置 DNS。
   a. 使用 `named.cachingnameserver.conf` 文件作为模板，输入 `cp /etc/named.caching-nameserver.conf /etc/named.conf`。
   b. 配置 DNS。
      i. 指定全局配置选项。
      ii. 为根、回环域以及正向和反向区域添加区域语句。
      iii. 创建正向和反向区域文件。
   c. 保存并退出。
   d. 要检查 `named` 语法，输入 `named-checkconf -f /etc/named.conf`。
2. 启动 `named` 服务。
   a. 要启动 `named` 守护进程，输入 `service named start`。
   b. 如果服务已经在运行，要重新加载 `named` 守护进程，输入 `service named reload`。
   c. 要重新加载区域文件，输入 `rndc reload`。
   d. 要在系统启动时启动 `named` 服务，输入 `chkconfig named on`。
3. 验证 DNS 服务。
   a. 要解析主机名，输入 `host google.com`。
   b. 观察 IP 地址返回。
   c. 要解析 IP 地址，输入 `host 8.8.8.8`。
   d. 观察主机名返回。

### 主题 D

# 管理远程系统

之前，你配置了网络服务允许系统访问网络资源。在向网络添加新系统的情况下，你将直接与系统通信并修改系统上的数据。作为系统管理员，你将处理来自不同位置的用户的需求。某些会议或活动需要你远程连接服务器。你可以从一个位置访问数据并排除故障。在本主题中，你将探索 SSH 和 VNC 并检查它们与系统通信的功能。

# PKC

定义：

公钥加密 (PKC) 是一种使用公钥和私钥对的加密方法。使用公钥加密数据并通过网络传输。当数据到达目的地时，使用私钥解密。

示例：

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_523_0.png)

**图 12-26:** 使用两个密钥的加密数据。

示例：

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_524_0.png)

图 12-27：SSH 在网络上控制安全通信。

## OpenSSH

OpenSSH 是 SSH 协议的免费版本，包含在大多数 Linux 发行版中。数据通过在两个系统之间建立的安全隧道进行传输。`Telnet` 传输的数据（包括密码）可以被网络上的任何系统轻易截获。OpenSSH 为通过 `Telnet` 及类似应用程序传输的数据提供了强力的客户端-服务器验证方法。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_524_1.png)

图 12-28：使用 OpenSSH 隧道进行数据传输。

## ssh-keygen 命令

`ssh-keygen` 命令用于生成、管理和转换身份密钥。下表列出了 `ssh-keygen` 命令的一些选项。

| 使用此 ssh-keygen 选项 | 如果您需要 |
|--- |--- |
| `-b {bits}` | 指定密钥中创建的位数。 |
| `-c` | 修改公钥和私钥文件中的注释。 |
| `-t {file name}` | 指定密钥文件的文件。 |
| `-l` | 显示指定的公钥文件的指纹。 |
| `-p` | 修改私钥文件的密码短语，而不是创建新的私钥。 |

## 公钥与私钥

私钥和公钥都参与验证过程。每个密钥都是字母、数字和特殊字符的集合，用于唯一标识每个系统。私钥参与公钥验证，并保留在本地系统中。公钥参与公钥验证，并被告知远程系统。私钥保留在本地系统中，公钥被告知远程系统。私钥绝不会传输到目标服务器。只有当远程的私钥与原始的公钥结合时，才会产生有效结果。在登录远程系统时，远程服务器会将私钥和公钥结合进行验证。如果用户需要登录系统并传输文件，则密钥必须匹配。真实性由远程服务器建立，由其授予必要的权限。

## 密钥文件

您使用 SSH 创建的密钥对存储在不同的文件中，取决于您使用的算法。

| 创建的文件 | 算法 |
| --- | --- |
| `id_dsa` and `id_dsa.pub` | DSA |
| `id_rsa` and `id_rsa.pub` | 使用 SSH 协议版本2 的 RSA |
| `identity` and `identity.pub` | 使用 SSH 协议版本1 的 RSA |

## Debian 上的 OpenSSH

在 Debian 上安装 `openssh` 时，会在 `/etc/ssh` 目录下创建两对（DSA 和 RSA 验证）公钥和私钥。创建的两个对是：`/etc/ssh/host_rsa_key` 和 `/etc/ssh/host_rsa_key.pub` 以及 `/etc/ssh/host_dsa_key` 和 `/etc/ssh/host_dsa_key.pub`（原文重复）。

## /etc/ssh/sshd_config 文件

`/etc/ssh/sshd_config` 文件是 SSH 服务器配置文件。该配置文件中的大多数行都被注释了，表示已启用的默认设置。您可以删除注释并更改默认设置。下表列出了一些 SSH 服务器配置选项。

| 使用此 sshd 选项 | 如果您需要 |
|--- |--- |
| `XForwarding yes` | 在一个系统上运行或停止程序，并在另一个系统上显示 X 窗口输出。 |
| `XForwarding no` | 在一个系统上停止运行程序，并在另一个系统上显示 X 窗口输出。 |
| `PermitRootLogin` | 允许 `root` 用户通过 SSH 登录。 |
| `MaxStartups {number}` | 指定到主机可以建立的最大连接数。 |
| `LoginGraceTime {time in seconds}` | 如果在登录宽时间内未建立连接，则丢弃连接。 |
| `AuthorizedKeysFile {file name}` | 指定包含身份密钥的文件位置。 |
| `PermitEmptyPasswords yes/no` | 指定是否允许或拒绝空密码。 |

## ssh-agent 程序

定义：
`ssh-agent` 程序是一个用于持有公钥验证私钥的程序。该程序随 X 会话或登录会话启动，并作为父进程，而所有其他程序或窗口都是它的客户端。`ssh-agent` 不通过通道发送私钥；相反，需要私钥的任务由代理执行，并将结果返回给客户端。初始状态，代理没有私钥。使用 `ssh-add` 工具添加密钥。

示例：

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_526_0.png)

图 12-29：`ssh-agent` 的角色。

## 服务器密钥

当安装 SSH 服务器时，会自动创建用于验证的公共主机密钥和服务器密钥。服务器密钥不存储在设备的任何地方；它们每小时自动重新生成以确保安全。

## known_hosts 文件

当连接到远程主机时，主机会向您发送用于验证的公钥和服务器密钥。您的系统查找 `~/.ssh/known_hosts` 文件查找主机密钥条目，如果找到条目，将允许访问该主机。否则，将显示消息，说明远程主机的真实性尚未建立。您可以输入“yes”来信任远程主机并连接。每当与远程终端建立 SSH 连接，该系统或主机的公钥就会添加到 `~/.ssh/known_hosts` 文件中。

## ~/.ssh/authorized_keys 文件

SSH 客户端的公钥和私钥必须添加到远程服务器上的 `~/.ssh/authorized_keys` 文件中。

## SSH 协议版本

默认情况下，OpenSSH 同时兼容 SSH 协议版本1 和2。虽然使用 SSH 2 提供了增强的安全优势，但您可以根据客户端使用 SSH 1。

## 多路 SSH 连接

如果在连接 SSH 服务器期间网络或防火墙设置发生变化，可能会丢失连接。为了防止连接丢失，SSH 允许并发连接。可以使用 `MaxStartups` 选项指定到主机的最大连接数。然而，在登录超时过期之前，额外的连接将被丢弃。使用 `LoginGraceTime` 选项指定。

## SCP 命令

SCP 代表安全复制。`scp` 命令允许您在加密网络上传输文件的副本。它使用 SSH 提供安全性，使用密码和密码短语。使用 `scp` 命令可以从远程系统复制到本地主机，反之亦然。此外，您可以在两个远程系统之间传输文件。

## .hosts 和 .shorts

使用 `.hosts` 或 `.shorts`，SSH 允许用户仅通过用户名登录另一个主机。验证不需要密码或密码短语。这种方法对安全构成威胁，因为如果允许访问远程机器，他们就可以访问其他机器。这由主目录下的 `.hosts` 或 `.shorts` 文件。

## sftp 命令

`sftp` 命令用于通过 SSH 创建安全 FTP 隧道。这提供了 FTP 的功能和 SSH 的安全性。安全 FTP 在交互模式下与所有普通 FTP 命令兼容。

```
sftp -C 192.168.0.1
```

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_528_0.png)

图 12-30：使用 `sftp` 连接到远程系统。

`sftp` 命令的语法是 `sftp {hostname}` 或 `sftp {user}@hostname`。该命令还可以配合 `-C` 标志使用文件压缩。

## 隧道

隧道是一种分层协议模型，其中一种协议构建在另一种协议之上。内部协议（称为负载协议）封装在另一种协议（称为交付协议）中。这为连接提供了安全性和灵活性。隧道协议包括 `GRE`、`GTP` 和 `MPLS`。

当建立 SSH 协议连接时会创建一个 SSH 隧道。SSH 隧道允许用户通过设置代理服务器访问网站并绕过防火墙。被防火墙拦截的协议被封装在未被防火墙拦截的不同协议中，从而建立连接。

## X Forwarding

定义：
X 转发是一种机制，程序在一台机器上运行，并将 X 窗口输出显示在另一台机器上。通过在 `/etc/ssh/sshd_config` 文件中将 `X11Forwarding` 选项设置为 `yes` 或 `no` 可以启用或禁用 X 转发。这允许通过 SSH 连接建立 X11 隧道。

示例：

```
root@localhost:/etc/x11$

File Edit View Window Tabs Help

# Accept-related environment variables

AcceptEnv LC LC TYPE LC COLLATE LC MONETARY LC MESSAGES

AcceptEnv LC PAPER NAME LC ADDRESS LC TELEPHONE LC MEASUREMENT

AcceptEnv LC_IDENTIFICATION LC_ALL

#AllowTcpForwarding yes

#GatewayPorts no

#X11Forwarding yes

#X11DisplayOffset 18
```
