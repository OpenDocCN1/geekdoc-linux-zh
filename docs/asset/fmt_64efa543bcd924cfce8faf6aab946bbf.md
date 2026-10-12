
换句话说，当你指定一个服务器守护进程时，你可以将其与一组主机名或 IP 地址关联。当发生匹配时，你还可以触发命令，例如向用户发送消息或记录日志项。

## 使用 TCP WRAPPERS 控制访问

此命令的最简单版本是

`ALL:` 

它适用于所有的 `xinetd` 守护进程和所有计算机。选项非常复杂，因此最好的办法是一个一个检查选项。

## TCP WRAPPER 守护进程

你可以指定单个守护进程，但请记住守护进程名称是 `/etc/xinetd.d` 中配置文件的名称（不带扩展名）。例如，如果文件是 `/etc/xinetd.d/telnet`，则守护进程是 `telnet`。

# 理解安全外壳 (SSH)

提示：你甚至可以在 Microsoft Windows 计算机上使用 SSH。截至本文编写时，可以从 Network Simplicity (`www.networksimplicity.com`) 下载免费版本的 OpenSSH 软件包。一旦安装并配置完成，该客户端的工作方式与 Linux 版本的 SSH 一致。

## SSH 配置

主要的 SSH 配置文件是 `/etc/ssh/sshd_config`。虽然默认文件在大多数情况下都可以工作，但你可以调整该文件中的设置以适用于特殊的 TCP/IP 端口——例如访问不同的 IP 地址、调整加密密钥的大小、覆盖 RSH 认证以及启用 Kerberos 的使用。

一旦安装了相应的软件包，下一步是创建私钥和公钥加密密钥。你将私钥保存在 Linux 服务器上。公钥加密允许他人对发送给你的消息进行加密。或者，你用私钥加密的消息包含公钥，公钥用于在你的目标计算机上解密消息。密钥基于巨大的随机数（512 位及更多），以至于使用个人电脑的破解者需要几周时间才能完成破解。

两个基本的 SSH 命令允许你创建私钥和公钥：`ssh-keygen -t rsa` 和 `ssh-keygen -t dsa`。这些命令让你能够根据 RSA Security 或数字安全算法（Digital Secure Algorithm）创建的算法创建密钥。

这两个命令默认会在用户主目录的 `ssh` 子目录下创建私钥和公钥；创建 `~/.ssh` 文件，如表 18.5 所示。在提示时，请创建一个短语。如果你不设置短语，破解者可能会窃你的 SSH 私钥。在某些情况下，这将允许破解者利用你的数字身份使用你的信用卡或以你的名义签署合同。

| 表格 18.5：默认 SSH 密钥文件 |
| 算法 | 私钥 | 公钥 |
| :--- | :--- | :--- |
| DSA | `~/.ssh/id_dsa` | `~/.ssh/id_dsa.pub` |
| RSA | `~/.ssh/id_rsa` | `~/.ssh/id_rsa.pub` |

## 示例会

一旦你在客户端上安装了 RPM 并创建了相应的 SSH 密钥，你就可以开始使用安全外壳了。如果需要，你可以通过 `service ssh status` 命令来检查 SSH 服务器是否正在运行。

现在你可以直接连接到另一台计算机上的你的账户。例如，假设你是一个名为 `chavez` 的用户，并且在两台计算机上都有账户。运行 `ssh sugaree.momabbears.com` 命令连接到该计算机。请确保将 `sugaree.momabbears.com` 替换为你选择的计算机名称或 IP 地址。

当你第一次尝试使用 ssh（或相关命令）连接时，你会看到类似下面的消息：

> 主机 'sugaree.momabbears.com (192.168.1.2)' 的真实性无法确认。

# 第 18 章 远程环境

RSA 密钥指纹为 `34:21:d2:3c:34:83:40:23:d2:c2:9f:34:90:e3:a3`。

你确定要继续连接吗 (yes/no)？

选择 Yes，并在远程计算机上输入你的密码以完成连接。你可以在远程计算机上工作，并且你的计算机之间的消息将经过加密。或者，你也可以登录不同的账户——例如如下登录 `vputin`：

```
# ssh vputin@sugaree.momabbear.com
```

