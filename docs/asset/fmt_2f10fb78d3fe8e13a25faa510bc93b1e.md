
``` 
zone "0.in-addr.arpa" IN {

  type master;

  file "named.empty"

  allow-update ( none );

};
```

# Localhost 反向映射：`named.loopback`

`localhost` 反向映射文件实现了名为 `localhost` 的本地回环接口的反向映射。该文件命名为 `named.loopback`。它被 IPv4 和 IPv6 映射区域引用。

在该文件的 IPv4 区域语句中，区域名称为 `0.0.127.in-addr.arpa`。IP 地址的域名部分反序输入，并附加 `in-addr.arpa`，即 `0.0.127.in-addr.arpa`。这里显示了 `named.rfc1912.zones` 的条目：

```
zone "0.0.127.in-addr.arpa" {

  type master;

  file "named.loopback";

  allow-update { none };

};
```

对于 IPv6 区域语句，Fedora 的实现使用了半字节格式（nibble format）处理反向地址：`0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa`。这里显示了 IPv6 区域语句：

```
zone "0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa" IN {

  type master;

  file "named.loopback";

  allow-update { none };

}
```

`named.loopback` 区域同时支持 IPv4 和 IPv6 地址。`NS` 记录指定了应该使用的名称服务器。该文件有一个 `PTR` 记录，将 IP 地址映射到 `localhost`。这里显示了 `named.localhost` 文件的内容：

```
$TTL 1D

IN SOA @ rname.invalid. (

    0 ; serial

    1D ; refresh

    1H ; retry

    1W ; expire

    3H ) ; minimum

  NS @
```

## IP 虚拟域名

基于 IP 的托管允许单台机器使用多个 IP 地址。如果一台机器注册了两个 IP 地址，可以使用其中任何一个来寻址该机器。如果你想将额外的 IP 地址视为域名中的另一个主机，只需在域名的区域文件中为它创建一个地址记录（address record）即可。该主机的域名将与你的域名相同。如果你想为这个额外的 IP 使用不同的域名，则必须为它设置一个虚拟域名。这需要为它创建一个带有独立 zone 文件的新区域语句。例如，如果额外的 IP 是 `192.168.0.42`，且你想给它分配 `sail.com` 域名，你必须为它创建一个名为新 zone 文件的区域语句。该区域语句看起来如下：`sail.com`：

```
zone "sail.com" {

    type master;

    file "sail.com.db";

};
```

在 `sail.com` 文件中，服务器名为 `turtle.mytrek.com`，邮箱地址是 `hostmaster@turtle.mytrek.com`。在名称服务器 (`NS`) 记录中，名称服务器是 `turtle.mytrek.com`。这与名称服务器运行的原始地址是同一台机器：`turtle.mytrek.com` 也是处理发往 `sail.com` 邮件 (`MX`) 的主机。随后，地址记录将额外的 IP 地址 `192.168.0.42` 与 `sail.com` 域名关联。该域名上的虚拟主机随后定义为 `jib.sail.com`。此外，还该主机创建了 `www` 和 `ftp` 别名，形成了 `www.sail.com` 和 `ftp.sail.com` 虚拟主机。

`sail.com` 的权威数据

```
TTL 1d

 hostmaster.turtle.mytrek.com. (

93071200 ; Serial (yyymddxx)

108000 ; Refresh 3 hours

3600 ; Retry 1 hour

3600000 ; Expire 1000 hours

86400 ; Minimum 24 hours

IN NS 10 turtle.mytrek.com.

IN MX 10 turtle.mytrek.com.

IN A 192.168.0.42 ; address of the sail.com domain

IN A 192.168.0.42

www IN A 192.168.0.42 CAME jib.sail.com.

tftp IN A 192.168.0.42 CAME jib.sail.com.
```

在你的反向映射文件 (`/var/named/1.168.192`) 中，为任何虚拟域名添加 `PTR` 记录。

```
42.168.192 IN PTR sail.com.

42.168.192 IN PTR jib.sail.com.
```
