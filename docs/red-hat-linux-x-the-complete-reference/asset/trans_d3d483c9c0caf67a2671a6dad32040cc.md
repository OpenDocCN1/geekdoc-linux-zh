
## IPv6 反向映射（IP6.ARPA 格式）

反向映射文件随后使用相同的位级格式来表示接口地址。

```
zone "\[xfec00000000000000/64].IP6.ARPA" in {
    type master;
    file "fec.ip6.arpa";
};
```

反向映射文件随后使用相同的位级格式来表示接口地址。

```
@ IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com. (
    92050300 ; Serial (yymmddxx 格式)
    10800 ; Refresh 3小时
    3600 ; Retry 1小时
    3600000 ; Expire 1000小时
    86400 ) ; Minimum 24小时

@ IN NS turtle.mytrek.com.
\[x00080800200C417A/64] IN PTR turtle.mytrek.com.
\[xfEDCBA9876543210/64] IN PTR rabbit.mytrek.com.
\[x00E018F73466007D/64] IN PTR lizard.mytrek.com.
```

### IPv6 IP6.INT 反向映射格式

较旧的 IP6.INT 格式使用半字节（nibble）格式来表示 IPv6 地址。十六进制地址被分割为每个十六进制数字，用点分隔并按逆序书写。这给出了 32 个逆序的十六进制数字。这里展示了 lizard 地址的 IP6.INT 版本。

```
FEC0:0000:0000:0000:0E00:18F7:3466:007D    lizard IPv6 地址
0.0.0.0.0.0.0.0.0.0.0.0.0.c.e.f           lizard 网络地址
D.7.0.0.6.6.4.3.7.F.8.1.0.E.0.0           lizard 接口地址
```

在 named.conf 文件中，带有 IP6.INT 扩展的反向映射的区域条目将使用网络地址的逆序半字节格式。

```
zone "0.0.0.0.0.0.0.0.0.0.0.0.0.c.e.f.IP6.INT" in {
    type master;
    file "fec.ip6.int";
};
```

反向区域文件随后使用每个接口地址的逆序半字节格式。

```
@ IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com. (
    92050300 ; Serial (yymmddxx 格式)
    10800 ; Refresh 3小时
    3600 ; Retry 1小时
    3600000 ; Expire 1000小时
    86400 ) ; Minimum 24小时

$ORIGIN 0.0.0.0.0.0.0.0.0.0.0.0.0.c.e.f IN NS turtle.mytrek.com.
A.7.1.4.C.0.0.2.0.0.8.0.8.0.0.0 IN PTR turtle.mytrek.com.
0.1.2.3.4.5.6.7.8.9.A.B.C.D.E.F IN PTR rabbit.mytrek.com.
D.7.0.0.6.6.4.3.7.F.8.1.0.E.0.0 IN PTR lizard.mytrek.com.
```

### 本地主机反向映射

本地主机反向映射文件为被称为 localhost 的本地环回接口实现反向映射，其网络地址为 127.0.0.1。该文件可以是任何名称。在大多数系统中，localhost 被命名为 named.local。在其他系统中，localhost 可能使用 IP 地址的网络部分，即 127.0.0。此文件允许将域名 localhost 映射到本地主机 IP 地址，该地址在每台机器上始终为 127.0.0.1。地址 127.0.0.1 是一个特殊地址，作为您的机器的本地地址发挥作用。它允许机器寻址自身。

在此文件的区域语句中，区域的名称是 0.0.127.IN-ADDR.ARPA。IP 地址的域名部分以逆序输入，并附加 IN-ADDR.ARPA，即 0.0.127.IN-ADDR.ARPA。named.conf 条目如下所示：

```
zone "0.0.127.IN-ADDR.ARPA" {
    type master;
    file "named.local";
};
```

用于本地主机反向映射文件的名称通常为 named.local，但也可以是任何名称。NS 记录指定本地主机应使用的名称服务器。此文件包含一个 PTR 记录，将 IP 地址映射到本地主机。用作名称的 1 会扩展为附加区域域名——在这种情况下，得到 1.0.0.127，这是一个反向 IP 地址。注意 localhost 后面的尾随句号：

```
@ IN SOA localhost. root.localhost. {
    1997022700 ; Serial
    28800 ; Refresh
    14400 ; Retry
    3600000 ; Expire
    86400 ) ; Minimum

IN NS turtle.mytrek.com.

1 IN PTR localhost.
```

在 IPv6 中，本地主机反向映射使用 IPv6 本地主机地址的逆序来指定。该地址由 31 个零和一个 1 组成，可以简写为 ::1，其中 :: 代表 31 个零的序列。使用 IPv6 IP6.ARPA 格式，这些可以写成位级格式，其中前 64 位由全零的网络地址组成，接口地址值为 1。

```
0000:0000:0000:0000:0000:0000:0000:0001  本地主机 IPv6 地址
\[x00000000000000000000000000000001/128]  本地主机地址
```

在 named.conf 文件中，IP6.ARPA 本地主机条目看起来像这样。

```
zone "\[x00000000000000000000000000000001/64].IP6.ARPA" in {
    type master;
    file "192.168.0";
};
```

