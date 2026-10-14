
# service nfs reload # 重新加载已导出的共享目录
# exports -rv # 重新加载已导出的共享目录
# exports -rv Verb # 详细重载已导出的共享
exporting client.example.com:/export/myshare
exporting *:/mnt/public

从 Linux 服务器系统，你可以使用 `showmount` 命令查看本地系统可用的哪些目录。例如：

```bash
# /usr/bin/showmount -e
Export list for server.example.com
/export/myshare client.example.com
/mnt/public
```

从客户端系统，你可以使用 `showmount` 命令查看从选定计算机可用的哪些目录。例如：

```bash
# /usr/bin/showmount -e server.example.com
/export/myshare client.example.com
/mnt/public
```

## 挂载 NFS 共享

使用 `mount` 命令将远程 NFS 共享挂载到本地计算机上。这是一个示例：

```bash
# mkdir /mnt/server-share
# mount server.example.com:/export/myshare /mnt/server-share
```

此示例说明了 NFS 服务器 (server.example.com) 和来自该服务器的共享目录 (/export/myshare)。本地挂载点必须在挂载共享之前存在，出现在命令的末尾 (/mnt/server-share)。

通过添加 `-o` 选项传递 NFS 特有选项给 `mount` 命令：

```bash
# mount -o rw,hard,int server.example.com:/export/myshare /mnt/server-share
```

`rw` 选项在权限允许的情况下以读写权限挂载远程目录。设置 `hard` 后，当读取或写入操作超时时，使用服务器的用户将看到服务器响应消息。如果发生这种情况，设置 `intr` 选项允许你中断指向远程服务器的挂起请求 (Ctrl+c)。

默认情况下使用 NFS 版本 3 (nfs3) 协议连接共享。要使用专为通过互联网和防火墙工作设计的 NFS 版本 4，请在命令行上如下指定该协议为文件系统类型：

```bash
# mount -t nfs4 server.example.com: /mnt/server-share
```

将此作为指南。你需要先创建挂载点目录。而且，你应该确保已按照你的喜好配置了 NFS。

> 注意：取决于你使用的 SUSE 版本，NFS v4 的实现可能不够健壮，无法用于生产。通过 SSH 隧道传输 NFS 错误可能更或更可靠。你可以通过搜索“nfs ssh”查找更多此主题的信息，访问 www.howforge.org/nfs_ssh_tunneling 和 http://tldp.org/HOWTO/HOWTO-security.html 了解更多关于安全和 NFS 的信息。

## 使用 Samba 共享远程目录

Samba 是 Windows 文件打印协议的开源实现，最初被称为服务器管理块 (SMB)，现在称为通用文件系统 (CIFS)。Linux 以及许多其他操作系统都有 Samba 的实现。用于共享、查询和监控共享目录的图形化工具。

# 第 12 章：访问网络资源

要查看更简洁的输出，请使用 -b 选项：

```
$ smstatus -b
```

## 查找 Samba 主机

NetBIOS 名称用于识别 Samba 中的主机。你可以使用 `nmblookup` 命令在本地子网上广播特定的 NetBIOS 名称，以确定计算机的 IP 地址：

```
$ nmblookup thompson
querying thompson on 192.168.1.255
192.168.1.1 server1<0>
```

要查找特定子网上服务器的 IP 地址，请使用 -U 选项：

```
$ nmblookup -U 192.168.1.255 server1
querying server1 on 192.168.1.255
192.168.1.1 server1<0>
```

## 检查 Samba 配置

如果你无法使用 Samba 服务器或在与 Samba 服务器通信时遇到其他问题，可以测试服务器上的 Samba 配置。可以使用 `testparam` 命令来检查主 Samba 配置文件 (smb.conf)：

```
$ testparam
Load smb config files from /etc/samba/smb.conf
Processing section "homes"
Processing section "profiles"
Processing section "users"
Processing section "groups"
Processing section "printers"
Processing section "print$"
Processing section "myshare"
Loaded services file OK.
Server role: ROLE_STANDALONE
Press Enter to see a dump of your service definitions
```

按照指示按回车键后，你可以看到 smb.conf 文件的设置。这里是之前示例中使用的 myshare 共享目录条目，它可能出现在 smb.conf 文件中：

```
[myshare]
path = /home/francois
username = francois
valid users = francois
hosts allow = einstein
available = yes
```

此项允许 Samba 用户 francois 从主机 endianian 访问 /home/francois 目录（由 myshare 共享名称表示）。

该共享显示当前可用。

之前的 `testparam` 示例显示了你在 smb.conf 中设置的条目。但它没有显示你未设置的所有默认条目。你可以使用 -v 选项查看这些内容。将其通过到 `less` 命令以分页查看设置：

```
$ testparam -v | less
```

如果你想在配置文件生效前对其进行测试，可以告诉 `testparm` 使用 /etc/samba/smb.conf 以外的文件：

```
$ testparm /etc/samba/test-smb.conf
```

## 使用 SSHFS 共享远程目录

通过 SSH 协议可以做的另一个神奇魔术是挂载远程文件系统。使用 SSH 文件系统 (sshfs)（它是 sshfs 软件包的一部分），你可以从本地 Linux 系统挂载你的用户账户可以访问的 SSH 服务器上的任何目录。sshfs 为挂载操作以及所有传输的数据提供了加密。sshfs 的另一个酷炫之处是它在服务器端不需要任何设置（运行该服务除外）。

以下是从远程服务器将文档目录挂载到本地目录的快速步骤。这只需要远程服务器运行 SSH、可以访问，并且你所需的目录对服务器上的用户账户是可访问的。在这里，我们将来自主机 10.0.0.50 的名为 /var/docs 的命名目录挂载到本地系统名为 /mnt/docs 的挂载点：

```
$ mkdir /mnt/docs
$ sshfs chris@10.0.0.50:/var/docs /mnt/docs
Create mount point
Mount remote directory
```

当你完成对远程目录的使用后，可以使用 `fusermount` 命令将其卸载：

```
$ fusermount -u /mnt/docs
Unmount remote directory
## 在 IRC 中与朋友聊天

尽管即时消息软件已经出现，但互联网中继聊天 (IRC) 今日仍被许多人使用。Freenode.net 拥有许多支持开源软件项目的聊天室。事实上，许多人全天登录其中，只看着他们喜爱的 Linux 项目的讨论不断滚动。这被称为“潜水”（lurking）。

xchat 实用是一个很好的图形化、多操作系统的 IRC 客户端。使用 IRC 的高级方式是在始终开启的机器（如旧服务器）上在 screen 中运行文本模式客户端。另一个更简单的选项是使用 IRC 代理客户端，也称为弹器（bouncer），例如 dircproxy。

原始的 IRC 客户端是 ircII。允许脚本（在某些方面类似于生产力套件中的宏）自动化了一些命令并增加了可用性。最受欢迎的是 Vagasso 开发的 Phoenix。然后是<unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk> [content]
