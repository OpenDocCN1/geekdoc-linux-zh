

## 4.3.4.1. 使用 TCP Wrappers 保护 rpcbind

使用 TCP Wrappers 来限制哪些网络或主机可以访问 rpcbind 服务至关重要，因为该服务没有内置的身份验证机制。

此外，在限制对该服务的访问时，仅使用 IP 地址。避免使用主机名，因为它们可能被 DNS 投毒和其他方法伪造。

## 4.3.4.2. 使用 firewalld 保护 rpcbind

为了进一步限制对 rpcbind 服务的访问，建议向服务器添加 firewalld 规则，并限制特定网络的访问。

以下是两个示例 firewalld 富语言命令。第一个命令允许来自 192.168.0.0/24 网络的 TCP 连接访问端口 111（由 rpcbind 服务使用）。第二个命令允许来自本地主机的 TCP 连接访问同一端口。所有其他数据包将被丢弃。

```bash
~]# firewall-cmd --add-rich-rule='rule family="ipv4" port port="111" protocol="tcp" source address="192.168.0.0/24" invert="True" drop'
~]# firewall-cmd --add-rich-rule='rule family="ipv4" port port="111" protocol="tcp" source address="127.0.0.1" accept'
```

以类似方式限制 UDP 流量，请使用以下命令：

```bash
~]# firewall-cmd --add-rich-rule='rule family="ipv4" port port="111" protocol="udp" source address="192.168.0.0/24" invert="True" drop'
```

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_47_0.png)

**注意**

在 `firewalld` 富语言命令中添加 `--permanent` 以使设置永久生效。有关实施防火墙的更多信息，请参阅 *Chapter 5, Using Firewalls*（第 5 章，使用防火墙）。

## 4.3.5. 保护 rpc.mountd

rpc.mountd 守护进程实现了 NFS MOUNT 协议的服务端，该协议被 NFS 版本 2 (RFC 1904) 和 NFS 版本 3 (RFC 1813) 使用。

如果正在运行 RPC 服务，请遵循以下基本规则。

### 4.3.5.1. 使用 TCP Wrappers 保护 rpc.mountd

使用 TCP Wrappers 来限制哪些网络或主机可以访问 rpc.mountd 服务至关重要，因为该服务没有内置的身份验证机制。

此外，在限制对该服务的访问时，仅使用 IP 地址。避免使用主机名，因为它们可能被 DNS 投毒和其他方法伪造。

### 4.3.5.2. 使用 firewalld 保护 rpc.mountd

为了进一步限制对 rpc.mountd 服务的访问，向服务器添加 firewalld 富语言规则，并限制特定网络的访问。

以下是两个示例 **firewalld** 富语言命令。第一个命令允许来自 `192.168.0.0/24` 网络的 `mountd` 连接。第二个命令允许来自本地主机的 `mountd` 连接。所有其他数据包将被丢弃。

```bash
~]# firewall-cmd --add-rich-rule 'rule family="ipv4" source NOT address="192.168.0.0/24" service name="mountd" drop'
~]# firewall-cmd --add-rich-rule 'rule family="ipv4" source address="127.0.0.1" service name="mountd" accept'
```

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_48_0.png)

在 **firewalld** 富语言命令中添加 `--permanent` 以使设置永久生效。有关实施防火墙的更多信息，请参阅 *Chapter 5, Using Firewalls*（第 5 章，使用防火墙）。

## 4.3.6. 保护 NIS

**网络信息服务**（NIS）是一种 RPC 服务，称为 `ypserv`，它与 `rpcbind` 和其他相关服务一起使用，将用户名、密码和其他敏感信息的映射分发到声称属于其域内的任何计算机。

NIS 服务器由几个应用程序组成。它们包括以下内容：

-   `/usr/sbin/rpc.yppasswd` - 也称为 `yppasswd` 服务，此守护进程允许用户更改其 NIS 密码。
-   `/usr/sbin/rpc.ypxfrd` - 也称为 `ypxfrd` 服务，此守护进程负责通过网络传输 NIS 映射。
-   `/usr/sbin/ypserv` - 这是 NIS 服务器守护进程。

按照当今标准，NIS 并不十分安全。它没有主机身份验证机制，并且通过网络传输的所有信息（包括密码哈希值）均未加密。因此，在设置使用 NIS 的网络时必须格外小心。这一点因 NIS 的默认配置本质上不安全而变得更加复杂。

建议计划实施 NIS 服务器的任何人首先按照 4.3.4 节“保护 `rpcbind`”中所述的安全措施保护 `rpcbind` 服务，然后解决网络规划等以下问题。

### 4.3.6.1. 仔细规划网络

由于 NIS 通过网络传输未加密的敏感信息，因此重要的是该服务应运行在防火墙后面，并且位于分段且安全的网络上。每当 NIS 信息在不安全的网络上传输时，就有被截获的风险。仔细的网络设计有助于防止严重的安全泄露。

### 4.3.6.2. 使用类似密码的 NIS 域名和主机名

NIS 域内的任何机器都可以使用命令从服务器提取信息，而无需身份验证，只要用户知道 NIS 服务器的 DNS 主机名和 NIS 域名即可。

