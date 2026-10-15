
![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_45_0.png)

## 注意

在 Red Hat Enterprise Linux 7 中，ExecShield 减轻了缓冲区溢出漏洞的威胁。ExecShield 是一种可执行内存分段和保护技术，受 x86 兼容的单处理器和多处理器内核支持。ExecShield 通过将虚拟内存分离为可执行和非可执行段来降低缓冲区溢出的风险。任何试图在可执行段之外执行代码的程序（例如从缓冲区溢出利用中注入的恶意代码）都会触发段错误并终止。

ExecShield 还支持 AMD64 平台和 Intel® 64 系统上的 No eXecute (NX) 技术。这些技术与 ExecShield 协同工作，以 4KB 可执行代码为粒度，防止恶意代码在虚拟内存的可执行部分中运行，从而降低缓冲区溢出利用的攻击风险。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_45_1.png)

## 重要

为了限制通过网络遭受攻击的暴露面，应关闭所有未使用的服务。

### 4.3.2. 识别和配置服务

为了增强安全性，Red Hat Enterprise Linux 7 安装的大多数网络服务默认关闭。不过，有一些值得注意的例外：

- `cups` – Red Hat Enterprise Linux 7 的默认打印服务器。
- `cups-lpd` – 另一种打印服务器。
- `xinetd` – 一个超级服务器，控制对一系列下级服务器（如 `gssftpd` 和 `telnet`）的连接。
- `sshd` – OpenSSH 服务器，是 Telnet 的安全替代品。

在决定是否让这些服务保持运行时，最好使用常识并避免承担任何风险。例如，如果没有打印机可用，就不要让 `cups` 保持运行。`portreserve` 也是如此。如果您不挂载 NFSv3 卷或使用 NIS（`ysbind` 服务），则应禁用 `rpcbind`。仅检查哪些网络服务在启动时可用是不够的。建议同时检查哪些端口是打开且正在监听的。更多信息请参阅第 4.4.2 节 “验证哪些端口正在监听”。

### 4.3.3. 不安全的服务

潜在地，任何网络服务都可能是不安全的。这就是为什么关闭未使用的服务如此重要。

服务漏洞通常会被揭示并修补，因此定期更新与任何网络服务相关的软件包非常重要。更多信息请参阅第 3 章 *保持系统最新*。

某些网络协议天生比其他协议更不安全。包括以下任何服务：

- **在网络上传输未加密的用户名和密码** – 许多旧协议，如 Telnet 和 FTP，不加密身份验证会话，应尽可能避免使用。
- **在网络上传输未加密的敏感数据** – 许多协议通过网络传输未加密的数据。这些协议包括 Telnet、FTP、HTTP 和 SMTP。许多网络文件系统，如 NFS 和 SMB，也通过网络传输未加密的信息。使用这些协议时，限制传输的数据类型是用户的责任。

天生不安全服务的示例包括 `rlogin`、`rsh`、`telnet` 和 `vsftpd`。

所有远程登录和 shell 程序（`rlogin`、`rsh` 和 `telnet`）都应避免使用，转而使用 `SSH`。有关 `sshd` 的更多信息，请参阅 *第 4.3.11 节* “保护 SSH”。

`FTP` 不像远程 shell 那样对系统安全性天生危险，但必须仔细配置和监控 `FTP` 服务器以避免问题。有关保护 FTP 服务器的更多信息，请参阅 *第 4.3.9 节* “保护 FTP”。

应仔细实现并放置在防火墙后面的服务包括：

- auth
- nfs-server
- smb 和 nbm (Samba)
- yppasswdd
- yperv
- ypfxrd

有关保护网络服务的更多信息，请参阅 *第 4.4 节* “保护网络访问”。

### 4.3.4. 保护 rpcbind

`rpcbind` 服务是 NIS 和 NFS 等 RPC 服务的动态端口分配守护进程。它具有较弱的身份验证机制，并能够为其控制的服务分配广泛的端口范围。因此，它很难得到保护。

> **注意**
>
> 保护 `rpcbind` 仅影响 NFSv2 和 NFSv3 实现，因为 NFSv4 不再需要它。如果您计划实现 NFSv2 或 NFSv3 服务器，则必须使用 `rpcbind`，并且下一节内容适用。

如果运行 RPC 服务，请遵循以下基本规则。

#### 4.3.4.1. 使用 TCP Wrappers 保护 rpcbind

使用 TCP Wrappers 来限制哪些网络或主机可以访问 `rpcbind` 服务至关重要，因为该服务没有内置的身份验证机制。

此外，在限制对该服务的访问时，仅使用 IP 地址。避免使用主机名，因为它们可能被 DNS 投毒和其他方法伪造。

#### 4.3.4.2. 使用 firewalld 保护 rpcbind

为了进一步限制对 `rpcbind` 服务的访问，建议向服务器添加 `firewalld` 规则，并限制特定网络的访问。

以下是两个示例 `firewalld` 富语言命令。第一个命令允许来自 `192.168.0.0/24` 网络的 TCP 连接访问端口 111（由 `rpcbind` 服务使用）。第二个命令允许来自本地主机的 TCP 连接访问同一端口。所有其他数据包将被丢弃。

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

### 4.3.5. 保护 rpc.mountd

`rpc.mountd` 守护进程实现了 NFS MOUNT 协议的服务端，该协议被 NFS 版本 2 (RFC 1904) 和 NFS 版本 3 (RFC 1813) 使用。

如果正在运行 RPC 服务，请遵循以下基本规则。

#### 4.3.5.1. 使用 TCP Wrappers 保护 rpc.mountd

使用 TCP Wrappers 来限制哪些网络或主机可以访问 `rpc.mountd` 服务至关重要，因为该服务没有内置的身份验证机制。

此外，在限制对该服务的访问时，仅使用 IP 地址。避免使用主机名，因为它们可能被 DNS 投毒和其他方法伪造。

#### 4.3.5.2. 使用 firewalld 保护 rpc.mountd

为了进一步限制对 `rpc.mountd` 服务的访问，向服务器添加 `firewalld` 富语言规则，并限制特定网络的访问。

以下是两个示例 `firewalld` 富语言命令。第一个命令允许来自 `192.168.0.0/24` 网络的 `mountd` 连接。第二个命令允许来自本地主机的 `mountd` 连接。所有其他数据包将被丢弃。

```bash
~]# firewall-cmd --add-rich-rule 'rule family="ipv4" source NOT address="192.168.0.0/24" service name="mountd" drop'
~]# firewall-cmd --add-rich-rule 'rule family="ipv4" source address="127.0.0.1" service name="mountd" accept'
```

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_48_0.png)

在 `firewalld` 富语言命令中添加 `--permanent` 以使设置永久生效。有关实施防火墙的更多信息，请参阅 *Chapter 5, Using Firewalls*（第 5 章，使用防火墙）。

### 4.3.6. 保护 NIS
