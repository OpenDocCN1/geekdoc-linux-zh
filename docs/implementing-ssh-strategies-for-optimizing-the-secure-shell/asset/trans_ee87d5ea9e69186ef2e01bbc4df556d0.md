
## 第1章 引言

除了偶尔提及外，并未对其进行深入介绍。高级用户可能会选择直接跳转到下一章。具体而言，本章讨论以下主题：

- SSH1 和 SSH2 之间的差异
- SSH 的用途
- SSH 的客户端/服务器架构
- SSH 的加密架构
- 使用 SSH 时的常见误区
- SSH 客户端/服务器的类型
- SSH 的基本设置
- SSH 最佳用途总结

### SSH1 和 SSH2 之间的差异

SSH 第 1 版（SSH1）是 SSH 的初始版本；然而，SSH1 存在若干局限性，包括使用端口转发，这促使了 SSH 的第二代版本 SSH 第 2 版（SSH2）的出现。除了这些局限性外，SSH1 还存在一些与其加密相关的**安全问题**，这也推动了 SSH2 的建立。

SSH1 和 SSH2 之间的差异对于大多数终端用户来说可能看似微小；然而，这些差异其实**意义重大**。SSH1 和 SSH2 是两种不同的协议。SSH2 是从头彻底重新编写的，赋予了它比 SSH1 更高的安全性、性能和灵活性。此外，SSH1 和 SSH2 使用不同的方式加密通信，从而缓解了 SSH1 加密方法中记录在案的若干问题。SSH1 目前已不再进行开发，而 SSH2 正逐渐成为一种标准。尽管仍存在许多 SSH1 的实现，但这类实现正日益减少，SSH2 则越来越受到青睐。就本书而言，我不会提及、使用或演示 SSH1。我仅专注于 SSH2 的使用和优化。以下是使用 SSH2 而非 SSH1 的优势列表：

- 在安全性和速度方面有显著改进
- 在安全文件传输协议（SFTP）方面具备显著更高的灵活性
- 能与多种不同的公钥算法互操作，包括 Diffie-Hellman（有关 Diffie-Hellman 的更多信息，请参见 http://www.rsasecurity.com/rsalabs/faq/3-6-1.html）
- 需要极少代码使用量的全新架构

### SSH 的多种用途

根据你的网络环境和业务需求，SSH 可以有多种使用方式。SSH 在任何动态或静态环境中提供的灵活性，使其在行业中的其他工具（无论是侧重安全性的工具，如 IPSEC，还是非侧重安全性的工具，如 FTP）中拥有显著优势。SSH 可以在服务器上仅运行一个进程（守护程序）或服务，即可支持多个用户，且大部分配置在客户端侧即可完成。在本书的进程中，我将探讨 SSH 的各种用途；不过，我将利用本章的大半篇幅来描述 SSH 的不同用途，以展示其完整的功能：

- 安全
- 远程命令执行
- 远程文件传输
- 远程网络访问
- 安全管理
- 代理服务

### 安全

在受信任或不受信任的环境中部署 SSH，可以抵御许多与 IPv4 相关的安全问题。IPv4 一直备受安全问题的困扰，这些问题从 TCP 头部数据包中较差的初始序列号（ISN），从而导致会话劫持，到在网络中分发未经验证的地址解析协议（ARP）数据包不等。使用 SSH 不仅能抵御前文所述的常见 LAN 攻击；它还能防范以下类型的攻击：

- **IP 地址伪装。** 远程设备（通常是操作系统）可以更改其 IP 地址，并伪装成其他来源（通常是受信任的来源）。
- **数据篡改。** 当数据在企业网络和互联网上传输时，任何中间人都有可能在中途修改这些数据。
- **ARP 污染。** 此情况发生在错误的 ARP 数据包被分发以重定向和捕获敏感数据时。
- **会话劫持。** 此情况发生在个人猜测或预测 TCP 头部的 ISN，从而接管 Telnet 和 RSH 会话时。
- **明文数据。** 此情况发生在关键的或敏感的明文数据（如用户名、密码和命令）被截获时。

上述列表并不详尽，因为 SSH 还能抵御许多其他直接攻击或间接攻击。SSH 如此受欢迎的原因在于它能够防御局域网（LAN）和广域网（WAN）上的网络嗅探。该特性使网络管理员和服务器管理员能够在不将敏感信息泄露给未授权用户风险下，管理和连接远程系统。图 1.1 展示了两个实体之间以明文传输的 Telnet 数据包：

请注意，在图 1.1 中，用户名以明文“kusrum”显示，密码也以明文“password”显示。只要会话是明文传输，任何类型的网络嗅探器都可以捕获该会话。一些最常见且易受攻击的连接（经常成为敏感信息（如密码）的目标）包括 Telnet、FTP、POP3、SMTP、IMAP、SNMP 和 HTTP。图 1.2 展示了与图 1.1 中使用相同的两个实体之间传输的 SSH 数据包。

