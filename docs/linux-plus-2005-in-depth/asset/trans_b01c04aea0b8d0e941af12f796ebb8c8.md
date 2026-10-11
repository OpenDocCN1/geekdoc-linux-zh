
option routers 192.168.1.254;

option domain-name-servers 192.168.1.200;

subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.1 192.168.1.100
}

[root@server1 root]# ~

请注意，根据上述输出，DHCP 服务器为客户端分配了介于 192.168.1.1 和 192.168.1.100 之间的 IP 地址，租约时间为 36,000 秒。此外，DHCP 服务器还将客户端的默认网关配置为 192.168.1.254，DNS 服务器配置为 192.168.1.200。

在 `/etc/dhcpd.conf` 文件配置了相应信息后，您可以使用命令 `/etc/rc.d/init.d/dhcpd start` 启动 DHCP 守护进程，并通过检查 `/var/lib/dhcpd/dhcpd.leases` 文件来查看当前的 DHCP 租约。与 *daemon* 的名称类似，如果您修改了 `/etc/dhcpd.conf` 配置文件，必须重新启动 DHCP 守护进程。

## 配置 Apache

Apache 是世界上最常见的 Web 服务器。回顾一下，Web 服务器使用超文本传输协议 (HTTP) 从目录树中的特定目录分发 HTML 文件和其他 Web 内容。此目录称为文档根目录，其中包含服务器上使用的默认网站。在 Red Hat Fedora Core 2 中，默认的文档根目录是 `/var/www/html`，从此目录分发的默认文档是 `index.html`。Apache 的大多数配置选项都在一个大型配置文件中设置；默认情况下，该配置文件是 `/etc/httpd/conf/httpd.conf`。`httpd.conf` 文件中的每一行都称为指令。表 15-4 列出了一些常见指令。

### 表 15-4 常见的 httpd.conf 指令

| 指令 | 描述 |
| :--- | :--- |
| Listen 80 | 指定 Apache 守护进程将在端口 80 上监听 HTTP 请求 |
| ServerName server1.class.com | 指定本地服务器的名称为 server1.class.com |
| DocumentRoot "/var/www/html" | 指定本地计算机的文档根目录为 /var/www/html |
| DirectoryIndex index.html | 指定将发送 index.html 文件给请求 HTML 文档的客户端 |
| ErrorLog /var/log/httpd/error_log | 指定所有 Apache 守护进程消息将写入 /var/log/httpd/error_log 文件 |
| MaxClients 150 | 将最大同时请求数设置为 150 |
| User apache | 指定 Apache 守护进程将作为 "apache" 本地用户账户运行 |
| Group apache | 指定 Apache 守护进程将作为 "apache" 本地组账户运行 |
| <Directory /var/www/html><br>Order allow,deny<br>Allow from all<br>Deny from 192.168.1.51<br></Directory> | 指定除 IP 地址为 192.168.1.51 的计算机外，所有主机都允许访问 /var/www/html 目录中的 HTML 文件和其他 Web 内容 |

`httpd.conf` 文件中的默认设置对于大多数简单的 Web 服务器来说已经足够；因此，您只需要将相应的 HTML 文件（包括 `index.html` 文件）复制到 `/var/www/html` 目录，并启动 Apache Web 服务器守护进程（`/etc/rc.d/init.d/httpd start`），即可在网络上托管 Web 内容。如果您更改文档根目录内的 HTML 内容，无需重新启动 Apache 守护进程。但是，如果您更改了 `httpd.conf` 的内容，则需要重新启动 Apache 守护进程以激活这些更改。

## 配置 Samba

目前网络上最常见的客户端计算机操作系统是 Windows。回顾前一章，Windows 计算机使用服务器消息块 (SMB) 格式化 TCP/IP 数据。因此，为了向 Windows 客户端计算机共享信息，您可以使用 Samba 守护进程，它模拟了 SMB 协议。此外，Windows 计算机使用 NetBIOS 协议广播其计算机名称；因此，您可以使用 NetBIOS 名称守护进程来创建和广播 Windows 计算机可以使用的 NetBIOS 名称，以便连接到您的 Linux 服务器。

当 Windows 客户端计算机使用 SMB 访问共享目录时，Windows 用户名和密码会随访问该共享目录的请求一起传输，该请求仅允许特定用户访问。因此，您应为每个 Windows 用户创建本地 Linux 用户账户，并使用 **smbpasswd** 命令为他们创建 Samba 密码，该密码应与他们在 Windows 计算机上使用的密码匹配，如下面的输出所示：

```
[root@server1 root]# useradd mary
[root@server1 root]# passwd mary
Changing password for user mary.
New UNIX password: ******
Retype new UNIX password: ******
passwd: all authentication tokens updated successfully.
[root@server1 root]# smbpasswd -a mary
New SMB password: ******
Retype new SMB password: ******
Added user mary.
[root@server1 root]# _
```

