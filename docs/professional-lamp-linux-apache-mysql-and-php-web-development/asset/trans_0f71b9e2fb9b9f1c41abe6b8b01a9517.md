
## AuthMySQLUserTable *table_name*

这是数据库中存储用户名和密码的表名。如果未指定表，则使用默认值 `user_info`。

## AuthMySQLNameField *column_name*

这是用户表（`AuthMySQLUserTable`）中存储用户名的列名。在 MySQL 中创建表时，请确保该列具有索引或键，以确保每个值都是唯一的。该列的*长度*由您在 MySQL 中决定。默认值为 `user_name`。

## AuthMySQLUserCondition

当 `mod_auth_mysql` 执行用户查找时，它会执行一个简单的 SQL SELECT 语句，其中包含执行匹配所需的任何条件。`AuthMySQLUserCondition` 字段允许您指定用于 SQL 语句 `WHERE` 子句的额外参数。

## AuthMySQLPasswordField *column_name*

这是用户表中存储用户密码的列名。MySQL 中该列的长度应至少与加密密码哈希值一样长。`AuthMySQLPasswordField` 的默认值为 `user_password`。

## AuthMySQLPwEncryption `none` | `crypt` | `scrambled` | `md5` | `aes` | `sha1`

这是在对数据库中密码进行编码时使用的加密方法，具体如下：

- `none`：无加密/明文
- `crypt`：UNIX `crypt()` 加密
- `scrambled`：MySQL `PASSWORD()` 加密
- `md5`：MD5 哈希
- `aes`：高级加密标准 (AES) 加密
- `sha1`：安全哈希算法 (SHA1)

如果未指定值，则使用默认值 `crypt`。

在使用 AES 密码加密时，请确保 MySQL 用户表中的密码字段是 BLOB 类型，而不是 CHAR、VARCHAR 或 BINARY 类型。除非列类型是 BLOB 变体之一，否则 MySQL 将从加密密码中删除多余的编码字符——这将导致永远无法将给定的密码与数据库值匹配。

## AuthMySQLSaltField

这允许您指定三个值之一，用作加密密码时的“盐值”。值为 `<>` 表示 `mod_auth_mysql` 使用密码本身作为盐字段。值为 `<string>` 表示使用 `string` 的值作为盐字段。任何未由小于号/大于号包围的字符串都被视为数据库列的名称，该列的值用作盐字段。

## Chapter 6

## AuthMySQLGroupTable

当 Apache 被告知检查组而不是单个用户（*require group* 对比 *require valid-user*）时，此指令用于设置包含组信息的表名。

## AuthMySQLGroupCondition

类似于 `AuthMySQLUserCondition`，此指令允许您指定在匹配用户组时包含在 **WHERE** 子句中的条件语句。

## AuthMySQLGroupField

这是数据库中包含组名的字段的名称。当使用 Apache 的 *require group* 指令匹配组时，会使用此字段。

## AuthMySQLAuthoritative

这告诉 Apache 在 MySQL 身份验证失败时是否回退到其他模块。

## Apache 和 SSL

通过使用 `htpasswd` 或 `mod_auth_mysql` 使用基本身份验证来保护您的 Web 文件夹可以提高安全性。不幸的是，基本身份验证提供的额外安全层可能会被旨在入侵系统的严重黑客消除。问题在于：当您在标准服务器上使用基本身份验证时，用户名和密码实际上是从客户端未加密地传输到服务器的。精通网络的黑客可能会监控您的机器和服务器之间的传输，并嗅探到明文密码。

解决方案：加密客户端和服务器之间的通信。在 Apache 中，这可以通过使用安全套接字层 (SSL) 来实现。Apache 中的 SSL 以 `mod_ssl` 的形式出现，这是一个 Apache 模块，它使 Apache 控制的网站支持 SSL，允许任何与 Apache 之间的通信使用广泛的加密方案进行加密。

要在 Apache 中启用 SSL，首先检查 SSL 是否包含在现有的 Apache 二进制文件或可加载模块中：

```bash
/path/to/httpd -l
ls /path/to/apache/modules/
```

如果在第一个命令输出中没有看到 `mod_ssl.c`，或在 Apache 模块列表中没看到 `mod_ssl.so`，则需要自己构建 Apache 的 SSL 功能。要静态启用 SSL，请在从源代码构建时向 Apache `configure` 脚本添加 `-enable-ssl`：

```bash
./configure \
--enable-ssl \
# ...以及您使用的任何其他 configure 设置
```

## Apache 技巧

如果您想使用动态模块，只需在启用 SSL 的行末尾添加 `#shared`：

```bash
./configure \
    --enable-ssl=shared \
    # ...以及您使用的任何其他 configure 设置
```

然后，使用 `make` 和 `make install` 构建并安装新的 Apache 二进制文件和模块。如果您将 Apache 构建为动态模块，请在 httpd.conf 的全局配置部分添加以下行以启用它：

```apache
LoadModule ssl_module modules/mod_ssl.so
```

现在您可能已经注意到，粗体提示应替换为您自己的适当值。此外，请确保您输入的共同名称 (Common Name) 是服务器的真实完全限定域名，例如 www.yourserver.com。

命令完成并回答所有提示后，您将得到两个新文件：`privkey.pem`（用于签署证书的私钥）和 `testcert.csr`（证书请求）。下一步是从上一步创建的密钥中移除口令。如果不移除口令，您每次启动 Apache 时都必须输入它。虽然这可能看起来像是额外的安全性，但实际上是个麻烦，因为如果您的服务器遭遇断电或您频繁重启 Apache，它会阻止 Apache 完全重启。

要移除口令，请使用以下命令：

```bash
openssl rsa -in privkey.pem -out testcert.key
```

这将提示您输入在上一个命令开始时使用的相同口令：

```text
Enter pass phrase for privkey.pem:
writing RSA key
```

下一步是将证书请求转换为已签署的证书：

```bash
openssl x509 \
-in testcert.csr \
-out testcert.cert \
-req \
-signkey testcert.key \
-days 3650
```

这将显示：

```text
Signature ok
subject=/C=US/ST=Ohio/L=Cincinnati/O=TestSSL/OU=SSL Testing
 Department/CN=www.example.com/emailAddress=youremail@example.com
Getting Private key
```

您这里所做的使用 openssl 命令请求了一个 X.509 证书，使用 testcert.csr 证书请求作为输入，并将生成的证书保存为 testcert.cert，该证书使用私钥 testcert.key 自签名，有效期为 10 年。

既然您已经拥有了自签名的服务器证书和密钥，您需要将两者都复制到 Apache 可以访问的位置：

```bash
mkdir -p /etc/apache/ssl.crt
mkdir -p /etc/apache/ssl.key
```
