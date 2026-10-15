
## SSL 握手流程

- 1. 服务器将其 SSL 证书发送给浏览器。
- 2. 浏览器通过 SSL 证书验证服务器的身份。
- 3. 浏览器生成一个对称加密密钥。
- 4. 浏览器使用 SSL 证书加密对称加密密钥。
- 5. 服务器将加密后的密钥发送给服务器。
- 6. 服务器使用其与公证书对应的私钥解密对称密钥。

浏览器和服务器现在可以根据对称密钥的共同知识来加密和解密流量。安全的数据交换现在可以进行。

## 创建 SSL 证书

为了用于安全的 HTTP 数据交换创建自己的 SSL 证书，你必须首先有一个支持 SSL 的 Web 服务器。随 Fedora 和其他 Linux 系统自带的 Apache Web 服务器（`httpd` 软件包）支持 SSL 的。创建 SSL 证书的以下程序是在包含 `httpd-2.2.3-5` 软件包中 Apache 的 Fedora 系统上完成的。对于其他 Linux 系统上的 Apache，此过程可能有所不同。

## 第二部分 运行演示

一旦你准备好了服务器，你就应该熟悉 SSL 证书的重要服务器端组件：

```
# ls -l /etc/httpd/conf
-rw-r--r-- 1 root root 36010 Jul 14 15:45 httpd.conf
lrwxrxrwx 1 root root 37 Aug 12 23:45 Makefile ->
    ../../usr/ssl/certs/Makefile
drwx------ 2 root root 4096 Aug 12 23:45 ssl.crl
drwx------ 2 root root 4096 Aug 12 23:45 ssl.crt
drwx------ 2 root root 4096 Jul 14 15:45 ssl.csr
drwx------ 2 root root 4096 Aug 12 23:45 ssl.key
drwx------ 2 root root 4096 Jul 14 15:45 ssl.prm
```

`/etc/httpd/conf` 和 `/etc/httpd/conf.d` 目录包含了创建 SSL 证书所需的所有组件。每个组件定义如下：

- `httpd-conf`— Web 服务器配置文件。
- `Makefile`— 证书脚本。
- `ssl.crl`— 证书吊销列表目录。
- `ssl.csr`— 证书签名请求目录。
- `ssl.key`— 证书私钥目录。
- `ssl.prm`— SSL 证书参数。
- `ssl-conf`— 主要 Web 服务器 SSL 配置文件。

现在你已经熟悉了基础组件，请查看用于创建 SSL 证书的工具：

```
# cd /etc/httpd/conf
# make
这允许你创建：
- 公钥/私钥对
- SSL 证书签名请求 (CSR)
- 自签名 SSL 测试证书
```

创建密钥对请运行 `make SOMETHING.key`。创建 CSR 请运行 `make SOMETHING.csr`。创建测试证书请运行 `make SOMETHING.crt`。在一个文件中创建密钥和测试证书请运行 `make SOMETHING.pem`。

创建用于 Apache 的密钥运行 `make genkey`。创建用于 Apache 的 CSR 运行 `make certreq`。创建用于 Apache 的测试证书运行 `make testcert`。

### 运行演示

注意

由于证书业务的流动性，当你阅读此内容时，某些公司可能仍在运营，而另一些可能已经不存在。要获取最新的证书颁发机构列表，请从你的 Mozilla Firefox 浏览器中选择“编辑首选项”。在出现的设置窗口中，选择“高级”->“管理证书”。在打开的证书管理器中，参考“机构”（Authorities）选项卡查看你从哪些机构接收了证书。

这些证书颁发机构都已经在全球几乎每一个 Web 浏览器中嵌入了一段加密代码。这段加密代码允许 Web 浏览器判断 SSL 证书是否真实。如果没有这种验证，黑客很容易生成自己的证书，并欺骗人们认为他们正在向信誉良好的来源提供敏感信息。

未验证的证书被称为自签名证书（self-signed certificates）。如果你遇到一个未经过受信任第三方身份验证的网站，你的 Web 浏览器将显示与图 6.2 所示类似的消息。

![](img/fa18693414a802b12c8add5f8c4be910_265_0.png)

这并不意味着你一定遇到了任何非法、不道德或肥胖的事情。许多网站选择使用自签名证书，并不是因为它们试图欺骗你，而是因为可能没有理由验证证书的真实所有者，并且不想支付验证证书的费用。使用自签名证书的一些理由包括：

