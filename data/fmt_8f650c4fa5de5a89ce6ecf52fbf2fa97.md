
```
# service ldap start          [ OK ]
Checking configuration files for slapd: config file testing succeeded [ OK ]
Starting slapd:                             [ OK ]
```

这完成了在命令行提示符配置 LDAP 客户端的操作。重启 ssh 服务并使用 `ssh` 命令登录系统测试认证。你可以使用 `ldapsearch` 命令从 LDAP 服务器提取用户信息，并使用 `openssl` 命令测试 TLS（如果已配置）。

```
# ldapsearch -x -Z
# openssl s_client -connect rhel04
```

# 使用认证配置器配置 LDAP 客户端

设置系统 `rhel03` 作为 `rhel04` LDAP 服务器的 LDAP 客户端，在 `rhel03` 上使用认证配置器执行以下步骤。

- 1. 在 X 终端窗口中执行 `system-config-authentication`（运行 `authconfig-tui` 获取其文本对应界面或使用命令 `authconfig`），或选择 (GNOME) 系统 / (KDE) 主菜单 -> 管理 -> 认证。认证配置器界面将如图 23-4 所示。

![](img/3f35ec29a294974bc1a4fdae3ae46652_523_0.png)

**图 23-4 认证配置器 – LDAP 客户端配置**

- 2. 在用户信息下选择启用 LDAP 支持并配置 LDAP。输入 LDAP 搜索基 DN 和 LDAP 服务器信息。完成后点击 OK。

![](img/3f35ec29a294974bc1a4fdae3ae46652_523_1.png)

**图 23-5 认证配置器 – LDAP 设置**

3. 转到认证选项卡，选择启用 LDAP 支持并点击配置 LDAP。输入 LDAP 搜索基 DN 和 LDAP 服务器信息。完成后点击 OK。

4. 转到选项卡并选择合适的选项。完成后点击 OK。工具将需要一段时间来执行请求的配置。它还将设置 LDAP 客户端功能在每次系统重启时在相应的运行级别启动。随后将立即启动客户端。

![](img/3f35ec29a294974bc1a4fdae3ae46652_524_0.png)

**图 23-6** 认证配置器 – LDAP 客户端选项

这设置了 LDAP 客户端功能并在 `rhel03` 上启动 `slapd` 守护进程。

# 总结

在本章中，你学习了 NIS 和 LDAP。你了解 NIS 的概念和组件——域、映射、主服务器、从服务器和客户端。你执行了 NIS 客户端的配置，并了解了如何测试它的步骤。你使用特殊命令显示了 NIS 映射内容并在其中搜索文本。你看到了在 NIS 环境中如何修改用户密码。你查看了手动将客户端与备 NIS 服务器绑定的步骤。

本章的第二个主要主题是 LDAP。你获得了 LDAP 的介绍及其相关的功能和优势。你了解 LDAP 组件的定义，如目录、条目、属性、匹配规则、对象类、架构、LDIF、DN、RDN、服务器、副本、客户端和引用。最后，你使用命令以及认证配置器配置了 LDAP 客户端。

# 互联网服务与电子邮箱

本章涵盖了以下主要主题：

- 互联网服务简介
- 互联网服务守护进程 (`xinetd`) 的作用
- 互联网服务配置文件
- 启用/禁用 `xinetd` 控制的服务和日志
- 极安全文件传输协议 (`vsFTP`) 简介
- SELinux 要求、配置文件和访问控制
- 配置并测试 `vsFTP` 服务器
- 电子邮件简介
- 邮件系统如何工作
- 配置 `sendmail` 和 `postfix` 邮件服务器
- 设置默认 MTA
- 配置安全的 `docot` 接收邮件服务器
- 验证邮件服务器功能

互联网服务允许系统作为服务的提供者为远程系统提供功能。RHEL 上支持多种邮件软件，用于发送和接收邮件。这些软件包括作为发送和接收邮件服务器的 `sendmail` 和 `postfix`。

# 互联网服务

当在网络上使用服务时，涉及到两个软件程序：客户端和服务器。客户端程序请求远程系统运行的服务。远程系统上的服务器程序（或守护进程）响应并服务客户端，建立通道。在任何时刻，系统都可以作为服务器和客户端。它可以为其他系统提供服务。

