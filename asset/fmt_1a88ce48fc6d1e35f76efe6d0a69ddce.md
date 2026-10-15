
要登录 SSH 服务器，请使用 `ssh` 并指定该服务器上存在的用户名以及服务器的 IP 地址或主机名。如果是第一次连接到指定的服务器，用户将会被提示先验证服务器的指纹：

```bash
# ssh user@example.com
```

无法建立主机 'example.com (10.0.0.1)' 的真实性。

ECDSA 指纹为 25:cc:73:b5:b3:96:75:3d:56:19:49:d2:5c:1f:91:3b。

你确定要继续连接吗 (yes/no)? yes

已将 'example.com' (ECDSA) 永久添加到已知主机列表中。

user@example.com 的密码是：user_password

SSH 密钥指纹系统在客户端连接时利用它来验证服务器的真实性。当用户在首次连接时通过输入 `yes` 接受密钥指纹，密钥的副本将保存到用户主目录下的 `.ssh/known_hosts` 中。未来的登录尝试将根据保存的密钥进行验证，如果服务器的密钥与保存的密钥不匹配，`ssh` 将显示警告。如果发生这种情况，用户在继续连接之前应先验证密钥变化的原因。

默认情况下，最新版本的 OpenSSH 只接受 SSHv2 连接。默认情况下，客户端将在可能的情况下使用版本 2，如果服务器不支持版本 2，将回退到版本 1。要强制 `ssh` 只使用指定的协议，请包含 `-1` 或 `-2`。更多选项可以在 `ssh(1)` 中描述。

使用 `scp(1)` 从远程机器安全复制文件。此示例将远程系统上的 `COPYRIGHT` 复制到系统当前目录下的相同文件中：

```bash
# scp user@example.com:/COPYRIGHT
```

user@example.com 的密码是：********

COPYRIGHT 100% |************************************| 4735

00:00

由于此主机的指纹已经过验证，在提示输入用户密码之前会自动检查服务器的密钥。

传递给 `scp` 的参数与 `cp` 类似。要复制的文件是第一个参数，复制的目标是第二个参数。由于文件是通过网络获取的，一个或多个文件参数采用 `user@host:<path_to_remote_file>` 的形式。在递归复制目录时请注意 `scp` 使用 `-r`，而 `cp` 使用 `-R`。

要打开用于复制文件的交互式会话，请使用 `sftp`。参阅 `sftp(1)` 获取 sftp 会话期间的可用命令列表。

### 14.8.1.1. 基于密钥的认证

客户端可以配置为使用密钥连接到远程机器而不是使用密码。使用 `ssh-keygen` 生成 RSA 认证密钥。生成公私钥对时，指定密钥类型并按照提示操作。建议使用易记但难以猜测的短语来保护密钥。

```bash
% ssh-keygen -t rsa
```

正在生成 rsa 公钥/私钥对。

输入保存密钥的文件 (/home/user/.ssh/id_rsa)：

输入短语（为空表示无短语）：

再次输入相同的短语：

您的标识已保存到 /home/user/.ssh/id_rsa。

公钥已保存到 /home/user/.ssh/id_rsa.pub。

密钥指纹为：

SHA256:54Xm9Uvtv6H4NOo6yjP/YCFODryvUUU7yWHZMqeXwh8user@host.example.com

密钥的随机艺术图像为：

```
+---[RSA 2048]----+
||
||
||
| . o.. |
| .S*+o |
| .O=Oo .. |
| =Oo= oo..|
| .oB.* +oo.
|=OE**.o..+
+----[SHA256]------+
```

在此处输入短语。它可以包含空格和符号。

重新输入短语以验证。

私钥存储在 `~/.ssh/id_rsa`，公钥存储在 `~/.ssh/id_rsa.pub`。为了使基于密钥的认证生效，必须将*公*密钥复制到远程机器上的 `~/.ssh/authorized_keys`。

## 警告

许多用户认为密钥设计是安全的，因此会在没有短语的情况下使用密钥。

