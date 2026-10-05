

# 跨网络自动化备份

设置一个智能备份系统，监控文件夹并将数据复制到您的服务器。

在您的网络上建立集中式备份方案对您的客户非常有用；他们不需要担心处理工作。你可以方便地在网络中选择的任何位置进行备份。UrBackup 是一款免费的开源备份软件，支持 Unix 和 Windows 客户端。虽然 UrBackup 极其精简，但它具有一些重要、易用且高效的核心功能（例如如果从多个客户端备份同一个文件，它仅保留一份副本）、对我们的文件进行可靠备份，以及简单的安装过程。

UrBackup 可以安装在大多数 Linux 发行版以及像 Synology 这样的 Windows 设备上。将在 Ubuntu 上安装 UrBackup。我们将使用以下命令安装 UrBackup 服务器：

```
$ sudo apt-get update
sudo apt-get install urbackup-server
```

在安装过程中，安装程序会询问备份位置。请选择可用空间最大的文件夹。如果你想对备份进行压缩，可以将位置设置在 Btrfs 或 ZFS 格式的分区上。为了增加额外的数据保护，你还可以考虑将备份文件存储在 RAID 5 上，以便在磁盘故障时可以轻松恢复数据。毕竟，集中式备份服务器是关重要的。

一旦 UrBackup 服务器运行，你可以通过 http://localhost:5684 访问 Web 界面。默认凭据为 admin/password。进入 Settings（设置），然后点击 create（创建）。在此处输入用户密码并点击创建。如果你想通过电子邮件接收通知，可以通过 Settings > Mail 配置 SMTP 设置。如果你想编辑备份文件夹位置，可以在 General（常规） > Backup Storage Path（备份存储路径）中找到。其他所有项均为默认设置。

## UrBackup 客户端设置

UrBackup 客户端适用于 Linux（包括 Arch Linux）和 Windows，可以在 https://www.urbackup.org/download.html 获取。下载并安装最新版本即可。UrBackup 客户端支持自动发现服务器，一旦配置完成，你就可以指定想要备份的文件夹，然后从服务器 Web 界面启动备份。

![](img/f4a034c4fbc20906a013558fa4e058a2_21_0.png)

## 备份状态

| 计算机名称 | 是否在线 | 上次文件备份 | 上次镜像备份 | 文件备份状态 | 镜像备份状态 |
| --- | --- | --- | --- | --- | --- |
| laptop | 是 | 2016-02-17 17:26 | 2016-02-17 17:26 | 21.4% | |

显示第 1 到 1 条记录

Rsync 是一种增量网络和远程文件复制工具。你可以使用 rsync 在网络上相互复制文件或目录。Rsync 仅传输文件中尚未传输的部分。对于文件，它会检查文件的哪些部分发生了变化，并仅传输这些部分。Rsync 是一个非常流行的传输工具。对于同一台计算机上的文件，可以使用以下命令：

```
$ rsync -fr source
```

此命令使用简单，但有不同之处：在这种情况下，传输将保留文件权限并保留部分文件。如果由于某种原因你在途中取消了传输，它将恢复执行。如果你断开了网络连接，那么……请记住，在这种情况下，发送端和接收端系统上都必须安装 rsync。

```
$ rsync -fr kun@192.168.1.48:/downloads
```

## 客户端下载

添加额外的互联网客户端

客户端名称：

## 互联网客户端

添加额外的互联网客户端

客户端名称：

## 额外客户端

主机名/IP

上述 UrBackup 显示了备份状态，并提供了客户端下载选项

![](img/f4a034c4fbc20906a013558fa4e058a2_21_1.png)

# 通过 SSH 和 VNC 远程访问文件

从世界任何地方通过命令行登录到您的服务器，或与远程机器共享桌面以获取图形用户界面（GUI）。

SSH（安全外壳）是远程登录系统的常用方法。OpenSSH 是最流行的 SSH 实现，适用于所有主流平台：Linux、Windows、Android、macOS。要安装 OpenSSH-server，请使用：

```
$ sudo apt-get install openssh-server
```

安装后，openssh-server 即可准备就绪，无需进一步配置。使用以下命令从远程机器登录：

```
$ ssh username@hostname
```

用户名应该已经存在于服务器上。默认情况下，OpenSSH 配置为密码认证。一种更安全的方法是使用公钥认证。在远程机器上生成公/私钥对：

