
## 授权：定义身份的访问权限 279

`LOCAL` 指向回环接口和未限定的主机名（名称中不包含点的主机名，即没有域名的主机名）。也就是说，主机名指的是与本地机器共享域名的机器。但请注意，`tcpd` 匹配 `/etc/hosts` 中的第一个名称。`LOCAL` 不匹配 `/etc/hosts` 中提供的以下可选字段。对于没有自己的本地域名的家用机器，防火墙机器将拥有由 ISP 分配的域名。内部局域网（LAN）机器将不是 `LOCAL`。它们将属于一个内部的私有域。

`PARANOID` 匹配任何名称与其地址不匹配的主机。`tcpd` 的默认模式是编译时对所有主机开启 `PARANOID` 检查。这意味着在查询访问控制列表之前，不匹配的主机将被拒绝访问被 TCP 封装的服务。如果在在关闭 `PARANOID` 的情况下重新编译了 `tcpd`，则可以使用 `PARANOID` 通配符来选择性地对个体应用 `PARANOID` 检查。

访问控制列表可以匹配模式。两种常见的模式是点后跟域名，以及以点结尾的网络地址。这两种模式都会匹配所匹配的域或网络中的任何主机。

以下是 `/etc/hosts.allow` 文件内容：

1. `LOCAL: .internal.lan`

2. `in: ftpd: friend@trusted.host.net`

3. `ssh: 10.30.27.`

4. `ipp3d: 10.30.27.45 EXCEPT PARANOID`

第 1 行允许从本地机器和内部局域网上的所有主机访问被 TCP 封装的服务。

第 2 行额外允许从远程用户账户访问 FTP 服务器。如果远程站点没有运行 `IDENT` 服务，则指定用户名将无效。如果远程机器是个人电脑、PC 或 Macintosh，指定用户名将无效。

第 3 行允许从远程 `10.30.27.0` 网络上的任何主机访问 SSH 服务器。

第 4 行允许从远程 IP 地址访问 POP 服务器。如果你在没有全局启用 `PARANOID` 功能的情况下重新编译了 `tcpd`，那么 `PARANOID` 异常将为此项访问规则启用该功能。第 4 行表示允许从 IP 地址到 POP 服务器的连接。

# 282 第 7 章 UNIX 系统管理层面的问题

文件系统的受限虚拟视图是在所定义的任何服务器特定访问限制之上的额外的一层额外的安全保护。

在 `chroot` 环境中运行的服务可能需要复制 `chroot` 环境之外的其他文件系统部分。例如，`ftp` 使用 `ls` 命令允许用户查看当前 `ftp` 目录的目录列表。在 `chroot` 环境中，这些二进制文件位于 `chroot` 目录之外，因此必须在 `chroot` 目录结构内复制这些二进制文件。系统配置文件、共享库和服务器日志文件可能也需要在 `chroot` 目录结构内进行复制。有关 `chroot` 程序的更多信息，请参阅帮助页，`chroot(1)`。

## 服务器特定配置

无论是否使用防火墙，保护自己的最佳方法之一是只运行你需要的的服务。如果你不需要某个服务，请将其关闭。如果你需要某个特定服务，请注意服务器的配置设置。

本节将从安全角度查看各个服务器配置选项。

## Telnet 配置问题

不应向远程站点提供 Telnet 服务；如果你必须使用它访问远程站点，除非你没有其他选择。SSH 优于 Telnet。通过 `/etc/inetd.conf` 启用 `telnetd`。作为 Red Hat 分发的版本，`telnetd` 是一个 `tcpwrapped` 服务。通过防火墙配置和 `/etc/hosts.allow` 配置，限制外部主机对你的 `telnet` 服务器的访问。

当启动 `telnet` 会话时，在发送登录提示之前，`/etc/issue.net` 的内容会打印在客户端终端上。`/etc/issue.net` 包含了你不希望公开给任何探测你 `telnet` 端口的身份信息。`/etc/issue.net` 的细节将在本章稍后讨论。

在 `telnet` 方面，可以将服务器配置为完全不打印系统信息，忽略 `/etc/issue.net` 并仅打印登录提示。通过带有 `-n` 选项启动服务器，将忽略 `/etc/issue.net`。可以通过编辑 `/etc/inetd.conf` 并将 `telnet` 条目更改为读取来配置 `telnet` 服务器：

```
telnet stream top nowait root /usr/sbin/tcpd in.telnet -h
```

