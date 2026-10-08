
选项字段允许管理员在以下示例中指定日志设施和优先级级别：

```
sshd : .example.com : severity emerg
```

## 2.6.2.2.4. 扩展

扩展与 `spawn` 和 `twist` 指令结合使用时，提供有关客户端、服务器和进程的信息。以下是支持的扩展列表：

- `a` 返回 IP 地址。
- `A` 返回服务器的 IP 地址。
- `C` 返回各种客户端信息，如用户名和主机名，或用户名和 IP 地址。
- `d` 返回守护进程名称。
- `h` 返回客户端主机名（如果主机名不可用则返回 IP 地址）。
- `H` 返回服务器主机名（如果主机名不可用则返回 IP 地址）。
- `n` 返回客户端主机名。如果不可用则输出 unknown。如果主机名和主机地址不匹配，输出 paranoid。
- `N` 返回服务器主机名。如果不可用则输出 unknown。如果服务器主机名和主机地址不匹配，输出 paranoid。
- `p` 返回守护进程的 ID。
- `s` 返回各种类型的服务器信息，如守护进程和服务器的主机或地址。
- `u` 返回用户名。如果不可用则输出 unknown。

已被服务器封禁：

```
vsftpd : .example.com \
  tcp /bin/echo "421 %h has been banned from this server!"
```

有关可用扩展的完整说明，以及额外的访问控制选项，请参阅 `hosts_access` 的 man页（`man 5 hosts_access`）和 `hosts_options` 的 man页。

有关 TCP Wrappers 的更多信息，请参阅第 2.6.5 节“额外资源”。

## 2.6.3. xinetd

`xinetd` 是一个封装超级服务（super service）的守护进程，用于控制对部分流行网络服务的访问，包括 FTP、IMAP 和 Telnet。它为访问控制、日志处理、绑定、重定向和资源利用控制提供了特定于服务的配置选项。

当客户端尝试连接到由 `xinetd` 控制的网络服务时，超级服务会接收请求并检查是否存在任何 TCP Wrappers 访问控制规则。

如果允许访问，`xinetd` 将验证该连接是否符合其针对该服务的访问规则。它还会检查该服务是否能够为其分配更多资源，以及是否违反了任何定义的规则。

如果满足所有条件（即：允许访问该服务；服务未达到其资源限制；且服务未违反任何定义的规则），`xinetd` 将启动请求服务的实例并将连接控制权交由该实例。在连接建立后，`xinetd` 不再参与客户端与服务器之间的通信。

## 2.6.4. xinetd 配置文件

`xinetd` 的配置文件如下：

- `/etc/xinetd.conf` — 全局 `xinetd` 配置文件。
- `/etc/xinetd.d/` — 包含所有特定于服务的文件的目录。

### 2.6.4.1. /etc/xinetd.conf 文件

`/etc/xinetd.conf` 文件包含影响 `xinetd` 控制下每个服务的通用配置设置。它在 `xinetd` 服务首次启动时被读取，因此为了使配置更改生效，您需要重启 `xinetd` 服务。以下是 `/etc/xinetd.conf` 示例：

```
defaults {
  instances = 60
  log_type = SYLOG
  log_on_success = HOST
  log_on_failure = HOST
  cps = 25
}
included /etc/xinetd.d
```

这些行控制着 `xinetd` 的以下方面：

- `instances` — 指定 `xinetd` 可以处理的最大并发请求数。
- `log_type` — 配置 `xinetd` 使用 authpriv 设施，该设施会将条目写入 `/var/log/secure` 文件。
- `log_success` — 配置 `xinetd` 连接尝试。默认情况下，远程主机的 IP 地址和处理请求的服务器进程 ID 会记录在 `/var/log/` 目录下。
- `log_failure` — 配置 `xinetd` 失败连接尝试或连接被拒绝的情况。
- `cps` — 配置 `xinetd` 任意服务每秒允许的连接不超过 25 个。如果超过此限制，服务将被暂停 30 秒。
- `included /etc/xinetd.d/` — 包含位于 `/etc/xinetd.d/` 目录下的特定服务文件中声明的选项。更多信息请参阅第 2.6.4.2 节“/etc/xinetd.d/ 目录”。

