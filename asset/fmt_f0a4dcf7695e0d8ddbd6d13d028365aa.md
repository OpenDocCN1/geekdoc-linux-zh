
```
struct tty { int tty.tty_locker 000 4 int tty.tty_mutex 004 4 struct tty.tp_virt 008 4 struct tty.tty_rawq 02c 10 int tty.tty_rawq.cmax 010 4 tty.tty_rawq.cxf 014 4 int tty.tty_rawq.clix 038 4 struct tty *tty.tty_rawq.c_001 4 struct tty *tty.tty_c_iop 020 8 unsigned char * tty.tty_rawq.c_buf 024 4 unsigned char * tty.tty_cq.buf_iop 008 4 struct tty.tty_cq.cmax 02c 20 intty.tty_cq.cc 022 4 int tty.tty_cq.cmax 030 4 tty.tty_cq.cxf 034 4 int tty.tty_cq.clix 038 4 struct tty *tty.tty_cq.tp_cpu 03c 4 struct *tty.tty_cq.tp_iop 004 8 unsigned char * tty.tty_cq.buf_cpu 044 8 unsigned char * tty.tty_cq.buf_iop 048 4 struct tty.tty_outq 04c 20 int 000 4 int tty.tty_outq.cc 064 050 4 int tty.tty_outq.clix 054 4 struct tty *tty.tty_outq.c_iop 060 4 unsigned char * tty.tty_outq.c_buf 064 4 unsigned char * tty.tty_outq.buf_iop 068 4 (*int()) tty.tty_oproc 006 6 (*int()) tty.tty_oproc_iop 070 4 (*int())tty.tty.stopproc_cpu 074 4 (*int()) tty.tty.stopproc_iop 078 4 struct thread tty.resel 07c 4
```

实际上，这由特定的选项生成。你可以控制每列的格式，无论你喜欢宽的还是窄的、十六进制还是十进制、前导零或其他。

你只需要一个生成 BSD/GCC 风格 stubs 的 C 编译器。（此处后续大量重复的段落已根据要求未重复翻译）

程序的各个部分相互进行通信等。如果我不需要现场推断这些位符（stabs）的组成，并对我的编译器与 gcc 之间的微小差异进行处理，可能也会有所帮助。

总之，它在这里了。应该可以在 perl v4 或更高版本上运行。也许低版本也可以。

- tom

# C_REHASH

## 名称

`c_rehash` - 为哈希值命的文件创建符号链接

### 概要

```
c_rehash [-old] [-h] [-n] [-v] [directory...]
```

### 描述

`c_rehash` 扫描目录并为指定目录列表中的每个 `.pem`、`.crt`、`.cer` 或 `.crl` 文件计算哈希，并为每个文件创建符号链接，其中链接的名称为哈希值。该实用程序非常有用，因为许多使用 OpenSSL 目录的程序首先按照此顺序设置以查找证书。（如果平台不支持符号链接，则会创建副本。）

如果命令行上指定了任何目录，将按顺序处理。如果没有，将查询环境变量 `SSL_DIRPATH`；它应该是一个由冒号分隔的目录列表。如果未设置该变量，则处理默认目录（特定于安装，但通常为 `/usr/local/ssl/certs`）。

为了处理目录，用户必须拥有该目录的权限，否则将被跳过。创建的链接格式为 `HHHHHNNNN.D`，其中每个 `H` 是十六进制字符，`D` 是一个十进制数字。在处理目录时，`c_rehash` 将首先删除该目录下所有具有此类名称的链接。如果你有其他用途的此类格式链接，它们将被删除。要跳过删除步骤，请使用 `-n` 标志。CRL 的哈希看起来相似，只是字母 `r` 出现在点之后，如下：`HHHHHNNNN.r`。

多个对象可能具有相同的哈希；它们将通过增加 `D` 值来。通过比较完整的 `SHA-1` 指纹可以发现重复项。如果发现重复，将显示警告。

如果存在无法解析为证书或 CRL 的文件，也将显示警告。