服务器程序通过两种方式启动：通过序列目录中的启动脚本或通过名为 `xinetd` 的主守护进程。`xinetd` 守护进程在系统启动到级别 3 时启动。该守护进程读取配置文件 `/etc/xinetd.conf`，并监听 `/etc/services` 和 `/etc/rpc` 中列出的 `/etc/xinetd.d` 目录定义的端口。当此类请求到达特定端口时，该守护进程启动与该端口对应的服务器程序。它接管通信连接。每个服务都使用 `services` 或 `rpc` 文件定义的唯一端口号。

## 常见互联网服务

互联网服务分为两大类：一类是在加州大学伯利分校开发的，称为 Berkeley 服务；另一类是由美国国防部高级研究计划局开发的，称为 ARPA 服务。

Berkeley 服务包括 `BIND` (DNS)、`daemon`、`finger`、`rexec`、`rpc`、`rlogin`、`rsh`、`rup` 和 `rwho`。这些服务主要为 UNIX 平台开发；但现在它们大多数也适用于 Linux 和 Microsoft Windows 等非 UNIX 平台。Berkeley 服务的名称以“r”开头，因此也可以称为“r”服务。

另一方面，ARPA 服务包括 `ftp` 和 `telnet`，它们可以在 Linux 和非 Linux 平台上均使用。

表 24-1 列出了并描述了常见的互联网服务。

| 服务 |  |
| --- | --- |
| fingerd | 启用 `finger` 命令以显示本地和远程系统上的用户信息。`fingerd` 守护进程由 `xinetd` 启动，并使用 79 端口。 |
| ftppd | 允许与其他 Linux 和非 Linux 系统进行文件传输。客户端程序为 `ftp` 或其变体之一。`ftppd` 守护进程由 `xinetd` 启动，并使用 21 端口。基于 Kerberos 的安全 FTP 服务。 |
| gsship | 启用主机名到 IP 以及 IP 到主机名的解析。`named` 守护进程通过 `nslookup`、`dig` 和 `host` 响应查询命令。 |
| ntpd | 保持系统与更可靠、更准确的时间源同步。 |
| rcp | 允许你执行文件复制。该协议使用 469 端口。|-|
| rexecd | 允许在远程系统上执行命令。该守护进程由 `xinetd` 启动。 |
| rsync | 允许你使用差异法执行文件复制。该守护进程由 `xinetd` 启动，并使用 873 端口。 |
| sendmail | `Sendmail` 是大型网络和互联网上最常用的邮件传输代理。它与各种客户端邮件程序配合工作，并使用 25 端口。 |
| telnetd | 允许用户登录远程系统。客户端程序为 `telnet`。`telnetd` 由 `xinetd` 启动，并使用 23 端口。 |
| tfipd | 与 `boots` 配合启用/禁用系统，并允许 Kickstart 客户端传输包含启动和其他配置数据的文件。客户端程序为 `tfip`。`tfipd` 由 `xinetd` 启动，并使用 69 端口。 |

### 表 24-1 Internet 服务

### xinetd 守护进程、/etc/xinetd.conf 文件和 /etc/xinetd.d 目录

`xinetd` 守护进程是许多互联网服务的父守护进程。当执行 `/etc/rc.d/init.xinetdd` 脚本时，该守护进程会在系统启动时自动启动。它代表 `/etc/xinetd.d` 目录和 `/etc/xinetd.conf` 文件中列出的服务，在 `services` 和 `rpc` 文件定义的端口上监听连接请求，并在请求到达时启动适当的服务器进程。当对 `xinetd.conf` 文件或 `xinetd.d` 目录中的文件进行更改，或者向 `xinetd` 目录添加或删除文件时，你都需要使用以下命令重新加载配置：

```bash
# service xinetd reload
```

此外，如果需要手动启动、停止或重启守护进程，请执行上述命令并根据需要传递 `start`、`stop` 或 `restart` 参数。你还需要通过运行以下命令来确保守护进程配置为在每次系统重启时自动启动：

```
# chconfig --list xinetd
xinetd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
```

如果不是开启状态，请运行以下命令：

```bash
# chconfig --xinetd on
```

`xinetd.conf` 文件的默认内容类似于所示：
