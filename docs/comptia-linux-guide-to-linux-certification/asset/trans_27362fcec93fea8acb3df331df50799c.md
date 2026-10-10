
## 关键术语

- **ftcp 命令** 在大多数操作系统中都可以找到的命令行 FTP 客户端程序。
- **hwclock 命令** 可用于查看和修改计算机 BIOS 中系统时钟的命令。
- **基础架构服务** 为网络上的其他计算机提供 TCP 配置、名称解析、时间同步或系统配置的服务。
- **迭代查询** 未使用顶级 DNS 服务器而解析完成的 DNS 解析请求。
- **抖动** 几个不同 NTP 服务器时间测量值之间的差异。
- **mail 命令** 在 UNIX、Linux 和 Macintosh 系统上常见的电子邮件客户端。
- **主 DNS 服务器** 参见*主要 DNS 服务器*。
- **NetBIOS** 一种由 Windows 计算机使用的协议，它向文件和打印机共享流量添加一个唯一的 15 个字符的名称。
- **网络文件系统 (NFS)** 一组可用于在网络上的 UNIX、Linux 和 Macintosh 计算机之间原生共享文件的软件组件。
- **网络信息服务 (NIS)** 一组可用于标准化多个不同 Linux 和 UNIX 计算机之间配置文件的软件组件。
- **网络时间协议 (NTP)** 一种可用于从 Internet 上的其他计算机获取时间信息的协议。
- **newaliases 命令** 可用于基于 */etc/aliases* 文件中的条目重建电子邮件别名数据库的命令。
- **NIS 客户端** NIS 域中的计算机，从 NIS 主服务器或 NIS 从服务器接收配置。
- **NIS 域** 共享相同 NIS 配置的计算机组。
- **NIS 映射** NIS 域内计算机共享的系统配置。
- **NIS 主服务器** NIS 域中包含所有 NIS 映射主副本的计算机。
- **NIS 从服务器** NIS 域中从 NIS 主服务器接收所有 NIS 映射只读副本的计算机。
- **nmblookup 命令** 可用于测试 Linux 系统上 NetBIOS 名称解析的命令。
- **NTP 守护进程 (ntpd)** 在 Linux 计算机上提供时间同步服务的最常见守护进程。
- **ntpdate 命令** 可用于查看当前系统时间以及将系统时间与 NTP 服务器同步的命令。
- **ntpq 命令** 可用于查询 NTP 服务器或客户端状态的命令。
- **偏移量** 使用 NTP 协议的两台计算机之间的时间差异。
- **Postfix** 在 Linux 系统上使用的常见电子邮件服务器守护进程。
- **PostgreSQL** 在 Linux 系统上使用的常见 SQL 服务器。
- **PostgreSQL 实用工具** 用于在 PostgreSQL 服务器上执行大多数数据库管理的程序。
- **主要 DNS 服务器** 包含区域读写副本的 DNS 服务器。
- **pgsql 命令** 用于启动 PostgreSQL 实用工具的命令。
- **记录** 数据库表中的一行，代表一个特定对象。
- **递归查询** 使用顶级 DNS 服务器解析完成的 DNS 解析请求。
- **关系数据库** 包含通过公共字段链接的多个表的数据库。
- **资源记录** DNS 服务器区域内为个别计算机提供名称解析的记录。
- **反向查找** 一种 DNS 名称解析请求，其中 IP 地址被解析为 FQDN。
- **次要 DNS 服务器** 包含区域只读副本的 DNS 服务器。
- **服务器消息块 (SMB)** Windows 计算机在 TCP/IP 网络上用于格式化文件和打印机共享流量的协议。
- **showmount 命令** 用于查看远程计算机上 NFS 共享目录的命令。
- **从 DNS 服务器** 参见*次要 DNS 服务器*。
- **smbclient 命令** 可用于连接到远程 Windows 或 Samba 服务器并传输文件的命令。
- **smbpasswd 命令** 用于为用户生成 Samba 密码的命令。
- **层级** NTP 层级内使用的级别，描述服务器相对于原始时间源（如原子钟）的相对位置。
- **结构化查询语言 (SQL)** 数据库服务器用于查询、添加和修改数据库中数据的语言。
- **SQL 服务器** 使其他程序和计算机能够访问数据库的服务器服务。
- **表** 使用记录和字段组织数据的数据库结构。
- **生存时间 (TTL)** 计算机被允许缓存从 DNS 服务器获取的名称解析信息的时间量。
- **testparm 命令** 可用于检查 Samba 配置文件中语法错误以及显示当前 Samba 配置的命令。
- **tzelselect 命令** 可用于更改 Linux 计算机时区的命令。
- **Very Secure FTP 守护进程 (vsftpd)** 现代 Linux 发行版中使用的默认 FTP 服务器程序。
- **Web 页面命中** 从 Web 浏览器发送到 Web 服务器的单个 HTTP 请求。
- **区域** 由一个或多个 DNS 服务器管理的域名空间的一部分。
- **区域传输** 从主 DNS 服务器到从 DNS 服务器复制区域资源记录的过程。

