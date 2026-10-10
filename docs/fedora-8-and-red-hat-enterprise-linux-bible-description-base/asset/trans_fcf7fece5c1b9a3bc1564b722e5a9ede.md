
## 对称加密

*对称加密*，又称*私钥*加密，使用同一个密钥来加密和解密消息。由于安全密钥交换的复杂性，这种方法通常不适用于保护将由第三方使用的数据。对称加密通常适用于加密供自己使用目的的数据。

对称加密的一个经典应用是个人密码保管箱。任何使用过互联网一段时间的人都会积累大量用于访问各种站点和资源的用户名和密码。个人密码保管箱允许你以加密形式存储这些访问信息。最终结果是，你只需要记住一个密码就可以解锁你所有的访问信息。

直到最近，美国政府一直标准化使用一种名为 DES（数据加密标准）的对称加密算法来保护重要信息。由于没有直接破解 DES 加密数据的方法，要在没有密码的情况下解密 DES 加密数据，你必须使用难以想象的大量计算能力来尝试猜测密码。这也称为解密的*暴力*方法。

随着个人计算能力近乎呈指数级增长，DES 算法不得不被淘汰。取而代之的是，经过漫长而有趣的搜寻，美国政府接受了 Rijndael 算法，并将其称为 AES（高级加密标准）。虽然 AES 算法也容易受到暴力攻击，但破解它所需的计算能力比 DES 算法显著更多。

如需了解 AES 的更多信息，包括该算法的命令行实现，你可以访问 `http://aesencrypt.sourceforge.net/`。

## 公钥加密

*公钥加密*不受密钥分发问题的困扰，这就是为什么它是安全互联网通信的首选加密方法。此方法使用两个密钥，一个用于加密消息，另一个用于解密消息。用于加密消息的密钥被称为公钥，因为它向所有人公开可见。用于解密消息的密钥是私钥，并被严格保密。整个过程的工作方式如下：

想象一下，你想使用公钥加密给我发送一条安全消息。我们需要做的是：

1. 我必须拥有公钥和私钥对。根据情况，我可能会自己生成密钥（使用专用软件），或者从密钥机构获取密钥。
2. 你想给我发送一条消息，所以你首先查找我的公钥（或者更准确地说，是你使用的软件查找它）。
3. 你使用公钥对消息进行加密。此时，消息只能使用私钥解密（公钥不能用于解密消息）。
4. 我收到消息并使用我的私钥进行解密。

## 安全套接层

公钥加密的一个经典实现是通过安全套接层（SSL）通信。这项技术使你可以安全地将信用卡信息提交给在线商家。SSL 加密会话的元素如下：

- 支持 SSL 的 Web 浏览器（Firefox、Mozilla、Internet Explorer、Opera、Konqueror 等）
- 支持 SSL 的 Web 服务器（Apache）
- SSL 证书

为了发起 SSL 会话，Web 浏览器首先通过端口 443 与 Web 服务器建立联系，该端口也被称为 HTTPS 端口（HyperText Transfer Protocol Secure）。在两台机器之间建立套接字连接后，会发生以下情况：

1. 服务器向浏览器发送其 SSL 证书。
2. 浏览器通过 SSL 证书验证服务器的身份。
3. 浏览器生成一个对称加密密钥。
4. 浏览器使用 SSL 证书加密该对称加密密钥。
5. 浏览器将加密后的密钥发送给服务器。
6. 服务器使用其私钥（对应于公钥 SSL 证书）解密对称密钥。
7. 浏览器和服务器现在可以基于对对称密钥的共同了解来加密和解密流量。

现在可以进行安全的数据交换了。

## 创建 SSL 证书

为了能够使用 SSL 证书进行安全的 HTTP 数据交换，你必须拥有一台支持 SSL 的 Web 服务器。Fedora 和 RHEL 自带的 Apache Web 服务器（httpd 软件包）支持 SSL。以下是你需要为自己的 Apache Web 服务器创建 SSL 证书所需的一些文件：

