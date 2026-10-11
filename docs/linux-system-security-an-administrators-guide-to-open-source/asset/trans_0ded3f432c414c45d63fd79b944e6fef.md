
如果服务是通过 `inetd` 调用的，你需要注释掉或移除 `/etc/inetd.conf` 中相应的条目，然后通知 `inetd` 你所做的更改。例如，假设你要禁止来自所有客户端的 *rlogin* 请求。编辑 `/etc/inetd.conf` 文件并更改条目

```
login stream tcp nowait root /usr/sbin/tcpd in.rlogind
```

只需在行首添加 `#` 注释字符，将其更改为以下内容：

```
#login stream tcp nowait root /usr/sbin/tcpd in.rlogind
```

然后通过执行以下命令来通知 `inetd` 这一更改：

```
# killall -HUP inetd
```

现在，`inetd` 将拒绝所有针对支持 *rlogin* 客户端程序的 `in.rlogind` 的请求。

某些服务存在大量漏洞。表 3.1 列出了许多可用的服务，并建议是否应使它们可用。它还列出了默认状态（开或关）以及与之关联的端口号。

### 表 3.1 标准服务和推荐用法

| 服务 | 状态/端口 | 功能描述 | 推荐用法 |
| --- | --- | --- | --- |
| chargen | 关/19 | 生成 ASCII 数据用于调试目的。 | 保持关闭。 |
| daytime | 关/13 | 以 ASCII 格式提供日期和时间。 | 通常不需要。保持关闭。 |
| discard | 关/9 | 丢弃接收到的任何数据。用于调试。 | 保持关闭。 |
| echo | 关/7 | 回显所有接收到的数据。用于调试。 | 保持关闭。 |
| ftp | 开/21 | 用于通过网络传输文件的文件传输协议。 | 通常是一项必需的服务。 |
| gopher | 开/70 | 基于命令行的 Web 浏览器前身。 | 通常不使用。关闭它。 |
| smtp | 关/25 | 简单邮件传输协议 | POP 必需；否则保持关闭。 |
| nntp | 关/119 | 网络新闻传输协议 | 仅当系统将成为网络新闻服务器时才必需。 |
| shell | 开/514 | 支持远程 shell 服务。 | 关闭它。替换为 sshd。 |
| login | 开/513 | 支持远程登录服务。 | 关闭它。替换为 sshd。 |
| exec | 关/512 | 通过 rexec 支持远程命令执行。 | 保持关闭。 |
| talk ntalk | 开/517 开/518 | 提供基于文本的交互式通信。 | 关闭它们。使用 Internet 中继聊天 (IRC) 或电子邮件。 |
| imap | 开/143 | Internet 邮件访问协议邮件服务。 | 除非系统是 IMAP 服务器，否则关闭它。 |
| pop-2 pop-3 | 开/109 开/110 | 提供邮局协议 (POP) 邮件服务。 | 除非系统是 POPv2 或 POPv3 邮件服务器，否则关闭这些服务。 |
| uucp | 关/117 | UNIX-to-UNIX 复制提供面向批处理和本地需求的文件传输服务。 | 除非系统必须提供 uucp 服务，否则关闭它。 |
| tftp | 关/69 | 平凡文件传输协议。ftp 的简化版本，不执行任何身份验证检查。 | 仅用于将作为安装服务器或无盘客户端服务器的系统。 |
| bootps | 关/67 | 为网络客户端（如 X 终端和无盘节点）提供启动服务。 | 仅用于将作为启动服务器的系统。 |
| finger | 开/79 | 提供用户信息。 | 除非特别配置用于 DMZ 操作，否则关闭它。 |
| systat | 关/11 | 通过 ps 提供系统信息。 | 保持关闭。 |
| netstat | 关/15 | 通过 netstat 提供网络统计数据。 | 保持关闭。 |
| time | 开/37 | 通过远程执行 rdate 或 ntp 等命令用于主机时间同步。 | 这可能对于主机时钟同步是必要的。 |
| auth | 开/113 | 提供连接所有权信息。 | 通常，对于连接到 Internet 的系统，此服务是开启的。 |
| linuxconf | 开/98 | 通过网络提供系统管理图形用户界面 (GUI)。 | 除非绝对必要，否则关闭它。 |
| portmap | 开/111 | 不受 inetd 控制。 | 用于远程过程调用 (RPC) 服务。通常必要。在 *Remote Procedure Call Applications*（第 36 页）中进一步讨论。 |
| mountd | 开/635 | 不受 inetd 控制。 | NFS 服务必需。第 15 章讨论的 CFS 和 TDFS 也需要它。如果你不使用其中任何服务，请关闭它。 |

如果你对 `inetd` 不熟悉，你至少必须阅读第 39 页 *General TCP/IP Networking Resources* 中引用的 *TCP/IP Network Administration*。为了更深入的理解，请查阅该部分中列出的其他参考资源。

