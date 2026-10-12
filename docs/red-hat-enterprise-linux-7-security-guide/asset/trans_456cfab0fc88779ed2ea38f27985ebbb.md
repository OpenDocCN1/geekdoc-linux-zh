

## SMTP SASL 安全选项

```
smtpd_sasl_security_options = noanonymous, noplaintext
smtpd_sasl_tls_security_options = noanonymous
```

上述示例规定，在未加密的会话期间，不允许匿名认证，也不允许使用传输未加密用户名或密码的机制。对于加密会话（使用 TLS），仅允许使用非匿名认证机制。

请访问 [http://www.postfix.org/SASL_README.html#smtpd_sasl_security_options](http://www.postfix.org/SASL_README.html#smtpd_sasl_security_options) 查看所有用于限制允许使用的 SASL 机制的支持策略列表。

### 附加资源

以下在线资源提供了有关配置 Postfix SMTP 通过 SASL 进行认证的有用附加信息。

- [http://wiki2.dovecot.org/HowTo/PostfixAndDovecotSASL](http://wiki2.dovecot.org/HowTo/PostfixAndDovecotSASL) – 包含有关如何设置 Postfix 以使用 Dovecot SASL 实现进行 SMTP 认证的信息。
- [http://www.postfix.org/SASL_README.html#server_sasl](http://www.postfix.org/SASL_README.html#server_sasl) – 包含有关如何设置 Postfix 以使用 Dovecot 或 Cyrus SASL 实现进行 SMTP 认证的信息。

## 4.3.11. 保护 SSH

安全外壳协议（SSH）是一种强大的网络协议，用于通过安全通道与另一系统进行通信。SSH 上的传输是加密的，并受到保护以防截获。有关 SSH 协议的一般信息以及在 Red Hat Enterprise Linux 7 中使用 SSH 服务的信息，请参阅《Red Hat Enterprise Linux 7 系统管理员指南》中的 OpenSSH 章节。

> **重要**
>
> 本节强调了保护 SSH 设置的常见方法。绝不应将此建议措施列表视为详尽无遗或决定性的。请参阅 sshd_config(5) 以获取有关可用于修改 sshd 守护进程行为的所有配置指令的描述，并参阅 ssh(1) 以了解基本 SSH 概念的解释。

### 4.3.11.1. 加密登录

SSH 支持使用加密密钥登录计算机。这比仅使用密码要安全得多。如果您将此方法与其他身份验证方法结合使用，则可以将其视为多因素认证。有关使用多种身份验证方法的更多信息，请参阅第 4.3.11.2 节，“多种身份验证方法”。

为了启用使用加密密钥进行身份验证，需要将 /etc/ssh/sshd_config 文件中的 PubkeyAuthentication 配置指令设置为 yes。请注意，这是默认设置。将 PasswordAuthentication 指令设置为 no 以禁用使用密码登录的可能性。

可以使用 ssh-keygen 命令生成 SSH 密钥。如果在调用时没有额外参数，它将创建 2048 位 RSA 密钥集。默认情况下，密钥存储在 ~/.ssh/ 目录中。您可以利用 -b 开关来修改密钥的位强度。通常使用 2048 位密钥就足够了。《Red Hat Enterprise Linux 7 系统管理员指南》中关于配置 OpenSSH 的章节包含了有关生成密钥对的详细信息。

您应该在 `~/.ssh/` 目录中看到两个密钥。如果在运行 `ssh-keygen` 命令时接受了默认值，则生成的文件名为 `id_rsa` 和 `id_rsa.pub`，分别包含私钥和公钥。您始终应通过使私钥仅对文件所有者可读来保护私钥免受暴露。然而，需要将公钥传输到您将要登录的系统。您可以使用 `ssh-copy-id` 命令将密钥传输到服务器：

```bash
$ ssh-copy-id -i [user@]server
```

该命令还会自动将公钥追加到服务器上的 `~/.ssh/authorized_keys` 文件。当尝试登录服务器时，`sshd` 守护进程将检查此文件。

与密码和其他任何身份验证机制类似，您应该定期更改 SSH 密钥。更改时，请确保从 `authorized_keys` 文件中删除任何未使用的密钥。

### 4.3.11.2. 多种身份验证方法

使用多种身份验证方法，即多因素认证，可以提高对未授权访问的保护级别，因此在加固系统以防止其被入侵时应予以考虑。尝试登录使用多因素认证系统的用户必须成功完成所有指定的身份验证方法才能被授予访问权限。

使用 /etc/ssh/sshd_config 文件中的 `AuthenticationMethods` 配置指令来指定要使用哪些身份验证方法。请注意，使用此指令可以定义多组所需的身份验证方法。如果是这种情况，用户必须在至少一组中完成所有方法。列表需要用空格分隔，而列表内的单个身份验证方法名称必须用逗号分隔。例如：

```text
AuthenticationMethods publickey,gssapi-with-mic publickey,keyboard-interactive
```

配置了上述 `AuthenticationMethods` 指令的 `sshd` 守护进程仅授予访问权限，前提是尝试登录的用户成功完成 `publickey` 身份验证后接着进行 `gssapi-with-mic` 身份验证，或者接着进行 `keyboard-interactive` 身份验证。请注意，请求的每个身份验证方法都需要使用 /etc/ssh/sshd_config 文件中的相应配置指令（例如 `PubkeyAuthentication`）明确启用。有关可用身份验证方法的一般列表，请参阅 `ssh(1)` 的 `AUTHENTICATION` 部分。

### 4.3.11.3. 保护 SSH 的其他方法

#### 协议版本

尽管 Red Hat Enterprise Linux 7 提供的 SSH 协议实现仍然支持 SSH 客户端的 SSH-1 和 SSH-2 协议版本，但尽可能情况下仅应使用后者。SSH-2 版本包含针对旧版 SSH-1 的若干改进，并且大多数高级配置选项仅在使用 SSH-2 时才可用。

Red Hat 建议使用 SSH-2 以最大程度地提高 SSH 协议对其所使用的身份验证和通信的保护程度。`sshd` 守护进程支持的协议版本可以通过 /etc/ssh/sshd_config 文件中的 `Protocol` 配置指令进行指定。默认设置为 `2`。请注意，SSH-2 版本是 Red Hat Enterprise Linux 7 SSH 服务器支持的唯一版本。

#### 密钥类型

虽然 `ssh-keygen` 命令默认生成一对 SSH-2 `RSA` 密钥，但可以使用 `-t` 选项指示其生成 DSA 或 ECDSA 密钥。ECDSA（椭圆曲线数字签名算法）在相同的等效对称密钥长度下提供更高的性能。它还生成更短的密钥。

#### 非默认端口

默认情况下，`sshd` 守护进程监听 TCP 端口 **22**。更改端口可以减少系统基于自动化网络扫描的攻击暴露，从而通过隐蔽性增加安全性。端口可以使用 /etc/ssh/sshd_config 配置文件中的 `Port` 指令进行指定。还请注意，必须更改默认 SELinux 策略以允许使用非默认端口。您可以通过修改 `ssh_port_t` SELinux 类型并执行以下命令来完成此操作（需以 `root` 身份运行）：

```bash
# semanage -a -t ssh_port_t -p tcp port_number
```

在上述命令中，将 *port_number* 替换为使用 `Port` 指令指定的新端口号。

#### 禁止 Root 登录

如果您的特定用例不需要作为 `root` 用户登录的可能性，您应考虑将 /etc/ssh/sshd_config 文件中的 `PermitRootLogin` 配置指令设置为 `no`。通过禁用作为 `root` 用户登录的可能性，管理员可以审计哪个用户在作为普通用户登录后获得了 root 权限并运行了哪些特权命令。

#### 使用 X 安全扩展

Red Hat Enterprise Linux 7 客户端中的 X 服务器不提供 X 安全扩展。因此，客户端无法在连接到带有 X11 转发的不可信 SSH 服务器时请求另一层安全。大多数应用程序无论如何都无法在此扩展启用时运行。默认情况下，/etc/ssh/sshd_config 文件中的 `ForwardX11Trusted` 选项设置为 `yes`，并且 `ssh -X remote_machine`（不可信主机）和 `ssh -Y remote_machine`（可信主机）命令之间没有区别。

> **警告**
>
> Red Hat 建议不要在与不可信主机连接时使用 X11 转发。

## 4.3.12. 保护 PostgreSQL

PostgreSQL 是一个对象关系数据库管理系统（DBMS）。在 Red Hat Enterprise Linux 7 中，`postgresql-server` 软件包提供 PostgreSQL。如果未安装，请以 root 用户身份输入以下命令进行安装：

```bash
# yum install postgresql-server
```

在开始使用 PostgreSQL 之前，您必须在磁盘上初始化一个数据库存储区域。这称为数据库集群。要初始化数据库集群，请使用随 PostgreSQL 一起安装的命令 `initdb`。数据库集群所需文件系统位置由 `-D` 选项指示。例如：

