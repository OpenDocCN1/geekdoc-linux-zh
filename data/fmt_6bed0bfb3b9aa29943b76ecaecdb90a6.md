
```
acl mynet { 192.168.0.1; 192.168.0.2; };
```

如果你指定一个范围，例如网络，你也需要通过在这些地址前加一个感叹号（`!`）来将例外添加到列表中。在以下示例中，`mynet` ACL 列出了 `192.168.0.0` 网络中的所有主机，除了 `192.168.0.3`：

```
acl myexceptions { 192.168.0.0; !192.168.0.3; };
```

已经为你定义了四个默认 ACL。你可以在任何选项使用地址列表作为参数的地方使用它们。这些是用于所有主机的 `any`，用于无主机的 `none`，用于所有本地 IP 地址的 `localhost`，以及用于由 DNS 服务器服务的本地网络上所有主机的 `localnet`。

一旦定义了一个列表，你就可以在 `zone` 语句中使用它配合 `allow-query`、`allow-transfer`、`allow-recursion` 和 `blackhole` 选项来控制对区域的访问。`allow-query` 指定可以查询 DNS 服务器的主机。`allow-transfer` 用于主/从区域，指定是否允许更新传输。`allow-recursion` 指定可以在服务器上执行递归查询的主机。`blackhole` 选项将拒绝其列表中任何主机的联系，而不发送拒绝响应。在下一个示例中，创建了一个 `mynet` 的 ACL。然后在 `mytrek.com` 区域中，只允许这些主机查询服务器。由于服务器没有从 DNS 服务器，区域传输完全禁用。`blackhole` 选项拒绝来自 `myrejects` 列表的访问，而不发送任何拒绝通知。

```
acl mynet { 192.168.0.0; };

acl myrejects { 10.0.0.44; 10.0.0.93; };

zone "mytrek.com" {

    type master;

    file "mytrek.com";

    allow-query { mynet; };

    allow-recursion { mynet; };

    allow-transfer { none; };

    blackhole { myrejects; };

};
```

### 密钥

不同的安全措施将使用通过 `dnssec-keygen` 命令生成的加密密钥。你可以使用 `dnssec-keygen` 创建不同类型的密钥，包括区域（`ZONE`）、主机（`HOST`）和用户（`USER`）密钥。你通过 `-n` 选项指定密钥类型。区域密钥需要名称 `ZONE` 和区域域名的名称。区域密钥用于 DNSSEC 操作。以下示例为 `mytrek.com` 区域创建区域密钥：

```
dnssec-keygen -n ZONE mytrek.com.
```

要创建主机密钥，你使用 `HOST` 类型。`HOST` 密钥常用于 TSIG 操作。

```
dnssec-keygen -n HOST turtle.mytrek.com.
```

你可以进一步指定加密算法（`-a`）和密钥大小（`-b`）。使用 `-h` 选项获取 `dnssec-keygen` 选项的列表。目前你可以从 RSA、DSA、HMAC-MD5 和 DH 算法中进行选择。位范围将根据算法而变化。RSA 的范围从 512 到 4096，HMAC-MD5 的范围从 1 到 512。以下示例使用 768 位密钥和 DSA 加密算法创建区域密钥：

```
dnssec-keygen -a DSA -b 768 -n ZONE mytrek.com.
```

`dnssec-keygen` 命令将创建公钥和私钥，每个都在具有后缀 `_.private_` 和 `_.key_` 的相应文件中。`_.key_` 文件是一个持有公钥的 KEY 资源记录。对于 DNSSEC，私钥用于生成区域的签名，公钥用于验证签名。对于 TSIG，使用由 HMAC-MD5 算法生成的共享私钥代替公钥/私钥对。

### DNSSEC

DNSSEC 为 DNS 提供加密身份验证。使用 DNSSEC，你可以创建一个签署的区域，该区域通过加密签名安全地标识。这种安全形式主要用于保护主 DNS 服务器和从 DNS 服务器之间的连接，使得主服务器仅向授权的从服务器传输更新记录，并且通过安全的加密通信进行此操作。建立这种安全连接的两个服务器使用一对公钥和私钥。实际上，你拥有一个父区域，可以安全地认证子区域，使用加密传输。这涉及为每个子区域创建区域密钥，并让这些密钥被父区域用来认证子区域。

### 区域密钥

你使用 `dnssec-keygen` 命令生成区域密钥，并指定区域类型，`ZONE`，使用 `-n` 选项。对于密钥名称，你使用区域的域名。以下示例为 `mytrek.com` 区域创建区域密钥：

```
dnssec-keygen -n ZONE mytrek.com.
```

你可以进一步指定加密算法（`-a`）和密钥大小（`-b`）。使用 `-h` 选项获取 `dnssec-keygen` 选项的列表。由于你正在设置公钥/私钥对，你应该选择 RSA 或 DSA 算法。位范围将根据算法而变化。RSA 的范围从 512 到 4096，DSA 的范围从 512 到 1024。以下示例使用 768 位密钥和 DSA 加密算法创建区域密钥：

```
dnssec-keygen -a DSA -b 768 -n ZONE mytrek.com.
```

`dnssec-keygen` 命令将创建公钥和私钥，每个都在具有后缀 `*.private` 和 `*.key` 的相应文件中。私钥用于生成区域的签名，公钥用于验证签名。`*.key` 文件是一个持有公钥的 KEY 资源记录。这用于解密由相应私钥生成的签名。你将公钥添加到 DNS 配置文件中，`named.conf`，使用 `$INCLUDE` 语句包含 `*.key` 文件。

### DNSSEC 资源记录

在区域文件中，你然后使用三个 DNSSEC DNS 资源记录来为给定区域实现安全通信：`KEY`、`SIG` 和 `NXT`。在这些记录中，你使用已经为区域生成的签署密钥。`KEY` 记录持有与区域、主机或用户相关的公钥。`SIG` 记录存储一组资源记录的数字签名和过期日期。`NXT` 记录用于确定某个域的资源记录不存在。此外，几个实用程序允许你管理 DNS 加密。使用 `dnskeygen` 实用程序，你生成了用于加密的公钥和私钥。`dssigner` 使用区域的私钥签署区域，设置身份验证。

为了使用 DNSSEC 保护 DNS 区域，你首先使用 `dnskeygen` 为 DNS 区域创建公钥和私钥。然后使用 `dssigner` 创建认证密钥。在 DNS 区域文件中，你输入一个 KEY 资源记录，其中包含公钥。公钥将显示为随机字符的长字符串。对于 KEY 记录，你输入域名，后跟 KEY，然后是公钥。

```
mytrek.com. KEY 0x4101 3 3 (AvqYXgk/uguxkJF/hbrP YZxZFG3x8EfnX389L7GX6w7rlLYBJ14TgvrDVXr84XsSxg+OFcUJaFnr84UDRE23dGnrlRAMZA1jFV0UWDWHCR2zjJnvgV92JB2ULMGJheDHeyzM1KG2dOGkAensm74N1FQkZy/3KZ9KnmQmEpj/EEBn48Va5gAT9KmjN+V3
```

对于身份验证，你可以为给定的域或主机签署特定的资源记录。输入域名或主机名，后跟术语 `SIG`，然后是资源记录的签名。

```
mytrek.com. SIG KEY 3 86400 19990321010705 19990218010705 4932 com. (

Am3TW3zEDzfulXwgg7hZkIjO4+8UQApt1JhUpQX1snKpDUpDZxm

igMZEVk= )
```

`NXT` 记录允许你对查询进行否定回答。

```
mytrek.com. NXT ftp.mytrek.com. A NS SOA MX SIG KEY NXT
```
