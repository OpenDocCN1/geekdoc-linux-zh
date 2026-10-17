
- 使用 INET 服务
- 实现 tcp_wrappers
- 设置路由
- 配置防火墙

安全是网络不可或缺的一部分。确保你的系统免受黑客的攻击并防止未经授权的使用是必须的。一些非常基础的安全问题可能会源于标准的日常活动。在当今如此强调网络安全的背景下，RHCE 在工作中能够熟练地设置网络安全至关重要。本着这一考虑，掌握网络安全工具和概念的配置及工作知识是必要的。在本章中，我们将讨论安全概念、NIS（网络信息服务）、PAM（可插件认证模块）、inetd 和 tcp_wrappers。我们还将讨论一些高级网络选项，包括路由、防火墙和 IP 掩装。

## NIS

NIS 是 Sun 的网络信息服务（Network Information Service）。它曾被称为 Yellow Pages，但在与英国电信商标纠纷后，Sun 将其更名为 Network Information Service。

NIS 是一个小型目录服务，其主要目的是允许本地网络系统上的用户进行认证。NIS 允许将 `passwd` 和 `group` 文件、sendmail 别名、挂载映射和 hosts 等配置信息存储在独立的服务器上。每个 NIS 域运行运行 NIS 客户端和 `ybind`，以查找服务器并检索其上相应的映射。

在一个 NIS 域内，必须至少有一个 NIS 服务器。在某些情况下，会设置多个 NIS 服务器，分为主服务器和从服务器。在主从设置中，从服务器会制作主 NIS 数据库更改的副本。

你必须运行 RPC PortMapper（`/usr/sbin/portmap`）才能运行 NIS。RPC PortMapper 服务器将 RPC 程序编号转换为 TCP/IP 或 UDP/IP 端口号。通常，PortMapper 服务器由 `inetd` 启动。我们将在本章稍后讨论 `inetd` 网络。

## Red Hat Linux NIS

Red Hat Linux 6.0 带有符合 NIS v.2 的客户端、服务器和工具。Red Hat Linux 6.0 中的三个 NIS 包包括 `ybind`（NIS 客户端）、`ypserv`（NIS 服务器）和 `yp-tools`（查询 NIS 服务器的实用）。只有当 `/etc/nsswitch.conf` 文件和 `ybind` 指定时使用 NIS。在本节中，我们将讨论 NIS 客户端和 NIS 服务器命令。

## 系统安全与管理

### NIS 客户端

NIS 客户端负责向 NIS 服务器查询 NIS 系统映射和其他 NIS 信息。NIS 客户端使用以下五种主要工具：

- `ybind`: 查找并存储有关 NIS 域和服务器的信息。信息存储在 `/var/yp/binding` 中。
- `ypwich`: 返回 NIS 客户端使用的 NIS 服务器名称。
- `ypcat`: 打印指定 NIS 数据库中所有键的值。
- `yppoll`: 返回指定 NIS 映射的版本和主服务器。
- `ypmatch`: 打印来自 NIS 映射的键值。

### NIS 服务器

NIS 服务器负责在它的专用机器上托管系统映射和认证文件。然后，NIS 服务器会响应 NIS 客户端对认证、系统映射和其他 NIS 信息的请求。除了 NIS 客户端命令外，NIS 服务器还使用如下 NIS 命令：

- `ypserv`: NIS 服务器程序。
- `ypppasswd`: 处理 NIS 密码更改的服务器。

### 其他 NIS 命令

在 NIS 网络上还有许多其他 NIS 命令可以使用。一些常用的 NIS 命令对是：

- `makedbm`: 将 ASCII 数据库（如 `/etc/passwd`）转换为 DBM 数据库。
- `yppush`: 当主数据库发生更改时通知从服务器。

## /etc/nsswitch.conf

只有当由 `/etc/nsswitch.conf` 文件指定或使用 `ybind` 时才实现 NIS。GNU C 库包含了对名称服务器切换文件（`/etc/nsswitch.conf`）的支持，该文件参考了 Solaris 2 上的 `nsswitch.conf` 文件。名称服务器切换文件配置了各种系统服务的查找顺序。以下片段是 Red Hat 6.0 附带的 `/etc/nsswitch.conf` 文件。

```
#
# /etc/nsswitch.conf
#
# 示例名称服务切换配置文件。此文件应该
# 将最常用的服务放在开头。
#
# 条目 '[NOTFOUND-return]' 意味着如果在上一个条目的搜索
# 没有找到结果，则停止对该条目的搜索。注意，如果搜索由于
# 其他原因失败（例如没有 NIS 服务器响应），则继续
# 使用下一个条目进行搜索。
#
# 合法条目有：
#
# nisplus or nis+      使用 NIS+
# nis or yp            使用 NIS (version 2)
# dns                  使用域名系统服务
# files               使用本地文件
# db                   使用本地数据库
# compat             使用兼容模式
# [NOTFOUND-return]    如果未找到则停止搜索
# 示例：
# passwd:             db files
# shadow:             db files
# group:              db files

# passwd:             db files
# shadow:             db files
# group:              db files

# hosts:             db dns
# hosts:              files dns

# services:           nisplus [NOTFOUND-return]
# networks:           nisplus [NOTFOUND-return]
# protocols:          nisplus [NOTFOUND-return]
# rpc:                nisplus [NOTFOUND-return]
# ethers:            nisplus [NOTFOUND-return]
# netmasks:           nisplus [NOTFOUND-return]
# bootparms:         nisplus [NOTFOUND-return]

# netgroup:           nisplus

publickey: nisplus

automount: files nisplus
alias: files nisplus
```