该程序使用 `openssl` 程序来计算哈希和指纹。如果在此用户的 PATH 中未找到，则将 `OPENSSL` 环境变量设置为完整路径。可以使用任何程序，它对于证书或 CRL 都将以如下方式调用：

```
$OPENSSL x509 -hash -fingerprint -noout -in FILENAME $OPENSSL crl -hash fingerprint -noout -in FILENAME
```

其中是文件名。它必须在第一行输出文件的哈希，在第二行输出指纹，可选地带有某些文本和等号的前缀。

`FILENAME`

### 选项

- `-old`

为 1.0.0 之前的版本使用旧式哈希（`MD5`，而非 `SHA-1`）来生成链接。请注意，当前版本将不再使用旧式样式。

- `-h`

显示简短的使用信息。

- `-n`

不删除现有的链接。当在同一目录中保留新旧样式链接时，需要此项。

- `-v`

打印关于删除的旧链接和创建的新链接的消息。默认情况下，`c_rehash` 只在处理每个目录时列出它。

## 环境

`OPENSSL`

用于生成哈希和指纹的可执行文件路径（见上文）。

`SSL_CERT_DIR`

要操作的目录分隔列表。如果命令行上列出了目录，则忽略。

### 参见

`openssl(1)`, `crl(1)`. `x509(1)`.

## 名称

`ca` - 示例最小 CA 应用程序

### 概要

```
openssl ca [-verbose] [-config filename] [-name section] [-gencrl] [-revoke file] [-nstatus serial] [-updatedb] [-crl_reason reason] [-crl_hold instruction] [-crl_compromise time] [-crl_CA_compromise time] [-crldays days] [-crlhours hours] [-crelets section] [-startdate date] [-enddate date] [-days arg] [-md arg] [-policy arg] [-keyfile arg] [-keyform PEM|DER] [-key arg] [-passin arg] [-cert file] [-selfsign] [-infile] [-out file] [-notext] [-outdir dir] [-infiles] [-spkac file] [-ss_cert file] [-preserveDN] [-noemailDN] [-batch] [-msie_hack] [-extensions section] [-extfile section] [-engine id] [-subj arg] [-utf8] [-multivalue-rdn]
```

### 描述

`ca` 命令是一个最小的 CA 应用程序。它可以用于签名各种形式的证书请求并生成 CRL，它还维护一个已发布证书及其状态的文本数据库。

选项描述将按每个用途划分。

# CA 选项

- `-config filename`

指定使用的配置文件。

- `-name section`

指定使用的配置部分节（覆盖 `ca` 部分中的默认 `ca`）。

- `-in filename`

输入文件名，包含一个要由 CA 签名的单个证书请求。

- `-ss_cert filename`

一个要由 CA 签名的自签名证书。

- `-spac filename`

一个包含已签名的 Netscape 公钥和要由 CA 签名的额外字段的文件。有关所需的输入和输出格式的信息，请参见 SPKAC FORMAT 部分。

- `-infiles`

如果这应该是最后一个选项，则所有后续参数都被假设为包含证书请求的文件名。

- `-out filename`

输出证书的输出文件。默认是标准输出。证书详情也将输出。

- `-outdir directory`

输出证书的目录。证书将以 `.pem` 格式写入。

- `-cert`

CA 证书文件。

- `-keyfile filename`

用于签名请求的私钥。

- `-keyform PEM|DER`

密钥的格式。默认是 `PEM`。

- `-key password`

用于加密私钥的密码。由于某些系统的限制，应谨慎使用。

- `-selfsign`

指示要签名的已发布证书。如果给了 `-spac`、`-ss_cert` 或 `-gencrl`，则忽略 `-selfsign`。`-selfsign` 的结果是自签名证书出现在证书数据库中。

- `-passin arg`

关键字来源。有关格式的更多信息请参见 `openssl(1)`。

- `-verbose`

这会打印有关正在执行的操作的额外细节。

- `-notext`
