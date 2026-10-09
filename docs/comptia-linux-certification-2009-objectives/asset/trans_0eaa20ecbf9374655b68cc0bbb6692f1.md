
仅当目的地的私钥与原始服务器的公钥结合时，验证才能完成。在登录远程系统时，远程服务器会将私钥和公钥组合起来进行验证。如果用户需要登录系统并传输文件，密钥必须匹配。远程服务器将验证真实性，然后授予必要的权限。

## 密钥文件

使用 SSH 创建的密钥对会根据所使用的算法存储在不同的文件中。

| 创建的文件 | 算法 |
| :--- | :--- |
| id_dsa, id_dsa.pub | DSA |
| id_rsa, id_rsa.pub | 使用 SSH 协议版本 2 的 RSA |
| identity, identity.pub | 使用 SSH 协议版本 1 的 RSA |

## /etc/ssh/sshd_config 文件

`/etc/ssh/sshd_config` 文件是 SSH 服务器配置文件。该配置文件中的大多数行都被注释掉了，这表示已经应用的默认设置。您可以移除注释并更改默认设置。下表列出了几个 SSH 服务器配置文件的选项。

| 使用此 sshd 选项 | 如果你需要 |
| :--- | :--- |
| X11Forwarding yes | 在一个系统上运行或停止运行程序，并在另一个系统上显示 X 窗口输出。 |
| X11Forwarding no | 停止在一个系统上运行程序，并停止在另一个系统上显示 X 窗口输出。 |
| PermitRootLogin | 允许 root 用户通过 SSH 登录。 |
| MaxStartups 数量 | 指定可以建立到主机连接的最大数量。 |
| LoginGraceTime 秒数 | 如果未在登录宽限时间内建立连接，则断开连接。 |
| AuthorizedKeysFile 文件名 | 指定包含认证密钥的文件位置。 |
| PermitEmptyPasswords yes/no | 指定是否允许或拒绝空密码。 |

## sftp 命令

![](img/477ccb2f05b6ba1b2d563ea74f18c197_607_0.png)

sftp 命令用于通过 SSH 创建安全的 FTP 隧道。因此，它提供了具有 SSH 安全性的 FTP 功能。安全 FTP 在交互模式下与所有常规 FTP 命令兼容。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_607_1.png)

图 12-56：使用 sftp 连接到远程系统。

### 语法

命令的语法是 `sftp hostname` 或 `sftp user@hostname`。该命令也可以与 `-C` 标志一起使用以允许文件压缩。

### 隧道技术

![](img/477ccb2f05b6ba1b2d563ea74f18c197_607_2.png)

隧道技术是一种分层协议模型，其中一个协议叠加在另一个协议之上。内部协议称为有效载荷协议，它封装在另一个称为传输协议中。这为连接提供了安全性和灵活性。一些隧道协议包括 GRE、GTP 和 MPLS。

当建立 SSH 协议连接时，会创建一个 SSH 隧道。SSH 隧道允许用户通过设置代理服务器来访问网站并绕过防火墙。被防火墙阻止的协议会被封装在另一个未被防火墙阻止的协议中，从而建立连接。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_607_3.png)

图 12-57：隧道协议及其架构。

## 虚拟网络计算

定义：

虚拟网络计算（VNC）是一个与平台无关的系统，用户可以通过它控制远程系统。虚拟网络由 VNC 客户端、VNC 服务器和 VNC 协议组成。客户端通过 VNC 协议查看服务器显示的输出。用户可以在同一时间运行多个 VNC 会话。然而，每个 VNC 客户端的显示可能与 VNC 服务器的显示不同。

示例：

![](img/477ccb2f05b6ba1b2d563ea74f18c197_608_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_608_1.png)

图 12-58：VNC 协议允许客户端查看由 VNC 服务器显示的输出。

## vncserver 命令

vncserver 命令用于启动带有 VNC 的系统。`$HOME/.vnc/xstartup` 文件允许用户控制远程系统上运行的应用程序。您可以指定 VNC 服务器启动时将使用的显示编号。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_608_2.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_609_0.png)

```bash
[root@localhost ~]# vncserver

New 'localhost:1 (root)' desktop is localhost:1
Starting applications specified in /root/.vnc/xstartup
Log file is /root/.vnc/localhost:1.log

[root@localhost ~]#
```

图 12-59：在 Linux 系统上启用 VNC。

vncserver 命令具有各种选项。

| 选项 | 允许你 |
| :--- | :--- |
| -name *桌面名称* | 指定桌面名称。 |
| -geometry *分辨率* | 指定远程桌面的屏幕分辨率。 |
| -depth *深度* | 指定桌面的像素深度。接受的值为 8、15 和 24。 |
| -pixelformat *格式* | 指定像素格式，例如 RGB 和 BGR。 |

### 语法

vncserver 命令的语法是 `vncserver { :显示编号 } { -选项 }`。

## vncviewer 命令

