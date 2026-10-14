

## squid — (版本 2.2.DEvel3, 1,861K)

Squid 是一款面向 Web 客户端的高性能代理缓存服务器，支持 FTP、gopher 和 HTTP 数据对象。与传统缓存软件不同，Squid 在单个非阻塞、I/O 驱动的进程中处理所有请求。Squid 将元数据和尤其是热门对象缓存在 RAM 中，缓存 DNS 查找结果，支持非阻塞 DNS 查找，并对失败的请求实现否定缓存。Squid 支持 SSL、广泛的访问控制和完整的请求日志记录。通过使用轻量级的 Internet 缓存协议，Squid 缓存可以按层次结构或网状结构排列，以进一步节省带宽。Squid 由一个主服务器程序 squid、一个域名系统查找程序 dnsserver、一个用于检索 FTP 数据的程序 ftpget 以及一些管理和客户端工具组成。当 Squid 启动时，它会生成可配置数量的 dnsserver 进程，每个进程可以执行单个阻塞式域名系统（DNS）查找。这减少了缓存等待 DNS 查找的时间。Squid 源自 ARPA 资助的 Harvest 项目。

## sysklogd — (版本 1.3.31, 112K)

[B]

sysklogd 包包含两个系统实用程序（syslogd 和 klogd），它们提供系统日志记录支持。Syslogd 和 klogd 以守护进程（后台进程）形式运行，并将系统消息记录到不同位置，如 sendmail 日志、安全日志、错误日志等。

## tcp_wrappers — (版本 7.6, 270K)

[W][S]

tcp_wrappers 包提供小型守护进程程序，可以监视和过滤针对 systat、finger、ftp、telnet、rlogin、rsh、exec、tftpd、talk 及其他网络服务的传入请求。如果您需要用于过滤传入网络服务请求的安全工具，请安装 tcp_wrappers 程序。

## tftp — (版本 0.10, 34K)

[W][S]

简单文件传输协议（TFTP）通常仅用于引导无盘工作站。tftp 包提供 TFTP 的用户界面，允许用户在远程机器之间传输文件。该程序和 TFTP 提供的安全性非常有限，除非确实需要，否则不应启用。TFTP 服务器从 /etc/inetd.conf 运行，并且在 Red Hat Linux 系统中默认禁用。

## timed — (版本 0.10, 74K)

[W][S]

timed 包包含 timed 守护进程和用于控制 timed 程序的 timedc 程序。Timed 将主机的时间与本地网络中其他机器的时间同步。timedc 程序用于控制和配置 timed 的操作。如果您需要使联网机器的时间保持同步的系统，请安装 timed 包。

## ucd-snmp — (版本 3.6.1, 1,504K)

[W][S]

SNMP（简单网络管理协议）是一种用于网络管理的协议（因此得名）。UCD-SNMP 项目包含各种 SNMP 工具：一个可扩展代理、一个 SNMP 库、用于向 SNMP 代理请求或设置信息的工具、用于生成和处理 SNMP 陷阱的工具、一个使用 SNMP 的 netstat 命令版本，以及一个 Tk/Perl MIB 浏览器。此包包含 snmpd 和 snmptrapd 守护进程、文档等。如果您需要网络管理工具，请安装 ucd-snmp 包。您可能还需要安装 ucd-snmp-utils 包，其中包含 UCD-SNMP 实用程序。

## wu-ftpd — (版本 2.4.2b18, 398K)

[S]

wu-ftpd 包包含 wu-ftpd FTP（文件传输协议）服务器守护进程。FTP 协议是一种在网络上和/或通过互联网在机器之间传输文件的方法。Wu-ftpd 的功能包括传输日志、命令日志、即时压缩和归档、用户类型和位置分类、每类限制、每目录上传权限、受限制的访客帐户、系统范围和每目录消息、目录别名、cpath、文件名过滤器和虚拟主机支持。如果您需要向远程用户提供 FTP 服务，请安装 wu-ftpd 包。

## xntp3 — (版本 5.93, 968K)

网络时间协议（NTP）用于将计算机的时间与另一个参考时间源同步。xntp3 包包含将通过 NTP 协议和 NTP 服务器将计算机时间同步到协调世界时（UTC）的实用程序和守护进程。Xntp3 包括 ntpdate（一个通过网络从远程机器获取日期和时间的程序）和 ntpd（一个持续调整系统时间的守护进程）。如果您需要工具来通过 NTP 协议保持系统时间同步，请安装 xntp3 包。

