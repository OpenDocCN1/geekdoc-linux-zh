
```
==================== 通用服务 <<=
[homes]
comment = 用户目录
browse = no # 只有登录的用户可以看到自己的家目录目录
writable = yes # 他们可以向其写入，其他人不行

[printers]
comment = 所有打印机
path = var/spool/samba # 使用的打印池目录
browse = yes # 显示在浏览列表中
public = yes # 允许用户 'guest account' 打印
guest ok = yes # 不是文件系统
writable = no
printable = yes # 这是一个打印服务

==================== 共享定义 <<<<=
# 此项适用于所有用户共享文件
[tmp]
comment = 临时文件空间
path = tmp
read only = no
public = yes # 所有人获得只读权限

一个公共访问的目录，但只读
[public]
comment = 公共物品
path = /home/ftp/pub
public = yes
writable = no # 'read only = 'yes' 也能做到这一点
printable = no
======================================================
```

# Samba 431

虽然这种简单的“共享所有”设计对于打印机选项是最简单的，但你可以通过为要共享的每个打印机创建一个节标题来选择性地共享任何打印机。更多详情请查阅 Samba 文档。

# 测试 `/etc/smb.conf` 的更改

在对 `/etc/smb.conf` 进行任何更改后，在将其投入生产之前，测试你的系统总是个好主意。

# 测试新的 SMB.CONF 配置—TESTPARM

你可以使用提供的测试工具 `testparm` 进行简单的语法检查，如图 8-21 所示。这并不会实际检查服务是否运行或运行正常；它只检查基本语法和分组。

# 停止并重启 Samba 服务

在对配置文件 `/etc/smb.conf` 进行任何更改后，你可以等待 Samba 服务在稍后的某个点重新读取配置文件，或者使用 `/etc/rc.init.d/smb` 控制脚本强制执行。脚本 `/etc/rc.init.d/smb` 用于启动、停止和重启 Samba 守护进程，如图 8-21 所示。

图 8-21 运行 `testparm`

```
root@unix:~ testparm
Load smb config files from /etc/smb.conf
Processing section "homes"
Processing section "printers"
Processing section "tmp"
Processing section "public"
Loaded services OK
按回车键查看服务定义的转储（dump）
```

# 432 第 8 章：网络客户端服务

# 检查 Samba 文件服务和打印服务

你可以使用 `smclient` 实用程序测试实际的连通性。在测试实际连通性之前，你应该强制重启 Samba 守护进程，如图 8-22 所示。

客户端工具—`smclient`

最后一个工具是客户端工具。通过此工具，你可以测试到任何 SMB 主机的连通性。它提供了一个让大多数 Linux 用户熟悉的类 FTP 接口。

# Samba 435

图 8-24

基于 Windows 的服务的 SMB 挂载示例

```
[root@linux6 ~]# mkdir /mnt/docs  # 确保目录存在
[root@linux6 ~]# ls -ld smbount \\\W98latop\docs -c '/mnt/docs'
Added interface ip:206.195.1.223 bcast=206.195.1.255 netmask=255.255.255.0
Got a pong query response from 206.195.123 (206.195.123 )
Server time is set to 26:34:56 1999
Securityshare
[root@linux6 ~]# ls -l /mnt/docs/*
-rwxr-xr-x 1 root 115070 May 19 18:37 /mnt/docs/PERL4DAVE.zip
-rwxr-xr-x 1 root 50622 May 7 18:45 /mnt/docs/UNIX1G.zip
-rwxr-xr-x 1 root 113261 Jun 2 09:27 /mnt/docs/VirtualNTMMachine
[root@linux6 ~]# ls /mnt/docs
[root@linux6 ~]# mount  # 列出所有挂载的文件系统
/dev/sda1 on type ext2 (rw)
none on proc type (rw)
/dev/sd7 on dos type vfat (rw)
/dev/sd8 on dos type vfat (rw)
none on debug typeA (rw,mode=0622)
//W98LAPTOP/DOCES on /mnt/docs type smbfs (0)
[root@linux6 ~]# unmount /mnt/docs  # 断开共享连接
[root@linux6 ~]#
```

该服务名为 DOCS，位于名为 W98LAPTOP 的 (Win98) 主机，挂载点名为 `/mnt/docs`。此连接随后对 Linux 主机上的所有用户作为本地目录可用。此连接将永久有效，直到下次重启。要使此连接在重启后持续存在，应在 `/etc/fstab` 文件中添加如下条目：
