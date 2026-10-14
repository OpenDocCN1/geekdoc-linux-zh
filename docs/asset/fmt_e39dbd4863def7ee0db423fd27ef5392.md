
obey pam restrictions = yes

随后的指令禁止 root 管理用户访问，从而提高安全性。

invalid users = root

后续指令将在 Windows 客户端上进行的更改同步到基于 Linux 的身份验证数据库。由于本书格式的限制，`passwd` chat 命令被分成了三行。如果你选择复制代码，请不要在行之间包含换车符。

passwd program = /usr/bin/passwd %u

passwd chat = *Enter\snew\sUNIX:password:* %n\n *Retype\snew\sUNIX:password:* %n\n *Retype\snew\s:password*ssatedsuccessfully*

# 394

# 共享定义

连接到 Samba 服务器的经过验证的客户端将访问它们的家目录。如果你激活了以下指令段，即可。换句话说，家目录限制为使用适当密码登录的用户。

```
[homes]
  comment = Home Directories
  browseable = no
```

以下指令将访问限制为家目录关联的用户名：

```
valid users = %S
```

大多数用户将写入他们的家目录，如果你将 `no` 更改为 `yes`，这是可能的。为了减少拼写错误导致的错误，`write` 是 Samba 配置文件中 `writable` 的同义词。

```
writable = no
```

最后，以下指令设置通过 Samba 连接在本地目录创建的文件和目录的权限。这影响远程创建文件和目录的用户。UCP 的候选人应该已经详细了解权限，此类主题在配套的 LPI 考试中涵盖。

```
create mask = 0700
directory mask = 0700
```

我经常在这里添加类似的指令段来共享文件。请注意；方括号中的名称显示为“共享目录”。你在括号内包含的名称不需要与现有目录匹配。

```
[tmp]
  comment = Temporary file /tmp
  path = /tmp
  read only = no
  public = yes
```

# 376 第 10 章：网络认证与文件系统

## 实现更改

当然，更改必须通过 Samba 脚本来实现。在大多数情况下，我使用以下命令重启脚本：

```
$ sudo /etc/init.d/samba restart
```

我可以在不重启 Samba 的情况下重新加载配置文件，这意味着现有的连接不需要被断开：

```
$ sudo /etc/init.d/samba reload
```

当然，这假设你已经解决了本节中描述的与密码数据库相关的问题——除非你实现了 LDAP 认证，否则你将可以使用与你用于 Linux 网络时相同的数据库。

## 一个 FTP 服务

FTP（文件传输协议）是基于 TCP/IP 协议族开发的最初几个网络应用程序之一。它遵循网络服务的标准模型，因为 FTP 需要一个客户端和一个服务器。大多数操作系统（包括 Ubuntu Linux）都默认安装了 FTP 客户端。虽然有多个选项可用，但本章的重点将放在 vftpd 上，它是许多 Linux 发行版的默认选择——事实上实际上，它是当前 Red Hat 发行版唯一使用的 FTP 服务器。你可以通过以下命令安装它：

```
$ sudo apt-get install vsftpd
```

两个关键配置文件是 `/etc/vsftpd.conf` 和 `/etc/ftpusers`。`vsftpd.conf` 配置文件是标准配置文件 `/etc/ftpusers` 通常被其他 FTP 服务器使用，用于配置不允许通过服务器访问的用户。

该文件中的命令是非常直观的。我敦促你亲自阅读该文件；注释使得许多命令变得自言易懂。请查看表 10-3 中的其中几条命令。这里是你可能需要更改以增强系统安全性的命令。默认 `vsftpd.conf` 文件中的命令仅是你可以使用的全部命令的一小部分。

一旦完成配置，使用以下命令重启服务器。你可以从本地系统连接，也可以从同一网络上的远程系统连接。

```
$ sudo /etc/init.d/vsftpd restart
```

## 设置网络文件系统 377

