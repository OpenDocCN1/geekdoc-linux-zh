

7. 在 /etc/ftpassess 中设置 guestgroup。因为您希望真实用户 mrfrog 成为访客用户，所以需要将 mrfrog 的组（也称为 mrfrog）添加到 guestgroup 组列表中。例如，

```
guestgroup  mrfrog
```

允许 mrfrog 组（在 /etc/group 中查找）的任何成员成为访客用户。换句话说，FTP 服务器将执行 chroot 操作。对于 mrfrog 用户，FTP 服务器将 chroot 到 /home/mrfrog。

8. 测试账户。通过 FTP 连接服务器并以 mrfrog 身份登录。如果一切设置正确，您只会看到该用户的主目录。尝试上传文件或创建目录。您应该被允许执行这些操作。然而，mrfrog 是否被允许删除、覆盖或重命名文件，取决于您在 /etc/ftpassess 中为这些操作设置的权限。例如，默认的 /etc/ftpassess 包含以下行：

```
chmod
    no    guest,anonymous
delete
    no    guest,anonymous
overwrite   no    guest,anonymous
rename
    no    guest,anonymous
```

这些行禁止访客账户执行 chmod、delete、overwrite 或 rename 操作。如果您希望允许访客账户执行这些操作，请将这些行默认类型列表中的 guest 移除，使其变成以下行：

```
chmod
    no    anonymous
delete
    no    anonymous
overwrite   no    anonymous
rename
    no    anonymous
```

如果您不想保留 anonftp 软件包，或者不希望在您的 FTP 服务器上拥有匿名 FTP 功能，请从相应的 (-ftp) 目录中移除软件包文件，或者直接运行以下命令：

```
rpm -e  anonftp-3.0-6.i386.rpm
```

不要忘记使用正确的文件名，因为您的版本或架构可能与此处描述的有所不同。

对于 FTP 服务而言，日志记录非常重要，因为您需要能够知道谁在对您的文件做什么。**wu-ftpd** 服务器将传输记录到 `xferlog` 文件中，该文件通常位于 `/var/log` 目录中。您可以使用前面讨论的 `log` 命令和 `log transfers` 关键字来自定义日志记录。

如果您有兴趣定期监控 `xferlog`，请尝试 **Dumpxfer**，您可以从 `ftp://ftp.microimages.com/tools/dumpxfer.1.2.tar.gz` 下载它。

## 使用商业 FTP 服务器

**wu-ftpd** 服务器是免费的，在提供标准 FTP 服务时具有相对较好的可配置性。然而，**wu-ftpd** 在高负载下的性能表现不佳，并且没有非常干净且可定制虚拟 FTP 服务解决方案。如果您需要高性能的 FTP 服务器，并且不介意付费，请考虑 **NcFTPd** 软件包，这是一款具有以下有趣特性的商业 FTP 服务器：

- 不通过 `inetd` 运行，因此启动性能比 **wu-ftpd** 好得多。基于 `inetd` 的进程从未打算用于高性能场景。
- 内置目录列表功能，而 **wu-ftpd** 必须为每个目录列表请求生成一个 `ls` 进程。因此，**NcFTPd** 在处理目录列表方面表现更好。它甚至可以将在内存中缓存目录列表，以在大型 FTP 站点中提供更快的此类列表传输。
- 高度可配置的虚拟主机功能。每个虚拟主机可以拥有自己的欢迎消息、匿名 FTP 目录树、密码认证方案、用户限制和日志文件。

通过从 `http://www.ncftp.com/download/` 下载来试用这款商业 FTP 服务器。

**NcFTPd** 对具有特定顶级域（例如 `.edu` 和 `.us`）的教育组织免费。

## 使用简单文件传输协议服务器

您可能已经安装了 TFTP 服务器。它被称为 tftpd 服务器。它实际上不是一个 FTP 服务器，因为它使用的是简单文件传输协议（Trivial File Transfer Protocol）而不是文件传输协议（File Transfer Protocol）。TFTP 使用 IP 上的 UDP，这是一种不可靠的、面向报文的传输方式。FTP 使用 IP 上的 TCP，这是一种可靠的、面向流的传输方式。TFTP 没有安全机制。FTP 有用户认证机制以确保安全。

