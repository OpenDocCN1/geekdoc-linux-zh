
- NIS 服务器为配置为 NIS 客户端的 Linux 计算机提供如 `/etc/passwd` 和 `/etc/shadow` 等关键配置文件。

- Apache 服务器通过 HTTP 协议从其文档根目录向网络上的计算机发送 Web 页面。

- Samba 可以使用 SMB 协议向 Linux、UNIX、Macintosh 和 Windows 共享文件。

- NFS 可在 Linux、UNIX 和 Macintosh 系统之间原生共享文件。NFS 客户端通过挂载 NFS 服务器上的共享目录访问这些文件。

- FTP 可向任何具有 FTP 客户端实用程序的计算机共享文件，它是网上文件共享最常用的方法。Fedora 13 中的默认 FTP 守护进程是 `vsftpd`。

电子邮件服务器向用户传递电子邮件。它们还接受用户的新邮件并将其转发到互联网上的其他电子邮件服务器进行传递。Linux 系统上常用的电子邮件服务器是 `Sendmail` 和 `Postfix`。

许多大型应用程序将其数据存储在服务器上的数据库中。这些应用程序使用 SQL 语句分析并检索跨网络数据库中的信息。

`PostgreSQL` 是 Linux 系统上常用的数据库服务器，提供了高级配置和实用程序。

## 关键术语

- `ab` (Apache benchmark) 命令行：一个可用于获取 Apache Web 服务器性能基准测试的命令。

- `apachectl`：一个可用于启动、停止和重启 Apache Web 服务器，并检查 Apache 配置文件中语法错误的命令。

- Berkeley Internet Name Daemon (BIND)：所有 DNS 服务器和 DNS 配置文件均遵循的标准。

- BIND 配置工具：一个可用于生成和修改 DNS 名称守护进程使用的文件的图形化实用程序。

- `curl`：一个可从 Web 服务器获取 Web 页面的命令。

- database (数据库)：包含组织成表格的数据的文件。

- directive (指令)：配置文件中的某行。

- DNS 缓存文件：一个包含顶级 DNS 服务器 IP 地址的文件。

- document root (文档根)：存储分发给计算机的 Web 内容的目录。

- exporting (导出)：创建数据库表的过程。

- field (字段)：数据库表中的属性。

- File Transfer Protocol (FTP)：一种传输文件的协议。

- forward lookup (正向查询)：将名称解析为 IP 地址的 DNS 查询。

- `ftp`：用于传输文件的命令。

- jitter (抖动)：两台计算机的时间差异。

- infrastructure services (基础设施服务)：提供网络相关服务的服务。

- iterative query (迭代查询)：使用顶级 DNS 服务器解析的 DNS 请求。

- `mail`：用于查看电子邮件的命令。

- master (主服务器)：NIS 域中包含 NIS 映射主副本的计算机。

- `nmblookup`：在 Linux 系统上测试 NetBIOS 名称解析的命令。

- `ntpdate`：用于查看当前系统时间并同步 NTP 服务器时间的命令。

- `ntpq`：查询 NTP 服务器状态的命令。

- offset (偏移量)：两台计算机的时间差异。

- `Postfix`：Linux 系统上常用的易于配置的电子邮件守护进程。

- `PostgreSQL`：Linux 系统上常用的 SQL 服务器。

- `PostgreSQL` utility (PostgreSQL 实用程序)：用于 `PostgreSQL` 服务器上执行大多数管理的程序。

- primary DNS server (主 DNS 服务器)：包含区域读写副本的服务器。

- record (记录)：数据库表中的表示特定对象的行。

- relational database (关系型数据库)：包含通过共同字段链接的多个表的数据库。

- resource records (资源记录)：DNS 服务器区域内提供单个计算机解析的记录。

- reverse lookup (反向查询)：将 IP 地址解析为 FQDN 的 DNS 查询。

- secondary DNS server (备 DNS 服务器)：包含区域只读副本的服务器。也称为从 DNS 服务器。

