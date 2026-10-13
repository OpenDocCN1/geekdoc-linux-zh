
```
# smbpasswd harris
New SMB password:
Retype new SMB password:
Password changed for user harris.
```

## 在 Windows 系统上访问共享文件（smbfs 文件系统）

SMB 文件共享可以双向工作。Samba 允许你将 FreeBSD 机器仅设置为 SMB 服务器，但也可以将其设置为客户端并像其他任何文件系统一样挂载远程 SMB 共享。这就是 smbfs，它在 FreeBSD 4.4 中作为标准内核模块提供，在更早版本中则位于 ports (/usr/ports/net/smbfs) 中。

FreeBSD 中的 smbfs 实现包括位于 /modules 中的 smbfs.ko 内核模块和位于 /sbin 中的 mount_smbfs 工具，其工作方式与用于挂载各种文件系统的所有其他 mount_* 工具类似。smbfs 最好的文档可在 man mount_smbfs 手册页中找到。

要使用 smbfs 挂载 SMB 文件系统，请使用 mount_smbfs 并带上几个基本选项。-I 标志指定主机名或 IP 地址，另外两个参数分别是远程共享名（格式为 //user@<NetBIOS name>/<share name>）和本地挂载点。要将名为 gaming-pc 的 Windows 机器上的名为 public 的共享挂载到本地 /smb/public 目录，请使用以下语法：

```
# mount_smbfs -I 64.41.131.139 //guest@gaming-pc/public /smb/public
```

系统会提示你输入密码。如果共享设置为允许完全访问，请使用空白密码；如果共享设置为只读或密码保护模式，请使用适当的密码。

![](img/ba0161b65b37e94cffc801ecbacaba5e_421_0.png)

> smbfs.ko 内核模块会在 mount_smbfs 需要时自动加载。如果你愿意，可以通过在 /boot/loader.conf 中添加以下行在启动时加载它：
> 
> smbfs_load='YES'
> 
> 然而，这可能并非必要。

要将 SMB 共享添加到 /etc/fstab，请使用以下语法：

```
//guest@gaming-pc/public  /smb/public  smbfs  rw,noauto  0  0
```

在启动期间发生的 mount -a 过程将在 FreeBSD 系统启动时自动挂载此共享。

## 摘要

在本课程关于 FreeBSD 的最后一小时中，你学习了如何使用多种协议将你的机器转变为文件共享服务器和客户端。你学习了如何设置 FTP 服务器，既可用于经过身份验证的用户，也可用于匿名用户。你学习了如何使用 NFS，在网络文件系统上双向共享文件。最后，你学习了如何设置基本的 Samba 配置，以便与本地网络上的 Windows 机器通信。

这些协议中的每一个，特别是 NFS 和 Samba，其灵活性远超本文所述；如果你有需要并有意愿，你将能够扩展对这些协议的了解，以提高你的文件共享机制的性能和便利性（以及安全性）至你所期望的任何水平。

## 问答

Q 使用 FTP 提供文件有什么意义？为什么不直接使用 HTTP？

A HTTP 确实取代了 FTP 存在的大部分目的，特别是在大型二进制下载（如软件归档）的情况下。然而，FTP 在其双通道连接模型（允许其穿过防火墙）、内置用户身份验证、能够上传文件并在服务器上执行文件系统操作，以及其传输机制针对支持大型二进制文件而非小型文本/HTML 文件（像 HTTP 那样）等方面具有优势。

Q 我的 /var 分区太小，无法容纳大型公共匿名 FTP 归档。

A 你可以在另一个更大的分区中创建一个位置来存放原本应放在 /var/ftp 中的内容。例如，将 /var/ftp 的内容移动到 /usr/ftp，然后使用以下命令在那里创建符号链接：

```
ln -s /usr/ftp /var/ftp.
```

Q 在本地网络上浏览 NFS 共享没有办法吗？

A 实际上有。名为服务定位协议（SLP）的系统可帮助局域网上的机器跟踪彼此的 NFS 服务。你可以从 ports 安装 OpenSLP（SLP 的免费实现），位于 /usr/ports/net/openslp。

