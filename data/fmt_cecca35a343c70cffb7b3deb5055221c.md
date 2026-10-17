
没有选项可以打印 PKCS#7 文件的所有字段。

此 PKCS#7 例程仅理解 RFC2315 中指定的 PKCS#7 v 1.5；目前它无法解析例如 RFC2630 中描述的新 CMS。

### 另请参阅

(1)

## PKCS8

### 名称

`pkcs8` – PKCS#8 格式私钥转换工具

### 概要

```
openssl pkcs8 [-topk8] [-inform PEM | DER] [-outform PEM | DER] [-in filename] [-passin arg] [-out filename] [-passout arg] [-noiter] [-nocrypt] [-nooct] [-eed] [-nsdb] [-v2prf alg] [-v1 alg] [-engine id]
```

### 描述

`pkcs8` 命令处理 PKCS#8 格式的私钥。它可以处理未加密的 PKCS#8 `PrivateKeyInfo` 格式以及使用多种 PKCS#5（v1.5 和 v2.0）和 PKCS#12 算法的 `EncryptedPrivateKeyInfo` 格式。

### 命令选项

- `-topk8`

  通常期望输入为 PKCS#8 私钥，并写入传统格式私钥。使用 `-topk8` 选项时，情况相反：它读取传统格式私钥并写入 PKCS#8 格式密钥。

- `-inform DER|PEM`

  指定输入格式。如果期望输入为 PKCS#8 格式密钥，则期望 PKCS#8 密钥的 DER 或 PEM 编码版本。否则，使用传统格式私钥的 DER 或 PEM 格式。

- `-outform DER|PEM`

  指定输出格式，选项含义与 `-inform` 选项相同。

- `-in` `filename`

  指定要读取密钥的输入文件名，如果未指定此选项，则从标准输入读取。如果密钥已加密，系统将提示输入密码。

- `-passin` `arg`

  输入文件的密码源。有关 `arg` 格式的更多信息，请参见 (1) 中的密码参数部分。

- `-out` `filename`

  指定要写入密钥的输出文件名，默认写入标准输出。如果设置了任何加密选项，系统将提示输入密码。输出文件名不应与输入文件名相同。

- `-passout` `arg`

  输出文件的密码源。有关 `arg` 格式的更多信息，请参见 (1) 中的密码参数部分。

- `-nocrypt`

  生成或输入的 PKCS#8 密钥通常是使用适当的基于密码的加密算法的 PKCS#8 `EncryptedPrivateKeyInfo` 结构。使用此选项时，期望或输出未加密的 `PrivateKeyInfo` 结构。此选项完全不加密私钥，仅应在绝对必要时使用。某些软件，如某些版本的 Java 代码签名软件，使用未加密的私钥。

- `-nooct`

  此选项生成某些软件使用的破损格式的 RSA 私钥。具体来说，私钥应包含在 OCTET STRING 中，但某些软件仅包含结构本身，没有外围的 OCTET STRING。

- `-eed`

  此选项生成破损格式的 DSA 密钥。DSA 参数嵌入在 `PrivateKey` 结构内部。在此形式中，OCTET STRING 包含由两个结构组成的 ASN1 SEQUENCE：一个包含参数的 SEQUENCE 和一个包含私钥的 ASN1 INTEGER。

- `-nsdb`

  此选项生成与 Netscape 私钥数据库兼容的破损格式 DSA 密钥。`PrivateKey` 包含一个分别由公钥和私钥组成的 SEQUENCE。

- `-v2` `alg`

  此选项启用 PKCS#5 v2.0 算法的使用。通常，PKCS#8 私钥使用名为 `pbeWithMD5AndDES-CBC` 的基于密码的加密算法加密，这使用 56 位 DES 加密，但它是 PKCS#5 v1.5 支持的最强加密算法。使用 `-v2` 选项时，使用 PKCS#5 v2.0 算法，这些算法可以使用任何加密算法，如 168 位三重 DES 或 128 位 RC2，但目前的许多实现尚不支持 PKCS#5 v2.0。如果您只是使用 OpenSSL 处理私钥，这并不重要。

  `alg` 参数是要使用的加密算法，有效值包括 `des`、`des3` 和 `rc2`。建议使用 `des3`。

