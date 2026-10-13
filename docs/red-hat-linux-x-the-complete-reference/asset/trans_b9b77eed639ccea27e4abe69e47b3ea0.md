
不同的安全措施将使用通过 `dnssec-keygen` 命令生成的加密密钥。您可以使用 `dnssec-keygen` 创建不同类型的密钥，包括区域（ZONE）、主机（HOST）和用户（USER）密钥。您通过 `-n` 选项指定密钥类型。区域密钥需要指定域名。区域密钥用于 DNSSEC 操作。以下示例为 mytrek.com 区域创建了一个区域密钥：

```bash
dnssec-keygen -n ZONE mytrek.com.
```

要创建主机密钥，您应使用 HOST 类型。HOST 密钥通常用于 TSIG 操作。

```bash
dnssec-keygen -n HOST turtle.mytrek.com.
```

您可以进一步指定加密算法（-a）和密钥长度（-b）。使用 `-h` 选项可以获取 `dnssec-keygen` 选项的列表。目前，您可以从 RSA、DSA、HMAC-MD5 和 DH 算法中进行选择。比特范围将根据算法而异。RSA 的范围从 512 到 4096，HMAC-MD5 的范围从 1 到 512。以下示例使用 768 位密钥和 DSA 加密算法创建一个区域密钥：

```bash
dnssec-keygen -a DSA -b 768 -n ZONE mytrek.com.
```

`dnssec-keygen` 命令将创建公钥和私钥，分别位于带有 `.private` 和 `.key` 后缀的对应文件中。`.key` 文件是一个存储公钥的 KEY 资源记录。对于 DNSSEC，私钥用于生成区域的签名，而公钥用于验证签名。对于 TSIG，使用 HMAC-MD5 算法生成的共享私钥，而不是公钥/私钥对。

## DNSSEC

DNSSEC 为 DNS 提供加密认证。借助 DNSSEC，您可以创建一个带有加密签名的安全标识的签名区域。这种安全形式主要用于保护主 DNS 服务器和从 DNS 服务器之间的连接，以便主服务器仅向授权的从服务器传输更新记录，并以此进行安全的加密通信。建立这种安全连接的两台服务器使用一对公钥和私钥来完成。实际上，您拥有一个父区域，可以通过加密传输安全地认证子区域。这涉及为每个子区域创建区域密钥，并让这些密钥由父区域用于认证子区域。

## 区域密钥

您使用 `dnssec-keygen` 命令生成区域密钥，并通过 `-n` 选项指定区域类型 ZONE。对于密钥名称，您使用区域的域名。以下示例为 mytrek.com 区域创建了一个区域密钥。

```bash
dnssec-keygen -n ZONE mytrek.com.
```

您可以进一步指定加密算法（-a）和密钥长度（-b）。使用 `-h` 选项可以获取 `dnssec-keygen` 选项的列表。由于您正在设置公钥/私钥对，您应选择 RSA 或 DSA 算法。比特范围将根据算法而异。RSA 的范围从 512 到 4096，DSA 的范围从 512 到 1024。以下示例使用 768 位密钥和 DSA 加密算法创建一个区域密钥：

```bash
dnssec-keygen -a DSA -b 768 -n ZONE mytrek.com.
```

`dnssec-keygen` 命令将创建公钥和私钥，分别位于带有 `.private` 和 `.key` 后缀的对应文件中。私钥用于生成区域的签名，而公钥用于验证签名。`.key` 文件是一个存储公钥的 KEY 资源记录。这用于解密由对应私钥生成的签名。您使用 `$INCLUDE` 语句将 `.key` 文件包含到 DNS 配置文件中 `named.conf`，以添加公钥。

## DNSSEC 资源记录

在区域文件中，您然后使用三个 DNSSEC DNS 资源记录来为特定区域实现安全通信：KEY、SIG 和 NXT。在这些记录中，您使用已为区域生成的签名密钥。KEY 记录保存与区域、主机或用户关联的公钥。SIG 记录存储一组资源记录的数字签名和过期日期。NXT 记录用于确定某个域的资源记录不存在。此外，几个实用程序允许您管理 DNS 加密。通过 `dnskeygen` 实用程序，您生成了用于加密的公钥和私钥。`dnssigner` 使用区域的私钥对区域进行签名，从而设置认证。

要使用 DNSSEC 保护 DNS 区域，您首先使用 `dnskeygen` 为 DNS 区域创建公钥和私钥。然后使用 `dnssigner` 创建认证密钥。在 DNS 区域文件中，您输入一个 KEY 资源记录，其中包含公钥。公钥将显示为长串随机字符。对于 KEY 记录，您输入域名，接着是 KEY，然后是公钥。