| 表 10-3 | 命令 | 描述 |
|---|---|---|
| 某些 vsFTP 服务器配置命令 | listen=YES | 支持 `/etc/init.d` 中的控制脚本。 |
| | anonymous_enable=YES | 如果你不想匿名访问，则必须将其设置为 NO。 |
| | # local_enable=YES | 如果你想让普通用户登录，通过取消注释符号 (#) 来激活它。 |
| | # write_enable=YES | 如果你想让普通用户写入，通过取消注释符号 (#) 来激活它。 |
| | dimmessage_enable=YES | 允许消息；默认位于 .message 文件中。 |
| | xferlog_enable=YES | 激活上传和下载的日志记录。 |
| | connect_from_port | 支持通过 TCP/IP 端口 20 进行数据传输。 |
| | secure_chroot_dir=/var/run/vsftpd | 指向一个空且 ftp 用户可的目录。 |
| | pam_service_name=vsftpd | 配置可插认证模块 (PAM) 安全性。 |
| | rsa_cert_file=/etc/ssl/ssl-cert-snakeoil.pem | 指向用于安全连接的证书。 |
| | rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key | 说明用于安全连接的证书密钥。 |

由于我已经识别了匿名访问，我预计能够使用用户名 `anonymous` 访问此 FTP 服务器。但我现在还不及创建 `/home/ftp` 目录。除非我也启用了匿名上传，否则该目录必须由 `ftp` 用户所有且不可写。我通过以下命令设置了这些内容：

```
$ sudo mkdir /home/ftp
$ sudo chown ftp /home/ftp
$ sudo chmod 555 /home/ftp
```

我现在可以匿名访问本地 vsFTP 服务器了。

## 共享文件夹 GUI 工具

可以通过 `sudo shares-admin` 命令打开共享文件夹 GUI 工具。如果本地系统安装了 Samba 和 NFS 服务器，可以使用此工具通过任一服务配置共享目录。

## 378 第 10 章：网络认证与文件系统

图 10-3

共享文件夹配置工具

![](img/8521db60567337b3b9ca1b288c5d36b6_397_0.png)

在开始之前，请备份当前版本的 `/etc/exports` 和 `/etc/samba/smb.conf` 配置文件。最简单的选项是通过以下命令将这些文件备份到你的家目录：

```
$ cp /etc/exports ~
$ cp /etc/samba/smb.conf ~
```

打开共享文件夹工具。第一次打开时，图 10-3 所示的窗口将是空白的。

“共享”选项卡列出了在 Samba 和 NFS 服务上配置的共享目录。当你通过共享文件夹工具配置目录或通过直接编辑关联配置文件来共享目录时，目录就会列出来。“常规属性”选项卡为 Samba 服务器配置一些基本设置。在接下来的练习中，我将描述如何通过 Samba 共享目录，另一个如何通过 NFS 共享。配置完成后，可以检查这些设置。

### 练习 10-2：使用 GUI 工具创建 Samba 共享

在此练习中，你将学习如何通过 Samba 共享目录，另一个通过 NFS 共享。配置完成后，可以检查这些设置。

## 设置网络文件系统 379

在此练习中，你将学习如何通过 Samba 共享目录，另一个通过 NFS 共享。配置完成后，可以检查这些设置。

1. 如果共享文件夹窗口尚未打开，在 GNOME 桌面打开一个命令行界面。点击应用程序 | 辅助工具 | 终端。
2. 在出现的终端窗口中，输入 `sudo shares-admin` 命令。一旦你验证了密码，“共享”选项卡就会出现。
3. 点击共享文件夹窗口中的“添加”。在出现的共享窗口中，如下所示，“通过”下拉框：Windows 网络 (SMB) 和 Unix 网络 (NFS)。由于本次练习使用 Samba，选择 Windows 网络 (SMB)。
4. 使用路径下拉框选择要共享的目录路径。应该是运行 `shares-admin` 命令的目录。如果目标目录不在列表中，点击其他，并导航到目标目录。对于本次练习，选择 `/home` 目录。
5. 在“名称”框中，使用默认值；这将在客户端可见。
6. 在“注释”框中，使用默认值；这描述将在客户端可见。
7. 在“密码”框中，使用默认值；这将在客户端可见。
8. 取消勾选“只读”选项并点击确定。
9. 你刚刚配置的共享目录将出现在主共享文件夹窗口的“共享”选项卡中。
