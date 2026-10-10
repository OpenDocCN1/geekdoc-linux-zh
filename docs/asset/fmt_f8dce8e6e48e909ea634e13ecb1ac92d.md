
有时，如果文件或目录是本地存在的，或者看起来是本地存在的，工作起来会更容易。例如，也许你有一个本地应用程序，它在你用于操作文件的服务器上不存在。你不需要从服务器下载文件，修改它，然后再将其上传回服务器，而是可以将远程目录挂载到本地工作站上。以下是通过`SSH`更新网站的示例。

```
$ mkdir web-files
$ sshfs www.example.com:/home/jason/public_html web-files
$ bluefish web-files/index.html
$ fusermount -u web-files
```

就像`ssh`命令一样，如果你的远程用户名与本地用户名不同，你可以使用`user@host`格式。此外，如果冒号后未指定目录，则默认使用你的主目录。

## 使用`Curl`从命令行获取你的公网`IP`

```bash
$ curl ifconfig.me
```

如果你需要确定你的公网（互联网）`IP`地址，可以使用`ifconfig.me`网站。

```bash
$ curl ifconfig.me
198.145.20.140
$ curl ifconfig.me/ip
198.145.20.140
$ curl ifconfig.me/host
pub2.kernel.org
```

## 无密码`SSH`登录远程系统

```bash
$ ssh-keygen
$ ssh-copy-id remote-host
$ ssh remote-host
```

为了无需密码即可`SSH`登录到远程主机，你需要一对`SSH`密钥，包含私钥和公钥。在远程主机上，公钥的内容需要位于`~/.ssh/authorized_keys`文件中。`ssh-copy-id`脚本会执行这项工作。

如果你想要生成一个没有密码的密钥，只需在提示输入口令（passphrase）时直接按回车即可。你也可以选择向`-N`选项提供一个空字符串（`ssh-keygen -N ""`）。

```bash
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/jason/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/jason/.ssh/id_rsa.
Your public key has been saved in /home/jason/.ssh/id_rsa.pub.
The key fingerprint is:
0d:2e:e4:32:dd:da:60:a5:2e:0f:c5:89:d5:78:30:ad
jason@laptop.localhost
The key's randomart image is:
+--[ RSA 2048]----+
|          O.      |
|          =.      |
|        +. =      |
|        BEB  O    |
|        + @ S .   |
|          \* =    |
|        o o .     |
|        +         |
|            .     |
+-----------------+
$ ssh-copy-id linuxserver
jason@192.168.122.60's password:
Now try logging into the machine, with "ssh 'linuxserver'", and check in:
    .ssh/authorized_keys
to make sure we haven't added extra keys that you weren't expecting.
```

```bash
$ ssh linuxserver
$ hostname
linuxserver
$
```

## 显示打开的网络连接

```bash
$ sudo lsof -Pni
```

`lsof`命令不仅可以用于显示打开的文件，还可以显示打开的网络端口和网络连接。`-P`选项可防止将端口号转换为端口名称。`-n`选项可防止将`IP`地址转换为主机名。`-i`选项指示`lsof`显示网络连接。

```bash
$ sudo lsof -Pni
COMMAND          PID USER   FD TYPE DEVICE SIZE/OFF NODE NAME
dhclient      989 root   6u  IPv4  11522  0t0  UDP *:68
sshd          1202 root   3u  IPv4  12418  0t0  TCP *:22 (LISTEN)
sshd          1202 root   4u  IPv6  12423  0t0  TCP *:22 (LISTEN)
ntpd          1210 ntp  16u  IPv4  12464  0t0  UDP *:123
ntpd          1210 ntp  17u  IPv6  12465  0t0  UDP *:123
ntpd          1210 ntp  18u  IPv4  12476  0t0  UDP 127.0.0.1:123
ntpd          1210 ntp  19u  IPv4  12477  0t0  UDP 192.168.122.60:123
ntpd            1210  ntp   20u  IPv6  12478  0t0  UDP  [::]:123
ntpd            1210  ntp   21u  IPv6  12479  0t0  UDP  [fe80::5054:ff:fe52:d858]:123
master           1364  root   12u  IPv4  12761  0t0  TCP  127.0.0.1:25 (LISTEN)
clock-app  12174 jason   21u  IPv4  78889         0t0  TCP  192.168.122.60:39021->184.25.102.40:80 (ESTABLISHED)
sshd             12339  root     3r  IPv4  74023  0t0  TCP  192.168.122.60:22->192.168.122.1:34483 (ESTABLISHED)
sshd             12342 jason     3u  IPv4  74023  0t0  TCP  192.168.122.60:22->192.168.122.1:34483 (ESTABLISHED)
```

## 比较远程文件和本地文件的差异

```bash
$ ssh remote-host cat /path/to/remote-file | diff /path/to/local-file -
```

要显示本地文件和远程文件之间的差异，可以通过`SSH`使用`cat`命令查看文件，并将输出管道传入`diff`或`sdiff`命令。`diff`和`sdiff`命令可以通过在其中一个文件名处提供减号（`-`）来接受标准输入代替文件。

```bash
$ ssh linuxsrv cat /etc/passwd | diff /etc/passwd -
32c32
< terry:x:503:1000::/home/terry:/bin/ksh
---
> terry:x:503:1000::/home/terry:/bin/bash
35a36
> bob:x:1000:1000:Bob Smith:/home/bob:/bin/bash
```

## 从命令行发送电子邮件

```bash
$ mail recipient@domain.com
$ echo 'message' | mail -s 'subject' recipient@domain.com
```

使用`mail`命令可以发送电子邮件。你可以交互式地输入消息，或者通过管道输入。交互消息以`ctrl-d`结束。

```bash
$ mail jim@mycorp.com
Subject: Message from the command line
Isn't this great?
EOT
$ echo "Here's the lazy way" | mail -s 'Message from the command line' jim@mycorp.com
```

## 从命令行发送电子邮件附件

```bash
$ mail -a /path/to/attachment recipient@domain.com
$ echo 'message' | mail -s 'subject' -a /path/to/attachment recipient@domain.com
```

如果你需要从命令行发送电子邮件附件，请使用`mail`命令的`-a`选项。

```bash
$ echo "Here is the file you requested" | mail -s "The file" -a /tmp/files.tgz jim@mycorp.com
```

## 创建`SSH`隧道以访问远程资源

```bash
$ ssh -N -L local-port:host:remote-port remote-host
```

要创建`SSH`隧道，请使用`-L`选项。第一个端口是将在你的本地机器上打开的端口。到该端口的连接将通过`remote-host`进行隧道传输，并发送到`-L`选项中指定的主机和远程端口。`-N`选项告诉`SSH`不要在远程主机上执行命令（例如你的`shell`）。

假设你想访问一个在互联网上不可用，但你拥有`SSH`访问权限的服务器可以访问的网站。你可以创建一个隧道，让你可以浏览该网站，就像你位于公司防火墙后面一样。此命令会将你本地机器端口`8000`上的任何连接通过跳板服务器转发到内网服务器端口`80`。将你的`web`浏览器指向`http://localhost:8000`并开始浏览。

```bash
$ ssh -N -L 8000:intranet.acme.com:80 jump-server &
[1] 23253
$ firefox http://localhost:8000
```

另一个用例是访问运行在你拥有`SSH`访问权限的服务器上的服务。如果你需要访问一个仅允许来自特定主机的数据库连接的`mysql`服务器，你可以为连接创建一个`SSH`隧道。由于`mysql`服务运行在远程主机的`localhost:3306`上，`-L`选项应该如下所示：`-L 3306:localhost:3306`。你可以使用本地机器上的`mysql`命令行客户端连接到数据库，但更有趣的是使用图形化桌面应用程序（这些应用程序在服务器上不可用）。例如，你可以使用此隧道并通过`MySQL Workbench`、`Navicat`或其他应用程序连接到数据库。

```bash
$ ssh -N -L 3306:localhost:3306 db01 &
[1] 13455
$ mysql -h 127.0.0.1
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 5.1.73 Source distribution
Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.
Oracle is a registered trademark of Oracle Corporation and/or its affiliates. Other names may be trademarks of their respective owners.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
mysql>
```

## 查找哪些程序正在监听哪些端口

```bash
$ sudo netstat -nutlp
```

以下是`netstat`选项的说明，用于获取正在监听的程序及其端口的列表。

- `-n` 显示数字地址而不是解析符号名称

- `-u` 包含`UDP`协议

- `-t` 包含`TCP`协议

- `-l` 仅显示监听套接字

- `-p` 显示`PID`和程序名称

```bash
$ sudo netstat -nutlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State PID/Program name
tcp   0      0      0.0.0.0:3306          0.0.0.0:*               LISTEN 4546/mysqld
tcp   0      0      0.0.0.0:22            0.0.0.0:*               LISTEN 1161/sshd
tcp   0      0      127.0.0.1:25          0.0.0.0:*               LISTEN 1325/master
tcp   0      0      :::80                 :::*                    LISTEN 4576/httpd
tcp   0      0      :::22                 :::*                    LISTEN 1161/sshd
udp   0      0      0.0.0.0:68            0.0.0.0:*                        1008/dhclient
```

## 为特定远程主机使用不同的`SSH`密钥

将以下内容放入`~/.ssh/config`文件中。

```bash
Host remote-host
    IdentityFile ~/.ssh/id_rsa-remote-host
```

如果你需要或希望为不同的主机使用不同的`SSH`密钥，你可以使用`ssh`的`-i`选项在命令行中显式指定它们。

```bash
$ ssh -i ~/.ssh/id_rsa-db1 db1.example.com
```

如果你不想每次都要指定密钥，可以在`~/.ssh/config`文件中创建一个条目并在那里指定密钥。

```bash
$ cat ~/.ssh/config
```

### 特定主机配置

```bash
Host db1.example.com
IdentityFile ~/.ssh/id_rsa-db1

$ ssh db1.example.com
```

您可以在主机规格说明中使用通配符。

```bash
$ cat ~/.ssh/config
Host db*
IdentityFile ~/.ssh/id_rsa-db1
Host *.work.net
IdentityFile ~/work-files/keys/id_rsa
$ ssh jim@jumboj.work.net
```

如果您的`SSH`密钥以相关主机的完全限定域名命名，您可以使用`%`转义字符来简化您的`~/.ssh/config`文件。无需为每台服务器都创建一个主机条目，`%`语法会扩展为您所连接主机的完全限定域名。

```bash
$ cat ~/.ssh/config
Host *.example.com
IdentityFile ~/.ssh/id_rsa-%h
$ ls -1 ~/.ssh/id_rsa-*
id_rsa-lax-db-01.example.com
id_rsa-lax-db-01.example.com.pub
id_rsa-lax-web-01.example.com
id_rsa-lax-web-01.example.com.pub
$ ssh lax-db-01.example.com
```

## 避免在通过`SSH`连接时输入用户名

将以下内容放入`~/.ssh/config`文件中。

```bash
Host remote-host
  User username
```

如果您在本地`Linux`机器上的用户名与远程`Linux`机器上的用户名不同，您在通过`SSH`连接时必须指定它。它看起来像这样。

```bash
$ ssh jim@server1.example.com
```

为了避免每次都要输入`username@`，请在您的`~/.ssh/config`文件中添加一个主机条目。

```bash
Host server1.example.com
  User jim
```

一旦您配置了该主机条目，您就可以简单地`ssh`到远程主机。

```bash
$ whoami
james
$ ssh server1.example.com
$ whoami
jim
$
```

## 简化多跳`SSH`连接并透明地代理`SSH`连接

将以下内容放入`~/.ssh/config`文件中。

```bash
Host jump-host.example.com
ProxyCommand none
Host *.example.com
ProxyCommand ssh -W %h:%p jump-host.example.com
```
