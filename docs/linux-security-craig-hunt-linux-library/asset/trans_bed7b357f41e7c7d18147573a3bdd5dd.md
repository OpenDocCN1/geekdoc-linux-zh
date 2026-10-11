
例如，请考虑列表 13.12 中的命令序列。

## 列表 13.12 获取 Kerberos 票据以配合使用经过 Kerberos 改造的 telnet 客户端

```
[ramon]$ hostname
atlantis.hontanon.com
[ramon]$ kinit ramon@HONTANON.COM
Password for ramon@HONTANON.COM:
[ramon]$ klist
Ticket cache: FILE:/tmp/krb5cc_501
Default principal: ramon@HONTANON.COM

   Valid starting     Expires     Service principal
02/24/01 20:59:12    02/25/01 06:59:12    krbtgt/HONTANON.COM@HONTANON.COM

Kerberos 4 ticket cache: /tmp/tkt501
klist: You have no tickets cached
[ramon]$ telnet -x -a -k HONTANON.COM challenger
Trying 163.109.21.167...
Connected to challenger (163.109.21.167).
Escape character is '^]'.
Waiting for encryption to be negotiated...
[ Kerberos V5 accepts you as `ramon@HONTANON.COM' ]
done.
Last login: Sat Feb 24 20:58:07 from atlantis
You have mail.
[ramon]$ exit
logout
Connection closed by foreign host.
[ramon]$ klist
Ticket cache: FILE:/tmp/krb5cc_501
Default principal: ramon@HONTANON.COM

   Valid starting     Expires     Service principal
02/24/01 20:59:12    02/25/01 06:59:12    krbtgt/HONTANON.COM@HONTANON.COM
02/24/01 20:59:29    02/25/01 06:59:12    host/challenger@HONTANON.COM

Kerberos 4 ticket cache: /tmp/tkt501
klist: You have no tickets cached
```

该序列始于主机 `atlantis.hontanon.com`，此时用户 ramon 没有任何 Kerberos 票据。ramon 随后使用 `kinit` 命令请求主体 ramon@HONTANON.COM 的 TGT。接着，ramon 使用经过 Kerberos 改造的 `telnet` 客户端登录到机器 `challenger.hontanon.com`。由于 ramon 在 `telnet` 命令中包含了 `-x` 选项，因此建立了一个加密连接。

在退出 `challenger` 会话后，用户 ramon 现在拥有额外的 Kerberos 票据：

02/24/01 20:59:29 02/25/01 06:59:12 host/challenger@HONTANON.COM

这是本地主机（atlantis）向 KDC 请求的票据，用于获取对 `challenger` 的 `telnet` 访问权限。请注意，你可以使用该票据访问 `challenger`，直到 2001 年 2 月 25 日上午 6:59。在那时，当你尝试执行 `telnet` 操作时，系统将要求你再次运行 `kinit`（以获取新票据）。

### ftp

与 `telnet` 命令类似，经过 Kerberos 改造的 `ftp` 客户端有两个与其标准 Linux 版本不同的命令行选项。它们列在表 13.7 中。

**表 13.7** Kerberos ftp 客户端命令行选项

| 选项 | 含义 |
| :--- | :--- |
| -k *realm* | 请求 `/etc/krb5.conf` 文件中 `default_realm` 变量未指定的其他领域的票据。 |
| -x | 启用加密。 |

就像普通的 `ftp` 客户端一样，文件 `.netrc` 用于自动化连接建立过程：

```
[ramon]$ cat .netrc
machine ftp.uu.net login anonymous password rhontanon@sybex.com
machine ftp.netscape.com login anonymous password rhontanon@aol.com
default login ramon
```

前述示例中 `.netrc` 文件的前两行定义了特定远程 FTP 服务器的默认用户名/密码。此示例中的最后一行定义了用于所有其他主机的默认用户名。请查看列表 13.13 中涉及经过 Kerberos 改造的 ftp 客户端的典型命令序列。

## 列表 13.13 获取 Kerberos 票据以配合使用经过 Kerberos 改造的 ftp 客户端

```
[ramon]$ hostname  
atlantis.hontanon.com
[ramon]$ kinit ramon@HONTANON.COM
Password for ramon@HONTANON.COM:  
[ramon]$ klist  
Ticket cache: FILE:/tmp/krb5cc_501
Default principal: ramon@HONTANON.COM

	Valid starting		Expires		Service principal
02/24/01 21:20:59	02/25/01 07:20:59	krbtgt/HONTANON.COM@HONTANON.COM

Kerberos 4 ticket cache: /tmp/tkt501
klist: You have no tickets cached
[ramon]$ ftp -x challenger
Connected to challenger.
220 challenger.hontanon.com FTP server (Version 5.60) ready.
334 Using authentication type GSSAPI; ADAT must follow
GSSAPI accepted as authentication type
GSSAPI authentication succeeded
200 Data channel protection level set to private.
232 GSSAPI user ramon@HONTANON.COM is authorized as ramon
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> pwd
257 "/home/ramon" is current directory.
ftp> bye
221 Goodbye.
[ramon]$ klist  
Ticket cache: FILE:/tmp/krb5cc_501
Default principal: ramon@HONTANON.COM

	Valid starting		Expires		Service principal
02/24/01 21:20:59	02/25/01 07:20:59	krbtgt/HONTANON.COM@HONTANON.COM
02/24/01 21:21:10	02/25/01 07:20:59	ftp/challenger@HONTANON.COM

