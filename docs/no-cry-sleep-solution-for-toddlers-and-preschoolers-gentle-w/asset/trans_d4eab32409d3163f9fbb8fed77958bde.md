

然后从菜单项运行 KonCD。你也可以打开一个终端窗口并输入程序的名称。

## 安全配置

安装完 Linux 系统后，你应该采取一些基本的安全措施来保护系统免受外部攻击。与 Internet 相连的系统会面临外部用户试图获得未经授权访问的企图。这通常表现为以下几种形式：

- 试图入侵系统
- 入侵后，更改或替换系统文件为被篡改或损坏的版本
- 试图拦截来自远程用户的通信
- 更改或替换发送给用户或来自用户的消息
- 冒充合法用户

防火墙、入侵防护、加密、数据完整性和身份验证是抵御此类攻击的方式。

- 防火墙可防止任何直接的未经授权的访问尝试。
- 入侵检测会检查系统文件的状态，以查看是否已被入侵者篡改。
- 加密可保护授权远程用户的传输，提供隐私。
- 完整性检查例如修改摘要可保证消息和数据在传输途中未被拦截、更改或替换。
- 身份验证方法例如数字签名可以验证声称发送消息或访问系统的用户是否确实是该人。

## 安全服务

Red Hat 包含多个用于保护系统和网络传输的安全服务（见表 4-3）。使用 GNU Privacy Guard（GPG）你可以加密要发送的电子邮件消息或文件，同时还能用加密的数字签名对其进行签名，以证明消息确实由你发送（见第 16 章）。数字签名还包含加密的修改摘要信息，提供完整性检查，使收件人能够验证收到的消息是否为原始消息，而非被更改或替换过的消息。

网络安全的一个良好基础是设置 Linux 系统作为网络的防火墙，以保护其免受未经授权的访问（见第 19 章）。你可以使用防火墙实现数据包过滤或代理。数据包过滤只是决定防火墙主机接收到的包是否应转发到本地系统或网络的过程。目前使用的防火墙软件包是 Netfilter（iptables）。旧版发行版使用名为 ipchains 的早期版本。要实现防火墙，你只需提供一系列规则来管理系统上允许何种访问。如果该系统也是私有网络的网关，系统的防火墙功能可以有效地保护网络免受外部攻击。你可以使用 redhat-config-securitylevel 为自己的系统提供简单配置，如第 4 章所述。

| Applications | Description |
|---|---|
| GNU Privacy Guard (GPG) | Encryption and digital signatures (Chapter 16) www.gnupg.org |
| Netfilter (iptables) | Firewall packet filtering (Chapter 19) www.netfilter.org |
| Squid | Web proxy server (Chapter 23) www.squid-cache.org |
| Open-SSH | Secure Shell encryption and authentication for remote access (Chapter 18) www.openssh.org |
| Kerberos | User authentication for access to services (Chapter 18) web.mit.edu/kerberos/www/ |
| Pluggable Authorization Modules (PAM) | Authentication management and configuration (Chapter 28) |
| Shadow passwords | Password encryption (Chapter 28) |
| Lightweight Directory Access Protocol (LDAP) | User management and authorization (Chapter 28) www.openldap.org |
| authconfig-gtk | Red Hat tool to enable and configure authentication tools: Kerberos, LDAP, and shadow passwords |

### TABLE 4-3 Security Applications

外部用户也可能通过你可能托管的任何 Internet 服务，例如网站，来尝试获得未经授权的访问。在这种情况下，你可以设置代理来保护你的站点免受攻击。对于 Linux 系统，使用 Squid 代理软件设置代理来保护你的 Web 服务器（见第 20 章）。

进一步控制对系统的访问方法是提供使用加密密码的安全用户身份验证、Lightweight Directory Access Protocol（LDAP）服务以及 Pluggable Authentication Modules（PAM）（见第 28 章）。Kerberos 服务器可以进一步控制某些服务的用户身份验证（见第 18 章）。Kerberos 身份验证提供另一层安全保护，其中单个服务可以得到保护，仅允许已获授权访问的用户使用。LDAP 和 Kerberos 都可通过 authconfig-gtk 启用和配置（系统设置菜单或窗口中的身份验证）。

为了保护来自网络外部主机的远程连接，传输可以被加密。对于 Linux 系统，你可以使用 Secure Shell（SSH）套件程序加密任何传输，防止他人读取（见第 18 章）。SSH 程序旨在取代远程工具如 rsh 和 rcp（见第 15 章），这些工具不执行任何加密。

