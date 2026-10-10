
```
acl internals { 172.16.72.0/24; 192.168.1.0/24; };
acl externals { bastion-ips-go-here; };
options {
  ...
  forward only;
  forwarders { // 转发到外部
    servers {
    bastion-ips-go-here;
    };
    allow-transfer { none; }; // 示例 allow
    transfer (no one)
    allow-query { internals; externals; }; // 限制查询访问
    allow-recursion { internals; }; // 限制递归
  ...
};
zone "site.example.com" { // 示例主区域
  type master;
  file "m/sitel.example.com";
  forwarders { }; // 执行正常的迭代
  tion (do not forward)
  allow-query { internals; externals; };
  allow-transfer { internals; };
};
// resolu-
zone "site2.example.com" {
  type slave;
  file "s/site2.example.com";
  masters { 172.16.72.3; };
  forwarders { };
  allow-query { internals; externals; };
  allow-transfer { internals; };
};
zone "site.internal" {
  type master;
  file "m/sitel.internal";
forwarders { };
allow-query { internals; };
allow-transfer { internals; }

zone "site2.internal" {
type slave;
file "s/site2.internal";
masters { 172.16.72.3; };
forwarders { };
allow-query { internals; }
allow-transfer { internals; }
```

外部（堡垒机）DNS 服务器配置：

```
acl internals { 172.16.72.0/24; 192.168.1.0/24; };
 externals { bastion-ips-go-here; };
```

```
options {
...
allow-transfer { none; }; // 示例 allow
transfer (no one)
allow-query { internals; externals; }; // 限制查询访问
allow-recursion { internals; externals; }; // 限制递归
};
```

```
zone "sitel.example.com" { // 示例从用区域
type master;
file "m/sitel.foo.com";
allow-query { any; };
allow-transfer { internals; externals; }
};
```

```
zone "site2.example.com" {
type slave;
file "s/site2.foo.com";
masters { another_bastion_host_maybe; };
allow-query { any; };
allow-transfer { internals; externals; }
};
```

# 第 4 章. 高级概念

在堡垒机（s）上的`resolv.conf`（或等效文件）中：

```
search ...
nameserver 172.16.72.2
nameserver 172.16.72.3
nameserver 172.16.72.4
```

### 4.4. TSIG

这是一份关于在`BIND`中设置基于事务签名（`TSIG`）事务安全性的简短指南。它描述了配置文件的更改，以及不同功能所需的更改，包括创建事务密钥的过程以及在`BIND`中使用事务签名的方法。

`BIND`主要支持用于服务器通信的`TSIG`。这包括区域传输、通知（`notify`）和递归查询消息。较新版本的`BIND 8`解析器对`TSIG`的支持有限。

`TSIG`在动态更新中可能最有用。动态区域的主服务器应该使用访问控制来控制更新，但基于`IP`的访问控制是重要的。基于密钥的访问控制要优得多，请参见建议标准（`Proposed Standards`）。`nupdate`程序通过`-k`和`-y`命令选项支持`TSIG`。

### 4.4.1. 为每对主机生成共享密钥

生成一个要在`host1`和`host2`之间共享的密钥。选择一个任意的密钥名称：`"host1-host2."`。密钥名称在两台主机上必须相同。

#### 4.4.1.1. 自动生成

以下命令将生成一个描述的 128 位（16 字节）`HMAC-MD5`密钥。更长的密钥更好，但用`MD5`更容易处理。注意，最大密钥长度为 512 位；密钥比产生 128 位所需的要长。

```
dnssec-keygen -a hmac-md5 -b 128 -n HOST host1-host2.
```

密钥位于文件`Khost1-host2.+.157+00000.private`中。不直接使用此文件，但可以从文件中提取`"Key:"`随后的`base64`编码字符串并用作共享密钥：

`Key:` `La/E5cG90+0sl1jq0a2da==`

字符串`"La/E5cG90+0sl1jq0a2da=="`可以用作共享密钥。

#### 4.4.1.2. 手动生成

共享密钥仅仅是经过`base64`编码的随机位序列。大多数`ASCII`字符串都是有效的`base64`（假设长度是 4 的倍数且仅使用有效字符），因此可以手动生成共享密钥。

此外，可以将已知字符串通过`mmencode`或类似的程序运行以生成`base64`编码数据。

### 4.4.2. 将共享密钥复制到两台机器

这超出了传输的范围。应该使用安全的传输机制。这可以是安全`FTP`、`ssh`、电话等。

### 4.4.3. 通知服务器密钥的存在

假设`host1`和`host2`都是服务器。在每台服务器的`named.conf`文件中添加以下内容：

```
key host1-host2. {
  algorithm hmac-md5;
  secret "LaESCJG90+0sljqq0a2jdA==";
}
```

算法`hmac-md5`是`BIND`支持的唯一算法。`secret`是上面生成的。由于这是一个密钥，建议`named.conf`不要对全局可读，或者将`key`指令添加到一个对全局不可读且被`named.conf`包含的文件中。