Kerberos 4 ticket cache: /tmp/tkt501
klist: You have no tickets cached
```

与 telnet 示例一样，ftp 会话是加密的。此外，请注意，在退出会话并查看你的 Kerberos 凭据后，你现在拥有以下形式的票据：

```
02/24/01 21:21:10  02/25/01 07:20:59  ftp/challenger@HONTANON.COM
```

这是 atlantis 向 KDC 请求以访问 challenger 的 FTP 服务的票据。

## login, rsh, and rcp

表 13.8 列出了经过 Kerberos 改造的 login、rsh 和 rcp 客户端中的 Kerberos 特定命令行选项。

**表 13.8** Kerberos login, rsh, and rcp 客户端命令行选项

| **选项** | **含义** |
|---|---|
| `-k realm` | 请求 `/etc/krb5.conf` 文件中 `default_realm` 变量未指定的其他领域的票据。 |
| `-x` | 启用加密。 |

通过一个示例可以最好地说明这三类客户端的用法。让我们首先建立到主机名称 challenger 的加密 rlogin 会话，如列表 13.14 所示。

## 列表 13.14 获取 Kerberos 票据以配合使用经过 Kerberos 改造（且加密）的 rlogin 客户端

```
[ramon]$ hostname
atlantis.hontanon.com
[ramon]$ kinit ramon@HONTANON.COM
Password for ramon@HONTANON.COM:
[ramon]$ klist
Ticket cache: FILE:/tmp/krb5cc_501
Default principal: ramon@HONTANON.COM

   Valid starting     Expires     Service principal
02/24/01 21:29:54   02/25/01 07:29:54 krbtgt/HONTANON.COM@HONTANON.COM

Kerberos 4 ticket cache: /tmp/tkt501
klist: You have no tickets cached
[ramon]$ rlogin -x challenger
This rlogin session is using DES encryption for all data transmissions.
Last Login: Sat Feb 24 21:29:33 from atlantis.hontanon.com
You have mail.
[ramon]$ exit
logout
Connection closed.
[ramon]$ klist
Ticket cache: FILE:/tmp/krb5cc_501
Default principal: ramon@HONTANON.COM

   Valid starting     Expires     Service principal
02/24/01 21:29:54  02/25/01 07:29:54 krbtgt/HONTANON.COM@HONTANON.COM
02/24/01 21:30:06  02/25/01 07:29:54 host/challenger@HONTANON.COM

Kerberos 4 ticket cache: /tmp/tkt501
klist: You have no tickets cached
```

重要的是要注意，rlogin、rsh 和 rcp 应用程序使用与 telnet 相同类型的主机/主机名称票据：

```
02/24/01 21:30:06  02/25/01 07:29:54 host/challenger@HONTANON.COM
```

接下来，你使用经过 Kerberos 改造的 rsh 应用程序，通过 Kerberos 认证从远程主机获取文件列表（参见列表 13.15）。

## 列表 13.15 使用 Kerberos 认证从远程主机获取文件列表

```
[ramon]$ rsh -x challenger.hontanon.com ls -l /usr/local/etc/*-gw
This rsh session is using DES encryption for all data transmissions.
-rwxr-xr-x 1 root root 1954587 Jan 30 21:22 /usr/local/etc/ftp-gw
-rwxr-xr-x 1 root root 2073268 Jan 30 21:22 /usr/local/etc/http-gw
-rwxr-xr-x 1 root root 1866661 Jan 30 21:22 /usr/local/etc/plug-gw
-rwxr-xr-x 1 root root 1912963 Jan 30 21:22 /usr/local/etc/ftpd-rlogin-gw
```

最后，你使用随发行版提供的经过 Kerberos 改造的 rcp 客户端从远程主机复制多个文件。在下例中，第一个命令在加密通道中复制文件，而第二个命令发出远程 shell 请求（同样加密）以验证文件是否已成功传输（参见列表 13.16）。

## 列表 13.16 使用经过 Kerberos 改造的 rcp 客户端从远程主机复制文件

```
[ramon]$ rcp -x file* ramon@challenger.hontanon.com:/tmp/
[ramon]$ rsh challenger.hontanon.com ls -l /tmp/file*
-rw-r--r--    1 ramon    users      4522 Feb 24 21:37 /tmp/file1
-rw-r--r--    1 ramon    users      4522 Feb 24 21:37 /tmp/file2
-rw-r--r--    1 ramon    users      4522 Feb 24 21:37 /tmp/file3
```

这结束了关于 Kerberos 认证系统的讨论。下一节将介绍用于一次性密码的 S/Key 和 OPIE 系统。

## S/Key 和 OPIE

使用传统认证的主要缺点之一是，如果攻击者获得了密码，他们就能冒充该用户。但如果密码每次都不同呢？*一次性密码*的概念激发了 Bellcore 工程师设计 S/Key 系统。通过使用由小秘密密钥（例如密码）引导的哈希算法，S/Key 系统允许你使用预定义的密码序列登录到 Linux 服务器，每个密码仅使用一次。

该方案的成功取决于这样一个事实：如果知道了当前密码，预测下一个密码极其困难。这是通过一个强大的哈希函数（基于 MD4 算法）实现的，该函数使用密码作为种子值。然后生成一组八字节密码序列并将其转换为六个英文单词。每次用户想要登录服务器时，必须使用此六词序列作为密码。

服务器首先期望序列中的最后一个密码，然后期望其余的密码按相反顺序排列。这意味着，如果攻击者获得了当前密码，他们必须猜测序列中的前一个密码，这意味着要逆转哈希函数。鉴于 MD4 算法的强大性，这是极其困难的。

1994 年，美国海军研究实验室（NRL）接受了 S/Key 概念，并使用更强的 MD5 哈希算法重新实现了它。所谓的 OPIE 系统

