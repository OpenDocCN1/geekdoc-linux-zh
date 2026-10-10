

## fss_get_mapping <base_share> <shadow_copy_set_id> <shadow_copy_id>

获取影子副本共享映射信息

## fss_recovery_complete <shadow_copy_set_id>

标记读写影子副本为恢复完成，允许进一步的影子副本请求

## 通用命令

- **debuglevel**
  - 设置用于记录信息的当前调试级别。
- **help (?)**
  - 打印所有已知命令的列表或特定命令的扩展帮助。
- **quit (exit)**
  - 退出 rpcclient。

## 缺陷

rpcclient 是作为开发人员测试工具设计的，在某些领域（如命令行解析）可能不够健壮。已知在解释器接收到无效参数失败时，会生成核心转储（core dump）。

源自 Luke Leighton 的原始 rpcclient man 页面：

*警告！* MSRPC over SMB 代码是通过检查网络跟踪信息开发的。原始创建者（Microsoft）没有提供关于 MSRPC over SMB 如何工作或各个 MSRPC 服务如何工作的文档。Microsoft 的这些服务的实现已被证明（并被报告为）在某些地方……有些不稳定。

Samba 实现的开发也有点粗糙，随着对更多服务的理解，甚至可能导致某些命令或服务不兼容的 (8) 和 (1) 版本。此外，开发人员正在向 Microsoft 发送报告，发现或报告给 Microsoft 的问题会在服务包中修复，这可能会导致不兼容性。

## 版本

此 man 页面对于 Samba 套件的版本 3 是正确的。

## 作者

最初的 Samba 软件和相关工具是由 Andrew Tridgell 创建的。现在 Samba 由 Samba Team 作为开源项目进行开发，类似于 Linux 内核的开发方式。

原始的 rpcclient man 页面由 Matthew Geddes、Luke Kenneth Casson Leighton 撰写，并由 Gerald Carter 重写。Samba 2.2 向 DocBook 的转换是由 Gerald Carter 完成的。Samba 3.0 向 DocBook XML 4.2 的转换是由 Alexander Bokovoy 完成的。

# RSA

## 名称

**rsa** - RSA 密钥处理工具

## 概要

```
openssl rsa [-inform PEM|NET|DER] [-outform PEM|NET|DER] [-in file] [-passin arg] [-out file] [-passout arg] [-sgckey] [-aes128] [-aes192] [-aes256] [-camia128] [-camia192] [-camia256] [-des] [-des3] [-idea] [-text] [-noout] [-modulus] [-check] [-pubin] [-pubout] [-RSAPublicKey_in] [-RSAPublicKey_out] [-engine id]
```

## 描述

**rsa** 命令处理 RSA 密钥。它们可以在各种形式之间转换，并打印出其组件。**注意** 此命令使用传统的 SSLeay 兼容格式进行私钥加密：新的应用程序应使用更安全的 **pkcs8** 工具使用的 PKCS#8 格式。

## 命令选项

- **-inform** **DER**|**NET**|**PEM**
  - 指定输入格式。**DER** 选项使用与 PKCS#1 RSAPrivateKey 或 SubjectPublicKeyInfo 格式兼容的 ASN1 DER 编码形式。**PEM** 形式是默认格式：它由 **DER** 格式的 base64 编码加上额外的标题和页脚行组成。在输入时，也接受 PKCS#8 格式的私钥。**NET** 形式是在注释部分中描述的格式。
- **-outform** **DER**|**NET**|**PEM**
  - 指定输出格式，选项与 **-inform** 选项相同。
- **-in** *filename*
  - 指定要读取密钥的输入文件名，如果未指定此选项，则从标准输入读取。如果密钥已加密，将提示输入密码。
- **-passin** *arg*
  - 输入文件密码源。有关 *arg* 格式的更多信息，请参见 (1) 中的 **密码短语参数** 部分。
- **-out** *filename*
  - 指定要写入密钥的输出文件名，如果未指定此选项，则写入标准输出。如果设置了任何加密选项，将提示输入密码。输出文件名**不应**与输入文件名相同。
