
放置在公共可访问的 FTP 目录中（通常是 `/var/ftp`）。登录后，您会收到接受 FTP 命令的 `ftp>` 提示符；表 14-2 展示了常见的 FTP 命令列表。

# **注意**

大多数 FTP 服务器要求用户在以匿名用户身份登录时输入密码；此密码通常是您的电子邮件地址。

### **表 14-2 常见的 FTP 命令**

| **命令** | **描述** |
| :--- | :--- |
| help | 显示命令列表 |
| pwd | 显示远程计算机上的当前目录 |
| dir, ls | 显示远程计算机上的目录列表 |
| cd *directory* | 将远程计算机上的当前目录更改为 *directory* |
| lcd *directory* | 将本地计算机上的当前目录更改为 *directory* |
| get *filename* | 将 *filename* 下载到本地计算机的当前目录 |
| ascii | 指定文本文件下载（默认） |
| binary | 指定二进制文件下载 |
| mget *filename* | 将 *filename* 下载到本地计算机的当前目录；它还允许使用通配符元字符来指定 *filename* |
| put *filename* | 将 *filename* 从本地计算机的当前目录上传到远程计算机的当前目录 |
| mput *filename* | 将 *filename* 从本地计算机的当前目录上传到远程计算机的当前目录；它还允许使用通配符元字符来指定 *filename* |
| ! | 在本地计算机上运行 shell |
| close | 关闭与远程计算机的 FTP 连接 |
| open *hostname or IP* | 打开到指定 *hostname or IP* 地址的 FTP 连接 |
| bye, quit | 退出 FTP 实用程序 |

在 FTP 会话期间显示的确切输出因 FTP 服务器上使用的 FTP 软件版本不同而略有差异。以下输出示例是使用 ftp 实用程序以 root 用户身份连接到名为 ftp.sampledomain.com 的 FTP 服务器：

