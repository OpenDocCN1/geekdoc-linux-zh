
# `cd /etc/httpd/conf`

# `make certreq`

`umask 077` :

`/usr/bin/openssl genrsa -des3 1024 > /etc/httpd/conf/ssl.key/server.key`

# 加固 Linux

现在你会被要求输入密码来保护你的私钥。此密码应至少八个字符，且不应该是字典单词，也不应包含数字或标点符号。你输入的字符将不会显示在屏幕上，防止他人通过肩后的窥视获取你的密码。

Enter pass phrase:

再次输入密码以验证。

Verifying - Enter pass phrase:

证书生成过程现在开始。
现在是时候为证书添加一些标识信息了，第三方稍后将进行验证。在此之前，你必须解锁刚刚创建的私钥。通过输入你为短语输入的密码，然后按照提示输入信息即可。为证书添加信息的示例例如所示：

```
Enter pass phrase for /etc/https/conf/ssl/server.key:
```

你将被要求输入将合并到你的证书请求中的信息。

你即将输入的内容被称为别要名称（Distinguished Name）。

有很多字段可以留空，如果你输入 `.`，该字段将留空。

国家名称 (Country Name)

州/省 (State or Province)

城市 (Locality)

组织名称 (Organization)

组织单位 (Organizational Unit)

通用名称 (Common Name)

电子邮件地址 (Email)

在完成证书的过程中，你会被询问是否要为证书添加更多信息。如果你不需要，直接按回车即可。

# 获取签名 CSR

一旦创建了 CSR，你需要将其发送给证书颁发机构。第一步是选择一个证书颁发机构。检查书中列出的所有证书颁发机构，看看哪一个适用于你。以下是不同的：

- 机构

每个证书颁发机构都有不同的验证方法。在过程的某个点，你会被要求将 CSR 粘贴到颁发机构的网页表单中。

```bash
/etc/httpd/conf/ssl.csr

-----BEGIN CERTIFICATE REQUEST-----

...
```

你可以使用鼠标将 CSR 粘贴到颁发机构的网页表单。

在完成信息验证、签名以及所有问题后，你就完成了大部分流程。在 48 到 72 小时内，你会收到一封带有新 SSL 证书的电子邮件。该证书看起来如下：

```
-----BEGIN CERTIFICATE-----

...
```

# 加固 Linux

`C2kbXN1cnYu29tMIGQACS53DB0BAQUA4ADBCIQ8G0DAHx+uzof`
`7JfdEnQt8U8BA4LYIFFHJ3YXPXLGMZmkMdJsa4x7AhErpubVNHVJ10`
`LnDopsX4yrn4+PBFYM5gbrcoY2Znkm2YJYqVF/7Y02pD2310t4aecYYaz40q`
`ptpHUJy24WKWAFFUGEGM1V2Q1DA04B1JTCCESAWQYDROTROBAWI`
`ADBEBNGHWSAEPTAY4MD6G2CS5G4UB88XCM0GBV1YKYYBOWAGAEWHGHD0HBZ`
`01B8vd33LzZcm1aDulmBvWb5cy6WvCVWRPRBA0QADgMcCGA1UDU0QOMMBG`
`MWCSAGG-S4EIEM0CqBIYOWHAGECC5G4QAFWIBMCMCDMGgCS5GAOUFBWBCWGJJAK`
`MWCSAGG8F6BgF80QYHA6LY9jDAWRCY29Cl22AuXnYvXp2429LTS29Y21GAHDW/MD00`
`XWXJX22221J3Y3BMSkCMGGCS4Q4E+F43C2Y30JASN29WMMT2YMAQQS51B3`
`B1LZXNraAAABJ4P5Vtttm1Qk5145nLeucLebCf14xPI1786BWXlKIEr4Novul13`
`WF0FIW+/A80WRYYJML2Q0V1V4XN25jpn6CVY9AASQHMII-3Ujesy7vtd11IX`
`n`

---

--- 证书---

将此复制并解析到名为 `server.crt` 的文件中，该文件必须位于
`/etc/conf/ssl.crt` 目录下，并重启你的服务器：

假设你的网站之前运行良好，现在可以通过在 Web 地址中添加 `https://` 来以安全的方式访问它。如果你之前是通过 `www.acmemarina.com` 访问网站的，现在可以通过以下地址进行安全访问：`https://www.acmemarina.com`。

# 创建自签名证书

生成并运行自签名 SSL 证书比拥有签名证书要简单得多。
在 Fedora 系统上生成自签名 SSL 证书，请执行以下操作：

- 1. 创建你自己的服务器密钥：

```bash
# cd /etc/httpd/conf

# rm ssl.key/server.key ssl.crt/server.crt
```

- 2. 创建自签名证书：

```bash
# make genkey
```

- 3. 输入以下内容创建自签名证书：

```bash
# make testcert

umask 77 : \/usr/bin/openssl req -new -key /etc/httpd/conf/ssl.key/server.key -x509 -days 365 -out /etc/httpd/conf/ssl.key/server.crt
```

# 第三部分 学习系统管理技能

此时，是时候向证书中添加一些标识信息了。在在此之前，你必须解锁你创建的私钥。通过这样做，你将输入之前输入过的密码。然后按照此示例步骤操作：

你即将输入将整合到你的证书请求中的信息。
你即将输入的内容被称为区分名称（Distinguished Name，简称 DN）。
有很多字段，但你可以留某些字段为空，这些字段会有默认值。
如果你输入 `.`，该字段将留空。

国家名称（两位字母代码） [GB]:US
州或省份名称（全称） [Berkshire]:Ohio
市辖名称（例如，城市） [Newbury]: Cincinnati
组织名称（例如，公司） [My Company Ltd]:Industrial Press, Inc.
组织单位名称（例如，部门） [:IT
通用名称（例如，你的名称或服务器主机名） []:www.industrialpress.com
邮箱地址 [:webmaster@industrialpress.com

此示例中的生成过程会将所有文件存放在正确的文件夹中。你只需要重新启动你的 Web 服务器，并在 URL 前将 `http` 替换为 `https`。不要忘记你的 Web 浏览器会收到证书验证消息，你可以安全地忽略它。

# 重启你的 Web 服务器

现在你已经注意到，你的 Web 服务器每次启动时都需要你输入证书密码。这是为了防止他人入侵你的服务器并窃取私钥。如果发生这种情况，你可以放心，私钥是一团乱码。破解者将无法利用它。如果没有这种保护，破解者可以获取你的私钥并轻易伪装成你，在所有情况下看起来都是合法的。

如果你实在无法忍受每次 Web 服务器启动时都要输入密码，并且愿意接受增加的风险，你可以移除私钥上的密码加密。
只需执行以下操作：

```bash
# cd /etc/httpd/conf/ssl.key

# /usr/bin/openssl rsa -in server.key -out server.key
```
