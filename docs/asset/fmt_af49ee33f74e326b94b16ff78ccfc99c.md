
使用这些 FTP 客户端，你可以与 FTP 服务器建立会话（而不是像 `wget` 和 `curl` 那样获取文件）。你可以像操作本地文件系统一样导航服务器，跨网络连接获取和存放文档。以下是使用 `ftp` 连接到 FTP 服务器的示例：

*(此处省略重复的示例代码，见上文)*

# 第 12 章：访问网络资源

使用 `-p` 选项可以保留复制文件的权限和时间戳：

```
$ scp -p myfile server1:/tmp/
```

如果 SSH 服务配置为监听在默认端口 22 以外的端口，请在 `scp` 命令行中使用 `-P` 来指明该端口：

```
$ scp -P 12345 myfile server1:/tmp/      连接到特定端口
```

若要从远程文件系统的特定位置进行递归复制，请使用 `-r` 选项：

```
$ scp -r mydir francois@server1:/tmp/      将所有 mydir 复制到远程 /tmp
```

虽然 `scp` 在你知道需要复制的文件确切位置时最有用，但某些情况下，通过交互式方式浏览和传输文件会更有帮助性。

## 在 sftp 和 lftp 会话中复制远程文件

`sftp` 命令允许你使用类似于 FTP 的接口通过 SSH 协议查找和复制文件。以下是启动 `sftp` 会话的示例：

```
$ sftp chris@server1
chris@server1:password: ******
sftp>
```

像使用普通 FTP 客户端一样使用 `sftp`。输入 `?` 可命令列表。你可以更改目录 (`cd`)、更改本地目录 (`lcd`)、检查当前和远程目录 (`pwd` 和 `lpwd`)，以及列出远程和本地计数 (`ls` 和 `ll`)。根据你登录用户的权限，你可能可以创建和删除目录 (`mkdir` 和 `rmdir`)，并更改文件和目录的权限 (`chmod`) 以及所有者/组 (`chown` 和 `chgrp`)。

你也可以将 `lftp`（在本章前面的部分讨论过）作为 `sftp` 客户端。使用 `lftp` 可以增加一些用户友好的功能，例如在 Tab 键下下进行路径自动补全：

```
$ lftp sftp://chris@server1
Password: ******
lftp chris@server1:->
```

## 使用 Windows 文件传输工具

在许多情况下，人们需要使用 Windows 客户端从 Linux 服务器获取文件。如果你的客户端操作系统是 Windows，你可以使用以下开源工具之一从 Linux 服务器获取文件：

- `WinSCP` (http://winscp.net) — 适用于 Windows 的 SSH1 和 SSH2 协议的图形化 `scp`、`sftp` 和 FTP 客户端。
- `FileZilla` (http://filezilla.sourceforge.net) — 在 Windows 中提供图形化客户端 FTP 和 SFTP 服务器，并提供 FTP 服务器功能。
- `PSCP` (www.chiark.greenend.org/~sgtatham/putty/) — PuTTY 套件的一部分的命令行 `scp` 客户端。
- `PSFTP` (www.chiark.greenend.org/~sgtatham/putty/) — PuTTY 组合件的一部分的命令行 `sftp` 客户端。

## 共享远程目录

本章到为止描述的工具实现了原子文件访问，即建立连接并一次性传输文件。在更具持久性的情况下，需要对远程文件目录进行访问，此时共享和挂载远程文件系统将最有用。此类服务包括网络文件系统 (`NFS`)、`Samba` 和 `SSHFS`。

## 使用 NFS 共享远程目录

假设服务器已运行 NFS 服务（在 Fedora 中以 root 身份运行 `service nfs start` 可启动它），你可以使用 `exports` 和 `showmount` 命令查看可用和已挂载的共享目录。挂载共享目录是通过标准 `mount` 命令的特殊选项完成的。

### 查看和导出 NFS 共享

在 NFS 服务器上运行此 `exports` 命令可显示该服务器上所有可用共享目录：

```
# /usr/bin/exports -v
/export/myshare client.example.com(ro,wdelay,root_squash,no_subtree_check)
  <world>(ro,wdelay,root_squash,no_subtree_check)
/mnt/public
```

正在共享的两个目录是 `/export/myshare`，第一个仅对主机 `client.example.com` 可用，而第二个对所有人可用。每个共享的选项显示在括号中。第一个共享为只读 (`ro`)；向服务器的写入将被延迟，以在导出更多写入时提高性能 (`wdelay`)；来自客户端 root 请求将映射为匿名 UID (`root_squash`)。此外，还会对文件系统权限进行较短的检查 (`no_subtree_check`)。第二个共享允许读写 (`rw`)。

通过修改 `/etc/exports` 文件来添加和修改 NFS 目录。要使更改生效，请以 root 身份执行以下任意命令：

```
# service nfs reload      重新加载导出的共享目录
# exportfs -r               重新加载导出的共享目录
# exportfs -rv              详细重新加载导出的共享
exporting client.example.com:/export/myshare
exporting *:/mnt/public
```

在 Linux 服务器系统上，你可以使用 `showmount` 命令查看本地系统可用的共享目录。例如：

```
# /usr/sbin/showmount -e
Export list for server.example.com
/export/myshare client.example.com
/mnt/public *
```

在客户端 Linux 系统上，你可以使用 `showmount` 命令查看所选计算机可用的共享目录。例如：

```
# /usr/sbin/showmount -e server.example.com
/export/myshare client.example.com
/mnt/public *
```

### 挂载 NFS 共享

使用 `mount` 命令挂载远程 NFS。以下是一个示例：

```
# mkdir /mnt/share
# mount server.example.com:/export/myshare /mnt/share
```

向 `mount` 命令传递 NFS 特有的选项：

```
# mount -o rw,hard,int server.example.com:/export/myshare /mnt/share
```

`rw` 选项允许读写访问。`hard` 选项确保在服务器不可用时客户端无限等待。`int` 选项设置请求超时。

> 注意：取决于你使用的 Fedora 版本，`NFS4` 的实现可能不够健壮。通过 SSH 隧道早期版本的 NFS 可能更安全、可靠。你可以在网上搜索“nfs ssh”获取更多信息。

## 使用 Samba 共享远程目录

`Samba` 是 Windows 文件和打印协议的开源实现，最初被称为消息块 (`SMB`)，现在称为通用网络文件系统 (`CIFS`)。`Samba` 不仅适用于 Linux，也适用于许多操作系统。

Windows 用于共享、查询和挂载共享目录的图形化工具包括 SWAT Web 管理工具。要在 Linux 中使用 SWAT 工具，安装 `samba-swat` 包，启用 `xinetd` 服务（输入 `xinetd`）并开启 SWAT（`chkconfig swat on`）。通过浏览器访问 SWAT 服务 (`http://localhost:901`) 并输入 root 用户名和密码。

用于 Samba 的命令可以查询 SMB 服务器、挂载目录和共享目录。要将现有的 Linux 用户添加为 Samba 用户，使用 `smbpasswd` 命令：

```
# smbpasswd -a francois
New SMB password: ******
Retype new SMB password: ******
Added user francois
```

### 第 12 章：访问网络资源

要列出服务器向匿名用户提供的服务，请输入以下命令：

```
$ smclient -l server
Password: *****
Anonymous login successful
Domain=[MYGROUP] OS=[Unix] Server=Samba 3.0.25a-3.fc7
tree connect failed: NT_ST_US_LOGON_FAILURE
```

以下是针对名为 `francois` 的特定用户的 `smclient` 输出：
