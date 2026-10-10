
# 配置 Samba 服务器

当 Windows 客户端计算机通过 SMB 访问共享目录时，如果该共享目录仅允许特定用户访问，则 Windows 用户名和密码会随请求一起传输。因此，你应该首先为每个 Windows 用户创建本地 Linux 用户账户，并使用 `smbpasswd` 命令为他们创建与他们在 Windows 计算机上使用的密码相匹配的 Samba 密码，如下面的输出所示：

```text
[root@server1 ~]# useradd mary
[root@server1 ~]# passwd mary
Changing password for user mary.
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully.
[root@server1 ~]# smbpasswd -a mary
New SMB password:
Retype new SMB password:
Added user mary.
[root@server1 ~]# _
```

接下来，你可以编辑 Samba 的主配置文件 /etc/samba/smb.conf。与 Apache 配置文件类似，`smb.conf` 包含可用于设置 NetBIOS 名称、服务器设置、共享目录和共享打印机的指令。在大多数 Linux 系统中，`smb.conf` 文件中的默认设置会共享所有打印机和主目录（针对已识别的 Windows 用户）。但是，你需要在此文件的 `[global]` 部分下添加一行来设置你的 NetBIOS 名称。例如，要将 NetBIOS 名称设置为 `server1`，你可以在 `smb.conf` 文件中添加指令 `netbios name = server1`。与 Apache 一样，如果你修改了 `smb.conf` 文件，必须重启 Samba 和 NetBIOS 名称守护进程。

![](img/c27875544958897d817484d558c208c8_620_0.png)

> 你可以使用 `testparm` 命令来确保 /etc/samba/smb.conf 文件没有语法错误。因此，在编辑 /etc/samba/smb.conf 文件后运行此命令是一个良好的实践。

# 连接 Samba 服务器

配置完 Samba 后，你应该测试其功能，以确保其正常运行。为此，你可以登录到一个 Windows 客户端，并在“运行”对话框中输入 `\\Samba_server`，其中 `Samba_server` 是你的 Samba 服务器的 NetBIOS 名称或 IP 地址。如果成功，Windows 操作系统将打开一个新窗口，显示你的主目录、共享打印机以及你有权访问的其他共享目录，如图 13-6 所示。

![](img/c27875544958897d817484d558c208c8_621_0.png)

图 13-6 从 Windows 客户端访问 Samba 服务器

或者，你可以在 Linux 计算机上使用 `smbclient` 命令连接到你的 Samba 服务器。只需使用已建立的 Windows 用户账户的登录信息登录到 BASH 终端。然后运行 `smbclient -L Samba_server` 命令，其中 `Samba_server` 是你的 Samba 服务器的 NetBIOS 名称或 IP 地址。这将使用当前用户账户的凭据将你的计算机连接到 Samba 服务器，并列出共享目录和可用打印机，如下面的示例输出所示：

```text
[root@server1 ~]# smbclient -L server1
Enter root's password:
Domain=[WORKGROUP] OS=[Unix] Server=[Samba 4.1.6-Ubuntu]
    Sharename    Type    Comment
    ---------    ----    -------
    IPC$ IPC IPC Service(server1 server (Samba, Ubuntu))
    print$    Disk    Printer Drivers
    printer1 Printer    printer1
    stuff    Disk    Good Stuff
    Server    Comment
    ----    -------
    ALIENWARE
    SERVER1    server1 server (Samba, Ubuntu)
    Workgroup    Master
    -------    ------
    WORKGROUP    SERVER1
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_621_1.png)

你可以使用 `smbclient` 命令连接到 Samba 和 Windows 服务器。

此外，你还可以使用 `smbclient` 命令显示类似 FTP 的界面，用于在 Samba 或 Windows 服务器的共享目录之间传输文件。下面的输出演示了如何使用类似 FTP 的界面连接到 `server1` 上的 `stuff` 共享目录：

```bash
[root@server1 root]# smbclient //server1/stuff
Enter root's password:
Domain=[MYGROUP] OS=[Unix] Server=[ Samba 4.1.6-0buntu]
smb: \> dir
```

```text
  D    0 Mon Sep  6 22:28:12 2015
