
- 该条目禁用通过系统日志进行记录。
- 系统内存：增加物理内存，可以增加 OpenLDAP 缓存的大小以使用更多的内存。
- 接下来让我们学习 DNS 服务的优化。

# 优化 DNS 服务

优化 DNS 服务是为了减少进行 DNS 查询时涉及的延迟。通过减少发送到远程服务器（即使该服务器是您所连接的子网的服务）的 DNS 查询次数，你可以获得极佳的性能。通过维护 DNS 信息的本地缓存，你可以增强请求 DNS 服务的客户端程序的性能。

在客户端，运行纯缓存服务器（caching-only server）是增强性能的唯一选择。在服务器端，你有更广泛的选项来提高性能。让我们讨论一下。

让我们从优化 DNS 客户端开始。

## 提高 DNS 客户端的性能

在 DNS 客户端，可以在 `/etc/named.conf` 中修改服务器选项以运行纯缓存服务器。该文件在安装 BIND 时创建。默认情况下，BIND 允许所有主机进行区域传输（zone transfers）。区域传输仅对于主备服务器是必要的，对于 DNS 客户端则。你可以通过向 `/etc/named.conf` 中添加以下行来禁用它们：

```
allow-transfer {

   ;

};
```

你可以配置纯缓存服务器，使其仅响应来自特定主机的持续查询。在 `/etc/named.conf` 的 `options` 部分添加以下行，将 `www.xxx.yyy.zzz` 替换为您的网络 IP 地址：

```
allow-query {

   www.xxx.yyy.zzz;

   localhost;

};
```

你可以配置纯缓存服务器使其仅响应来自特定主机的递归查询。在 `/etc/named.conf` 的 `options` 部分添加以下行，将 `www.xxx.yyy.zzz` 替换为您的网络 IP 地址：

```
allow-recursion {

www.xxx.yyy.zzz;

localhost;

}
```

通常，纯缓存服务器无法直接访问互联网，因此它会创建一个缓存文件来存储 DNS 信息。你可以指定你想要转发请求的服务器 IP 地址。在 `/etc/named.conf` 的 `options` 部分添加以下行，将 `www.xxx.yyy.zzz` 替换为您的网络 IP 地址：

```
forwarders-transfer {

www.xxx.yyy.zzz;

}
```

接下来，提高 DNS 服务器的性能。

## 提高 DNS 服务器的性能

BIND 允许所有主机进行区域传输，这对于主备服务器是必要的。你可以通过向 `/etc/named.conf` 添加以下行来指定备服务器的 IP 地址，将 `www.xxx.yyy.zzz` 替换为备服务器的 IP 地址：

```
allow-transfer {

none;

}
```

你可以配置主服务器使其仅响应来自特定主机的持续查询。在 `/etc/named.conf` 的 `options` 部分添加以下行，将 `www.xxx.yyy.zzz` 替换为您的内部 IP 地址：

```
allow-query {

www.xxx.yyy.zzz;

localhost;

}
```

你可以配置备服务器使其仅响应来自特定主机的递归查询。在 `/etc/named.conf` 的 `options` 部分添加以下行，将 `www.xxx.yyy.zzz` 替换为您的内部 IP 地址：

```
allow-recursion {

www.xxx.yyy.zzz;

localhost;

}
```

让我们讨论一下日志。

## 使用日志

你可以配置纯缓存备服务器和主服务器自动轮转 `/var/log/named.log` 文件，以防止文件系统被旧信息填满。在 `/etc/logrotate.d` 文件（在 BIND 安装期间创建）中进行以下更改：

- 删除显示内容的行：

```
create 0644 named named
```

- 将行：

```
/bin/service named reload 2> /dev/null || true
```

改为：

```
/bin/kill -HUP 'cat /var/run/named.pid 2> /dev/null 2>' /dev/null || true
```

- 禁用 LAME 服务器的日志，因为这些服务器似乎是某个域名的名称服务器但实际上不是。使用以下行：

```
logging(

category lame-servers { null; };

);
```

让我们学习邮件服务的优化。

# 优化邮件服务

为了提高您的邮件服务的速度，你可以采取以下方法之一：使用多个邮件服务器将邮件处理负载分散到多个系统上，你还可以将 Sendmail 替换为另一个邮件服务器，以从 Sendmail 获取速度，并尝试多种方法来从 Postfix 获得更好的性能。

让我们学习帮助你从 Sendmail 获取速度的技巧以及可以从 Postfix 获得更好性能的方法。

首先关于提高 Sendmail 的性能

## 提高 Sendmail 的性能

你可以在 `/etc/sendmail.cf` 文件中配置许多选项来运行纯缓存服务器。[等待，检查上下文：……从 Sendmail 获取速度以及可以从 Postfix 获得更好性能的方法。

## 提高 Postfix 的性能

如果你有大量邮件停留在 Postfix 的输出队列中，你可能正在向繁忙的站点发送邮件。你可以通过为该站点创建传输（transport）项来解决此问题，并为每个连接设置更短的超时时间。

# 优化 Internet 服务

例如，假设有两个繁忙站点 `slow.com` 和 `reallysite.net` 你难以及时获取邮件。在 `/etc/postfix/transport` 中创建以下项：

| slow.com | deadbeasts: |
| reallysite.net | deadbeasts: |

接下来在 `/etc/postfix/main.cf` 中创建相应的项，将并发连接数增加到 50，允许更多邮件传输到 `slow.com` 和 `reallysite.net`：

| deadbeasts | unix - n | smtp |
| -0 | smtp_timeout=-5 | smtp_helo_timeout=5 |

上述 `/etc/postfix/master.cf` 中的项告诉 postfix，deadbeasts 的 SMTP 连接将在 5 秒后超时，且必须在 HELO 命令后 5 秒内开始 SMTP 事务，否则关闭连接。
为了减少传入邮件的超时时间，如下修改 `/etc/postfix/master.cf`：

| relay | unix - n | smtp |
| -0 | smtp_timeout=2 -o smtp_helo_timeout=2 |

如果 postfix 响应传入 SMTP 连接的速度慢，但 POP 或 IMAP 连接响应速度很快，那么你需要运行更多的 SMTP 服务进程。编辑 `main.cf` 中的 `smtpd` 项并增加进程限制。同时增加 `main.cf` 中的 `default_process_limit` 项以允许 FTP 服务。
让我们讨论如何优化 FTP 服务

# 优化 FTP 服务

众所周知，`vsftpd` 是一个安全且极快速的 FTP 守护进程。可以通过以下步骤获得更高的性能：

- 如果可能，禁用 `/etc/n.conf` 中用于 passwd、shadow 和 group 查询的 NIS 和 NISplus。这可以避免将必要的库加载到 vsftpd 内存空间，并避免使用 NIS 查询可以通过文件查找更快解决的问题。
- 将大目录拆分为较小目录以提高 CPU 性能。
- 限制并发连接数。
- 利用 vsftpd 的带宽限流功能，限制单个连接或连接类消耗的网络带宽。

## 第 6 章

### 优化 Web 服务

可以通过以下设置对 Apache 进行微调，以获得高效性能：

- 增加 `MaxClients` 设置会增加 httpd 服务器开始拒绝额外连接之前的最大并发连接数。你可以将其设置为 256。计算 `MaxClients` 的规则如下：

```
MaxClients = (Physical RAM - shared Memory for httpd Process) / Size
```
