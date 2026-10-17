
### default gateway（默认网关）
在 IP 网络中，默认网关是连接此网络与外部世界的路由器。每台计算机都需要配置默认网关；否则数据包无法发送到外部网络。

### dentry cache（目录项缓存）
这是内核内存中的一个区域，用于缓存目录项。查找文件和目录需要这些项。在读取大量内容的系统中，`dentry`缓存会相对较高。

### dig
`Dig`是一个可以查询 DNS 名称的实用。

### Domain Name System (DNS)（域名系统）
`DNS`允许网络用户使用易记的名字而不是难以记忆的 IP 地址。每台计算机都需要配置至少一个 DNS 服务器。

### Dynamic Host Configuration Protocol (DHCP)（动态主机主机配置协议）
`DHCP`是一种用于为网络上的计算机提供 IP 地址和其他 IP 信息的协议。

### inode
`inode`包含了文件的完整管理信息。事实上，文件就是`inode`。实际上，为了方便起见，我们为文件分配了名称。内核本身通过`inode`节点工作。使用 `ls -s -i` 可以找到特定文件的`inode`节点。

### insert mode
插入模式在编辑器中，插入模式是可以输入文本的模式。这与命令模式相反，命令模式是输入命令的模式，例如保存文档的命令。

### Inter-Process Communication (IPC)
进程间通信是指直接发生在进程之间的通信。内核分配套接字（`sockets`）和命名管道（`named pipes`）以允许 IPC 发生。

### internal command
内置命令是`shell`二进制文件文件的一部分。它在磁盘上无法找到，但当`shell`加载时会被加载。

### IP masquerading
IP 伪装（IP 伪装）是一种技术，在网络公侧使用已注册的 IP 地址，而在网络私侧使用不可路由的私有 IP 地址。IP 伪装用于将这些私有 IP 地址翻译为公共 IP 地址，允许所有私有地址连接到互联网。

### iSCSI
`iSCSI`是通过 IP 发送 SCSI 命令的协议。它是实现共享存储的常用方案，这在高可用性集群中通常是需要的。

## Glossary 术语表

### kdump
`Kdump`是内核的一个特殊版本，当内核崩溃时会加载。在 Linux 中，`Kdump`会获取内存转储并确保将其写入磁盘。

### key distribution center (KDC)
密钥中心 (`KDC`) 用于 Kerberos 持票据。身份验证成功后，`KDC`允许客户端连接到 Kerberos 创建的服务之一。

### key transfer
密钥传输 密钥传输是传输密钥的过程。这通常通过使用公钥/私钥完成。

### key-based authentication
基于密钥的身份验证是一种交换密码的解决方案。然而，身份验证通过用户使用特殊密钥证明其身份，该密钥对 SSH 环境也是公开的。

### keyring
密钥环在 GPG 加密中，密钥环是用户收集的所有密钥的集合，包括其他用户的密钥以及用户所属的密钥。

### kickstart file
`kickstart`文件包含自动安装服务器所需的所有答案。

### LDAP Input Format (LDIF)
`LDIF`是在 LDAP 目录中输入信息的默认格式。

### leaf-entries
在 LDAP 中，叶子节点（`leaf entry`）是指自身不能包含任何条目的节点。这与容器节点（`container entry`）相反，后者用于在 LDAP 数据库中创建结构。

### library
库是一个包含共享代码的文件。库用于使编程更高效。通用代码包含在库中，程序文件需要链接这些库。

### Libvirt
`Libvirt`是一个用于管理虚拟化环境的通用接口。`KVM Virtual Machine Manager`等常用工具使用它来管理 Red Hat Enterprise Linux 中的虚拟化。

### Lightweight Directory Access Protocol (LDAP)
`LDAP`是一种目录服务，用于存储大型环境中所需的项目，因为 LDAP 比扁平化身份验证灵活得多。参见硬链接（`hard link`）和软链接（`soft link`）。

### load average
平均负载 平均负载是服务器上的平均工作负载。对于性能优化，了解服务器共同的平均负载是非常重要的。

### load balancing
负载均衡 负载均衡是一种用于在不同物理服务器之间分配工作负载的技术。这种技术通常与高可用集群结合使用，以确保高负载得到高效处理。

### log target
日志目标 在 `syslog` 中，日志目标定义了日志消息发送的位置。这可以是多个目的地，例如文件、控制台或远程日志服务器。

