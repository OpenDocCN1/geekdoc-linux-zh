

## Linux 简介

- 一种可与各种应用程序配合使用的通用认证方案。
- PAM 可以集成到各种应用程序中，而无需重新编译应用程序以专门支持 PAM。
- 为管理员和应用程序开发人员提供了极大的灵活性和对认证的掌控力。
- 应用程序开发人员无需针对特定的认证方案开发其程序。相反，他们可以完全专注于程序的具体细节。

目录 `/etc/pam.d` 包含 PAM 配置文件（以前是 `/etc/pam.conf`）。每个应用程序或服务都有自己单独的文件。文件中的每一行包含四个元素：

- 模块：
  - auth：提供实际的认证（例如询问并检查密码）并设置凭据，如组成员身份或 Kerberos 票据。
  - account：检查是否允许用户访问（账户未过期、用户允许在此时段登录等）。
  - password：用于设置密码。
  - session：在用户通过认证后使用。此模块执行允许访问所需的额外任务（例如，挂载用户的主目录或使他们的邮箱可用）。

模块堆叠的顺序，以便可以使用多个模块，这一点非常重要。

- *控制标志*：告知 PAM 在失败或成功时采取哪些操作。值可以是 required、requisite、sufficient 或 optional。
- *模块路径*：要使用的可插拔模块的路径，通常位于 `/lib/security` 中。
- *参数*：供模块使用的信息

影子密码文件会被 PAM 自动检测。

更多信息可参见 **pam** 的手册页或 Linux-PAM 项目主页。

## 10.3.9.3 LDAP

轻量级目录访问协议（LDAP）是一种用于通过网络访问全局或本地目录服务的客户端-服务器系统。在 Linux 中，使用的是 OpenLDAP 实现。它包括 **slapd**（一个独立服务器）、**slurpd**（一个独立的 LDAP 复制服务器）、实现 LDAP 协议的库，以及一系列实用工具、工具和示例客户端。

使用 LDAP 的主要好处是整合组织内某些类型的信息。例如，组织内所有不同的用户列表可以合并到一个 LDAP 目录中。该目录可以被任何需要此信息的 LDAP 支持的应用程序查询。它也可以被需要目录信息的用户访问。

其他 LDAP 或 X.500 Lite 的优势包括其实现的简便性（与 X.500 相比）及其明确定义的应用程序编程接口（API），这意味着支持 LDAP 的应用程序和 LDAP 网关的数量在未来应该会增加。

从负面角度看，如果你想使用 LDAP，你需要支持 LDAP 的应用程序或使用 LDAP 网关的能力。虽然 LDAP 的使用应该会持续增加，但目前针对 Linux 的支持 LDAP 的应用程序并不多。此外，虽然 LDAP 确实支持一些访问控制，但它拥有的安全功能不如 X.500 多。

由于 LDAP 是一个开放且可配置的协议，它可以用来存储与特定组织结构相关的几乎任何类型的信息。常见的例子包括邮件地址查找、结合 PAM 的中央认证、电话簿和机器配置数据库。

详情请参见你所在系统的具体信息和相关命令（如 **ldappmodify** 和 **ldapsearch**）的手册页。更多信息可参见 Linux LDAP HOWTO <http://www.tld.org/HOWTO/LDAP-HOWTO.html>，该文档讨论了在 Linux 上安装、配置、运行和维护 LDAP 服务器。本 Linux 简介文档的作者还撰写了一份 LDAP 操作 HOWTO <http://tille.xalysys.com/training/ldap/>，描述了在处理 LDAP 管理、操作和服务集成时每个人都应该知道的基本知识。

## 10.4 远程执行应用程序

### 10.4.1 简介

有几种不同的方式可以在远程机器上执行命令或运行程序，并将输出（无论是文本还是图形）发送到你的工作站。连接可以是安全的，也可以是不安全的。虽然建议将安全连接而不是在网络上未加密地传输密码，但我们将讨论一些旧（不安全）机制的实际应用，因为它们在现代网络环境中仍然有用，例如用于故障排除或运行特殊程序。

### 10.4.2 Rsh、rlogin 和 telnet

rlogin 和 rsh 命令用于远程登录和远程执行命令，继承自 UNIX。由于它们明显不安全，因此很少被使用，但几乎所有 Linux 发行版都包含它们，以保持与 UNIX 程序的向后兼容性。

另一方面，telnet 仍被广泛使用，通常由系统和网络管理员使用。Telnet 是远程访问文件和远程管理的强大工具之一，允许从互联网上的任何地方建立连接。结合 X 服务器，可以在本地显示远程图形应用程序。在本地机器上和远程机器上工作之间没有区别。

