
## 第 8 章 | 网络文件系统与远程访问

默认情况下，加密密钥基于 RSA 算法，可以配置为 768 位及以上。位数较大的密钥（例如 4,096 位）可能需要一些时间来创建。虽然可以使用相同的命令通过 `-t dsa` 选项创建 DSA 密钥，但只有 1,024 位的 DSA 密钥可用。你现在应该可以在家目录的 `.ssh/` 子目录下看到上述 `id_rsa` 和 `id_rsa.pub` 文件。

下一步是将 `id_rsa.pub` 密钥拷贝到远程服务器。虽然你可以使用 U 盘来实现此目的，但你也可以使用 `ssh-copy-id` 命令来传输公钥：

```
$ ssh-copy-id -i .ssh/id_rsa.pub LucidServer.example.org
```

如果这是首次连接到上述 LucidServer 系统，你将看到类似于图所示的消息：

> 无法建立主机 'lucidservermin.example.org' (192.168.100.27) 的真实性。RSA 密钥指纹为 [某些解码后的十六进制数字]

假设 IP 地址是你的预期值，请在提示处输入 `yes` 以继续连接：

你确定要继续连接吗？ (yes/no)? yes
警告: 已将 'lucidserver.example.org' (RSA) 永久添加到已知主机列表中。

如果你永远不想在网络上传输加密密码，那么接下来的消息应该让你停下来考虑。如果你有意，请在此处停止并通过 U 盘退出。
michael@lucidservermin.example.org's password:

如果你使用有效的密码继续操作，上述 `id_rsa.pub` 文件的内容将附加到远程系统 `.ssh/authorized_keys` 文件的末尾。换句话说，如果你真的非常谨慎（妄想），可以将 `id_rsa.pub` 文件拷贝到 U 盘，将 U 盘连接到远程系统，并在远程系统上运行以下命令（在此例中为 lucidserver.example.org）：

```
$ cat id_rsa.pub >> .ssh/authorized_keys
```

如果成功，你现在将能够使用口语连接到远程系统。你将看到以下提示：

Enter passphrase for key '/home/michael/.ssh/id_rsa':

或者，如果网络上启用了 X11 通信，可能会看到类似于图 8-1 所示的窗口。

## 238 第 2 部分 | 分层安全与 Linux

![](img/c0608a8c8a0777903dfec4ff61fdffa1_263_0.png)

## 网络与加密

你已经介绍了使用 SSH 的加密通信方法。还有其他方法。一种常用的是网协议安全，在 Linux 中被称为 IPSec。它在连接的两端工作，通过协议 50 和 51 对通信进行隧道。在隧道模式下，它是虚拟专用网络的形式。

另一种方法基于安全套接层 (SSL) 协议。对于大多数系统，它被传输层安全 (TLS) 取代。在大多数情况下，它使用不同的协议为常用服务启用加密通信。SSL 和 TLS 的用法将详细讨论，从本章讨论电子邮件客户端开始。更多信息，请参阅第 9 章关于网络应用程序安全版本的讨论。

本节的重点是 IPSec 连接。IPSec 是一种使用安全隧道连接远程主机和网络的方法。IPSec 可以通过 Internet 连接不同的私有网络。它依靠封装来隐藏公用网络上的通信。

IPSec 连接使用不同的端口和协议号。假设每个网络上都配置了防火墙，你必须确保这些端口和协议在相应网络上是这些：

- * 封装负载 (ESP)—使用协议号 50。ESP 流量可以通过 iptables 防火墙的 `-p 50 -j ACCEPT` 选项允许。
- * 身份验证头 (AH) 协议——使用协议号 51。AH 流量可以通过 iptables 防火墙的 `-p 51 -j ACCEPT` 选项允许。
- * 互联网密钥交换 (IKE) 协议——使用端口 500 上的数据报协议 (UDP)。IKE 流量可以通过 iptables 防火墙的 `-p udp --dport 500 -j ACCEPT` 选项允许。
- * 网络地址转换 (NAT) 穿透协议——使用端口 4500 上的传输控制协议 (TCP) 和 UDP。NAT 流量可以通过 iptables 防火墙的 `-p tcp --dport 4500 -j ACCEPT` 选项允许。

通过 Ike 服务（有时称为 racoon）进行 IPsec 加密。I 服务在 `/etc/racoon/` 目录下的文件中配置。在 Ubuntu 系统上，IPSec 在 `/etc/ipsec-tools.conf` 文件中配置。或者，如果你使用 Red Hat 的网络配置工具，你将在 `/etc/sysconfig/network-scripts/` 目录下的专用文件中看到相应的配置指令。Red Hat 的配置在以下每个小节中首先描述，因为它包含了需要配置的内容。无论何种情况，如果连接成功，你都可以在两端运行类似 `tcpdump` 的命令来检测带有上述端口号的流量。

## Red Hat 主机到主机 IPSec

在 Red Hat 系统上，IPSec 主机到主机连接在 `/etc/sysconfig/network-scripts/` 目录下的两个文件中配置。一个是 `ifcfg-host`，其中 `host` 是主机到主机设备的名称。配置简单，仅包含四个指令：

```
DST=192.168.122.127
TYPE=IPSEC
BOOT=yes
IKE_METHOD=PSK
```

假设本地主机是连接的一端；`DST` 是目标。这是一个在启动过程中激活的 IPSec 连接，且 IKE 方法应该是远程系统上的匹配文件。区别在于与 `DST` 指令关联的 IP 地址。

两个系统都需要认证。该文件将存储在相同的 `/etc/sysconfig/network-scripts/` 目录下，名为 `keys-host`。该文件应仅为 root 管理用户设置读写权限。

## Ubuntu 主机到主机 IPSec

在 Ubuntu 系统上，IPSec 主机到主机连接在 `/etc/sysconfig/network-scripts/` 目录下的两个文件中配置。一个是 `ifcfg-host`，其中 `host` 是主机到主机设备的名称。配置简单，仅包含四个指令：

```
DST=192.168.122.127
TYPE=IPSEC
BOOT=yes
IKE_METHOD=PSK
```

（注：由于原文 OCR 文本存在重复和混乱，此处已根据逻辑进行了清理合并。）