```
$ ssh-keygen -t rsa
```

上述命令将为你生成两个文件。它们位于 ~/.ssh/id_rsa 和 id_rsa.pub。id_rsa 是你的私钥——不要与任何人共享。复制 id_rsa.pub（公钥）的内容，并将其放置在远程服务器的 ~/.ssh/authorized_keys 文件夹中。下次，你将无需密码即可登录。

![](img/f4a034c4fbc20906a013558fa4e058a2_22_0.png)

# 访问 Windows

几乎所有现代 Windows 操作系统都开发了远程桌面连接（通常称为 RDP 功能），你可以用它访问远程计算机上的桌面服务。这包括 Windows 7、8、10 和 11。请注意，Windows 家庭版不支持连接到远程桌面。Windows 家庭版可以使用 VNC 或 Remmina 连接到远程机器。Remmina 正在活跃开发，并提供了安装 Windows 的完整功能：

```
sudo apt-get update
sudo apt-get install remmina-remmina-plugin-rdp
remmina-plugin-vnc
```

# 用于远程桌面会话的 TightVNC

VNC 是一个使用 RFB 协议实现的桌面共享系统，用于通过网络共享当前桌面。VNC 可以为服务器的多个用户同时提供隔离的桌面环境。这意味着所有用户都可以在自己的桌面上运行桌面，而互不干扰。

```
$ sudo apt-get install tightvncserver xfce4-goodies xfce4-server
```

我们还安装了轻量级桌面环境 Xfce，我们将用它为远程用户启动 GUI 会话。使用 Autocut 在主机和客户端之间添加复制粘贴支持。我们需要配置桌面环境，创建 ~/.vnc/ 并添加：

```
$ /bin/bash
startxfce4 &
```

使用 `sudo chmod +x startup` 使其具有可执行权限。对于每个用户，必须创建一个服务实例，对于 VNC 服务器，你将为多个访问自己桌面的用户设置显示号和分辨率，然后你需要为每个用户创建一个启动文件，并在服务文件中为用户分配不同的显示号。

你可以使用以下命令启动 VNC。这里是 VNC 服务器上运行的显示号。根据显示号，vncserver 将位于 :5900。如果显示号是 1，它位于 5901。现在你需要使用任何 VNC 客户端连接服务器，在这种情况下应为 <服务器地址>:5900。

# 设置文件和媒体服务器以共享数据

在家里流传输你的电影、音乐和相册。下面的 Plex 有一个界面，可以让你轻松跟进设置文件服务器。最常用的服务器之一是 Samba。由于其共享协议，它适用于所有平台，包括 Linux、macOS、Windows、Android。要安装 Samba 服务器，请参考以下包：

```
$ sudo apt-get install samba-common
```

你可以通过编辑 /etc/samba.conf 文件配置 Samba 服务器。让我们从全局部分开始。在这里我们设置标识服务器的工作组：

```
workgroup = GROUP
server string = Samba
map to guest = Bad User
```

设置日志：

```
log file=/var/log/samba
```

设置访客账户：

```
guest account = myguestuser
```

设置访客共享（无密码）：

```
[SharedFolder]
path=/media/SharedFolder
```

![](img/f4a034c4fbc20906a013558fa4e058a2_23_0.png)

下面的 Plex 可以帮助 BBC Player 等网络电视频道。文件服务器允许通过网络扩展自己的存储。

```
comment = My Shared Folder
writeable = yes
browse = yes
```

此共享将映射到访客账户，确保用户具有访问 /MyShared 的权限。你可以从 Windows、Linux 和 Mac 计算机访问共享文件夹。此文件可以使用 URL //服务器IP地址/MyShared 进行访问。为了创建一个密码保护的共享，添加一个组：

```
$ sudo addgroup smbgrp
```

将用户添加到组：

```
adduser user1 -G smbgrp
```

然后为用户创建 Samba 密码：

```
$ smbpasswd -a user1
```

现在你有一个想要共享的用户：user1。该用户将拥有访问文件夹的所有权限。最后一步是在 smb.conf 中创建共享：

```
[ProtectedShare]
path=/home/user1/shared
```

![](img/f4a034c4fbc20906a013558fa4e058a2_23_1.png)

