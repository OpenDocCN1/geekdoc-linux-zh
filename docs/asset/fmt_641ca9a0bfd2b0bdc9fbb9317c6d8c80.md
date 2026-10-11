
> 注意：Samba 4 是最新的下一代 Samba。在它的增强功能中，Samba 4 实现了兼容 Active Directory (AD) 的域控制器。它原生支持 AD 登录和管理协议（Kerberos, LDAP, RPC 等）。这意味着由于 `pam_winbind` 模块、`libnss_winbind`（winbind 的名称切换库）设施以及其他相关子系统的存在，所有 Windows 客户端都可以透明地加入运行在基于 Linux/UNIX 的 Samba 4 服务器上的 Samba 4 域，它们的表现就像是原生 AD 域的成员一样。

## winbindd 守护进程

`winbindd` 守护进程用于从原生 Windows 服务器解析用户账户（用户和组）信息。它也可以用于解析其他类型的系统信息。它通过使用 `pam_winbind`（一个与 `winbindd` 守护进程交互以认证用户的 PAM 模块）、`libnss_winbind`（winbind 的名称切换库）设施以及其他相关子系统来实现这一点。

设置 Linux 机器咨询 Windows 服务器进行用户认证的过程也称为将 Samba 设置为 AD 环境中的成员（Member）。实现这一点的的步骤非常直观，并可以总结如下：

1. 如果尚未安装 `winbind` 软件，请安装它。
2. 使用正确的指令配置 Samba 的配置文件 (`smb.conf`)。
3. 将 winbind 添加到 Linux 系统的名称切换设施 (`/etc/nsswitch.conf`)。
4. 将 Linux/Samba 服务器加入 Windows 域。
5. 测试各项功能。

这里展示了一个示例场景，其中 Linux 服务器 `serverA` 将使用 Windows 服务器满足其用户认证需求。该 Samba 服务器将作为 Windows 域成员运行。

在此场景中，Windows 服务器被配置为域控制器（同时也是 DNS 服务器）。它的主机名为 `win-server`，IP 地址为 `192.168.1.100`。短的 Windows 域名为 `WINDOWS-DOMAIN`。

我们刻意排除了此示例 Samba 配置中的任何共享定义，你必须创建或指定自己的定义（如果需要；请参考本章前面的部分了解如何操作）。让我们详细分解此过程：

1. 如果尚未安装 `winbind` 包，请安装它。在 Fedora、CentOS 或 openSESE 等基于 RPM 的系统中，你可以通过执行此命令安装它：

```bash
[root@fedora-server ~]# dnf -y samba-winbind
```

在 Ubuntu 等基于 Debian 的系统中，你可以使用此命令安装包：

```bash
master@ubuntu-server:~$ sudo apt-get install winbind
```

2. 为 Linux AD 成员服务器创建一个 `/etc/samba/smb.conf` 文件

```ini
# Linux AD 成员的示例 smb.conf 文件
[global]
workgroup = WINDOWS-DOMAIN
password server = 192.168.1.100
security = ads
realm = WINDOWS-DOMAIN.COM
dedicated keytab file = /etc/krb5.keytab
kerberos method = secrets and keytab
```

```ini
idmap config * : backend = tdb
idmap config * : range = 1000-9999
idmap config WINDOWS-DOMAIN : backend = ad
idmap config WINDOWS-DOMAIN : schema_mode = rfc2307
idmap config WINDOWS-DOMAIN : range = 10000-9999
```

```ini
winbind nss info = rfc2307
winbind trusted domains only = no
winbind use default domain = yes
winbind enum users = yes
winbind expand groups = yes
winbind tickets = yes
winbind normalize names = yes
vfs objects = acl_xattr
acl inherit = yes
store attributes = yes
```

3. 修改 `/etc/nsswitch.conf` 文件，将 winbind 添加其中，如下：

```text
passwd: winbind
shadow: winbind
group: winbind
```

4. 修改 `/etc/resolv.conf` 文件，使 Windows 服务器成为主 DNS：

```text
search windows-domain.com
nameserver 192.168.1.100
```

5. 使用 `net` 命令将 Samba 服务器加入域。假设使用 Windows Administrator：

```bash
[root@fedora-server]# net join -S WINDOWS-DOMAIN -U Administrator
Joined FEDORA-SERVER to domain WINDOWS.COM
```

6. 接下来 Red Hat 类系统中，你可以使用 `authconfig-tui` 工具配置其他用户信息。从命令行启动该工具并在 User Information 中选择 Winbind。在 Authentication 下选择 Next，最后点击 OK 保存。

7. 在使用 systemd 作为服务管理器的 Linux 发行版上，可以使用 `systemctl` 命令启动 winbind：

```bash
[root@fedora-server ~]# systemctl start winbind
```

在 Debian 系发行版的非 systemd 版本中，可以通过执行此命令启动守护进程：

```bash
ubuntu-server:-$ sudo /etc/init.d/winbind start
```

8. 使用 `wbinfo` 工具（由 `samba-winbind-clients` 包提供）列出 Windows 域中的所有用户，以确保运行正常：

```bash
# wbinfo -u
```

就是这些。Linux 服务器现在可以咨询 Windows 服务器来实现用户认证需求。

## Samba 故障排除

以下是在使用 Samba 时可能会遇到的一些问题的解决方案：

- 重启 Samba。可能是因为 Samba 进入了未定义状态，或者更有可能是你对配置进行了重大更改但忘记重加载 Samba 以使其生效。
- 确保配置选项正确。`smb.conf` 文件中的错误通常出现在目录、用户名、网络号和主机名中。常见的错误是当新客户端添加到具有服务器特殊访问权限的组时，没有告知 Samba 新客户端的名称。
- 日志文件。Samba 可以配置为生成任意数量的日志，且具有不同程度的细节。在排除 Samba 问题时，日志文件是你的朋友。Red Hat 类发行版的 Samba 特有日志文件位于 `/var/log/samba/` 目录下。密切关注日志！

# 摘要

本章讨论了 Samba 的编译、安装和配置过程，以便你的基于 Linux 的服务器能够与基于 Windows 的网络集成。Samba 是一个强大的工具，具有替代用于文件和打印机共享以及身份服务的 Microsoft Windows 服务器的潜力。

大量的文档可能不是你最喜欢的消磨时间的方式，但你会发现 Samba 文档是完整、有用且易于阅读的。至少要浏览一下这些文件，看看里面包含什么，这样当你需要获取额外信息时，你就知道该去哪里了。

凭借现有的所有 Samba 文本（有些免费，有些收费），你应该拥有配置即使是最复杂的设置所需的所有内容。一些专门针对 Samba 各方面的优秀文本和资源立刻浮入脑海：由 John Terpstra 和 Jelmr Vernooij 编写的《Official Samba-3 HOWTO and Reference Guide, Second Edition》（第二版），该书于 2005 年由 Prentice Hall 出版，仍然具有价值；而位于 https://wiki.samba.org 的官方 Samba Wiki 则始终是具有参考价值的。

# 第 25 章 | 分布式文件系统 (DFS)

# Linux 系统管理：入门指南