上述 `nsswitch.conf` 文件格式使用 `database: location[result-action]` 布局，其中 `database` 是请求数据库的名称，`location` 是数据库的位置，`result` 是请求的结果，`action` 是匹配结果后执行的操作。因此，在上述 Red Hat 6.0 默认 `nsswitch.conf` 文件中，使用 `getpw*` C 库的 passwd 查找将首先访问本地 `passwd` 文件，如果未找到，第二次访问 `NIS+`，如果仍未找到，最后尝试 `NIS`。

> 注意：任何结果的操作总是 `RETURN` 或 `CONTINUE`。

| 表 11.1 NIS 数据库。 |
| :--- | :--- |
| 数据库 | 数据库说明 |
| aliases | sendmail 使用的别名 |
| ethers | 以太网号 |
| group | 用于 `getgrp` 函数的用户组 |
| hosts | 用于 `gethostbyname` 类似函数的主机和数字 |
| netgroup | 用于访问规则的网络范围主机和用户列表 |
| network | 网络名称和数字，用于 `getnetent` 函数 |
| passwd | 用于 `getpasswd` 函数的用户密码 |
| protocols | 用于 `getprotocol` 函数的网络协议 |
| publicKey | 用于安全 RPC、NIS+ 和 NFS 的公钥和密钥 |
| rpc | 用于 `getrpcbyname` 类似函数的远程过程调用名称和数字 |
| services | 用于 `getservent` 函数的网络服务 |

| 表 11.2 NIS 位置。 |
| :--- | :--- |
| 位置 | 位置描述 |
| nisplus (nis+) | 通过 NIS+ 查找 |
| nis (yp) | 通过 NIS 查找 |
| compat | 以与旧版本 glibc 兼容的方式通过 NIS 查找 |
| db | 通过本地数据库文件查找 |
| files | 通过文本文件查找 |
| dns | 通过 DNS 查找 |

| 表 11.3 NIS 结果。 |
| :--- | :--- |
| 结果 | 结果描述 | 默认操作 |
| SUCCESS | 发生错误并返回了请求的条目。 | 返回 (Return) |
| NOTFOUND | 查找过程正常，但未找到所需的值。 | 继续 (Continue) |
| UNAVAIL | 服务永久不可用。这可能意味着所需的文件不可，或者对于 DNS 来说，服务器不可用或不允许查询。 | 继续 (Continue) |
| TRYAGAIN | 服务临时不可用。这可能意味着文件被锁定或服务器无法接受更多连接。 | 继续 (Continue) |

## 可插式认证模块 (PAM)

PAM 是可插式认证模块系统，它允许在不需要重新编写各个独立服务的情况下实现规则集。所有关注安全的程序（如 login、su 和 ftp）都通过 PAM 配置以执行各种认证和安全检查。

当使用如 login 这样的服务时，PAM 将检查其配置文件以确定如何验证用户身份。例如，PAM 可能会通过检查 `/etc/passwd`、kerberos 或 NIS 来进行认证。在确定认证方法后，PAM 将向服务返回一个结果，以指示用户是否已通过认证。

## PAM 配置

所有的 PAM 配置文件都位于 `/etc/pam.d/`。每个可以使用 PAM 的应用程序服务在 `/etc/pam.d/` 中也有一个条目。在 `/etc/pam.d/` 下常见的最常见条目包括 chfn, csh, halt, lunixconf, login, password, ppp, reboot, rlogin, shutdown, su, xdm 和 xscreaver。如果安装了这些程序，你可能在这里还会看到 kde、samba 和 ssh。查看这些文件，你将看到四列信息。它们包括模块类型（module-type）、控制标志（control-flag）、模块路径（module-path）和参数（arguments）。查看以下 `/etc/pam.d/` 下 login 条目的示例：

```
#PAM-1.0
auth required /lib/security/pam_securetty.so
auth required /lib/security/pam_pwdb.so shadow nullock
auth required /lib/security/pam_login.so
account required /lib/security/pam_pwdb.so
password required /lib/security/pam_cracklib.so
password required /lib/security/pam_pwdb.so nullock use_authtok
session required /lib/security/pam_pwdb.so
session optional /lib/security/pam_console.so
```

## 模块类型 (module-type)

目前在 PAM 配置文件的模块类型列中可以找到四种模块。它们包括 auth（认证）、account（账户）、session（会话）和 password（密码）。

