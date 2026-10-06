
> 虽然 `sshd` 服务本质上是安全的，但必须保持服务更新以防止安全威胁。请参阅第 1.5 节“安全更新”获取更多信息。

`GPG` 是确保电子邮件通信的一种方法。它可以既用于在公网通过电子邮件发送敏感数据，也可用于保护硬盘上的敏感数据。

## 2.2. 服务器安全

当系统在公共网络上作为服务器使用时，就会成为攻击目标。对于系统管理员来说，加固系统和锁定服务至关重要。

在深入特定问题之前，查看以下增强服务器安全性的通用建议：

- 保持所有服务更新，以防止最新的威胁。
- 尽可能使用安全协议。
- 尽可能每台机器仅提供一种类型的网络服务。
- 仔细监控所有服务器的可疑活动。

## 2.2.1. 使用 TCP Wrappers 和 xinetd 保护服务

`TCP Wrappers` 为各种网络服务提供访问控制。大多数现代网络服务（如 `SSH`、`Telnet` 和 `FTP`）都使用 `TCP Wrappers`，它在入站请求和请求的服务之间进行守卫。

当 `TCP Wrappers` 与 `xinetd` 配合使用时，其提供的优势会增强，`xinetd` 是一个超级服务器，提供额外的访问、日志、绑定、重定向和资源利用控制。

> 将 `iptables` 防火墙规则与 `TCP Wrappers` 和 `xinetd` 结合使用以创建服务访问控制的冗余是一个好主意。请参阅第 2.8 节“防火墙”获取有关使用 `iptables` 命令实现防火墙的更多信息。

以下子节假设对每个主题均有基础知识，并关注特定的安全选项。

### 2.2.1.1. 使用 TCP Wrappers 增强安全性

`TCP Wrappers` 的功能不仅限于拒绝访问服务。本节说明了如何使用它们发送连接横幅（banners）、警告来自特定主机的攻击以及增强日志功能。请参考 `hosts_options` 手页获取相关信息。

#### 2.2.1.1.1. TCP Wrappers 和连接横幅

在用户连接时显示合适的横幅是让攻击者知道系统保持警惕的好方法。在本示例中使用 `banner` 选项。为了实现这一点，在 `/etc/` 创建一个文件，内容如下：

```
Hello, %c
不当的使用将导致您的访问被移除。
```

`%c` 令牌提供主机名或 IP 地址。为了在入站连接时显示此横幅，在 `/etc/hosts.allow` 中添加以下行：

```
vsftpd : ALL :
```

#### 2.2.1.1.2. TCP Wrappers 和攻击警告

如果检测到特定主机或网络正在攻击服务器，可以使用 `TCP Wrappers` 警告管理员。在本示例中，检测到来自 `206.182.68/24` 的破解者。在 `/etc/hosts.deny` 中放置以下行：

```
ALL : spawn /bin/date %d >> /var/log/intruder_alert
```

`%d` 令牌提供攻击者尝试访问的服务名称。为了允许连接并进行记录，放置 `spawn` 指令

> 注意 由于 `spawn` 指令会执行任何 shell 命令，因此在特定客户端尝试连接时创建一个特殊脚本是一个好主意。

#### 2.2.1.1.3. TCP Wrappers 和增强日志

如果某些类型的连接比其他类型更关注，可以使用 `severity` 选项提高日志级别。在本示例中，任何尝试连接到服务器端口 23（`Telnet` 端口）的人都是黑客。为了表示这一点，在日志文件中使用 `emerg` 标记 own默认标记 `info`。要这样做，在 `/etc/hosts.deny` 中放置以下行：

```
in.telnet : ALL : severity emerg
```

这使用了 `authpriv` 日志设施，但优先级从默认值 `info` 提高到 `emerg`，会将日志直接发布到控制台。

### 2.2.1.2. 使用 xinetd 增强安全性

本节重点介绍使用 `xinetd` 设置陷阱服务（trap service）并使用它控制任何 `xinetd` 服务可用的资源级别。为服务设置资源限制有助于防止拒绝服务 (`DoS`) 攻击。请参考 `xinetd` 和 `xinetd.conf` 页面获取可用选项列表。

#### 2.2.1.2.1. 设置陷阱

