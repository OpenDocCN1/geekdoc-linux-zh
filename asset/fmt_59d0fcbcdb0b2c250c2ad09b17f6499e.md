
```
~]$ openssl ciphers -v 'ECCDH+aECDSA+AES:kECDH+AES+aRSA:kEDH+aRSA+AES' | column -t
ECDHE-ECDSA-AES256-GCM-SHA384       TLSv1.2  Kx=ECDH  Au=ECDSA  Enc=AESGCM(256)
Mac=AES
ECDHE-ECDSA-AES256-SHA384            TLSv1.2  Kx=ECDH  Au=ECDSA  Enc=AES(256)
Mac=SHA384
ECDHE-ECDSA-AES256-SHA               SSLv3    Kx=ECDH  Au=ECDSA  Enc=AES(256)
Mac=SHA1
ECDHE-ECDSA-AES128-GCM-SHA256        TLSv1.2  Kx=ECDH  Au=ECDSA  Enc=AESGCM(128)
Mac=AES
ECDHE-ECDSA-AES128-SHA256            TLSv1.2  Kx=ECDH  Au=ECDSA  Enc=AES(128)
Mac=SHA256
ECDSA-AES128-SHA Mac=SHA1 SSLv3 Kx=ECDH Au=ECDSA Enc=AES(128)
ECDHE-RSA-AES256-GCM-SHA384 Mac=AESAD TLSv1.2 Kx=ECDH Au=RSA Enc=AESGCM(256)
ECDHE-RSA-AES256-SHA384 Mac=SHA384 TLSv1.2 Kx=ECDH Au=RSA Enc=AES(256)
ECDHE-RSA-AES256-SHA Mac=SHA1 SSLv3 Kx=ECDH Au=RSA Enc=AES(256)
ECDHE-RSA-AES128-GCM-SHA256 Mac=AESAD TLSv1.2 Kx=ECDH Au=RSA Enc=AESGCM(128)
ECDHE-RSA-AES128-SHA256 Mac=SHA256 TLSv1.2 Kx=ECDH Au=RSA Enc=AES(128)
ECDHE-RSA-AES128-SHA Mac=SHA1 SSLv3 Kx=ECDH Au=RSA Enc=AES(128)
DHE-RSA-AES256-GCM-SHA384 Mac=AESAD TLSv1.2 Kx=DH Au=RSA Enc=AESGCM(256)
DHE-RSA-AES256-SHA256 Mac=SHA256 TLSv1.2 Kx=DH Au=RSA Enc=AES(256)
DHE-RSA-AES256-SHA Mac=SHA1 SSLv3 Kx=DH Au=RSA Enc=AES(256)
DHE-RSA-AES128-GCM-SHA256 Mac=AESAD TLSv1.2 Kx=DH Au=RSA Enc=AESGCM(128)
DHE-RSA-AES128-SHA256 Mac=SHA256 TLSv1.2 Kx=DH Au=RSA Enc=AES(128)
DHE-RSA-AES128-SHA Mac=SHA1 SSLv3 Kx=DH Au=RSA Enc=AES(128)
```

上述命令省略了所有不安全的密码，优先选择 `临时椭圆曲线 Diffie-Hellman` 密钥交换和 `ECDSA` 密码，并省略了 `RSA` 密钥交换（从而确保 `完美前向保密`）。

请注意，这是一种相当严格的配置，在实际场景中可能需要放宽条件，以便与更广泛的客户端范围兼容。

#### 4.13.2.2. 在 GnuTLS 中处理密码套件

`GnuTLS` 是一个实现了 `SSL` 和 `TLS` 协议及相关技术的通信库。

> `注意`
>
> Red Hat Enterprise Linux 7 上的 `GnuTLS` 安装提供了最优的默认配置值，为大多数使用场景提供了足够的安全性。除非您需要满足特殊的安全要求，否则建议使用提供的默认值。

使用带有 `-1`（或 `--list`）选项的 `gnutls-cli` 命令来列出所有支持的密码套件：

```
~]$ gnutls-cli -1
```

