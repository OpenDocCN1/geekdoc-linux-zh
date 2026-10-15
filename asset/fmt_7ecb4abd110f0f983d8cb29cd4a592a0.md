
进入 `/etc/pki/tls/certs` 目录，找到 `xxx.json`。

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

### 1. 删除当前存在的密钥和证书

```bash
# rm /etc/pki/tls/certs/localhost.crt
# rm /etc/pki/tls/private/localhost.key
```

### 2. 创建你自己的服务器密钥

```bash
# make genkey
```

### 3. 通过输入以下内容创建自签名证书

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

## 通用名称（例如，您的姓名或您服务器的主机名）

[ ]: www.industrialpressinc.com

## 电子邮件地址 [ ]

[ ]: webmaster@industrialpressinc.com

上述生成过程将所有文件放置到正确的位置。您需要做的只是重启您的 Web 服务器，并在您的 URL 前面加上 https 而不是 http。请别忘了：您的 Web 浏览器会弹出证书验证消息，您可以安全地忽略它。

## 导出加密技术