### 远程过程调用应用

有许多服务，包括 NFS 和网络信息服务 (NIS)（参见第 37 页的 *Some Major Applications*），使用远程过程调用 (RPC) 来管理通信，包括端口使用。RPC 应用通过 portmap 守护进程（在第 10 章中讨论）调用。portmap 守护进程将为请求的服务提供一个端口号，该号码将在整个通信期间使用。与本章中的其他主题一样，RPC 是一个你应该熟悉的话题。如果你不熟悉，请查阅 *General TCP/IP Networking Resources*（第 39 页）中列出的某些资源。

### 受信任主机文件和相关命令

在本节中，我们将概述 `$HOME/.rhosts`、`/etc/hosts.equiv` 和 `$HOME/.netrc`（此处统称为受信任主机文件）的行为。这些文件是服务器端文件，与服务器端守护进程 `rlogind`、`in.rshd`、`in.rexecd` 和 `in.ftpd` 相关。相关的客户端应用程序是 `rlogin`、`rsh`、`rcp`、`ftp` 和 `rexec`（通常统称为 r-commands 或 Berkeley r-commands，因为它们源自 Berkeley 系统发行版 [BSD]）。表 3.2 提供了受信任主机文件及其应用程序关联的列表。

| 客户端应用程序 | 服务器端守护进程 | 服务器端受信任主机文件 |
| :--: | :--: | :--: |
| rlogin | in.rlogind | /etc/hosts.equiv<br>`$HOME/.rhosts` |
| rsh | in.rshd | /etc/hosts.equiv<br>`$HOME/.rhosts` |
| rcp | in.rshd | /etc/hosts.equiv<br>`$HOME/.rhosts` |
| ftp | in.ftpd | `$HOME/.netrc` |
| rexec | in.rexecd | `$HOME/.netrc` |

6. Shell 环境变量 HOME 包含用户的家目录。

`/etc/hosts.equiv` 文件为非 root 用户提供身份验证数据库。`$HOME/.rhosts` 和 `$HOME/.netrc` 文件为居住在其家目录中的用户提供身份验证数据库。这些文件的目的是提供无需密码的用户身份验证。

`$HOME/.netrc` 文件的语法记录在 `tcp(1)` 手册页中。`/etc/hosts.equiv` 和 `$HOME/.rhosts` 文件的语法记录在 *TCP/IP Network Administration* 等资源中，该资源在第 39 页的 *General TCP/IP Networking Resources* 中引用。额外的配置信息在 `in.rlogind(8)` 和 `in.rshd(8)` 手册页中提供。

由于受信任主机文件允许用户无密码登录，强烈不建议使用它们。如果你在网络中配置了受信任主机，那么一个系统的沦陷将导致所有信任该系统的系统沦陷。因此，r-commands 通常被称为邪恶的 r-commands。r-commands 的所有功能都应该并且可以被 SSH（在第 11 章中讨论）安全地替换。

## 一些主要应用

在这本书中，我们将讨论网络文件系统 (NFS)、Samba、网络信息服务 (NIS) 和域名服务 (DNS)，并与我们描述的各种实用程序相关联。

NFS 是由 Sun Microsystems, Inc. 开发的远程文件系统。它允许通过 TCP/IP 对远程目录进行透明的本地访问。不幸的是，截至内核版本 2.2.x，Linux 中尚未实现 NFS 的身份验证。服务器可以在 `/etc/exports` 中指定访问控制列表，并且已识别 UID 的使用可以被粉碎（禁止）。你应该始终在每个 NFS 资源上使用访问限制。有关更多详细信息，请参阅 `exports(5)`、`nfs(5)` 和 `mount(8)` 手册页。从安全角度来看，最好只允许在你的组织网络内访问 NFS，并允许来自 Internet（或其他公共网络）的传入 NFS 请求。这可以通过 `ipchains`（在第 16 章中讨论）或类似实用程序实现。有关更多信息，本节末尾引用了额外的参考资源。

Samba 在概念上类似于 NFS，只是它是在 Microsoft Networking 协议上实现的。Samba 1.9.17p2 及更高版本被认为相对安全。Samba 允许基于密码的身份验证，并且可以配置为在网络上传输哈希后的密码而不是明文密码。还可以使用访问控制列表进行配置。Samba 服务器可以被配置为在 chroot 环境中运行。确保你充分利用这些安全特性。

NIS 提供了一种机制，用于集中管理一组通过网络连接在一起的系统。NIS 在设计时没有考虑安全性；相反，它是为了方便而设计的。不要允许来自除专门参与你的 NIS 管理的网络以外的网络访问你的 NIS 数据库。通过 portmap 实现访问控制（参见第 10 章）。

