

# 关键技能

## 11.2 配置 vsftpd

**vsftpd** 服务器并没有像其某些竞争对手那样拥有众多配置选项，而是专注于将基础功能做好。它足以满足大多数 FTP 需求，而缺失的功能大多可被视为“花哨功能”，或者可以通过其他方式实现。在本模块的其余部分，我将介绍如何为一个支持用户和匿名访问的服务器进行配置。除了安装 **vsftpd rpm** 包之外，您可能还需要确认是否已安装 FTP 客户端和 **anonftp** 包。

```
[root@tux /root]# rpm -qa | grep ftp
lftp-2.5.2-4
anonftp-4.0-12
ftp-0.17-15
vsftpd-1.0.1-7
gftp-2.0.13-4
```

**anonftp** 包本身并不是一个 FTP 服务器，但它为使用 **vsftpd** 或其他 FTP 守护进程搭建匿名 FTP 服务器提供了一套框架。

正如我之前提到的，FTP 是互联网早期设计的，它缺乏我们在现代互联网使用中习以为常的许多安全功能。当我们谈论 **vsftpd** 等服务器的安全性时，主要指的是其抵御定向攻击的能力。通过 FTP 会话传输的所有数据（包括密码）仍然都是未加密发送的。因此，不建议在不安全的环境或传输敏感数据时使用 FTP。如果您需要更安全地传输文件，建议研究更安全协议，如安全外壳协议（SSH）/安全拷贝协议（SCP）。只有*匿名式* FTP 服务器应暴露在互联网上。

### 阅读 README 文档

您会发现，**vsftpd** 附带了几个纯文本格式的文档文件，位于 `/usr/share/doc/vsftpd-1.0.1/` 目录下。这些文档详细介绍了 **vsftpd** 的安全性和设计考虑。我强烈建议您花几分钟时间阅读这些文档。如果您理解这些配置选项如何整合到整个软件包中，它们会更有意义。在带着问题去任何讨论论坛之前，也建议先阅读随软件包提供的文档。

### 修复您的 xinetd.conf 文件

正如您在模块 8 中可能记得的，`/etc/inetd.conf` 文件由 **xinetd** 程序管理，该程序作为一种“超级服务器”，代表许多服务器应用程序监听网络请求，并在检测到连接请求时启动相应的服务器应用程序。如果其配置文件 `/etc/xinetd.conf` 被更改，您需要向 **xinetd** 进程发送信号，通知其重新加载配置文件。

Red Hat 在 `/etc/xinetd.d/` 目录中附带了一个 **vsftpd** 的配置文件，但默认是禁用的。如果您在下图所示的服务配置工具中启用 **vsftpd**，则 **xinetd.d** 文件中 **vsftpd** 的 disable 指令行将从 “disable = yes” 更改为 “disable = no”。

![](img/ec2066d370d3af1a767664d36aa7ddfe_370_0.png)

如果您不使用服务配置工具，也可以使用您喜欢的文本编辑器进行相同的更改。生成的文件应与以下内容相似：

```
# default: off
# Description: The vsftpd FTP server serves FTP connections. It uses \
# normal, unencrypted usernames and passwords for authentication.
service ftp
{
	disable = no
	socket_type = stream
	wait = no
	user = root
	server = /usr/sbin/vsftpd
	nice = 10
}
```

现在我们需要告诉 `xinetd` 重新读取其所有配置文件。最简单的方法是运行：

```
[root@tux /root]# /etc/init.d/xinetd reload
```

您也可以通过向其发送 `SIGUSR1` 信号来强制其重新加载配置，方法如下。

```
[root@tux /root]# kill -SIGUSR1 `cat /var/run/xinetd.pid`
```

现在您应该能够 **ftp** 到您自己的系统了。如果您目前无法登录也不要担心——您将在下一节中处理这些细节——但至少您应该能够看到 FTP 登录提示符。

```
[michael@tux michael]$ ftp localhost
Connected to localhost (127.0.0.1).
220 ready, dude (vsFTPd 1.0.1: beat me, break me)
Name (localhost:michael):
```

## 11.3 配置 vsftpd

**vsftpd** 软件包附带一个示例配置文件，您可以根据需求轻松地进行修改。您的默认 **conf** 文件可能类似于以下内容。

