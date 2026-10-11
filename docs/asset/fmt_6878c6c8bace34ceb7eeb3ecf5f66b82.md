
```options {

    search FlenovM;

    domain.name;

    nameserver 10.1.1.1;

    nameserver 10.1.1.2;

};

zone "." {

    type hint;

    file "named.cache";

};

zone "redhat.com" {

    type master;

    file "redhat.zone";

};

zone "77.168.192.in-addr.arpa" {

    type master;

    file "192.168.77.zone";

};
```

`sitename.zone` 文件的内容可能如下：

```
@ IN SOA ns.sename.com root.sename.com ( 

1 ; serial

28800 ; refresh

7200 ; retry

604800 ; expire

86400 ; ttl

)

IN NS ns.sename.com.

IN MX 10 mail.sename.com.

ns A 190.12.10.1

mail A 190.12.10.2
```

### 用于配置 DNS 记录的主指令功能如下

- 区域起始(`SOA`) — 指定主要信息，包括管理员的电子邮件地址、记录更新的频率、缓存记录的 `TTL` 等。
- 地址(`A`) — 指明计算机名和 IP 地址。
- 规范别名(`CNAME`) — 为 `A` 记录类型中的真实域名名指定别名。
- 指针 (`PTR`) — 通过 IP 地址显示域名名。
- 文本(`TXT`) — 用于描述信息的自由文本描述。
- 负责人(`RP`) — 指定负责服务运行的人员的电子邮件地址。
- 主机信息 (`HINFO`) — 关于计算机的指定信息，如操作系统类型和安装的设备。

出于安全考虑，不使用 `HINFO` 和 `TXT` 记录；因此它们不会向黑客泄露任何信息。不应向黑客提供关于计算机的任何信息，无论这些信息看起来多么无害，事实远非无害。`HINFO` 和 `TXT` 记录纯粹是信息性的，在获取服务器运行状态后不包含任何数据。

现在，回到 `sitename.zone` 文件并考虑其内容。在第一条记录（`IN SOA` 类型）中，描述了区域。首先给出了 DNS 服务器的名称（`sitename.com`）和负责记录的人员（`root@sitename.com`）。括号中的参数为了方便起见，每个都单独占一行指定。第一个参数是序列号（`serial`）。在每次修改后，将此参数加 1，或者用记录最后修改的日期替换它。通过此值，其他服务器将发现记录是否被修改。

`refresh` 参数设置了其他服务器更新其信息的频率。如果发生错误，服务器必须在 `retry` 参数指定的周期后重试。

`expire` 参数指定了缓存区域信息何时不再有效。`ttl` 参数定义了条目在缓存服务器上的最小 `TTL`。

这些参数告知 DNS 的其他部分如何刷新由你的 DNS 服务器控制的区域信息。

下一条记录是 `NS` 类型；可以有几条这样的记录。在这种情况下，`NS` 代表名称服务器（name server）。该记录描述了负责该区域的 DNS 服务器。所有其他 DNS 参与将使用这些服务器将 `sitename.com` 符号名解析为其 IP 地址。

接下来可以是邮件交换（`MX`）记录。DNS 服务器使用这些记录来确定将邮件发送到 `sitename.com` 域名的位置。在本示例中，这是 `mail.sitename.com` 服务器。服务器名称前的数字指定了 `MX` 条目的优先级。如果有多个 `MX` 记录，将按照它们优先级的顺序使用。

注意：`NS` 和 `MX` 条目必须以句号结束。

最后记录记录用于反向查找。它们的格式如下：
`name A address`

示例中有两条这样的记录：
`ns A 190.12.10.1`
`mail A 190.12.10.2`

这意味着 `ns.servername.com` 和 `mail.servername.com` 符号名分别解析为 `190.12.10.1` 和 `190.12.10.2` IP 地址。

## 11.6. 反向区域

反向查找文件（用于将 IP 地址解析为对应的主机名）的格式类似于：

```
@ IN SOA ns.sitename.com root.sitename.com (

+1 ; serial

28800 ; refresh

7200 ; retry

604800 ; expire

86400 ; ttl

) IN NS localhost.

1 PTR servername.com.

2 PTR mail.servername.com.
```
