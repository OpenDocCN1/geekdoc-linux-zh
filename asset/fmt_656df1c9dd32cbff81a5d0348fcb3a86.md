
`apt-get install samba-common smbclient swat`

`/etc/init.d/samba start`

- Gentle——对于 Gentle，你需要在内核中配置 `net-fs` 支持以使用 Samba 服务器功能。安装 `net-fs` 软件包 (`emerge-fs`) 应该可以让你获得所需的包。要启动服务，运行 `rc-update` 并立即启动服务：

```
emer samba

rc-update add samba default

/etc/init.d/samba start
```

- Fedora 和 Red Hat Linux 系统——你需要在 Fedora 中使用 Samba，需要安装 `samba`、`samba-client`、`samba-common`，以及可选的 `system-config-samba` 和 `samba-swat` 软件包。然后你可以使用 `service` 和 `chkconfig` 命令启动 Samba，如下：

```
service smb start

chkconfig smb on
```

在大多数使用 Samba 的 Linux 系统上，命令和配置文件是相同的。Samba 项目本身提供了一个基于 Web 的界面来管理 Samba，称为 Web 管理工具 `SWAT`。对于第一次设置 Samba 的人来说，`SWAT` 是让其运行起来的好方法。

### 注意

如果你的 Linux 安装没有提供适用于 Samba 的帮助文档，请查阅 Samba 项目主页 (`www.samba.org`) 上的文档。此外，检查 `SWAT` 自带的详细帮助信息。

# 使用 SWAT 配置 Samba

除了提供丰富的 Samba 选项接口外，`SWAT` 还带有一个优秀的帮助功能。如果你需要从另一台计算机管理 Samba，可以配置 `SWAT` 远程访问，并通过要求管理员登录和密码来确保安全。

## 开启 SWAT 服务

在使用 `SWAT` 之前，你必须进行一些配置。你必须做的第一件事是开启 `SWAT` 服务，这在不同的 Linux 发行版中方法不同。

是在 Fedora 和 Red Hat Enterprise Linux 系统中设置 `SWAT` 的方法：

- 在终端窗口中以 root 用户身份输入以下内容来开启 `SWAT` 服务：

```
# chkconfig swat on
```

- 通过如下方式重启 `inetd` 启动脚本来使更改生效：

```
# service inetd restart
```

诸如 Debian、Slackware 和 Gentoo 等 Linux 发行版通过 `inetd` 监督守护进程开启 `SWAT` 服务。在安装 `SWAT` 后，你只需删除 `/etc/inetd.conf` 文件中 `SWAT` 行前的注释字符（以 root 用户身份，使用任何文本编辑器）并重启守护进程。以下是 Ubuntu 中 `SWAT` 的示例：

```
# service inetd restart
```

`samba` 守护进程使你添加到你的 Linux 系统中的文件共享和打印服务供 Windows 客户端计算机使用。`Samba` 软件包支持以下客户端计算机：

- Windows 9x
- Windows NT
- Windows ME
- Windows 2000
- Windows 2007
- Windows XP
- Windows Vista
- Windows for workgroups
- MS Client 3.0 for DOS
- OS/2
- Dave for Macintosh computers
- Mac OS X
- Samba for Linux

### 注意

Mac OS X 服务器附带了 Samba，因此你可以将 Macintosh 系统作为服务器。本章讨论的是如何使用 Linux 系统作为服务器。然后你可以拥有 Macintosh、Windows 或 Linux 客户端计算机。此外，Mac OS X 同时附带了 Samba 的客户端和服务器软件。

## 启动 SWAT

当你完成后，输入以下内容：

```
http://localhost/
```

### 提示

使用 GUI 更改配置可能会丢失你手动输入的某些信息。在编辑之前，为 `/etc/samba/smb.conf` 备份。

## 在 SWAT 中创建全局设置

一组全局设置影响文件和打印共享通常的方式。这些设置出现在 `/etc/samba/smb.conf` 中的 `[global]` 标题下。要查看和编辑全局变量，点击 `SWAT` 上的 `GLOBALS` 按钮。

## 选项

以下选项与你的 Samba 服务器的基本信息相关：

- `Workgroup`——与 Samba 组关联的工作组名称。此字段的默认值为 `WORKGROUP`。
- `Realm`——如果你使用 kerberos 验证，此值指示要使用的 realm。通常由服务器的主机名反映。
- `NetBIOS`——分配给此 Samba 服务器的名称。你可以使用与你的 DNS 主机名相同的名称，也可以留空，这将会自动使用 DNS 主机名。你的 DNS 主机名已填充。
- `NetBIOS alias`——允许你使用与 TCP/IP DNS 名称不同的主机计算机别名。
- `Server string`——标识服务器的字符串。此名称出现在打印机注释框等地方。默认显示为 Samba 和版本号。
- `Interfaces`——允许你使用多个网络接口并让 Samba 浏览不同的子网。此字段的格式可以是 IP 地址/子网掩码。或者，你可以指定计算机上的第一块以太网接口（如 `eth0`）。例如，一个 C 类网络地址可能显示为

```
192.168.24.11/255.255.255.0
```