这种行为是*危险*的。管理员可以通过手动查看私钥来验证密钥对是否受短语保护。如果私钥中包含 `ENCRYPTED` 单词，则密钥所有者正在使用短语。此外，为了更好地保护终端用户，可以将限制放在公钥文件中。例如，在 `ssh-rsa` 前缀之前添加 `from="192.168.10.5"` 将仅允许特定用户从该 IP 地址登录。

选项和文件随不同的 OpenSSH 版本而异。为了避免问题，请查阅 `ssh-keygen`。如果使用了短语，每次都会被提示输入短语。为了避免输入短语，请使用 `ssh-agent`。`ssh-agent` 可以将密钥加载到内存中。例如，`~/.bashrc` 可能如下：

```bash
exec ssh-agent
ssh-add ~/.ssh/id_rsa
```

`ssh-agent` 程序是一个助手。它允许你在每次连接时都无需输入短语。`ssh-agent` 守护在后台运行并在内存中持有解密后的密钥。当你连接到远程服务器时，`ssh` 客户端会向 `ssh-agent` 请求密钥。如果 `ssh-agent` 拥有该密钥，它将将其提供给客户端。

`ssh-agent` 守护可以通过多种方式启动。最常见的方法是使用 `ssh-agent` 命令：

```bash
% ssh-agent
```

该命令设置了环境变量 `SSH_SOCK` 和 `SSH_AUTH_SOCK`，允许客户端与代理通信。你也可以手动设置这些变量：

```bash
SSH_SOCK=/tmp/ssh-agent.1234
SSH_AUTH_SOCK=/tmp/ssh-agent.1234
```

使用 `ssh-add` 命令将密钥添加到代理中。列出代理中当前密钥使用 `ssh-add` 的 `-l` 标志：

```bash
% ssh-add -l
```

从代理中删除所有密钥，使用：

```bash
% ssh-add -D
```

从代理中删除特定密钥，使用：

```bash
% ssh-add -d ~/.ssh/id_rsa
```

`ssh-agent` 守护可以由许多桌面管理器自动启动。欲了解更多信息，请参阅 `ssh-agent`。

从远程机器到 22 和 80 端口，以允许 SSH 和网页浏览。这防止了对任何使用非 22 或 80 端口服务的访问。

解决方案是向网络防火墙之外的机器建立 SSH 连接，并使用它隧道到所需的服务：

```
% ssh -2 -N -f 8888:music.example.com:8000 user@unfirewalled-system.example.org
```

user@unfirewalled-system.example.org:password: ******

在此示例中，流媒体 Ogg Vorbis 客户端现在指向 localhost 端口 8888，该端口将转发到 music.example.com 的 8000 端口，成功绕过防火墙。

## 14.8.2. 启用 SSH 服务器

除了提供内置 SSH 客户端程序外，FreeBSD 系统还可以配置为 SSH 服务器，接受来自其他 SSH 客户端的连接。

要查看 sshd 是否正在运行，请使用 service(8) 命令：

```
# service sshd status
```

如果服务未运行，请向 /etc/rc.conf 添加以下行：

```
sshd_enable="YES"
```

这将在系统下次启动时启动 sshd（OpenSSH 的守护进程程序）。要现在启动它：

```
# service sshd start
```

在 FreeBSD 系统上启动服务时，系统主机密钥将自动创建，指纹将在控制台上显示。为用户提供指纹，以便他们下次连接到服务器时进行验证。

请参阅 sshd(8) 以获取启动 sshd 时的可用选项列表，以及关于身份验证、登录过程和各种配置文件的更完整讨论。

此时，sshd 应该对系统中所有拥有用户名和密码的用户可用。

## 14.8.3. SSH 服务器安全

虽然 sshd 是 FreeBSD 最广泛使用的远程管理设施，但暴力破解和随机路过攻击对于任何暴露在公共网络上的系统都是常见的的。有几个额外的参数可以防止这些攻击的成功，将在本节中进行描述。

在 OpenSSH 服务器配置文件中使用 `AllowUsers` 关键字来限制哪些用户可以登录 SSH 服务器以及从何处登录是一个好主意。例如，仅允许 root 从 192.168.1.32 登录，请向 /etc/ssh/sshd_config 添加此行：

280

第 14 章 安全

AllowUsers root@192.168.1.32