- `-v2prf` `alg`

  此选项设置与 PKCS#5 v2.0 一起使用的 `PRF` 算法。典型的值可以是 `hmacWithSHA256`。如果未设置此选项，则使用该密码器的默认值，如果没有默认值，则使用 `hmacWithSHA1`。

- `-v1` `alg`

  此选项指定要使用的 PKCS#5 v1.5 或 PKCS#12 算法。可能的完整算法列表包含在下面。

- `-engine` `id`

  指定引擎（通过其唯一的 `id` 字符串）将导致 `pkcs8` 尝试获取指定引擎的功能引用，从而在必要时对其进行初始化。该引擎随后将被设置为所有可用算法的默认引擎。

### 注意事项

PEM 编码的 PKCS#8 文件的加密形式使用以下头部和尾部：

```
-----BEGIN ENCRYPTED PRIVATE KEY-----
-----END ENCRYPTED PRIVATE KEY-----
```

未加密的形式使用：

```
-----BEGIN PRIVATE KEY-----
-----END PRIVATE KEY-----
```

使用 PKCS#5 v2.0 算法和高迭代次数加密的私钥比使用传统 SSLkey 兼容格式加密的私钥更安全。因此，如果认为额外的安全性很重要，应转换密钥。

默认加密只有 56 位，因为这是大多数当前 PKCS#8 实现支持的加密方式。

某些软件可能在 PKCS#8 格式私钥中使用 PKCS#12 基于密码的加密算法；这些会自动处理，但没有选项来生成它们。

由于加密细节在 ASN1 级别包含，而传统格式在 PEM 级别包含，因此可以写出 PKCS#8 格式中 DER 编码的加密私钥。

#### PKCS#5 V1.5 AND PKCS#12 算法

可以与 `-v1` 命令行选项一起使用各种算法，包括 PKCS#5 v1.5 和 PKCS#12。下面更详细地描述这些算法。

- `PBE-MD2-DES` `PBE-MD5-DES`

  这些算法包含在最初的 PKCS#5 v1.5 规范中。由于两者都使用 DES，它们只提供 56 位的保护。

- `PBE-SHA1-RC2-64` `PBE-MD2-RC2-64` `PBE-MD5-RC2-64` `PBE-SHA1-DES`

  这些算法未在最初的 PKCS#5 v1.5 规范中提到，但它们使用相同的密钥导出算法，并受某些软件支持。它们在 PKCS#5 v2.0 中提到。它们使用 64 位 RC2 或 56 位 DES。

- `PBE-SHA1-RC4-128` `PBE-SHA1-RC4-40` `PBE-SHA1-3DES` `PBE-SHA1-2DES` `PBE-SHA1-RC2-128` `PBE-SHA1-RC2-40`

  这些算法使用 PKCS#12 基于密码的加密算法，允许使用如三重 DES 或 128 位 RC2 等强加密算法。

### 示例

使用三重 DES 将私钥从传统格式转换为 PKCS#5 v2.0 格式：

`openssl pkcs8 -in key.pem -topk8 -v2 des3 -out enckey.pem`

使用 256 位 CBC 模式的 AES 和 `hmacWithSHA256` PRF 将私钥从传统格式转换为 PKCS#5 v2.0 格式：

`openssl pkcs8 -in key.pem -topk8 -v2 aes-256-cbc -v2prf hmacWithSHA256 -out enckey.pem`

使用与 PKCS#5 1.5 兼容的算法（DES）将私钥转换为 PKCS#8：

`openssl pkcs8 -in key.pem -topk8 -out enckey.pem`

使用与 PKCS#12 兼容的算法（3DES）将私钥转换为 PKCS#8：

`openssl pkcs8 -in key.pem -topk8 -out enckey.pem -v1 PBE-SHA1-3DES`

读取 DER 格式的未加密 PKCS#8 格式私钥：

`openssl pkcs8 -inform DER -nocrypt -in key.der -out key.pem`

将任意 PKCS#8 格式的私钥转换为传统格式：

`openssl pkcs8 -in pk8.pem -out key.pem`

### 标准

该 PKCS#5 v2.0 实现的测试向量已使用三重 DES、DES 和高迭代次数在 RC2 中发布到 pkcs-tng 邮件列表，多人确认他们可以解密生成的私钥，因此可以假设 PKCS#5 v2.0 实现对于这些算法而言是相对准确的。
