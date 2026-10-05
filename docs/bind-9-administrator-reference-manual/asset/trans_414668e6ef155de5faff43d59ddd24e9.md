

# 第 4 章. 高级概念

内部 DNS 服务器配置：

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
```
forwarders { };
allow-query { internals; };
allow-transfer { internals; }

```

```
zone "site2.internal" {
type slave;
file "s/site2.internal";
masters { 172.16.72.3; };
forwarders { };
allow-query { internals; }
allow-transfer { internals; }

```

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

在堡垒机（s）上的 resolv.conf（或等效文件）中：

```
search ...
nameserver 172.16.72.2
nameserver 172.16.72.3
nameserver 172.16.72.4
```

## 4.4. TSIG

这是一份关于在 BIND 中设置基于事务签名（TSIG）事务安全性的简短指南。它描述了配置文件的更改，以及不同功能所需的更改，包括创建事务密钥的过程以及在 BIND 中使用事务签名的方法。

BIND 主要支持用于服务器通信的 TSIG。这包括区域传输、通知（notify）和递归查询消息。较新版本的 BIND 8 解析器对 TSIG 的支持有限。

TSIG 在动态更新中可能最有用。动态区域的主服务器应该使用访问控制来控制更新，但基于 IP 的访问控制是重要的。基于密钥的访问控制要优得多，请参见建议标准（Proposed Standards）。`nupdate` 程序通过 `-k` 和 `-y` 命令选项支持 TSIG。

### 4.4.1. 为每对主机生成共享密钥

生成一个要在 host1 和 host2 之间共享的密钥。选择一个任意的密钥名称：“host1-host2.”。密钥名称在两台主机上必须相同。

#### 4.4.1.1. 自动生成

以下命令将生成一个描述的 128 位（16 字节）HMAC-MD5 密钥。更长的密钥更好，但用 MD5 更容易处理。注意，最大密钥长度为 512 位；密钥比产生 128 位所需的要长。

```
dnssec-keygen -a hmac-md5 -b 128 -n HOST host1-host2.
```

密钥位于文件 `Khost1-host2.+.157+00000.private` 中。不直接使用此文件，但可以从文件中提取 "Key:" 随后的 base64 编码字符串并用作共享密钥：

Key: La/E5cG90+0sl1jq0a2da==

字符串 "La/E5cG90+0sl1jq0a2da==" 可以用作共享密钥。

#### 4.4.1.2. 手动生成

共享密钥仅仅是经过 base64 编码的随机位序列。大多数 ASCII 字符串都是有效的 base64（假设长度是 4 的倍数且仅使用有效字符），因此可以手动生成共享密钥。

此外，可以将已知字符串通过 `mmencode` 或类似的程序运行以生成 base64 编码数据。

### 4.4.2. 将共享密钥复制到两台机器

这超出了传输的范围。应该使用安全的传输机制。这可以是安全 FTP、ssh、电话等。

### 4.4.3. 通知服务器密钥的存在

假设 host1 和 host 2 都是服务器。在每台服务器的 `named.conf` 文件中添加以下内容：

```
key host1-host2. {
  algorithm hmac-md5;
  secret "LaESCJG90+0sljqq0a2jdA==";
}
```

算法 `hmac-md5` 是 BIND 支持的唯一算法。secret 是上面生成的。由于这是一个密钥，建议 `named.conf` 不要对全局可读，或者将 `key` 指令添加到一个对全局不可读且被 `named.conf` 包含的文件中。

至此，密钥已被识别。这意味着如果服务器接收到由此密钥签名的消息，它可以验证签名。如果签名成功，响应将由相同的密钥签名。

### 4.4.4. 指示服务器使用密钥

由于密钥在两个主机之间共享，必须指示服务器何时使用密钥。在 host1 的 `named.conf` 文件中添加以下内容，如果 host2 的 IP 地址为 10.1.2.3：

```
server 10.1.2.3 {
  keys { host1-host2. };
}
```

可以存在多个密钥，但只使用第一个。该指令不包含密钥，因此全局公开。

如果 host1 向该地址发送消息，该消息将使用指定的密钥签名；host1 将期望响应由相同的密钥签名。

在 host2 的配置文件（带有 host1 的地址）中必须存在类似的语句，以便 host2 签名。

### 4.4.5. TSIG 密钥访问控制

acl internals { 172.16.72.0/24; 192.168.1.0/24; };
 externals { bastion-ips-go-here; };

### 4.4.6. 错误

TSIG 的处理可能会导致多种错误。如果 TSIG 感知服务器接收到未知密钥，将返回 FORMERR。如果 TSIG 感知服务器接收到无效签名，将返回 BADSIG。如果 TSIG 感知服务器接收到时间超出允许范围的消息，将返回 BADTIME。在任何这些情况下，rcode 均被设置为 NOTAUTH。