```
# Example config file /etc/vsftpd.conf
#
# The default compiled in settings are very paranoid. This sample file
# loosens things up a bit, to make the ftp daemon more usable.
#
# Allow anonymous FTP?
anonymous_enable=YES
#
# Uncomment this to allow local users to log in.
local_enable=YES
#
# Uncomment this to enable any form of FTP write command.
write_enable=YES
#
# Default umask for local users is 077. You may wish to change this to 022,
# if your users expect that (022 is used by most other ftpd's)
local_umask=022
#
# Uncomment this to allow the anonymous FTP user to upload files. This only
# has an effect if the above global write enable is activated. Also, you will
# obviously need to create a directory writable by the FTP user.
anon_upload_enable=YES
#
# Uncomment this if you want the anonymous FTP user to be able to create
# new directories.
anon_mkdir_write_enable=YES
#
# Activate directory messages - messages given to remote users when they
# go into a certain directory.
dirmessage_enable=YES
#
# Activate logging of uploads/downloads.
xferlog_enable=YES
#
# Make sure PORT transfer connections originate from port 20 (ftp-data).
connect_from_port_20=YES
#
# If you want, you can arrange for uploaded anonymous files to be owned by
# a different user. Note! Using `root' for uploaded files is not
# recommended!
#chown_uploads=YES
#chown_username=whoever
#
# You may override where the log file goes if you like. The default is shown
# below.
#xferlog_file=/var/log/vsftpd.log
#
# If you want, you can have your log file in standard ftpd xferlog format
xferlog_std_format=YES
#
# You may change the default value for timing out an idle session.
#idle_session_timeout=600
#
# You may change the default value for timing out a data connection.
#data_connection_timeout=120
#
# It is recommended that you define on your system a unique user which the
# ftp server can use as a totally isolated and unprivileged user.
#nopriv_user=ftpsecure
#
# Enable this and the server will recognize asynchronous ABOR requests. Not
# recommended for security (the code is non-trivial). Not enabling it,
# however, may confuse older FTP clients.
#async_abor_enable=YES
#
# By default the server will pretend to allow ASCII mode but in fact ignore
# the request. Turn on the below option to have the server actually do ASCII
# mangling of files when in ASCII mode.
# Beware that turning on ascii_download_enable enables malicious remote parties
# to consume your I/O resources, by issuing the command "SIZE /big/file" in
# ASCII mode.
# These ASCII options are split into upload and download because you may wish
# to enable ASCII uploads (to prevent uploaded scripts etc. from breaking),
# without the DoS risk of SIZE and ASCII downloads. ASCII mangling should be
# on the client anyway..
#ascii_upload_enable=YES
#ascii_download_enable=YES
#
# You may fully custimise the login banner string:
#ftpd_banner=Welcome to blah FTP service.
#
# You may specify a file of disallowed anonymous e-mail addresses. Apparently
# useful for combatting certain DoS attacks.
#deny_email_enable=YES
# (default follows)
#banned_email_files=/etc/vsftpd.banned_emails
#
# You may specify an explicit list of local users to chroot() to their home
# directory. If chroot_local_user is YES, then this list becomes a list of
# users to NOT chroot().
#chroot_list_enable=YES
# (default follows)
#chroot_list_file=/etc/vsftpd.chroot_list
#
# You may activate the "-R" option to the built-in ls. This is disabled by
# default to avoid remote users being able to cause excessive I/O on large
# sites. However, some broken FTP clients such as "ncftp" and "mirror" assume
# the presence of the "-R" option, so there is a strong case for enabling it.
ls_recurse_enable=YES
pasv_service_name=vsftpd
```

示例文件注释相当完善，因此您可能只需通读一遍即可弄清如何使基本功能正常工作。您将在接下来的几个章节中介绍一些最重要的功能，包括默认 **config** 文件中未提到的一些选项。在阅读以下选项的说明时，您可能需要参考此文件。

### 通用配置选项

在介绍不同的访问选项之前，您应该熟悉一些基本的配置选择。本节仅提供简要参考，您可以进一步探索与您的设置相关的主题。

- **connect_from_port_20** 此选项决定数据连接是否使用 20 端口（在正常模式下运行时）。默认值为 “no” 可能会让一些人感到惊讶。原因是这是 **vsftpd** 安全模型的一部分。通过不要求使用低编号端口，守护进程的某些部分可以在权限较低的模式下运行。权衡之处在于，某些客户端的安全模型坚持要求连接来自 20 端口，因此在我们的示例文件中，该选项已设置为 “yes”。
- **pasv_enable** 此选项启用被动模式，默认值为 “yes”。如果出于某种原因您希望禁止使用被动模式，请禁用它。
- **pasv_promiscuous** **vsftpd** 的安全预防措施之一是确保在被动模式下，数据连接与控制连接来自相同的 IP 地址。启用此选项将绕过该预防措施。如果您计划执行本模块开头提到的那种三方 FTP 会话，或者如果您使用某种会被其干扰的安全隧道方案，则可能有理由这样做。否则，您最好保持禁用状态。

