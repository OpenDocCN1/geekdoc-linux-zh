
"valid users"选项指定允许登录此服务的用户列表。在我们的示例中，仅允许 "admin" 用户访问该服务。

Copyright 1999 - 2000 Gerhard Maurani, Open Network Architecture © and OpenDocs Publishing

# 服务器软件（文件共享网络服务） | 2 第 1 章

`invalid users = root bin daemon nobody named sys list mem kmkm`

"invalid users"选项指定不应登录此服务的用户列表。这实际上是一个“偏执性”检查，以绝对确保设置不当不会破坏你的安全性。建议允许默认用户在服务器上运行守护进程。

# "etc/imhosts"文件的配置

配置你的 "etc/imhosts" 文件。"imhosts" 文件是 Samba Net BIOS 名称到 IP 地址的映射文件。它与 "etc/hosts"格式非常相似，不同之处在于主机名部分必须与 Net BIOS 命名对应。

创建 Imhosts 文件（`touch /etc/imhosts`）并添加你的客户端主机：

```
# Samba Imhosts 文件示例。
#
127.0.0.1    localhost
192.168.1.1    deep
192.168.1.4    win
```

在我们的示例中，该文件包含 IP 到 Net BIOS 名称的映射。`localhost` (127.0.0.1)、名为 `deep` 的客户端 (192.168.1.1) 和名为 `win` 的客户端 (192.168.1.4)。

# "etc/pam.d/samba"文件的配置

配置你的 "etc/pam.d/samba" 文件以使用 pam 认证。

创建 samba 文件（`touch /etc/pam.d/samba`）并添加以下行：

| Auth | required | /lib/security/pam_pwdb.nullock shadow |

| Account | required | /lib/security/pam_pwdb |

# "etc/logrotate.d/samba"文件的配置

配置你的 "etc/logrotate.d/samba" 文件以每周自动轮转日志文件。

创建 samba 文件（`touch /etc/logrotate.d/samba`）并添加以下行：

```
/var/log/samba/log.nmbd {
  notifempty
  missingok
  postrotate
    /usr/bin/killall -HUP nmbd
  endscript
}

/var/log/samba/log.smb {
  notifempty
  missingok
  postrotate
    /usr/bin/killall -HUP smbd
  endscript
}
```

# 为你的客户端创建一个加密的 Samba 密码文件

"etc/smbspasswd" 文件是 Samba 加密密码文件。它包含了允许访问 Samba 服务器的用户名；Unix UID 和 SMB 哈希密码、账户标志信息以及密码上次更改的时间。在你的客户端连接到 Samba 服务器之前，创建此密码文件并包含所有允许的用户是非常重要的。如果没有这一步，将无人连接到你的 Samba 服务器。

## Step 1

要创建 Samba 账户，你必须先为他们创建一个有效的 Linux 账户，因此在生成 Samba 的 /smbpasswd 文件之前，先在 /etc/passwd 文件中创建所有想要连接到 Samba 服务器的用户。

- 要向 "/etc/passwd" 文件添加新用户，请使用以下命令：

## Step 2

一旦我们已用户添加到文件中，现在就可以生成 smbpasswd 了。

## Step 3

最后，我们必须执行的最后一步是创建 smb 文件。

## Step 4

不要忘记更改你的 smb 文件的权限，使其 root 可读写（0600）。这是一项安全措施。

# /etc/rc.d/init.d/samba文件的配置

配置你的 /etc/rc.d/init.d/samba 文件以自动启动和停止 Samba smbd 和 nmbd 守护进程。

# 服务器软件（文件共享网络服务） 2

第 1 章

```bash
echo "Usage: $0 (start|stop|restart|status)
exit 1
}
esac
exit $RETVAL
```

现在，让此脚本具有可执行权限并更改其默认权限：

使用命令为 Samba 创建符号链接：

当重启服务器时，Samba 不会自动更新 smbd 和 nmbd 守护进程。

