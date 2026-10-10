
- 主机名
- 互联网地址
- 子网掩码（此项为可选）
- 十六进制站点地址或客户端 ID（此项为可选）
- 引导文件名
- 是否使用以太网或 IEEE 802.3 进行引导
- 是否向客户端或设备发送主机名

你可以根据系统当前是否禁用或启用来支持此功能，从“操作”菜单中选择“启用协议服务器”或“禁用协议服务器”。当你“启用协议服务器”时，同时也会启用简单文件传输协议（TFTP），引导设备使用它来获取引导文件。当你启用或禁用此功能时，/etc/inetd.conf 将被编辑。此文件包含有关系统上运行的网络服务的信息。如果 /etc/inetd.conf 中的某一行前面带有“#”，则该行被视为注释。读取此文件条目的守护进程是 /usr/sbin/inetd。在启用或禁用引导之前，您可能希望查看 /etc/inetd.conf 文件，了解哪些服务已启用。通过 SAM 进行更改后，您可以再次查看 /etc/inetd.conf，查看哪些内容已被修改。有关 /etc/inetd.conf 的安全相关信息，请参阅“系统访问”。以下是来自启用引导和 TFTP 的系统中 /etc/inetd.conf 文件开头的部分。此外，文件开头还提供了此文件中字段的简要说明：

```
# Configured using SAM by root
#
# Inetd reads its configuration information from this file upon ex-
# ecution and at some later time if it is reconfigured.
#
# A line in the configuration file has the following fields separated
# by tabs and/or spaces:
#
# service name          as in /etc/services
# socket type           either "stream" or "dgram"
# protocol              as in /etc/protocols
# wait/nowait           only applies to datagram sockets, stream
#                       sockets should specify nowait
# user                  name of user as whom the server should run
# server program        absolute pathname for the server inetd
#                       will execute
# server program args.  arguments server program uses as they
#               normally are starting with argv[0] which
#               is the name of the server.
#
# See the inetd.conf(4) manual page for more information.
#
#
#
#
# ARPA/Berkeley services
#
ftpd                stream  tcp     nowait  root    /usr/sbin/ftpd      ftpd -l
telnet              stream  tcp     nowait  root    /usr/bin/telnetd   telnetd

# Before uncommenting the "ftpp" entry below, please make sure
# that you have a "ftpp" user in /etc/passwd. If you don't
# have one, please consult the tftpd(8) manual entry for
# information about setting up this service.

tftpd               dgram   udp     wait    root    /usr/sbin/tftpd    tftpd
bootps              dgram   udp     wait    root    /usr/sbin/bootpd   bootpd
#finger             stream  tcp     nowait  bin     /usr/bin/fingerd   fingerd
login               stream  tcp     nowait  bin     /usr/sbin/rlogind  rlogind
shell               stream  tcp     nowait  bin     /usr/sbin/rexecd   rexecd
exec                stream  tcp     nowait  root    /usr/sbin/rexecd   rexecd
#ucp                stream  tcp     nowait  bin     /usr/sbin/ucp     ucp
```

如果您选择*固定地址设备客户端名称*，则可以从*操作*菜单中选择*修改*或*移除*，以更改与客户端相关的某个参数（例如其地址或子网掩码），或完全移除该客户端。

## DNS (BIND)

域名服务（DNS）是一种用于解析主机名到 IP 地址映射的名称服务器。HP-UX 使用 BIND（伯克利互联域），这是可用于实现 DNS 的名称服务之一。DNS 服务器负责解析网络或子网上的所有主机名。每个 DNS 客户端将依赖服务器代表其解决所有 IP 地址到主机名的映射问题。引导文件由服务器用于定位数据库文件。数据库文件将主机名映射到 IP 地址，并将 IP 地址映射到主机名。通过 SAM，可以轻松设置 DNS 服务器。

有关 DNS 及其设置和管理的更多信息，请参阅 HP-UX 手册*《安装和管理互联网服务》*。

## Hosts

*Hosts* 子区域用于维护系统中的默认网关和远程主机。当您进入此子区域时，您将收到系统中指定的主机列表。此信息从系统的*/etc/hosts*文件中检索。

然后您可以从*操作*菜单中*添加*新主机、*指定默认网关*、*修改*其中一个主机，或*移除*其中一个主机。在添加主机时，系统将要求提供与该主机相关的信息，包括其互联网地址、系统名称、系统别名以及注释。

## NIS

网络信息服务（NIS）是一种数据库系统，用于在系统网络中传播公共配置文件。在主服务器上管理诸如*/etc/passwd*、*/etc/hosts*和*/etc/automounter*等文件，这些文件由自动挂载器使用。NIS 以前被称为“黄页”，它将这些文件转换为自己的数据库文件，称为映射（maps），供 NIS 域中的客户端使用。当客户端请求信息时（例如用户登录并输入密码时），信息是从服务器检索的，而不是从客户端系统检索的。因此，此类信息只需在服务器上维护即可。

通过 SAM，可以配置、启用、禁用和移除 NIS 主服务器、从服务器和客户端。一旦建立主服务器、从服务器和客户端，您可以轻松地构建、修改并将各种映射推送到从服务器。

NIS 在可信系统上不可用。

## NIS+

HP-UX 11i 支持 NIS+。这不是 NIS 的增强功能，而是一种新服务，包括标准系统和可信系统以及非 HP-UX 系统。如果您已经使用 NIS，NIS+ 的兼容模式版本允许服务器响应来自 NIS 和 NIS+ 客户端的请求。当在可信系统上配置 NIS+ 时，SAM 的*审计和安全*区域中会显示一个新的子区域，即*受审计的 NIS+ 用户*。

## 名称服务切换

名称服务切换文件*/etc/nsswitch.conf*现在可以通过 SAM 进行配置。此服务允许您确定使用哪个名称服务（FILES、NIS、NIS+、DNS 或 COMPAT）来查找信息的优先级。除非您专门使用这些服务之一，否则应使用默认的 FILES。FILES 指定支持使用本地 /etc 目录来存储诸如*/etc/passwd*、*/etc/hosts*和*/etc/services*等管理文件。（COMPAT 用于 NIS+ 的兼容模式。）

有关名称服务切换文件及其设置的更多信息，请参阅 HP-UX 手册*《安装和管理 NFS 服务》*。

## 网络接口卡

此子区域用于配置系统中的任何网络卡。您可以从操作菜单中*启用*、*禁用*和*修改*网络卡，以及*修改系统名称*。在*添加 IP 逻辑接口*下，您可以为现有的网络卡添加额外的逻辑 IP 地址。

*网络接口卡*屏幕列出了系统中安装的网络卡，包括下面列出的信息。您可能需要扩大窗口或滚动以查看所有此信息。

- 卡类型，例如以太网、IEEE 802.3、令牌环、FDDI 等。
- 卡名称
- 硬件路径
- 状态，例如卡是否已启用
- 互联网地址
- 子网掩码
- 十六进制站点地址

在以太网卡的*配置*部分中包含*高级选项*，它将修改此卡的最大传输单元（MTU）。您系统中的其他卡也可以在此处进行配置，例如 ISDN、X.25、ATM 等。

## 网络服务

此子区域用于启用或禁用系统中的*部分*网络服务。您将在图 11-39 中识别出一些网络服务，这些服务对应于前面显示的 /etc/inetd.conf 文件中的服务。此屏幕有三列，分别是网络服务的名称、状态和*描述*。图 11-39 中*网络服务*子区域显示了一些可以管理的网络服务：

