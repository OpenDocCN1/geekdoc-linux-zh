
`openssl req -text -in ssl.csr/server.csr`

您将看到类似于列表 45-1 所示的结果。

![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_360_0.png)

# 创建证书签名请求

## 列表 45-1：检查证书签名请求

证书请求：

```
数据:
版本: 0 (0x0)
Subject: CS, ST=Virginia, L=Anytown, O=TrixWare, OU=Cosmology.
CN=www.trixware.com/email@newdoo@trixware.com
公钥信息:
公算法: rsaEncryption
RSA 公钥 (1024 bit):

00:ac:fd:51:b4:b0:42:80:ec:f7:53:54:61:b8:
13:fe:45:91:7c:d5:a5:28:23:68:a3:d1:b4:
05:e1:77:57:21:26:b3:a5:b6:50:ca:81:2e:55:
e22:e5:39:64:e3:65:d8:b0:d7:45:53:f8:91:
39:28:b5:c4:e2:a3:29:c6:e3:a5:17:a8:99:72:
32:d6:40:70:32:86:10:a6:f0:ac:f9:66:e9:64:
c1:a0:dc:ca:77:61:01:4a:b3:5f:0d:15:1d:
6a:0b9:ca:e2:c8:dd:ac:93:04:e3:44:3e:1d:f8:
c3:ef:ca:30:c0:le6:f6:a39

属性:
a00:

Signature: md5WithRSAEncryption

04:e1:60:d3:46:b9:22:f9:e7:f7:a1:e2:24:21:33:89
7f:ba:67:79:34:9c:9e:23:f0:74:96:0a:bf:57:99:6d:08
0e:ad:a4:d8:a0:5c:f3:42:f3:43:a2:f4:55:24:c7:4b:02:55
18:de:b8:24:12:a9:91:d0:be:f1:63:62:d8:73:95:62:c9:f8
6a:ca:c6:34:f7:67:02:34:d3:dc:b6:35:99:c7:96:37:9
29:b4:da6:c5:de6:69:95:d3:e3:e5:b8:fd:f2:dc:a4:b6:55
f66:f4:e1:c2:f0:13:13:be:b6:f7:bb:b9:a4:29:04

--- CERTIFICATE REQUEST ---

MI3BDSUCAQAWGZScCAJQBNBWAYATITVMMSQ0QODYQOWWIYTMETBEMGAI16
B8XMXJYV6XZYT2TDBBEMGAI6KUHGEPL22FVYZTZESMBAUECKQJ0Q29Z
B9b2d8b5s9w6y902XQO33D3XJ33311112225555222222221111111999000000QQQQQ111111111111YY777777711111111111111111111111111111111111111111111141444555505550055555555555555555555551115111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111

01PenKEMB5/aW0WHYgbbnk45/j2rdK07U+Hf7D088b5wPG7tCAWAAAMQ
CSQ1G3B3EBAA4BRA4L01LAUS78H1E19X9S00zJsPr5ASBAQ4v5l17c4
AgTpWvP8806JK/FkX05VR22+00SSZQ8CnNHhtYZl1/Mpqgt
--- CERTIFICATE REQUEST ---
```

您可以看到证书包含了所需的所有信息。`CSR`使用你的私钥进行数字签名，`CA`使用`CSR`中包含的密钥进行验证。将`CSR`（`/etc/httpd/conf/ssl/server.csr`）发送到你选择的证书机构。

## 技巧：使用 SSL 证书保护你的 Apache 服务器

当你收到最终证书时，只需将其复制到`/etc/httpd/conf/server.crt`并重启你的`Apache`服务器。`Fedora`会在它期望的地方找到它。要查看证书状态，重启你的`Apache`服务器：

```
# /sbin/service httpd restart
Stopping httpd: [OK]
Starting httpd: [OK]
```

出于安全原因，你的部分私钥文件是加密的。

## 创建自签名证书

创建自签名证书与创建`CSR`一样简单，但你最终得到的是证书而不是请求。如果你没有使用`Fedora`，可以使用证书和密钥模块生成`SSL`证书。为了读取它们，你必须提供短语。

```
localhost.localdomain:443
输入短语：
```

以下是使用`Fedora`创建自签名证书的步骤：

- 打开终端窗口并使用`su`命令获取超级用户权限。
- 进入`/etc/httpd/conf`目录：
  `$ cd /etc/httpd/conf`
- 输入`makecert`并按回车。系统提示输入私钥密码。`SSL`会提示你在创建`CSR`时提供的信息（位置、组织等）。依次回答每个问题。注意`Apache`请求保护你私钥的短语。
- 现在，打开浏览器并连接`https://127.0.0.1`。
- 注意`URL`是`https`而不是`http`。你已经创建了自签名证书并将其安装在`Apache`服务器上。由于用户遇到此证书时会收到警告，所以给他们一个简单的警告是好的。查看侧边栏“Mozilla 遇到自签名证书”了解其工作原理。创建自签名证书并将其保存在`/etc/httpd/conf/server.crt`。

## 当 Mozilla 遇到自签名证书

自签名证书是不可信的。当你访问带有自签名证书的网站时，你会收到`Mozilla`的警告，询问你是否知道以及证书对你是否足够（见下图）。从这里开始按照以下步骤检查证书：

你会发现发行者（`issuer`）和主体（`subject`）是相同的——这就是自签名证书。要在命令行验证证书，使用以下命令：

```
# openssl x509 -in server.crt -text
```

## 使用 openssl 创建签名机构

如果你要在组织内部签名证书，请使用`openssl`创建签名机构（`CA`）。如果你想向组织内人员分发受信任软件，自己的`CA`将非常有用。此外，如果你想保护公司内部的内容。

`CA`有三个职责：

- 验证身份
- 签名请求
- 维护签名证书数据库

`openssl`带有一个可以处理你站点最后两个职责的程序。适用于站点的身份验证方法：如果你为公司创建`CA`，身份证可能就足够。

## 创建证书机构

要创建`CA`，请遵循以下步骤：

- 打开终端窗口并使用`su -`命令获取超级权限：
  `$ su`
  `Password:`
- 如果你使用的是`Fedora`或`SuSE`，进入包含`CA` shell脚本的目录：
  `# cd /usr/share/ssl/misc`
  如果你使用的是`Mandrake`：
  `# cd /usr/lib/ssl/misc`
- 使用以下命令创建`CA`架构：
  `# ./CA -newca`

![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_363_0.png)

点击检查证书（`Examine certificate`）按钮查看证书详情（下图）：

点击详情（`Details`）选项卡，并在证书字段中高亮发行者（`Issuer`）行。在字段值中，你会看到证书发行者的名称和电子邮件地址。你可以自己判断此人是否可靠。

## 技巧 45：使用 SSL 证书保护你的 Apache 服务器

在`Mandrake`和`SuSE`系统上，此命令为：

`./CA.sh -newca`

- 打开终端窗口并使用`su -`命令获取超级用户权限：
  `$ su -`
  `Password:`
- `CA`脚本会问你一系列问题，其中大多数现在应该已经熟悉了。创建`CA`架构的第一步是创建一个新的自签名证书。系统提示输入现有证书：

  `CA 证书文件名`

- 进入包含`CA` shell脚本的目录：
  `$ cd /usr/share/ssl/misc`
  （或创建）
- 输入以下命令：
  `$ openssl ca -policy anything -in filename.csr -out filename.crt`
- 直接按回车即可创建新证书。
- 输入保护`CA`私钥的短语：

  `生成 1024 位 RSA 私钥`
  `验证新的 RSA 私钥；完成`
  `随机数位数: 1024`
