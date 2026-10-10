
私钥密码源。有关 `arg` 格式的更多信息，请参阅 (1) 中的 `PASS PHRASE ARGUMENTS` 部分。

- `-verify` `filename`

  使用“`filename`”中的公钥验证签名。输出为“Verification OK”或“Verification Failure”。

- `-prverify` `filename`

  使用“`filename`”中的私钥验证签名。

- `-signature` `filename`

  要验证的实际签名。

- `-hmac` `key`

  使用“`key`”创建哈希 `MAC`。

### `-mac alg`

创建 MAC（基于密钥的消息认证码）。最受欢迎的 MAC 算法是 `HMAC`（基于哈希的消息认证码），但也存在其他非基于哈希的 MAC 算法，例如由 `ccgost` 引擎支持的 `gost-mac` 算法。MAC 密钥和其他选项应通过 `-macopt` 参数设置。

### `-macopt nm:v`

向由 `-mac` 键指定的 MAC 算法传递选项。以下选项同时被 `HMAC` 和 `gost-mac` 支持：

- `key:string`

  以字母数字字符串形式指定 MAC 密钥（仅当密钥仅包含可打印字符时使用）。字符串长度必须符合 MAC 算法的任何限制，例如对于 `gost-mac` 必须恰好为 32 个字符。

- `hexkey:string`

  以十六进制形式指定 MAC 密钥（每字节两个十六进制数字）。密钥长度必须符合 MAC 算法的任何限制，例如对于 `gost-mac` 必须恰好为 32 个字符。

### `-rand file(s)`

包含用于初始化随机数生成器的随机数据的文件或文件列表，或者一个 `EGD` 套接字（参见 (3)）。可以指定多个文件，使用依赖于操作系统的字符分隔。在 MS-Windows 上分隔符为 `;`，在 OpenVMS 上为 `,`，在其他系统上为 `:`。

### `-non-fips-allow`

即使在 FIPS 模式下，也允许使用非 FIPS 算法，例如 `MD5`。

### `-fips-fingerprint`

使用特定密钥计算 `HMAC`，用于某些 OpenSSL-FIPS 操作。

### `file...`

要摘要的文件。如果未指定文件，则使用标准输入。

### 示例

创建文件的十六进制编码消息摘要：`openssl dgst -md5 -hex file.txt`

使用 SHA-256 对文件进行签名，输出二进制文件：`openssl dgst -sha256 -sign privatekey.pem -out signature.sign file.txt`

验证签名：`openssl dgst -sha256 -verify publickey.pem -signature signature.sign file.txt`

### 注意事项

对于所有新应用，首选的摘要算法是 `SHA1`。然而，其他摘要算法仍被广泛使用。

在签署文件时，`dgst` 会根据私钥的 `ASN.1` 信息自动确定用于签名的算法（`RSA, ECC, 等`）。在验证签名时，它仅处理 `RSA, DSA, 或 ECDSA` 签名本身，而不处理 `x.509, CMS, 和 S/MIME` 格式中用于标识签名者和所用算法的相关数据。

某些签名算法（特别是 `ECDSA` 和 `DSA`）需要随机数源。

只有当签署或验证单个文件时，才应使用签署和验证选项。

无法使用 `openssl` 验证十六进制签名。相反，请使用“`xxd -r`”或类似程序将十六进制签名转换为二进制签名，然后再进行验证。

### RM

### 名称

`rm` - 删除文件或目录

### 概要

```
rm [OPTION]... [FILE]...
```

### 描述

本手册页记录了 `rm` 的 GNU 版本。`rm` 删除每个指定的文件。默认情况下，它不删除目录。

如果提供了 `-I` 或 `--interactive=once` 选项，并且文件多于三个，或者提供了 `-r`、`-R` 或 `--recursive`，则 `rm` 会提示用户确认是否继续整个操作。如果响应不是肯定的，整个命令将被中止。

否则，如果文件不可写，标准输入是终端，且未提供 `-f` 或 `--force` 选项，或者提供了 `-i` 或 `--interactive=always` 选项，`rm` 会提示用户确认是否删除该文件。如果响应不是肯定的，该文件将被跳过。

### 选项

删除（解除链接）`FILE(s)`。

- `-f, --force`

  忽略不存在的文件和参数，从不提示

- `-i`

  在每次删除前提示

- `-I`

  在删除多于三个文件或递归删除前提示一次；比 -i 侵入性小，但仍提供防止大多数错误的保护

- `--interactive[=WHEN]`

  根据 `WHEN` 提示：never（从不）、once（一次，`-I`）或 always（总是，`-i`）；若无 `WHEN`，则总是提示

- `--one-file-system`

  在递归删除层级结构时，跳过位于与相应命令行参数不同的文件系统上的任何目录

- `--no-preserve-root`

  不将 `/` 视为特殊对象

- `--preserve-root`

  不删除 `/`（默认）

- `-r, -R, --recursive`

  递归删除目录及其内容

- `-d, --dir`

  删除空目录

- `-v, --verbose`

  解释正在执行的操作

- `--help`

  显示此帮助并退出

- `--version`

  输出版本信息并退出

默认情况下，`rm` 不删除目录。使用 `--recursive`（`-r` 或 `-R`）选项来删除列出的每个目录及其所有内容。

若要删除文件名以 ‘`-`‘ 开头的文件，例如 ‘`-foo`‘，请使用以下命令之一：

```
rm -- -foo
rm ./*foo*
```

请注意，如果您使用 `rm` 删除文件，在具备足够的专业知识和时间条件下，可能会恢复其部分内容。为了确保内容真正不可恢复，请考虑使用 `shred`。

### 作者

由 Paul Rubin, David MacKenzie, Richard M. Stallman, and Jim Meyering 编写。

### 报告错误

GNU coreutils 在线帮助：<> 向 <> 报告 `rm` 翻译错误。

### 版权

Copyright 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 版本 3 或更高版本 <>。这是自由软件：您可以自由更改和重新分发它。在法律允许的范围内，无保修。

### 参见

(1), (2), (1), (1)

完整文档在：<> 或本地通过：info ‘(coreutils) rm invocation’

### RMDIR

### 名称

`rmdir` - 删除空目录

### 概要

```
rmdir [OPTION]... DIRECTORY...
```

### 描述

如果 `DIRECTORY(ies)` 为空，则删除。

- `-ignore-fail-on-non-empty`

  忽略仅因目录非空而导致的每个失败

- `-p, --parents`

  删除 `DIRECTORY` 及其祖先目录；例如，‘`rmdir -p a/b/c`’ 类似于 ‘`rmdir a/b/c a/b a`’

- `-v, --verbose`

  为每个处理的目录输出诊断信息

- `-help`

  显示此帮助并退出

- `-version`

  输出版本信息并退出

### 作者

由 David MacKenzie 编写。

### 报告错误

GNU coreutils 在线帮助：<> 向 <> 报告 `rmdir` 翻译错误。

### 版权

Copyright 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 版本 3 或更高版本 <>。这是自由软件：您可以自由更改和重新分发它。在法律允许的范围内，无保修。

### 参见

(2)

完整文档在：`<>` 或本地通过：info ‘(coreutils) rmdir invocation’

### rmid

### 名称

`rmid` - 启动激活系统守护进程，使对象能够在 Java 虚拟机 (JVM) 中注册和激活。

### 概要

```
rmid [options]
```

`options`

命令行选项。参见“选项”。

### 描述
