
此命令使用 `sjones` 账户将 `smbsrv` 上的 `images` 共享挂载到 `/usr/local/graphics`。文件将由 `nobody`（UID 为 `65534`）拥有，并且对所有用户可读（文件权限为 `0444`，目录权限为 `0555`），但对任何人不可写。

发出 `mount_smbfs` 命令后，除非你包含 `-N` 选项，否则你会被要求输入密码。要使用此选项，你需要在运行 `mount_smbfs` 的用户的主目录中（通常是 `root`）有一个 `/usr/local/etc/nsmb.conf` 文件或 `~/.nsmbrc` 文件。此文件包含根据服务器分组的详细信息。在没有密码的情况下挂载共享的基本信息具有以下形式：

```
{servername:username:sharename}
password=pass
```

你也可以添加其他选项。例如，`workgroup=wgnme` 行设置工作组，因此你可以省略 `-w` 命令行选项。你可以使用 `addr=ip-address` 选项设置服务器的 IP 地址。

> 注意：如果你将密码存储在 `nsmb.conf` 或 `.nsmbrc` 文件中，这些密码可能可被其他人访问。请务必将文件的权限设置为 `0600`，以防止其他人读取它。对于 `nsmb.conf`，该文件应由 `root` 拥有；对于 `.nsmbrc`，则应由运行 `mount_smbfs` 命令的用户拥有。

通常，只有 `root` 可以使用 `mount_smbfs`。如果你想赋予普通用户挂载 SMB/CIFS 共享的能力，你可以使 `mount_smbfs` 程序变为 SUID `root`，如第 8 章所述：

```
# chmod a+s /sbin/mount_smbfs
```

## 第 24 章：网络工具

### 注意

*进行此更改可能存在风险；如果 `mount_smbfs` 中存在漏洞，恶意用户可能会以不可预测的方式利用它。即使没有漏洞，挂载 SMB/CIFS 共享的功能也可能被滥用；例如，恶意用户可能通过标准 FreeBSD 目录（如 `/etc`）挂载共享，从而更改任意安全设置或文件。*

当你使用完通过 `mount_smbfs` 挂载的共享后，你可以像卸载任何已挂载的分区或共享一样，使用 `umount` 将其卸载：

```
# umount /usr/local/graphics
```

### 远程登录客户端

远程登录客户端使你能像在本地一样访问远程系统。你可以运行驻留在这些系统上的程序，查看存储在这些系统上的数据文件，等等。第 21 章描述了在远程系统上提供此功能的登录服务器。本节介绍了两种常见的文本模式远程登录客户端。

#### 提示

*GUI 远程登录客户端在第 21 章中与其匹配的服务器一起描述。*

#### 使用 Telnet 客户端

FreeBSD 的 Telnet 客户端在基本操作上相当直接——输入 `telnet`，后跟你要连接的主机名或 IP 地址。如果一切顺利，你会看到密码提示，然后你就可以登录：

```
$ telnet barroom.threeroomco.com
Trying 192.168.1.1...
Connected to barroom.threeroomco.com.
Escape character is '^]'.
Password:

Copyright (c) 1992-2002 The FreeBSD Project.
Copyright (c) 1979, 1980, 1983, 1986, 1988, 1989, 1991, 1992, 1993, 1994
The Regents of the University of California. All rights reserved

FreeBSD 5.0-RELENG1 #0: Sun Apr 7 02:51:42 GMT 2002
bash-2.05f
```

此命令尝试连接到 `barroom.threeroomco.com` 的 Telnet 服务器。默认情况下，FreeBSD 的 `telnet` 会透明地将你的用户名发送给 Telnet 服务器，因此你不需要输入它，只需输入你的密码（密码不会在屏幕上回显）。如果你需要以其他用户的身份登录，你可以使用 `-l username` 选项传入你的用户名。

登录后，你可以运行大多数文本模式程序——编辑器、邮件阅读器、编译器等等。你甚至可以使用 `su` 获取超级用户权限，并通过 `sysinstall` 或其他文本模式工具管理系统。正如第 21 章所述，你可以输入几个命令，然后从你的 Telnet 登录中启动基于 X 的程序。

