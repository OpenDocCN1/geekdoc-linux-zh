

其中 *id* 是密码引擎的 ID。要检查引擎的可用性，请执行以下命令：

```bash
~]$ openssl engine -t
```

要对名为 *plaintext* 的数据文件进行签名，请执行如下命令：

```bash
~]$ openssl pkeyutl -sign -in plaintext -out sigtext -inkey privkey.pem
```

要验证签名的数据文件并提取数据，请执行如下命令：

```bash
~]$ openssl pkeyutl -verifyrecover -in sig -inkey key.pem
```

要验证签名，例如使用 DSA 密钥，请执行如下命令：

```bash
~]$ openssl pkeyutl -verify -in file -sigfile sig -inkey key.pem
```

`pkeyutl(1)` 手册页介绍了公钥算法实用工具。

### 使用对称算法

要列出可用的对称加密算法，请使用不支持的选项（例如 -l）执行 `enc` 命令：

```bash
~]$ openssl enc -l
```

要指定算法，请使用其名称作为选项。例如，若要使用 **aes-128-cbc** 算法，请使用以下语法：

```bash
openssl enc -aes-128-cbc
```

若要使用 **aes-128-cbc** 算法加密名为 **plaintext** 的文件，请输入以下命令：

```bash
~]$ openssl enc -aes-128-cbc -in plaintext -out plaintext.aes-128-cbc
```

要解密在前一个示例中获得的文件，请使用 **-d** 选项，如以下示例所示：

```bash
~]$ openssl enc -aes-128-cbc -d -in plaintext.aes-128-cbc -out plaintext
```

> ### **重要说明**
>
> `enc` 命令不正确支持 AEAD 密码，并且 ecb 模式被认为是不安全的。为了获得最佳结果，请勿使用 cbc、cfb、ofb 或 ctr 以外的其他模式。

### 4.7.5. 生成消息摘要

`dgst` 命令生成所提供文件或多个文件的十六进制格式消息摘要。该命令也可用于数字签名和验证。消息摘要命令的形式如下：

```bash
openssl dgst algorithm -out filename -sign private-key
```

其中 *algorithm* 是 `md5|md4|md2|sha1|sha|mdc2|ripemd160|dss1` 之一。在本文撰写时，首选 SHA1 算法。如果您需要使用 DSA 进行签名或验证，则必须将 *dss1* 选项与由 `-rand` 选项指定的包含随机数据的文件一起使用。

若要使用 *sha1* 算法生成默认 Hex 格式的消息摘要，请执行以下命令：

```bash
~]$ openssl dgst sha1 -out digest-file
```

若要使用私钥 *prikey.pem* 对摘要进行数字签名，请执行以下命令：

```bash
~]$ openssl dgst sha1 -out digest-file -sign prikey.pem
```

更多信息请参阅 `man dgst(1)`。

### 4.7.6. 生成密码哈希

*passwd* 命令计算密码的哈希值。要在命令行上计算密码的哈希值，请执行如下命令：

```bash
~]$ openssl passwd password
```

默认使用 `-crypt` 算法。

若要使用基于 MD5 的 BSD 算法 *-1* 从标准输入计算密码的哈希值，请执行如下命令：

```bash
~]$ openssl passwd -1 password
```

*-apr1* 选项指定了 BSD 算法的 Apache 变体。

若要计算存储在文件中的密码的哈希值，并使用盐值 *xx*，请执行如下命令：

```bash
~]$ openssl passwd -salt xx -in password-file
```

*password* 会被发送到标准输出，没有用于指定输出文件的 *-out* 选项。`-table` 将生成一个包含密码哈希值及其对应明文密码的表格。

更多信息和示例请参阅 `man sspasswd(1)`。

### 4.7.7. 生成随机数据

若要生成包含随机数据的文件，并使用种子文件，请执行以下命令：

```bash
~]$ openssl rand -out rand-file -rand seed-file
```

可以使用冒号 `:` 作为列表分隔符，指定多个用于为随机数据进程提供种子的文件。

更多信息请参阅 `man rand(1)`。

