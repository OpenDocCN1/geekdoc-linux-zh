
## sign.sh 签名 SSL 证书请求 (CSR)
版权所有 (c) 1998-1999 Ralph S. Engenschal，保留所有。

```bash
# 确保环境

if [ ! -d ca.db.certs ]; then
  mkdir ca.db.certs
fi

if [ ! -f ca.db.serial ]; then
  echo '01' > ca.db.serial
fi

if [ ! -f ca.db.index ]; then
  cp /dev/null ca.db.index
fi
```

```bash
# 创建自己的 OpenSSL 配置

cat > ca.config <<EOT
{
CA_own = CA_own
dir = /usr/share/ssl/
certs = /usr/share/ssl/certs
new_certs_dir = /usr/share/ssl/ca.db.certs
database = /usr/share/ssl/ca.db.index
serial = /usr/share/ssl/ca.db.serial
RANDFILE = /usr/share/ssl/ca.db.rand
certificate = /usr/share/ssl/certs/ca.crt
private_key = /usr/share/ssl/private/ca.key
default_days = 365
default_crl_days = 30
default_md = md5
policy = policy_anything
[ policy_anything]
countryName = optional
stateProvince = optional
locality = optional
organizationUnitName = optional
commonName = supplied
emailAddress = optional
}
EOT
```

```bash
# 签名证书

echo "signing: $CSR -> $CERT"
openssl ca -config ca.config -out $CERT -infiles $CSR
echo "CA verifying: $CERT <-> CA cert"
openssl verify -CAfile /usr/share/ssl/certs/ca.crt $CERT
```

### 清理 OpenSSL
```bash
rm -f ca.config
rm -f ca.db.serial.old
rm -f ca.db.index.old
```

```bash
# 退出
exit 0
```

第 2
一旦脚本文件创建，将其变为可执行并更改默认权限是重要的。使此文件可执行将允许系统运行它，更改默认权限是为了仅允许 root 用户更改此文件。

- 为了创建此脚本并更改其默认权限，请使用命令：
`[root@deep] chmod 700 /usr/share/ssl/misc/sign`

# OpenSSL 1
## 第 5 章

随您的证书请求一同发送
挑战密码 [..]:
可选公司名称 [..]:

> 警告：当 OpenSSL 提示你输入*通用名称（Common Name）*时，请确保输入的是服务器的 FQDN（完全限定域名）（例如，当你为一个以后通过 `https://www.mydomain.com/` 访问的网站生成 CSR 时）。

生成证书请求（CSR）后，你必须将此证书发送给商业证书授权机构（CA）（如 Thawte 或 Veris）进行签名。你通常需要将 CSR 提交到 Web 表单，支付签名费用，等待签名后的证书并将其存储在 `~mydomain.com.crt` 文件中。结果是一个真实的证书，可以配合 Apache 使用。

# CA 与 CSR 生成：

如果你不想付费给商业证书授权机构（CA）来签署证书，可以使用自己的 CA，现在只需对由该 CA 生成的 CSR 进行签名。这种方案非常经济，允许任何人托管自己的 CA 服务器，并根据需要生成任意数量的证书，而无需向商业 CA 支付一分钱。

遗憾的是，在电子领域使用自己的 CA 生成证书会导致问题，因为客户需要信任你的组织或使用受认可的 CA。请看下文如何使用自己的 CA 签名 CSR。

## 第 1 步

对于上面的 Apache 服务器，第一步是为你的 CA 创建一个受密码短保护的 RSA 私钥。下面的命令将生成 1024 位的 RSA 私钥并将其存储在文件 `..ca.key` 中。它会要求你输入密码短：请使用安全且容易记住的内容。如果没有密钥，你的证书将毫无用处。

- 为你的 (CA) 创建 RSA 私钥，请使用以下命令：
`[root@deep #]# cd /usr/share/ssl/`
`[root@deep $]# openssl genrsa -des3 -out ca.key 1024`
Generating RSA private key, 1024 bit long modulus
..................................................******
 e is 65537 (0x10001)
Enter PEM pass phrase:
Verifying passphrase - 

> 警告：请在安全位置备份你的 `..ca.key` 文件，并记住你输入的密码短。良好的选择是将此信息备份到软盘或其他可移动介质上。

# OpenSSL | 1
## 第 5 章

### 第 2 步
现在，我们通过 CA 的 RSA 密钥创建一个自签名 (CA) 证书（x509 结构）。
使用 `-x509` 切换开关时，`req` 命令会创建一个自签名证书。

