
输入私钥文件（如果存在）和输出私钥文件（如果将创建一个）的密码。命令行选项 `passin` 和 `passout` 会覆盖配置文件中的值。

### `default_bits`

这指定默认的密钥位数。如果未指定，则使用 512。当使用 `-new` 选项时，会使用该值。可以使用 `-newkey` 选项进行覆盖。

### `default_keyfile`

这是写入私钥的默认文件名。如果未指定，密钥将写入标准输出。可以使用 `-keyout` 选项进行覆盖。

### `oid_file`

这指定包含额外 `OBJECT IDENTIFIERS` 的文件。文件的每一行应由对象标识符的数值形式组成，后跟空白，然后是短名称，后跟空白，最后为长名称。

### `oid_section`

这指定配置文件中包含额外对象标识符的部分。每一行应由对象标识符的短名称组成，后跟 `=` 和数值形式。使用此选项时，短名称和长名称相同。

### `RANDFILE`

这指定放置随机数种子信息并从中读取的文件名，或 EGD 套接字（参见 `RAND_egd(3)`）。它用于私钥生成。

### `encrypt_key`

如果设置为 `no`，则如果生成私钥，它 **不会** 被加密。这等效于命令行选项 `-nodes`。为了兼容性，`encrypt_rsa_key` 是一个等效选项。

### `default_md`

此选项指定使用的摘要算法。可能的值包括 `md5`、`sha1`、`mdc2`。如果不存在，则使用 `MD5`。此选项可以通过命令行覆盖。

### `string_mask`

此选项屏蔽某些字段中特定字符串类型的使用。大多数用户不需要更改此选项。

它可以设置为几个值：

- `default`（也是默认选项）使用 PrintableStrings、T61Strings 和 BMPStrings。
- 如果使用 `pkix` 值，则仅使用 PrintableStrings 和 BMPStrings。这遵循 RFC2459 中的 `PKIX` 建议。
- 如果使用 `utf8only` 选项，则仅使用 UTF8Strings；这是 RFC2459 中 2003 年之后的 PKIX 建议。
- 最后，`nostr` 选项仅使用 PrintableStrings 和 T61Strings：某些软件在使用 BMPStrings 和 UTF8Strings 时存在问题；特别是 Netscape。

### `req_extensions`

这指定配置文件中包含要添加到证书请求中的扩展列表的部分。可以使用 `-reqexts` 命令行开关进行覆盖。有关扩展部分格式的详细信息，请参阅 (5) 手册页。

### `x509_extensions`

这指定配置文件中包含要添加到使用 `-x509` 开关生成的证书中的扩展列表的部分。可以使用 `-extensions` 命令行开关进行覆盖。

### `prompt`

如果设置为值 `no`，则禁用证书字段的提示，并直接从配置文件获取值。它还更改 `distinguished_name` 和 `attributes` 部分的预期格式。

### `utf8`

如果设置为值 `yes`，则字段值被解释为 UTF8 字符串。默认情况下，它们被解释为 ASCII。这意味着字段值，无论是从终端输入还是从配置文件获取，都必须是有效的 UTF8 字符串。

### `attributes`

这指定包含任何请求属性的部分：其格式与 `distinguished_name` 相同。通常，这些可能包含 `challengePassword` 或 `unstructuredName` 类型。目前 OpenSSL 的请求签名工具会忽略它们，但某些 CA 可能需要它们。

### `distinguished_name`

这指定包含在生成证书或证书请求时提示的鉴别名称字段的部分。其格式在下一节中描述。

## 可区分的名称和属性部分格式

可区分名称和属性部分有两种不同的格式。如果 `prompt` 选项设置为 `no`，则这些部分仅由字段名和值组成：例如，

```
CN=My Name OU=My Organization emailAddress=
```

这允许外部程序（例如基于 GUI 的程序）生成包含所有字段名和值的模板文件，并直接将其传递给 `req`。此类配置文件的示例包含在 EXAMPLES（示例）部分中。

或者，如果 `prompt` 选项缺失或未设置为 `no`，则文件将包含字段提示信息。它由以下形式的行组成：

```
fieldName="prompt" fieldName_default="default field value" fieldName_min= 2 fieldName_max= 4
```

`fieldName` 是正在使用的字段名称，例如 `commonName`（或 `CN`）。`prompt` 字符串用于请求用户输入相关信息。如果用户未输入任何内容，则使用默认值；如果不存在默认值，则省略该字段。即使存在默认值，如果用户仅输入 `,` 字符，字段仍可被省略。

输入的字符数必须在 `fieldName_min` 和 `fieldName_max` 限制之间：基于所使用的字段可能还存在额外的限制（例如 `countryName` 的长度只能为两个字符，并且必须适合 PrintableString）。

因此，字段（如 `organizationName`）可以在 DN 中使用多次。这带来了一个问题，因为配置文件无法识别同一名称出现两次的情况。为了避免这个问题，如果 `fieldName` 包含某些字符后跟一个句号，它们将被忽略。因此，例如，通过将其称为 `1.organizationName` 可以输入第二个 `organizationName`。

实际允许的字段名称是任何对象标识符的短名称或长名称。这些被编译到 OpenSSL 中，并包括通常的值，如 `commonName`、`countryName`、`localityName`、`organizationName`、`organizationUnitName`、`stateOrProvinceName`。此外，还包含 `emailAddress` 以及 `name`、`surname`、`givenName`、`initials` 和 `dnQualifier`。

可以通过配置文件中的 `oid_file` 或 `oid_section` 选项定义额外的对象标识符。任何额外字段都将被视为 DirectoryString 处理。

## 示例

检查和验证证书请求：

`openssl req -in req.pem -text -verify -noout`

创建私钥，然后从中生成证书请求：

`openssl genrsa -out key.pem 1024; openssl req -new -key key.pem -out req.pem`

相同的效果，但仅使用 `req`：

`openssl req -newkey rsa:1024 -keyout key.pem -out req.pem`

生成自签名根证书：

`openssl req -x509 -newkey rsa:1024 -keyout key.pem -out req.pem`

`oid_file` 选项指向的文件示例：

```
1.2.3.4 shortName A longer Name
1.2.3.6 otherName Other longer Name
```

利用变量扩展的 `oid_section` 指向的部分示例：

```
testoid1=1.2.3.5
testoid2=${testoid1}.6
```

提示字段值的示例配置文件：