### 4.7.8. 对系统进行基准测试

若要测试系统针对特定算法的计算速度，请执行以下格式的命令：

```bash
openssl speed algorithm
```

其中 `algorithm` 是您打算使用的受支持算法之一。要列出可用算法，请输入 `openssl speed`，然后按 Tab 键。

### 4.7.9. 配置 OpenSSL

OpenSSL 具有一个配置文件 `/etc/pki/tls/openssl.cnf`，称为主配置文件，由 OpenSSL 库读取。也可以为每个应用程序拥有单独的配置文件。配置文件包含多个部分，部分名称如下：`[ section_name ]`。注意，文件的第一部分，直到第一个 `[ section_name ]` 为止，被称为默认部分。当 OpenSSL 在配置文件中搜索名称时，首先搜索命名部分。除非在命令中使用选项指定了替代配置文件，否则所有 OpenSSL 命令都使用主 OpenSSL 配置文件。配置文件的详细说明请参阅 `config(5)` 手册页。

两个 RFC 解释了证书文件的内容。它们是：

- 互联网 X.509 公钥基础设施证书和证书吊销列表 (CRL) 规范
- 互联网 X.509 公钥基础设施证书和证书吊销列表 (CRL) 规范更新

## 4.8. 使用 STUNNEL

stunnel 程序是客户端和服务器之间的加密包装器。它监听配置文件中指定的端口，加密与客户端的通信，并将数据转发到监听其常规端口的原始守护进程。通过这种方式，您可以保护本身不支持任何类型加密的任何服务，或者提高使用您出于安全原因希望避免使用的加密类型（例如受 POODLE SSL 漏洞（CVE-2014-3566）影响的 SSL 版本 2 和 3）的服务的安全性。详见 https://access.redhat.com/solutions/1234773。CUPS 是一个不提供在其自身配置中禁用 SSL 方式的分层的示例。

### 4.8.1. 安装 stunnel

以 root 身份输入以下命令来安装 stunnel 包：

```bash
# yum install stunnel
```

### 4.8.2. 将 stunnel 配置为 TLS 包装器

要配置 stunnel，请遵循以下步骤：

- 无论您将 stunnel 与什么服务一起使用，都需要一个有效的证书。如果没有合适的证书，您可以向证书颁发机构申请获取一个，或者创建一个自签名证书。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_102_0.png)

# 警告

对于运行在生产环境中的服务器，请务必使用由证书颁发机构签名的证书。自签名证书仅适用于测试目的或私有网络。

有关证书颁发机构颁发的证书的更多信息，请参阅 *第 4.7.2.1 节，“创建证书签名请求”*。另一方面，要为 stunnel 创建自签名证书，请输入 `/etc/pki/tls/certs/` 目录，并以 *root* 身份输入以下命令：

```bash
certs]# make stunnel.pem
```

回答所有问题以完成过程。

- 2. 当您拥有证书后，为 stunnel 创建配置文件。它是一个文本文件，其中每一行指定一个选项或服务定义的开始。您还可以在文件中保留注释和空行以提高其可读性，其中注释以分号开始。

stunnel RPM 包包含 `/etc/stunnel/` 目录，您可以在其中存储配置文件。虽然 stunnel 不需要文件名或其扩展名的任何特殊格式，但请使用 `/etc/stunnel/stunnel.conf`。以下内容将 *stunnel* 配置为 TLS 包装器：

```ini
cert = /etc/pki/tls/certs/stunnel.pem
; 仅允许 TLS，从而避免 SSL
sslVersion = TLSv1
chroot = /var/run/stunnel
setuid = nobody
setgid = nobody
pid = /stunnel.pid
socket = l:TCP_NODELAY=1
socket = r:TCP_NODELAY=1

[service_name]
accept = port
connect = port
TIMEOUTclose = 0
```

或者，您可以通过将包含 `sslVersion = TLSv1` 的行替换为以下各行来避免使用 SSL：

```ini
options = NO_SSLv2
options = NO_SSLv3
```

选项的用途如下：

- `cert` – 证书的路径