至此，密钥已被识别。这意味着如果服务器接收到由此密钥签名的消息，它可以验证签名。如果签名成功，响应将由相同的密钥签名。

### 4.4.4. 指示服务器使用密钥

由于密钥在两个主机之间共享，必须指示服务器何时使用密钥。在`host1`的`named.conf`文件中添加以下内容，如果`host2`的`IP`地址为`10.1.2.3`：

```
server 10.1.2.3 {
  keys { host1-host2. };
}
```

可以存在多个密钥，但只使用第一个。该指令不包含密钥，因此全局公开。

如果`host1`向该地址发送消息，该消息将使用指定的密钥签名；`host1`将期望响应由相同的密钥签名。

在`host2`的配置文件（带有`host1`的地址）中必须存在类似的语句，以便`host2`签名。

### 4.4.5. `TSIG`密钥访问控制

```
acl internals { 172.16.72.0/24; 192.168.1.0/24; };
 externals { bastion-ips-go-here; };
```

### 4.4.6. 错误

`TSIG`的处理可能会导致多种错误。如果`TSIG`感知服务器接收到未知密钥，将返回`FORMERR`。如果`TSIG`感知服务器接收到无效签名，将返回`BADSIG`。如果`TSIG`感知服务器接收到时间超出允许范围的消息，将返回`BADTIME`。在任何这些情况下，`rcode`均被设置为`NOTAUTH`。

## 第 4 章 高级概念

还必须与父区域和/或子区域的管理员通信，以传输密钥和签名。父区域必须指示一个区域的安全状态，以便支持`DNSSEC`的解析器能够信任其数据。

为了让其他服务器信任此区域中的数据，它们必须是静态地配置此区域的区域密钥，或者配置`DNS`树中该区域之上任何区域的密钥。

### 4.7.1. 生成密钥

`dnskeygen`程序用于生成密钥。

一个安全的区域必须包含一个或多个区域密钥。区域密钥将对区域中的所有记录进行签名，且区域密钥的名称必须与区域相同，类型为`ZONE`，并用于身份验证。建议区域密钥使用`IETF`设计为“强制实施”的加密算法；目前这些算法包括`RSA1`（在`BIND 9.2`中不支持）和`DSA`。

以下命令将为`child.example`区域生成一个 768 位的`DSA`密钥：

```
dnsseckey -a DSA -b 768 -n ZONE.example.
```

将产生两个输出文件：`Rchild.example,+00312345.key`和`Rchild.example,+00312345.private`（其中`12345`是密钥标记示例）。密钥文件名包含了密钥名称（`child.example.`）、算法（`3`是`DSA`，`1`是`RSA`等）以及密钥标记（本例中为`12345`）。私钥（在`.private`文件中）用于生成签名，公钥（在`.key`文件中）用于签名验证。

要生成另一个具有相同属性（但标记不同）的密钥，请重复该命令。

应使用`INCLUDE`语句将公钥插入到区域文件中，包括`.key`文件。

### 4.7.2. 创建密钥集

`dnsmakekeysyset`程序用于从一个或多个密钥创建一个密钥集（`keyset`）。

密钥生成后，必须构建一个密钥集传输给父区域的管理员，以便父区域可以使用其自身的区域密钥对密钥进行签名，并正确指示此区域的安全状态。构建密钥集时，必须指定要包含的密钥列表以及集合的`TTL`，也可以指定父区域签名的预期有效期。

插入密钥集的密钥列表还可能包含位于区域顶部的非区域密钥。`dnssec-makekeyset`也用于区域中的其他名称。

以下命令生成一个包含上述密钥另一个密钥的密钥集，其`TTL`为`3600`，从现在开始的签名有效期为 10 天。

```
dnssec-makekeyset -t 3600 -e +864000 Kchild.example.+003+12345 Kchild.example.+003+23456
```

产生一个输出文件：`keyset-child.example..`。该文件应传输给父区域进行签名。它包含了密钥，以及由区域密钥本身生成的对密钥集的的签名，这些签名用于证明私钥的所有权并确保预期的有效期。

### 4.7.3. 对子密钥集签名

`dnssec-signkey`程序用于对子区域的密钥集进行签名。如果`child.example`有任何安全的委托（例如`grand.child.example`），子区域管理员应接收每个安全子区域的密钥集文件。这些密钥必须由此区域的密钥进行签名。

以下命令使用区域密钥对子密钥集进行签名：

```
dnssec-signkey keyset-grand.child.example. Kchild.example.+003+12345 Kchild.example.+003+23456
```

产生一个输出文件：`signedkey-grand.child.example..`。该文件应既传回子区域又要保留。它包含了来自密钥集文件的所有密钥（子区域密钥）以及由此区域密钥生成的签名。

### 4.7.4. 对区域签名

`dnssec-signzone`程序用于对区域进行签名。将存在对应于安全子区域的任何`signedkey`文件，以及父区域生成的此区域的签名文件（如果有）。区域签名器将为该区域生成`NXT`和`SIG`记录，还将合并父区域的区域密钥签名并在所有委托点指示安全状态。

