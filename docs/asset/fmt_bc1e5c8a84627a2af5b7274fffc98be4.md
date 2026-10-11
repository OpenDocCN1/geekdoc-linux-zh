
`pam_vsfpd_name=ftp` 开启了访用户功能。`guest_username=authors` 允许所有登录指向 `authors` 账户。`local_enable=YES` 允许本地用户登录，这对访用户是必须的。`anon_readable_only=NO` 使访用户可以读取目录内容，而 `root_local_users=YES` 导致 `vsfpd` 将 `authors` 用户 `chroot` 到 `/var/ftp/root`。

在做出更改后，启动或重启 `vsfpd` 服务：

```bash
# service vsfpd restart
```

使用你上面创建的任意用户名/密码组合来测试配置。

让我们尝试在 SSL 之上运行 `vsfppd`。

## 通过 SSL 运行 vsftpd

`Vsftpd` 使用安全套接层 (`SSL`) 支持来加密文件传输过程中的 FTP 控制通道。要在 `vsftpd` 中使用 `SSL`，你需要在 `/etc/vsftpd/vsftpd.conf` 文件中设置以下配置。

向 `/etc/vsftpd/vsftpd.conf` 添加以下条目：

```conf
ssl_enable=YES
allow_anon_ssl=YES
force_local_data_ssl=YES
force_local_logins_ssl=YES
ssl_tlv1=YES
```

创建一个自签名 RSA 证书文件：

```bash
# cd /usr/share/ssl/certs
```

按回车并等待终端返回输出。现在，启动或重启 `vsftpd` 服务器：

```bash
# service vsfpd start
```

在上一节讨论了 Open FTP 服务器的配置后，让我们讨论一下 SFTP 服务器。

## 使用 SFTP

除了在 SSL 之上运行 `vsftpd` 之外，你还可以使用 `sftp-server`。`sftp-server` 是 OpenSSH 安全客户端和服务器程序套件的一部分。它实现了 FTP 协议的服务器端。当 SSH 守护进程 `sshd` 接收到传入的 FTP 请求时，会调用它。

使用以下命令检查系统中是否安装了所需的 OpenSSH 软件包：

```bash
[root@vadeinmein ~]# rpmquery openssh-{clients,askpass,server}
openssh-clients-5.2pl-6.fc11.i586
openssh-clients-5.2pl-6.fc11.i586
openssh-askpass-5.2pl-6.fc11.i586
openssh-server-5.2pl-6.fc11.i586
```

如果未安装这些软件包，请在继续操作之前安装。然后检查 `/etc/ssh/sshd_config` 中是否存在以下行：

| 子系统 | 路径 |
| :--- | :--- |
| sftp | /usr/libexec/openssh/sftp-server |

该行告诉 `sshd` 执行 `/usr/libexec/openssh/sftp-server` 来提供 SFTP 子系统。

如果不存在，请将此行添加到 `/etc/ssh/sshd_config` 并重启 SSH 守护进程。

```bash
# service sshd restart
```

请参考实验。

# 第4章

## 总结

本章介绍了 BIND 的概览。之后，让我们总结一下要点。

### 练习题

1. 系统在哪个文件中进行查找？
   - a. `named.conf`
   - b. `resolve.conf`
   - c. `host.conf`
   **答案: c**

2. 哪些是必须的？
   - a. `named.conf`
   - b. 以上 a 和 b
   - c. 都不是
   **答案: b**

3. 正确的顺序是哪个？
   - a. MUA, MTA
   - b. MTA, MUA
   - c. 都不是
   **答案: a**

4. 默认是哪个？
   - a. MUA
   - b. Postfix
   - c. 都不是
   **答案: d**

5. `vsftp` 一词代表？
   - a. Vast FTP daemon
   - b. Secure FTP daemon
   - c. Simple FTP daemon
   **答案: b**

## 配置 Apache

Apache 的配置非常简单，因为开发者和维护者对其开发付出了持续努力。在配置 Apache Web 服务器之前，请确保你的系统中已安装了 Apache。使用以下命令验证你的系统中是否安装了 Apache：

```
# rpmqueryhttpd
httpd-2.2.15-fc11.i586

# rpmqueryhttpd [manual,devel]
httpd-manual-2.2.15-fc11.i586
httpd-devel-2.2.15-fc11.i586
```

如果尚未安装，请安装 Apache。如果你获得了输出内容，说明你的 Apache 已经安装，可以继续进行配置。

在本节中，你将以默认配置作为配置 Apache 的起点。你将学习相关的 Apache 配置指令以及 Fedora 提供的默认配置。

当 Apache 启动时，主服务器会读取并处理 `/etc/httpd/conf/httpd.conf` 文件（Apache 配置文件）。Apache 还会读取 `/etc/mime` 来配置 MIME 系统，因为它将文件扩展名映射到内容类型。

在主服务器执行一些检查并打开日志文件后，它会启动配置文件中定义的一个或多个进程。这些子服务器负责监听独立进程或线程。这取决于主服务器的运行时配置行为以及它的编译方式。这些服务器响应 HTTP 端口（默认为 80）上的请求。

Apache 包含约 950 条指令。其中某些指令针对特定操作系统，某些提供向后兼容性，另一些则用于处理特定情况。Apache 文件 `/etc/httpd/conf/httpd.conf` 被组织为三个部分：描述 Apache 全局特征的指令、描述主服务器或默认服务器的指令以及关于虚拟主机的配置。

让我们学习全局行为。

### 配置全局行为

第一部分由控制整个 Apache 服务器（全局环境）的指令组成。以下是 `/etc/httpd/conf/httpd.conf` 中全局环境的指令：

```
### Section 1: Global Environment
ServerTokens 0
ServerRoot "/etc/httpd"
Pidfile run/httpd.pid
Timeout 120
KeepAlive off
MaxKeepRequests 100
KeepAliveTimeout 15
<IfModule prefork_module.c>
StartServers 8
MinSpareServers 5
```

| | |
|---|---|
| MaxSpareServers | 20 |
| ServerLimit | 256 |
| MaxClients | 256 |
| MaxRequestsPerChild | 4000 |
| </IfModule> | |
| <IfModule module_worker.c> | 2 |
| StartServers | |
| MaxClients | 150 |
| MinSpareThreads | 25 |
| MaxSpareThreads | 75 |
| ThreadsPerChild | 25 |
| MaxRequestsPerChild | 0 |
| </IfModule> | |
| Listen 80 |
| Include conf.d/*.conf |
