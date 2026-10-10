
为了能够使用 SSL 证书进行安全的 HTTP 数据交换，你必须拥有一个支持 SSL 的 Web 服务器。随 Fedora 提供的 Apache Web 服务器（`httpd` 包）是支持 SSL 的。以下是你需要创建自己的 Apache Web 服务器 SSL 证书所需的某些文件：

- `/etc/httpd/conf/httpd.conf` — Web 服务器配置文件
- `/etc/pki/tls/certs/Makefile` — 证书构建脚本
- `/etc/httpd/conf.d/ssl.conf` — 主要 Web 服务器 SSL 配置文件（来自 `mod_ssl` 包）

既然你已经熟悉了基本组件，下面看一下用于创建 SSL 证书的工具：

```
# cd /etc/pki/tls/certs
# make
```

此 `makefile` 允许你创建：

- 公钥/私钥对
- SSL 证书签名请求（CSRs）
- 自签名 SSL 测试证书

要创建密钥对，运行 "`make SOMETHING.key`"。

要创建 CSR，运行 "`make SOMETHING.csr`"。

要创建测试证书，运行 "`make SOMETHING.crt`"。

要在一个文件中创建密钥和测试证书，运行 "`make SOMETHING.pem`"。

要为 Apache 创建密钥，运行 "`make genkey`"。

要为 Apache 创建 CSR，运行 "`make certreq`"。

要为 Apache 创建测试证书，运行 "`make testcert`"。

要创建序列号不为零的测试证书，请添加 `SERIAL=num`

```
Examples:
make server.key
make server.csr
make server.crt
make stunnel.pem
make genkey
make certreq
make testcert
make server.crt SERIAL=1
make stunnel.pem SERIAL=2
make testcert SERIAL=3
```

`make` 命令利用 `Makefile` 来创建 SSL 证书。（`make` 命令用于 C 和 C++ 编程中的多种软件任务。）不带任何参数时，`make` 命令仅打印上述列出的信息。以下定义了你可以给 `make` 的每个参数：

- `make server.key` — 创建通用的公钥/私钥对。
- `make server.csr` — 生成通用的 SSL 证书服务请求。
- `make server.crt` — 生成通用的 SSL 测试证书。
- `make stunnel.pem` — 生成通用的 SSL 测试证书，但将私钥放在与 SSL 测试证书相同的文件中。
- `make genkey` — 与 `make server.key` 相同，但它将密钥放置在 `ssl.key` 目录中。
- `make certreq` — 与 `make server.csr` 相同，但它将证书服务请求放置在 `ssl.csr` 目录中。
- `make testcert` — 与 `make server.crt` 相同，但它将测试证书放置在 `ssl.crt` 目录中。
- `make server.crt SERIAL=1` — 使用非零序列号生成上述提到的密钥。

### 使用第三方证书签名者

在现实世界中，我通过认识你的脸、声音和举止来知道你是谁。在互联网上，我看不到这些东西，必须依赖一个受信任的第三方来证明你的身份。为了确保证书不可篡改，它在发行时必须由受信任的第三方签名，并且每当最终用户加载你的安全网站时都要进行验证。以下是受信任的第三方证书签名者列表：

- GlobalSign — `www.globalsign.com/`
- GeoTrust — `www.geotrust.com/`
- VeriSign — `www.verisign.com/`

# 第570页 第三部分：管理 Fedora

- `RapidSSL.com` — `www.rapidssl.com/`
- `Thawte` — `www.thawte.com/`
- `Entrust` — `www.entrust.com/`
- `ipcsCA` — `www.ipcsca.com/`
- `COMODO Group` — `www.comodogroup.com/`

> **注意：** 由于证书行业的流动性，当您阅读此书时，其中一些公司可能已不再经营，而另一些公司可能才刚成立。要获取更最新的证书颁发机构（CA）列表，请在您的 Mozilla Firefox 浏览器中选择“编辑” -> “首选项”。在出现的首选项窗口中，选择“高级” -> “加密” -> “查看证书”。在出现的证书管理器窗口中，参考“权威机构”选项卡，查看您已接收证书的证书颁发机构。建议您为公开访问的资源使用知名证书颁发机构。

这些证书颁发机构（CA）中的每一个都将一段加密代码嵌入到了世界上几乎每一个 Web 浏览器中。这段加密代码使 Web 浏览器能够判断 SSL 证书是否真实有效。如果没有这种验证，黑客生成自己的证书并欺骗人们认为他们正在向可信赖的来源提供敏感信息将变得极其简单。

未被验证的证书称为自签名证书。如果您遇到一个身份未经验证的可信第三方认证的站点，您的 Web 浏览器将显示警告消息。

这并不一定意味着您遇到了非法、不道德或令人发胖的内容。许多站点选择使用自签名证书，并非因为她们想欺骗您，而是因为可能没有理由验证证书的真实所有者，而且她们不想支付验证证书的费用。使用自签名证书的一些原因包括：

- **Web 站点不接受输入** — 在这种情况下，作为最终用户的您没有什么需要担心的。因为没有人在试图窃取您的信息，您也没有提供任何信息。大多数情况下，这样做只是为了确保从服务器到您的 Web 传输的安全性。数据本身可能并不敏感，但作为一个好的网络公民，该站点启用了传输安全功能，以防止第三方嗅探流量。
- **Web 站点服务于少量客户** — 如果您运行的是一个拥有非常有限客户群的 Web 站点，例如应用服务提供商（ASP），您可以简单地通知用户您没有证书签名者，他们可以浏览证书信息并通过电话或当面与您进行验证。
- **测试** — 如果您只是在测试新的 Web 站点或基于 Web 的应用程序，支付 SSL 证书的费用是没有意义的。在您准备正式启用之前，请使用自签名证书。

#### 创建证书服务请求

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

> **注意**：您应确保提供的主机名（本例中为 www.acmemarina.com）与您的 Web 站点的实际主机名匹配。如果名称不匹配，用户将看到看似证书错误的信息。此外，如果您为密钥输入密码，每次重启 `httpd` 时都需要输入该密码。

要完成此过程，您会被要求是否希望向证书添加任何额外属性。除非您有理由提供更多信息，否则应在以下每个提示处直接按 Enter 键以将其留空。

```bash
Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password [] :
An optional company name [] :
```

#### 获取 CSR 签名

创建 CSR 后，您需要将其发送给签名机构进行验证。此过程的第一步是选择一个签名机构。每个签名机构的协议、价格和产品各不相同。查看本章前面“使用第三方证书签名者”部分列出的每个签名机构，以确定哪个最适合您。签名机构在以下方面存在差异：

- 信誉和稳定性
- 定价
- 浏览器识别度
- 保修
- 支持
- 证书强度

选定证书签名者后，您必须完成一些验证步骤。每个签名者验证身份和证书信息的方法各不相同。有些要求您传真公司章程，而有些则要求公司负责人可供验证操作员联系。在过程的某个阶段，您将被要求将创建的 CSR 内容复制并粘贴到签名者的 Web 表单中。