例如，如果有人将笔记本电脑连接到网络，或者从外部闯入网络（并设法伪造内部 IP 地址），以下命令将显示 `/etc/passwd` 映射：

```bash
ypcat -d <NIS_domain> -h <DNS_hostname> passwd
```

如果该攻击者是 root 用户，他们可以通过输入以下命令获取 `/etc/shadow` 文件：

```bash
ypcat -d <NIS_domain> -h <DNS_hostname> shadow
```

> **注意**
>
> 如果使用 Kerberos，`/etc/shadow` 文件不会存储在 NIS 映射中。

为了使攻击者更难访问 NIS 映射，请为 DNS 主机名创建随机字符串，例如 `o7hfawtgmlwv.domain.com`。同样，创建一个*不同的*随机 NIS 域名。这使得攻击者访问 NIS 服务器变得更加困难。

### 4.3.6.3. 编辑 `/var/yp/securenets` 文件

如果 `/var/yp/securenets` 文件为空或不存在（默认安装后的情况便是如此），NIS 将监听所有网络。首先要做的事情之一是在该文件中放入网络掩码/网络对，以便 `ypserv` 仅响应来自适当网络的请求。

以下是 `/var/yp/securenets` 文件中的示例条目：

```text
255.255.255.0     192.168.0.0
```

> **警告**
>
> 切勿在创建 `/var/yp/securenets` 文件之前首次启动 NIS 服务器。

这种技术无法提供对 IP 欺骗攻击的保护，但它至少限制了 NIS 服务器服务的网络范围。

### 4.3.6.4. 分配静态端口并使用富语言规则

所有与 NIS 相关的服务器都可以分配特定端口，除了 `rpc.yppasswd` 之外 – 该守护进程允许用户更改其登录密码。为其他两个 NIS 服务器守护进程 `rpc.ypxfrd` 和 `ypserv` 分配端口，允许创建防火墙规则以进一步保护 NIS 服务器守护进程免受入侵者攻击。

为此，请向 `/etc/sysconfig/network` 添加以下行：

```bash
YPSERV_ARGS="-p 834"
YPPFRD_ARGS="-p 835"
```

然后可以使用以下富语言 **firewalld** 规则来强制执行服务器监听这些端口的网络：

```bash
~]# firewall-cmd --add-rich-rule='rule family="ipv4" source address="192.168.0.0/24" invert="True" port port="834-835" protocol="tcp" drop'
~]# firewall-cmd --add-rich-rule='rule family="ipv4" source address="192.168.0.0/24" invert="True" port port="834-835" protocol="udp" drop'
```

这意味着服务器仅允许来自 **192.168.0.0/24** 网络的请求连接端口 834 和 835。第一个规则适用于 **TCP**，第二个规则适用于 **UDP**。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_50_0.png)

> **注意**
>
> 有关使用 iptables 命令实施防火墙的更多信息，请参阅 *Chapter 5, Using Firewalls*（第 5 章，使用防火墙）。

### 4.3.6.5. 使用 Kerberos 身份验证

使用 NIS 进行身份验证时需要考虑的问题之一是，每当用户登录到机器时，`/etc/shadow` 映射中的密码哈希值都会通过网络传输。如果入侵者访问 NIS 域并嗅探网络流量，他们可以收集用户名和密码哈希值。经过足够的时间，密码破解程序可以猜测弱密码，攻击者可以获取网络上一个有效账户的访问权限。

由于 Kerberos 使用秘密密钥加密，因此密码哈希值永远不会通过网络传输，这使得系统更加安全。有关 Kerberos 的更多信息，请参阅 *Linux Domain Identity, Authentication, and Policy Guide*（Linux 域身份、身份验证和策略指南）中的 *Logging into IdM Using Kerberos*（使用 Kerberos 登录 IdM）部分。

## 4.3.7. 保护 NFS

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_50_1.png)

> **重要**
>
> NFS 流量可以使用 **TCP** 传输所有版本，NFSv3 应使用 **TCP** 而非 **UDP**，并且使用 NFSv4 时是必需的。所有版本的 NFS 都支持作为 **RPCSEC_GSS** 内核模块一部分的 Kerberos 用户和组身份验证。仍然包含有关 **rpcbind** 的信息，因为 Red Hat Enterprise Linux 7 支持利用 **rpcbind** 的 NFSv3。

### 4.3.7.1. 仔细规划网络

NFSv2 和 NFSv3 传统上不安全地传递数据。现在所有版本的 NFS 都有能力使用 Kerberos 对普通文件系统操作进行身份验证（并可选地加密）。在 NFSv4 中，所有操作都可以使用 Kerberos；在 NFSv2 或 NFSv3 中，文件锁定和挂载仍不使用它。使用 NFSv4.0 时，如果客户端位于 NAT 或防火墙后面，可以关闭委派。有关使用 NFSv4.1 允许委派通过 NAT 和防火墙操作的信息，请参阅 Red Hat Enterprise Linux 7 *Storage Administration Guide*（存储管理指南）中的 **pNFS** 部分。

