
表示 foo.edu 域中的主机 fake（即主机 fake.foo.edu.）拥有 IP 地址 192.168.1.1。A 记录采用以下形式：

```text
<host name>  IN  A  <IP address>
```

CNAME 记录表示主机名的别名。在此示例中，www 是主机 brain.foo.edu. 的别名：

```text
www    IN  CNAME  brain.foo.edu.
```

这意味着，任何解析 www.foo.edu 的请求实际上都会像针对 brain.foo.edu. 的请求一样被解析。

MX 记录指明该域的邮件交换器的主机名。当邮件消息发送到 foo.edu 域时，投递邮件的邮件服务器会利用此信息来决定将邮件投递到哪个邮件交换器。MX 记录采用以下形式：

```text
<domain>  IN  MX  <preference><host name>
```

优先数字表示尝试投递邮件的顺序：优先数字越低，访问该服务器的优先级就越高。在此示例中，mail.foo.edu 的优先级为 10，mail2.foo.edu 的优先级为 20。这意味着 mail.foo.edu 是主邮件交换器，而 mail2.foo.edu 是备份。如果由于某种原因无法将邮件投递到 mail.foo.edu，则会尝试投递到 mail2.foo.edu。

> **注意**
>
> 对于属于该区域文件所定义域的任何邮件交换器，你都应有相应的 A 记录。如果使用的备份邮件交换器属于另一个域，则无需在该区域文件中添加 A 记录，该记录将出现在另一个域的主名称服务器的区域文件中。

用于 foo.edu 反向名称查找的区域文件 /var/named/zone.192.168.1 与 foo.edu 的区域文件类似，但包含一些不同的记录：

```text
; File: zone.192.168.1
;
1.168.192.in-addr.arpa.  IN  SOA     fake.foo.edu. hostmaster.foo.edu. (
                           1998021700     ;Serial
                           8H             ;Refresh
                           2H             ;Retry
                           1W             ;Expire
                           1D             ;Minimum
                         )
              IN  NS      fake.foo.edu.
1             IN  PTR     fake.foo.edu.
2             IN  PTR     pinky.foo.edu.
3             IN  PTR     brain.foo.edu.
4             IN  PTR     mail.foo.edu.
5             IN  PTR     mail2.foo.edu.
```

与 foo.edu 区域文件一样，该文件包含一个 SOA 记录和至少一个 NS 记录。

此外，它还包含一系列 PTR 记录，这些记录定义了可用于反向名称查找的 IP 地址指针。PTR 记录的形式如下：

```text
<IP address>  IN  PTR  <host name>
```

请注意，IP 地址在指定时没有末尾的点。这使得它们相对于该区域文件提供反向名称查找数据的网络。因此，以下条目：

```text
3  IN  PTR  brain.foo.edu.
```

表示 IP 地址 192.168.1.3 指向主机 brain.foo.edu。

用于本地回环网络的反向名称查找文件 /var/named/127.0.0 与 foo.edu 的反向查找区域类似：

```text
;
; File: zone.127.0.0
@       IN      SOA     fake.foo.edu.        hostmaster.foo.edu. (
                19960101401              ;Serial
                8H                       ;Refresh
                2H                       ;Retry
                1W                       ;Expire
                1D                       ;Minimum
        IN      NS      fake.foo.edu.
1       IN      PTR     localhost.
```

该文件包含一个 SOA 记录、一个或多个 NS 记录以及一个或多个 PTR 记录。

## 启动 named

现在我们可以启动 named 了。在版本 8 中，引入了一个名为 ndc 的新程序来管理和控制 named，但如果你愿意，仍然可以直接调用 named。不过，ndc 提供了一种简洁的方式来启动、停止和检查 named 的状态。

使用配置文件 /etc/named.conf 以及 /var/named 中定义的区域文件，我们可以通过以下方式使用 ndc 启动 named：

```text
# ndc start
```

启动 named 后，检查 /var/log/messages，确保没有报告错误。如果存在错误，日志条目会让你了解问题所在。你需要修复配置或区域文件中可能出现的任何错误，然后重新启动 named。

启动后，你可以使用以下命令检查 named 的状态：

```text
# ndc status
```

你也可以使用 ndc 命令停止 named：

```text
# ndc stop
```

## 防火墙后专用网络的主名称服务器

以下是一个位于企业防火墙后的专用网络的主名称服务器的典型 named.conf 文件：

