
- 您已在 Windows 机器与 Red Hat Linux 服务器之间允许基于明文的服务，例如 FTP 和 Telnet。
- 您的网络未连接到 Internet，因此使用明文密码不会对您的组织构成很大威胁。
- 您只想先让 Samba 正常工作，然后再处理加密密码，或计划长期将所有身份验证任务委托给 Windows NT 服务器。
- 使用加密密码进行身份验证。

您可能会选择第一个选项，因此接下来会进行描述。有关使用加密密码进行身份验证的详细信息，请参阅本章最后一节“Securing Your Samba Server。”

如果您使用的是 Windows 98、带有 Service Pack 3 或更高版本的 Windows 95，或带有 Service Pack 3 或更高版本的 Windows NT 4，请按照以下步骤启用明文密码：

- 1. 运行名为 RegEdit 的 Windows 注册表编辑器程序。
- 2. 对于 Windows 9x，定位以下注册表项：
```
/HKEY_LOCAL_MACHINE
/System
/CurrentControlSet
/Services
/VxD
/VNETSUP
```
对于带有 Service Pack 3 或更高版本的 Windows NT 4，定位以下注册表项：
```
/HKEY_LOCAL_MACHINE
/SYSTEM
/CurrentControlSet
/Services
/Rdr
/Parameters
```
- 3. 在注册表树中找到 VNETSUP 分支（适用于 Windows 9x）或 Parameters 分支（适用于 Windows NT）后，选择 编辑→ 新建 并选择创建新的 DWORD 值。
- 4. RegEdit 将在注册表中插入一个名为 New Value #1 的新 DWORD 值。将此新值重命名为 EnablePlainTextPassword 并双击此新名称。
- 5. 弹出一个对话框，使您能够为刚创建的 EnablePlainTextPassword 设置值。将值输入为 1 并像平常一样关闭 RegEdit。
- 6. 重启您的 Windows 9x/NT 系统。

这可确保您的 Windows 9x/NT 系统能够使用明文密码进行 SMB 身份验证。

## 套接字选项

默认情况下，全局配置部分中的 socket options 参数设置为 TCP_NODELAY，这可在某些平台上增强 Samba 性能。应保持此参数不变。

## DNS 代理

此参数影响 Samba 套件内置的 Windows Internet 名称服务器 (nmbd) 在无法将 Windows 系统名称 (NetBIOS 名称) 解析为 IP 地址时的行为。如果将此参数设置为 yes，nmbd 服务器将把 NetBIOS 名称视为 Internet 域名并尝试使用 DNS 协议解析它。建议保持默认设置。

## 设置 [homes] 参数

[homes] 部分是一个特殊的配置部分，允许您从 Windows 系统设置主目录访问。换句话说，在 Red Hat 系统上具有有效用户名/密码的用户可以从 Windows 系统访问其在 Linux 系统上的主目录。默认的 [homes] 配置如下：

```
[homes]
    comment = Home Directories
```
```
browseable = no
writable = yes
```

以下是您可以更改这些参数的方法。

- **comment.** 正如其名称所示。将其设置为您想要的任何内容。
- **browseable.** 控制主目录是否在浏览器列表中可见（例如“网络邻居”）或从 Windows 命令提示符使用 NET VIEW 命令时是否可见。根据需要将其设置为 yes 或 no。
- **writable.** 控制用户是否可以写入自己的主目录。对于大多数实际用途，此项需要设置为 yes。如果将其设置为 no，用户将只能以只读方式访问自己的主目录。

## 设置 [printers] 参数

[printers] 部分仅在 Red Hat Linux 系统上连接有一个或多个打印机时才有用。默认的 [printers] 配置如下：

```
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
guest ok = no
writable = no
printable = yes
```

以下是您可以更改这些参数的方法。

- **comment.** 正如其名称所示。将其设置为您想要的任何内容。
- **path.** 将其设置为打印机数据文件将被 spool 的目录。如果用户很多，请确保该目录有足够的磁盘空间。
- **browseable.** 默认情况下，打印机在浏览器中不可见（例如网络邻居）或 NET VIEW 命令输出中不可见。要更改此行为，请将其设置为 yes。
- **guest ok.** 默认情况下，打印机服务对没有密码的访客用户不可用。要更改此行为，请将其设置为 yes。
- **printable.** 默认情况下，此参数允许打印。如果将其设置为 no，打印将被完全禁用。

默认配置包含许多已注释的配置参数和附加部分。请仔细检查这些选项并启用您想要使用的任何功能。但是，如果您第一次使用 Samba，请先使用默认配置使其正常工作。