## 复习题

1. 可以使用 NFS 与运行 Microsoft Windows 操作系统的计算机原生共享文件。判断对错？

2. 在 Fedora 20 中，哪个文件存储 Apache 配置？
    a. `/etc/apache2/httpd.conf`
    b. `/etc/apache2.conf`
    c. `/etc/httpd.conf`
    d. `/etc/httpd/conf/httpd.conf`

3. 哪种 DNS 资源记录是其他记录的别名？
    a. A
    b. AAAA
    c. CNAME
    d. NS

4. NIS 客户端使用 NIS 记录访问其配置信息。判断对错？

5. 哪个命令可用于连接并检查 `/etc/samba/smb.conf` 文件的语法错误？
    a. `apachecl`
    b. `sambackl`
    c. `testparm`
    d. `psql`

6. 你修改了 `/etc/aliases` 文件以包含一个新的电子邮件别名。但是，当你向该别名发送电子邮件时，它无法送达。你应该怎么做？
    a. 将行添加到 `/etc/aliases.db` 文件代替。
    b. 运行 `newaliases` 命令。
    c. 重启 Postfix 守护进程。
    d. 注销系统，然后重新登录系统并重发邮件。

7. 在命令行 FTP 实用程序中，哪个命令可用于更改本地计算机上的当前目录？
    a. `cd`
    b. `dir`
    c. `lcd`
    d. `get`

8. 你已在电子邮件服务器上打开了端口 25 的 telnet 会话。你可以在 telnet 会话中输入什么命令来开始电子邮件会话？（选择所有适用项。）
    a. `START`
    b. `HELO`
    c. `EHLO`
    d. `WAZUP`

9. 为了使用 NFS 共享目录，你必须执行以下哪些操作？（选择所有适用项。）
    a. 编辑 `/etc/exports` 文件。
    b. 使用 `mount` 命令将目录挂载到 `/etc/exports` 目录。
    c. 运行 `exportfs -a` 命令。
    d. 启动或重启 NFS 守护进程。

10. DHCP 客户端在需要新的 IP 配置时会发送 DHCPREQUEST 数据包。判断对错？

11. 哪个命令可用于连接到名为 data 的远程 Windows 共享，服务器名为 filesrver？
    a. `smbclient -L filesrver:data`
    b. `smbclient -L //filesrver/data`
    c. `smbclient //filesrver/data`
    d. `smbclient \\filesrver\data`

12. Apache 配置文件中修改 Apache 功能的行称为指令。判断对错？

13. 以下哪些可用于在 PostgreSQL 中创建数据库？（选择所有适用项。）
    a. PostgreSQL 实用工具中的 `CREATE DATABASE` 语句。
    b. PostgreSQL 实用工具中的 `ADD DATABASE` 语句。
    c. `adddb` 命令。
    d. `createdb` 命令。

14. Stratum 1 NTP 服务器不从其他 NTP 服务器获取时间信息。判断对错？

15. 要将你的计算机转变为 DNS 服务器，你必须做什么？（选择所有适用项。）
    a. 创建区域文件。
    b. 为 DNS 查找创建资源记录。
    c. 创建 NIS 映射。
    d. 运行名称守护进程 (named)。