你可以通过执行以下命令将其设置为默认执行：

```bash
[root@deep /#] chmod 700 /etc/rc.d/init.d/smb
[root@deep /#] chconfig -add smb
[root@deep /#] chconfig -level 345 smb on
```

```
使用以下命令手动启动 Samba 服务器：
启动 SMB 服务: [ OK ]
启动 NMB 服务: [ OK ]
```

# 加固 Samba

### 使重要配置文件文件免疫

不可变位（immutable bit）可以防止意外删除或覆盖必须保护的文件。它还可以防止他人创建指向该文件的符号链接。

已经创建了 "smb.conf" 和 "hosts" 文件，使用类似下面的命令对其进行免疫是一个好主意：

```bash
[root@deep /#] chattr +i /etc/smb.conf
[root@deep /#] chattr +i /etc/hosts
```

# 优化 Samba

### 配置文件中的 "wide links" 参数

在 Samba 配置文件 `/etc/smb.conf` 中将 "wide links" 参数设置为 "no"。将 "wide links" 参数设置为 "yes" 是一个巨大的错误，它会告诉 Samba 不要跟踪指定为共享区域之外的符号链接。为了判断链接是否指向共享区域，Samba 必须跟踪链接并进行目录路径查找，以确定链接在文件系统中的最终位置。一项测试显示，设置此参数会导致 Samba 性能下降 25-30%。

# 调整缓冲区缓存

修改文件系统缓存调优参数可以显著提高 Linux 的性能，提升可达两倍。Linux 将尝试使用未用于其他用途的内存进行文件系统缓存。一个名为 `bdflush` 的特殊守护进程会定期将“脏”缓冲区（包含修改过的文件系统数据或元数据的缓冲区）刷新到磁盘。

秘诀是尽可能长时间将尽可能数据留在内存中。写入磁盘是任何文件系统中最慢的部分。如果你知道文件系统将被频繁使用，就可以为 Linux Samba 调整此过程。有了许多内核可调选项，可以通过向 /proc 文件系统中的特殊文件写入内容来在线完成。技巧在于，你必须告诉 Linux 这样做。你通过执行适用于 Linux 2.2 内核的命令来实现。

Copyright 1999-2000 Gerhard Maurani, Open Network Architecture & OpenDocs Publishing

# 服务器软件（文件共享网络服务） | 2 第 1 章

RedHat Linux 下 "bflush" 参数的默认设置为：

40 500 64 256 500 3000 500 1884 2

- 要更改 bflush 的值，请在终端上输入以下命令：

RedHat Linux 6.1

`[root@deep /#] echo "0 500 64 64 15 6000 6000 1884 2" >/proc/sys/vm/bflush`

你可以将上述命令添加到 "/etc/rc.d/local" 脚本文件中，这样下次重启系统时就不需要再次输入了。

RedHat Linux 6.2

编辑 "/etc/sysctl.conf" 文件并添加以下行：

```bash
# Improve file system performance
vm.bflush = 80 500 64 64 15 6000 6000 1884 2
```

你必须重启网络使更改生效。重启内核的命令是：

- 要手动重启系统上的所有网络设备，请使用以下命令：

`[root@deep /#] /etc/rc.d/init.network restart`

设置网络参数

启动接口 lo [ OK ]

启动接口 eth0 [ OK ]

启动接口 eth1 [ OK ]

此行代码告诉 "bflush" 当文件系统缓冲区缓存达到 80% 满 (80) 时不要担心将脏缓冲区写入磁盘。其他值调整了单次操作写入的缓冲区数量 (500)、允许脏缓冲区在内核中存活的时间 (60*HZ) 等。你可以在 2.2 内核文档的 "/linux/Documentation/sysctl/vm.txt" 文件中找到完整细节，也可以查看第 4 章“通用系统优化”获取更多信息。

# 调整缓冲区内存 (buffermem)
