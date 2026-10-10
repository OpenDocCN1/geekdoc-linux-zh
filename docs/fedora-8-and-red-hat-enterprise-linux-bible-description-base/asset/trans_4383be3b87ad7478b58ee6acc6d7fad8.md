

![](img/fb202c163797a743c3c6cf236316bc96_660_0.png)

这并不一定意味着你遇到了任何非法、不道德或令人发胖的事情。许多网站选择使用*自签名*证书，这并非因为他们想对你耍花招，而是因为验证证书真正所有者的原因可能并不存在，且他们不想承担获得证书验证的成本。使用*自签名*证书的一些原因包括：

- **网站不接受任何输入** — 在这种情况下，作为最终用户你无需担心。因为你没有提供任何信息，所以没有人试图窃取你的信息。大多数时候，这样做只是为了保护从服务器到你之间的 Web 传输。数据本身可能并不敏感，但作为一个负责任的网民，该网站启用了安全传输以防止第三方嗅探流量。
- **网站服务于少数客户** — 如果你运营的网站拥有非常有限的客户群体，例如应用服务提供商（ASP），你可以简单地告知用户你没有证书签发机构，他们可以浏览证书信息并通过电话或亲自与你进行验证。
- **测试** — 如果你只是在测试新的网站或基于 Web 的应用程序，那么花钱购买 SSL 证书是没有意义的。在准备好上线之前，请使用*自签名*证书。

## 创建证书服务请求

要创建经过第三方验证的 SSL 证书，你首先需要从证书服务请求（CSR）开始。要在 Web 服务器上创建 CSR，请执行以下操作：

```bash
# cd /etc/pki/tls/certs
# make certreq
/usr/bin/openssl
```

你即将被要求输入将合并到你的证书请求中的信息。
你即将输入的是称为区分名称（Distinguished Name 或 DN）的内容。
虽然有许多字段，但你可以留空一些。
某些字段将有默认值，
如果你输入“.”，该字段将保持空白。

