

# 如果未启用服务，禁用 inetd 或 xinetd

如果 inetd 或 xinetd 服务已被禁用，则没有必要让 inetd 或 xinetd 继续运行。要防止 inetd 或 xinetd 在启动时执行，请禁用 /etc/rc.d 和 /etc/rc.local 中的相应文件。

# 确保开启日志记录

如果正在运行 inetd，请编辑 inetsvc 文件并确保调用 inetd 时带有 -t 标志。对于 xinetd，请编辑 xinetd.conf 并确保存在以下行：

```
log_type = SYSLOG authpriv
```

此外，编辑 syslog.conf 并确保启用了 *.info 以将日志记录到 /var/log/messages 中。

# 加固远程服务

本节提供了针对 Unix 和 Linux 主机上某些常用远程服务的加固建议。

使用 netstat 查找在 TCP 和 UDP 端口上监听的进程：

```
[bash]# netstat -nap
Proto Local Address Foreign Address State PID/name
tcp 0 0.0.0.0:139 0.0.0.0:* LISTEN 1251/smbd
tcp 0 0.0.0.0:80 0.0.0.0:* LISTEN 11228/X
tcp 0 0.0.0.0 0.0.0.0:* LISTEN 2047/httpd
tcp 0 0.0.0.0:113 0.0.0.0:* LISTEN 728/identd
tcp 0 0.0.0.0:22 0.0.0.0:* LISTEN 750/sshd
udp 0 0.0.0.0:512 0.0.0.0:* LISTEN 14059/xinetd
...]
```

# WU-FTPD

FTP（文件传输协议）是一种用于从一个主机传输文件到另一个机的协议。WU-FTPD 是 Unix 和 Linux 上最广泛使用的 FTP 守护进程。可以在 http://www.wu-ftpd.org/ 获取。采取以下步骤加固 WU-FTPD：

- 修改服务器横幅（banner）。编辑 /etc/ftpaccess 并使用 greeting 指令指定新的服务器信息。例如：
`greeting text No banner information available. Sorry.`

- 确保 /etc/ftpusers 包含一个不允许进行 FTP 登录的用户列表。root、bin 和 http 等用户不应允许 FTP 登录。

- 编辑 inetd.conf 或 /etc/xinetd.d/ftpd，并确保调用 in.ftpd 时带有 -l 标志。这将启用日志记录。

- 如果允许匿名上传，则上传的文件必须是不可见的，并且应该禁止下载上传的文件。否则，你的 FTP 服务器可能会被软件盗贼滥用。详情请参阅 http://www.wu-ftpd.org/HOWTO/upload.configuration.HOWTO。

- 使用 ch狱（chrooted）FTP 环境，特别是针对匿名访问。请参阅 http://www.wu-ftpd.org/HOWTO/HOWTO 获取有关如何设置的详细说明。

考虑将 ProFTPD 作为 WU-FTPD 的替代品，因为它已被证明没有像 WU-FTPD 那样容易受到许多远程漏洞的影响。ProFTPD 可 http://www.proftpd.org 获取。

# SSH

SSH 是一种用于交换数据的安全协议。它可以用于登录远程机器、远程执行命令以及传输文件。由于与 SSH 的通信是加密的，因此它是 telnet、login 和 FTP 等远程登录解决方案的理想替代品。采取以下措施加固 SSH：

- 确保禁用 SSH 协议版本 1。sshd_config 文件必须包含以下行：
`Protocol 2`

- 不应允许 root 用户通过 SSH 登录。确保 sshd_config 中存在以下行：
`PermitRootLogin no`

- 如 ssh_host_key、ssh_host_rsa_key 和 ssh_host_rsa_key 等私钥文件应仅允许 root 用户读取。

- 确保已开启特权分用（Privilege Separation）。sshd_config 中必须存在以下行：
`UsePrivilegeSeparation yes`

# Sendmail

Sendmail 是互联网上最流行的 MTA（邮件传输代理）。要加固 Sendmail，请确保采取以下措施：

