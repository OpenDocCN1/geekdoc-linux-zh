
`email_in_dn`

与 `-noemailDN` 相同。如果你想从证书的 DN 中删除 EMAIL 字段，只需将其设置为 `no`。如果不是，默认允许 DN 中有 email 字段。

`msie_hack`

与 `-msie_hack` 相同。

`policy`

与 `-policy` 相同。强制性。更多信息请参见 `POLICY FORMAT` 节。

`name_opt`,`cert_opt`

这些选项允许在请求用户签名时显示证书详情。`x509` 工具支持的所有 `-nameopt` 和 `-certopt` 切换开关均可在此处使用。`no_signame` 和 `no_sigdump` 被永久设置且无法禁用（这是因为此时证书尚未签名，无法显示签名）。

为了方便起见，两者接受 `ca_default` 以产生合理的输出。

如果这两个选项都不存在，则使用早期版本 OpenSSL 的格式。强烈建议不要使用旧格式，因为它只显示策略节中提到的字段，错误地处理多字符字符串类型且不显示扩展。

`copy_extensions`

决定如何处理证书请求中的扩展。如果设置为 `none`（或未出现此选项），则忽略扩展且不复制到证书中。如果设置为 `copy`，则将请求中任何尚未存在的扩展复制到证书中。如果设置为 `copyall`，则将请求中的所有扩展复制到证书中：如果扩展已存在于证书中，则先将其删除。在使用此选项之前请参见 `WARNINGS` 节。

此选项的主要用途是允许证书请求提供扩展（如 `subjectAltName`）的值。

# 策略格式

策略部分由一组与证书 DN 字段对应的变量组成。如果值为“match”，则该字段值必须与 CA 证书中的相同字段匹配。如果值为“supplied”，则该字段必须存在。如果值为“optional”，则该字段可能存在。策略部分中未提到的任何字段都将被静默删除，除非设置了 `-preserveDN` 选项，但这可以更多地看作是一个异常行为而非刻意的设计。

# SPKAC 格式

`-spkac` 命令行选项的输入是一个 Netscape 签名的公钥和挑战。这通常来自 HTML 表单中的 KEYGEN 标签，用于创建新的私钥。然而，也可以使用 `spkac` 工具创建 SPKAC。

该文件应包含设置为 SPKAC 值的变量 `SPKAC`，以及作为键值对（name value pairs）的所需的 DN 组件。如果你需要包含两个相同的组件，可以在其前面加上数字和一个“\”。

在处理 SPKAC 格式时，如果使用了 `-out` 标志，输出为 DER 格式；如果发送到 stdout 或使用 `-outdir` 标志，则输出为 PEM 格式。

## 示例

这些示例假设 ca 目录结构已经建立，且相关文件已经存在。这通常涉及使用 req 创建 CA 证书和私钥、一个序列号文件和一个空索引文件，并将它们放置在相关的目录中。

在使用示例配置文件之前，将创建 `demoCA`、`demoCA/private` 和 `demoCA/newcerts` 目录。CA 证书将复制到 `demoCA/cacert.pem`，其私钥将复制到 `demoCA/private/cakey.pem`。将创建一个文件 `demoCA/serial`，其中包含“01”，以及一个空索引文件 `demoCA/index.txt`。

签名证书请求：

```
openssl ca -in req.pem -out newcert.pem
```

使用 CA 扩展程序签名证书请求：

```
openssl ca -in req.pem -extensions v3_ca -out newcert.pem
```

生成 CRL：

```
openssl ca -gencrl -out crl.pem
```

签名多个请求：

```
openssl ca -infiles req1.pem req2.pem req3.pem
```

认证一个 Netscape SPKAC：

```
openssl ca -spkac.txt
```

一个示例 SPKAC 文件（为了清晰起见，SPKAC 行已截断）：

