
## FTP 服务器配置文件（vsftpd 守护进程）

配置文件示例如下：

- 软件包：vsftpd
- 守护进程：/usr/sbin/vsftpd
- 脚本：/etc/init.d/vsftpd
- 配置：/etc/vsftpd/vsftpd.conf, /etc/vsftpd.ftpusers, /etc/pam.d/vsftpd
- 日志：/var/log/xferlog

## 安装和配置 FTP 服务器的步骤

执行以下步骤以安装和配置 FTP 服务器（vsftpd 守护进程）：

### 安装 VSFTPD 守护进程

查找扩展名为 .rpm 的文件（在 Linux 发行版 CD 或 DVD 上查找）。

输入以下命令以安装 FTP 服务器：

```
[root@netmon tmp]# rpm -ivh vsftpd-1.5.6-i386.rpm
```

### 启动 VSFTPD 守护进程

在启动后，使用以下命令来启动、停止和重启 VSFTPD：

```
[root@netmon tmp]# service vsftpd start
[root@netmon tmp]# service vsftpd stop
[root@netmon tmp]# service vsftpd restart
```

使用以下 chkconfig 命令在启动时启动 VSFTPD。

```
[root@netmon tmp]# chkconfig --level 345 vsftpd on
```

### 测试 VSFTPD 状态

您可以随时使用 netstat 命令测试 VSFTPD 进程是否正在运行，该命令会列出服务器正在监听流量的所有 TCP 和 UDP 端口。下面的示例显示如下输出：

```
[root@netmon root]# netstat -a | grep ftp | grep tcp:21
```

![](img/f3b9cff79e19317416c12eaf5ded7245_143_0.png)

```
[root@netmon root]#
```

### 编辑 vsftpd.conf 文件

vsftpd.conf 文件使用了一些您需要了解的默认设置。

正如代码片段中所示，配置文件相当直观：

```
# 是否允许匿名 FTP？
anonymous_enable=YES
# 取消注释以允许本地用户登录。
local_enable=YES
# 取消注释以启用任何形式的 FTP 写命令。
# （即使用户需要能够上传文件，也需要此设置）
write_enable=YES
# 取消注释以允许匿名 FTP 用户上传文件。这仅在
# 全局写权限激活时有效。此外，您显然需要创建一个
# 可被 FTP 用户写入的目录。
anon_upload_enable=YES
# 如果您希望匿名 FTP 用户能够创建新目录，请取消
# 注释。
anon_mkdir_write_enable=YES
# 启用上传/下载日志。
xferlog_enable=YES
# 如果您愿意，可以覆盖日志文件的存放位置。
# 默认设置如下所示。
xferlog_file=/var/log/vsftpd.log
# 匿名登录后 vsftpd 将尝试切换到的目录。
# （默认值 = /var/ftp）
anon_root=/data/directory
```

要激活或停用某项功能，请删除或添加相应行开头的 #。关于此内容的更多说明可以在 vsftpd.conf man（手册）页面中找到。

以下各点说明了 VSFTPD 的配置：

