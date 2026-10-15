
最初的 Samba man 页由 Karl Auer 撰写。man 页源码被转换为 YODL 格式（另一种优秀的开源软件，可在 [link missing] 获取），并由 Jeremy Allison 为 Samba 2.0 版本进行更新。Samba 2.2 版本转换为 DocBook 的工作由 Gerald Carter 完成。Samba 3.0 版本转换为 DocBook XML 4.2 的工作由 Alexander Bokovoy 完成。

## SMBGET

### 名称

`smbget` - 用于通过 SMB 下载文件的类似 wget 的工具

### 概要

```
smbget [-a, --guest] [-r, --resume] [-R, --recursive] [-u, --username=STRING] [-p, --password=STRING] [-w, --workgroup=STRING] [-n, --nonprompt] [-d, --debuglevel=INT] [-D, --dots] [-P, --keep-permissions] [-o, --outfile] [-f, --rcfile] [-q, --quiet] [-v, --verbose] [-b, --blocksize] [-O, --stdout] [-U, --update] [-?, --help] [--usage] { [url]... }
```

### 描述

此工具是 `smbclient(7)` 套件的一部分。

`smbget` 是一个具有类似 wget 语义的简单工具，可以从 SMB 服务器下载文件。你可以在命令行中指定想要下载的文件。

文件应遵循 smb-URL 标准，例如，对于 UNC 路径 `\\HOST\SHARE\file`，请使用 `smb://HOST/SHARE/file`。

### 选项

- `-a, --guest`

  以 guest 用户身份工作

- `-r, --resume`

  自动恢复中断的文件

- `-R, --recursive`

  递归下载文件

- `-u, --username=STRING`

  要使用的用户名

- `-p, --password=STRING`

  要使用的密码

- `-w, --workgroup=STRING`

  要使用的工作组（可选）

- `-n, --nonprompt`

  不询问任何问题（非交互式）

- `-d, --debuglevel=INT`

  要使用的调试级别

- `-D, --dots`

  显示点作为进度指示

- `-P, --keep-permissions`

  在本地文件上设置与远程文件上设置的 samba 权限相同。

- `-o, --outfile`

  将正在下载的文件写入指定的文件。不能与 `-R` 一起使用。

- `-O, --stdout`

  将正在下载的文件写入标准输出。

- `-f, --rcfile`

  使用指定的 rcfile。它将按指定顺序加载 - 例如，如果你在此选项之前指定任何选项，它们可能会被 rcfile 的内容覆盖。

- `-q, --quiet`

  保持安静

- `-v, --verbose`

  详细显示

- `-b, --blocksize`

  块中下载的字节数。默认为 64000。

- `-?, --help`

  显示帮助信息

- `--usage`

  显示简短的使用信息

- `-U, --update`

  仅当远程文件比本地文件新或本地文件缺失时下载。

- `-e, --encrypt`

  此命令行参数要求远程服务器支持 UNIX 扩展或已选择 SMB3 协议。请求加密连接。使用 SMB3 或通过 GSSAPI 使用 POSIX 扩展进行 SMB 加密协商。使用给定的凭据进行加密协商（如果提供了域/用户名/密码三元组，则使用 kerberos 或 NTLMv1/v2）。如果无法协商加密，则连接失败。

### SMB URLs

SMB URL 应按以下格式指定：

`smb://<server>/*`

`<server>`: 名称，如果名称是工作组，则是此工作组中的所有服务器；或者如果名称是服务器，则是此服务器上的所有共享。

### 示例

- 递归下载 'src' 目录： `smbget -R smb://server/share/src`

- 下载 FreeBSD ISO 并启用恢复： `smbget -r smb://server/share/FreeBSD-iso`

- 递归下载所有 ISO： `smbget -Rr smb://server/share/*iso`

- 备份 rthonwyn 上的我的数据： `smbget -Rr smb://rthonwyn/share`

### 缺陷

在某些情况下，当错误原因未知时（例如非法格式化的 smb: url 或未开启 `-R` 选项却试图获取目录），会返回权限拒绝。

### 版本

此 man 页适用于 Samba 套件的 3 版本。

### 作者

最初的 Samba 软件和相关工具由 Andrew Tridgell 创建。Samba 现在由 Samba 团队作为一个开源项目进行开发，其开发方式类似于 Linux 内核。

`smbget` man 页由 Jelmer Vernooij 撰写。

## SMIME

### 名称

`openssl smime` - S/MIME 工具

### 概要

```
openssl smime [-encrypt] [-decrypt] [-sign] [-resign] [-verify] [-pk7out] [-cipher] [-in file] [-CAfile file] [-CApath dir] [-trusted_first] [-no_alt_chains] [-certfile file] [-signer file] [-recip file] [-inform SMIME|PEM|DER] [-passin arg] [-inkey file] [-out file] [-outform SMIME|PEM|DER] [-content file] [-to addr] [-from addr] [-subject s] [-text] [-indef] [-noindir] [-stream] [-rand file(s)] [-md digest] [cert.pem],...
```

### 描述

`smime` 命令处理 S/MIME 邮件。它可以加密、解密、签名和验证 S/MIME 消息。

### 命令选项

共有六个操作选项用于设置要执行的操作类型。其他选项的含义根据操作类型而异。

- `-encrypt`

  为指定的收件人证书加密邮件。输入文件是待加密的消息。输出文件是 MIME 格式的加密邮件。

- `-decrypt`

  使用提供的证书和私钥解密邮件。输入文件应为 MIME 格式的加密邮件消息。解密后的邮件将被写入输出文件。

- `-sign`

  使用提供的证书和私钥对邮件进行签名。输入文件是待签名的消息。MIME 格式的已签名消息将被写入输出文件。

- `-verify`

  验证已签名的邮件。输入应为已签名的邮件消息，并输出已签名的数据。支持明文和不透明签名两种方式。

- `-pkcs7out`

  获取输入消息并输出 PEM 编码的 PKCS#7 结构。

- `-resign`

  重新签名消息：获取现有消息和一个或多个新的签名者。

- `-in 文件名`

  待加密或签名的输入消息，或待解密或验证的 MIME 消息。

- `-inform S/MIME|PEM|DER`

  指定 PKCS#7 结构的输入格式。默认值为 `S/MIME`，即读取 S/MIME 格式的消息。`PEM` 和 `DER` 格式会将此更改为期望 `PEM` 和 `DER` 格式的 PKCS#7 结构。目前，这仅影响 PKCS#7 结构的输入格式；如果没有输入 PKCS#7 结构（例如使用 `-encrypt` 或 `-sign` 时），此选项无效。

- `-out 文件名`

  已解密或验证的消息文本，或者是已签名或验证的输出 MIME 格式消息。

- `-outform S/MIME|PEM|DER`

  指定 PKCS#7 结构的输出格式。默认值为 `S/MIME`，即写入 S/MIME 格式的消息。`PEM` 和 `DER` 格式会将此更改为写入 `PEM` 和 `DER` 格式的 PKCS#7 结构。目前，这仅影响 PKCS#7 结构的输出格式；如果没有输出 PKCS#7 结构（例如使用 `-verify` 或 `-decrypt` 时），此选项无效。

- `-stream -indef -noindef`