Country Name (2 letter code) [GB] : US
State or Province Name (full name) [Berkshire] : Connecticut
Locality Name (eg, city) [Newbury] : Mystic
Organization Name (eg, company) [My Company Ltd] : Acme Marina, Inc.
Organizational Unit Name (eg, section) [] : InfoTech
Common Name (eg, your name or your server's hostname)
[] : www.acmarina.com
Email Address [] : webmaster@acmarina.com

为了完成流程，系统会询问你是否希望向证书添加任何额外属性。除非你有理由提供更多信息，否则你应该简单地在以下每个提示处按 Enter 键将其留空。

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password [] :
An optional company name [] :

### 获取 CSR 签名

一旦你的 CSR 创建完成，你需要将其发送给签名机构进行验证。此过程中的第一步是选择一个签名机构。每个签名机构都有不同的交易、价格和产品。查看本章前面“使用第三方证书签发者”部分列出的各个签名机构，以确定哪个最适合你。签名机构在以下方面存在差异：

- 信誉和稳定性
- 定价
- 浏览器识别
- 保修
- 支持
- 证书强度

选择证书签发者后，你需要通过一些验证步骤。每个签发者验证身份和证书信息的方法各不相同。有些要求你传真公司章程，而有些则要求公司高管可供验证操作员联系。在过程中的某个阶段，系统会要求将你创建的 CSR 内容复制并粘贴到签发者的 Web 表单中。

# 第 14 章：计算机安全问题 629

```bash
# cd /etc/pki/tls/certs
# cat localhost.csr
-----BEGIN CERTIFICATE REQUEST-----
MIIBjCCACGAgEwKBgQAwKz2AbgBNVATVATMPQwXpYDVOQIbWuB2s5uZNW0aWNj
AiE8PMAGAIUBEBMAMVXJlZ4GJjM8c0WYDQXGQK89F8Y21I1FehCumlYoSWgSM5jleR
MAGCSAIUECXM1SjMSmbiRLY2y0GzX2AGVNMBATTmeJBd35xYJJ11blYhYA5MSLmhVqtTEn
MWOGCGSGQ3Tb3DQB2JARY02VIBWFcGDGV0qwJhwZTxhpXpmuEY2ym2lmgMeGAcQQg
3iD50BQEBAQUAA GNADCBk1QBgQCQYH4FjmKXmLQ14KXmco8u8BVoVlmM2YhRwBqE
g3u2c8vyl6m4wuXuWaxiDu8xbuBwv//Jv80YDMXO4dGqMn5135E0l0F4YzY2wNJlw
AU6CjVRO46OnXyaqXZQPiRCXSNGRB4OnsqGfZJ7LLPvpQ25S9ZQW1Bt4TCkNQwc
gWBwmjDAQABoAwDQyKJZjzIHYvcABQE0aDQeAnV6eDAJOAGZQoSMRSY2YRK9wg
18o8L3mgoPHG0Sccw3Pw0w4Bq0wGQ7on84ds/+GGCZM1I21gefaQSMTNkZl1I7Fa
YiWY8bpGTTM4CbpOZZtUCRYQwR4ixN0BxX7IJu/3a25nXKrY7vGnLN9q+7681J8
W9AJ3XAvb2+ynntcB1=
-----END CERTIFICATE REQUEST-----
```

你可以使用鼠标将 CSR 复制并粘贴到签发者的 Web 表单中。

完成信息验证、支付签名费用并回答所有问题后，你就完成了大部分流程。在 48 到 72 小时内，你应该会收到一封电子邮件，里面包含你崭新的 SSL 证书。该证书看起来类似于以下内容：

```text
-----BEGIN CERTIFICATE-----
MIIEFPjCCAi3+gwIBAgQIOM1+6ZZa6NjZGn97tJAVFODANBgkqhkiG9w0BAQUFADCB
ujEfM0BGAJUBEBMVMvWyAVnP2p42gvHKi3cQgw7w0v2uYqAZRMBCGNAJiUECw9MuwNvy
aWJvZ24aI1BluxY4xzM2AxzAbgBNMvZKLZl1mT4aDlB1dA0ybVbuFUA01YUWYcOVY
dn0VjENBI/COG2Zh3MgMcPJMBCQlL01rY2GDq3d343L21cnlzaMduLMLVlb9BDFMG
5W5j5J3wLfmwJ5lFJZ1d4TG1JMSRZTEBXURCA0ykYkSNYBNZXJCpJZl2njbJAEFow
MzAxKmTuMWwAMDaBFwoNDaAxMTYwMU52NliAMiQwmwacwQcDYDQQgwVJVBtEMBEg
A1UECBMVk2PzaGlU23RVh1ThrB+rE37LH6BQXKlVMvkZXJhbCBExYXcxgXzGAZBgNVBA0U
EkLBTESBTZxJ2uAgnMlcggSW5jIjJEbmAoALBUCxGQD43k7mBwWQDYDQFlPCFcUZJmt
cyBvZ8i1c2UgYYcqg3dSjLnZjlm1zwAULwBnScv46GtKGPbMDAX6DASA6BUV8AMuC
21kXhnlcnYuY29MIMQFAOQCSQGSJ13DQBGAQQUAAGNADG1OKQyBDAHSK+uZOf
7jJDEFEXG78uBaLI3yFILLXPfhi3XpXLGz2LmKDnd0j78xa4s7AhB5pr1uVnbuTViO
FlDnpOq4Xyy4n4w8rFSw5MSg3b2g2ZyFbn0k2jjyGfwjVfQYQKPDL3G14azGcaVzaqA
qRphThdrjE04tWXCAKFiwIiBeQuiCNRwZQiDDAQBSo4JBTTCGASB9cQ4VDROA7B4aW
A0BEEBGYHhAS8FPAZ7DDCSCGSAQO+2uBKn2c0CMCVRwK1Y1WYB8BQh0O4Ewh2ihO8b
OI8wd34G1B2lQm0cewIMLhNbYh8v9yc0EcwCQURFRBPCADGAwMGCag3411BgQBhWm8B
CW6CSAG3zLliEMOQoWVWu9oAWBQ6CCoQaYFVWM6C9MQGcGzAGQFUBEBBQCSw7JAK
BgdYRgEFBQCoWYAYHRCcDoCLVrJcAcuADmYa4y4XpX2Z4Yn2FY2M5N0IG1UDqM7WDOu
OA65oDe6GNW0dHA6LY691cmUduMyyaoZN24aY2n10LXN0YmN01UDlgyBvpM6o9y
YWKTXZZZXTuiY3J8BbGcOMCSCGAO+8iL4Fn8Cz2XJDASXN2WWMTYMAOQC5QGl3
QjBBBAUAAAGBAI/PsVtmLDIkJaQ1EsnLudcEeL4FJ4AL51PwT6EXXlkIRe4a8QvVlD
81LLZXN4ra+acf5E0T01B3Qpg3v2JlmwjkrPMClWjQefvXdaHX7+Mbg/f6OmnKS9AW
9AatWF01FW/+a8OWRYQJMLB2QOQVHX4JXpGCWNY9A8HM1uiE3SJ7vt4ilX
-----END CERTIFICATE-----
```

将此证书复制并粘贴到一个名为 `server.crt` 的空文件中，该文件必须位于 `/etc/pki/tls/certs` 目录中，然后重新启动你的 Web 服务器：

```bash
# service httpd restart
```

假设你的网站之前运行正常，你现在可以通过在 Web 地址中的 http 后面加上“s”来安全地查看它。因此，如果你之前在 http://www.acmemarina.com 查看你的网站，现在可以通过访问 https://www.acmemarina.com 以安全的方式查看它。

## 创建自签名证书

生成并运行自签名 SSL 证书比拥有签名的证书要简单得多。要生成自签名 SSL 证书，请执行以下操作：

1. 删除当前存在的密钥和证书：

```bash
# rm /etc/pki/tls/certs/localhost.crt
# rm /etc/pki/tls/private/localhost.key
```

2. 创建你自己的服务器密钥：

```bash
# make genkey
```

3. 通过输入以下内容创建自签名证书：

```bash
# make testcert
umask 77 ; \
/usr/bin/openssl req -new -key /etc/httpd/conf/ssl.key/server.key
    -x509 -days 365 -out /etc/httpd/conf/ssl.key/server.crt
...
```

此时，是时候向证书添加一些识别信息了。在此之前，你必须解锁刚才创建的私钥。通过输入之前输入的密码来完成此操作。然后按照以下示例流程操作：

> 你即将被要求输入将合并到你的证书请求中的信息。你即将输入的是称为区分名称（Distinguished Name 或 DN）的内容。虽然有许多字段，但你可以留空一些。某些字段将有默认值，如果你输入“.”，该字段将保持空白。
> -----
> Country Name (2 letter code) [GB]:US
> State or Province Name (full name) [Berkshire] : Ohio
> Locality Name (eg, city)  [Newbury]: Cincinnati
> Organization Name (eg, company) [My Company Ltd]:Industrial Press, Inc.
> Organizational Unit Name (eg, section) []:RT