Q 我的 NFS 挂载有时会冻结；有时解冻需要很长时间，在此期间我的终端会话被锁定。

A 请确保在挂载 NFS 共享时使用 -i 选项。这在本地网络上通常不是必要的；但如果你通过广域网挂载共享，并且连接偶尔导致挂载停滞，-i 选项可能是最佳选择。

Q 如何通过 AppleTalk 与 Macintosh 机器共享文件？

A 你需要安装位于 `/usr/ports/netatalk` 的 netatalk port。请注意，Mac OS X 也可以使用 NFS 和 SMB 以及 AppleTalk 来共享文件。

Q 配置 Samba 没有更用户友好的方法吗？

A 有一个名为 SWAT 的基于 Web 的管理工具，随 Samba port 一起安装。有关如何使用它的更多信息，请参阅 Samba 的网站（http://www.samba.org）。请注意，由于它必须能够修改系统配置文件，因此必须以特权用户身份运行，运行 SWAT 会带来许多潜在的安全漏洞。如果安装 SWAT，这些漏洞已在软件包中记录；请务必注意警告。

## 工作坊

本互动部分旨在通过测验问题巩固你对 FTP、NFS 和 Samba 的理解，并通过练习扩展你对这些工具使用的视野。

### 测验

+   1. FreeBSD 自带的默认 FTP 服务器是什么？
+      A. WU-FTPD
+      B. ProFTPD
+      C. BSD ftpd
+   2. 我应将用户名添加到哪个文件中以防止他们通过 FTP 登录？
+      A. `/etc/ftpusers`
+      B. `/etc/ftp/users`
+      C. `/etc/ftpbanned`
+      D. `/var/ftp/etc/ftpusers`
3. 哪个 NFS 挂载选项用于“后台化”挂载进程，使其不阻塞系统？
A. - i
B. -b
C. -T
D. noauto

4. nmbd 守护进程用于什么？
A. It does name services for Samba.
B. It services incoming NFS connection requests.
C. It services incoming Samba connection requests.
D. It maps incoming RPC calls to an unused server port.

5. 使用什么命令将 SMB 文件系统挂载到 FreeBSD 机器上？
A. mount
B. mount_nfs
C. mount_smbfs
D. mount -t smbfs

### 测验答案

1. 正确答案是 C。
2. 正确答案是 A。
3. 正确答案是 B，不过 A 也很有用。
4. 正确答案是 A。
5. 正确答案是 C 或 D。

### 练习

1. 你可能会发现 FreeBSD 内置的 FTP 服务器不符合你的需求。例如，你可能想要做复杂的按目录访问控制，或者你可能想要让用户能够即时获取整个目录树的 Zip 归档。你可以通过安装 ProFTPD 和 WU-FTPD 等替代 FTP 服务器来实现；两者都可在 ports 中找到，位于 /usr/ports/ftp。尝试安装 ProFTPD，看看其配置模型能为你提供什么好处。

2. 你可以设置 Samba 做远不止与对等 Windows 机器共享文件。你可以用它将 FreeBSD 机器加入 Windows 域，甚至作为整个 Windows 网络的域控制器。如果你手头有，可以尝试为家庭网络创建一个域并让各种 Windows 机器订阅它。这并不容易，但如果你能做到，这将是一项很棒的技能！

3. 本章讨论了 UNIX 和 Windows 内置的标准文件共享方法。然而，近年来备受关注的文件共享形式是内容为中心、点对点的那种，它由 Napster 开创，并在数十种不同的流行应用中延续，如 KaZaA、Morpheus 和 Gnutella。许多这些应用可用于 FreeBSD，要么作为直接 port，要么通过 Linux 二进制兼容层运行。在 `/usr/ports/net` 中，你会找到 eDonkey、gtk-gnutella、LimeWire 和 Mutella 等 port。如果你对那种让 RIAA 夜不能寐的文件共享感兴趣，可以尝试这些。请注意，大多数这些客户端需要 KDE 或 GNOME。
