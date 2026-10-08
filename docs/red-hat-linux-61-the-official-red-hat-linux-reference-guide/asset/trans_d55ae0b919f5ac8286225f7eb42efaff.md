

## 第 12 章 伯克利互联网域名 (BIND)

```
604800 ; 过期 1 周
86400 ; 最小 TTL 1 天
```

```
IN NS dns1.example.com.
IN NS dns2.example.com.
```

```
20 IN PTR alice.example.com.
21 IN PTR betty.example.com.
22 IN PTR charlie.example.com.
23 IN PTR doug.example.com.
24 IN PTR ernest.example.com.
25 IN PTR fanny.example.com.
```

该区域将通过 `named.conf` 文件中的 zone 语句调用，其格式如下：

```
zone "0.10.in-addr.arpa" IN (
  type master;
  file "example.com.rr"
  allow-update ( none );
)
```

此示例与标准 zone 语句之间的区别非常小，区域区域名称。注意，反向域名解析需要通过 `in-addr.arpa` 反转 IP 地址的前三个字节。这允许反向域名解析区域文件中使用的单个 IP 数字块与该区域关联。

## 12.4. 使用 rndc

BIND 包含一个工具 `rndc`，它允许从本地或远程主机对 `named` 守护进程进行命令行管理。

为了防止未经授权访问 `named` 进程，BIND 使用密钥方法来授予主机权限。这意味着 `/etc/named.conf` 和 `rndc` 配置文件 `/etc/named.conf` 中必须存在相同的密钥。

### 12.4.1. 配置 /etc/named.conf

为了让 `rndc` 连接到 `named` 服务，BIND 服务器的 `/etc/named.conf` 中必须有一个 `controls` 语句。

示例中的 `controls` 语句允许 `rndc` 从本地连接。

```
controls {
  inet 127.0.0.1 allow { localhost; }; keys <key-name>;
}
```

该语句告诉 `named` 监听回环地址的默认 TCP 端口 953，并在提供正确密钥的情况下允许来自本地的 `rndc` 命令。`<key-name>` 对应于 `/etc/named.conf` 文件中的 `key` 语句。下一个示例说明了一个示例密钥语句。

```
key <key-name> {
  algorithm hmac-md5;
  secret "<key-value>";
}
```

在这种情况下，`<key-value>` 是一个 HMAC-MD5 密钥。使用以下命令生成 HMAC-MD5 密钥：

使用至少 256 位的密钥是一个好主意。应该放置在 `<key-value>` 区域的实际密钥可以在 `<key-file-name>` 中找到。

注意

由于 `/etc/named.conf` 是全局可读的，建议将 `key` 语句放置在仅限 root 读取的独立文件中，然后使用 `include` 语句引用它，如下所示：

```
include "/etc/rndc.conf";
```

### 12.4.2. 配置 /etc/rndc.conf

`key` 语句是 `/etc/rndc.conf` 中最重要的语句。

```
key "<key-name>" {
    algorithm hmac-md5;
    secret "<key-value>";
}
```

`<key-name>` 和 `<key-value>` 应与在 `/etc/named.conf` 中的设置完全相同。

为了匹配目标服务器 `/etc/named.conf` 中指定的密钥，请向 `/etc/rndc.conf` 中添加以下行：

```
options {
    default-server localhost;
    default-key "<key-name>";
}
```

此命令设置了全局默认密钥。但 `rndc` 命令也可以为不同的服务器使用不同的密钥，如下所示：

```
server localhost {
    key "<key-name>";
}
```

注意

确保 root 用户读取或写入 `/etc/named.conf` 中的 `controls` 文件。

### 12.4.3. 命令行选项

`rndc` 命令的格式如下：

```
rndc <options> <command>
```

在本地运行 `named` 上执行 `rndc` 时可以使用以下命令：

- halt — 停止 `named`
- query — 记录查询
- refresh — 刷新 `named`
- reload — 重新加载 `named`
- stats — 导出 `named` 统计信息
- stop — 停止 `named`

`rndc` 还可以使用以下选项进行更新：

- -c <configuration-file> — 告诉 `rndc` 使用配置文件
- -p <port-number> — 指定用于 `rndc` 的端口号
- -s <server> — 告诉 `rndc` 发送到服务器
- -y <key-name> — 指定 `rndc` 使用密钥

## 12.5. BIND 的高级功能

BIND 支持多种方法来保护主服务器和从服务器的区域更新和传输：

### 12.5.1. 协议增强

BIND 支持增量区域传输 (IXFR)，从服务器仅下载主服务器上修改的部分。对于具有大量区域文件和许多从服务器的热门域名，IXFR 减少了通知和更新过程。

注意 IXFR 仅在使用动态更新区域记录时可用。如果手动编辑区域文件，则使用 AXFR。

### 12.5.2. 多视图

通过在 `named.conf` 使用 `view` 语句，BIND 可以根据请求者呈现不同的信息。

这主要用于拒绝本地网络外的特定 DNS 条目，同时允许本地网络内部的查询。

`view` 语句使用 `match-clients` 选项映射 IP 地址或整个网络，并提供特定的选项和区域数据。

### 12.5.3. 安全性

BIND 支持多种方法来保护主从服务器的区域更新和传输：

- DNSSEC — DNS 安全扩展，该功能允许使用密钥对区域进行加密签名。通过这种方式，可以验证特定区域的信息确实来自使用私钥签名的服务器，只要接收方拥有该服务器的公钥。

- TSIG — 事务签名，该功能允许在验证主服务器和从服务器上存在共享密钥后，授权从主到从服务器的传输。

### 12.5.4. IP 版本 6

BIND 版本 9 可以通过 A6 区域记录在 IP 版本 6 (IPv6) 环境中提供名称解析。