- 创建自签名 (CA) 证书，请使用以下命令：
`[root@deep ssl]# openssl req -new -x509 -days 365 -key ca.key -out ca.crt`
Using configuration from /usr/share/ssl/openssl.cnf
Enter PEM pass phrase:
你将被要求输入将纳入证书请求中的信息。
你将输入的内容称为区分名称（Distinguished Name，简称 DN）。
有几个字段可以留空，某些字段会有默认值，
如果你输入 `,`，该字段将留空。
国家名称（2 位代码） [CA]:
州或省（全名） [Quebec]:
地区名称（例如，城市） [Montreal]:
组织名称（例如，公司） [OpenNA, Inc.]:
组织单位名称（例如，部门） [Open Network]:Sales Dept
通用名称（例如，你的名称） [www.openssl.com]:
邮箱地址 [noc@openssl.com]:sales@openssl.com

### 第 3 步
一旦创建了自签名 (CA) 证书，我们必须将所有证书和 CA 文件放置到相应的目录中。

- 将文件放入相应的目录，请使用以下命令：
`[root@deep ssl]# mv www.mydomain.com.key private/`
`[root@deep ssl]# mv ca.key private/`
`[root@deep ssl]# mv ca.crt certs/`

### 第 4 步
最后，你可以使用此 CA 签名所有服务器的 CSR，以便为网络内部创建真实的 SSL 证书（假设你手头有一个 `www.mydomain.com.csr`）。
我们必须准备用于签名的“sign”脚本。

字体 签名服务器 CSR 以创建真实的 SSL 证书，请使用以下命令：
`[root@deep ssl]# / -> /usr/share/ssl/misc/sign www.mydomain.com.csr`
CA signing: www.mydomain.com -> www.mydomain.com.crt
Using configuration from ca.config
Enter PEM pass phrase:
Check that the request matches the signature
Signature ok: ok
The Subjects Distinguished Name is as follows
countryName :PRINTABLE:'CA'
stateProvinceName :PRINTABLE:'Quebec'
localityName :PRINTABLE:'Montreal'
organizationName :PRINTABLE:'OpenNA, Inc.'
organizationalUnitName :PRINTABLE:'Open Network Architecture'
commonName :PRINTABLE:'www.openssl.com'
emailAddress :IA5STRING:'noc@openssl.com'
Certificate is to be certified until Oct 18 14:59:29 2001 GMT (365 days)
Sign the certificate? [y/n]:y

1 out of 1 certificate requests certified, commit? [y/n]y
Write out database with 1 new entries
Data Base Updated
CA verifying: www.mydomain.com.crt <-- CA cert
www.mydomain.com.crt: OK

这会签名 CSR 并生成一个 `www.mydomain.com.crt` 文件。将此文件移动到相应的目录中：

- 将 CRT 文件移动到相应的目录，请使用以下命令：
`[root@deep ssl $] mv www.mydomain.com.crt/`

现在你有两个文件：`www.mydomain.com.key` 和 `www.mydomain.com.crt`。这些文件现在可以如下所示用于 Apache 服务器的 `httpd.conf` 虚拟主机部分：

```
SSLCertificateFile /usr/share/ssl/certs/www.mydomain.com.crt
SSLCertificateKey /usr/share/ssl/private/www.mydomain.com.key
```

在本例中，`www.mydomain.com.crt` 是我们的服务器证书，`www.mydomain.com.key` 是我们的私钥。`csr` 文件不再需要了，可以删除它。

- 从系统中删除此文件，请使用以下命令：
`[root@deep ssl $] rm -f .mydomain.csr`

# 第 5 章

# 加固 OpenSSL
本节专门介绍用于改进和加强 OpenSSL 安全性的操作。请注意，我们指的是程序自带的功能，而不是任何额外的软件。

## 修改 OpenSSL 密钥的默认模式：

让你的密钥仅供超级用户 `root` 读取和写入。这很重要，因为没有人需要碰这些文件。

- 要让密钥仅供 `root` 读写，请使用以下命令：

```
[root@deep] # chmod 400 /usr/share/ssl/private/
[root@deep] # chmod 400 /usr/share/ssl/certs/ca.crt
[root@deep] # chmod 400 /usr/share/ssl/certs/www.mydomain.com.crt
[root@deep] # chmod 400 /usr/share/ssl/private/ca.key
[root@deep] # chmod 400 /usr/share/ssl/private/www.mydomain.com.key
```
