
从 DNS 服务器直接绑定到主 DNS 服务器，并定期从其接收 DNS 信息。你使用主 DNS 服务器自动配置其从 DNS 服务器。对主服务器所做的任何更改都会自动传输到其从服务器。这种信息传输称为区域传输。区域传输会在从服务器的刷新时间到达时或从服务器收到主服务器的通知消息时自动启动。刷新时间是区域 SOA 条目中的第二个参数。通知消息会在对主区域配置文件进行更改并重新启动 `named` 守护进程时由主服务器自动发送。实际上，从区域由主区域自动配置，接收主区域的区域文件并将其作为自己的文件使用。

## 从区域

使用前面的示例，假设你想在 `rabbit.mytrek.com` 上设置一台从服务器。如下例所示的区域条目设置在 `rabbit.mytrek.com` 的从 DNS 服务器的 `named.conf` 配置文件中。从服务器在与主服务器相同的域中运行，因此它具有相同的区域名称 `mytrek.com`。其 SOA 文件名为 `slave.mytrek.com`。文件名中的“slave”只是便于识别为从服务器配置文件的一种约定。`masters` 语句列出了其主 DNS 服务器——在本例中为 `192.168.0.1`。每当从服务器需要进行区域传输时，它都会从该主 DNS 服务器传输数据。该从服务器的反向映射文件条目将其反向映射文件列为 `slave.192.168.0`。

```
zone "mytrek.com" {
    type slave;
    file "slave.mytrek.com";
    masters { 192.168.0.1;
    };
}
```

```
zone "1.168.192.IN-ADDR.ARPA" {
    type slave;
    file "slave.192.168.0";
    masters { 192.168.0.1;
    };
}
```

## 从属记录

在主 DNS 服务器上，主 SOA 区域文件中有条目用于标识持有从属 DNS 服务器的主机并将其指定为 DNS 服务器。在本示例中，你将在 `mytrek.com` 区域文件中放置以下内容：

```
IN    NS    192.168.0.2
```

你还需要在 `mytrek.com` 反向映射文件中为此名称服务器放置一个条目：

```
IN    NS    192.168.0.2
```

## 控制传输

主 DNS 服务器可以使用 `allow-transfer` 语句控制哪些从属服务器可以从其传输区域信息。将该语句与要允许访问的从属服务器的 IP 地址列表一起放置。此外，主 DNS 服务器应确保其 `notify` 选项未被禁用。`notify` 选项由 `options` 或 `zone` `named.conf` 条目中的 `"notify no"` 语句禁用。只需删除 `"no"` 参数即可启用 `notify`。

## 增量区域传输

使用 BIND 版本 8.2.2 和 9.0，BIND 现在支持增量区域传输（IXFR）。以前，更新时所有区域数据都会被替换，而不是像添加几个资源记录这样的更改只是被编辑进去。使用增量区域传输，主区域会维护一个更改数据库。然后只将更改传输到从属区域，从属区域使用此信息更新其自己的区域文件。要实现增量区域传输，你需要在 `options` 部分打开 `maintain-ixfr-base` 选项。

```
maintain-ixfr-base yes;
```

然后你可以在 `zone` 部分使用 `ixfr-base` 选项指定一个特定的数据库文件来保存更改。

```
ixfr-base "db.mytrek.com.ixfr";
```

## IP 虚拟域

基于 IP 的虚拟主机允许为一台机器使用多个 IP 地址。如果一台机器有两个已注册的 IP 地址，任一地址都可用于寻址该机器。如果你想将额外的 IP 地址作为域中的另一个主机来处理，你只需在域的区域文件中为其创建一个地址记录。主机的域名将与你的域名相同。但是，如果你想为额外的 IP 使用不同的域名，则必须为其设置虚拟域。这需要为其创建新的 `zone` 语句并使用自己的区域文件。例如，如果额外的 IP 地址是 `192.168.0.42` 并且你想为其指定域名 `sail.com`，你必须在 `named.conf` 文件中为其创建一个新的 `zone` 语句并使用新的区域文件。`zone` 语句看起来像以下这样。区域文件名为 `sail.com`。

