
[root@alpha ldap]# ls /var/lib/ldap/

accesslog cn.bdb __db.002 dn2id.bdb log.000000000 ou.bdb

alock __db.001 __db.003 id2entry.bdb Object.Class sn.bdb

```
我们可以看到一系列带有 `.bdb` 扩展的文件，这些是数据库文件，以及一个或多个事务文件（`log.0000000001`）。根据 OpenLDAP 官方手册，这些文件应该定期进行备份以备恢复。为了实现这一点，我们可以采取两种方法之一：

- 备份整个数据库，并同时定期备份事务日志文件。
- 使用 `slapcat` 生成 LDIF 文件。

如果我们选择第一种方案，可以使用 `db_hotbackup` 命令进行热备份。

```
[root@alpha ldap]# db_hotbackup -h /var/lib/ldap/ -b ../bdb_backup/

root@alpha ldap]# ls bdb_backup/

alock dn2id.bdb log.000000001 ou.bdb

cn.bdb id2entry.bdb objectClass sn.bdb
```

通过这种方式，我们将数据库文件以及事务日志复制到了新位置。如果需要，可以从那里进行恢复。恢复是通过 `db_recover` 工具执行的。

```
[root@alpha ldap]# db_recover -v -h /var/lib/ldap/

BDB2526 Finding valid LSN: file: 1 offset 3571

BDB1514 Recovery starting from Jun 15 10:33:38 2017

BDB1519 Maximum transaction ID 8000002 recovery checkpoint

[root@alpha ldap]#
```

如果我们决定使用第二种方案，我们应该生成一个 LDIF 文件，稍后用于恢复数据。

```
[root@alpha ldap]# slapcat -b "dc=linuxaholics,dc=com" > myOpenLDAP.ldif
```

但在这种情况下，如果数据库文件损坏，我们可能需要重新安装，并在 OpenLDAP 服务器重新运行后从 LDIF 文件中插入数据。到目前为止我们还没有见过的另一个非常有用的工具是 `db_verify`，用于验证数据库文件。

```
[root@alpha ldap]# db_verify -h /var/lib/ldap/

BDB5105 Verification of /var/lib/ldap/dn2id.bdb succeeded.

[root@alpha ldap]#
```

### 工具

我们有几个实用的工具可以查询和管理 LDAP 服务器。其中一些工具已经在本章中使用，另一些将在接下来的章节中使用。

### 服务器工具

这些工具包含在 OpenLDAP 服务器二进制执行文件中，并直接作用于 `slapd` 数据库。使用它们时应谨慎，因为它们很容易导致数据库损坏。这种情况可能会发生，因为……（此处原文不完整，翻译随之结束）

注，由于提供的文本在结尾处截断，上述内容已根据提供的片段进行了翻译。

（注：由于用户提供的待翻译文本在“Server Tools”部分之后截断，我仅针对提供的文本内容进行了翻译，未生成不存在的后续。）

# 第 2 章 保护目录

SSL 和 TLS 可用于加密通信。然而，由于 SSL 协议存在许多已知漏洞，建议使用其继任者 TLS 协议。

LDAP 以及许多其他协议（如超文本传输协议 (HTTP) 或简单邮件传输协议 (SMTP)）既可以通过安全方式（使用 TLS）也可以通过不安全方式通信，因此服务器和客户端需要商定是否建立安全连接。实现这一点的典型方法是为安全和不安全连接使用不同的端口号，但也可以对两者使用相同的端口。在这种情况下，当客户端想要建立 TLS 连接时，它会发送 STARTTLS 请求。

STARTTLS 是明文协议的一种扩展，允许使用与标准非加密版本协议相同的端口号对通信进行加密。为了这一目的，SMTP、FTP 和 LDAP 等许多协议使用了 STARTTLS。

TLS 依赖于使用 X.509 证书来承载服务器身份，因此我们需要服务器证书。此外，取决于我们如何配置系统，我们可能还需要客户端证书。我们将在本书的后后部分介绍一些示例。

我们对知名电子商务网站使用的证书熟悉，这些证书由受信任的证书颁发机构 (CA) 签名。在案例中，我们将创建自己的 CA 并签名自己的证书，以便与 LDAP 使用。要做到这一点，我们首先开始安装 openssl 包，除非它已经安装。

```
[root@alpha ~]# yum install openssl
```

## 准备环境

确保每个涉及的计算机都能相应地解析服务器名称是非常重要的。在我们的示例中，服务器名称为 alpha.linuxaholics.com，关联 IP 地址为 192.168.1.229。如果我们在基础设施中使用域名系统 (DNS) 服务器，我们应该添加相应的 A 记录和 PTR 记录。然而，如果在没有 DNS 服务器的实验室环境中工作，我们可以简单地为处理过程中的每台计算机编辑 `/etc/hosts` 文件。要编辑该文件，我们可以使用 Linux 中提供的许多编辑器之一，如 `vi`、`vim`、`nano` 等。文件的内容应该类似于所示：

```
[root@alpha ~]# cat /etc/hosts

127.0.0.1    localhost localhost.localdomain localhost4 localhost4.localdomain4

::1            localhost localhost.localdomain localhost6 localhost6.localdomain6

192.168.1.229    alpha.linuxolics
```

如果主机名或服务器的 IP 不同，我们应该相应地编辑该文件。可以使用 `hostnamectl` 命令轻松设置主机名，如下：

```
[root@alpha ~]# hostnamectl set-hostname alpha.linuxolics
```

### 创建 CA 和服务器证书

安装 `openssl` 包后，在 `/etc/pki/CA` 下我们应该有一个预定义的树形结构。

```
[root@alpha ~]# cd /etc/pki/CA/

[root@alpha CA]# ls -l

drwxr-xr-x. 2 root root 4096 abr 11 2018 certs

drwxr-xr-x. 2 root root 6 abr 11 2018 crl

drwxr-xr-x. 2 root root 45 abr 11 2018 newcerts

drwx------. 2 root root 4096 abr 11 2018 private
```

为了跟踪已颁发的证书，我们创建了 `index.txt` 和 `serial` 文件。在创建 `serial` 文件时，我们应该注意开头的零。

```
[root@alpha CA]# touch index.txt

[root@alpha CA]# echo 0001 > serial
```

现在我们为 CA 创建密钥。我们将为该密钥设置密码，否则将得到错误：

```
[root@alpha CA]# openssl genrsa -aes256 -out /etc/pki/CA/private/ca.pem

Generating RSA private key, 1024 bit long modulus

......................++++

++++++++
```
exponent is 65537 (0x10001)

Enter passphrase for /etc/pki/CA/private/ca.pem:
Verifying -Enter passphrase for /etc/pki/CA/private/ca.pem:
```

一旦我们有了密钥文件，就可以创建 CA 证书。

```
[root@alpha CA]# openssl req -new -x509 -days 365 -key /etc/pki/CA/private/ca.pem -extensions v3 ca -out /etc/pki/CA/certs/ca.pem
Enter passphrase for /etc/pki/CA/private/ca.pem:
```

你将被要求输入将整合到证书请求中的信息。你将输入所谓的区别别名称（Distinguished Name）。有几个字段可以留空。某些字段有一个默认值，如果你输入 '.'，该字段将留空。

Country Name (字母代码) [XX]:ES

State or Province (全名) []:Madrid
