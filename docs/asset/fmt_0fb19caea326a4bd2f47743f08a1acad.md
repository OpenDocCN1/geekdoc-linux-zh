
```
# pk12util -l certs.p12 输入 PKCS12 文件密码：密钥（shrouded）：友好名称：Thawte 免费邮件 Meer 的 Thawte Consulting (Pty) Ltd. ID 加密算法：PKCS #12 V2 PBE 使用 SHA-1 And 3KEY 三重 DES-CBC 参数：盐值：45:2e:6a:a0:03:4d:7b:a1:63:3c:15:ea:67:37:62:1f 迭代次数：1 (0x1) 证书：数据：版本：3 (0x2) 序列号：13 (0xd) 签名算法：PKCS #1 SHA-1 使用 RSA 加密 颁发者："E=,CN=Thawte Personal Freemall C A, OU=Certification Services
```

Division,0=Thawte Consulting,L=Cape Town,ST=Western Cape,C=ZA""

或者，`-r` 选项会打印证书，然后将它们导出到独立的 DER 二进制文件中。这使得证书可以被提供给支持 `.p12` 文件的另一个应用程序。每个证书都被写入按顺序编号的文件中，从 `file0001.der` 开始，依次递增到 `file000N.der`，每个证书对应一个递增的编号：

```
pk12util -l test.p12 -r Enter password for PKCS12 file: Key(Shrouded):
Friendly Name: Thawte Freel-mail Meer's Thawte Consulting (Pty) Ltd. ID
Encryption algorithm: PKCS #12 V2 PBE With SHA-1 And 3KEY Triple DES-CBC Parameters: Salt: 45:2e:6a:a0:03:4d:7b:a1:63:3c:15:ea:67:37:62:1f
Iteration Count: 1 (0x1) Certificate Friendly Name: Thawte Personal
Freemail Issuing CA - Thawte Consulting Certificate Friendly Name: Thawte
Freemail Meer's Thawte Consulting (Pty) Ltd. ID
```

## 密码加密

PKCS#12 不仅提供对私钥的保护，还提供与密钥相关的证书和元数据的保护。基于密码的加密用于在导出到 PKCS#12 文件时保护私钥，并可选地保护整个数据包。如果未指定算法，工具默认使用 `PKCS12 V2 PBE with SHA1 and 3KEY Triple DES-cbc` 进行私钥加密。当处于非 FIPS 模式时，`PKCS12 V2 PBE with SHA1 and 40 Bit RC4` 是整个数据包加密的默认算法。在 FIPS 模式下，没有数据包加密。

私钥默认始终受到强加密保护。

支持多种类型的密码。

- PKCS#5 V2 对称 CBC 密码

    - `DES-CBC`

    - `RC2-CBC`

    - `RC5-CBCPad`

    - `DES-EDE3-CBC`（密钥加密的默认算法）

    - `AES-128-CBC`

    - `AES-192-CBC`

    - `AES-256-CBC`

    - `CAMELLIA-128-CBC`

    - `CAMELLIA-192-CBC`

    - `CAMELLIA-256-CBC`

- PKCS#12 PBE 密码

    - `PKCS #12 PBE with Sha1 and 128 Bit RC4`

    - `PKCS #12 PBE with Sha1 and 40 Bit RC4`

    - `PKCS #12 PBE with Sha1 and Triple DES CBC`

    - `PKCS #12 PBE with Sha1 and 128 Bit RC2 CBC`

    - `PKCS #12 PBE with Sha1 and 40 Bit RC2 CBC`

    - `PKCS12 V2 PBE with SHA1 and 128 Bit RC4`

    - `PKCS12 V2 PBE with SHA1 and 40 Bit RC4`（非 FIPS 模式的默认算法）

    - `PKCS12 V2 PBE with SHA1 and 3KEY Triple DES-cbc`

    - `PKCS12 V2 PBE with SHA1 and 2KEY Triple DES-cbc`

- `PKCS12 V2 PBE with SHA1 and 128 Bit RC2 CBC`

- `PKCS12 V2 PBE with SHA1 and 40 Bit RC2 CBC`

- PKCS#5 PBE 密码

    - `PKCS #5 Password Based Encryption with MD2 and DES CBC`

    - `PKCS #5 Password Based Encryption with MD5 and DES CBC`

    - `PKCS #5 Password Based Encryption with SHA1 and DES CBC`

对于 PKCS#12，加密提供者可以是软令牌模块或外部硬件模块。如果加密模块不支持请求的算法，则选择下一个最佳匹配（通常是默认值）。如果找不到所需算法的合适替代方案，工具将返回错误 `no security module can perform the requested operation`。

### NSS 数据库类型

NSS 最初使用 BerkeleyDB 数据库来存储安全信息。这些 *legacy* 数据库的最后几个版本是：

- `cert8.db` 用于证书

- `key3.db` 用于密钥

- `secmod.db` 用于 PKCS #11 模块信息

然而，BerkeleyDB 存在性能限制，这使得它难以被多个应用程序同时使用。NSS 具有一定的灵活性，允许应用程序使用自己的、独立的数据库引擎，同时保持共享数据库并绕过访问问题。不过，NSS 需要更多的灵活性来提供真正共享的安全数据库。

2009 年，NSS 引入了一套新的数据库，这些数据库是 SQLite 数据库而不是 BerkeleyDB。这些新数据库提供了更高的可访问性和性能：

- `cert9.db` 用于证书

- `key4.db` 用于密钥

- `pkcs11.txt`，它是安全数据库目录中一个包含所有 PKCS #11 模块的新子目录中的列表

由于 SQLite 数据库旨在被共享，因此这些是 *shared* 数据库类型。推荐使用共享数据库类型；保留 legacy 格式是为了向后兼容。

默认情况下，工具（`certutil`、`pk12util`、`modutil`）假设给定的安全数据库遵循更常见的 legacy 类型。必须通过在使用给定的安全目录时使用 `sql:` 前缀来手动指定使用 SQLite 数据库。例如：

```
# pk12util -i /tmp/cert-files/users.p12 -d sql:/home/my/sharednssdb
```

要将共享数据库类型设置为工具的默认类型，将环境变量 `NSS_DEFAULT_DB_TYPE` 设置为 `sql:`

```bash
export NSS_DEFAULT_DB_TYPE="sql"
```

将此行添加到 `~/.bashrc` 文件中可以使更改永久化。

大多数应用程序默认不使用共享数据库，但可以配置它们使用共享数据库。例如，这篇操作指南涵盖了如何配置 Firefox 和 Thunderbird 使用新的共享 NSS 数据库：

关于共享 NSS 数据库变化的工程草案，请参阅 NSS 项目 wiki：

### 参见

- `certutil (1)`

- `modutil (1)`

NSS wiki 包含了关于新数据库设计以及如何配置应用程序使用它的信息。

### 其他资源

有关 NSS 和与其他 NSS 相关的工具（如 JSS）的信息，请查看位于 m[]] 的 NSS 项目 wiki。NSS 网站直接与 NSS 代码更改和发布相关。

邮件列表：

IRC：Freenode 上的 `#dogtag-pki`

### 作者

NSS 工具由来自 Netscape、Red Hat、Sun、Oracle、Mozilla 和 Google 的开发者编写和维护。

作者：Elio Maldonado `<>`、Deon Lackey `<>`。

### 许可证

根据 Mozilla Public License, v. 2.0 授权。如果未随此文件分发 MPL 副本，您可以在 获取一份

### 注释

1. Mozilla NSS bug 836477

### PKACTION

### 名称

`pkaction` - 获取有关已注册操作的信息

### 概要
