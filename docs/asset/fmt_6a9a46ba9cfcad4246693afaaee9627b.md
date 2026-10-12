
```
（原文此处逻辑不完整，注：此处为补全逻辑）

有了这样的条目，域名 `www.oneoursource.com` 将翻译为域名 `ftp`（此处），然后进一步翻译为 IP 地址 `38.89.136.109`。

## 名称服务器记录类型 (Name Server Record Type)

如前所述，每个域名可以有一个或多个名称服务器；这些可以通过 `NS` 记录来定义。原始（主）名称服务器在 `SOA` 记录中指定，但也需要 `NS` 记录。辅助（从）名称服务器也需要通过 `NS` 记录定义。你可以创建如下记录来定义名称服务器：

```

@ IN NS ns.sample.com.

@ IN NS ns2.sample.com.

```

即使是主服务器，`NS` 条目指定的是域名而不是 IP 地址。注意：`NS` 示例中的 `@` 字符可以完全移除。数据的第一个字段被假设为 `$ORIGIN` 的值。

## 邮件交换记录类型 (Mail Exchange Record Type)

假设邮件发送到 `info@oneoursource.com`。发送域名的 `MTA`（邮件传输代理）需要确定哪台机器处理 `oneoursource.com` 域名的入站。`MTA` 通过查询邮件交换（`MX`）记录来实现。

域名的 `MX` 记录通常如下：

```

@ IN MX 10 mail1.oneoursource.com

@ IN MX 20 mail2.oneoursource.com

```

现在你理解记录类型，大多数 `MX` 记录应该变得很简单了。`10` 和 `20` 的值与你之前看到的不同。这些数字提供了优先级，数字越小，优先级越高。

## 第 21 章：创建和维护 DNS 区域 427

管理员经常混淆优先级值。如果一台邮件服务器的优先级为 `10`，另一个为 `20`，发送域名的 `MTA` 最初尝试向优先级为 `10` 的服务器发送邮件。如果服务器没有响应，则联系优先级为 `20` 的邮件服务器。由于大多数邮件服务器 `24/7` 运行，第二台邮件服务器可能永远不会被使用。

更常见的方法是每个邮件服务器设置相同的优先级值以便负载均衡。在这种情况下，邮件服务器的使用率大致相等（缓存 DNS 服务器可能会稍微导致负载不平衡）。

只有 `MX` 记录也是不常见的，因为许多中小型公司都需要电子邮件。

## PTR 记录类型 (PTR Record Type)

之前描述的地址记录用于正查找区域文件将域名翻译为 IP 地址。`PTR` 记录用于反向区域文件，将 IP 地址翻译为域名。一个典型的 `PTR` 记录如下：

```

109.136.89.38.in-ar.oneoursource.com PTR www.oneoursource.com.

```

第一个字段是反序的 IP 地址，例如 `109.136.89.38.in-ar.oneoursource.com`。在这种情况下，域名相对于 `$ORIGIN` 的默认定义给出，但也可以以完全限定的形式提供：

```

109.136.89.38.in-ar.oneoursource.com. PTR www.oneoursource.com.

```

`PTR` 的值表示此行代表指针记录类型，`www.oneoursource.com.` 的值与 IP 地址 `109.136.89.38` 关联的域名。

注意：`PTR` 记录仅放置在反向查找区域文件中。

## 总结 (Putting It All)

从零开始创建 DNS 服务器对于新手管理员来说通常是一项艰巨的任务。当你创建第一台 DNS 服务器时，请使用 `KISS` 原则（保持简单，别傻了）。如果你尝试实现许多花哨的 DNS 设置，将很难确定问题在哪里。

在关注细节之后，查看整体视图会有帮助。带着这种想法，让我们来看简单的 DNS 配置。在这个示例中，我们为 `sample.com` 域名创建需要的文件。由于这只是测试域名，我们使用私有 IP 地址。

首先，参见示例 21-2 中的 `/etc/named.conf` 文件。注意，为了简洁已删除文件中的注释，演示中添加的条目已**加粗**。

### 示例 21-2 新的 /etc/named.conf 文件

```
options {

    listen-on port 53 { 127.0.0.1 };

    listen-on-v6 port 53 { ::1 };

    directory "/var/named";

    dump-file "/var/named/data/cache_dump.db";

    statistics-file "/var/named/data/named_stats.txt";

    memstatistics-file "/var/named/data/named_mem_stats.txt";

    allow-query { localhost };

    recursion yes;

    dnssec-enable yes;

    dnssec-validation yes;

    dnssec-lookatside auto;

    bindkeys-file "/etc/named.iscdlv.key";

    pid-file "/run/named/named.pid";

    session-keyfile "/run/named/named/session.key";

}

logging {

    channel default_debug {

        file "data/named.run";

        severity dynamic;

    };

}

zone "." IN {

    type hint;

    file "named.ca";

}
```

### 第 21 章：创建和维护 DNS 区域

```
include "/etc/named.rfc1912.zones"

include "/etc/named.root.key";

zone "sample.com" {

type master;

file "named.sample.com";

}

zone "1.168.192.in-addr.arpa" {

type master;

file "db.192.168.1";

}
```

根据示例 21-2 中的条目，你应该能够识别出正向和反向查找区域都已定义。此外，你还应该确定该系统作为 `sample.com` 域名域的主服务器（`master server`），这意味着对区域文件的所有更改都应该在这台机器上进行。

如果这是一个从服务器（`slave server`），你就不需要创建区域文件，因为这些文件将在首次从主服务器进行区域区域传输时自动创建。然而，由于这是主服务器，你需要创建一个正向区域文件，如示例 21-3 所示。

### 示例 21-3 的 /var/named/named.sample.com 文件

```
@ IN SOA ns.sample.com. root.sample.com. (
00 ; serial
1D ; refresh
1H ; retry
1W ; expire
3H ) minimum
; Nameservers:
@ IN NS ns1.sample.com.
@ IN NS ns2.sample.com.
; Address records:
www IN A 192.168.1.100
ns1 IN A 192.168.1.1
ns2 IN A 192.168.1.2
maill IN A 192.168.1.200
mail2 IN A 192.168.1.201
test IN A 192.168.1.45
```

```
; Aliases:
ftp
; IN CNAME www
; MX records
@ IN MX 10 mail1.onecoursesource.com.
@ IN MX 20 mail2.onecoursesource.com.
```

在完成这些更改后，我建议重启你的 BIND 服务器并进行一些简单的测试（可以使用下一节描述的 `dig`、`nslookup` 或 `host` 命令完成）。

你还需要创建一个反向区域文件，它要简单得多，因为你只需要 `SOA` 记录、`NS` 记录和指针（`PoInter`）记录。参见示例 21-4。

### 示例 21-4 的 /var/named/db.192.168.1 文件

```
$TTL 1D
@ IN SOA ns.sample.com. root.sample.com. (
      0 ; serial
      1D ; refresh
      1H ; retry
      1W ; expire
      3H ) minimum
)
; Nameservers:
@ IN NS ns1.sample.com.
@ IN NS ns2.sample.com.
; Address records:
