
#### 实验练习

编辑 `hosts.allow`、`hosts.deny` 和 `hosts.lpd` 文件，允许或拒绝下列表主机访问相应服务。完成此任务的相应行在练习下方。

#### hosts.allow

允许 `lucasgames.com` 网络上的所有主机访问 FTP。

```
ftpd: .lucasgames.com
```

允许 `lucaslearning.com` 网络上的所有主机（64.41.207.50 外）访问 Telnet。

```
telnetd: .lucaslearning.com EXCEPT 64.41.207.50
```

允许本地网络上的所有主机。

```
ALL: LOCAL
```

#### hosts.deny

拒绝 `lucasgames.com` 网络上的所有主机访问 Telnet。

```
telnetd: .lucasgames.com
```

拒绝 `lucaslearning.com` 网络上的所有主机（64.41.207.50 外）访问 FTP。

```
ftpd: .lucaslearning.com EXCEPT 64.41.207.50
```

拒绝所有主机访问所有服务。

```
ALL: ALL
```

#### hosts.lpd

允许 `lucasgames.com` 网络上的所有主机打印。

```
+.lucasgames.com
```

拒绝 `lucaslearning.com` 网络上的所有主机打印。

```
-.lucaslearning.com
```

# Rootkits 与 Rootkit 检测器 339

## 安装 ROOTKIT 之前

```
Checking 'chfn...' Not vulnerable
Checking 'chsh...' Not vulnerable
Checking 'cron...' Not vulnerable
Checking 'sshd...' Not vulnerable
Checking 'du...' Not vulnerable
Checking 'find...' Not vulnerable
Checking 'fingerd...' Not vulnerable
Checking 'su...' Not vulnerable
Checking 'ifconfig...' Not vulnerable
Checking 'inetd...' Not vulnerable
Checking 'killall...' Not vulnerable
Checking 'login...' Not vulnerable
Checking 'ls...' Not vulnerable
Checking 'netstat...' Not vulnerable
Checking 'passwd...' Not vulnerable
Checking 'pidof...' Not vulnerable
Checking 'ps...' Not vulnerable
Checking 'rshd...' Not vulnerable
Checking 'syslogd...' Not vulnerable
Checking 'tcpd...' Not vulnerable
Checking 'top...' Not vulnerable
Checking 'telnet...' Not vulnerable
Checking 'bindshell...' Not vulnerable
'z2...' Checking 'wted...' Nothing deleted
Checking 'sniffer'...
```

```
eth0 PROMISC
Checking 'aliens...' No suspect files
```

正在搜索嗅探器日志，可能需要一些时间... 未发现任何内容

Chrootkit 在对系统进行彻底检查后未发现任何错误。

现在，检查安装 rootkit后的输出。

## 安装 ROOTKIT 之后

```
Checking 'chfn...' Not vulnerable
Checking 'chsh...' Not vulnerable
Checking 'cron...' Not vulnerable
Checking 'sshd...' Not vulnerable
Checking 'du...' Not vulnerable
Checking 'find...' Not vulnerable
Checking 'fingerd...' Not vulnerable
Checking 'su...' Not vulnerable
Checking 'ifconfig...' INFECTED
Checking 'inetd...' Not vulnerable
Checking 'killall...' Not vulnerable
Checking 'login...' INFECTED
Checking 'ls...' Not vulnerable
```

```
Checking 'netstat'... Not vulnerable
Checking 'passwdw'... Not vulnerable
Checking 'pidof'... Not vulnerable
Checking 'ps'... Not vulnerable
Checking 'radhi'... Not vulnerable
Checking 'sylogd'... Not vulnerable
Checking 'tcpd'... Not vulnerable
Checking 'top'... Not vulnerable
Checking 'telnet'... Not vulnerable
Checking 'bindshell'... Not vulnerable
Checking 'z2'... Checking 'wted'... Nothing deleted
Checking 'sniffer'...
eth0 is PROMISC
Checking 'aliens'... No suspect files
正在搜索嗅探器日志，可能需要一些时间... 未发现任何内容
正在搜索 't0rn' 的默认文件和目录... 可能安装了 t0rn rootkit
Checking '1km'... 你在 ps 命令中隐藏了1 个进程
警告：可能安装了 LKM 木马
```

现在，存在几个漏洞，例如 `ifconfig` 和 `login`。这是一个问题，因为 `login` 漏洞会让黑客获得对系统的访问权限。

## 结论

虽然 rootkit 检测器无法确保完全的安全，但它们允许对 root 密码的完整性进行定期检查。新的 rootkit 发布频繁，拥有最新版本至关重要。

## 问题

+ 1. 什么是 rootkits？它们为什么会对系统安全构造成威胁？

2. 为什么拥有最新的 rootkit 检测器很重要？

3. 什么是被木马化的命令？

## 答案

+ 1. Rootkits 是黑客用来替换现有系统命令为修改后版本的程序。这些命令帮助黑客规避检测并随时重新进入系统。

+ 2. 拥有最新的检测器是重要的，因为黑客在不断改进和更改 rootkits。

+ 3. 木马化的命令是 rootkits 插入以替换现有系统命令的命令，帮助它们规避检测。

## 高级问题

+ 1. 在安装 rootkit 后如何使系统恢复过程自动化？

# 部分

第三部分

# 练习题与答案

## 练习题

### 第 1 章：操作原理

+ 1. PGP 是一个可以用于创建、加密和发送电子邮件的程序。

A. 正确

B. 错误

+ 2. PGP 是利用以下哪项的加密程序？（选择所有适用项）

A. 私钥加密

B. RSA 加密算法

C. 公钥加密

D. 以上所有项

E. 以上都不是

+ 3. DES 是一种安全的加密算法。

A. 正确

B. 错误

+ 4. 公钥加密：

+ A. 仅为加密和解密创建一个密钥。

+ B. 总是依赖于一次性密文。

+ C. 必须使用 RSA。

+ D. 是 DES 加密的一部分。

+ E. 使用公钥和私钥对数据进行加密和解密。

+ 5. 使用公钥加密发送消息需要什么？

+ A. 接收者和发送者的密钥都不需要

+ B. 接收者和发送者的密钥

+ C. 发送者的密钥

+ D. 接收者的密钥

+ E. 一个双方共享的私钥

+ 6. 系统管理员想为用户账户和密码实现最高级别的安全。哪些操作将极大地保护系统的完整性？（选择所有适用项）：

+ A. 实施影子密码（shadow passwords）在本地保护密码。

+ B. 要求根据过期策略定期更改密码。

+ C. 通过电子邮件发送管理员分配密码。

+ D. 要求所有用户在连接服务器时使用 `ssh` 而非 Telnet。

+ E. 强制用户使用超过 7 位的字母数字密码。

+ F. 以上所有项都是有效的。

+ 7. 默认情况下，shadow 套件会将普通密码文件替换为：

+ A. `/etc/passwd`

+ B. `/etc/shadow`
