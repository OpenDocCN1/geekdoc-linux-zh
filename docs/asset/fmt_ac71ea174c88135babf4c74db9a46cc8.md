
即使是经过受信任方法验证的客户端也不被允许为所有人中继邮件。身份验证身份和授权身份必须一致，才能中继邮件。要更改该行为，你需要创建自己的重写规则。自定义重写规则定义可以在`Local_check_rcpt`规则集或`Local_trust_auth`规则集中，以验证客户端是否已身份验证以及使用了什么身份验证方法完成任务。`Local_trust_auth`规则集用于修改这一事实：只有当身份与挑战/响应验证的身份相同时，Sendmail才在`Mail From:`头部中发送`AUTH`关键字。三个变量包含了可以在这些规则集中使用的身份验证信息。这些变量是：

- `(auth_type)`：此变量包含用于验证客户端的身份验证技术名称——例如，`DIGEST-MD5`。
- `(auth_authen)`：此变量包含客户端和服务器之间原始挑战/响应交换验证的身份名称。
- `(auth_author)`：此变量初始包含授权身份的值。如果在`MAIL From:`头部中通过`AUTH`关键字定义了值，则该值将成为`{auth_author}`变量的值。

![](img/9639113aa446fb8976cb3d377f7aafdd_372_0.png)

身份验证仅用于中继这一事实降低了`AUTH`协议的整体安全重要性。熟悉加密的读者可能希望`AUTH`用于对电子邮件的源和内容提供密码学验证。事实并非如此。`AUTH`作为对抗垃圾邮件和未经授权中继的另一种工具最为有效。

`RFC 2554`规定，`AUTH`扩展可以可选用于后续协议交互的安全层，这意味着消息加密。然而，它并不是这样使用的。`STARTTLS`是加密消息传输的协议。

## 传输层安全

`AUTH`扩展使用共享密钥。身份验证数据使用相同的密钥进行加密和解密，使`AUTH`成为对称加密系统。相反，`TLS`是公共加密系统。事实上，`TLS`是`SSL`，用于保护`Web`通信的公共加密系统。使用`SSL`保护电子邮件与使用`SSL`保护`Web`通信需要相同。

> 注意：要了解更多关于`Linux` `Web`服务器的`SSL`，请参阅`Charles Auids`所写的《`Apache Web Server Administration`》(`Sybek`, 2000)。

`SSL`公钥加密需要三样东西：

- 证书颁发机构：公钥加密需要一个称为证书颁发机构（`CA`）的第三方。`CA`是获取公钥的服务器。你不能信任直接从终端系统获取的公钥，除非你拥有密钥，否则你无法验证该系统是它所声称的主机。另一方面，`CA`是一个著名的服务器。某些工具（如`Netscape`浏览器）预配置为识别许多证书颁发机构。
- 证书：这是公钥。它以`X509`证书的形式存在，由`CA`签名，包含了你的身份以及验证密钥有效的日期。
- 私密钥：这是你用于加密通信的密钥，随后由公钥解密。私密钥必须保持安全。

基本信息必须在`Sendmail`中标识。存储证书的路径由`confPATH`定义，单个证书由`confCACERT`定义。只要目录可以由`root`，就可以放在任何地方。

除了`CA`证书外，`Sendmail`还需要知道它用于识别和加密自身通信的公私密钥密钥。`Sendmail`根据它是作为服务器还是客户端使用不同的公私密钥集。这些值由四个`m4`参数定义：

- `confCACERT`: `/etc/httpd/conf/ssl.crt`
- `ServerCertFile`：`ServerCertFile`选项识别`Sendmail`作为服务器时使用的`X509`证书文件。实际上，这是服务器的公钥。例如：

```
define(`confSERVER_CERT`, `/etc/httpd/conf/ssl.crt`)
```

- `ServerKeyFile`选项：`ServerKeyFile`选项识别`Sendmail`作为服务器时使用的私密钥文件。`confSERVER_KEY`参数可以定义如下：

```
define(`confSERVER_KEY`, `/etc/httpd/conf/ssl.crt/server.key`)
```

- `ClientCertFile`选项：`ClientCertFile`识别`Sendmail`作为客户端时使用的`X509`证书文件。实际上，这是客户端的公钥。以下示例指向`Apache SSL`目录：

```
define(`confCLIENTCERT`, `/etc/httpd/conf/client.crt`)
```

- `ClientKeyFile`选项：`ClientKeyFile`选项识别`Sendmail`作为客户端时使用的私密钥文件。后续命令告诉`Sendmail`客户端的私钥在哪里：

```
define(`confCLIENT_KEY`, `/etc/httpd/conf/client.key`)
```