- **VSFTPD 作为匿名 FTP 服务器运行：** 默认情况下，匿名 FTP 服务始终处于开启状态。您可以将配置文件中的 anonymous_enable 指令设置为 no 以禁用此功能。您还需要同时取消 local_enable 指令前的注释符号 (#)，以启用本地用户登录。

- **VSFTPD 仅允许远程用户进行匿名 FTP 下载，而不允许他们上传：** 您可以通过修改上面所示的 anon_upload_enable 指令来更改此设置。

- **VSFTPD 不允许匿名用户在您的 FTP 服务器上创建目录：** 您可以通过修改 anon_mkdir_write_enable 指令来更改此设置。

- **VSFTPD 将 FTP 访问记录到 /var/log/vsftpd.log 日志文件中：** 您可以通过修改 xferlog_file 指令来更改此设置。

### 更改 FTP 欢迎横幅

更改 vsftpd.conf 文件中的默认欢迎横幅，以使得恶意用户更难确定您系统的类型。该文件中的指令为：

```
ftpd_banner=Welcome to S.P.I.T. FTP site
```

## FTP 客户端

### 使用匿名访问

执行以下步骤以使用 FTP 服务器的匿名访问：

1. 检查 FTP 客户端上是否存在测试文件。

   输入以下命令以检查 FTP 客户端上是否存在测试文件：

   ```
   [root@netx tmp]# ll
   total 1
   -rw-r--r-- 1 root 0 June 4 09:09 testfile
   [root@netx tmp]#
   ```

2. 通过 FTP 连接到 netmon。

   在 root 模式下输入以下命令，使用 FTP 连接到 netmon 服务器：

   ```
   [root@netx tmp]# ftp 172.16.1.100
   Connected to 172.16.1.100 (172.16.1.100)
   220 ready, dude (vsFTPD 1.1.0: beat me, break me)
   Name (172.16.1.100:root): anonymous
   331 Please specify the password.
   Password: (在此处输入 "anonymous")
   230 Login successful. Have fun.
   ftp> ha
   ftp> bin
   ftp> get vsftpd-*
   local: vsftpd-1.1.0-1.i386.rpm.tmp remote: vsftpd-1.1.0-1.i386.rpm
   227 Entering Passive Mode (172,16,1,100,44,156)
   150 Opening BINARY mode data connection for vsftpd-1.1.0-1.i386.rpm (76288 bytes).
   226 File send ok.
   76288 bytes received in 0.499 secs (1.5e+02 Kbytes/sec)
   ftp> exit
   221 Goodbye.
   ```

   - `ftp > bin` 用于二进制模式数据传输
   - `ftp > ha` 在下载时启用哈希标记作为进度条

### 故障排除 FTP

1. 初始设置失败可能是由于客户端和服务器之间的防火墙阻止了某些或所有类型的 FTP 流量所致。要禁用防火墙的默认设置，请运行以下命令：

   ```
   [root@netmon tmp]# iptables -F
   ```

   > *Iptables* 是 Linux 防火墙模块，我们可以使用它来指定防火墙规则。*iptables -F* 清除所有防火墙规则。有关 iptables 的更多信息，请参阅附录。

2. 由于 SELinux 策略，您可能无法访问 ftp 服务器。

   要禁用 SELinux ftp 策略，请运行以下命令：

   ```
   [root@netmon tmp]# setsebool -P ftpd_disable_trans 1
   ```

   **Security** Enhanced Linux (SELinux) 增强功能由美国联邦国家安全局 (NSA) 开发，从 Fedora Core 版本 3 和 Red Hat Enterprise Linux 版本 4 开始包含在内。Linux 内核支持细粒度访问控制架构。支持*类型*强制和**基于角色的访问控制 (RBAC)**。系统进程和文件（包括套接字描述符、IPC、设备等）均被分配一组称为*安全上下文*的安全属性。有关 Selinux 的更多信息，请参阅附录。

### 为共享目录添加只读访问权限的 FTP 用户

此示例适用于不想要匿名 FTP，而需要为受信任用户组提供对共享目录的只读访问权限的情况。

执行以下步骤以添加具有共享目录只读访问权限的 FTP 用户：

- 禁用匿名 FTP

  ```
  # 是否允许匿名 FTP？
  # anonymous_enable=YES
  ```

- 启用单独登录

  ```
  # 取消注释以允许本地用户登录。
  local_enable=YES
  ```

  按照上述步骤修改 `/etc/vsftpd.conf` 后，启动 VSFTPD。

  ```
  [root@netmon tmp]# service vsftpd start
  ```

- 创建用户组和共享目录。在此情况下，使用 `/home/share-docs` 作为远程用户的共享目录，并使用 share-resource 作为用户组名称。

  ```
  [root@netmon tmp]# groupadd share-resource
  [root@netmon tmp]# mkdir /home/share-docs
  ```

- 使目录可被 share-resource 组访问。

  ```
  [root@netmon tmp]# chmod 750 /home/share-docs
  [root@netmon tmp]# chown root:share-resource /home/share-docs
  ```

- 添加用户，并将他们的默认目录设置为 `/home/share-docs`。

  ```
  [root@netmon tmp]# useradd -g share-resource -d /home/share-docs aday
  ```

- 将供用户下载的文件复制到 `/home/share-docs` 目录中。

- 将 `/home/share-docs` 目录中文件的权限更改为组只读访问。

  ```
  [root@netmon tmp]# chown root:share-resource /home/share-docs/*
  [root@netmon tmp]# chmod 740 /home/share-docs/*
  ```

用户现在应该能够使用新的用户名和密码通过 FTP 登录到服务器。如果您绝对不希望任何 FTP 用户能够向任何目录写入，则应将 vsftpd.conf 文件中的 write_enable 行设置为 no：

```
write_enable = NO
```

需要注意的是，您必须重启 VSFTPD，以确保配置文件中所做的更改已生效。

```
[root@netmon tmp]# service vsftpd restart
```

## 总结

在这个 Linux 实验室中，您将学习使用 FTP (VSFTPD) 守护进程配置 Linux FTP 服务器（匿名 FTP 服务器和私有 FTP），该守护进程非常安全。FTP 客户端是所有操作系统和 Web 浏览器的一部分。FTP 服务是向互联网用户提供文档归档和软件文件的主要方法。

