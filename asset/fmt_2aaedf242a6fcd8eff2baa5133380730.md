
我们指定了 LDAP 服务器的地址以及执行查询的 LDAP 账户和该账户关联密码。一旦完成所有更改，我们就重启 LDAP 和 `saslauthd` 服务。

我们可以通过 `testsaslauthd` 命令检查 SASL 认证是否正常工作。

```
[root@alpha ~]# testsaslauthd -u Tux -p /run/saslauthd/mux

: NO "authentication failed"
```

我们可以看到认证失败了，因此我们将包含一个额外的参数来指定基搜索。

```
[root@alpha ~]# cat /etc/saslauthd.conf

ldap_servers: ldap://127.0.0.1

ldap_search_base: ou=users,dc=linuxaholics,dc=com

ldap_bind_dn: cn=Tux,ou=users,dc=linuxaholics,dc=com

ldap_password: linuxrules
```

## 第 2 章 安全目录

重启 `saslauthd` 服务后，如果重复测试，这次的结果将是成功的。

```
[root@alpha ~]# testsaslauthd -u Tux -f /run/saslauthd/mux: OK
```

### SASL 代理授权

SASL 有一个名为“代理授权”（proxy authorization）的很棒的功能，它允许已认证的用户代表另一个用户执行操作。这在很多情况下非常有用。例如，如果一组用户需要对某些资源具有相同的访问权限，我们可以向单个账户授予权限，并允许所有需要这些权限的用户代表该账户进行操作。这可以使用 SASL 代理来实现。

假设我们在 LDAP 服务器中定义了用户 `cn=WebApp,ou=apps,dc=linuxaholics,dc=com`。如果我们还没有创建它，现在可以创建它。

```
[root@alpha ~]# cat apps.ldap

dn: ou=apps,dc=linuxaholics,dc=com

objectClass: organizationalUnit
```
```
[root@alpha ~]# ldapadd -x -H ldapi:/// -b "ou=apps,dc=linuxaholics,dc=com" <<EOF
dn: cn=WebApp,ou=apps,dc=linuxaholics,dc=com
objectClass: inetOrgPerson
cn: WebApp
EOF
```

然而，在执行 `ldapsearch` 时，可以使用 SASL 代理认证。

```
[root@alpha ld]# ldapsearch -U Antonio -w antonio -b "ou=apps,dc=linuxholics,dc=com" "(uid=WebApp)"X u:webmaster
SASL/DIGEST-MD5 authentication started
SASL username: u:webmaster
SASL SSF: 128
SASL data security layer installed.
.
# WebApp, apps, linuxholics.com
dn: uid=WebApp,ou=apps,dc=linuxholics,dc=com
cn: WebApp
sn: User for WebApp
objectClass: inetOrgPerson
userPassword:: V2ViQXBw
uid: WebApp
# search result
search: 4
result: 0 Success
# numResponses: 2
# numEntries: 2
```

我们可以看到，这个 Antonio 无需输入任何额外密码即可读取数据。

### 客户端证书

我们在本章已经已经了如何使用服务器证书来保护与 LDAP 服务器的连接。为了增加额外的安全层级，我们还可以使用客户端证书。

我们将为我们的客户端计算机 `bravo.linuxholics.com` 创建一个新证书。该过程与我们创建服务器证书的操作非常相似。

## 第 2 章 保护目录

我们已经创建了自己的 CA，因此不需要需要重复此过程。我们将开始为新的客户端证书生成密钥。

```
[root@alpha CA]# openssl genrsa -out /etc/pki/CA/private/bravo.linuxaholics.com.key
Generating RSA private key, 2048 bit long modulus
..................................+++
..................................+++
e is 65537 (0x10001)
```

接下来，我们创建证书请求。

```
[root@alpha CA]# openssl req -new -key /etc/pki/CA/private/bravo.linuxaholics.com.key -out /etc/pki/CA/certs/bravo.linuxaholics.com.csr
你将被要求输入将整合到证书请求中的信息。
你即将输入的内容被称为有名名称（Distinguished Name，简称 DN）。
有很多字段，但你可以留空一些。
对于某些字段将有一个默认值，
如果你输入 '.'，该字段将被留空。
-----
国家名称 (两位字母代码) [XX]:ES
州或省名称 (全称) []:Madrid
地区名称 (例如，城市) [Default City]:Madrid
组织名称 (例如，公司) [Default Company Ltd]:linuxaholics
组织单位名称 (例如，部门) []:
通用名称 (例如，你的姓名或你服务器的主机名) []:bravo.linuxaholics.com
电子邮箱地址 []:
```

请输入以下随你的证书请求一起发送的“额外”属性

挑战密码 []:

可选的公司名称 []:

## 第 2 章 保护目录

我们用我们的 CA 对请求进行签名以获取实际的证书文件。

```
[root@alpha CA]# openssl ca -keyfile /etc/pki/CA/private/ca.key.pem -cert /etc/pki/CA/certs/ca.cert.pem -in /etc/pki/CA/certs/bravo.linuxaholics.com.csr -out /etc/pki/CA/certs/bravo.linuxaholics.com.crt
Using configuration from /etc/pki/tls/openssl.cnf
Enter pass phrase for /etc/pki/CA/private/ca.key.pem:
Check that the request matches the signature
Signature ok
Certificate Details:
```

Serial Number: 2 (0x2)

Validity

Not Before: Jan 24 12:22:09 2018 GMT

Not After : Jan 24 12:22:09 2019 GMT

Subject:

countryName = ES

stateOrProvinceName = Madrid

organizationName = linuxaholics

commonName = bravo.linuxaholics.com

X509v3 extensions:

X509v3 Basic Constraints:

CA:FALSE

Netscape Comment:

OpenSSL Generated Certificate

X509v3 Subject Key Identifier:

31:DD:BA:DF:34:F2:C2:EC:3A:8E:EE:BF:3A:93

X509v3 Authority Key Identifier:

keyid:86:9C:4F:A9:34:6A:38:CB:EE:EF:78:2A:4F:BD:CD:59:07

Certificate is to be certified until Jan 24 12:22:09 2019 (365 days)

Sign the certificate? [y/n]:y

+   1 certificate requests, commit? [y/n]

Write out database with 1 new entries

Data Updated

保护目录

现在我们只需要将客户端证书以及 CA 证书传输到客户端计算机。
