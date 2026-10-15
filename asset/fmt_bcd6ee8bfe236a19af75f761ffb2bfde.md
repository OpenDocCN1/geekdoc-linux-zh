
Linux-Windows 网络集成最常见的方法是让 Linux 系统作为网络上 Windows 客户端的文件和打印服务器。这是通过使用 Samba 实现的。Samba 是一个软件集合，使 Linux 能够支持 SMB（Server Message Block）协议，该协议是 Windows 网络文件和打印共享的基础。基于 Linux 的 SMB 服务器可能的客户端包括 LAN Manager、Windows 95/98/Me、Windows NT/2000、OS/2 以及其他 Linux 系统。

# 安装 Samba

完整的 Samba 软件包并未随书中附 Red Hat Linux 7.1 光盘提供。但是，如果你有那两张光盘，你可能在安装 Linux 时已经安装了 Samba。你可以使用 `rpm` 命令进行检查：

```
$ rpm -q samba
$ rpm -q samba-client
$ rpm -q samba-common
```

如果你发现没有安装 Samba，可以从适当的 Red Hat CD-ROM 通过将 CD-ROM 挂载到本地位置（例如 `/mnt/cdrom`），然后使用 `rpm` 安装三个 Samba 软件包：

```
# rpm -i /mnt/cdrom/RedHat/RPMS/samba-2.0.7-36.i386
# rpm -i /mnt/cdrom/RedHat/RPMS/samba-client-2.0.7-36.i386
# rpm -i /mnt/cdrom/RedHat/RPMS/samba-common-2.0.7-36.i386
```

随附的出版版光盘仅包含 `samba-client` 和 `samba-common` 软件包。虽然这足够从局域网上的 Microsoft Windows 连接共享资源（见后文中的 `smbmount` 命令），但不足以从你的 Linux 向同一网络上的 Microsoft Windows 共享资源。

# 从互联网安装 Samba

如果你想要最新版本的 Samba，可以下载最新的 Samba 源码或 RPM。请按照 Samba 网站 `http://www.samba.org` 的说明查找最新版本。NetBIOS 名称通常与主机名相同，少于 15 个字符。

# 安装了哪些内容

当你安装 Samba 时，会安装几个文件：

- `/usr/sbin/smbd` 处理连接的 Samba 服务器
- `/usr/sbin/nmbd` 允许客户端定位的 NetBIOS 服务器
- `/usr/bin/smclient` 用于访问 SMB 的基础 Samba 客户端
- `/etc/samba/smb.conf` 配置文件

# 配置 Samba

整个 Samba 配置现在包含在 `/etc/samba/smb.conf` 中。`smb.conf` 文件由多个条目组成。例如：

```
[tmp]
comment = Temporary file space
path = /tmp
read only = no
public = yes
```

## [global] 部分

大多数 `smb.conf` 文件以 `[global]` 部分开头，定义影响 Samba 整体行为的参数。`[global]` 部分的常用参数包括：

- `printing`: 指定使用的打印系统；除非你使用的是旧版本的 Linux。
- `printcap name`: 指定 printcap 文件的位置；通常是 `/etc/printcap`。
- `load printers`: 如果共享打印机，应设置为 `yes`。
- `guest account`: 指定连接时使用的用户；大多数 Linux 管理员将其设置为 `nobody`。
- `workgroup`: 指定 Samba 服务器所属的 Windows 工作组或域。
- `security`: 指定如何验证访问用户。四个选项：`user`、`server`、`domain` 和 `share`。

`user` 从本地 `/etc/passwd` 文件检查用户名和密码。这是最常见且最简单的选项。

`server` 从 `server` 参数指定的 Windows NT/2000 域服务器进行验证。

`domain`: 需要将 Samba 服务器的 NetBIOS 名称添加到相应的域控制器中。

`share`: 将 Linux 设置为对等点网络的一部分，这是 Microsoft Windows 式工作负载的特征。

考虑典型服务器中的 `[global]` 部分：

```
[global]
printing = lprng
printcap name = /etc/printcap
load printers = yes
guest account = nobody
workgroup = testgroup
security = user
```

该部分指定了打印系统类型，设置来账户使用 Linux 用户 `nobody`，使服务器成为 `testgroup` 工作负载的一部分，并指定 Samba 使用本地 `/etc/passwd` 文件进行验证。

`comment` 参数提供了关于该部分的额外信息，但不会影响其运行。`browseable` 参数用于指示其他用户是否可以浏览目录；将其设置为 `no` 将限制只有具有权限的用户访问。`read only` 参数设置为 `no`，以便用户可以在其主目录中读取和写入文件。`preserve case` 和 `short case` 参数确保不区分大小写的 Windows 系统不会更改文件名中字母的大小写，因为 Linux 是区分大小写的。最后，`create mode` 参数指定了通过 Samba 连接的用户所创建的文件应赋予什么权限；在示例中，`0755` 表示文件对所有者可读、可写、可执行，对同组组的用户可读、可执行，而对其他人禁止访问。

为了让用户能够从 Windows 系统访问其主目录，他们必须使用其用户名作为共享名称。例如，用户用于访问 `smbserv` 上的主目录的用户名，他们应该访问 `\smbserv\username`。

## [printers] 部分

由于 `[homes]` 部分用于共享所有用户的主目录，因此 `[printers]` 部分用于将所有 Linux 打印机共享到 Windows 网络。

表 29.1 列出了 `[printers]` 部分中的常用参数。

表 29.1：常用 `[printers]` 部分参数

| 参数 |  |
| --- | --- |
| comment | 提供关于该部分的信息，但不影响其运行。 |
| path | 指定打印池路径；你可能想为 Samba 创建自己的打印池目录并将其指向该处。（例如，Red Hat Linux 创建了 `/var/spool/samba` 并指向那里。） |
| browseable | 与主目录一样，将此参数设置为 `no` 可确保只有具有权限的用户才能浏览打印机。 |
| printable | 这应设置为 `yes`，否则打印将无法工作。（如何向不可打印的打印机打印呢？） |
| public | 如果设置为 `yes`，则来账户可以打印；在许多网络中，将此参数设置为 `no` 以防止来用户过度打印是明智的。 |
| writable | 打印机不可写，因此此参数应设置为 `no`。 |
| create mode | 此参数指定打印过程中创建的打印池文件的权限；这通常设置为 `0700`。 |

这些参数结合起来可以用于产生相当常见的 `[printers]` 部分，如下例所示的默认 Red Hat Linux 部分：

```
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
printable = yes
public = no
writable = no
create mode = 0700
```

从 Windows 访问 Linux 打印机的方法与访问目录相同。共享名称是 `printcap` 文件中的 Linux 打印机名称。例如，要访问 `smbserv` 上的 `printername` 打印机，Windows 用户应该访问 `\smbserv\printername`。

## 共享用于公共访问的目录

有时，需要创建一个所有用户都可以访问且只读的公共访问目录。该目录可以配置为集中式共享信息，从而防止用户修改信息。

考虑以下条目：

```
[public]
path = /public/directory
public = yes
read only = yes
printable = no
```

这创建了一个名为 `public` 的共享，所有用户都可以访问（因此 `public = yes`），但它是只读的（因此 `read only = yes`）。

考虑另一个示例：共享 `/tmp` 作为一个所有用户都可读可写的公共访问临时目录。这这可以通过以下条目实现：

```
[tmp]
path = /tmp
read only = no
public = yes
```

## 共享用于私有访问的目录