`xinetd` 的一个重要功能是能够将主机添加到全局拒绝访问列表（`no_access` list）。列表上的主机在一段时间内或直到 `xinetd` 重启之前，被拒绝访问由 `xinetd` 管理的服务。您可以使用 `SENSOR` 属性来实现此功能。这是阻止尝试扫描服务器端口的主机的简单方法。

设置 `SENSOR` 的第一步是选择一个您不计划的服务。在本示例中，使用了 `Telnet`。

## 第 2 章 保护您的网络

编辑 `/etc/xinetd.d/telnet` 文件并将 `flags` 行更改为：

| `flags = SENSOR` |

添加以下行：

| `deny_time = 30` |

这将拒绝来自该主机在 30 分钟内对该端口发起的任何进一步连接尝试。`deny_time` 属性的其他可用值为 `FOREVER`（它将保持禁用状态直到 `xinetd` 重启）以及 `NEVER`（它允许连接并记录日志）。

最后，最后一行应为：

| `disable = no` |

这将启用陷阱（trap）本身。

虽然 `SENSOR` 是检测和停止来自不可信主机的连接的好方法，但它有两个缺点：

- 它对隐藏扫描（stealth scans）无效。
- 知道正在运行 `SENSOR` 的攻击者可以通过伪造其 IP 地址并连接到被禁端口，对特定主机发起拒绝服务攻击（DoS）。

#### 2.2.1.2.2. 控制服务器资源

`xinetd` 的另一个重要功能是能够对对其控制的服务设置资源限制。

它通过以下指令实现：

- `cps = <number_of_connections> <wait_period>` — 限制传入连接的速率。该指令接受两个参数：
  - `<number_of_connections>` — 每秒处理的连接数。如果传入连接的速率高于此值，服务将被临时禁用。默认值为五十 (50)。
  - `<wait_period>` — 在禁用后重新启用服务之前等待的秒数。默认间隔为十 (10) 秒。
- `instances = <number_of_connections>` — 指定允许访问服务的总连接数。该指令接受整数值或 `UNLIMITED`（无限制）。
- `per_source = <number_of_connections>` — 指定每个主机允许访问服务的连接数。该指令接受整数值或 `UNLIMITED`。
- `rlimit_as =` — 指定服务可以占据的内存地址空间大小，单位为千 KB 或 MB。该指令接受整数值或 `UNLIMITED`。
- `rlimit_cpu = <number_of_seconds>` — 指定服务占用 CPU 的时间，以秒为单位。该指令接受整数值或 `UNLIMITED`。

使用这些指令可以帮助防止单个 `xinetd` 服务导致系统过载，从而拒绝服务。

## 2.2.2. 保护 portmap

`portmap` 服务是用于 `NIS` 和 `NFS` 等 `RPC` 服务的动态端口守护进程。它具有脆弱的身份验证机制，并能够为其控制的服务分配广泛的端口。由于这些原因，它很难被保护。

> 注意
>
> 保护 `portmap` 仅影响 `NFSv2` 和 `NFSv3` 的实现，`NFSv4` 不再需要它。如果您计划实现 `NFSv2` 或 `NFSv3` 服务器，则需要 `portmap`，并且适用于以下章节。

如果运行 `RPC` 服务，请遵循以下基本规则。

### 2.2.2.1. 使用 TCP Wrappers 保护 portmap

使用 `TCP Wrappers` 限制哪些网络或主机可以访问 `portmap` 服务是非常重要的，因为它没有内置的身份验证形式。

此外，在限制访问服务时，仅使用 IP 地址。避免使用主机名，因为它们可能被 DNS 投毒或其他方法伪造。

### 2.2.2.2. 使用 iptables 保护 portmap

为了限制对 `portmap` 服务的访问，在服务器上添加 `iptables` 规则并限制对特定网络的访问是一个好主意。

以下是两个 `iptables` 命令示例。第一个允许来自 `192.168.0.0/24` 网络到端口 111（`portmap` 服务使用）的 TCP 连接。第二个允许来自本地主机（`localhost`）到相同端口的 TCP 连接。对于 Nautilus 使用的 `sg_fam` 服务是必要的。所有其他数据包将被丢弃。

```
iptables -A INPUT -p tcp -s 192.168.0.0/24 --dport 111 -j DROP
iptables -A INPUT -p tcp -s 127.0.0.1 --dport 111 -j ACCEPT
```

类似地限制 UDP 流量，请使用以下命令。

```
iptables -A INPUT -p udp -s 192.168.0.0/24 --dport 111 -j DROP
```

