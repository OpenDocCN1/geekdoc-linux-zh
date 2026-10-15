
输入一个长的密码短语——它可以是一个包含空格和标点符号的句子——然后按回车。新密钥现在位于`/etc/httpd/conf/ssl.key/server.key`文件中。

## 生成证书请求

下一步是生成一个证书请求，你可以将其发送给证书机构以请求经过签名的数字证书。通常，你需要为 CA 的服务支付年费。Verisign、Entrust、Thawa 是美国一些知名的 CA。你可以在 PKI 页面（`http://www.pki-page.org/`）找到其他 CA 的链接。要生成证书请求，输入：

```
cd /etc/httpd/conf

make certreq
```

系统会提示你输入密码短语——输入你创建密钥时输入的密码短语。系统还会提示你输入以下信息：

- **国家名称 (Country name)**：输入两个字母的国家代码（例如，Maryland）。双字母国家代码的官方列表请参阅 `http://www.iso.org/iso/prods-services/iso3166ma/02iso-3166-code-lists/list-enl.html`。
- **州或省名称 (State or province name)**：输入全称（例如，Maryland）。
- **地区名称 (Locality name)**：输入你所在的城市或城镇名称（例如，North Potomac）。
- **组织名称 (Organization name)**：输入你的组织名称。
- **组织单元 (Organization unit)**：输入部门名称。
- **通用名称 (Common name)**：输入服务器的主机名。
- **电子邮件地址 (Email address)**：输入个人的电子邮件地址。

完成信息输入后，证书请求将创建并保存在`/etc/httpd/conf/ssl.crt`中。

## 创建测试证书

为了测试目的，Red Hat Linux PC 生成一个自签名证书。要生成证书，请以 root 登录并输入以下内容：

```
cd /etc/httpd/conf

make test

umask 77 :

/usr/bin/openssl genrsa -des3 1024 > \
/etc/httpd/conf/ssl.key/server.key

Generating RSA private key, 1024 bit long modulus

..................................................++++++

++++++++++++++

e fs 65537 (0x10001)

Enter PEM pass phrase:
```

`openssl req -x509 -new -days 365 -key /etc/httpd/conf/ssl.key/server.key -out /etc/httpd/conf/ssl.crt/server.crt -config /etc/httpd/conf/openssl.conf`

系统会提示输入密码短语，如下所示：

```
Starting http: Apache/2.0.40 mod_ssl/2.0.40 (Pass Phrase Dialog)

Some of your key files are encrypted for security reasons.

In order to read them you have to provide us with the pass phrases.
```
Server_host.name:443 (RSA)
Enter pass phrase:
```

输入你创建密钥时使用的密码短语。

## 测试安全服务器

在安装 CA 签名证书或创建测试证书后，你可以尝试安全服务器。假设 Apache 已经在运行，以 root 登录并输入以下命令重启服务器：

```
service httpd restart
```

由于你的服务器密钥已加密，系统会提示输入密码，如下：

```
Starting http: Apache/2.0.40 mod_ssl/2.0.40 (Pass Phrase Dialog)
Some of your key files are encrypted for security reasons.
In order to read them you have to provide us with the pass phrases.
```

Server_host.name:443 (RSA)

Enter pass phrase:

输入你创建密钥时使用的密码短语并按回车。Apache 服务器现在应该运行。

你可以从其他 PC 的 Web 浏览器连接到安全服务器。例如，如果你的 Red Hat Linux 系统（运行 Apache 服务器的系统）IP 地址为`192.168.0.8`，则输入以下 URL：

```
https://192.168.0.8/
```