接下来，您可以编辑 Samba 的主配置文件；在 Red Hat Fedora Core 2 中，此文件默认为 */etc/samba/smb.conf*。与 Apache 的 *httpd.conf* 文件一样，*smb.conf* 包含可用于设置 NetBIOS 名称、服务器设置、共享目录和共享打印机的指令。默认情况下，*smb.conf* 文件共享所有打印机和主目录（针对经过重新识别的 Windows 用户）；但是，您需要在此文件的 [global] 部分下添加一行以设置您的 NetBIOS 名称。例如，要将 NetBIOS 名称设置为 *server1*，您可以将指令 *netbios name = server1* 添加到 *smb.conf* 文件中。

最后，您可以使用命令 */etc/rc.d/init.d/smb start* 启动 Samba 和 NetBIOS 名称守护进程。与 Apache 一样，如果您修改了 *smb.conf* 文件，必须重新启动 Samba 和 NetBIOS 名称守护进程。

> **注意**
>
> 已经开发了许多用于修改 *smb.conf* 文件并简化使用 Samba 共享资源的工具。例如，在 Red Hat Fedora Core 2 中，您可以在桌面环境中使用 *system-config-samba* 命令。

## 配置 NFS

网络文件系统 (NFS) 允许 UNIX 和 Linux 计算机透明地共享文件。在 NFS 中，一台计算机通过将该目录的名称放入 */etc/exports* 文件来共享目录树中的某个目录（这一过程称为 *导出*），另一台计算机可以使用 *mount* 命令在本地计算机上挂载该远程目录，从而通过网络访问该目录，如第 14 章“网络配置”中所述。要配置 NFS 服务器，您可以执行以下步骤：

1. 创建一个目录，其中包含要共享给客户端计算机的信息。虽然您可以使用现有目录，但尽量避免这样做，以免意外允许客户端计算机查看或修改现有系统文件。
2. 接下来，编辑 */etc/exports* 文件并添加一行，列出要共享的目录和适当的选项。例如，*/etc/exports* 文件中的以下行将 */source* 目录共享给计算机 *server1*，允许用户读写数据，并确保 root 用户在 NFS 服务器上被视为匿名用户，同时将 */admin* 目录共享给所有用户，允许用户读写数据：

```
/source    server1(rw,root_squash)
/admin     (rw)
```

保存对文件的更改并返回命令提示符。

3. 运行命令 `exportfs -a` 以从 `/etc/exports` 文件更新内存中的导出文件系统列表。
4. 在命令提示符处输入以下命令并按 `Enter` 键来重启 NFS 进程：

```
/etc/rc.init.d/nfs restart
/etc/rc.init.d/nfslock restart
```

## 配置 FTP

当今在公共网络上用于传输文件的最常见协议是文件传输协议 (FTP)。大多数操作系统都附带一个 FTP 客户端程序，它可以连接到 FTP 服务器，该服务器为主目录提供文件目录供用户下载到他们的计算机，如第 14 章所述。FTP 托管文件的方式与 NFS 不同。可以为任何希望连接的用户（称为匿名访问）提供特殊的目录，或者只要用户在 FTP 客户端程序中输入有效的用户名和密码，用户就可以连接到 FTP 服务器上的其主目录。最常见的 FTP 服务器程序是华盛顿大学 FTP 守护进程 (wu-ftpd)。要配置 wu-ftpd 为其他计算机托管文件供下载，前提是他们以用户 "user1" 的身份登录并使用有效的密码，您可以执行以下步骤：

1. 在 user1 的主目录下创建一个目录来托管文件，并确保 user1 拥有此目录。
2. 接下来，编辑 `/etc/xinetd.d/wu-ftpd` 文件并更改以下行：

   ```text
   disable  =  yes
   ```

   使其读作：

   ```text
   disable  =  no
   ```
3. 保存对文件的更改并返回命令提示符。
4. 在命令提示符处，运行命令 `/etc/init.d/xinetd restart` 以重启 Internet 超级守护进程。

接下来，您可以运行 ftp 客户端实用程序以 user1 的身份登录 FTP 服务器，并进入 /home/user1 目录。默认情况下，您被阻止以 root 用户身份登录 wu-ftpd。要更改此设置，只需从 `/etc/ftpusers` 文件中删除 root 行，并从 `/etc/ftpaccess` 文件中删除 deny-uid % 99 %65534- 和 deny-gid % 99 %65534- 行；这允许名为 root 的用户以及 UID 小于 99 的用户通过 FTP 登录。

默认授予匿名 FTP 访问权限；任何使用 ftp 客户端实用程序以用户 "anonymous" 身份登录的用户将被放置在 /var/ftp 目录中。只需执行之前显示的第 2 步和第 3 步，以确保 FTP 守护进程已启动。

不幸的是，您必须从互联网下载 wu-ftpd 软件包，因为 Red Hat Fedora Core 2 不包含它。相反，Fedora Core 2 提供了 Very Secure FTP 守护进程 (vsftpd)；它是一个独立的守护进程，比……

