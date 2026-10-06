

# 邮件 517

```
#imap stream tcp nowait root /usr/sbin/tcpd imapd
```

要正确配置 inetd，只需找到这些行中的每一行，删除行开头的井号（#），并保存修改后的文件。然后通过执行命令重启 inetd：

```
killall -HUP inetd
```

# sendmail 的管理

sendmail 的服务器管理脚本为 /etc/rc.d/init.d/sendmail。通过使用适当参数调用此脚本，你可以控制服务器的运行。

# 启动和重启服务

要启动 sendmail，执行命令：

```
/etc/rc.d/init.d/sendmail start
```

要重启 sendmail，执行命令：

```
/etc/rc.d/init.d/sendmail restart
```

# 停止服务

要停止 sendmail，执行命令：

```
/etc/rc.d/init.d/sendmail stop
```

# 检查服务状态

要检查 sendmail 的状态，执行命令：

```
/etc/rc.d/init.d/sendmail status
```

# 日志

除了发布到系统日志 (/var/log/messages) 的条目外，sendmail 还保留了自己的日志文件 /var/log/maillog。如果邮件服务运行不正常，请检查这两个日志文件以寻找问题问题的线索。

# 更多信息

关于 sendmail 的信息，请查看 sendmail 网站 www.sendmail.org、sendmail-doc 软件包的内容（位于 /usr/doc/sendmail），以及以下 man 页面：

- aliases
- mailstats
- makemap
- newaliases
- praliases
- rmail
- sendmail

关于 IMAP 和 POP 的信息，请查看 /usr/doc/imap-* 下的文档文件以及 imapd 和 popd man 页面。现在完成练习 21.4 以获得 Linux 邮件服务的实践经验。

# 练习 21.4

# 安装和配置邮件服务

邮件服务无处不在，因此每个系统管理员都必须熟悉邮件的安装和配置。执行以下步骤以获得第一手体验：

1. 安装三个 sendmail 包和 IMAP/POP 包。
2. 使用 mailconf 指定接受邮件的系统。
3. 使用 mailconf 指定几个用户邮件别名。
4. 使用邮件客户端（如 pine）验证你的邮件配置是否运行正常。

你可以参考这本书来帮助配置邮件。但是，在参加 RHCE 考试之前，请确保你可以在没有书籍或笔记帮助的情况下执行简单的邮件配置操作。

# NFS

网络文件系统 (NFS) 提供了对文件和目录的共享访问。在运行期间，NFS 服务器为客户端指定一个或多个可用目录。这些指定的目录被称为“共享”（shares），被认为是由服务器“导出”（exported）的。一旦被 NFS 服务器导出，客户端系统就可以以类似于挂载本地文件系统的方式挂载 NFS 共享。Linux 的实现在功能上与其它 Unix 系统上的可用 NFS 实现类似，其客户端在很大程度上兼容 NFS 3.0 版本。

一个 NFS 服务器运行三个与 NFS 相关的守护进程：

- portmap，将客户端请求转发到正确的 NFS 进程访问请求
- rpc.nfsd，将远程文件访问请求转换为本地文件请求
- rpc.mountd，负责挂载和卸载文件系统

如果一个主机运行了所有三个守护进程，则它既可以是 NFS 服务器也可以是客户端。

# 安装

在 Hat Linux 6.2 下，大部分 NFS 代码已整合到 Linux 内核中。要使用 NFS，你只需要这些包：

- nfs-utils，包含使用 NFS 所需的工具
- portmap，包含与 portmap 相关的文件，并被 NFS 服务器使用

要安装 NFS，移动到包含包的目录并执行命令：
rpm -Uvh nfs-utils-*.rpm portmap-*.rpm

# 服务器配置

NFS 服务器配置文件为 /etc/exports，其中每一行都是一个指令，用于指定共享（即导出的目录）和关联的访问权限。以下是典型的 /etc/exports 文件中的某行：

```
/exports/database free.azusapacific.com bob.azusapacific.com
```

指令的通用格式：

```
path host_list
```

# 第 21 章 · 安装和配置主要网络服务

其中 path 是共享目录的绝对路径，host_list 是可以访问该共享的一个或多个主机的列表。每个主机之间应通过一个或多个空格与相邻主机隔开。
可以通过几种方式之一指定主机：

- 使用主机名，如果该主机是本地域的一部分
- 使用完全限定域名 (FQDN)
- 使用包含通配符 (*) 的主机名
- 使用 IP 地址
- 使用网络地址，例如 192.168.1.0/255.255.255.0

通配符字符最多匹配主机名中的单个组件。例如，主机标识符 =*.azuspacific.com 匹配 www.azuspacific.com 但不匹配 .science.azuspacific.com。通配符可以匹配主机名组件的一部分。例如，主机标识符 dtc*.azuspacific.com 匹配 dtc01.azuspacific.com、dtc02.azuspacific.com 等。

默认情况下，允许客户端对共享进行读取访问。要允许读写访问，请在 exports 页面后面加上 (rw)。例如，这里的读写共享：

```
/exports/database fred.azuspacific(ro)
bob.azuspacific(rw)
```

主机 fred 允许读取访问，而主机 bob 允许读写访问。注意不要在主机标识符和权限之间插入空格。默认情况下，如果客户端以 root 登录，请求将映射到用户 65535。如果你允许 root 访问，请指定 no_root_squash 选项。例如：

```
/exports/database bob.azuspacific(rw,no_root_squash)
```

exports 文件可以手动编辑。但是，如果你愿意，linuxconf 提供了管理 NFS 共享的设施。

# 客户端配置

如所述，客户端可以像处理本地文件一样处理导出目录。要挂载共享目录，使用 mount 命令的特殊形式。例如：

```
mount -t nfs server:/exports/databases /mnt/database
```

该命令将 server 导出的 exports/databases 挂载为本地目录 /mnt/database。脚本 /etc/rc.init/netfs 在启动时运行，自动挂载 /etc/fstab 中指定的 NFS 目录。如果你希望启动时自动挂载 NFS 共享，只需将其包含在 /etc/fstab 文件。例如：

```
server:/exports/database /mnt/database nfs defaults 0 2
```

若干挂载选项允许你控制 NFS 共享的运行：

- hard, intr 允许杀死或中断被不可服务器阻塞的
- nolock 禁用文件锁定，以便 NFS 客户端访问不支持的 NFS 服务器
- rsize=8192 和 wsize=8192 分别分配比默认更大的读写缓冲区，并显著提高 NFS 吞吐量

你可以 linuxconf 挂载 NFS 共享或指定包含在 /etc/fstab 中的 NFS 共享。启动 linuxconf，并选择 Access NFS Volume > Add to the menu。

![](7a53e2be7760e1d422d1c89dbf5d6ede)

nfslock 服务为 NFS 客户端提供文件锁定服务。如果你的 NFS 客户端需要锁定文件，请确保启用 nfslock 服务。

Red Hat Linux 还提供了 autofs 服务，你可以配置它按需挂载 NFS 共享。autofs 服务位于同名的可选包中。更多信息请参见 man 页面 auto.master, autofs(5), autofs(8) 和 automount。

# NFS 管理

NFS 的服务器管理脚本为 /etc/rd.d/init.portmap 和 /etc/rd.d/init.nfs。通过使用适当参数调用这些脚本，你可以控制 NFS 服务器的运行。