通常，`/etc/xinetd.conf` 中的 `log_success` 和 `log_failure` 设置会在特定服务的配置文件中进一步修改。更多信息可能会出现在该服务的文件中。更多信息请参阅第 2.6.4.3 节“日志选项”。

## 2.6.4.2. /etc/xinetd.d/ 目录

`/etc/xinetd.d/` 目录包含由 `xinetd` 管理的每个服务的配置文件，且服务名称与服务相关联。与 `/etc/xinetd.conf` 不同，该目录仅在 `xinetd` 服务启动时被读取。为了使更改生效，管理员必须重启 `xinetd` 服务。

`/etc/xinetd.d/` 目录中的文件格式使用与 `/etc/xinetd.conf` 相同的惯例。将每个服务的配置存储在单独文件中主要原因是为了使自定义更简单，并减少影响其他服务的概率。

要要了解这些文件的结构，请考虑 `/etc/xinetd.d/telnet` 文件：

```
service telnet
{
  flags          = REUSE
  socket_type    = stream
  wait           = no
  user           = root
  server         = /usr/sbin/telnet
  log_on_failure = USERID
  disable        = yes
}
```

这些行控制着 `telnet` 服务的各个方面：

- `service` — 指定名称，通常列在 `/etc/services` 文件中。
- `flags` — 为连接设置任意数量的属性。`REUSE` 指示 `xinetd` 为 Telnet 连接复用 socket。

> 注意：`REUSE` 标记已弃用。所有服务现在都隐式地使用 `REUSE` 标记。

- `socket_type` — 将网络套接类型设置为流（stream）。
- `wait` — 指定服务是单线程（yes）还是多线程（no）。
- `user` — 指定进程运行下的用户 ID。
- `server` — 指定要启动的二进制执行文件。
- `log_on_failure` — 除了 `xinetd.conf` 中定义的参数外，指定连接失败时的日志参数。
- `disable` — 指定服务是禁用（yes）还是启用（no）。

有关这些选项的用法，请参阅 `xinetd.conf` man页。

## 2.6.4.3. 修改 xinetd 配置文件

`xinetd` 为服务提供系列指令。本节重点介绍一些常用的选项。

### 2.6.4.3.1. 日志选项

日志选项适用于 `/etc/xinetd.conf` 以及 `/etc/xinetd.d/` 目录下的服务配置文件。

以下是一些常用日志选项的列表：

- `ATTEMPT` — 记录发生失败尝试的情况（`log_on_failure`）。
- `DURATION` — 记录远程系统使用服务的时间（`log_on_success`）。
- `EXIT` — 记录远程主机的 IP 地址（`log_on_failure` 和 `log_on_success`）。
- `PID` — 记录接收请求的服务器进程 ID（`log_on_success`）。
- `USERID` — 使用 RFC 1413 方法为所有多线程流服务记录远程用户（`log_on_failure` 和 `log_on_success`）。

日志选项的完整列表请参阅 `xinetd.conf` man页。

## 2.6.4.2. 访问控制选项

`xinetd` 用户选择使用 TCP Wrappers 主机访问规则、通过 `xinetd` 配置文件提供访问控制，或两者结合使用。有关 TCP Wrappers 主机访问控制的更多信息，请参阅第 2.6.2 节，“TCP Wrappers”。

在结合 `xinetd` 访问控制使用 TCP Wrappers 运行时，理解这两种访问控制机制之间的关系非常重要。

以下是客户端请求连接时 `xinetd` 遵循的事件序列：

- 1. `xinetd` 守护进程使用 `libwrap` 库检查 TCP Wrappers 主机规则。如果匹配到拒绝（deny）规则，则连接被丢弃。如果允许（allow）规则匹配客户端，则连接将传递给 `xinetd`。
- 2. `xinetd` 守护进程会针对 `xinetd` 服务和请求的服务检查其自身的访问控制规则。如果拒绝（deny）规则匹配客户端，则连接被丢弃。否则，`xinetd` 会启动请求服务的实例并将连接的控制权交给该实例。