```text
mytrek.com. KEY 0x4101 3 3 (
AvqYxGkK/uguxkJF/hbRpYzxZFG3x8EFNX38917GX6w7r1Ly
BJ14TqvrDVx84XaShg+OfCUJafNr84U4ER2dggNrlRAMZA1
JFFv0UpWDwCBR2jJngv9qZB2UMGJHeDevytMIKGd2oGk
Aensm7AN1fUqKzy/3KZ9KnQmEpj/EEBr48VasqT9kMjnN+V3
NgAwfqqsG0dwj5OiRJoIR4+cRt+s32OUkSca1AODF2Tdt xRn
vXF3qIVOS8oewMBEwh3trXIlc7nDMQC3RmoY8RVGt5U6LMAQ
KITDyHU3VmrJ36vn77QgSzb eUPz8ZEnbpik8kPykJZFKcyj
jZoHTlxkJltk )
```

对于认证，您可以对特定域名或主机的特定资源记录进行签名。输入域名或主机，接着是术语 SIG，然后是资源记录的签名。

```text
mytrek.com. SIG KEY 3 86400 19990321010705 19990218010705 4932 com. (
Am3tWJzEDzFU1xwg7hzkiJ0+8UQaPtlJhUpQxlSnKpDUqZxm
igMZE Vk= )
```

NXT 记录允许您对查询给出否定回答。

```text
mytrek.com. NXT ftp.mytrek.com. A NS SOA MX SIG KEY NXT
```

## 签名密钥

要在父（主）和子（从）DNS 服务器之间设置安全通信，公钥随后需要发送到父区域。在那里，该密钥可以由父区域签名。由于您可能拥有一个以上的区域密钥，您使用 `dnssec-make keyset` 命令创建密钥集。这将生成一个扩展名为 `.keyset` 的文件，然后将其发送到父区域。然后，父区域使用 `dnssec-signkey` 命令对子区域的密钥集进行签名。这将生成一个前缀为 `signedkey-` 的文件。此文件被发送回子区域，现在包含子区域的密钥集和父区域的签名。一旦子区域拥有 `signedkey-` 文件，`dnssec-signedzone` 命令将生成一个扩展名为 `.signed` 的文件。然后，此文件通过 `INCLUDE` 操作包含在 `named.conf` 文件中。`trusted-keys` 语句需要列出父区域的公钥。

## TSIG 密钥

TSIG（传输签名）也提供安全的 DNS 通信，但它们共享私钥，而不是私钥/公钥对。它们通常用于两个本地 DNS 服务器之间的通信，以及为动态更新（例如 DNS 服务器和 DHCP 服务器之间的更新）提供认证。

**注意** 对于 BIND 8.0，您使用 `dnskeygen` 而不是 `dnssec-keygen`。

## 生成 TSIG 密钥

要为您的 DNS 服务器创建 TSIG 密钥，您使用如上所述的 `dnssec-keygen` 命令。不使用您用于 DNSSEC 的相同密钥，而是创建一套新的用于传输签名的密钥。对于 TSIG，使用共享私钥而不是公钥/私钥对。对于 TSIG 密钥，您使用 HMAC-MD5 算法，该算法在 `.key` 和 `.private` 文件中生成相同的密钥。使用 `-a` 选项指定要使用的 HMAC-MD5 算法，并使用 `-b` 选项指定比特大小（HMAC-MD5 的范围从 1 到 512）。`-n` 选项用于指定密钥类型，在此情况下为 HOST，表示主机名。比特范围将根据算法而异。以下示例使用 128 位密钥和 HMAC-MD5 加密算法创建一个主机密钥：

```bash
dnssec-keygen -a HMAC-MD5 -b 128 -n HOST turtle.mytrek.com
```

这会创建一个私钥和公钥，分别位于 `.key` 和 `.private` 文件中。在 TSIG 方案中，两个主机都使用相同的私钥进行认证。例如，要启用 DHCP 服务器更新 DNS 服务器，两者都需要 TSIG 认证的私钥（密钥）。HMAC-MD5 密钥用作共享私钥，在 `.key` 和 `.private` 文件中生成相同的私钥和公钥。

## 密钥语句

然后，您在 `named.conf` 文件中使用 `key` 语句指定密钥。对于 `algorithm` 选项，您列出 HMAC-MD5 算法；对于 `secret` 选项，您列出私钥。此密钥将列在 `.private` 和 `.key` 文件中。前面的示例将生成名为 `K turtle.mytrek.com.+157.43080.key` 和 `K turtle.mytrek.com.+157.43080.private` 的密钥和私钥文件。`.key` 文件的内容由这里显示的资源记录组成：

```text
turtle.mytrek.com. IN KEY 512 3 157 ONQAfBLnvWU9H8hRqq/WA==
```

私钥文件的内容显示相同的密钥以及算法。

```text
Private-key-format: v1.2
Algorithm: 157 (HMAC_MD5)
Key: ONQAfBLnvWU9H8hRqq/WA==
```

在 `named.conf` 文件中，您然后使用 `key` 语句为密钥命名。