若要允许 admin 从任何地方登录，请在不指定 IP 地址的情况下列出该用户：

AllowUsers admin

多个用户应列在同一行，如下：

AllowUsers root@192.168.1.32 admin

在修改 /etc/ssh/sshd_config 后，运行以下命令让 sshd 重新加载配置：

```
# service sshd reload
```

注意

当使用此关键字时，列出每个需要登录此机器的用户是至关重要的。

在行行中未指定的任何用户都将被锁定在外。此外，OpenSSH 服务器配置文件中使用的关键字对大小写敏感。如果关键字拼写错误（包括大小写），它将被忽略。始终测试对此文件的更改，以确保编辑按预期工作。参阅 sshd_config(5) 以验证可用关键字的拼写和用法。

此外，用户可能被强制通过公钥和私钥使用双因子身份验证。当需要时，用户可以使用 ssh-keygen(1) 生成密钥对并将公钥发送给管理员。该密钥文件将如上文客户端部分所述被放在 authorized_keys 中。为了强制用户仅使用密钥，可以配置以下选项：

# AuthenticationMethods publickey

提示

不要将 /etc/ssh/sshd_config 与 /etc/ssh/ssh_config 混淆（注意第一个文件名中多了一个 d）。第一个配置服务器，第二个配置客户端。

参阅 ssh_config(5) 以获取可用客户端设置的列表。

## 14.9. 访问控制列表

由 Tom Rhodes 贡献。

访问控制列表 (ACLs) 以一种与 POSIX® 文件兼容的方式扩展了标准的 UNIX® 权限模型。这允许管理员利用更精细的权限模型。

FreeBSD GENERIC 内核为 UFS 文件系统提供了 ACL 支持。偏好于编译自定义内核的用户必须在他们的自定义内核配置文件中包含以下选项：

options UFS_ACL

此时，sshd 应该对系统中所有拥有用户名和密码的用户可用。

## 14.9.1. 启用 ACL 支持

280

第 14 章 安全

启用支持

## 14.9.2. 使用 ACL

访问控制列表 (ACLs) 以一种与 POSIX® 文件兼容的方式扩展了标准的 UNIX® 权限模型。这允许管理员利用更精细的权限模型。

FreeBSD GENERIC 内核为 UFS 文件系统提供了 ACL 支持。偏好于编译自定义内核的用户必须在他们的自定义内核配置文件中包含以下选项：

options UFS_ACL

此时，sshd 应该对系统中所有拥有用户名和密码的用户可用。

## 14.10. 监控第三方安全问题

由 Tom Rhodes 贡献。

在过去的几年里，安全领域在处理漏洞评估方面进行了许多改进。随着第三方工具在任何可用操作系统上被安装和配置，系统入侵的威胁也随之增加。

漏洞评估是安全的关键因素。虽然 FreeBSD 为基础系统发布告告，但为每个第三方工具发布公告超出了 FreeBSD 项目的能力。有一种方法可以缓解第三方漏洞并警告管理员已知的安全问题。一个名为 pkg 的 FreeBSD 附加工具包含了专门为此目的的选项。

pkg 轮询数据库以获取安全问题。该数据库由 FreeBSD 安全团队和端口开发者更新和维护。

请参阅安装 pkg 的说明。

安装提供了用于维护 pkg 数据库的定期(8) 配置，并提供了一种程序化的更新方法。如果启用，此功能将-

访问控制列表 (ACLs) 以一种与 POSIX® 文件兼容的方式扩展了标准的 UNIX® 权限模型。这允许管理员利用更精细的权限模型。

FreeBSD GENERIC 内核为 UFS 文件系统提供了 ACL 支持。偏好于编译自定义内核的用户必须在他们的自定义内核配置文件中包含以下选项：

options UFS_ACL

此时，sshd 应该对系统中所有拥有用户名和密码的用户可用。

问题类型：cups-base -- HPGL 缓冲区溢出漏洞。

参考：<https://www.FreeBSD.org/ports/portaudit/40a3bca2-6809-11d9-a9e7-0001020eed82.html>

在您安装的包中找到找到 1 个问题。

