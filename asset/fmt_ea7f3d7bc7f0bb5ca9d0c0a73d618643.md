
在你相当确定你的 Kerberos 设置正确后，请考虑以下问题：

```
www.syng.com
```

# 网络身份验证与加密 • 第 6 章 341

- 除非你有一个具有完美正向和反向区域的 DNS 服务器，否则 DNS 将无法使用 Kerberos。仅仅拥有正向区域或填充的 `/etc/hosts` 文件是不足以运行 Kerberos 的。
- Kerberos 发的票据对时间敏感。为了减少身份验证问题，Kerberos 不会向时钟与 KDC 相差超过五分钟的主机颁发票据。NTP 旨在确保所有服务器的时间均一致。`www.ecics.udel.edu` 的服务器上有关于 NTP 的更多信息，包括你可以安装的网络守护进程。
- 旧旧的凭据：当你尝试使用 `kadmin` 管理 Kerberos 时，重要的是意识到，如果你使用某个用户对数据库进行了重大更改，你必须使用 `destroy` 然后通过 `kinit` 来获取新凭据。
- 不支持的客户端应用程序：确保该应用程序实际支持 Kerberos 协议且版本匹配。
- 未启动的 Kerberos 客户端守护进程：检查你目标服务器上的 `xinetd` 配置，以确保该服务器已启动正确的 Kerberos 守护进程。例如，如果你想通过 Kerberos FTP 连接连接到服务器 james 来测试 Kerberos，请确保在 james 上启动了支持 Kerberos 的 FTP 服务器。
- Kerberos 日志文件：如果你遇到问题，请使用 `tail -f` 命令持续读取 `/var/log/kadmind.log` 和 `kberos5dc.log` 文件。
- 安全考虑：你必须配置你的 Kerberos 主机仅使用 Kerberos 客户端。为了正确使用 Kerberos，除非使用 OTP、加密或类似的安全协议，否则网络上不应使用其他客户端应用程序或服务器守护进程。例如，如果你只有一个 Telnet 守护进程在接受连接，密码不能穿越网络。

有关配置 Kerberos 客户端的更多信息，请参阅 `/usr/share/doc/kerb5-workstation-1.2.2/` 目录下的文档。

# Kerberos 客户端应用程序

工作站包安装的 Kerberos 客户端都在 `/usr/kerberos/bin/` 目录下。以下是提供的常用程序描述：

![](img/a7a9caa80ec85507179284d91e216f9f_344_0.png)

# 第 6 章 • 网络身份验证与加密

- `kpasswd`：Kerberos 守护进程客户端可以使用 `/usr/kerberos/bin/kpasswd` 命令更改 Kerberos KDC 上的密码。
- `ftp`：支持 Kerberos 的 FTP 客户端。
- `krlogin`：支持 Kerberos 的 rlogin 客户端，允许你在不提供密码的情况下登录远程主机。此版本是对标准 rlogin 的改进，因为密码不会以明文发送。
- `krsh`：支持 Kerberos 的 rsh 客户端，允许在不密码的情况下在远程主机上执行命令。
- `ksu`：要求用户在被允许成为 root 或其他用户之前联系 KDC。

# Kerberos 身份验证与 klogin

在你为 klogin 创建主体（`login/hostname.domainname.com@YOURREALM.COM`）并更新了所有涉及主机的 keytab 文件后，你就可以配置你的主机允许他人在不泄露你密码的情况下访问你的主目录。你只需要在主目录下创建一个名为 `.klogin` 的隐藏文件。点（`.`）使该文件变为隐藏。然后你必须输入你想要允许访问的用户主体。当然，该用户必须在 KDC 上定义，并且用户联系你的主机必须拥有更新后的 keytab 文件，该文件包含 `krlogin` 的主机和守护进程名称。

如果你想向 `.k5login` 文件添加多个主体，可以通过每行输入一个主体来实现，如下所示：

```
patrick@YOURREALM.COM
susan@MYREALM.ORG
```

这些条目使得 patrick 和 susan 能够访问主目录（包含 `.k5login` 文件的系统主目录），而无法访问你机器或其他或网络上的任何其他区域。如果你想撤销对主目录的访问，只需编辑 `.k5login` 文件并删除相关项即可。

# 练习：配置 Kerberos 客户端

在此练习中，你将向你的 Kerberos 领域添加主机、托管主机和主机守护进程主体。此练习假设三个不同的系统承担以下角色：

