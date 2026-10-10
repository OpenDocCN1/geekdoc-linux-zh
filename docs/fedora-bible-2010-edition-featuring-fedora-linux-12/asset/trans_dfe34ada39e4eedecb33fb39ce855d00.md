
# 第570页 第三部分：管理 Fedora

- **RapidSSL.com** — `www.rapidssl.com/`
- **Thawte** — `www.thawte.com/`
- **Entrust** — `www.entrust.com/`
- **ipcsCA** — `www.ipcsca.com/`
- **COMODO Group** — `www.comodogroup.com/`

> **注意：** 由于证书行业的流动性，当您阅读此书时，其中一些公司可能已不再经营，而另一些公司可能才刚成立。要获取更最新的证书颁发机构（CA）列表，请在您的 Mozilla Firefox 浏览器中选择“编辑” -> “首选项”。在出现的首选项窗口中，选择“高级” -> “加密” -> “查看证书”。在出现的证书管理器窗口中，参考“权威机构”选项卡，查看您已接收证书的证书颁发机构。建议您为公开访问的资源使用知名证书颁发机构。

这些证书颁发机构（CA）中的每一个都将一段加密代码嵌入到了世界上几乎每一个 Web 浏览器中。这段加密代码使 Web 浏览器能够判断 SSL 证书是否真实有效。如果没有这种验证，黑客生成自己的证书并欺骗人们认为他们正在向可信赖的来源提供敏感信息将变得极其简单。

未被验证的证书称为自签名证书。如果您遇到一个身份未经验证的可信第三方认证的站点，您的 Web 浏览器将显示警告消息。

这并不一定意味着您遇到了非法、不道德或令人发胖的内容。许多站点选择使用自签名证书，并非因为她们想欺骗您，而是因为可能没有理由验证证书的真实所有者，而且她们不想支付验证证书的费用。使用自签名证书的一些原因包括：

- **Web 站点不接受输入** — 在这种情况下，作为最终用户的您没有什么需要担心的。因为没有人在试图窃取您的信息，您也没有提供任何信息。大多数情况下，这样做只是为了确保从服务器到您的 Web 传输的安全性。数据本身可能并不敏感，但作为一个好的网络公民，该站点启用了传输安全功能，以防止第三方嗅探流量。
- **Web 站点服务于少量客户** — 如果您运行的是一个拥有非常有限客户群的 Web 站点，例如应用服务提供商（ASP），您可以简单地通知用户您没有证书签名者，他们可以浏览证书信息并通过电话或当面与您进行验证。
- **测试** — 如果您只是在测试新的 Web 站点或基于 Web 的应用程序，支付 SSL 证书的费用是没有意义的。在您准备正式启用之前，请使用自签名证书。

## 创建证书服务请求

要创建经过第三方验证的 SSL 证书，您必须从证书服务请求（CSR）开始。要创建 CSR，请在您的 Web 服务器上执行以下操作：

```bash
# cd /etc/pki/tls/certs
# make certreq
/usr/bin/openssl
```

您即将被要求输入将包含在您的证书请求中的信息。您即将输入的是所谓的可分辨名称或 DN（Distinguished Name）。字段相当多，但您可以留空其中一些。某些字段将有默认值。如果您输入“.”，该字段将留空。`-----`
国家名称（2 位代码）[GB] :US
州或省名称（全名）[Berkshire] : Connecticut
地区名称（例如，城市）[Newbury] : Mystic
组织名称（例如，公司）[My Company Ltd] : Acme Marina, Inc.
组织单位名称（例如，部门）[] :InfoTech
通用名称（例如，您的姓名或服务器的主机名）[] : www.acmemarina.com
电子邮件地址 [] : webmaster@acmemarina.com

> **注意**：您应确保提供的主机名（本例中为 www.acmemarina.com）与您的 Web 站点的实际主机名匹配。如果名称不匹配，用户将看到看似证书错误的信息。此外，如果您为密钥输入密码，每次重启 httpd 时都需要输入该密码。