由于整个连接都是未加密的，允许 telnet 连接意味着承担极高的安全风险。对于普通的程序远程执行，建议使用 Secure Shell 或 ssh。我们将在本节稍后讨论这种安全方法。

然而，telnet 在许多情况下仍在使用。以下是一些测试邮件服务器和 Web 服务器回复的示例：

检查邮件服务器是否正常工作：

```
[jimmy@blob ~]$ telnet mailserver 25
Trying 192.169.42.1....
Connected to mailserver.
Escape character is '^]'.
220 ml.some.net ESMTP Sendmail 8.11.6/8.11.6; 200302281626
250-ml.some.net Hello blob.some.net [10.0.0.1], pleased to meet you
250-ENHANCEDSTATUSCODES
250-8BITMIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
250-XUSR
250 HELP
mail from: jimmy@some.net
250 2.1.0 jimmy@some.net... Sender ok
rcpt to: davy@some.net
250 2.1.5 davy@some.net... Recipient ok
data
354 Enter mail, end with "." on a line by itself
test
.
250 2.0.0 g2MARl619237 Message accepted for delivery
quit
221 2.0.0 ml.some.net closing connection
Connection closed by foreign host.
```

检查 Web 服务器是否响应基本请求：

```
[jimmy@blob ~]$ telnet www.some.net 80
Trying 64.39.151.23...
Connected to www.some.net.
Escape character is '^]'.
HEAD / HTTP/1.1

HTTP/1.1 200 OK
Date: Fri, 22 Mar 2002 10:05:14 GMT
Server: Apache/1.3.22 (UNIX) (Red-Hat/Linux)
mod_ssl/2.8.5 OpenSSL/0.9.6
DAV/1.0.2 PHP/4.0.6 modperl/1.24_01
Last-Modified: Fri, 04 Jan 2002 08:21:00 GMT
Etag: "70061-68-3c3565ec"
Accept-Ranges: bytes
Content-Length: 104
Connection: close
Content-Type: text/html

Connection closed by foreign host.

[jimmy@blob ~]$
```

这是完全安全的，因为你永远不需要提供用户名和/或密码来获取你想要的数据，所以没有人可以从线缆上窥探到那些重要信息。

### 10.4.3 X 窗口系统

#### 10.4.3.1 X 特性

正如我们在第 7 章（见 7.3.3 节）中已经解释过的，X 窗口系统附带一个 X 服务器，为需要显示的客户端提供图形服务。

理解 X 服务器和 X 客户端应用程序之间的区别很重要。X 服务器直接控制显示器，并负责通过键盘、鼠标和显示器进行的所有输入和输出。另一方面，X 客户端不直接访问输入和输出设备。它与处理输入和输出的 X 服务器通信。真正执行工作（如计算值、运行应用程序等）的是 X 客户端。X 服务器只是为指定的客户端打开窗口以处理输入和输出。

在正常运行（图形模式）中，每个 Linux 工作站都是其自身的 X 服务器，即使它只运行客户端应用程序。你正在运行的所有应用程序（例如，Gimp、终端窗口、你的浏览器、你的办公应用、你的 CD 播放工具等等）都是你的 X 服务器的客户端。在这种情况下，服务器和客户端运行在同一台机器上。

X 系统的这种客户端/服务器性质使其成为远程执行应用程序和程序的理想环境。因为进程实际上是在远程机器上执行的，本地主机只需要很少的 CPU 功率。仅作为 X 服务器的此类机器被称为 X 终端，曾经非常受欢迎。更多信息可参见远程 X 应用程序迷你 HOWTO <http://www.tldp.org/HOWTO/Remote-X-Apps.html>。

#### 10.4.3.2 Telnet 和 X

如果你想使用 **telnet** 来显示在远程机器上运行的图形应用程序，首先需要授予远程机器访问你的显示器（即你的 X 服务器）的权限，方法是使用 **xhost** 命令，在你的本地机器的终端窗口中输入类似以下的命令：

```
davy:~> xhost +remote.machine.com
```

之后，连接到远程主机并告诉它将图形显示在本地机器上，方法是设置环境变量 **DISPLAY**：

```
[davy@remote ~]  export DISPLAY="local.host.com:0.0"
```

完成此步骤后，在此终端窗口中启动的任何应用程序都将显示在你的本地桌面上，使用远程资源进行计算，但使用你的本地图形资源（你的 X 服务器）来显示应用程序。

此过程假设你已经在你想要显示图像的机器上设置了某种 X 服务器（XFree86、X.org、Exceed、Cygwin）。只要允许你在其上运行 X 服务器，客户端机器的架构和操作系统并不重要。

请注意，从远程机器显示终端窗口也被视为显示图像的一种形式。

