
```
; 
; db.sniglets
; 
@       in      SOA     dns.sniglets.com.
hostmaster.sniglets.com (
        19990610  ; Serial - date & revision
                    YYYYMMREV
        21600   ; Refresh (6 hours)
        3600    ; Retry (15 minutes)
        604800  ; Expire (7 days)
        86400   ; Minimum
)

                IN      NS      dns1.sniglets.com
                IN      NS      dns.sniglets.com

pilots    IN      A       192.168.3.4
drivers   IN      CNAME   pilots.sniglets.com
          IN      MX      10 mail.sniglets.com.
          IN      MX      20 sniglets.com.
          IN      HINFO   HP HP/UX

$INCLUDE hosts.sniglets.4
;end of primary zone file
```

（这些值可防止）服务器无限期地分发数据，如果主服务器已更改或长时间停机的话。最小 TTL（生存时间）是其他名称服务器可以缓存该域数据的时间量。缓存数据的能力有助于将负载从主服务器分配到从服务器，但过长的 TTL 可能导致从服务器缓存过期的数据。

在为你的 `SOA` 记录确定值时，没有唯一的正确答案。每天有数千次 DNS 更改的 ISP 需要较短的取值，以便新的 DNS 更改能够快速生效。但是，该 ISP 还需要有足够的资源来应对由此产生的额外流量。相反，一个只有一百条 DNS 记录的小型企业可以采用相当大的取值，因为其数据很少会更改。在公司服务器上运行的 DNS 服务器在此情况下可以很好地工作，但新记录可能需要数天才能传播到互联网中。

我们 `hosts.*.snippet` 文件中的下一条记录是：

```
IN    NS    dns1.sniglets.com

IN    NS    dns.sniglets.com
```

这些记录定义了两个重要条目。`IN` 条目是记录类别，`IN` 代表 Internet。在本章的所有示例中，我们处理的都是 Internet 类别。如果省略类别标识符，则默认是 `IN`。下一个字段是资源条目，其中包含 `NS` 条目示例。`NS` 资源标识域的名称服务器。在我们的示例中，`dns1.sniglets.com` 和 `dns.sniglets.com` 被定义为域 `ee.gatech.edu` 的名称服务器。虽然 `NS` 记录不是必需的，但该信息可能对调试很有用。如果你是一个注重安全的人，你可能希望省略 `NS` 记录，以免向世界“宣传”你的 DNS 服务器。

> 如果你注重安全，你可能希望省略 `NS` 记录，以免向世界“宣传”你的 DNS 服务器。

我们文件中的下一条记录是 `A` 记录，它将主机名映射到主机 IP 地址：

```
pilots    IN    A       192.168.3.4
```

`A` 记录告诉我们主机名 `pilots.sniglets.com` 与 IP 地址 `192.168.3.4` 相关联。`CNAME` 记录，例如

```
drivers    IN    CNAME    pilots.sniglets.com
```

创建别名，即从一个主机条目到另一个主机条目的重复映射。在此示例中，`drivers.sniglets.com` 被映射到 `pilots.sniglets.com`。你可以根据需要将任意数量的 `CNAME` 条目映射到单个 `A` 记录。你甚至可以将 `CNAME` 条目映射到其他 `CNAME` 条目。但请注意，每个不同的 IP 地址只能有一个 `A` 记录。

> `A` 记录是一对一映射，每个不同的 IP 地址只能有一个 `A` 记录。你可以根据需要将任意数量的 `CNAME` 条目与单个 `A` 记录关联。你也可以将 `CNAME` 条目与其他 `CNAME` 条目关联。

![](img/415c89a1ede71e11e5040a0038b6916c_223_0.png)

理解了 `SOA`、`NS`、`A` 和 `CNAME` 记录后，你就可以构建一个功能正常的区域（zone）。然而，在创建主 DNS 信息时，还有两个资源记录对你很有用。如果我们回头看看 `pilots.sniglets.com` 的条目，你首先会看到定义的 `MX` 资源记录：

```
pilots          IN  A       192.168.3.4

drivers         IN  CNAME   pilots.sniglets.com
                IN  MX      10 mail.sniglets.com.
                IN  MX      20 sniglets.com.
                IN  HINFO   HP710 HP/UX
```

`MX` 资源定义条目的 SMTP 邮件交换器。当你希望将传入的 SMTP 邮件重定向到单个或一组明确定义的 SMTP 邮件服务器时，邮件交换器非常有用。在大型网络中，让每个 UNIX 系统都充当自己的邮件服务器是不明智的。通过使用 `MX` 记录，你提供了一种机制，告知远程 SMTP 服务器应尝试将发送给定义系统中用户的邮件投递到哪里。

在此示例中，`mail.sniglets.com` 是 `pilots.sniglets.com` 的主要 SMTP 系统，而系统 `sniglets.com` 在 `mail.sniglets.com` 无法响应时充当备份邮件服务器。SMTP 服务器前面的整数值表示权重，数值越小表示该 SMTP 服务器越受优先选择。有关配置 SMTP 邮件服务器的更多信息，请参阅第 9 章“电子邮件和消息传递”。

你会发现最后一个有用的资源记录是 `HINFO` 资源。`HINFO` 提供了一种将注释信息插入 DNS 的方法。`HINFO` 记录定义为由空格分隔的两个字段的文本记录。你可以使用这两个字段插入有关系统的信息，例如系统类型、操作系统级别、系统所有者或位置。如果你有一个大型安装，或者想通过 DNS 共享信息，这会非常有用。

## 反向查找数据库文件

现在你已经可以从主机名到 IP 地址进行查找了，你还需要能够进行逆向操作，即从 IP 地址到主机名。这称为反向查找，反向查找文件是主机数据库文件的补充，该文件将主机名分配给 IP 地址。反向查找文件与主机数据库文件的形式类似：

```
;
; db.3.168.192.in-addr.arpa
;
@       IN      SOA     dns.sniglets.com. hostmaster.sniglets.com. (
                        19990604 ; Serial
                        10800    ; Refresh (15 minutes)
                        3600     ; Retry (15 minutes)
                        604800   ; Expire (5 days)
                        86400 )  ; Minimum TTL(4 hours)
        IN      NS      dns.sniglets.com.
        IN      NS      duchess.sniglets.com.

4       IN      PTR     pilots.sniglets.com.
```

你可以看到相同的 `SOA` 记录信息以及名称服务器信息。虽然 `SOA` 记录的形式相同，但数据条目可能不同。在大多数情况下，你希望保持 `Refresh`、`Retry`、`Expire` 和 `TTL` 值一致；但你的序列号很可能不同，因为 DNS 的日常管理可能会导致你在不同的时间间隔内修改数据库文件。

反向查找文件中不同的条目是与 IP 地址关联到主机名的那些值。反向查找文件条目的记录类型为 `PTR` 类型，它将 IP 地址关联到主机名。

```
4       IN      PTR     pilots.sniglets.com.
```

此条目将 IP 地址 `192.168.3.4` 与主机名 `pilots.sniglets.com` 关联起来。在创建 `PTR` 记录时，请确保仅将 IP 地址与你在正向数据库文件中设置好的 `A` 记录关联。虽然可以创建多个 `PTR` 记录，但大多数系统并未利用此功能。此外，请确保每个 `PTR` 记录以句点结尾。未包含句点可能会导致你的 DNS 服务器出现问题。

> `PTR` 记录末尾未包含句点会导致 DNS 服务器出现不一致，并且可能难以调试。

## 本地主机数据库文件