在本地主机反向映射文件中，本地主机条目将显示如下。

```
\[x0000000000000001/64]    IN    PTR    localhost.
```

对于较旧的 IP6.INT 格式，本地主机条目将使用相同的零网络地址，但本地主机反向映射文件将使用地址的半字节格式，如下所示。

```
1.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0  IN    PTR    localhost.
```

## 子域和从服务器

向 DNS 服务器添加子域只需在 named.conf 文件中创建额外的主条目，然后在主 DNS 服务器的区域文件中放置该子域的名称服务器和授权条目即可。子域拥有自己的区域文件，其中包含其 SOA 记录以及列出属于其子域的宿主机的条目，包括其自身的邮件和新闻服务器。

### 子域区域

子域的名称可以完全不同，也可以是具有与主域相同后缀的名称。在以下示例中，子域被称为 beach.mytrek.com。它也可以轻松地被称为 mybeach.com。在该示例中，该域的名称服务器位于主机 crab.beach.mytrek.com 上。其 IP 地址为 192.168.0.33，其区域文件为 beach.mytrek.com。beach.mytrek.com 区域文件包含由此名称服务器服务的所有宿主机的 DNS 条目。以下示例显示了其 named.conf 的区域条目：

```
zone "beach.mytrek.com" {
    type master;
    file "beach.mytrek.com";
};
```

```
zone "1.168.192.IN-ADDR.ARPA" {
    type master;
    file "192.168.0";
};
```

### 子域记录

在主 DNS 服务器上，以示例中的 turtle.mytrek.com 为例，你需要在主区域文件中放置条目，以识别子域服务器的主机并将其指定为名称服务器。此类条目也被称为粘合记录（glue records）。在此示例中，你将在 turtle.mytrek.com 上的 mytrek.com 区域文件中放置以下条目：

```
beach.mytrek.com.  IN  NS  beach.mytrek.com.
beach.mytrek.com.  IN  A   192.168.0.33
```

现在，由 beach.mytrek.com 服务的宿主机的 URL 引用可以从由 mytrek.com 服务的任何主机访问，后者无需维护关于 beach.mytrek.com 宿主机的任何信息。它只是将此类 URL 引用转发给 beach.mytrek.com 名称服务器。

### 从服务器

从 DNS 服务器直接连接到主 DNS 服务器，并定期从中接收 DNS 信息。你使用主 DNS 服务器自动配置其从 DNS 服务器。你对主服务器所做的任何更改都会自动传输到其从服务器。这种信息传输称为区域传输。每当从区域的刷新时间到达或从服务器收到主服务器的 notify 消息时，区域传输会自动启动。刷新时间是区域 SOA 条目中的第二个参数。每当对主区域的配置文件做出更改并重启 named 守护进程时，主服务器会自动发送 notify 消息。实际上，从区域由主区域自动配置，接收主区域的区域文件并将其作为自己的区域文件。

### 从区域

使用前面的示例，假设你想在 rabbit.mytrek.com 上设置一个从服务器。在 rabbit.mytrek.com 上的从 DNS 服务器的 named.conf 配置文件中设置区域条目，如以下示例所示。从服务器运行在与主服务器相同的域中，因此它具有相同的区域名称，即 mytrek.com。其 SOA 文件名为 slave.mytrek.com。文件名中的术语 "slave" 只是一种约定，有助于识别它是从服务器配置文件。masters 语句列出了其主 DNS 服务器——在此情况下为 192.168.0.1。每当从服务器需要进行区域传输时，它都会从该主 DNS 服务器传输数据。此从服务器的反向映射文件条目将其反向映射文件列为 slave.192.168.0。

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

### 从记录

在主 DNS 服务器上，主 SOA 区域文件中包含条目，以识别持有从 DNS 服务器的主机并将其指定为 DNS 服务器。在此示例中，你会在 mytrek.com 区域文件中放置以下内容：

```
IN    NS    192.168.0.2
```

你还需要在 mytrek.com 反向映射文件中为此名称服务器放置一个条目：

```
IN    NS    192.168.0.2
```

### 控制传输

主 DNS 服务器可以使用 allow-transfer 语句控制哪些从服务器可以从中传输区域信息。将该语句与你要允许访问的从服务器的 IP 地址列表一起放置。此外，主 DNS 服务器应确保其 notify 选项未被禁用。notify 选项可以通过 options 或 zone named.conf 条目中的 "notify no" 语句被禁用。只需擦除 "no" 参数即可启用 notify。

### 增量区域传输

在 BIND 8.2.2 和 9.0 版本中，BIND 现在支持增量区域传输（IXFR）。以前，在更新中，所有区域数据都会被替换，而不是简单地编辑诸如添加少量资源记录之类的更改。使用增量区域传输时，主区域会维护一个更改数据库。然后，只有更改会被传输到从区域，从区域使用此信息更新其自己的区域文件。要实现增量区域传输，你必须在 options 部分开启 maintain-ixfr-base 选项。

```
maintain-ixfr-base yes;
```

然后，你可以在区域部分使用 ixfr-base 选项来指定一个特定的数据库文件来保存更改。

```
ixfr-base "db.mytrek.com.ixfr";
```