要缩小由 `-1` 选项显示的密码套件列表，请向 `--priority` 选项传递一个或多个参数（在 `GnuTLS` 文档中称为 `priority strings` 和 `keywords`）。有关所有列表的列表，请参阅位于 http://www.gnutls.org/manual/gnutls.html#Priority-Strings 的 `GnuTLS` 文档

可用的优先级字符串。例如，要获取至少提供 128 位安全性的密码套件列表，请执行以下命令：

```
~]$ gnutls-cli --priority SECURE128 -l
```

要获取满足第 4.13.1 节“选择要启用的算法”中列出的建议的密码套件列表，请使用类似以下命令：

```
~]$ gnutls-cli --priority SECURE256:+SECURE128: -VERS-TLS-ALL:+VERS-TLS1.2: -RSA: -DHE-DSS: -CAMELLIA-128-CBC: -CAMELLIA-256-CBC -l
```

| 密码套件 | 十六进制代码 | 协议版本 |
| :--- | :--- | :--- |
| TLS_ECDHE_ECDSA_AES_256_GCM_SHA384 | 0xc0, 0x2c | TLS1.2 |
| TLS_ECDHE_ECDSA_AES_256_CBC_SHA384 | 0xc0, 0x24 | TLS1.2 |
| TLS_ECDHE_ECDSA_AES_256_CBC_SHA1 | 0xc0, 0x0a | SSL3.0 |
| TLS_ECDHE_ECDSA_AES_128_GCM_SHA256 | 0xc0, 0x2b | TLS1.2 |
| TLS_ECDHE_ECDSA_AES_128_CBC_SHA256 | 0xc0, 0x23 | TLS1.2 |
| TLS_ECDHE_ECDSA_AES_128_CBC_SHA1 | 0xc0, 0x09 | SSL3.0 |
| TLS_ECDHE_RSA_AES_256_GCM_SHA384 | 0xc0, 0x30 | TLS1.2 |
| TLS_ECDHE_RSA_AES_256_CBC_SHA1 | 0xc0, 0x14 | SSL3.0 |
| TLS_ECDHE_RSA_AES_128_GCM_SHA256 | 0xc0, 0x2f | TLS1.2 |
| TLS_ECDHE_RSA_AES_128_CBC_SHA256 | 0xc0, 0x27 | TLS1.2 |
| TLS_ECDHE_RSA_AES_128_CBC_SHA1 | 0xc0, 0x13 | SSL3.0 |
| TLS_DHE_RSA_AES_256_CBC_SHA256 | 0x00, 0x6b | TLS1.2 |
| TLS_DHE_RSA_AES_256_CBC_SHA1 | 0x00, 0x39 | SSL3.0 |
| TLS_DHE_RSA_AES_128_GCM_SHA256 | 0x00, 0x9e | TLS1.2 |
| TLS_DHE_RSA_AES_128_CBC_SHA256 | 0x00, 0x67 | TLS1.2 |
| TLS_DHE_RSA_AES_128_CBC_SHA1 | 0x00, 0x33 | SSL3.0 |

证书类型：CTYPE-X.509

协议：VERS-TLS1.2

压缩：COMP-NULL

椭圆曲线：CURVE-SECP384R1, CURVE-SECP521R1, CURVE-SECP256R1

PK 签名：SIGN-RSA-SHA384, SIGN-ECDSA-SHA384, SIGN-RSA-SHA512, SIGN-ECDSA-SHA512, SIGN-RSA-SHA256, SIGN-DSA-SHA256, SIGN-ECDSA-SHA256

上述命令将输出限制为至少具有 128 位安全性的密码，并优先选择更强的密码。它还禁止使用 `RSA` 密钥交换和 `DSS` 认证。

请注意，这是一个相当严格的配置，在实际场景中，可能需要放宽条件以允许与更广泛客户端的兼容性。

### 4.13.3. 配置特定应用程序

不同的应用程序提供自己的 TLS 配置机制。本节介绍了最常用的服务器应用程序所使用的 TLS 相关配置文件，并提供了典型配置的示例。

无论您选择使用哪种配置，请务必确保您的服务器应用程序强制实施服务器端密码顺序，以便使用的密码套件由您配置的顺序决定。

#### 4.13.3.1. 配置 Apache HTTP 服务器