```
[root@server1 root]# ftp ftp.sampledomain.com
Connected to ftp.sampledomain.com.
220 www.sampledomain.com FTP server (Version wu-2.6.1-18) ready.
331 Please login with USER and PASS.
530 Please login with USER and PASS.
KRB5ERROR_W4 rejected as an authentication type
Name (ftp.sampledomain.com:root): root
331 Password required for root.
Password:
230 User root logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

在上述输出中，远程计算机上的当前目录是 root 用户的主目录。要验证此信息并查看要下载的文件列表，您可以在 ftp> 提示符下使用以下命令：

```
ftp> pwd
257 "/root" is current directory.
ftp> ls
227 Entering Passive Mode (192,168,0,1,56,88)
150 Opening ASCII mode data connection for directory listing.
total 2064
-rw-r--r--    1 root     root      1756 Aug 14 08:48 file1
-rw-r--r--    1 root     root       160 Aug 14 08:48 file2
-rw-r--r--    1 root     root    1039996 Aug 14 08:39 file3
drwxr-xr-x    2 root     root      4096 Aug 14 08:50 stuff
226 Transfer complete.
ftp>
```

上述输出显示有三个文件和一个子目录。要将 file3 下载到本地计算机的当前目录，您可以使用以下命令：

```
ftp> get file3
local: file3 remote: file3
227 Entering Passive Mode (192,168,0,1,137,37)
150 Opening BINARY mode data connection for file3 (1039996 bytes).
226 Transfer complete.
ftp>
```

![](img/09bf13b782f71165e17bb3839040c96a_568_0.png)

# **注意**

如果您的 Internet 连接速度较慢，您可以改为使用 `get file3.gz` 命令。FTP 服务会自动使用 gzip 实用程序对 file3 进行压缩，然后再进行传输。

同样，要将远程计算机上的当前目录更改为 /root/stuff，并将本地计算机当前目录中 file4 的副本上传到该目录，同时查看结果并退出 ftp 实用程序，您可以在 ftp> 提示符下使用以下命令：

```
ftp> cd stuff
250 CWD command successful.
ftp> pwd
257 "/root/stuff" is current directory.
ftp> mput file4
mput file4? y
227 Entering Passive Mode (192,168,0,1,70,109)
150 Opening BINARY mode data connection for file4.
226 Transfer complete.
929 bytes sent in 0.00019 seconds (4.8e+03 Kbytes/s)
ftp> ls
227 Entering Passive Mode (192,168,0,1,235,35)
150 Opening ASCII mode data connection for directory listing.
total 8
-rw-r--r--    1 root    root        929 Aug 14 09:26 file4
226 Transfer complete.
ftp> bye
[root@server1 root]#
```

## 使用 NFS 访问文件

尽管不如 FTP 常见，但网络文件系统（NFS）是另一种在 UNIX 和 Linux 计算机之间传输文件的常用方法。要使用 NFS 访问文件，您只需将网络中已启动 NFS 守护进程的远程计算机上的某个目录挂载到本地目录即可。只需将 nfs 文件系统类型、服务器名称或 IP 地址、远程目录和本地目录作为 mount 命令的参数即可。例如，要使用 NFS 将名为 nfs.sampledomain.com（IP 地址 192.168.0.1）的远程计算机上的 /var 目录挂载到本地计算机上的 /mnt 目录并查看结果，您可以使用以下命令：

```
[root@server1 root]# mount -t nfs nfs.sampledomain.com:/var /mnt
[root@server1 root]# mount
/dev/hda1 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/shm type tmpfs (rw)
sunrpc on /var/lib/nfs/rpc_pipefs (rw)
nfsd on /proc/fs/nfsd type nfsd (rw)
192.168.0.1:/var on /mnt type nfs (rw,addr=192.168.0.1)
[root@server1 root]# ls /mnt
arpwatch ftp kerberos lock mailman nis run tux
cache gdm lib log mars_nwe opt spool www
db iptraf local mail named preserve tmp yp
[root@server1 root]#
```

现在，您可以像使用其他任何本地目录一样使用 /mnt 目录；所有文件操作都是在远程计算机上的 /var 目录中执行的。随后可以使用 umount 命令正常卸载 NFS 文件系统。

## 访问 Windows 文件

NFS 是将信息传输到 Linux 和 UNIX 计算机及从它们传输信息的常用方法；但是，很难找到适用于 Microsoft Windows 操作系统的 NFS 软件。要将信息传输到共享的 Windows 目录及从该目录传输，您可以像 NFS 一样将该目录挂载到本地 Linux 目录；但是，文件系统类型必须是 smbfs。

> **注意**
> SMB 代表 Server Message Block（服务器消息块）。它定义了 Microsoft 计算机用于跨网络传输信息的格式。

例如，要将名为 accounting 的共享目录从名为 windowxsp 的 Windows 计算机挂载到 /mnt 目录并查看结果，您可以使用以下命令：

```
[root@server1 root]# mount -t smbfs //windowxsp/accounting /mnt
[root@server1 root]# mount
/dev/hda1 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/shm type tmpfs (rw)
sunrpc on /var/lib/nfs/rpc_pipefs (rw)
//windowxsp/accounting on /mnt type smbfs (0)
```

```
[root@server1 root]# ls /mnt
Final Exam.doc Part 0.DOC Part 2.doc Part 4.doc Part 6.doc
homework questions.doc Part 1.DOC Part 3.DOC Part 5.DOC TOC.doc [root@server1 root]#
```

![](img/09bf13b782f71165e17bb3839040c96a_570_0.png)

# **注意**

> smbmount 命令也可以用于挂载 Windows 共享目录。命令 smbmount //windowsxp/accounting /mnt 等同于前文输出中用于挂载 accounting 目录的命令。

与 NFS 一样，可以使用 umount 命令从本地 /mnt 目录卸载 Windows 共享目录。

在 Linux 和 Windows 计算机之间共享文件时，另一个有用的实用程序是 smbclient 实用程序。要查看之前使用的 windowsxp 计算机的信息，您可以使用以下命令：

```
[root@server1 root]# smbclient -L windowsxp
added interface ip=192.168.0.1 bcast=192.168.255.255 nmask=255.255.0.0
Got a positive name query response from 192.168.0.1 ( 192.168.0.1 65.95.133.77 )
Password:
Domain=[HOME] OS=[Windows 5.1] Server=[Windows 2000 LAN Manager]
```

| 共享名 | 类型 | 注释 |
| --- | --- | --- |
| IPC$ | IPC | 远程 IPC |
| print$ | 磁盘 | 打印机驱动 |
| movies | 磁盘 | |
| My Jams | 磁盘 | |
| HPLaserJ | 打印机 | HP LaserJet 6P/6MP PostScript |
| accounting | 磁盘 | |
| ADMIN$ | 磁盘 | 远程管理 |
| C$ | 磁盘 | 默认共享 |

| 服务器 | 注释 |
| --- | --- |
| WINDOWSXP | |

| 工作组 | 注释 |
| --- | --- |
| HOME | WINDOWSXP |

```
[root@server1 root]#
```
