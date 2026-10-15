
该区域将通过 `named.conf` 文件中的 `zone` 语句调用，其格式如下：

```
zone "0.10.in-addr.arpa" IN (
  type master;
  file "example.com.rr"
  allow-update ( none );
)
```

此示例与标准 `zone` 语句之间的区别非常小，区域区域名称。注意，反向域名解析需要通过 `in-addr.arpa` 反转 IP 地址的前三个字节。这允许反向域名解析区域文件中使用的单个 IP 数字块与该区域关联。

## 12.4. 使用 `rndc`

BIND 包含一个工具 `rndc`，它允许从本地或远程主机对 `named` 守护进程进行命令行管理。

为了防止未经授权访问 `named` 进程，BIND 使用密钥方法来授予主机权限。这意味着 `/etc/named.conf` 和 `rndc` 配置文件 `/etc/named.conf` 中必须存在相同的密钥。

### 12.4.1. 配置 `/etc/named.conf`

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

### 12.4.2. 配置 `/etc/rndc.conf`

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