**注意**

虽然你可以使用 `su` 从 Telnet 登录获取超级用户权限，但这样做几乎总是不明智的。Telnet 默认不加密密码，因此如果恶意用户在网络上安装了嗅探器，使用 Telnet 进行系统管理会将你的 `root` 密码暴露给恶意用户去窃取。最好使用 SSH 来执行远程系统管理。

由于 Telnet 以未加密的形式发送所有数据（包括你的密码），Telnet 最好保留给少数人使用的小型隔离网络（如未连接到互联网的住宅网络）。在较大的网络或当流量通过互联网时，最好使用 SSH 进行远程文本访问。

#### 使用 SSH 客户端

SSH 的工作方式与 Telnet 非常相似，但它将加密作为协议的标准部分。此加密适用于用户名、密码以及通过连接发送的所有数据。与 FreeBSD 的 `telnet` 一样，`ssh` 客户端程序会自动发送你的用户名，因此你在连接时不需要指定远程系统上的用户名。SSH 登录看起来像这样：

```
$ ssh barseom.threeroomco.com
The authenticity of host 'barseom.threeroomco.com (192.168.1.6)'
can't be established.
RSA key fingerprint is 48:17:8e:1c:da:ab:81:fe:01:76:bc:a4:f1:90:ff:00.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'barseom.threeroomco.com' (RSA) to the list
of known hosts.
jbarse@barseom.threeroomco.com's password:
Last login: Mon Jun 3 00:26:45 2002 from speaker
Copyright (c) 1980, 1983, 1986, 1988, 1990, 1991, 1993, 1994
The Regents of the University of California.  All rights reserved
FreeBSD 5.0-DELI (GENERIC) #0: Sun Apr 7 02:51:42 GMT 2002
bash-2.05$
```

此输出异常冗长，因为这是首次连接。SSH 客户端将其连接到的所有服务器的加密标识符存储在用户主目录中的 `.ssh/known_hosts` 和 `.ssh/known_hosts2` 文件中。如果找不到服务器信息或其与已存储的信息不匹配，`ssh` 会通知你该事实，并在继续之前要求确认。这种做法旨在防范攻击，例如恶意用户接管已知 SSH 服务器的 IP 地址以拦截密码。如果你批准连接或服务器的身份得到自动确认，`ssh` 会询问你的密码，如果验证通过，你就登录了。

此时，你几乎可以执行从 Telnet 登录所能执行的任何操作——运行基于文本的程序、将 X 重定向以使用本地显示器等。正如第 21 章所述，SSH 还支持隧道其他协议——即拦截通常使用非 SSH 协议和端口的数据，并通过 SSH 连接发送这些数据，从而对原本未加密的数据进行加密。隧道的最常见用途之一是隧道 X 连接。你可以通过在 `ssh` 命令行上使用 `-X` 选项来激活此功能。或者，你可以将以下行添加到 `/etc/ssh/ssh_config` 中以实现此任务：

> ForwardX11 yes

当然，服务器也必须配置为转发 X 连接，如第 21 章所述。`/etc/ssh/ssh_config` 文件还支持设置各种其他选项，但标准的 FreeBSD 配置将所有选项设置为其默认值。

## 总结

在 FreeBSD 工作站上运行的网络客户端在许多环境中都非常重要。一些客户端（如邮件阅读器和 web 浏览器）有助于提供与外部世界的连接，使你能够与同事协作、与朋友和家人沟通、进行在线研究等等。其他工具（如文件共享客户端）更常用于本地网络，并通过启用资源共享来贡献办公室生产力或网络效率。仍然有其他工具（如 FTP 客户端和远程登录客户端），可以根据你的需求仅用于本地网络或更广泛地使用。在大多数情况下，FreeBSD 提供多种网络客户端程序的选择，从而满足许多人的需求和偏好。

## 完整参考

![](img/f34d37e3abe9f4517128e54f80ab2616_636_0.png)

## 第 25 章

办公工具