- auth: 此模块类型提供了两种验证用户的方法。首先，它确认用户确实是其声称的身份。它通过指示应用程序提示用户输入密码来实现。该模块随后可以通过其凭据属性授予组成员身份（独立于 `/etc/groups`）或其他特权。
- account: 此模块执行非基于认证的账户管理。它通常用于根据一天中的时间、最大用户数甚至用户的位置来限制或允许对服务的访问（例如，允许用户“root”仅从控制台登录）。
- session: 此模块与在用户获得服务之前需要执行的职责有关。受此影响的服务包括用户打开和关闭数据的记录、挂载目录等。
- password: 此模块用于更新与每个用户相关的认证令牌（token）。通常对于每个基于挑战或响应的认证（auth）模块类型，都对应一个模块。

## 控制标志 (control-flag)

control-flag 用于指示 PAM 库如何对与其关联的模块成功或失败做出反应。用于指定模块操作的四个标志是 required（必须）、requisite（必要）、sufficient（足够）和 optional（可选），描述如下：

- required: 表示该模块的成功是该模块类型功能成功的必要条件。如果此模块失败，在执行完所有相同类型的模块之前，用户将不会察觉到失败。
- requisite: 类似于 required，但如果此模块失败，控制将立即返回给应用程序。此标志有助于防止用户在不安全的介质上输入密码的可能性。
- sufficient: 表示 Linux-PAM 库认为该模块类型已实现其目的。如果之前没有模块失败，则不再调用更多此类类型的堆栈模块。如果此模块失败，结果被认为对应用程序不是致命的。
- optional: 此控制标志标记该模块对于用户访问服务的成功或失败至关重要。事实上，Linux-PAM 在确定模块栈是成功还是失败时会忽略此类模块。

## 模块路径与参数 (module-path And Arguments)

module-path 是动态加载模块的路径名。模块的默认路径设置为 `/usr/lib/security/`，除非提到了其他路径。通常无论都会列出完整路径 `/usr/lib/security/`。

每个条目的参数列列出了模块被调用时传递给模块的参数。通常，这些参数是可选的，并具体列给每个模块。如果参数无效，模块将忽略它。如果发生此类错误，模块将被将错误写入 syslog。大多数模块可以理解的五种通用参数是 debug、no_warn、use_first_pass、try_first_pass 和 user_mapped_pass，描述如下：

- debug: 使用 syslog 调用将调试信息记录到系统日志。
- no_warn: 指示模块不对应用程序提供警告消息。
- use_first_pass: 模块不提示用户输入密码。相反，它应该从前面的模块获取之前输入的密码。如果失败，用户将无法通过认证。
- try_first_pass: 模块应该尝试使用从前面的模块获取之前输入的密码进行认证。如果失败，则提示用户输入密码。
- user_mapped_pass: 指示模块获取之前模块输入的明文令牌，并使用它生成加密（或解码）密钥，以安全地存储或检索模块所需的认证令牌。

由于与加密限制相关的后果，Linux-PAM 发行版中的任何模块目前都不支持 user_mapped_pass。美国或其本国家的开发者可以在其国内自由实现。

auth 示例中列出的特殊参数是 shadow。这指的是对影子密码的支持，pam_pwdb.so 支持此项。影子密码通过替换 `/etc/passwd` 中的密码字段（用“x”）并创建 `/etc/shadow` 文件包含密码哈希值，使得系统密码信息更难以提取。

Red Hat 6.0 在安装时可以使用影子密码。如果安装期间没有启用影子密码，可以通过运行 `pwconv` 程序将系统转换为使用影子密码。如果需要，可以使用 `pwunconv` 回普通密码。此更改对于所有使用 PAM 的程序都是透明的。

## /etc/securetty

作为 PAM 最流行的用途之一，`/etc/securetty` 文件用于指定系统中安全 tty 访问的设置。`/etc/securetty` 被 login 用于启用 root 允许登录的 tty 设备。通常只列出本地控制台。通过限制访问本地控制台，你禁用了从控制台以外任何地方的直接登录超级用户权限。但不安全的，因为禁用虚拟终端控制台登录并

# 276 第11章

不限制用户从用户账户使用 `su` 登录为 root。`/etc/security` 文件的输出非常简单，因为它只列出了允许 root 登录的 tty 设备。图 11.1 显示了默认 Red Hat 6.0 `/etc/security` 文件的示例输出。

## inetd

inetd 守护进程是一个互联网守护进程，用于控制大多数网络服务监听您机器上的传入连接。该守护进程在后台运行，绑定所有相关端口并在时调用相应的服务器。

`/etc/inetd.conf` 配置文件控制 inetd 守护进程。此 inetd.conf 文件指定了机器应该管理的服务，并包含一个由七个字段组成的条目列表。这七个字段包括服务名、套类型、协议、wait/nowait、用户、服务器程序和参数，描述如下：

- 服务名（Service Name）：通过在 `/etc/services` 文件中查找服务名，将服务名转换为端口号。
- SocketType：指定 TCP 的 `stream` 或 用于 UDP 的 `dgram`。
- 协议（Protocol）：指定服务使用的传输层协议名称。
- wait/nowait：指定 dgram 套接字的 wait 或 nowait 选项（它不会影响 stream）。
- 用户（User）：执行进程的用户登录 ID。

![](img/7a3d74d02590d83bf562ed6969db9ba0_307_0.png)

图 11.1 `/etc/security` 的示例输出。
