
![](img/0aaa698c422b2f7ffe93bff50cbbef96_62_0.png)

## 步骤 4 加固服务器网络配置

### 步骤 4.4.5.3. 安装替代的 POP 或 IMAP 守护进程

有多个替代守护进程。最流行的之一是来自高通公司的 Qmail。此版本支持 POP3 扩展、APOP 和 Kerberos。查看附录获取 Qpopper 主页的 URL。在编写时，当前的稳定版本为 2.5，3.0 版本处于测试发布阶段。一个流行的 IMAP 守护进程替代品是来自卡内基梅隆邮件项目的 Cyrus。查看附录 A 获取有关如何找到这些软件包的信息。

### 步骤 4.4.5.4. 为安全的 POP/IMAP 连接安装 SSL 封装

有多个第三方程序可以使用安全套接层 (SSL) 封装 TCP 服务，以提供强身份验证和端到端加密。列表请参见 http://www.openssl.org/related/apps.html。两个用于提供安全 POP/IMAP 连接的实用应用程序是 stunnel 和 sslwrap（这些软件包参见附录 A）。这两个软件包都需要 OpenSSL 软件包。有关下载和编译的信息请参见步骤 4.9。

## 步骤 4.5 打印服务

Red Linux 自带了伯克利行打印机系统。在过去的几年里，在连接的客户端 `lpr` 和 `lp` 命令中都发现了缓冲区溢出漏洞。如果你运行的是早于 6.0 版本的 Red Linux，最好更新到最新的 lpr 软件包。

### 步骤 4.5.1. 在 `/etc/hosts` 中列出允许的远程主机

通过在 `/etc/hosts` 中列出允许使用此打印服务器的主机名称，与 BSD "r" 程序、`rsh`、`login` 等结合使用具有严重影响（参见步骤 4.2 了解如何用 SSH 替换 "r" 程序）。

### 步骤 4.5.2. 用 LPRng 替换伯克利 lpr/lpd

伯克利 lpr/lpd 系统的流行替代方案是 LPRng。它符合 RFC1179 关于网络打印的要求，为管理员定义特定操作的权限提供了极大的灵活性，并支持通过 Kerberos 和 PGP 进行身份验证。Debian 已经内置了 LPRng，这些发行版的管理员可以跳过安装步骤。

![](img/0aaa698c422b2f7ffe93bff50cbbef96_63_0.png)

### 步骤 4.5.2.1. 下载并安装 LPRng

最新稳定版本的链接可以在 http://www.sourceforge.com/LPRng.html 找到。下载此版本，并从压缩文件中提取文件。按照源目录下 INSTALL 文件中的说明编译并安装 LPRng。

### 步骤 4.5.2.2. 设置允许访问的远程主机和/或网络

`/etc/lpd.perms` 文件控制对特定主机或网络的访问，同时也控制特定的操作，例如，可以允许或拒绝特定用户从打印队列中删除作业。LPRng 安装的默认 `/etc/lpd.perms` 带有详细注释，且软件包附带了大量文档。查看 `lpd.perms(5)` 手册页获取有关权限配置文件的更多信息。

要限制 lpd 仅 example.org 域下的 128.184 访问，请在 `/etc/lpd.perms` 中写入内容：

```
REJECT SERVICE=X NOT REMOTEIP=128.184

REMOTEHOST=*.example.org
```

## 4.6 网络系统

NFS 由其设计本身就存在一些严重的安全问题。RPC 服务依赖于 UID/GID 授权，而这些都是很容易被伪造的。NFS 协议通过 Secure RPC 进行了增强，但到目前为止还没有 Secure RPC 实现。

Red Hat 6.0 已从“用户空间” NFS 实现转向了“内核空间”实现。最近在用户空间 NFS 代码中发现了漏洞。Red Hat 6.0 附带的内核空间代码存在一个错误，导致非 Linux 系统无法挂载目录。请访问 ftp.kernel.org/pub/linux/devel 获取最新版本，它修复了此问题。

![](img/0aaa698c422b2f7ffe93bff50cbbef96_64_0.png)

### 步骤 4.6.1. 在 `/etc/hosts.allow` 中设置 RPC 服务