更改 SMTP 欢迎消息。编辑 sendmail.cf 文件并更改 SmtGreetingMessage 的值以反映新的横幅（banner）。或者，你可以编辑 sendmail.mc 并将 confSMTP_LOGIN_MSG 的值更改为新的欢迎语。

EXPN 和 VRFY 是 SMTP 协议支持的用于用户名枚举的两个命令。你应该通过编辑 sendmail.cf 来关闭它们，并确保 PrivacyOptions 设置为 authwarnings, noexpn, novrfy, restrictqun。或者，你可以编辑 sendmail.mc 文件并确保存在以下行：

`define('CONFPRIVACY_FLAGS', 'authwarnings, noexpn, novrfy, restrictqun')dnl`

还可以设置其他标记，如 goaway、restrictmail、restrictqun 和 nobodyturn。详情请参考 Sendmail 文档。

使用 smush 作为 MDA（邮件投递代理），它是一个 sh sh 程序；它限制了可以使用 Sendmail 的 "command" 语法运行的命令。要启用 smush，请确保以下内容：

| 文件或目录 | 用户 | 权限 |
| :--- | :--- | :--- |
| /etc/aliases | root | -rw-- |
| /etc/mail | root | drwxr-xr-x |
| /var/mail | root | drwxr-xr-x |
| /var/spool/mail | root | drwxr-xr-x |

检查 sendmail.mc 中 MaxSize 的值：
`define('MaxSize', '1048576')`

众所周知 Sendmail 易受到漏洞影响。考虑使用 qmail 作为

这将生成 sendmail.cf：
```
m4 sendmail.mc > sendmail.cf
```

# BIND

DNS（域名系统系统）是一种用于解析域名和 IP 地址的协议。BIND（Berkeley Internet Name）是互联网上使用广泛的 DNS。采取以下措施加固 BIND：

- 编辑 BIND 配置 named.conf 并覆盖版本：
`version "Not available"`

- 限制区域传输。使用 allow-transfer 指令指定主机：
`options { allow-transfer { ip_address }; };`

- 关闭递归查询。这将防止你的 DNS 服务器受到欺骗攻击：
`options { recursion no; };`

- 在 ch狱（chrooted）环境中运行 BIND。详情请参阅 http://www.homeport.org/~adam/dns.html。

- 限制动态更新，因为该功能允许远程实体删除和添加记录。默认情况下，BIND 不允许动态更新。只有使用 allow-update 语句才能启用。

# Apache (HTTP 和 HTTPS)

考虑使用 djbdns 作为 BIND 的替代品。djbdns 服务器可以在 http://cr.to/djbdns.html 获取。

Apache 是目前最流行的 Web 服务器。可以采取以下步骤加固服务器配置：

- 修改你的 HTTP 横幅。编辑 httpd.conf 并确保以下指令为：
`ServerSignature Off`
`ServerTokens Prod`

如果你不想在 Server 标签中显示 "Apache"，但想显示虚假信息如 "Server: Not-allowed"），你需要：

1. 下载 Apache 源码。
2. 编辑 httpd.h 文件，并将行 `#define SERVER_BASEPRODUCT "Apache"` 中的字符串值更改为其他：
`#define SERVER_BASEPRODUCT "Not-allowed"`
3. 重新编译、安装并重启 Apache。

- 关闭自动索引。这将指示 Apache 在没有默认索引文件（如 index.html）时不提供目录列表。在 httpd.conf 中使用 IndexIgnore 指令来实现此点。

- 配置 Apache 不提供 .htaccess,.htpasswd,.inc,.jsp,.java 或 .php 等敏感文件。例如，在 httpd.conf 中使用以下指令限制 Apache 提供以 .ht 开头的文件：

```
<Files
  "\*.ht"
  Order allow, deny
  Deny from all
</Files>
```

- 移除默认帮助页。
- 移除默认和示例 CGI 脚本及应用程序。