vncviewer 命令用于查看 VNC 客户端。有各种选项用于指定 vncviewer 参数。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_609_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_610_0.png)

图 12-60：vncviewer 命令用于连接 VNC 服务器。

| 选项 | 允许你 |
| :--- | :--- |
| -display Xdisplay | 指定 X 显示。 |
| -listen 端口 | 查找来自 VNC 服务器的反向连接。 |
| -Shared | 保持多个 VNC 连接打开。 |
| -FullScreen | 以全屏模式启动 VNC 客户端。 |
| -via 网关 | 创建到网关系统的隧道，然后连接客户端到主机。 |

## rdesktop 工具

rdesktop 是一个开源工具，在 GPL 下发布。它使运行 Linux 的客户端系统能够通过网络登录到运行 Microsoft Windows 的系统。它支持 Microsoft 的远程桌面协议（RDP）。rdesktop 命令可用于登录到远程 Windows 系统。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_610_1.png)

rdesktop 工具

![](img/477ccb2f05b6ba1b2d563ea74f18c197_610_2.png)

图 12-61：使用 rdesktop 帮助 Linux 系统登录到 Windows 系统。

### 语法

`rdesktop` 命令的语法是 `rdesktop [选项] 服务器[:端口]`。

### rdesktop 命令选项

下表列出了常用的一些 `rdesktop` 命令选项。

| 选项 | 用于 |
| :--- | :--- |
| -u | 指定服务器上认证的用户名。 |
| -d | 指定认证域。 |
| -s | 启动特定应用程序而不是资源管理器。 |
| -c | 指定用户的初始工作目录。 |
| -p | 指定认证密码。 |

## RDP

RDP 是一种多通道协议，允许运行其他操作系统的用户连接到运行 Microsoft Windows 的系统，反之亦然，在网络上实现。

## 简单网络管理协议

![](img/477ccb2f05b6ba1b2d563ea74f18c197_611_0.png)

简单网络管理协议（SNMP）使你能够远程监控和配置网络组件，如网桥、路由器、网卡和交换机。

SNMP 管理需要两个主要元素：网络管理器和 SNMP 代理。

| 元素 | 描述 |
| :--- | :--- |
| 网络管理器 | 运行在工作站上的软件，网络管理员通过它监控和控制组成网络的不同硬件和软件系统。 |
| SNMP 代理 | 运行在网络设备上并实现 SNMP 协议的一部分软件。SNMP 准确定义了网络管理器如何与 SNMP 代理通信。 |

## 远程监控

远程监控（RMON）是一种网络管理协议，允许在单一工作站上收集网络信息。要使 RMON 正常工作，网络设备，如集线器和交换机，必须支持它。

## 如何管理远程网络系统

### 操作参考：使用安全 shell 通信

若要使用安全 shell 进行通信：

- 1. 登录为用户。
- 2. 安全连接到另一台计算机。
  - a. 输入 `ssh user_name@(目标主机名或 IP)` 以连接到远程主机。
  - b. 如果提示，将该主机添加为受信任主机。
  - c. 输入密码以登录系统。
- 3. 在另一台计算机上安全地执行命令。
  - a. 输入 `ssh user_name@(目标主机名或 IP)` 以连接到远程主机。
  - b. 如果提示，将该主机添加为受信任主机。
  - c. 输入密码以登录系统。
  - d. 输入命令以执行所需操作。
- 4. 使用 SSH 创建隧道。
  - a. 输入 `ssh -L (端口号):(远程服务器 IP 或 FQDN):(端口号) user_name@远程服务器 IP 或 FQDN` 以使用 SSH 创建隧道。
  - b. 如果提示，将该主机添加为受信任主机。
  - c. 输入密码以登录系统。
- 5. 使用 SSH 密钥对隧道进行认证。
  - a. 输入 `ssh-keygen -d` 以生成密钥。
  - b. 按 Enter 键三次，在 `/root/ssh` 中生成密钥 `id_dsa` 和 `id_dsa.pub`。
  - c. 登录到你要建立 SSH 连接的第二个系统的 root 用户。
  - d. 输入 `ssh-keygen -d`。
  - e. 按 Enter 键三次，在 `/root/ssh` 中生成密钥 `id_dsa` 和 `id_dsa.pub`。
  - f. 输入 `scp /root/.ssh/id_dsa.pub user_name@(第一个系统的 IP 或 FQDN):/root/.ssh/authorized_keys` 以将公钥从第二个系统复制到第一个系统。
  - g. 如果提示，将该主机添加为受信任主机。
  - h. 输入密码以登录系统。
  - i. 输入 `scp /root/.ssh/id_dsa.pub user_name@(第一个系统的 IP 或 FQDN):/root/.ssh/authorized_keys` 以将公钥从第一个系统复制到第二个系统。
  - j. 如果提示，将该主机添加为受信任主机。
  - k. 输入密码以登录系统。

### 操作参考：安全地传输文件到另一台计算机

若要安全地传输文件到另一台计算机：

- 1. 在 CLI 中登录为用户。