> 注意
>
> 关于使用防火墙的更多信息，请参考以下章节。

## 2.2.3. 保护 NIS

网络信息服务（`NIS`）是一种与 `portmap` 配合使用的服务。

### 2.2.3.1. 仔细规划网络

### 2.2.3.2. 使用密码域和主机名

### 2.2.3.3. 编辑 /var/securenets 文件

### 2.2.3.4. 分配静态端口并使用 iptables 规则

### 2.2.3.5. 使用 Kerberos 身份验证

## 第 2 章 保护你的网络

由于 `Kerberos` 使用密钥加密法，网络上永远不会传输任何密码哈希值，这使得系统安全得多。有关 `Kerberos` 的更多信息，请参阅第 2.6 节“`Kerberos`”。

## 2.2.4. 保护 NFS

![](img/41d4f31e0edc30c079027fe8eaac3a44_55_0.png)

> > 注意
>
> Fedora 中包含的 `NFS` 版本（`NFSv4`）不再需要第 2.2.2 节“保护 Portmap”所述的 `portmap` 服务。`NFS` 流量现在所有版本中都使用 TCP 而不是 UDP。在使用 `NFSv4` 时，`NFSv4` 包含了 `Kerberos` 用户和组认证，这是 `RPCSEC_GSS` 内核模块的一部分。由于 Fedora 支持 `NFSv2` 和 `NFSv3`（这两者都利用 `portmap`），因此仍然保留了关于 `portmap` 的信息。

### 2.2.4.1. 仔细规划网络

现在 `NFS` 已经能够通过 `Kerberos` 在网络上传递所有文件信息，如果存在防火墙或位于分段网络，正确配置服务至关重要。`NFSv2` 和 `NFSv3` 仍然不安全地传输数据，应当被考虑在内。在所有这些方面进行仔细的网络设计可以防止安全泄露。

### 2.2.4.2. 警惕语法错误

`NFS` 服务器通过配置 `/etc/exports` 文件来确定要导出的文件系统以及导出这些目录的主机。编辑此文件时，注意不要添加多余的空格。

例如，`/etc/exports` 文件中的以下行将 `/tmp/nfs` 目录以读写权限共享给主机 `bob.example.com`。

```
/tmp/nfs bob.example.com(rw)
```

另一方面，`/etc/exports` 文件中的这一行由于在主机名后有一个空格字符，它将相同的目录以只读权限共享给主机 `bob.example.com`，并向所有人以读写权限共享。

```
/tmp/nfs bob.example.com (rw)
```

使用 `showmount` 命令检查任何配置的 `NFS` 共享是一个良好的习惯，用以验证共享了哪些内容：

```
showmount -e <hostname>
```

### 2.2.4.3. 不要使用 no_root_squash 选项

默认情况下，`NFS` 将 `root` 用户更改为 `nobody` 用户（一个无特用户账户）。这会将所有 `root` 创建的文件的所有者更改为 `nobody`，从而防止设置了 `setuid` 位的程序被上传。

如果使用了 `no_root_squash`，远程 `root` 用户将能够更改共享文件系统上的任何文件，并让应用程序感染木马，供其他用户无意中执行。

### 2.2.4.4. NFS 防火墙配置

用于 `NFS` 的端口由 `rpcbind` 动态分配，这在创建防火墙规则时可能会导致问题。为了简化此过程，使用 `/etc/sysconfig/nfs` 文件指定要使用的哪些端口：

- `MOUNT_PORT` — `mountd` (`rpc.mount`) 的 TCP 和 UDP 端口
- `STAT_PORT` — `status` (`rpc.statd`) 的 TCP 和 UDP 端口
- `LOCKD_TCPPORT` — `nlockmgr` (`rpc.lockd`) 的 TCP 端口
- `LOCKD_UDPPORT` — `nlockmgr` (`rpc.lockd`) 的 UDP 端口

指定的端口号不能被任何其他服务使用。配置防火墙以允许指定的端口号，以及 TCP 和 UDP 端口 2049 (`NFS`)。

在 `NFS` 服务器上运行 `rpcinfo -p` 命令以查看使用了哪些端口和 `RPC` 程序。

## 2.2.5. 保护 Apache HTTP Server

`Apache HTTP Server` 是 Fedora 附带的最稳定、安全的服务之一。有大量的选项和技术可以保护 `Apache HTTP Server` —— 多到无法深入研究。下节将介绍保护 `Apache HTTP Server` 的一些良好实践。