### logical operators
逻辑运算符 逻辑运算符用于 Bash 脚本，根据之前执行命令的结果来执行命令。有两种逻辑运算符：`a || b` 仅在 `a` 未成功完成时才执行 `b`，`a && b` 仅在 `a` 执行成功时执行 `b`。

### Logical Volume Manager (LVM)
逻辑卷管理器 逻辑卷是组织磁盘存储的灵活方法。与使用分区相比它们具有优势，例如，增加或减少逻辑卷的大小比分区要容易得多。

### Linux Unified Key Setup (LUKS)
`LUKS`是一种用于创建加密磁盘和卷的方法。`LUKS`增加了一层安全性，并确保当设备连接到另一台机器时，如果不输入正确的短语，就无法访问设备上的数据。

### management interface for high-availability clusters
高可用集群管理接口。作为集群解决方案的一部分，它探测集群节点上的代理（`agents`）并与它们交换信息。

### mail exchange (MX)
邮件交换 邮件交换是负责处理特定 DNS 域名电子邮件的邮件服务器。

### mail queue
邮件队列 电子邮件首先被放在邮件队列中。从那里，它会被邮件进程拾取并发送到目的地。有时消息会“挂起”在队列中。如果发生这种情况，刷新队列或等待邮件服务器进程尝试发送消息会有帮助。

### mail user agent (MUA)
邮件代理 (`MUA`) 是用于发送和读取电子邮件消息的用户程序。

### master name server
主名称服务器主 DNS 名称服务器（也称为主名称服务器）是负责 DNS 域名中资源记录的服务器。它与从或辅助 DNS 名称服务器通信，以同步数据实现冗余。

### memory over-allocation
内存过度分配 内存过度分配是指进程声称比实际使用的更多的内存，以防以后可能需要。已声明但未使用的内存总量称为虚拟内存。

### message delivery agent (MDA)
消息投递代理 `MDA` 是邮件服务器的一部分，确保消息在被消息传输代理接收后被投递到终端用户的邮箱箱中。

### message transfer agent (MTA)
消息传输代理 `MTA` 是邮件服务器的一部分，负责将消息发送到收件人的的邮件服务器。为了找到该邮件服务器，它使用 DNS 中的 MX 记录。

### meta package handler
元包处理器 元包处理器是一种使用存储库解决 RPM 软件包依赖问题的解决方案。在 Red Hat Enterprise Linux 中，`yum`工具被用作元包处理器。

### mkfs utility
`mkfs`工具 `mkfs`工具用于在存储设备上创建文件系统，设备可以是分区或 LVM 逻辑卷。此过程在其他系统中被称为格式化。

### module
模块模块是可以轻松包含在更大的软件框架中的软件片段。模块被不同的解决方案使用。Linux 内核和 Apache 服务器可能是最好的例子。

### mounting
挂载是将存储设备连接到目录的过程。一旦挂载，用户就可以访问设备上的数据。

### name servers
名称服务器（DNS 名称服务器）是联系的服务器将 DNS 名称（如 `www.example.com`）转换为 IP 地址（通过 IP 网络通信所需的地址）。每个客户端都需要配置至少一个 DNS 服务器的 IP 地址。

### ncurses
`ncurses`是菜单式界面的通用泛指。在 Red Hat Linux 中，有一些菜单式界面适用于配置不运行图形界面的服务器。

### network service
网络服务用于管理网络接口。

### Neighbor Discovery Protocol (NDP)
邻居发现协议 (`NDP`) `NDP`是一种用于 IPv6 的协议，用于发现使用 IPv6 的其他节点。根据这些信息，节点可以发现自己处于哪个 IPv6 网络，并添加其 MAC 地址以配置其使用的 IPv6 地址。

### Netfilter
`Netfilter`是 Linux 中使用的内核级防火墙。要配置 `Netfilter`，管理员使用 `iptables`命令或系统防火墙菜单式界面。

### Network Address Translation (NAT)
网络地址转换 (`NAT`) `NAT`是一种用于隐藏私有网络内部节点的解决方案。这些节点使用 NAT 路由器或防火墙的公共 IP 地址访问外部服务器。因此，外部服务器无法在没有直接请求的情况下发送回复。

### Network Manager Service
网络管理器服务是一种简化管理 IP 地址的服务。它监控 IP 配置文件并立即对这些文件进行更改。它还使用图形界面让管理员更容易管理 IP 地址和相关信息。