建议您立即更新或卸载受影响的包。

通过将网络浏览器指向显示的 URL，管理员可以获取有关该漏洞的更多信息。这包括根据 FreeBSD 端口版本（port version）受影响的版本，以及可能包含安全公告的其他网站。

`pkg` 是一个强大的工具，在配合 `ports-mgmt/portmaster` 使用时极其有用。

# 14.11. FreeBSD 安全公告

贡献者：Tom Rhodes。

与许多优质操作系统的发行商一样，FreeBSD 项目拥有一个安全团队，负责确定每个 FreeBSD 发布版本的终生命周期（EoL）日期，并为尚未达到 EoL 的受支持版本提供安全更新。有关 FreeBSD 安全团队和受支持版本的更多信息，请访问 FreeBSD 安全页面。

安全团队的一项任务是响应报告的 FreeBSD 操作系统漏洞。一旦确认漏洞，安全团队将验证修复该漏洞所需的步骤，并更新源代码。他们将详细信息作为“安全公告”（Security Advisory）发布。安全公告发布在 FreeBSD 网上，并发送到 freebsd-security-notifications、freebsd-security 和 freebsd-announce 邮件列表。

283

# 安全公告的格式

本节描述了 FreeBSD 安全公告的格式。

# 14.11.1. 安全公告的格式

这是一个 FreeBSD 安全公告的示例：

```
======================================================================

-----BEGIN PGP SIGNED MESSAGE-----

Hash: SHA512

======================================================================

FreeBSD-SA-14:04.bind Security Advisory

The FreeBSD Project

Topic: BIND remote denial of service vulnerability vulnerability\nCategory: contrib

Module: bind
```

发布：2014-01-14

致谢：ISC

影响：FreeBSD 8.x 和 FreeBSD 9.x

已修复：2014-01-14 19:38:37 UTC (stable/9, 9.2-STABLE)

2014-01-14 19:42:28 UTC (releng/9.2, 9.2-RELEASE-p3)

2014-01-14 19:42:28 UTC (releng/9.1, 9.1-RELEASE-p10)

2014-01-14 19:38:37 UTC (stable/8, 8.4-STABLE)

2014-01-14 19:42:28 UTC (releng/8.4, 8.4-RELEASE-p7)

2014-01-14 19:42:28 UTC (releng/8.3, 8.3-RELEASE-p14)

CVE 名称：CVE-2014-0591

有关 FreeBSD 安全公告的通用信息（包括上述字段的描述、安全分支以及后续章节），请访问 <URL:http://security.FreeBSD.org/>。

I. 背景

BIND 9 是域名系统 (DNS) 协议的实现。`named(8)` 守护进程是一个互联网域名服务器。

II. 问题描述

由于处理针对 NSEC3 签名区域的查询时存在缺陷，BIND 在处理具有某些属性的查询时，会在 `name.c` 中因“INSIST”失败而崩溃。此问题仅影响至少包含一个 NSEC3 签名区域的权威域名服务器。仅递归服务器不受影响。

# III. 影响

能够发送特殊构造查询的攻击者会导致 `named(8)` 崩溃，从而导致拒绝服务。

# IV. 规避措施

没有可用的规避措施，但未运行 `named(8)` 且未包含一个 NSEC3 签名区域的权威 DNS 服务的系统不受影响。

# V. 解决方案

执行以下操作之一：

- 1) 将您的受影响系统升级到修复日期之后的受支持 FreeBSD 稳定或发布/安全分支（releng）。

- 2) 通过源码补丁更新您的受影响系统：

以下补丁已验证适用于相应的 FreeBSD 版本分支。

284

第 14 章 安全

a) 从下方位置下载相关补丁，并使用您的 PGP 工具验证分离的 PGP 签名。

[FreeBSD 8.3, 8.4, 9.1, 9.2-RELEASE 和 8.4-STABLE]

```
# fetch http://security.FreeBSD.org/patches/SA-14:04/bind-release.patch
```

```
# fetch http://security.FreeBSD.org/patches/SA-14:04/bind-release.patch.asc
```

```
# gpg --verify bind-release.patch.asc
```

[FreeBSD 9.2-STABLE]