- **-passout** *password*
  - 输出文件密码源。有关 *arg* 格式的更多信息，请参见 (1) 中的 **密码短语参数** 部分。
- **-sgckey**
  - 使用某些版本的 Microsoft **ITS** 和 **SGC** 密钥使用的修改后的 **NET** 算法。
- **-aes128|-aes192|-aes256|-camia128|-camia192|-camia256|-des|-des3|-idea**
  - 这些选项在输出前使用指定的密码加密私钥。将提示输入密码。如果未指定这些选项中的任何一个，密钥将以纯文本形式写入。这意味着使用 **rsa** 工具读取没有加密选项的加密密钥可用于删除密钥的密码短语，或者通过设置加密选项可以添加或更改密码短语。这些选项只能与 **PEM** 格式的输出文件一起使用。
- **-text**
  - 除了编码版本外，以纯文本形式打印出各种公钥或私钥组件。
- **-noout**
  - 此选项防止输出密钥的编码版本。
- **-modulus**
  - 此选项打印出密钥模数的值。
- **-check**
  - 此选项检查 RSA 私钥的一致性。
- **-pubin**
  - 默认情况下从输入文件读取私钥；使用此选项将改为读取公钥。
- **-pubout**
  - 默认情况下输出私钥；使用此选项将改为输出公钥。如果输入是公钥，则自动设置此选项。
- **-RSAPublicKey_in, -RSAPublicKey_out**
  - 类似于 **-pubin** 和 **-pubout**，但使用的是 **RSAPublicKey** 格式。
- **-engine id**
  - 指定引擎（通过其唯一的 **id** 字符串）将使 **rsa** 尝试获取指定引擎的功能引用，从而在需要时初始化它。该引擎将设置为所有可用算法的默认引擎。

## 注释

**PEM** 私钥格式使用以下标题和页脚行：

```
-----BEGIN RSA PRIVATE KEY-----
-----END RSA PRIVATE KEY-----
```

**PEM** 公钥格式使用以下标题和页脚行：

```
-----BEGIN PUBLIC KEY-----
-----END PUBLIC KEY-----
```

**PEM** **RSAPublicKey** 格式使用以下标题和页脚行：

```
-----BEGIN RSA PUBLIC KEY-----
-----END RSA PUBLIC KEY-----
```

**NET** 形式是一种与旧版 Netscape 服务器和 Microsoft **iis** .key 文件兼容的格式，它使用无盐 **RC4** 进行加密。它不太安全，因此仅在必要时使用。

因此，较新版本的 **iis** 在导出的 .key 文件中包含额外的数据。要使用这些文件，使用二进制编辑器查看文件并查找字符串 “private-key”，然后回溯到字节序列 **0x30, 0x82**（这是一个 **ASN1 SEQUENCE**）。从该点开始复制所有数据到另一个文件，并使用该文件作为 **rsa** 工具的输入，使用 **-inform NET** 选项。如果在输入密码后收到错误，请尝试 **-sgckey** 选项。

## 示例

要删除 RSA 私钥的密码短语：
`openssl rsa -in key.pem -out keyout.pem`

要使用三重 DES 加密私钥：
`openssl rsa -in key.pem -des3 -out keyout.pem`

要将私钥从 PEM 转换为 DER 格式：
`openssl rsa -in key.pem -outform DER -out keyout.der`

要将私钥组件打印到标准输出：
`openssl rsa -in key.pem -text -noout`

仅输出私钥的公共部分：
`openssl rsa -in key.pem -pubout -out pubkey.pem`

以 **RSAPublicKey** 格式输出私钥的公共部分：
`openssl rsa -in key.pem -RSAPublicKey_out -out pubkey.pem`

## 缺陷

命令行密码参数目前不支持 NET 格式。

应该有一个选项自动处理 .key 文件，而无需手动编辑它们。

## 参见

(1), (1), (1), (1)