- `Sendmail`：Fedora 13 中默认的电子邮件守护进程。

- Server Message Block (SMB)：Windows 计算机在 TCP/IP 网络上用于文件和打印机共享流量的协议。

- slave DNS server (从 DNS 服务器)：包含区域只读副本的服务器。

- `smb`：一个可用于连接到远程 Windows 或 Samba 服务器并传输文件的命令。

`smmpasswd` 命令：一个用于为用户生成 Samba 密码的命令。

SQL server：一种服务器服务，为其他程序和计算机提供访问数据库的能力。

strata 层级：NTP 分层次结构中使用的层级描述了服务器相对于原始时间源（如原子钟）的相对位置。

结构化查询语言 (SQL)：数据库服务器用于查询、添加和修改数据库内数据的语言。

table 表：一种组织数据记录和字段的数据库结构。

生存时间 (TTL)：计算机允许缓存从 DNS 服务器获取的名称信息的时间。

`tset` 命令：一个可以用于更改 Linux 计算机时间的命令。

Very FTP 守护进程 (`vsftpd`)：现代 Linux 发行版（包括 Fedora 13）中的默认 FTP 服务器程序。

Web 页面访问 (Web page hit)：从 Web 浏览器发送到 Web 服务器的单个 HTTP 请求。

zone 区域：域名空间的一部分由一个或多个 DNS 服务器管理。

区域传输 (zone transfer)：从主 DNS 服务器向从用 DNS 服务器复制某个区域的资源记录的过程。

## 复习习题

1. NFS 可以用于与运行 Microsoft Windows 操作系统的计算机原生共享文件。对或错？

2. Fedora 13 中哪个文件存储了 Apache 配置？
    a. `/etc/apache/httpd.conf`
    b. `/etc/apache.conf`
    c. `/etc/httpd.conf`
    d. `/etc/httpd/conf/httpd.conf`

3. 哪个 DNS 资源记录是其他记录的别名？
    a. `A`
    b. `AAAA`
    c. `CNAME`
    d. `NS`

4. NIS 客户端使用 NIS 记录访问它们的配置信息。对或错？

5. 使用哪个命令连接 `/etc/samba/smb.conf` 文件检查语法错误？
    a. `apachectl`
    b. `sambactl`
    c. `testparam`
    d. `psql`

![img](img/bafa5678973f896b93838a140b8f7840_638_0.png)

6. 你修改了 `/etc/aliases` 文件以包含一个新的电子邮件别名。然而，当你向该别名发送电子邮件时，无法送送。你应该做什么？
    a. 将该行添加到 `/etc/aliases.db` 文件中。
    b. 运行 `newaliases` 命令。
    c. 重启 `Sendmail` 守护进程。
    d. 退出系统并重新登录系统然后发送电子邮件。

7. 命令行 FTP 工具中的哪个命令可以更改本地计算机上的当前目录？
    a. `cd`
    b. `dir`
    c. `lcd`
    d. `get`

8. 你在你的电子邮件服务器的 25 端口开启了 `telnet` 会话。你可以在 `telnet` 会话中输入什么命令启动电子邮件会话？（选择所有适用）
    a. `START`
    b. `HELO`
    c. `EHLO`
    d. `WAZUP`

9. 使用 NFS 共享目录时必须执行以下哪些操作？（选择所有适用）
    a. 编辑 `/etc/exports` 文件。
    b. 使用 `mount` 命令将目录挂载到 `/etc/exports` 目录。
    c. 运行 `exportfs -a` 命令。
    d. 启动或重启 NFS 守护进程。

10. DHCP 客户端在需要新的 IP 配置时发送 `DHCPPREREQUEST` 数据包。对或错？

11. 使用哪个命令连接到文件服务器上的远程 Windows 缓存数据？
    a. `smbclient -L fileserver:data`
    b. `smbclient -L //fileserver/data`
    c. `smbclient //fileserver/data`
    d. `smbclient \fileserver\data`