如果存在防火墙或位于分段网络，正确配置服务至关重要。在运行 `Apache HTTP Server` 之前，确保任何脚本都是安全的。在 `httpd/httpd.conf` 中配置以下选项，以 `root` 用户执行以下命令：

1. `chown <directory_name>`
2. `chmod 755 <directory_name>`

在 `/etc/httpd/httpd.conf` 中配置以下选项：

**FollowSymLinks**

该指令默认开启，在 Web 使用符号链接时要小心。

**Indexes**

该指令默认开启，在访问目录时可能需要它。

**UserDir**

该指令默认开启，在用户目录时可能需要它。

**Exec**

该指令默认关闭，除非绝对需要。

**SSI**

该指令默认关闭，除非绝对需要。

`Apache HTTP Server` 是 Fedora 附带的最稳定、安全的服务之一。有大量的选项和技术可以保护 `Apache HTTP Server` —— 多到无法深入研究。下节将介绍保护 `Apache HTTP Server` 的一些良好实践。在运行 `Apache HTTP Server` 之前，确保任何脚本都是安全的。在 `httpd/httpd.conf` 中配置以下选项，以 `root` 用户执行以下命令：

1. `chown <directory_name>`
2. `chmod 755 <directory_name>`

在 `/etc/httpd/httpd.conf` 中配置以下选项：

**FollowSymLinks**

该指令默认开启，在 Web 使用符号链接时要小心。

**Indexes**

该指令默认开启，在访问目录时可能需要它。

**UserDir**

该指令默认开启，在用户目录时可能需要它。

**Exec**

该指令默认关闭，除非绝对需要。

**SSI**

该指令默认关闭，除非绝对需要。

## 第 2 章 保护网络安全

## 2.2.6.3. 用户账户

由于 `FTP` 在不安全网络上通过未加密的用户名和密码进行身份验证，因此禁止系统用户通过其用户账户访问服务器是一个做法。

要禁用 **`vsftpd`** 中的所有用户账户，请在 `/etc/vsftpd/vsftpd.conf` 中添加以下指令：

```
local_enable=NO
```

### 2.2.6.3.1. 限制用户账户

要对特定帐户或账户组（例如 `root` 用户和具有 `sudo` 权限的用户）禁用 `FTP`，最简单的方法是使用第 2.1.4.2.4 节“使用 PAM 禁用 root”提到的 `PAM` 列表文件。`vsftpd` 的 `PAM` 配置文件为 `/etc/pam.d/vsftpd`。

也可以在每个服务内部禁用用户账户。

要禁用 **`vsftpd`** 中的用户账户，请将用户名添加到 `/etc/vsftpd.ftpsusers`。

## 2.2.6.4. 使用 TCP Wrappers 控制访问

按照第 2.2.1.1 节“使用 TCP Wrappers 增强安全性”所述，使用 `TCP Wrappers` 控制每个 `FTP` 守护程序的访问。

## 2.2.7. 保护 Sendmail

`Sendmail` 是一种邮件传输代理 (`MTA`)，使用简单邮件传输协议 (`SMTP`) 在 `MTA` 之间传递电子邮件，并传递给客户端或代理。`MTA` 能够加密彼此之间的流量，但大多数不能，因此在任何公共网络上发送电子邮件本质上是一种不安全的通信形式。

建议任何计划实现 `Sendmail` 服务器的人关注以下问题。

### 2.2.7.1. 限制拒绝服务攻击

由于电子邮件的特性，检测到的攻击者可以轻易向服务器填充邮件并导致拒绝服务。通过为 `/etc/sendmail.mc` 中的指令设置限制，可以限制此类攻击的有效性。

- **CONNECTION_RATE_THROTTLE** — 服务器每秒接收的连接数。默认情况下，`Sendmail` 不限制连接数。如果设置了限制并达到，后续连接将被拒绝。
- **MAX_DAEMON_CHILDREN** — 服务器可以创建的最大进程数量。默认情况下，`Sendmail` 不限制子进程数量。如果设置了限制并达到，后续连接将被拒绝。
- **MIN_FREE_BLOCKS** — 服务器接收邮件必须可用的最小空块数。默认为 100 块。
- **MAX_HEADERS_LENGTH** — 消息头的最大接受大小（字节）。