请注意，在图 1.2 中，没有任何信息是明文或可识别的，因此已被加密。该连接类似于 Telnet 连接（远程命令行执行），但在用户名和密码“kusrum”上的安全性显著提高。

SSH 提供以下三种关键的安全功能：

- **加密。** SSH 使用各种加密算法对通信进行加密。
- **双因子认证。** SSH 可以要求使用用户名/密码或公钥进行认证。此外，这两种选项可以一起使用来实现双因子认证。
- **完整性。** SSH 可以创建从一个实体传输到另一个实体的数据的数字签名，以确保数据未以任何方式被篡改。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_34_0.png)

图 1.1 两个实体之间以明文传输的 Telnet 数据包。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_35_0.png)

**图 1.2** SSH 数据包的内容。

### 远程命令行执行

SSH 提供了在远程实体（可以是操作系统或网络设备）上执行命令的功能。在 Unix 世界中，SSH 会为远程用户提供 /etc 目录中 passwd 文件中列出的 Shell；然而，通信仍然通过线路加密。例如，基于以下 Unix passwd 文件：

```
root::x:0:0:/root:/bin/bash
ksum::x:4:101:Kusum:/home/Kusum:/bin/bash
shreya::x:4:102:shreya:/home/shreya:/bin/bash
sudhanshu::x:4:103:sudhanshu:/home/sudhanshu:/bin/csh
sangeeta::x:4:104:sangeeta:/home/sangeeta:/bin/bash
jgnesh::x:4:105:jgnesh:/home/jgnesh:/bin/bash
kanchan::x:4:106:kanchan:/home/kanchan:/bin/bash
Katie::x:4:107:Katie:/home/Katie:/bin/csh
amit::x:4:108:amit:/home/amit:/bin/bash
rohan::x:4:109:rohan:/home/rohan:/bin/bash
anand::x:4:110:anand:/home/anand:/bin/bash
amlee::x:4:111:amlee:/home/amlee:/bin/sh
neeraja::x:4:112:neeraja:/home/neeraja:/bin/sh
jumdnj1::x:4:113:Jumdnj1:/home/Jumdnj1:/sbin/nologin
```

root 获得 bash shell，sudhanshu 获得 C shell，neeraja 获得 Korn shell，而用户[umdnj1]不被允许登录，因为尽管[umdnj1]的账户进行了有效的 SSH 连接，但其分配的 shell 为 nologin。运行在 Unix 服务器上的 SSH 守护程序会查询 passwd 文件中的信息，以处理用于认证的用户名。SSH 不使用自己的用户名和密码进行认证；它使用操作系统的用户名和密码信息，这大大简化了该过程。结果将是，拥有 passwd 文件中合适 shell 的有效账户经过认证后将获得正确的 shell，同时通过 SSH 进行加密。

在 Windows 世界中，该过程略有不同，但结果仍然相同。由于 Windows 没有不同的 shell 选项，所有 SSH 用户都将被赋予一个命令提示符（cmd.exe）或命令提示符的某种形式。与 Unix 世界类似，Windows 中的 SSH 服务使用现有的密码数据库（SAM 或 ntds.dit 文件）进行认证。

### 远程文件传输

远程文件传输类似于远程命令行执行。SSH 提供了从远程实体获取和发送文件的功能。在 Unix 世界中，远程文件传输实际上有两种形式。SSH 在一些 SSH1 和 SSH2 的安装中提供安全复制协议（SCP），在大多数 SSH2 的安装中提供安全文件传输协议（SFTP）。在 Windows 世界中，只有 SFTP 存在。SCP 和 SFTP 提供相似（甚至相同）的功能，即以安全方式从远程实体发送和接收文件。SFTP 在 Unix 上使用现有的 SSH 守护程序，在 Windows 上使用现有的 SSH 服务。启用安全文件传输不需要额外步骤；在大多数 SSH2 版本中自动启用。许多 SSH 客户端也附带了 SCP 或 SFTP 客户端；因此，使用并执行这些附加功能非常直接。此外，还有一些专门的 SCP/SFTP 客户端，例如在第 3 章中讨论的 PuTTY。但许多 SSH 客户端的安装都包含某种文件传输工具。

与前文所述的 Telnet 会话类似，大多数 SCP 或 SFTP 安装都能抵御 FTP 明文通信的弱点。图 1.3 展示了两个实体之间以明文传输的 FTP 数据包。

```
220 Microsoft FTP Service
USER kusum
331 Password required for kusum.
PASS divyedi
```

![](img/c99d6f526a5f9fa62f2c34daada85ad7_36_0.png)