- 网站不接受任何输入。在这种情况下，作为终端用户，无需担心。没有人试图窃取你的信息，因为你没有提供任何信息。大多数情况下，这仅仅是为了确保从服务器到你的 Web 传输安全。数据本身可能并不敏感，但作为一个良好的邻居，该网站允许你加密传输，以防止第三方嗅探流量。
- 网站面向少数客户。如果你运行的是一个客户群非常有限的网站（例如应用程序服务供应商），你可以直接告知用户你没有证书签名者。他们可以浏览证书信息并通过电话或面对面与你进行验证。
- 测试。如果你只是在测试一个新的网站或基于 Web 的应用程序，那么为 SSL 证书付费没有意义。在准备好上线之前，请使用自签名证书。

## 保护 Linux

### 创建证书服务请求

要从 Fedora 系统创建第三方验证的 SSL 证书，你必须首先从证书服务请求（CSR）开始。要创建 CSR，请在你的 Web 服务器上执行以下操作：

```bash
# cd /etc/httpd/conf
# make certreq
umask 77 : \
/usr/bin/openssl genrsa rsa -des3 1024 > /etc/httpd/conf/ssl.key/server.key
```

现在你会被要求输入密码来保护你的私钥。此密码至少应该是八个字符，且不应该是字典单词，也不包含数字或标点符号。你输入的字符不会显示在屏幕上，以防止有人窥视你的密码。

输入短语（pass phrase）：

再次输入密码以验证。

验证 - 输入短语（pass phrase）：

证书的生成过程现在开始。

此时，是时候开始为第三方来源将验证的证书添加一些标识信息了。在此之前，你必须解锁刚刚创建的私钥。只需通过输入你之前为短语输入的密码。然后按照提示输入信息。这里是为证书添加信息的会话示例：

为 `/etc/httpd/conf/ssl.key/server.key` 输入短语：

你将被要求输入将包含在证书请求中的信息。

你将要输入的内容被称为

区分名称（Distinguished Name，简称 DN）。

字段很多，但你可以留空。

某些字段将有一个默认值，

如果你输入 '.'，则该字段将留空。

-----

国家名称（两位字母代码）[GB]:US

州或省名称（全称）[Berkshire]:Connecticut

地区名称（例如，城市）[Newbury]:Mystic

组织名称（例如，公司）[My Company]:Acme Marina, Inc.

组织单元名称[:InfoTech

通用名称（例如，你的名称或服务器主机） []:www.acemarina.com

电子邮件 []:webmaster@acemarina.com

要完成过程，系统将询问你是否想为证书添加任何额外属性。除非你有理由提供更多信息，否则你应该在每个提示处直接按回车键留空。

请输入随证书请求的“额外”属性

挑战密码（challenge password）[];

可选公司名称 []:

### 签名 CSR

一旦创建了 CSR，你就将其发送给签名机构进行验证。此过程的第一步是选择一个签名机构。每个签名机构都有不同的优惠方案、产品和价格。请查看本章前面“使用第三方证书签名者”中列出的每个签名机构，以确定最适合你的。以下是签名机构存在差异领域：

- 信誉与稳定性
- 价格
- 浏览器识别
- 质保
- 支持
- 证书强度

选择证书签名者后，你必须通过一些验证步骤。每个签名者都有不同的身份验证方法。有些需要注册证明，有些需要沟通。在过程的某个阶段，你会被要求将 CSR 内容复制并粘贴到签名者的 Web 表单中。

```bash
# /etc/httpd/conf/ssl.csr
cat server.csr
-----BEGIN CERTIFICATE REQUEST-----
MI6B6J6CCMVCAQuaBX6Awq2CAJBBGNVAVTAI1MRQYWEQGDQWIEtDb25Z0AWN1DDEPEMA06A1UEXmGTQ12mMKGADQYQKFKBY211UhlSwG5W6J6LERMAGA81UECXMISW5mb12qGZA2BgGNVAMENT3d5y211bFWY5aHmLNvbbEn
```

## 第二部分 运行

### 创建自签名证书

生成和运行自签名 SSL 证书比使用经过签名的证书要简单得多。

在 Fedora 系统上生成自签名 SSL 证书，请执行以下操作。

- 1. 删除当前存在的密钥和证书：