```
zone "sail.com" in {
    type master;
    file "sail.com";
};
```

在 `sail.com` 文件中，名称服务器名为 `turtle.mytrek.com`，电子邮件地址为 `hostmaster@turtle.mytrek.com`。在名称服务器（NS）记录中，名称服务器是 `turtle.mytrek.com`。这是运行名称服务器的同一台机器，使用原始地址。`turtle.mytrek.com` 也是处理发往 `sail.com` 的邮件的主机（MX）。然后地址记录将额外的 IP 地址 `192.168.0.42` 与 `sail.com` 域名关联起来。然后在此域上定义一个虚拟主机 `jib.sail.com`。还为该主机生成了 `www` 和 `ftp` 别名，创建了 `www.sail.com` 和 `ftp.sail.com` 虚拟主机。

```
; Authoritative data for sail.com
; @ IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com. (
    93071200 ; Serial (yymmddxx)
    10800    ; Refresh 3 hours
    3600     ; Retry 1 hour
    3600000  ; Expire 1000 hours
    86400 )  ; Minimum 24 hours

    IN  NS    turtle.mytrek.com.
    IN  MX  10 turtle.mytrek.com.
    IN  A     192.168.0.42 ;address of the sail.com domain

jib  IN  A     192.168.0.42
www  IN  A     jib.sail.com.
ftp  IN  CNAME jib.sail.com.
```

在你的反向映射文件（`/var/named/1.168.192`）中，为任何虚拟域添加 PTR 记录。

```
42.1.168.192  IN  PTR  sail.com.
42.1.168.192  IN  PTR  jib.sail.com.
```

你还必须配置你的网络连接以在你的机器上侦听这两个 IP 地址（参见第 5 章）。

## 缓存文件

缓存文件用于将 DNS 服务器连接到 Internet 上的根服务器。文件可以是任何名称。在许多系统上，缓存文件称为 `named.ca`。其他系统可能将缓存文件称为 `named.cache` 或 `roots.hints`。缓存文件通常是由你的 BIND 软件安装的标准文件，其中列出了 Internet 指定根服务器的资源记录。你可以从 `rs.internic.net` FTP 站点获取 `named.ca` 文件的当前版本。以下示例显示了从 `named.ca` 文件中取出的示例条目：

; formerly NS.INTERNIC.NET

;

3600000 IN NS A.ROOT-SERVERS.NET.

A.ROOT-SERVERS.NET. 3600000 A 198.41.0.4

; formerly NS1.ISI.EDU

;

3600000 NS B.ROOT-SERVERS.NET.

B.ROOT-SERVERS.NET. 3600000 A 128.9.0.107

如果要创建隔离的内联网，则在连接到互联网之前需要创建自己的根 DNS 服务器。实际上，你正在创建一个假的根服务器。这可以是系统上另一个假装成根的服务器或同一个名称服务器。

## 动态更新：DHCP 和日志文件

存在需要动态更新区域的情况。不是手动编辑区域文件来更改区域中的内容，而是外部进程更新区域，自动进行更改并保存文件。动态更新既由主区域更新从区域完成，也由 DHCP 服务器将为主机生成的 IP 地址提供给 DNS 服务器完成。

会维护一个日志文件来记录对区域所做的所有更改，其扩展名为 `.jnl`。如果系统崩溃，将读取此文件以实施最新更改。如果要手动更新动态更新的区域，则首先需要删除其日志文件；否则，你的更改将被日志文件条目覆盖。

你可以通过指定 `allow-update` 选项来允许区域自动更新。此选项指示可以执行更新的主机。

```
allow-update {turtle.mytrek.com};
```

或者，对于主区域，你可以使用 `update-policy` 语句创建更精细的访问规则集。使用 `update-policy` 语句，你可以为不同主机和主机类型列出多个授予和拒绝规则。

## TSIG 签名和更新