以下命令对区域进行签名，假设它位于名为`zone.child.example.`的文件中。默认情况下，所有具有私钥的区域密钥都将被用于签名。

```
dnssec-signzone -o child.example zone.child.example
```

产生一个输出文件：`zone.child.example.signed`。该文件应被`named.conf`引用为该区域的输入文件。

### 4.7.5. 配置服务器

与`BIND 8`不同，`BIND 9`在加载时不验证数据，因此权威区域的区域密钥不需要在配置文件中指定。

任何安全根的公钥必须存在于文件的`trusted-keys`语句中，如本文后文所述。

### 4.8. `BIND 9`对`IPv6`的支持

`BIND 9`完全支持所有定义的`IPv6`名称到地址和地址到名称的查找。它将在支持`IPv6`的系统上使用`IPv6`地址进行查询。

对于正向查找，`BIND 9`同时支持`A`和`AAAA`记录。`AAAA`记录的使用已被弃用，但对于主机同时拥有`AAAA`和`A6`记录仍然有用，以保持与仅支持`AAAA`查询的存根解析器的实现向后兼容，因为跟踪`A6`链比执行`AAAA`查询更困难。

对于`IPv6`反向查找，`BIND 9`支持`ipv6.arpa`域使用的新的“位字符串”（`bitstring`）格式，以及在`ipv6`域使用的较旧的“半字节”（`nibble`）格式。`BIND 9`包含一个轻量级解析器，新应用程序可以选择避免跟踪`A6`链位字符串标签的复杂性，见第 5 章。

有关`IPv6`地址格式和结构的概述，请参见第 3 节。

### 4.8.1. 使用`AAAA`记录进行地址查找

`AAAA`记录与`IPv4`记录并行。它在一个记录中指定整个地址。

```
$ORIGIN example.com.

host AAAA fffe:8050:201:80::
```

虽然它们的使用已被弃用，但它们对于支持旧的`IPv6`很有用。不应在不需要的地方添加它们。

### 4.8.2. 使用`A6`记录进行地址查找

`A6`记录比`AAAA`记录更灵活。它在记录中指定整个地址。由于跟踪位字符串标签的链链比执行`AAAA`查询更困难，新应用程序可能选择避免跟踪`A6`链位字符串的复杂性。例如：

```
$ORIGIN example.com.

host AAAA fffe:8050:201:80::
```

### 4.8.3. 使用半字节格式进行地址到名称查找

虽然使用半字节格式查找名称已被弃用，但为了与现有的`IPv6`应用向后兼容，它仍然可用。

在半字节格式下查找时，地址组件简单的反转，就像`IPv4`一样，并附加`ip6.int.`。例如，以下内容为`:3fffe:8050:201:860::1`的主机提供反向查找：

```
$ORIGIN 0.6.8.1.1.0.2.0.5.0.8.f.3.ip6.int.

1.0.0.0.0.0.0.0.2.4.0.0 1400
```

### 4.8.4. 使用位字符串格式进行地址到名称查找

位字符串标签可以在任何位边界开始和结束，而不是在半字节格式的 4 位倍数处。它们还使用`ipv6.arpa`而不是`ip6.int`。

使用位字符串重现之前的示例：

```
$ORIGIN [x3fffe805020021860/64].ip6.arpa.

[x004200000000001/64] 14400 IN PTR host.example.com.
```

### 4.8.5. 使用`DNS`委托`IPv6`反向地址

在`IPv6`中，同一个主机可能具有来自多个网络提供者的多个地址。由于地址的后缀通常保持不变，`DNAME`可以减少需要维护的反向映射区域文件的数量。

例如，考虑一个具有两个供应商（`example.net`和`example2.net`）以及两个`IPv6`地址的主机。由于主机选择自己的 64 位主机地址部分，只有提供者地址是发生变化的。

| host | IN | A6 | 64 | ::1234:5678:1212:5675 cust1.example.net. |
| | IN | A6 | 64 | ::1234:5678:1212:5675 subnet5.example.net. |
| $ORIGIN example.net. | IN | A6 | 48 | 0:0:0:0:::ipv6net.example.net. |
| cust1 | IN | A6 | 0 | aa:bb:cccc: |
| $ORIGIN example2.net. | IN | A6 | 48 | 0:0:0:1::ipv6net.example2.net. |
| ipv6net | IN | A6 | 0 | 6666:5555:54:: |

这设置了正向查询。为了处理反向查询，`example.net`服务商将拥有：

```
$ORIGIN [x0aabbcccc/48].ip6.arpa.

[dddd/16] IN DNAME ipv6-rev.example.com.
```

而`example2.net`将拥有：

```
$ORIGIN [x66665555000/48].ip6.arpa.

[x0001/16] IN DNAME ipv6-rev.example.com.
```

`example.com`只需要一个区域来处理这两种反向映射：

```
$ORIGIN ipv6-rev.example.com.
