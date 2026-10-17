
# 第 12 章：保护 Linux 安全

`make` 命令用于创建创建 SSL 证书的 Makefile。在不传递任何参数的情况下，`make` 命令仅会打印上一个示例中列出的信息。以下定义了你可以给 `make` 的每个参数：

- `make server.key`——创建通用的公钥/私钥对。
- `make server.csr`——生成通用的 SSL 服务请求。
- `make server.crt`——生成通用的 SSL 测试证书。
- `make stunnel.pem`——生成通用的 SSL 测试证书，但将私钥放在与 SSL 测试证书相同的同一个文件中。
- `make genkey`——与 `make server.key` 相同，但它将密钥存放在 `ssl.key` 目录下。
- `make createreq`——与 `make server.csr` 相同，但它将证书服务请求放在 `ssl.csr` 目录中。
- `make testcert`——与 `make server.crt` 相同，但它将证书放在 `ssl.csr` 目录中。

## 使用第三方证书颁发机构

在现实世界中，我知道你是是因为我能认出你的脸、声音和举止。在互联网上，我无法看到这些，必须依靠第三方来为你的身份背书。为了确保证书是不可更改的，在证书颁发时必须由第三方签名，并且每当终端用户访问你的网站并加载它时，都必须进行验证。以下是第三方证书颁发机构列表：

- GlobalSign—www.globalsign.com/
- GeoTrust—https://www.geotrust.com/
- VeriSign—https://www.verisign.com/
- RapidSSL—https://www.rapidssl.com/
- Thawte—www.thawte.com/
- EnTrust—www.entrust.com/
- ipsCA—www.ipsca.com/
- COMODO Group—www.comodo.com/

### 注意

由于证书业务的流动性，当你阅读这些内容时，其中某些可能不再有效，另一些可能已经出现。要获取更新的证书颁发机构列表，请从你的 Firefox 浏览器选择“编辑设置”（Edit Preferences）。在出现的设置窗口中，选择“高级”（Advanced）->“加密”（Encryption），然后选择“查看证书”（View Certificates）按钮。在出现的证书管理器中，参考“授权机构”（Authorities）来查看你接收过证书的证书颁发机构。■

这些证书颁发机构中的每一个都向几乎几乎每一个 Web 浏览器嵌入了一段加密代码。这段加密代码允许 Web 浏览器判断 SSL 证书是否真实。如果没有这种验证，黑客很容易生成自己的证书，并欺骗人们认为他们正在向信誉良好的源提供敏感信息。

未验证的证书被称为自签名证书。如果你遇到一个未由受信任第三方识别身份的网站，你的 Web 浏览器将显示类似于图 12-5 所示的消息。

## 图 12-5

当网站未通过验证时，会弹出一个窗口。

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_443_0.png)

这并不意味着你一定遇到了任何非法、不道德或肥胖的内容。许多网站使用自签名证书，并不是因为它们试图欺骗你，而是因为可能没有理由验证证书的真实所有者，而且不想支付获取自签名证书的费用：

- 网站不接受输入——在这种情况下，终端用户必须担心。
- 网站允许你保护传输过程。
- 其中的数据可能是敏感的。
- 使用自签名证书直到你准备好
- 第三方源稍后验证。

# 第 12 章：保护 Linux 安全

### 创建服务请求

要从 Fedora Linux 系统创建第三方验证的证书，你必须首先从证书请求（CSR）开始。要创建 CSR，请在你的服务器上执行：

```bash
@ cd /etc/pki/tls/certs
@ make certreq
@ umask 077
/usr/bin/openssl req -utf8 -new key /etc/pki/tls/private/local.key -out /etc/pki/tls/certs/local.csr
```

你会被要求输入密码来保护你的私钥。这个密码长度为八个字符，不应该是字典单词或包含数字或标点符号。你输入的字符不会显示在屏幕上，以防止他人窥视

输入密码：
再次输入密码以验证。
验证 - 输入密码：

证书生成过程现在开始。

现在是时候向稍后验证的证书添加一些信息了。在此之前，你必须解锁你创建的私钥。通过输入你为密码输入的密码，然后按照提示输入信息。

输入 `/etc/pki/tls/private/local.key` 的密码： *****
你将输入将纳入证书请求的信息。
你要输入的内容被称为区分名称（Distinguished Name）或 DN。
有很多字段可以留空。对于某些字段有一个默认值，
如果你输入 "，则该字段将留空。

```
国家名称（两位字母代码） [GB]:US
州或省（全称） [Berkshire]:Connecticut
地名名称（例如，城市）：Mystic
组织名称（例如，公司） [My Company Ltd]:Acme Marina, Inc.
组织单元名称（例如，部门） [:InfoTech
通用名称（例如，你的姓名或你服务器的主机名） []:www.acmemarina.com
电子邮件地址 [:]:webmaster@acmemarina.com
```

要完成此过程，系统将询问你是否想为你的证书添加任何额外属性。除非你有理由提供更多信息，否则你只需在以下每个提示处直接按回车键，以将其留空。

请输入以下将与你的证书请求一并发送的“额外”属性：
挑战密码：
可选的公司名称：

## 获取你的 CSR 签名

- 可信誉与稳定性
- 价格
- 浏览器识别
- 质保
- 支持
- 证书有效期

选择好证书后，你将必须通过一些验证步骤。每个签名者都有不同的验证方法和证书信息。有些签名者要求你传真公司注册副本，另一些则要求公司官员在场与验证操作员通话。在过程的某个阶段，你会被要求将 CSR 的内容复制并粘贴到签名者的 Web 表表中。

```
# cd /etc/pki/certs/
# create localhost.csr
--- CERTIFICATE REQUEST ---
MBI6JCCAMCA0OAAwgKBAQAgAjBGBVAY1TMRROEgYDWQOIEwtb25ZWN0AWN1
DDEOPMAUG16HMXTZd1jMRUGGYAYODODQQE5YH2111E1hclmY3bIFfYAWsSwG51JlWS
BAUAGGAEXCMS5B1MR1Y2JRdY2fVdYvGOGFbWWXYJpBmeYp29tIWfMAFGCSQG
MCUCGC3GS3D1B5OEAA1QDBQ0HY4pKMIlyXCrozcaubV0vWNNLHYRYwB6SZ
u2ebc6W14qwaXubuaDubmB0Y/Y9IDM126W4q4waM1P315020f4wyt3JnLyw
u6j3V0R40Qd6qAY7PKCRUSR0On5sqqGJ77LpPv253vQMIBTYW2ZckNnc
jwW0I8IAGBABAAw0YKZoChInTvcNAQEEDBAQVAN6E6ajaozZZQopNR5HY2KR9wG
1b8I1m60PGOTMC4b2SccWwaS0b4d0Q70nBdsS++-QQCZW11fegaOSMnKII117TFS
Y1YWbPGOTMC4b2Z7urRY77W9A3JPH4xb2+yntcb1 ---
--- CERTIFICATE REQUEST ---
```

你可以使用该方法将 CSR 复制并粘贴到签名者的 Web 表表中。

# 第 2 章：保护 Linux

完成问题后，你必须提供签名请求并回答所有问题。在 48 到 72 小时内，你应该会收到一封带有你崭新的 SSL 证书的电子邮件。证书看起来将如下：

```
--- BEGIN CERTIFICATE ---
MIIEFJC3+aBIBAQIBAg1BAgIL2622Z6IzN97JAFVODBaqqkhIGwBOADFADDCB
UjEF0BA61wMA0G13QSIb3DQEAAgIEFn44y+pBFSAJK11I3cQ0W0029aZEMBUGA1UEECMOWWvY
```
