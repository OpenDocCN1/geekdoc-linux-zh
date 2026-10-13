
C. `/usr/bin/smclient`

D. `/etc/smb.conf`

16. 你对配置文件进行了几次更改，需要对其进行语法错误测试。你应该运行什么工具？

A. `smbmount`

B. `smclient`

C. `smbfs`

D. `testparm`

17. 你想强制 Samba 服务立即重新读取配置文件。你应该如何做？

A. `testparm`

B. `/etc/smb.conf`

C. `/rc.d/init.d/smb`

D. `restart`

18. Windows 用户抱怨他们看不到“网络邻”。`smb.conf` 中缺少了什么选项？

A. `Hidden = no`

B. `Browseable = yes`

C. `NetworkDisplay = on`

D. `Viewable = no`

19. 你的 Linux 工作站需要从创建了共享服务的 Windows 机器获取文件。你会引入哪种可能知道如何使用的工具？

A. `smbmount`

B. `smbfs`

C. `smclient`

D. `smb`

# RHCE

红帽认证工程师

# 第 9

# 网络管理

# 认证目标

- 9.01 DNS/Bind
- 9.02 Squid 代理服务器
- 9.03 NFS
- 9.04 互联网新闻
- 9.05 DHCP/Bootp
- 9.06 其他文件共享方法
- 9.07 时间同步
- 9.08 PPP 配置（作为客户端）使用 netcfg 及生成的文件

## 第 9 章：网络管理

Red Hat Linux 中更复杂的网络服务需要更高级的管理方法。虽然可以使用如 `linuxconf` 等图形化工具来协助配置 Linux 网络的各个方面，但通过熟悉网络服务的命令行环境，可以对这些概念有更具体的领悟。

本章的第一节讨论了域名命名系统（DNS）。该服务允许将人类可读的域名（例如 `www.redhat.com`）翻译为机器可读的 IP 地址（例如 `206.132.41.202`），反之亦然。下一节将介绍 Squid 代理服务器，它作为终端用户与 Web 网站之间的中介。缓存服务器可以显著提高用户在上网时的性能。关于网络文件系统（NFS）的一大章节讨论了在服务器和工作站之间强大且多功能的各种共享文件系统。关于互联网新闻的章节概述了旧而熟悉的 Usenet，以及如何在你的网络上运行服务器为本地用户提供服务。DHCP 允许 Linux 服务器分发动态 IP 地址。PPP 节演示了 Linux 服务器如何使用拨号连接进行个人或网络接入接入。

## 认证目标 9.0.1

## DNS/Bind

DNS 是域名命名系统（Domain Name System）。DNS 转换机器名称和 IP 地址。它实现从名称到地址以及从地址到名称映射，并为机器及其用户提供其他有用信息。

在本节中，将讨论两种服务器配置：仅缓存服务器和一个域主 DNS 服务器。`/etc/nsswitch.conf`、`/etc/resolv.conf` 和 `/etc/hosts` 等文件在 DNS 服务器上应该已经正确设置。此设置还假设服务器没有位于任何阻止名称查询的防火墙之后。

### DNS/Bind

Red Hat Linux 上运行着名为 `named` 的程序。这是由 Paul Vicie 为互联网软件协会协调的 BIND（Berkeley Internet Name Daemon）包的一部分。`named` 包含在大多数 Red Hat Linux 安装中，通常安装在 `/usr/sbin/named`。如果服务器上没有 `named`，可以从 Linux FTP 站点下载二进制文件，或从 `ftp/ftp.isc.org/isc/bind/src/cur-bind-8/` 获取最新源码。目前有两个版本的 BIND 可用：BIND 4 和 BIND 8。BIND 8 使用名为 `/etc/named.conf` 的配置文件，而 BIND 4 使用 `/etc/named.boot`。这两个版本之间截然不同，因此这里将只讨论 BIND 8。BIND 4 存在严重的安全问题，因此强烈建议使用 BIND 8。Red Hat 6.x 附带 Bind 8。

#### 仅缓存名称服务器

缓存名称服务器将找到名称查询的答案，并在下次需要时记住该答案。这将显著缩短查询的等待时间，特别是对于缓慢或共享的连接。第一个要查看的文件是 `/etc/named.conf`。它在 `named` 时被读取。目前，它应该只包含：

```
// Config file for caching only name server
options {
    directory "/var/named";
    // 如果你必须通过防火墙且
    // 运行不正常，取消此注释可能有帮助：
    // query-source port 53;

    zone "* {
        type hint;
        file "root.hints";
    }
    zone "0.0.127.in-addr.arpa" {
        type master;
        file "pz/127.0.0";
    }
```

`"directory"` 行告诉去哪里查找文件。所有后续命名的文件都相对于 `/var/named`：例如，`pz` 是 `/var/named` 下的一个目录：换句话说就是 `/var/named/pz`。根据 Linux 文件层次结构标准，`/var/named` 是正确的目录。名为 `/var/named/root.hints` 的文件在此命名。`/var/named/root.hints` 应该包含：

| | | |
|---|---|---|
| | 60 IN NS | G.ROOT-SERVERS.NET |
| | 60 IN NS | J.ROOT-SERVERS.NET |
| | 60 IN NS | K.ROOT-SERVERS.NET |
| | 60 IN NS | L.ROOT-SERVERS.NET |
| | 60 IN NS | M.ROOT-SERVERS.NET |
| | 60 IN NS | A.ROOT-SERVERS.NET |
| | 60 IN NS | H.ROOT-SERVERS.NET |
| | 60 IN NS | C.ROOT-SERVERS.NET |
| | 60 IN NS | D.ROOT-SERVERS.NET |
| | 60 IN NS | E.ROOT-SERVERS.NET |
| | 60 IN NS | I.ROOT-SERVERS.NET |
| | 60 IN NS | F.ROOT-SERVERS.NET |
| | | |
|---|---|---|
| G.ROOT-SERVERS.NET. | 60 IN A | 192.112.36.4 |
| J.ROOT-SERVERS.NET. | 60 IN A | 192.48.0.1 |
| K.ROOT-SERVERS.NET. | 60 IN A | 193.0.14.29 |
| L.ROOT-SERVERS.NET. | 60 IN A | 198.32.64.12 |
| M.ROOT-SERVERS.NET. | 60 IN A | 202.27.33 |
| A.ROOT-SERVERS.NET. | 60 IN A | 198.125.1.18 |
| H.ROOT-SERVERS.NET. | 60 IN A | 128.63.2.57 |
| B.ROOT-SERVERS.NET. | 60 IN A | 128.9.0.10 |
| C.ROOT-SERVERS.NET. | 60 IN A | 128.33.4.12 |
| D.ROOT-SERVERS.NET. | 60 IN A | 128.6.59 |
| E.ROOT-SERVERS.NET. | 60 IN A | 192.203.29.10 |
| I.ROOT-SERVERS.NET. | 60 IN A | 192.36.148.17 |
| F.ROOT-SERVERS.NET. | 60 IN A | 192.5.2.4 |

该文件描述了世界上根名称服务器。这些随时间变化且必须进行维护。维护此文件的 shell 脚本可以在节末尾找到。`named.conf` 的下一个部分应该包含：

```
0 IN SOA ns.your-domain.com. (
      ; Serial
      8 ; Refresh
      2 ; Expire
      1) ; Minimum TTL

NS ns.your-domain.com.
PTR localhost.
```

接下来，`/etc/resolv.conf` 应该像：

```
search subdomain.your-domain.com your-domain.com
nameserver 127.0.0.1
```