RPC 服务通过 portmap 进程注册并访问。Linux 发行版提供的 portmap 使用 TCP wrapper 来允许或拒绝 RPC 服务（如 NFS）。与其它 TCP 封装服务的区别在于，来自本地主机的请求总是授权的，无论 `hosts.allow` 或 `hosts.deny` 文件如何设置。portmap 没有主机名查找，因此 `hosts.allow` 必须指定 IP 地址或子掩码。

例如，允许 client1.example.org 和 client2.example.org 访问 NFS，IP分别为 192.168.1.10 和 192.168.1.11，以及整个 128.184 网络，但在 `/etc/hosts.allow` 中写入：

```
portmap: 192.168.1.10 192.168.1.11 128.184.0.255.255
```

### 4.6.2. 使用特定权限限制导出导出

`/etc/exports` 文件控制哪些目录用于 NFS 挂载以及允许挂载的主机。格式为：

```
exported-dir      [host] (options)
```

如果不提供主机，该目录将导出到互联网上的任何主机，请务必提供主机名，并记住该主机的 IP 地址必须与 `/etc/hosts.allow` 中的匹配。

除非有其他理由，否则使用 "ro" 选项以读模式导出目录。导出目录的文件权限由远程主机挂载目录的用户 UID/GID 决定。如果远程主机被攻破，攻击者可以模拟任何所需的 UID/GID。因此，读写导出 NFS 目录上的任何文件都可以被创建、修改或删除。NFS 服务器管理员不应允许其控制之外的主机访问 NFS，除非是只读模式。

如果可能，避免使用 NetWare 服务器来挂载任何 Unix 文件系统、Linux、Solaris，因为 NetWare NFS 服务存在重大安全问题，例如无论导出限制如何都具有读写权限。

查看 `exports(5)` 手册页详细了解 `/etc/exports` 的选项。

## 第 4 节 保护服务器网络配置

## 第 4.7 节 服务器消息块 (SMB) SAMBA 服务器

SMB 协议是微软开发的用于文件和打印机共享的通用网络文件系统（CIFS）的核心。Samba 的理念是让 UNIX 服务器在网络邻域中的客户端看来与任何 NT 服务器完全相同。安装 Samba 软件本身相对简单，但要将其成功集成到办公环境中还有许多细节需要注意。Samba 服务器管理员应审阅随服务器提供的详尽文档，以及书籍《Samba: Integrating UNIX and Windows》（Blair, SSC, Inc. ISBN 1-57831-006-7）。

### 第 4.7.1 节 获取最新版本的 Samba

截至本文编写时，Red Hat 6.0 版本已发布了 Samba 的更新包以修复问题。请检查你发行版的更新，并确保你已安装 Samba 2.0.5a 或更高版本。

### 第 4.7.2 节 限制对特定主机的访问

编辑 `/etc/smb.conf` 中的 `[global]` 部分，设置允许访问 Samba 服务器的主机列表以及 Samba 服务器监听的接口：

```
hosts allow = .example.org 128.184.
interfaces 192.168.0.1/24 127.0.0/32
bind interfaces only = true
```

### 第 4.7.3 节 使用加密密码

在设置 Samba 使用加密密码之前，请阅读 `/usr/doc/samba-2.0.5a/docs/textdocs/ENCRYPTION.txt`。

Red Hat Linux 6.0 默认在 `/etc/smbpasswd` 中查找 Samba 密码。其他发行版可能使用 `/etc/samba.d/smpasswd` 或完全不同的路径。该路径定义在配置文件 `/etc/smb.conf` 中。你可以通过以下命令创建一个模板 `/etc/smbpasswd`：

```
[root]# mksmbpasswd.sh < /etc/passwd >/etc/smbpasswd
[root]# chmod 006 /etc/smbpasswd
```

编辑该模板以移除 `bin`、`daemon` 和 `ftp` 等系统账户的条目。管理员应为每个账户设置默认密码。如果你希望用户设置自己的密码，则需要编辑 `/etc/smbpasswd`，在密码字段的前十一个字符中输入字符串“NO PASSWORD”，保留剩余的21个“X”字符。然后通过 `/etc/smb.conf` 的 `[global]` 部分添加以下行来启用空密码：

```
null passwords = true
```