![](img/a7a9caa80ec85507179284d91e216f9f_345_0.png)

# 网络身份验证与加密 • 第 6 章 343

- Kerberos KDC (主机 A)
- 支持 Kerberos 的 FTP 客户端 (主机 B)
- 支持 Kerberos 的 FTP 守护进程 (主机 C)

# 网络身份验证与加密 • 第 6 章 344

- Kerberos KDC (主机 A)
- 支持 Kerberos 的 FTP 客户端 (主机 B)
- 支持 Kerberos 的 FTP 守护进程 (主机 C)

# 网络身份验证与加密 • 第 6 章 345

- Kerberos KDC (主机 A)
- 支持 Kerberos 的 FTP 客户端 (主机 B)
- 支持 Kerberos 的 FTP 守护进程 (主机 C)

# 网络身份验证与加密 • 第 6 章 346

- Kerberos KDC (主机 A)
- 支持 Kerberos 的 FTP 客户端 (主机 B)
- 支持 Kerberos 的 FTP 守护进程 (主机 C)

# 网络身份验证与加密 • 第 6 章 347

- Kerberos KDC (主机 A)
- 支持 Kerberos 的 FTP 客户端 (主机 B)
- 支持 Kerberos 的 FTP 守护进程 (主机 C)

# 网络身份验证与加密 • 第 6 章 348

- Kerberos KDC (主机 A)
- 支持 Kerberos 的 FTP 客户端 (主机 B)
- 支持 Kerberos 的 FTP 守护进程 (主机 C)

# 网络身份验证与加密 • 第 6 章 349

- Kerberos KDC (主机 A)
- 支持 Kerberos 的 FTP 客户端 (主机 B)
- 支持 Kerberos 的 FTP 守护进程 (主机 C)

## 总结

在本章中，你已经学习了避免嗅探攻击的方法。加密传输和确保密码不以明文形式跨越网络是其中的两种核心策略。你学习了如何使用 OPIE 实现一次性密码（OTP），然后学习了 Kerberos 如何允许你建立一种更健壮但更复杂的身份验证方案。现在你已经掌握了在客户端和服务器上实现 OPI 的基本操作，并掌握了实现 Kerberos 的方法。从实体创建到静态密钥交换以及凭据确认，你现在了解了在小型网络以及使用多个 Kerberos 领域（realms）的企业级网络中实现 Kerberos 所需要素。

在实现 Kerberos 时，你会发现必须投入额外的资源来管理 Kerberos 实体和安全网络守护进程。你还会发现有必要对客户端/服务器配置进行故障排除。尽管如此，这些解决方案将帮助你保护网络安全。现在，是时候学习如何使用加密技术（如 Secure Shell）来阻止嗅探攻击了。

## 解决方案快速通道

### 理解网络身份验证

- 即使员工留在防火墙后，许多系统服务仍允许明文身份验证，包括 Telnet、文件传输协议 (FTP) 和标准网络信息服务 (NIS)。尽管传输可以被加密，但存在许多工具可以帮助黑客发起嗅探攻击来获取加密信息。
- 在捕获包含加密密码的数据包后，黑客会使用如 L0phhtCrack 之类的破解程序，这些程序设计用于捕获并破解嗅探到的加密密码。

### 创建身份验证和加密解决方案

- 要进行安全身份验证，你有两个选择：找到一种无需跨网络发送密码的身份验证方法，或者找到一种丢弃任何跨网络密码的方法。这种策略的通用术语是一次性密码（OTP）。

![](img/a7a9caa80ec85507179284d91e216f9f_348_0.png)

- Kerberos 增加了在身份验证后加密传输的能力。然而，OTP 的使用并不加密后续传输。不过，OTP 的实现通常比 Kerberos 简单得多。
- 其他加密解决方案包括安全套接层 (SSL)、安全外壳 (SSH) 和 IPSec。

### 实现一次性密码 (OTP 和 OPIE)

- 在 Linux 世界中，在 Linux 系统中实现一次性密码（OTP）支持的最通用方法是安装 One-Time Passwords in Everything (OPIE)。OPIE 支持消息摘要算法5 (MD5) 算法。
- 默认情况下，当你交互式登录时，OPIE 不强制执行 OTP。任何用户都可以选择使用 OTP 或标准登录程序。
- 使用 `opiepasswd` 创建 OPIE 用户。一旦对用户使用了 `opiepasswd` 命令，该用户就可以使用 OTP 登录。`opiekey` 命令用于响应。