> 在结合 `xinetd` 访问控制使用 TCP Wrappers 访问控制时应小心。配置不当可能会导致意外后果。

## 2.6.4.3. 绑定与重定向选项

`xinetd` 的服务配置文件支持将服务绑定到 IP 地址，并将对服务的请求重定向到另一个 IP 地址、主机名或端口。

绑定由特定服务配置文件中的 `bind` 选项控制，并将服务链接到系统上的一个 IP 地址。如果配置了此项，`bind` 选项仅允许指向正确 IP 地址的请求访问服务。你可以使用此方法根据需求将服务绑定到不同的网络接口。

这对于具有多个网络适配器或多个 IP 地址的系统特别有用。在这样的系统上，例如 Telnet，可以配置为仅监听连接到私有网络的接口，而不监听连接到互联网的接口。

`redirect` 选项接受一个 IP 地址或主机名，后面紧跟一个端口号。它配置服务将这些请求重定向到指定的主机和端口号。此功能可以指向相同系统上的另一个端口、将请求重定向到系统上的不同 IP 地址、将请求转移到完全不同的系统和端口号，或者这些选项的任何组合。因此，连接到系统上特定服务的可能会被重路由到另一个系统而不会发生中断。

`xinetd` 守护进程通过产生一个进程来实现这种重定向，该进程在请求客户端机器与实际提供服务的主机之间的连接期间一直存活，并在两个系统之间传输数据。

`bind` 和 `redirect` 选项的优势在结合使用时得得明显。通过将服务绑定到系统上的特定 IP 地址，并将对该服务的请求重定向到只有第一台机器可见的第二个机器，可以使用内部系统为完全不同的网络提供服务。或者，这些选项也可以用于限制多网口主机上特定服务的暴露范围到已知 IP 地址，并将该服务的请求重定向到另一台专门为该目的配置的机器。

例如，考虑一个作为防火墙的系统，其 Telnet 服务有如下设置：

```
service telnet
{
  socket_type = stream
  wait = no
  server = /usr/kerberos/sbin/telnetd
  log_on_success += DURATION USERID
  log_on_failure += USERID
  bind = 123.123.123.123
  redirect = 10.0.1.13
}
```

该文件中的 `bind` 和 `redirect` 选项确保 Telnet 服务绑定到外部 IP 地址 `123.123.123.123`，即面向互联网的地址。此外，任何发送到 `123.123.123.123` 的 Telnet 服务请求都会通过网络适配器重定向到内部 IP 地址 `10.0.1.13`，防火墙和内部系统可以访问该地址。防火墙转发两个系统之间的通信，连接的系统认为它连接到了 `123.123.123.123`，但实际上它连接到了另一台机器。

标准的 Internet 协议安全 (IPsec) 实现。这些 VPN 解决方案无论是基于硬件还是软件，都充当存在于一个办公室到另一个办公室的 IP 连接之间的的专用路由器。

## 2.7.1. VPN 是如何工作的？

当数据包从客户端发送时，它会通过 VPN 路由器或网关，该网关会添加身份验证，并根据需要对数据进行加密。IPsec 有多种模式。最常用的配置是使用带有封装安全载负载 (ESP) 的隧道模式 (Tunnel Mode)。某些专有的 VPN 客户端使用带有 ESP 的传输模式 (Transport Mode)，尽管传输模式在通过 NAT 部署时会遇到困难。部署认证标头 (AH) 并不常见，主要用于核心路由器之间，这是因为在这些地方 ESP 的开销是不必要的，且不需要加密。由 Red Hat Enterprise Linux 部署的 ESP 包含了身份验证标头，尽管其他版本的软件实现有时会被 ESP + AH 错误地解密，导致双重身份验证层。

