
需要注意的是，NFS 默认会忽略 Root（超级用户）权限。因此，即使你以 `root` 权限登录，任何相关操作默认都会被忽略。这是一种安全措施，防止系统被远程接管。尽管如果需要，可以按共享范围授予 `root` 权限。

首先，必须为你要挂载的 NFS 共享创建一个挂载点，输入：`sudo mkdir -p /var/nfs/myshare`。需要注意的是，这些目录 `/var/nfs` 和 `/var/nfs/myshare` 将具有 `777` 权限，输入：`sudo chmod -R 777 /var/nfs/myshare`。

要配置共享的权限，你需要将它们添加到 `/etc/exports` 文件中。你将为想要共享的每个目录创建一行。例如：`share_directory client_ip_address(share_option1,...)`。

- `rw`：授予客户端计算机对共享内容的读写权限。
- `sync`：此选项强制 NFS 在回复之前写入本地存储。
- `no_subtree_check`：此选项防止子树检查，具有轻微的安全影响。但在某些情况下可以提高性能。
- `no_root_squash`：默认情况下，NFS 将远程 `root` 用户转换为服务器上的非特权用户。此选项禁用了这种行为。

在修改 `/etc/exports` 文件后，必须重启 NFS 服务使更改生效，输入：`sudo service nfs-kernel-server restart`

## 为 NFS 设置防火墙

如果主机上运行了防火墙（通常情况下如此），你需要在防火墙上开放特定端口，以便 NFS 服务对远程系统可用。

**注意：** *本节假设你的电脑上安装了 `UFW` 工具来管理防火墙。有关 `UFW` 工具的更多信息，请参见下一节“让 IPTABLES 简单”。*

你首先想做的是检查防火墙状态，输入：`sudo ufw status`

**注意：** *如果防火墙未启用，建议启用此功能。*

查看防火墙启用了哪些应用程序，输入：`sudo ufw app list`

**注意：** *`UFW` 工具将检查 `/etc/services` 以服务使用的端口和协议。*

要将端口添加到防火墙，输入：`sudo ufw allow from any to any port nfs`

需要注意的是，NFS 最佳实践建议限制连接到特定的客户端，输入：`sudo ufw allow from 192.168.0.100 to any port nfs`

要安装 NFS 客户端，请输入：

`sudo apt-get install nfs-common`

-或者-

`sudo yum install nfs-utils`

接下来，你必须创建作为客户端 NFS 挂载点的目录，输入：

`sudo mkdir -p /var/nfs/remoteshare`

执行 NFS 挂载命令以访问远程共享，输入：

`sudo mount 192.169.0.100:/var/nfs/myshare /var/nfs/remoteshare`

要在每次重新启动时自动挂载 NFS 共享，你需要在 `/etc/fstab` 文件中添加一行，例如：

`192.169.0.100:/var/nfs/myshare /var/nfs/remoteshare nfs auto 0 0`

显示所有已连接的 NFS 挂载点，输入：

`mount`

-或者-

`df -h`

## 锁定 NFS 服务（可选）

将 NFS 服务锁定为仅允许你想要授予权限的远程服务器访问。你需要告诉系统仅接受来自已批准远程设备的连接。这是一个多步骤过程，首先你必须告诉系统阻止所有连接，除非是已批准的连接。

要阻止所有未经批准的客户端连接到 NFS 服务。打开 `/etc/hosts.deny` 文件，然后添加以下行：

`rpcbind mountd nfsd statd lockd rquotad : ALL`

要授予系统或设备连接服务的权限，请将 IP 地址（或）添加到以下文件中。打开 `/etc/hosts.allow` 文件，然后添加以下行：

`rpcbind mountd nfsd statd lockd rquotad : approved_IP_address_list` 修改权限文件后，你必须重启 NFS 服务使更改生效，输入：

`sudo service nfs-kernel-server restart`

**注意：** *有三个 NFS 配置文件：`/etc/default/nfs-kernel-server`、`/etc/default/nfs-common`, `/etc/exports`*

# Samba 快速指南

Samba 是一项允许 Linux 托管或访问基于 Microsoft SMB 的资源的服务，例如跨网络的文件共享、打印机和其他计算机资源。通过此服务，Linux 客户端可以连接到基于 Microsoft SMB 的网络，并与其他 Windows 服务器和客户端共享文件。

通过此服务，Linux 服务器也可以托管基于 Microsoft SMB 的网络文件共享，以便其他 Windows 客户端可以访问它们。尽管如此，本书中未涵盖此功能，可能会包含在未来的版本中。

## 安装 Samba 服务

要安装 Samba 服务，请输入：

`sudo apt-get install samba`

## 安全文件共享

要对 Samba 文件共享设置密码保护，你需要创建一个名为 "`smbgrp`" 的组，并为每个用户设置密码。

`$ sudo addgroup smbgrp`

`$ sudo usermod user_name -aG smbgrp`

`$ sudo smbpasswd -a user_name`

**注意：** *`user_name` 账户必须属于本地系统，否则无法保存。*

## 配置 Samba

为你的 Samba 共享创建一个目录，输入：`mkdir ~/samba_share/`

**注意：** *用于创建存储共享文件的安全目录。`sudo mkdir -p /srv/samba/secure_shares` 接下来，在目录上设置适当的权限。`sudo chmod -R 0770 /srv/samba/secure_shares` `sudo chown -R root:smbgrp /srv/samba/secure_shares`*

编辑 Samba 配置文件，输入：

`nano /etc/samba/smb.conf`

在文件末尾，添加以下行：

```
[sambashare]
comment = My Samba Share
path = /home/user_name/samba_share
read only = no
browsable = yes
```

（要保存文件并退出编辑器，按 `Ctrl+X`，输入：`y` 并按回车）有更多更高级的指令用于创建不同类型的共享（例如：只读、读写、仅限匿名等）。要使更改生效，你必须重启 Samba 守护进程，输入：

`sudo systemctl restart smbd`

-或者-

`sudo service smbd restart`

**提示：** *要测试你当前的 Samba 设置，输入：`testparm`*

## 连接到 SMB 共享

打开 X-Windows 中的默认文件管理器，点击“连接到服务器”（Connect to Server），输入：

`smb://domain_or_ip_address/sambashare`

### 在 UFW 防火墙中启用 Samba

如果你的系统上启用了 `UFW` 防火墙，你必须添加以下规则以允许 Samba 流量通过防火墙。根据你所在的网络类型，你可能需要更改这些命令以指定正确的 IP 范围（示例中为 C 类）。

`sudo ufw allow proto udp to any port 137 from 192.168.1.0/24`

`sudo ufw allow proto udp to any port 138 from 192.168.1.0/24`

`sudo ufw allow proto udp to any port 139 from 192.168.1.0/24`

`sudo ufw allow proto tcp to any port 445 from 192.168.1.0/24`

# 安装 SSH 服务

Secure Shell (`SSH`) 是一种加密通道，允许你连接到远程服务器。它取代了旧的 Telnet，后者提供的是明文通信。

# /PROC 虚拟文件

`/proc` 目录是一个虚拟文件系统，提供了有关进程、内核等的信息。这对于系统性能分析非常有用。

# 使用 Git（针对初学者）

`git` 是众所知的 VCS（或版本控制系统）。基本上，像 `git` 这样的 VCS 被程序员（以及许多其他人）常用于存储源代码（或其他类型的内容）、跟踪对其进行的更改（也称为“版本”），并通过将其公开供像你这样的人下载或贡献来共享它。

*搜索“图形化 Git 客户端”*