要完成此过程，您会被要求是否希望向证书添加任何额外属性。除非您有理由提供更多信息，否则应在以下每个提示处直接按 Enter 键以将其留空。

```bash
Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password [] :
An optional company name [] :
```

## 获取 CSR 签名

创建 CSR 后，您需要将其发送给签名机构进行验证。此过程的第一步是选择一个签名机构。每个签名机构的协议、价格和产品各不相同。查看本章前面“使用第三方证书签名者”部分列出的每个签名机构，以确定哪个最适合您。签名机构在以下方面存在差异：

- 信誉和稳定性
- 定价
- 浏览器识别度
- 保修
- 支持
- 证书强度

选定证书签名者后，您必须完成一些验证步骤。每个签名者验证身份和证书信息的方法各不相同。有些要求您传真公司章程，而有些则要求公司负责人可供验证操作员联系。在过程的某个阶段，您将被要求将创建的 CSR 内容复制并粘贴到签名者的 Web 表单中。

```
# cd /etc/pki/tls/certs
# cat localhost.csr
----- BEGIN CERTIFICATE REQUEST -----
MIIE8jCCAQMCAQAwgaKxCzAJBgnNVBAYTA LVITMQreEgYDVUQwEGY2EtbU5lZHR5a
2NW0aWNW1 dEEPMCAGAU1BXBxMGTxIzdGlJmRowGAYDVOQQEXbFV2l 1lBiHcmluY3SwG5WSjLjER
MA8GA1UECxMI5W5mb1RI2gxgzxZA2BgNVBATEn43dyShY211bWFya5hLmV0cTNrTng
MCUGCGSd5B3DqJARYyDV1BWFzGDYvQGjbdwYfXJpbpoBuu29gMlfgAAGCCSgZ
STJ3DEEAOUM4AGNMADCB4QOBCDCyGyHpxKmlYXCzM2e8uEVYoWg5ZM7WkRwBWGZ
C2bDweyJ64YwXuwWixDxuBDboMwV/YQ3Nf2MWX44Dg4mxpR153E01oFc4YtZJN1yW
aU6G3W7OrA6N0WqXZDIP1RcxUsG9RU-one4KQJ6TL7LPX2g923Q4VWETzCkIInC-
gwOBwuTIDAQABAOADqDOqYJ1K2Yi2vQ2AgOwOEAOgYDQxZAMy6eOLuzEGQzOZM5RSzKy9Rye
18C8L3MgoPHO65CCWp3w0cq4QdBC7X7On8dS/+OOCCZW11IgefGaSQMlTZKllTZl7Ff8
YiWYB6qpPTMC4bPOZZLURCywZc7kDCBqXBw7B1U/ 3A25SnvkRY7vGNL9nq+7E8J718
W9Aj3PX4vb2+4yrTTcBl=
----- END CERTIFICATE REQUEST -----
```

您可以使用鼠标将 CSR 复制并粘贴到签名者的 Web 表单中。

完成信息验证、支付签名费用并回答所有问题后，您就完成了大部分流程。在 48 到 72 小时内，您应该会收到一封电子邮件，其中包含您的崭新 SSL 证书。证书的外观类似于以下内容：