..    D    0 Mon Sep  6 22:28:12 2015
Final Exam.doc    A    26624 Mon Sep  6 23:17:30 2015
homework questions.doc    A    46080 Mon Sep  6 23:33:03 2015
Part 0.DOC    A    13312 Mon Sep  6 23:27:51 2015
Part 1.DOC    A    35328 Mon Sep  6 23:24:44 2015
Part 2.doc    A    70656 Mon Sep  6 23:25:28 2015
Part 3.DOC    A    38912 Mon Sep  6 23:26:07 2015
Part 4.doc    A    75776 Mon Sep  6 23:26:57 2015
Part 5.DOC    A    26624 Mon Sep  6 23:27:23 2015
Part 6.doc    A    59904 Mon Sep  6 23:05:32 2015
TOC.doc    A    58880 Mon Sep  6 23:09:16 2015
39032 blocks of size 262144. 14180 blocks available
```

```bash
smb: \> help
```

```text
?      allinfo      altname      archive    backup
blocksize cancel     case_sensitive cd       chmod
chown      close      del        dir      du
echo       exit       get        getfacl    getears
hardlink   help       history    iosize     lcd
link       lock       lowercase  ls       l
mask       md         mget       mkdir      more
mput       newer      notify     open       posix
posix_encrypt posix_open posix_mkdir posix_rmdir posix_unlink
print      prompt     put        pwd      q
queue      quit       readlink   rd       recurse
rget       rename     reput      rm       rmdir
showacl    setae      setmode    stat       symlink
tar        tarpmode   timeout    translate  unlock
volum      void       wdel       logon      listconnect
showconnect tcon     tdis       tid      logoff
..        !
smb: \> get TOC.doc
getting file \TOC.doc of size 58880 as TOC.doc (16.0 KiLoBytes/sec) (aver-age 16.0 KiLoBytes/sec)
smb: \> exit
[root@server1 root]# _
```

## NFS

网络文件系统（NFS）允许 UNIX、Linux 和 Macintosh OS X 计算机透明地共享文件。在 NFS 中，一台计算机通过在 /etc/exports 文件中放置该目录的名称来共享（或导出）目录树中的一个目录。另一台计算机然后可以使用 `mount` 命令将远程目录挂载到本地计算机上，从而通过网络访问该目录。

### 配置 Linux NFS 服务器

要在 Linux 中配置 NFS 服务器，请执行以下步骤：

- 1. 从软件仓库安装 NFS 服务器软件包。
- 2. 创建一个包含要共享到客户端计算机信息的目录。虽然你可以使用现有目录，但最好避免这样做，因为你可能会无意中让客户端计算机获得查看或修改现有系统文件的能力。
- 3. 编辑 /etc/exports 文件并添加一行，列出要共享的目录和适当的选项。例如，/etc/exports 文件中的以下行将 /source 目录共享到计算机 server1，允许用户读写数据，并确保 root 用户在 NFS 服务器上被视为匿名用户，同时还将 /admin 目录共享给所有用户，允许用户读写数据：

```
/source server1(rw,root_squash) /admin *(rw)
```

- 4. 保存你对 /etc/exports 文件的更改并返回命令提示符。
- 5. 运行 `exportfs -a` 命令以从 /etc/exports 文件更新内存中的导出文件系统列表。
- 6. 重启 NFS 守护进程。

![](img/c27875544958897d817484d558c208c8_623_0.png)

NFS 服务器软件包的名称因 Linux 发行版而异。在 Fedora 20 上，你可以安装 `nfs-utils` 软件包；在 Ubuntu Server 14.04 上，你可以安装 `nfs-kernel-server` 软件包。

![](img/c27875544958897d817484d558c208c8_623_1.png)

NFS 守护进程的名称是 `nfsd`。要重启此守护进程，你可以使用 Fedora 20 上的 `systemctl restart nfs.service` 命令或 Ubuntu Server 14.04 上的 `service nfs-kernel-server restart` 命令。

### 连接 Linux NFS 服务器

你可以使用 `showmount` 命令查看远程服务器上可用的 NFS 共享目录列表。例如，要查看服务器 `nfs.sampledomain.com` 上的共享目录列表，你可以使用以下命令：

```
[root@server1 ~]# showmount -e nfs.sampledomain.com
Export list for 192.168.1.104:
/var *
[root@server1 ~]# mount
```

从上述输出可以看出，`nfs.sampledomain.com` 服务器上的 /var 目录已共享给所有主机（*）。

要使用 NFS 访问文件，你需要将网络中远程 NFS 服务器上的目录挂载到你本地计算机上的目录。也就是说，你指定 NFS 文件系统类型、服务器名称或 IP 地址、远程目录和本地目录作为 `mount` 命令的参数