## 通过 Web 管理 Samba

使用随 Samba 提供的新的基于 Web 的配置工具 SWAT，您可以使用标准 Web 浏览器管理 Samba。以下是如何使用 SWAT。

- 1. 验证您的 `/etc/services` 文件是否包含以下行：
```
swat 901/tcp
```
如果上述行不存在，请添加此行并保存 `/etc/services` 文件。
- 2. 验证您的 `/etc/inetd.conf` 文件是否包含以下行：
```
swat stream tcp nowait.400 root /usr/sbin/swat swat
```
如果上述行缺失或被注释掉，请添加或取消注释并保存 `/etc/inetd.conf` 文件。在这种情况下，使用 `killall -HUP inetd` 命令重启 inetd 守护进程。
- 3. 接下来，运行可以访问您的 Samba 服务器的任意 Web 浏览器。输入以下 URL：
```
http://your-samba-server:901/
```
- 4. 系统会要求您输入用户名和密码。将 root 输入为用户名并输入相应的密码。如果您输入了合适的用户名/密码组合，您将看到 SWAT 欢迎屏幕。
- 5. 单击可用链接以管理 Samba 的各个方面。

如果您计划从 Samba 服务器本身以外的机器访问 SWAT，应按如下方式对其进行保护：

- 1. 编辑 /etc/inetd.conf，使其包含以下行：
```
swat stream tcp nowait.400 root /usr/sbin/tcpd /usr/sbin/swat swat
```
- 2. 编辑 /etc/hosts.deny，使其包含以下行：
```
swat: ALL
```
- 3. 接下来，编辑 /etc/hosts.allow，使其包含如下行：
```
swat: IP-address-of-machine
```
这里的 IP-address-of-machine 是您计划运行将访问 SWAT 的 Web 浏览器的机器的 IP 地址。

您可以列出多个 IP 地址，只要它们至少用一个空格字符分隔即可。

## 测试 /etc/smb.conf 配置

只要您更改 Samba 配置文件，请运行随 Samba 包提供的 testparm 实用程序。当您从命令行运行此便捷实用程序时，它会检查 /etc/smb.conf 文件的语法并提供有用的警告和错误消息。由于配置错误的 /etc/smb.conf 文件可能成为安全漏洞，因此在修改此文件时请使用此实用程序。

## 启动、停止和重启 Samba 服务

在确保 /etc/smb.conf 文件无误后，您就可以启动 Samba 了。Samba 包包含两个守护进程。smbd 守护进程是 Samba 服务器，nmbd 守护进程是 NetBIOS 名称服务器。要启动守护进程，请以 root 身份运行以下命令：

```
/etc/rc.d/init.d/smb start
```
然后您可以从 Windows 计算机开始访问 Samba 服务器。要停止 Samba 服务器，请使用 stop 参数运行相同的命令。您也可以使用 restart 参数运行相同的命令来重启守护进程。

如果您想在启动时启动 Samba 服务，请按如下方式创建符号链接：

```
ln -s /etc/rc.d/init.d/smb  /etc/rc.d/rc3.d/S91smb
```
这将在 Red Hat Linux 服务器进入运行级别 3 时启动 Samba 服务，而运行级别 3 是所有多用户系统的默认运行级别。

如果您使用基于 X Window 系统的登录（使用 XDM）并希望自动启动 Samba，请创建以下链接：

```
ln -s /etc/rc.d/init.d/smb  /etc/rc.d/rc5.d/S91smb
```

## 在 Windows 上使用 Linux 文件服务器

在 Windows 上使用 Linux 文件服务器可能是 Linux/Windows 环境中的 Linux 管理员考虑使用 Samba 的最常见原因。例如，假设您想将名为 /intranet 的 Linux 分区（或目录）提供给 LAN 上的 Windows 用户组（john、mary 和 phil）使用。以下是您需要执行的操作：

- 1. 如果您将 [global] 配置部分中的 security 参数设置为 user 或 share，请在 Linux 系统上创建三个用户帐户（john、mary 和 phil）。这些用户帐户需要设置成每个帐户的密码与其 Windows 对应项匹配。例如，如果 jennifer 在其 Windows 系统上的密码设置为 tsk#tsk，那么您必须使用相同的密码设置她的 Linux 帐户。此外，在 /etc/group 中创建一个名为 intranet 的组，其中仅包含用户 jennifer、chad 和 phil 作为成员。
- 2. 修改 /etc/smb.conf 文件以添加以下内容：
```
[Intranet]
    comment = Intranet Directory
    path = /intranet
```
