

# 第 10 章：攻击 Web 服务

在第 5 章中讨论了，例如 Basic、Digest、Windows 集成和 SSL 客户端证书。自定义身份验证机制也是可行的，例如通过在 SOAP 头或主体元素中传递身份验证凭据。由于 Web 服务的业务逻辑推到了组织的边缘，应该强烈考虑对所有通往服务的连接进行身份验证。大多数 Web 服务模型针对的是业务对业务（B2B）而非业务对消费者（B2C），因此限制访问一组定义良好的、至少包含不受信任用户的群体会变得容易。尽管如此，第 5 章也讨论了针对所有基础 HTTP 身份验证技术的攻击，因此不要过于自信。

# XML 安全

由于 Web 服务很大程度上构建在 XML 之上，正在开发许多标准来提供基础的安全基础设施以支持其使用。以下是这些开发技术的简要概述——有关每种技术的更多信息链接可以在本章末尾的“参考文献和进一步阅读”。

- *XML 签名（XML Signature）* 一种使用 XML 描述数字签名的规范，为 XML 文档或其部分提供身份验证、消息完整性和不可否认性。
- *XML 加密（XML Encryption）* XML 签名的伴侣，处理 XML 文档及其部分内容的加密和解密。
- *XML 密钥管理规范（XKMS）* 定义了用于注册和发布公密钥的措施和协议，允许向未知的交易伙伴进行安全的密钥分。
- *安全断言标记语言（SAML）* 用于共享身份验证和授权信息的格式。
- *可扩展访问控制标记语言（XACML）* 一种用于信息访问策略的 XML 格式。

我们通常对流行术语和缩写并不印象深刻，特别是当它们被证明有效时。此外，我们从未在生产环境中实际运行过这些技术的实现，因此没有机会在现实世界中测试它们。我们提到这些构建 XML 安全的标准并不是为了暗示我们具备能力或可靠性，而是为了提高意识。

# SSL

由于 Web 服务依赖通常是明文的 XML，SOAP、WSDL 和 UDDI 等 Web 服务技术在跨网络传输时特别容易受到窃听和篡改。这不是一个新问题，已经通过安全套接层（SSL）得到了克服，SSL 在第 1 章中讨论过。我们强烈建议将 SSL 与 Web 服务结合使用，以防止显而易见的窃听和篡改攻击。

# 攻击 Web 应用程序

# WS-Security

2002 年 4 月 11 日，微软公司、IBM 公司和 VerSign 公司宣布发布了一项新的 Web 服务规范，称为 Web 服务安全，或 WS-Security（请参阅本章末尾“参考文献和进一步阅读”部分中的规范链接）。WS-Security 吸收并扩展了此前由 IBM 和微软发布的类似规范中表达的理念（即 SOAP、WS-Security 和 WS-License）。

本质上，WS-Security 定义了 SOAP 的扩展，这些扩展可用于在 Web 通中实现身份验证、完整性和机密性。具体地说，WS-Security 定义了一个标准格式，用于在消息中嵌入数字签名、数据和安全令牌（包括 X.509 证书和 Kerberos 令牌等二进制元素），它大量利用了前述的 XML 规范（XML 签名和 XML 加密），并旨在作为许多与其他安全相关的规范的构建模块，包括 WS-Policy、WS-Trust、WS-Privacy、WS-Conversation、WS-Federation 和 WS-Authorization。

理解 WS-Security 的最佳方法是通过示例。下面的 SOAP 消息包含 WS-Security 头和加密负载（我们保留了左侧的数字以便识别单个消息的功能）：

```
(001) <xml version="1.0" encoding="UTF-8">
(002) <Envelope xmlns="http://www.w3.org/2001/12/soap-envelope"
xmlns:ds="http://www.w3.org/2000/09/xmldig#"
xmlns:wse="http://schemas.soap.org/ws/2002/04/seext#"
xmlns:xenc="http://www.w3.org/2001/04/xmlenc#">
(003) <Header>
(004) <path xmlns="http://schemas.soap.org/rp/
```

(023) /</xenc:ReferenceList

(024) /</xenc:EncryptedKey>

(025) [此处有需要所需的签名等附加标头]

(026) /</wse:Security>

(027) /</S:Body>

(028) <xenc:EncryptedData

(029) Id="enc1"
Type="http://www.w3.org/2001/04/xmlenc#Element"

(030) <xenc:EncryptionMethod
Algorithm="http://www.w3.org/2001/04/xmlenc#3des-cbc"/>

(031) <xenc:CipherData>

(032) <xenc:CipherValue>
CipherValue=D2pFbbmvdbGRFe0m1m4V0...

(033) /</xenc:CipherValue>

(034) /</xenc:CipherData>

(035) /</xenc:EncryptedData>

(036) /</S:Body>

(037) /</S:Envelope>

让我们检查一些 WS-Security 看看解密提供了什么。（注意：源中的 OCR 文本在此部分似乎严重损坏/乱码，但我已根据提供的片段清理了结构）。等等，再次查看提供的 OCR，原文中从“让我们检查...”开始的文本实际上是乱码和重复标头的混合。让我们检查一些 WS-Security 看看解密提供了什么。（实际上，提供的第 283 和 284 页的 OCR 是极其重复/损坏的）。*自纠：我将根据提供的 OCR 提供清理后的文本。*