接收端 VPN 路由器解析标头信息，解密数据并将其路由到目标地（工作站或网络上的节点）。使用网络到网络的连接，局域网上的接收节点接收到解密后并准备好处理的数据包。网络到网络 VPN 中的加密和解密过程对于本地层来说是透明的。

有了这种高水平的安全性，攻击者不仅能够拦截数据包，还需要能够解密数据包。在服务器和客户端之间进行中间人攻击的入侵者至少需要一个用于会话身份验证的私钥。此外，添加此类私钥只会影响当前的流量，而不会影响过去加密发送的流量。由于 VPN 采用了多层身份验证和加密，它是将远程节点连接为统一虚拟局域网 (ifanet) 的安全且有效的方法。

## 2.7.2. Openswan

### 2.7.2.1. 概述

Openswan 是 Red Hat Enterprise Linux 中的一个开源用户空间 IPsec 实现。它采用了密钥建立 IKE (互联网密钥交换) v1 和 v2，并作为用户级守护进程实现。也可以通过 `ip xfrm` 命令进行手动密钥建立，但不建议这样做。Openswan 使用 netlink 与 Linux 内核交互以传输加密密钥。数据包的加密和解密在 Linux 内核中进行。

### 加密支持

Openswan 使用 NSS (网络安全服务) 加密库，这是 FIPS 安全合规性要求的。关于 FIPS (联邦信息处理标准) 的更多信息可以在第 9.2 节“联邦信息处理标准 (FIPS)”找到。

### 安装

运行 `yum install openswan` 命令安装 Openswan。

## 2.7.2.2. 配置

### 位置

本节列出了并了用于配置 OpenSwan 的文档和文件。

- `/etc/ipsec.d` - 主目录。存储 OpenSwan 相关文件。
- `/etc/ipsec.conf` - 配置文件。可以在 `/etc/ipsec.d` 中创建额外的 `*.conf` 配置文件进行单独配置。
- `/etc/ipsec.secrets` - 主密钥文件。可以在 `/etc/ipsec.d` 中创建额外的 `*.secrets` 文件进行单独配置。
- `/etc/ipsec.d/cert*.db` - 数据库文件。默认的 NSS 数据库文件为 `8.db`。从 Red Hat Enterprise Linux 6 开始，`9.db` 文件使用了 nss sqlite 数据库。
- `/etc/ipsec.d/key*.db` - 密钥数据库文件。默认的旧 NSS 数据库文件是 key3.db。从 Red Hat Enterprise Linux 6 开始，`key4.db` 文件使用了 nss sqlite 数据库。
- `/etc/ipsec.d/cacerts` - 证书机构 (CA) 证书的旧位置。建议将 CA 证书导入 NSS 数据库文件。此位置在下一个 Red Hat Enterprise Linux 版本中将废弃。
- `/etc/ipsec.d/certs` - 机器证书的旧位置。建议将机器证书导入 NSS 数据库文件。
- `/etc/ipsec.d/config` - 全局配置。
- `/etc/sec.conf` - 全局配置。
- `/etc/ipsec.d/secrets` - 全局配置。
- `/etc/sec.conf` - 全局配置。
- `/etc/ipsec.d/key` - 全局配置。
- `/etc/ipsec.d/key` - 全局配置。
- `/etc/ipsec.d/config` - 全局配置。
- `/etc/ipsec.d/key` - 全局配置。
- `/etc/ipsec.d/config` - 全局配置。
- `/etc/ipsec.d/key` - 全局配置。
- `/etc/ipsec.d/config` - 全局配置。
- `/etc/ipsec.d/key` - 全局配置。
- `/etc/ipsec.d/config` - 全局配置。
- `/etc/ipsec.d/key` - 全局配置。
- `/etc/ipsec.d/config` - 全局配置。
- `/etc/ipsec.d/key` - 全局配置。
- `/etc/ipsec.d/config` - 全局配置。
- `/etc/ipsec.d/key` - 全局配置。
- `/etc/ipsec.d/config` - 全局配置。
- `/etc/ipsec.d/key` - 全局配置。
- `/etc/ipsec.d/config` - 全局配置。