```
SPKAC:MIG0MGawXANBqJhkkiIGw0BAQEFAANLADBIAKEAnPDhCeV/xIXUg8V70YRXK2A5
CN=Test emailaddress=openssl.org 0.0=OpenSSL Group
1.OU=Another Group
```

包含 CA 相关部分的示例配置文件：

```
[ ] default_ca = CA_default 默认部分 [ CA_default ]
./demoCA # 顶部索引数据库 = $dir/index.txt # 索引文件。new_certs_dir
=$dir/newcerts # 新证书目录 = $dir/cacert.pem # CA证书
s=$dir/serial # 序列号文件 private key = $dir/private/cakey.pem #
CA私钥 RANDFILE = $dir/private/ # 随机数
default_days = 365 # 默认认证有效期
crl_days = 30 # CRL 之前的有效期
next before CRL default = md5 # 使用策略
_policy = any = 默认策略
email_in = no # 不将电子邮件添加到 DN 中
name_opt ca_default # 主体名称显示
copy opt_cert = ca_default # 证书显示
copy extensions = none # 不从请求复制扩展
from request [ _policy_any ] countryName = supplied stateProvinceName =
optional organizationName = optional organizationalUnitName = optional
CommonName = supplied emailAddress = optional
```

### 文件

注意：所有文件的位置都可以通过编译时选项、配置文件条目、环境变量或命令行选项发生变化。下方的值反映了默认值。

```
/usr/local/ssl/lib/openssl.cnf - 主配置文件
./demoCA - 主 CA 目录
./demoCA/cacert.pem - CA 证书
./demoCA/private/cakey.pem - CA 密钥
./demoCA/serial - CA 序列号
./number file ./demoCA/serial.old - CA 私钥 ./demoCA/serial - CA 序列号备份文件
./demoCA/index.txt - CA 文本数据库文件 ./demoCA/index.old - CA 文本
数据库备份文件 ./demoCA/certs - 证书输出文件 ./demoCA/.rnd
- CA 随机种子信息
```

## 环境变量

`OPENSSL_CONF` 反映主配置文件的位置，它可以通过 `-config` 命令行选项覆盖。

# 限制

文本数据库索引文件是过程中的关键部分，如果损坏，则很难修复。理论上，可以从所有已颁发的证书和当前 CRL 重建索引文件：但没有选项可以执行此操作。

目前不支持增量 CRL 等 V2 CRL 特性。

虽然可以一次性输入并处理多个请求，但只能包含一个 SPKAC 或自签名证书。

# Bug

当存在大量证书时，使用内存文本数据库可能会导致问题，因为如所示，数据库必须保持在内存中。

## 示例

取消当前打印作业：`cancel` 取消作业“myprinter-42”：`cancel myprinter-42` 取消所有作业：`cancel -a`

# 注意

希望通过 `-u` 选项防止未经授权取消作业的管理员，应该在 `cupsd.conf(5)` 中对 Cancel-Jobs 操作要求身份验证。

# 另另

`cupsd.conf(5)`, `lp(1)`, `lpmove(8)`, `lpstat(1)`, CUPS 在线帮助 (`http://localhost:631/help`)

# 版权

Copyright © 2007-2014 Apple Inc.

## 名称

`capsh` - 能力 shell 包装器

### 概要

```
capsh [OPTION]...
```

### 描述

可以使用此工具探索和限制 Linux 能力的支持和使用。该工具为某些类型的能力测试和环境创建提供了方便的包装器。它还提供了一些有助于总结能力状态的调试功能。

### 选项

该工具接受多个可选参数，并按照提供的顺序对其进行操作。它们如下：

- `--print`

  显示当前的能力和相关状态。

- `--args`

  带有尾随参数执行 `/bin/bash`。注意，你可以使用 `-c ‘要执行的命令’`执行特定命令。

- `-- ===`

  使用剩余参数再次执行 `capsh`。对于测试 `exec()` 行为很有用。

- `--caps-set`
