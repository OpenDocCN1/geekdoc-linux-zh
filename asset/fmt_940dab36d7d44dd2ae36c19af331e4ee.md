
## 基本组件

- `httpd.conf` — Web 服务器配置文件。
- `Makefile` — 证书构建脚本。
- `ssl.crl` — 证书吊销列表目录。
- `ssl.crt` — SSL 证书目录。
- `ssl.csr` — 证书服务请求目录。
- `ssl.key` — SSL 证书私钥目录。
- `ssl.prm` — SSL 证书参数。
- `ssl.conf` — 主要 Web 服务器 SSL 配置文件。

现在，既然你已熟悉基本组件，请查看用于创建 SSL 证书的工具：

```bash
# cd /etc/httpd/conf
# make
```

此 `Makefile` 允许你创建：

- 公钥/私钥对
- SSL 证书签名请求（CSRs）
- 自签名 SSL 测试证书

要创建密钥对，运行 `make SOMETHING.key`。

要创建 CSR，运行 `make SOMETHING.csr`。

要创建测试证书，运行 `make SOMETHING.crt`。

要在一个文件中创建密钥和测试证书，运行 `make SOMETHING.pem`。

要为 Apache 创建密钥，运行 `make genkey`。

要为 Apache 创建 CSR，运行 `make certreq`。

要为 Apache 创建测试证书，运行 `make testcert`。

示例：

```bash
make server.key
make server.csr
make server.crt
make stunnel.pem
make genkey
make certreq
make testcert
```

`make` 命令利用 `Makefile` 创建 SSL 证书。如果不带任何参数，`make` 命令仅打印上述信息。以下定义了你可以给 `make` 的每个参数：

- `make server.key` — 创建通用的公钥/私钥对。
- `make server.csr` — 生成通用的 SSL 证书服务请求。
- `make server.crt` — 生成通用的 SSL 测试证书。
- `make stunnel.pem` — 生成通用的 SSL 测试证书，但将私钥放在与 SSL 测试证书相同的文件中。
- `make genkey` — 与 `make server.key` 相同，但将密钥放置在 `.ssl.key` 目录中。
- `make certreq` — 与 `make server.csr` 相同，但将证书服务请求放置在 `.ssl.csr` 目录中。
- `make testcert` — 与 `make server.crt` 相同，但将测试证书放置在 `.ssl.crt` 目录中。

### 使用第三方证书签署机构

在现实世界中，我认识你，因为我辨认得出你的脸、声音和举止。在互联网上，我无法看到这些，必须依赖受信任的第三方来证明你的身份。为确保证书不可篡改，在证书颁发时，必须由受信任的第三方对其进行签名；并且每次最终用户利用你的安全站点加载证书时，都要进行验证。以下是受信任的第三方证书签署机构列表：

- `GlobalSign` — http://www.globalsign.net/
- `GeoTrust` — http://www.geotrust.com/
- `VeriSign` — http://www.verisign.com/
- `FreeSSL` — http://www.freesll.com/
- `Thawte` — http://www.thawte.com/
- `En Trust` — http://www.entrust.com/
- `ipscA` — http://www.ipsca.com/
- `COMODO Group` — http://www.comodogroup.com/

注意：由于证书业务的动态变化性质，当你阅读本文时，其中一些公司可能已不再营业，而其他一些公司可能已经成立。要获取更当前的证书颁发机构列表，请使用 Mozilla Firefox 浏览器，选择“编辑” > “首选项”。在出现的首选项窗口中，选择“高级” > “管理证书”。在出现的证书管理器窗口中，参阅“颁发机构”选项卡，查看你已从中收到证书的证书颁发机构。

这些证书颁发机构中的每一个都在世界上几乎每个 Web 浏览器中都嵌入了一段加密代码。这段加密代码使 Web 浏览器能够判断 SSL 证书是否真实。如果没有这种验证，攻击者将可以轻易生成自己的证书，并欺骗人们以为他们正在向信誉良好的来源提供敏感信息。

未经验证的证书被称为 `自签名证书`。如果你访问到一个身份未受可信第三方认证的站点，你的 Web 浏览器将显示类似于图 14-3 所示的消息。

![](img/b22364e57409c2481ba806e4e6b9309c_586_0.png)

图 14-3：当站点未经验证时，弹出窗口会发出警报。

这并不一定意味着你遇到了什么非法、不道德或令人发胖的东西。许多站点选择使用 `自签名` 证书，并非因为它们试图对你耍花招，而是因为可能没有理由验证证书的真实所有者，而且它们不想支付获得证书验证的成本。使用 `自签名` 证书的一些原因包括：

- `该 Web 站点不接受任何输入` — 在这种情况下，作为最终用户的你无需担心。没有人试图窃取你的信息，因为你没有提供任何信息。大多数情况下，这样做只是为了保护从服务器到你这边的 Web 传输安全。数据本身可能并不敏感，但作为一个好的网络公民，该站点已启用安全传输，以防止第三方嗅探流量。
- `该 Web 站点服务于少量客户群` — 如果你运营一个客户群非常有限的 Web 站点，例如应用服务提供商（ASP），你可以简单地通知用户你没有证书签名者，他们可以浏览证书 `信息` 并通过电话或亲自与你进行验证。
- `测试` — 如果你只是在测试新的 Web 站点或基于 Web 的应用程序，为 SSL 证书付费是没有意义的。在你准备上线之前，请使用 `自签名` 证书。

### 创建证书服务请求

为了创建由第三方验证的 SSL 证书，你必须首先从证书服务请求（CSR）开始。要创建 CSR，请在你的 Web 服务器上执行以下操作：

```bash
# cd /etc/httpd/conf
```

```bash
# make certreq
umask 77 ; /usr/bin/openssl genrsa -des3 1024 > /etc/httpd/conf/ssl.key/server.key
```

现在你会被要求输入密码以保护你的私钥。该密码长度应至少为 8 个字符，并且不应是字典中的单词，也不应包含数字或标点符号。为了阻止他人偷看你的密码，你输入的字符不会显示在屏幕上。

```text
Enter pass phrase:
```

再次输入密码以进行验证。

```text
Verifying - Enter pass phrase:
```

证书生成过程现在开始。

此时，是时候开始向证书添加一些识别信息，稍后第三方将验证这些内容。在此之前，你必须解锁刚才创建的私钥。通过输入上面输入的密码来执行此操作。然后按照提示输入信息。以下是一个向证书添加信息的会话示例：

```text
Enter pass phrase for /etc/httpd/conf/ssl.key/server.key:
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called
a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [GB]:US
State or Province Name (full name) [Berkshire]: Connecticut
Locality Name (eg, city) [Newbury]: Mystic
Organization Name (eg, company) [My Company Ltd]:Acme Marina, Inc.
Organizational Unit Name (eg, section) []:InfoTech
Common Name (eg, your name or your server's hostname)
[]:www.acmemarina.com
Email Address []: webmaster@acmemarina.com
```