- /etc/httpd/conf/httpd.conf — Web 服务器配置文件
- /etc/pki/tls/certs/Makefile — 证书构建脚本
- /etc/httpd/conf.d/ssl.conf — 主要 Web 服务器 SSL 配置文件

既然你已经熟悉了基本组件，让我们来看看用于创建 SSL 证书的工具：

```
# cd /etc/pki/tls/certs
# make
```

此 makefile 允许你创建：

- 公钥/私钥对
- SSL 证书签名请求（CSRs）
- 自签名的 SSL 测试证书

要创建密钥对，运行 `make SOMETHING.key`。
要创建 CSR，运行 `make SOMETHING.csr`。
要创建测试证书，运行 `make SOMETHING.crt`。
要在一个文件中创建密钥和测试证书，运行 `make SOMETHING.pem`。

要创建用于 Apache 的密钥，运行 `make genkey`。
要创建用于 Apache 的 CSR，运行 `make certreq`。
要创建用于 Apache 的测试证书，运行 `make testcert`。

要创建序列号不为零的测试证书，添加 `SERIAL=num`。

示例：

```
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

make 命令利用 Makefile 来创建 SSL 证书。（make 命令用于 C 和 C++ 编程中的各种软件任务。）如果不带任何参数，make 命令只会打印上面列出的信息。以下定义了你可以传给 make 的每个参数：

- make server.key—创建通用的公钥/私钥对。
- make server.csr—生成通用的 SSL 证书服务请求。
- make server.crt—生成通用的 SSL 测试证书。
- make stunnel.pem—生成通用的 SSL 测试证书，但将私钥放在与 SSL 测试证书相同的文件中。
- make genkey—与 make server.key 相同，只是将密钥放置在 ssl.key 目录中。
- make certreq—与 make server.csr 相同，只是将证书服务请求放置在 ssl.csr 目录中。
- make testcert—与 make server.crt 相同，只是将测试证书放置在 ssl.crt 目录中。
- make server.crt SERIAL=1—使用非零序列号的密钥生成上述密钥。

## 使用第三方证书签发者

在现实世界中，我认识你是因为我认得你的脸、你的声音和你的举止。在互联网上，我无法看到这些东西，必须依赖可信赖的第三方来担保你的身份。为了确保证书不可篡改，在证书颁发时必须由可信赖的第三方进行签名，并且在每次最终用户利用你的安全站点加载它时都要进行验证。以下是可信赖的第三方证书签发者列表：

- **GlobalSign** — www.globalsign.net/
- **GeoTrust** — www.geotrust.com/
- **VeriSign** — www.verisign.com/
- **RapidSSL.com** — www.rapidssl.com/
- **Thawte** — www.thawte.com/
- **Entrust** — www.entrust.com/
- **ipscA** — www.ipscA.com/
- **COMODO Group** — www.comodogroup.com/

> **注意：** 由于证书行业的流动性，当你阅读本文时，其中一些公司可能已不再经营，而另一些公司可能已经成立。要获取更当前的证书颁发机构列表，请从 Mozilla Firefox 浏览器中选择“编辑”⇒“首选项”。在出现的首选项窗口中，选择“高级”⇒“加密”⇒“查看证书”。在出现的证书管理器窗口中，参阅“颁发机构”选项卡，查看你收到证书的证书颁发机构。

这些证书颁发机构中的每一个都嵌入到世界上几乎每个 Web 浏览器中的一段加密代码。这段加密代码使 Web 浏览器能够确定 SSL 证书是否真实。如果没有这种验证，黑客生成自己的证书并欺骗人们认为他们正在向可靠来源提供敏感信息将变得轻而易举。

未经验证的证书被称为*自签名证书*。如果你遇到一个身份未经可信赖第三方验证的网站，你的 Web 浏览器将显示类似图 14-3 中所示的消息。
