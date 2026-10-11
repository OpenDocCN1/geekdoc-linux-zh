
如果密钥本身需要加密，则必须通过额外选项（例如 `-aes256`）指定加密算法名称。在命令执行期间，`openssl` 会两次提示输入加密密码。

- `-list-standard-commands | list-message-digest-commands | list-cipher-commands | list-cipher-algorithms | list-message-digest-algorithms | list-public-key-algorithms`
列出 `openssl` 支持的命令、算法等。

- `-rand [options] n`
向标准输出写入 `n` 字节的伪随机数据。注意，输出是二进制数据，而不是 ASCII 文本！`-base64` 选项会让 `openssl` 以 ASCII 格式执行 Base64 编码。这会使结果字符串的长度增加约三分之一。

- `-req [options]`
生成一个用于签名证书的请求（即证书签名请求 [CSR] 文件）。使用 `-new`，你可以指定必须设置新证书。`-key` 指定要使用的密钥文件。如果不使用此选项，`openssl` 将为此目的生成一个新的 RSA 密钥，你可以使用 `-keyout` 将其保存到单独的文件。`openssl req -new -sha256 -key server.key -out server.csr` 随后 `openssl` 会以交互方式请求证书密钥数据，即国家代码、位置、你的姓名、主机名（通用名称）等。通过额外的 `-x509 -days n` 选项，`openssl` 将直接生成一个有效期为 `n` 天的自签名证书，而不是证书请求。

- `-rsa [options]`
处理 RSA 密钥，并在不同形式和格式之间生成并转换它们。`-in file` 和 `-out file` 指定读取原始密钥的文件和写入新密钥的文件。如果你不指定任何额外选项，`openssl` 将移除密钥的加密（口令）。密钥的格式可以通过 `-inform` 和 `-outform` 指定（默认是 PEM 或 DER）。通过 `-in file -text`，你可以确定现有密钥的属性，例如密钥长度。

- `-sclient [options]`
作为 SSL/TLS 客户端测试与加密服务器的连接。你可以在以下地址找到示例：`https://www.misterki.com/openssl-s-client`

- `-speed`
执行多次基准测试。结果显示在相应的硬件上处理了多少字节（处理得越多，硬件运行得越快）。

- `-x509 [options]`
显示证书数据、签名证书并在不同格式之间转换证书。`-in` 和 `-out` 指定源证书和目标证书的文件。使用 `-req`，`openssl` 期望输入一个证书请求而非证书本身。`-CA` 指定用于签名的 CA 证书。`-CAkey` 指定对应的私钥。

`openssl` 命令有独立的 man 手册。`req` 描述 `rsa` 的选项。

## 示例

如果你想让官方证书机构（例如）为你的 Web 服务器签名证书，你应该首先生成密钥，然后生成证书签名请求。密钥在这里不是加密的，否则 Web 服务器每次启动时都会询问加密密码。

```
root# genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out server.key
```

```
root# chmod 400 server.key
```

```
root# openssl req -new -key server.key -out server.csr
```

通用名称 (Common Name): `company.com`

你可以查看 CSR 文件来检查此：

```
root# openssl req -in server.csr -text
```

然后，你需要将 CSR 文件发送给证书机构。你将从那里获得签名的证书。通常的文件标识是 `.pem` 或 `.crt`。你必须在 Apache 配置中输入此文件以及来自证书机构的 CA 证书。

```apache
# Apache 配置文件

CertificateFile /etc/apache2/server.pem

CertificateKeyFile /etc/apache2/server.key

CertificateChainFile /etc/apache2/sub.ca.pem

File /etc/apache2/ca.pem
```

如果你不想为官方签名付费，可以自己签名证书：

```bash
root# openssl x509 -req -days 1900 -in server.csr -signkey server.key -sha256 -out server.pem

Signature ok

subject=/C=DE/L=Boston/O=John Doe/CN=www.company-abc.com/

emailAddress=webmaster@company-abc.com/
```

### 获取私钥

要查看证书文件，你可以运行 `openssl x509 -in server.pem -text`：

```bash
root# openssl x509 -in server.pem -text

Certificate:

Data:

Version: 3 (0X1)

Serial Number: 1

Signature Algorithm: sha256WithRSAEncryption

Subject: C=DE/L=Boston/O=John Doe/CN=www.company-abc.com/

emailAddress=webmaster@company-abc.com/

Issuer: C=DE/L=Boston/O=John Doe/CN=www.company-abc.com/

Algorithm: sha256WithRSAEncryption

Validity:

	Before: Jan 1 00:00:00 2024 GMT

	Not After: Sep 27 23:59:59 2029 GMT
```

```
pactl command [parameter]
```

`pactl` 控制 PulseAudio 系统。这个支持网络的音频服务器默认安装在大多数 Linux 发行版中，并通常使用 ALSA 作为基础。PulseAudio 让多个程序能够并行使用音频系统而不会产生任何问题。`pactl` 包含约 30 条命令，此处仅列出了其中最重要的：

- `info|stat`
显示 PulseAudio 系统的关键数据或内存消耗情况。

- `list [short] [modules|sinks|sources|clients|cards|...]`
提供由 PulseAudio 管理的所有模块、音频源和输出端、流等详细描述。额外的 `short` 关键字可以将输出简化为每个元素一行。通过指定模块或输出端（sinks）等，`pactl` 只列出相关元素。

- `set-default-sink n`
定义默认音频输出。除了音频系统的编号 `n`（参见 `/proc/asound/cards`），你也可以输入其名称。可以使用 `pactl list short cards` 确定允许的名称。

- `set-sink-mute n 0|1|toggle`
取消、激活或切换音频输出 `n` 的静音功能。

- `set-sink-volume n`
设置音频输出 `n` 的音量。音量可以指定为整数、百分比或分贝值（例如 `10%` 或 `20dB`）。

## 示例

以下两条命令将第一个音频设备作为标准输出设备，音量设为 20%：

```
user$ pactl set-default-sink 0
```

```
user$ pactl set-sink-volume 0 20%
```

```
pandoc [options] in1 [in2 in3 ...] [> out]
```