```conf
 // File: /etc/named.conf
 // Primary Name Server for foo.dom
 //              Internal Network
 options {
     directory "/var/named";
     // Uncommenting this might help if you have to go through a
     // firewall and things are not working out:
     fake-iquery yes;
     query-source address * port 53;
     forward first;
     forwarders {
         192.168.1.1
     }
 };
 zone "." {
     type hint;
     file "root.hints";
 };
 zone "foo.dom" {
     type master;
     file "zone.foo.dom";
 };
 zone "10.in-addr.arpa" {
     type master;
     file "zone.10";
 };
 zone "0.0.127.in-addr.arpa" {
     type master;
     file "zone.127.0.0";
 };
```

请注意，此 named.conf 文件与前面用于说明已注册域的主名称服务器的文件之间存在若干差异：

- 在 options 部分中，添加了几个新的指令：

```text
     fake-iquery yes;
     query-source address * port 53;
     forward first;
     forwarders {
         192.168.1.1
     }
```

  fake-iquery 和 query-source 指令在某些防火墙环境中是必需的，它们允许内部 DNS 服务器查询外部 DNS 服务器。forward 和 forwarders 指令表示，对于任何不是此服务器作为主主服务器处理的域的查询，都应转发到 192.168.1.1 进行解析，而不是直接尝试解析这些查询。请求被转发到的服务器将返回对查询的任何响应。

- 已定义了一个 `foo.dom` 域，并带有相关的反向查找区域。该域供专用网络内部使用，目的是利用 DNS 解析内部主机名。`foo.dom` 域不属于标准域名层次结构的一部分，不会影响互联网，也不需要注册。`foo.dom` 域中的名称仅在本地有效，不能用作互联网上的主机名。

可以使用本章前面“创建区域文件”一节中所述的区域和反向查找区域的相同技术来创建区域文件。

完成此操作后，按照前面“启动 named”一节中的说明启动 named。

## 辅助名称服务器

在了解如何设置主名称服务器之后，为域创建辅助名称服务器就相当简单了。对于辅助服务器，只需要一个 named.conf 文件。当辅助服务器启动时，所有区域文件信息都将从主名称服务器传输过来。

foo.edu 域的辅助名称服务器的 named.conf 文件类似于以下内容：

```conf
// Secondary Name Server for foo.edu
options {
        directory "/var/named";
};
zone "." {
        type hint;
        file "root.hints";
};
zone "0.0.127.in-addr.arpa" {
        type master;
        file "zone.127.0.0";
};
zone "foo.edu" {
        type slave;
        file "zone.foo.edu";
        masters {
                192.168.1.1;
        };
};
zone "1.168.192.in-addr.arpa" {
        type slave;
        file "zone.192.168.1";
        masters {
                192.168.1.1;
        };
};
```

该文件与主主服务器的 named.conf 文件非常相似，不同之处在于某些区域被定义为从区域。对于每个从区域，你都必须指定一个区域文件，以便将下载的信息保存到该文件中。此外，你还需要指定该域的主名称服务器（主服务器）的 IP 地址，辅助服务器可以从该主服务器获取区域信息。

你必须按照前面关于为已注册互联网域创建主名称服务器一节中的说明，为回环网络定义一个区域文件。

在 named.conf 文件、回环网络的区域文件以及 root.hints 文件都就绪后，按照前面“启动 named”一节中的说明启动 named。

## 解析名称

*解析器* 是库例程，用于在需要解析名称的系统上对 DNS 名称空间执行名称查找。这些通过 `/etc/resolv.conf` 配置。此外，解析名称时搜索不同名称空间（如 DNS 和 NIS）的顺序在 `/etc/nsswitch.conf` 文件中指定。

考虑一下位于专用网络中的企业防火墙后的主机所使用的以下 resolv.conf 文件：

```conf
; File: /etc/resolv.conf
domain foo.dom       ; internal private domain
search foo.dom foo.edu  ; foo.edu is the internet domain
nameserver      10.0.0.1 ; primary for foo.dom
nameserver      10.0.0.2 ; secondary for foo.dom
```

该文件的工作方式如下：

- 注释以分号 (;) 开头，直到行尾结束。
- domain 指令指定主机所属的域。
- search 指令指定一个或多个域，当尝试解析未使用域名完全限定的不完整主机名时，应在这些域中进行搜索。
- nameserver 指令按你应查询的顺序指定名称服务器的 IP 地址。解析名称时，你的系统会查询列出的第一个服务器；如果该服务器不可用或无法响应，系统将继续查询下一个指定的服务器，并依次类推。你可以拥有与名称服务器数量一样多的 nameserver 指令。

根据你的系统配置，你可能需要将 DNS 解析添加到 `/etc/nsswitch.conf` 文件中。例如，假设该文件包含一个类似以下的条目：

```text
hosts: files nis
```

你需要按如下方式将 dns 添加到该行：

```text
hosts: files nis dns
```