然而，TFTP 服务器的工作方式与 FTP 服务器大致相同。唯一的主要区别是，它*不*适用于除类似匿名 FTP 且不使用认证的文件传输之外的任何其他用途。

许多人主要将 TFTP 与引导协议结合使用，以加载无盘工作站，例如 X 窗口系统终端。TFTP 服务在 `/etc/inetd.conf` 文件中默认是禁用的。您可以通过从以下行中移除 \#（注释符号）来启用它：

```
# tftp dgram udp wait root /usr/sbin/tcpd \
 in.tftpd /tftpboot
```

启用上一行后，重启 inetd 服务器以使更改生效。请注意，`/tftpboot` 是 TFTP 客户端可以访问的目录。确保此目录中不包含任何您不希望与他人共享的文件。请记住，访问此文件不需要认证，因此任何能够访问您服务器的人都可以访问此目录。您可能还希望仅允许对该目录中的文件进行只读访问。

# 第 11 章

# 使用 Samba 共享文件和打印机

## 安装 Samba

如果您在 Red Hat Linux 安装期间选择了 DOS/Windows 兼容性选项，则 Samba RPM 软件包会自动安装。但是，如果您在安装期间没有安装 Samba 软件包，您可以随时使用 rpm 命令安装它们。例如，要为 x86 Red Hat Linux 系统安装 Samba 客户端/服务器软件包，我从官方 Red Hat CD-ROM 的 /RedHat/RPMS 目录运行了以下命令：

```
rpm -ivh samba-version.1386.rpm
```

使用此命令安装 Samba 软件包时，不要忘记将 samba-version.1386.rpm 替换为实际的软件包文件名。

## 配置 Samba

安装 Samba RPM 软件包时，它会在您的 /etc/samba 目录中安装一个名为 smb.conf 的配置文件。清单 11-1 显示了默认的 /etc/samba/smb.conf，其中包含一些小的格式更改。

## 清单 11-1 默认的 /etc/samba/smb.conf 文件

```
/etc/samba/smb.conf

# This is the main Samba configuration file.
# You should read the smb.conf(5) manual page in
# order to understand the options listed
# here. Samba has a huge number of configurable
# options (perhaps too
# many!) most of which are not shown in this example
#
# Any line which starts with a ; (semi-colon) or a
# (hash) is a comment and is ignored. In this example
# we will use a for commentary and a;
# for parts of the config file that you
# may wish to enable
#
# NOTE: Whenever you modify this file you should
# run the command "testparm" to check that you
# have not many any basic syntactic errors.

# =================Global Settings ======================
[global]

# workgroup = NT-Domain-Name or Workgroup-Name
workgroup = MYGROUP

# server string is the equivalent of the NT
# Description field
server string = Samba Server

# This option is important for security.
# It allows you to restrict connections to machines
# which are on your local network. The following
# example restricts access to two C class networks and
# the "loopback" interface. For more examples of
# the syntax see

# the smb.conf man page
# hosts allow = 192.168.1. 192.168.2. 127.

# if you want to automatically load your printer list rather
# than setting them up individually then you'll need this
   printcap name = /etc/printcap
   load printers = yes

# It should not be necessary to spell out the print system type unless
# yours is non-standard. Currently supported print systems include:
#  bsd, sysv, plp, iprmg, aix, hpux, qpx
   printing = iprpg

# Uncomment this if you want a guest account, you must add this to /etc/passwd
# otherwise the user "nobody" is used
# guest account = pcguest

# this tells Samba to use a separate log file for each machine
# that connects
   log file = /var/log/samba/%m.log

# Put a capping on the size of the log files (in Kb).
   max log size = 0

# Security mode. Most people will want user level security. See
# security_level.txt for details.
   security = user

# Use password server option only with security = server or
# security = domain
#   password server = <NT-Server-Name>

# Password level allows matching of _n_ characters of the password for
# all combinations of upper and lower case.
# password level = 8
```

