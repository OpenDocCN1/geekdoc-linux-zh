

可用的优先级字符串。例如，要获取至少提供 128 位安全性的密码套件列表，请执行以下命令：

```
`~]$ gnutls-cli --priority SECURE128 -l`
```

要获取满足第 4.13.1 节“选择要启用的算法”中列出的建议的密码套件列表，请使用类似以下命令：

```
`~]$ gnutls-cli --priority SECURE256:+SECURE128: -VERS-TLS-ALL:+VERS-TLS1.2: -RSA: -DHE-DSS: -CAMELLIA-128-CBC: -CAMELLIA-256-CBC -l`
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

上述命令将输出限制为至少具有 128 位安全性的密码，并优先选择更强的密码。它还禁止使用 *RSA* 密钥交换和 *DSS* 认证。

请注意，这是一个相当严格的配置，在实际场景中，可能需要放宽条件以允许与更广泛客户端的兼容性。

## 4.13.3. 配置特定应用程序

不同的应用程序提供自己的 TLS 配置机制。本节介绍了最常用的服务器应用程序所使用的 TLS 相关配置文件，并提供了典型配置的示例。

无论您选择使用哪种配置，请务必确保您的服务器应用程序强制实施服务器端密码顺序，以便使用的密码套件由您配置的顺序决定。

### 4.13.3.1. 配置 Apache HTTP 服务器

Apache HTTP 服务器可以使用 OpenSSL 和 NSS 库来满足其 TLS 需求。根据您对 TLS 库的选择，您需要安装 mod_ssl 或 mod_nss 模块（由同名软件包提供）。例如，要安装提供 OpenSSL mod_ssl 模块的软件包，请以 root 身份执行以下命令：

```
[#] yum install mod_ssl
```

mod_ssl 软件包安装 `/etc/httpd/conf.d/ssl.conf` 配置文件，该文件可用于修改 Apache HTTP 服务器的 TLS 相关设置。类似地，mod_nss 软件包安装 `/etc/httpd/conf.d/nss.conf` 配置文件。

安装 httpd-manual 软件包以获取 Apache HTTP 服务器的完整文档，包括 TLS 配置。`/etc/httpd/conf.d/ssl.conf` 配置文件中可用的指令在 `/usr/share/httpd/manual/mod/mod_ssl.html` 中有详细说明。各种设置的示例位于 `/usr/share/httpd/manual/ssl/ssl_howto.html` 中。

在修改 `/etc/httpd/conf.d/ssl.conf` 配置文件中的设置时，请至少考虑以下三个指令：

- **SSLProtocol**
  使用此指令指定您允许使用的 TLS（或 SSL）版本。
- **SSLCipherSuite**
  使用此指令指定您首选的密码套件或禁用您不希望使用的套件。
- **SSLHonorCipherOrder**
  取消注释并将此指令设置为 `on`，以确保连接的客户端遵守您指定的密码顺序。

例如：

```
SSLProtocol all -SSLv2 -SSLv3
SSLCipherSuite HIGH:!aNULL:!MD5
SSLHonorCipherOrder on
```

请注意，上述配置是最低限度的配置，通过遵循 [第 4.13.1 节，“选择要启用的算法”](#) 中概述的建议，可以对其进行显著增强。

要配置和使用 `mod_nss` 模块，请修改 `/etc/httpd/conf.d/nss.conf` 配置文件。`mod_nss` 模块源自 `mod_ssl`，因此它与 `mod_ssl` 共享许多特性，尤其是配置文件的结构以及可用的指令。请注意，`mod_nss` 指令的前缀是 `NSS` 而不是 `SSL`。有关 `mod_nss` 信息的概览，包括不适用于 `mod_nss` 的 `mod_ssl` 配置指令列表，请参阅 [https://git.dredarohosted.org/cgit/mod_nss.git/plain/docs/mod_nss.html](https://git.dredarohosted.org/cgit/mod_nss.git/plain/docs/mod_nss.html)。

### 4.13.3.2. 配置 Dovecot 邮件服务器

要配置您的 Dovecot 邮件服务器安装以使用 TLS，请修改 `/etc/dovecot/conf.d/10-ssl.conf` 配置文件。您可以在 `/usr/share/doc/dovecot-2.2.10/wiki/SSL.DovecotConfiguration.txt` 中找到该文件中一些基本配置指令的说明（此帮助文件随 Dovecot 的标准安装一起安装）。

在修改 `/etc/dovecot/conf.d/10-ssl.conf` 配置文件中的设置时，请至少考虑以下三个指令：

- `ssl_protocols`
  使用此指令指定您允许使用的 TLS（或 SSL）版本。
- `ssl_cipher_list`
  使用此指令指定您首选的密码套件或禁用您不希望使用的套件。
- `ssl_prefer_server_ciphers`
  取消注释并将此指令设置为 `yes`，以确保连接的客户端遵守您指定的密码顺序。

例如：

```
ssl_protocols = !SSLv2 !SSLv3
ssl_cipher_list = HIGH:!aNULL:!MD5
ssl_prefer_server_ciphers = yes
```

请注意，上述配置是最低限度的配置，通过遵循 [第 4.13.1 节，“选择要启用的算法”](#) 中概述的建议，可以对其进行显著增强。

### 4.13.4. 其他信息

有关 TLS 配置和相关主题的更多信息，请参阅下面列出的资源。

#### 已安装的文档

- `config(1)` – 描述了 `/etc/ssl/openssl.conf` 配置文件的格式。
- `ciphers(1)` – 包括可用的 `OpenSSL` 关键字和密码字符串列表。
- `/usr/share/httpd/manual/mod/mod_ssl.html` – 包含 Apache HTTP 服务器中 `mod_ssl` 模块使用的 `/etc/httpd/conf.d/ssl.conf` 配置文件中可用指令的详细描述。
- `/usr/share/httpd/manual/ssl/ssl_howto.html` – 包含 Apache HTTP 服务器中 `mod_ssl` 模块使用的 `/etc/httpd/conf.d/ssl.conf` 配置文件中实际设置的实用示例。
- `/usr/share/doc/dovecot-2.2.10/wiki/SSL.DovecotConfiguration.txt` – 解释了 Dovecot 邮件服务器使用的 `/etc/dovecot/conf.d/10-ssl.conf` 配置文件中的一些基本配置指令。

#### 在线文档

- Red Hat Enterprise Linux 7 SELinux 用户和管理员指南 – Red Hat Enterprise Linux 7 的 SELinux 用户和管理员指南介绍了 SELinux 的基本原理，并详细记录了如何配置和使用 SELinux 以及各种服务，例如 Apache HTTP 服务器。
- http://tools.ietf.org/html/draft-ietf-uta-tls-bcp-00 – 关于安全使用 TLS 和 DTLS 的建议。

#### 另请参阅

- 第 A.2.4 节，“SSL/TLS” 提供了 SSL 和 TLS 协议的简要描述。
- 第 4.7 节，“使用 OpenSSL” 描述了（除其他内容外）如何使用 OpenSSL 创建和管理密钥、生成证书以及加密和解密文件。

## 4.14. 使用共享系统证书

共享系统证书存储允许 NSS、GnuTLS、OpenSSL 和 Java 共享获取系统证书锚点和黑名单信息的默认来源。默认情况下，信任存储包含 Mozilla CA 列表，包括正向和负向信任。系统允许更新核心 Mozilla CA 列表或选择其他证书列表。

### 4.14.1. 使用系统范围的信任存储

在 Red Hat Enterprise Linux 7 中，集成的系统范围信任存储位于 `/etc/pki/ca-trust/` 和 `/usr/share/pki/ca-trust-source/` 目录中。`/usr/share/pki/ca-trust-source/` 中的信任设置的优先级低于 `/etc/pki/ca-trust/` 中的设置。
证书文件根据其安装所在的子目录进行处理：

- `/usr/share/pki/ca-trust-source/anchors/` 或 `/etc/pki/ca-trust/source/anchors/` - 用于信任锚点。参见第 4.5.6 节，“理解信任锚点”。
- `/usr/share/pki/ca-trust-source/blacklist/` 或 `/etc/pki/ca-trust/source/blacklist/` - 用于不受信任的证书。
- `/usr/share/pki/ca-trust-source/` 或 `/etc/pki/ca-trust/source/` - 用于扩展 BEGIN TRUSTED 文件格式中的证书。