## SSH 配置问题

`SSH` 是 `telnet` 和 `login` 等程序的第三方替代品。`SSH` 会话不仅是加密的，而且加密从初始连接建立时就开始，在用户被提示密码之前。`SSH` 既作为非商业用途的免费软件包提供，也作为功能更全面的商业产品。有关 `SSH` 的信息可以在芬兰的 SSH Communications Security 找到。其网站为 http://www.ssh.fi/。`SSH` 的非商业版本以源代码形式分发，你必须在自己的系统中进行编译。官方源码仓库位于 `ftp://cs.net.fi/pub/ssh`。原始的 1 版本和新版本 2 均可用。

`ssh` 守护进程通常作为独立的后台进程启动，而不是像 `inetd` 那样按需启动。SSH Communications Security 解释，对于大于 512 位的主机密钥（768 位是默认主机密钥大小），RSA 主机加密密钥交换的时间可能比 `inetd` 的超时时间长。由于服务器通常从 `/etc/inetd.conf` 封装，`SSH` 在编写时内置了对 `top_wrappers` 的支持。

编译并安装原始 `SSH1` 版本 `1.2.26` 源码或较新的、重写的 `SSH2` 版本 `2.0.13` 源码的方法如下：

```
/config -with-libwrap
make all
make install
```

对于 `SSH1`，编辑服务器配置文件 `/etc/ssh_config` 和客户端配置文件 `/etc/ssh_config` 以适应你的需求。对于包含你预期共享连接的主机的域名的 RSA 密钥：

```
make-ssh-known-hosts <domain>
```

然后，为了在启动时自动启动 `ssh` 守护进程，编辑 `/etc/rc.d/rc.local` 并添加以下行：

```
/usr/local/sbin/sshd
```

对于 `SSH2`，编辑服务器配置文件 `/etc/ssh2/sshd2_config` 和客户端配置文件 `/etc/ssh2/sshd2_config` 以适应你的需求。在安装过程中自动创建了 RSA 密钥。

然后，为了在启动时自动启动 `ssh2` 守护进程，编辑 `/etc/rc.d/rc.local` 并添加：

```
/usr/local/sbin/sshd
```

关于 `ssh` 使用的更多信息，请查看帮助页 `ssh(1)`、`sshd(8)`、`keygen(1)` 以及 `ssh2(1)`、`sshd2(8)`、`keygen(1)`。

## SMTP 配置问题

邮件服务器具有很长的漏洞利用历史，包括 `smtp` 和 `sendmail`，以及邮件投递代理 `pop` 和 `imap`。仔细控制对这些服务器的远程访问可以为这些服务提供极大帮助。已经做了大量工作使当前的邮件服务器 `sendmail` 尽可能安全。Red Hat Linux 6.0 分发的 `sendmail` 版本为 `8.9.3`，是较新版本之一。

然而，`sendmail` 的潜在问题在于允许远程主机通过本地服务器中继时的本地配置。对于我们来说，`sendmail` 的默认 Linux 配置是安全的。单系统站点不需要对 `sendmail` 配置做任何操作。

为 LAN 提供邮件服务的系统需要为 LAN 主机启用中继。否则，你的邮件服务器将接受来自本地机器的发送邮件。特定主机在两个文件 `/etc/mail/access` 或 `/etc/mail/relay-domains` 中启用中继。小型 LAN 的 `/etc/mail/access` 示例可能包含：

| localhost.localdomain | RELAY |

| localhost | RELAY |

| windows.private.lan | RELAY |

| linux2.private.lan | RELAY |

| macintosh.private.lan | RELAY |

`/etc/mail` 中的配置文件是文件对，一个 ASCII 文件和一个从 ASCII 文件创建的哈希数据库文件。在编辑一个 ASCII 文件后，其哈希副本需要更新。以下命令更新 `/etc/mail/access` 哈希表 `/etc/mail/access.db`：

```
makemap /etc/mail/access
```

关于 `sendmail` 配置的附加信息可以在帮助页找到：`sendmail(8)`、`aliases(5)` 和 `newaliases(1)`。

## 286 第 7 章 UNIX 系统管理层面的问题

对于运行本地 `named` 服务器的系统，单条 `nameserver` 指令将指向本地机器。`resolv.conf` 的一个示例可能包含：

```
domain my.isp.net
nameserver 127.0.0.1
```
