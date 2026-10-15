
`604800 : (7 days) expire`

`3600 : (1 hour) TTL`

`IN NS aminews.com.`

`IN MX 5 aminews.com.`

`ns A 207.177.175.60`

`mail A 207.177.175.60`

`www A 207.177.175.61`

`wsd A 207.177.175.63`

`ftp CNAME ns`

记得前面的网络，这些 IP 地址没有分配给任何服务器。这些是 WSD Pro 在接口 #1 上响应的 IP 地址。在本章后面，你将配置 WSD Pro，使得 DNS、SMTP、POP3、IMAP 或 FTP 请求到达 `207.177.175.60` 时，会被重定向到 `192.168.2.3`。同样，当 HTTP 请求到达 `207.177.175.61` 时，会被重定向到 `192.168.2.1` 或 `192.168.2.2`。列表 20-9 显示 `aminews.com` 的反向 DNS 配置。

### 列表 20-9：`/var/named/aminews.rev`

```
@ IN SOA aminews.com. hostmaster.aminews.com. (
      199902401 : serial YYYYMMDD
      7200 : refresh
      3600 : (1 hour) retry
      43200 : (12 hours) expire
      3600 : (1 hour) minimal TTL
IN NS aminews.com.
IN MX 5 aminews.com.
60 IN PTR aminews.com.
60 IN PTR mail.aminews.com.
61 IN PTR www.aminews.com.
63 IN PTR wsd.aminews.com.
```

用于 NFS 骨干网络的域分别具有列表 20-10 和 20-11 所示的正向和反向配置文件。

# 第六部分：性能优化

### 列表 20-10：`/var/named/aminews-lan.db`

```
@ IN SOA aminews-lan.com. hostmaster.aminews-lan.com. (
      199902150 : serial YYYYMMDD
      7200 : refresh
      3600 : (1 hour) retry
      604800 : (7 days) expire
      3600 : (1 hour) minimal TTL
```

@ 名称服务器和邮件交换记录
`IN NS aminews-lan.com.`

- A 记录
`ns A 192.168.1.60`
`www1 A 192.168.1.61`
`www2 A 192.168.1.62`

`ns.aminews-lan.com.` 被分配了 `192.168.1.60`，这是 DNS/FTP/SMTP/POP3/IMAP 服务器上 `eth1` 的 IP 地址。另外两个 IP 地址被分配给 Web 服务器上的 eth 接口。

### 列表 20-11：`/var/named/aminews-lan.rev`

```
@ IN SOA aminews-lan.com. hostmaster.aminews-lan.com. (
      199902150 : serial YYYYMMDD
      7200 : refresh
      3600 : (1 hour) retry
      43200 : (12 hours) expire
      3600 : (1 hour) minimal TTL
```

@ 名称服务器和邮件交换记录
`IN NS aminews-lan.com.`

- PTR 记录
`60 IN PTR ns.aminews-lan.com.`
`61 IN PTR www1.aminews-lan.com.`
`62 IN PTR www2.aminews-lan.com.`
```

### 列表 20-12：`/etc/hosts`

```
127.0.0.1         localhost
192.168.1.60      ns.aminews-lan.com
192.168.1.61      www1.aminews-lan.com
192.168.1.62      www2.aminews-lan.com
```

在这里，`/www/data` 目录通过 NFS 骨干局域网导出到 `www1.aminews-lan.com` (`192.168.1.61`) 和 `www2.aminews-lan.com` (`192.168.1.62`) Web 服务器。这两台服务器上的所有具有读/写 (`rw`) 权限的 CGI 都将获得完全访问权限。

## 设置邮件服务器 (SMTP/POP3/IMAP)

由于你希望让 `mail.aminews.com` 上的 `sendmail` 守护进程处理所有邮件，你必须配置 Web 服务器上的 `sendmail` 守护进程，将邮件中继到该服务器。换句话说，`mail.aminews.com` 上的 `sendmail` 服务器已成为 Web 服务器上其他 `sendmail` 守护进程的智能主机（smart host）。这要求你在 `/etc/mail/relay-domain` 文件中添加 Web 服务器。因此，你应该向此文件添加 `192.168.2.1` 和 `192.168.2.2`，以便 `mail.aminews.com` 服务器上的 `sendmail` 允许另外两个 `sendmail` 守护进程通过它中继邮件。

你应该在 `/etc/mail/sendmail.cw` 文件中添加 `aminews.com` 域名，以便 `sendmail` 守护进程处理所有来自 `aminews.com` 的邮件。阅读第 10 章学习如何测试 `sendmail` 守护进程。在更改配置文件后，忘记重启 `sendmail` 服务器。

SuSE Linux 自带并包含在第一张配套光盘上的默认 POP3/IMAP 服务器在此环境中工作不需要任何特殊配置。你只需要确保它按常例设置即可。

![](img/1d90939eac39ca76d12e353542e54751_589_0.png)

要了解更多关于如何设置 POP3/IMAP，请访问第 10 章。

## 设置 FTP 服务器

阅读第 12 章启用 FTP 服务器 —— 这是唯一需要做的配置。

## 在域名服务器上设置 rdist

你必须在域名服务器上配置 `rdist`，使其能够将适当目录下的所有 Web 相关文件分发 Web 服务器。例如，如果你将所有 Web 文件和目录都放在 `/www` 分区下，你可以设置 `rdist` 通过骨干局域网将该分区中的所有文件分发到 Web 服务器。列表 20-16 显示了一个 `distfile` 示例。

# 第 20 章：构建多服务器 Web 网络

### 列表 20-16：示例 distfile 文件

```
#
# rdist 的 distfile
#
# 用于将文件从 ns.aminews-lan.com
# 分发到 www[12].aminews-lan.com 系统。
#
# $Author$
# $Version$
# $Date$
# $Id$

HOSTS = (http://www.aminews-lan.com http://www2.aminews-lan.com)

FILES = (/www)

CLUDE_DIR = (/www/data)

$(FILES) -> $(HOSTS)
    install :
    except $(CLUDE_DIR);
```

你可以使用此 `distfile` 将 `/www` 中的所有文件（`/www/data` 因为其已经为 CGI 应用程序挂载了 NFS）分发到 `www.aminews-lan.com` 和 `www2.aminews-lan.com` 主机。`distfile` 预期 Web 服务器上存在一个名为 `http` 的用户。该 `http` 用户还必须配置 `.hosts` 文件，允许 `ns.aminews-lan.com` 主机分发文件。你可以使用列表 20-17 所示的 `rdist.sh` 脚本运行 `rdist`。

### 列表 20-17：`rdist.sh` 脚本

```
#!/bin/sh
#
# 此脚本运行 rdist 以更新 Web 服务器
# 非路由的局域网 aminews-lan.com。该脚本
# 由 cron 按固定间隔运行。
#
# /etc/rc.d/local 启动脚本以清理
# 可能关机时留下的临时文件。
# 此过程还删除了
# 日志文件。
#
# $Author$
# $Version$
# $Id$
# $Date$
```