```
----- BEGIN CERTIFICATE-----
MII2EP3CCAI+gwAIBAgiI2MIZ62d6nj1ZgN97cTAVFODANBGqkghliU3qoBUAQFADCb
ujBFbm8GA1UEGBWVmVyaW9u3gCnPTJmAVZDqXcEYXMzQaU3M2UQVbSUDXMONVvW
YvaVNP224h1El1uYx4zGxAxBGnVBA5TLZL2lIcmTAwu4DLEUd0yGvvLbm4FwoAbwUVyg
dmVylENBIcg2Zxhzc3MgMzQ2X2MPEMBlCGI1orfZnDOD3d3Ln2lczAWuLMHibv95DUFMg
SW5jb3Rl4m351FJ1Zl4gTELBqqIMS9ZZIE7ECUrCcVxyEWyBXZjQxU2JlbZBVXQcQFw
M2AuXHTWDMWDBAcPvkwmDAAW2Z3bHNSW91Mm03TQ4xYmcyGYZ0QKQXBJVUEETMBl8
AL1UCEVMCV2PzluGl2UV3ThERzrE271UBXKCJLRmkY7XKJbCXRXQXcGZAgzAEJBVa8U
EklLTSTBZXJ2XaWMLcw9gSW5jl2JMMcAluU1ECQQD433MTMWmNQWYVDQFCpClUZlJtc
CYBvZBziCGUYYQDQ3d3LnZlcUazw4DunMBS9ycGC6KGMpM6DAXBdASBgnVBAU
C2klbXNlCnYuY29tMIGFMA0GCSqGSIb3dQEAQUAANQDADCB4IQKBgQdDaHSk+uzOf
7/jDPEnQ78UBai1LyPFILKXfjhj3XpXLGW2LmkDmdzj7Xsa4x7AhErplubuNVhjVI0
FnlDopax4pyr4nn+P8FYm54MS9crbcZykZ1mK2Q1yqz9F/7yOWpD13Qtc4eqYCrazQ
g9hTXD2/BO4twvCAFCwUWbOQuLCNVZqojDABQBo4AI3TCTCASSCQ5EVDY07TBA7n
ADBEBSgVHGSAFP7XDKAG2C0SAQCCSUBBCsXDMC6wkAYlIKoYBROBuqGZKWhClOJh8g
O18vtzid3lnZ1cmlzlaMUdLdmNvfbS9ycGBwCQWVRBRpBQDRdqMwcGmgCgdIUdqQDHW88g
CWSOSAG+BIEMOGoCwIYBQUaHBCC&C#5aD1FVbmBMQCCmcGAQUPBwBEBcwJiAQ
BqgBEBFEGQcVWYYAaHRCvDoVvLL29jC2AcudVyaXNP224uY2tMEYGA1UDhW0w/MO
O6AsODenGNHWOdHA6L9jc mwdudVNvqaZN24uY2tLN8sYXN6M0LulGViJyBmFWa
B1Ll2XnAr+aChESR0Lb3Qrjgv2yLmwjjkPMCJWjceYfdX4H+Mbg/61QmmK9auWAT
WFo1FW/+a8OWRQJQLMA2QOQVhX4zNj6pGCNVYAQQSHumIlESj7vt4d1LX
----- END CERTIFICATE -----
```

将此证书复制并粘贴到一个名为 server.crt 的空文件中，该文件必须位于 /etc/pki/tls/certs 目录下，然后重启您的 Web 服务器。

```
# service httpd restart
```

假设您的 Web 站点之前工作正常，现在您可以在 Web 地址中的 http 后添加一个“s”来以安全方式查看它。因此，如果您之前通过 http://www.acmemarina.com 查看您的 Web 站点，现在您可以通过访问 https://www.acmemarina.com 以安全方式查看它。

# 创建自签名证书

生成并运行自签名 SSL 证书比拥有签名证书容易得多。要生成自签名 SSL 证书，请执行以下操作：

1. 移除当前存在的密钥和证书：
   ```
   # rm /etc/pki/tls/certs/localhost.crt
   # rm /etc/pki/tls/private/localhost.key
   ```

2. 创建您自己的服务器密钥：
   ```
   # make genkey
   ```

3. 通过键入以下内容创建自签名证书：
   ```
   # make testcert
   umask 77 ; \
   /usr/bin/openssl req -new -key /etc/httpd/conf/ssl.key/server.key \
       -x509 -days 365 -out /etc/httpd/conf/ssl.key/server.crt
   .
   .
   .
   ```

此时，是时候开始向证书添加一些识别信息了。在此之前，您必须解锁刚刚创建的私钥。输入之前键入的密码来完成此操作。然后按照以下示例过程操作：

> 您即将被要求输入将包含在您的证书请求中的信息。

