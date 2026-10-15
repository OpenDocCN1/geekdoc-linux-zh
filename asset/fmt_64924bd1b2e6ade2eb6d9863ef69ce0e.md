
诚然，这只是两个对内存和 CPU 影响微乎其微的模块，但每一点小改进都有帮助。

- **以较低的值运行 XFree86。** 通过提高 XFree86 其他进程的优先级，你将获得响应更快的系统。这样做的方法之一是使用命令 `nice -n 10 X0` 启动 XFree86。使用此命令需要 root 权限。如果你从 XDM、GDM 或 KDM 运行 XFree86，请修改服务器文件（`/etc/X11/xdm/xservers`）。XDM 是 X 显示管理器，GDM 是 GNOME 显示管理器，KDM 是 KDE 显示管理器。这三个服务都为用户提供图形化登录。

找到类似于下面的内容的行：

```
:0 local /usr/X11R/bin/X
```

将其更改为如下所示的内容，然后退出并重启 X。

```
:0 local nice -10 /usr/X11R/bin/X
```

重启 X。如果你长时间运行 XFree86，内存会作为缓存被占用。偶尔重启 X 可以刷新潜在的过时缓存并释放可能因泄漏丢失的内存。

## 优化 NFS

这里有一些你可以使用的技巧，可以增加系统网络文件系统 `NFS` 服务器的性能。这里的大多数技巧都能帮助你通过为服务器配置以最佳性能，从而为你的用户提供更好的服务。

# 第 20 章：优化系统的十条技巧

- `dns proxy`: 除非你的 Samba 服务器充当 Windows 互联网命名服务 `WINS` 服务器，否则此选项应设置为 `no`。将此选项设置为 `no` 可以防止服务器进行不必要的名称查找，同时提高系统性能。
- `debug level`: 此选项的调试级别应设置为 `2` 或更小。调试级别高于 `2` 会导致服务器在每次操作后都刷新日志文件，这确实是一个非常耗时的过程。
- `Level2 oplocks`: 此选项允许在客户端机器上对下载的文件进行缓存。将此选项设置为 `true` 可以提高系统性能。

## 优化 DNS

你可以通过对 `/etc/named.custom` 文件的 `options` 部分进行一些更改，来提高主域域名服务器的性能。你可以做的第一个更改是仅允许主服务器和从服务器之间进行区域传输。默认情况下，`BIND` 允许所有主机之间进行区域传输。但是，由于区域传输只需要在主从服务器之间进行，你可以指定从服务器的 IP 地址，以便主服务器只查找该服务器。在 `/etc/named.custom` 的 `options` 部分中输入以下行：

```
allow-transfer { enter IP address of slave server; };
```

下一个更改是配置你的主服务器仅响应来自指定主机的查询，这些主机是位于防火墙内的其他计算机。在 `/etc/named.conf` 中输入以下行。

```
allow-query { enter your internal network number here; localhost; };
```

如果你设置了缓存名称服务器，可以配置它们仅响应来自指定主机的递归请求。同样，指定的主机是位于防火墙内的其他计算机。在你的仅缓存服务器的 `/etc/named.conf` 中输入以下行：

```
Allow-recursion { enter your internal network number here; localhost; };
```

你对调整域名命名系统 `DNS` 设置所可以做的最后一件事是更改 DNS 日志文件的性能。你可以做两处更改。第一，你可以启用对无效服务器 `lame servers` 的记录。无效服务器看起来是某个域的名称服务器，但实际上并不是。通过排除这些服务器，你可以减少系统资源消耗。在 `/etc/named.conf` 中添加以下行：

```
Logging {

  category lame-servers { null };

};
```

# 第六部分：十之篇

接下来，配置你的日志自动轮转——即自动删除——以防止日志文件填满系统。

当你安装 `BIND` 时，系统会创建一个文件 `/etc/logrotate.d/named`。该文件的列表所示：

```
/var/log/named.log (

missingok

  create 0644 named named

  postrotate

    /sbin/service named reload 2> /dev/null > /dev/null || true

endscript
```

删除此行：

```
create 0644 named named
```

并将该行

```
/sbin/service named reload 2> /dev/null > /dev/null || true
```

更改为以下内容：

```
/bin/kill -HUP 'cat /var/run/named.pid 2> /dev/null > /dev/null || true'
```

保存更改并重启 `named` 服务器。

## 优化 Sendmail

在本节中，我将为你提供一些你可以使用的技巧，以保持 `Sendmail` 服务器高效运行。`Sendmail` 尝试发送的所有消息首先发送到位于 `/var/spool/mailqueue` 的邮件队列中。如果可能，队列中的消息将发送到目的地。有时，消息由于各种原因无法递送。这些未递送的消息堆积在邮件队列中，最终会导致你的系统性能受损。定期检查邮件队列是否有无法递送的邮件并强制 `Sendmail` 清空队列。

要查看邮件队列的内容，可以使用列表 20-1 所示的 `mailq` 命令：

列表 20-1: `mailq` 命令

```
Queue-size  Size     Time     Owner  Sender                    Recipient

-------------------------------------------------------------

     1  1234 Oct 1 10:00  root  root@localhost          user@example.com

     2  5678 Oct 1 10:05  root  root@localhost          admin@example.com
```
