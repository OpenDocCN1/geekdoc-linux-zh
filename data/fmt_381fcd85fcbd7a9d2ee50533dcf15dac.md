
`type master;`

`file "named.local";`

};

## IPv4 本地主机

用于本地主机反向映射文件的名称通常为 `named.local`，但可以是任何名称。`NS` 记录指定 `localhost` 应使用的名称服务器。该文件有一个 `PTR` 记录，将 IP 地址映射到 `localhost`。用作名称的 `1` 扩展为附加区域域名——在这种情况下，得到 `1.0.0.127`，即反向 IP 地址。`named.local` 文件的内容如下所示。请注意 `localhost` 的尾随点：

```
$TTL 1d

@   IN SOA    localhost.    root.localhost. .

        1997022700    ; Serial

        28800       ; Refresh

        14400       ; Retry

        3600000     ; Expire

        86400 )     ; Minimum

            IN      NS      turtle.mytrek.com.

1             IN      PTR     localhost.
```

## IPv6 本地主机

在 IPv6 中，`localhost` 反向映射使用 IPv6 `localhost` 地址的反转来指定。该地址由 31 个零和一个 1 组成，可以简写为 `::1`，其中 `::` 代表 31 个零的序列。在 IPv6 `IP6.ARPA` 格式中，这些可以写成位级格式，其中前 64 位由全零的网络地址组成，接口地址的值为 1。

```
0000:0000:0000:0000:0000:0000:0000:0001    localhost IPv6 address
[x00000000000000000000000000000001/128]  localhost address
```

在 `named.conf` 文件中，`IP6.ARPA` `localhost` 条目如下所示：

```
zone "[x00000000000000000000000000000001/64].IP6.ARPA"  in {
    type master;
    file "named.ip6.local";
};
```

在本地主机反向映射文件中，`localhost` 条目如下所示：

```
{x0000000000000001/64} IN PTR localhost.
```

## 子域名和从服务器

向 DNS 服务器添加子域名是一件简单的事情：只需在 `named.conf` 文件中创建额外的主条目，然后在主 DNS 服务器的区域文件中放置该子域的名称服务器和权限条目。反过来，子域名有自己的区域文件，包含其 SOA 记录以及列出属于其子域名部分的主机的条目，包括其自身的任何邮件和新闻服务器。

### 子域名区域

子域的名称可以完全是另一个名称，也可以是具有与主域相同后缀的名称。在以下示例中，子域名称为 `beach.mytrek.com`。它同样可以被命名为 `mybeach.com`。在此示例中，该域的名称服务器位于主机 `crab.beach.mytrek.com` 上。其 IP 地址为 `192.168.0.33`，其区域文件为 `beach.mytrek.com`。`beach.mytrek.com` 区域文件保存由此名称服务器服务的所有主机的 DNS 条目。以下示例显示了其 `named.conf` 中的区域条目：

```
zone "beach.mytrek.com" { type master; file "beach.mytrek.com"; };
```

```
zone "1.168.192.IN-ADDR.ARPA" { type master; file "192.168.0"; };
```

### 子域名记录

在主 DNS 服务器上，在示例 `turtle.mytrek.com` 中，你需要在主区域文件中放置条目以识别子域服务器的主机并将其指定为名称服务器。此类条目也称为 *glue records*。在此示例中，你需要在 `turtle.mytrek.com` 上的 `mytrek.com` 区域文件中放置以下条目：

```
beach.mytrek.com. IN NS beach.mytrek.com. beach.mytrek.com. IN A 192.168.0.33.
```

对由 `beach.mytrek.com` 服务的主机的 URL 引用现在可以从由 `mytrek.com` 服务的任何主机访问，后者无需维护关于 `beach.mytrek.com` 主机的任何信息。它只是将这些 URL 引用转发给 `beach.mytrek.com` 名称服务器。

### 从服务器

从 DNS 服务器直接连接到主 DNS 服务器，并定期从中接收 DNS 信息。你使用主 DNS 服务器来配置其从服务器

DNS 服务器自动完成此过程。你对主服务器所做的任何更改都会自动传输到其从服务器。这种信息传输被称为*区域传输*。每当达到从区域的刷新时间或从服务器接收到来自主服务器的通知消息时，就会自动发起区域传输。*刷新时间*是区域 SOA 条目中的第二个参数。每当对主区域配置文件进行更改并重启 `named` 守护进程时，主服务器会自动发送通知消息。实际上，从区域由主区域自动配置，接收主区域的区域文件并将其作为自己的文件使用。

## 从区域

结合前面的示例，假设你想在 `rabbit.mytrek.com` 上设置一个从服务器。如以下示例所示，在 `rabbit.mytrek.com` 上的从 DNS 服务器的 `named.conf` 配置文件中设置区域条目。从服务器运行在与主服务器相同的域名中，因此具有相同的区域名称 `mytrek.com`。其 SOA 文件命名为 `slave.mytrek.com`。文件名中的“slave”仅是一种惯例，有助于将其识别为从服务器配置文件。`masters` 语句列出了其主 DNS 服务器——在本例中为 `192.168.0.1`。每当从服务器需要进行区域传输时，它都会从该主 DNS 服务器传输数据。该从服务器的反向映射文件条目将其反向映射文件列为 `slave.192.168.0`。

```
zone "mytrek.com" {
    type slave;
    file "slave.mytrek.com";
    masters { 192.168.0.1;
    };
}
zone "1.168.192.IN-ADDR.ARPA" {
    type slave;
    file "slave.192.168.0";
    masters { 192.168.0.1;
    };
}
```

## 从记录

在主 DNS 服务器上，主 SOA 区域文件中包含条目，用于标识持有从 DNS 服务器的主机并将其指定为 DNS 服务器。在本示例中，你应将以下内容放入 `mytrek.com` 区域文件：

```
IN   NS  192.168.0.2
```

你还应在 `mytrek.com` 反向映射文件中为该名称服务器放置一个条目：

```
IN   NS  192.168.0.2
```

## 控制传输

主 DNS 服务器可以使用 `allow-transfer` 语句控制哪些从服务器可以从中传输区域信息。请放置该语句，并列出你希望允许访问的从服务器的 IP 地址列表。此外，主 DNS 服务器应确保其 `notify` 选项未被禁用。`notify` 选项会通过 `options` 或 `zone` 条目中的 `"notify no"` 语句被禁用。只需擦除 `"no"` 参数即可启用 `notify`。

### 增量区域传输

在 BIND 8.2.2 和 9.0 版本中，BIND 现在支持增量区域传输（IXFR）。以前，更新时会替换所有区域数据，而不是简单地编辑诸如添加少量资源记录之类的更改。使用增量区域传输时，主区域维护一个更改数据库。然后，仅将更改传输到从区域，从区域使用这些信息来更新其自己的区域文件。为了实现增量区域传输，你需要在 `options` 部分打开 `maintain-ixfr-base` 选项。

```
maintain-ixfr-base yes;
```

然后，你可以在 `zone` 部分使用 `ixfr-base` 选项来指定一个特定的数据库文件以保存更改。

```
ixfr-base "db.mytrek.com.ixfr";
```