或者，你也可以使用与 SSH 关联的安全 FTP 服务。如果用户 `vputin` 在他的账户中有一组 RPM 软件包，并且你拥有密码，你就可以使用安全 FTP 服务从他的主目录下载文件到远程计算机。例如，以下命令登录该账户并将新的 GNU C 编译器的源代码下载到本地的 `/tmp` 目录：

```
# sftp vputin@sugaree.momambear.com

sftp get gcc-3.9-8.src.rpm /tmp
```

## 访问问题排排除

有了所有这些层保护，理解访问问题可能需要一些侦查工作。如果你的用户在访问你计算机上的服务时遇到困难，请遵循以下步骤：

- 确保服务已安装。
- 检查服务是否处于激活状态。
- 检查与服务相关的安全配置文件。
- 如果是 `xinetd` 服务，检查 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。
- 通过 `iptables -L` 检查 iptables 链。

### 检查服务是否已安装

检查已安装的服务很简单；如第 10 章所述，使用 `rpm -q package` 检查 RPM 软件包的安装情况。请记住，将服务组织在独立的客户端和服务器软件包中是常见的。例如，Telnet、FTP 和 SSH 都有独立的客户端和服务器软件包。

### 验证服务是否已激活

使用 `/etc/rc.d/init.d` 目录下的脚本非常容易。正如第 13 章讨论，每个守护进程都包含该目录下的一个脚本，你可以通过 `/etc/rc.d/init.d status` 命令检查它。或者，你可以使用 `service status` 命令。

如果你对 `xinetd` 服务感兴趣，请检查 `/etc/xinetd.conf` 中的配置文件。默认情况下，这些服务被设置为 `no`，这将保持服务关闭状态。不要忘记使用如 `xinetd` 等工具来确保下次重启时服务处于激活状态。例如，以下命令验证了服务 处于激活状态：

```
# httpd on
```

## 启动访问所需的 TFTP

在这种情况下，TFTP（简易文件传输协议）服务器的作用是支持从 PXE 启动环境访问共享的操作系统。一旦 Linux 加载到终端上，将使用 NFS 连接到共享目录。

TFTP 是一个 `xinetd` 服务。它默认是关闭的。因此，您将需要运行以下命令，以确保现在和下次启动 Linux 时它都能通过 `xinetd` 运行：

```
# chkhconfig --level tftp on
```

我们假设您没有更改 `xinetd` 的默认设置（`xinetd` 默认在运行级别 3、4 和 5 下启动）。

## 为无盘化访问配置 DHCP 服务器

PXE 启动系统依赖 DHCP 服务器来获取 IP 地址信息。这意味着您需要知道如何配置 DHCP 服务器，这在第 19 章中会有描述。关键在于，您需要为网络上您想要配置的每个终端配置 DHCP 地址。

在第 4 章中，我们简要描述了为网络安装配置 PXE 启动的过程。对于无盘工作站服务器，其基本步骤是相同的。您需要将基本命令添加到主 DHCP 配置文件 `/etc/dhcpcd.conf` 中。

```
allow booting;

allow boot;

class "pexclients" {

match substring(option vendor-class-identifier, 0, 9)="PXEClient";

next-server 192.168.1.4;

filename "linux-install/pxelinux.0";

}
```

Red Hat 系统还要求您为每个无盘工作站配置静态 IP 地址。在标准的 `dhcpcd.conf` 文件中，已经有一组用于为 DNS 服务器配置 IP 地址的标准标准命令。您可以根据需要为每个工作站调整这些命令。

```
host diskless1 {

  next-server server.example.com;

  hardware ethernet AB:CD:EF:12:34:56;

  fixed-address 192.168.1.122;

}
```

此特定命令假设无盘工作站有一个特定的硬件地址（`AB:CD:EF:12:34:56`）。它分配了特定的主机名（`diskless1`）和 IP 地址（`192.168.1.122`）。

您可能可以从 BIOS 中获取 PXE 网卡的硬件地址。或者，它可能在您启动 PXE 引导时列出。

如果您尚未为您的网络激活 DHCP 服务器，您将需要按照第 19 章描述的那样进行。正如我们在第 13 章描述的，基本命令非常直观。我们启动服务并确保它在您启动 Linux 时启动：

```
# service dhcpd start

# chkhconfig --level 3 dhcpd
```
