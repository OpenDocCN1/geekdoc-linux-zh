

*   **序列号**（Serial Number）——序列号是 BIND 跟踪区域文件新近程度的方式。每次更新区域文件时，你都必须递增该数字，以便 BIND 知道需要从该文件刷新其信息。标准做法是使用 `YYYYMMDDN` 格式作为该数字；最后两位数字表示一天内的修订版本。在进行更改时，更新该数字以反映当前日期。

> **注意**
> 当你使用 `ndc reload` 来刷新主区域文件的信息时，无论序列号如何，BIND 都会自动确定数据需要刷新。然而，保持序列号的准确性是一个好习惯；这将确保在某些情况下（例如手动刷新从区域数据）的正常操作。

*   **刷新间隔**（Refresh）——此数字（以秒为单位）指定从服务器应多久检查一次主服务器以获取更新的区域数据。如果自上次区域传输以来主服务器的序列号已更改，则执行新的区域传输。
*   **重试间隔**（Retry）——如果无法联系到主服务器，从服务器将按此数字指定的间隔（以秒为单位）进行重试。
*   **过期时间**（Expire）——如果在此时间（以秒为单位）内无法联系到主服务器，从服务器将丢弃该区域的所有数据。
*   **最小 TTL**（Minimum TTL）——此数字（以秒为单位）指定“负缓存”响应（指示数据缺失）应保留多久。

## 名称服务器（NS）记录

列表 31.2 显示了以下示例名称服务器（NS）记录：

```
; DNS Servers
@      IN NS         stirpes.somewhere.com.
@      IN NS         spots.somewhere.com.
```

这些记录指定了允许对有关该区域的查询提供权威答案的 DNS 服务器。请注意，`@` 符号指向当前的 `$ORIGIN`（在这种情况下是 somewhere.com），并且两个服务器名称都有末尾点（表示它们是绝对名称）。

你可以为子域或当前区域中的区域创建 NS 记录。例如，假设你在名为 cluster.somewhere.com. 的区域中有一组机器，它们的 DNS 信息由自己的名称服务器（ns.cluster.somewhere.com）处理。为该服务器创建的一个有效 NS 记录，允许外部主机查询该服务器的集群 IP 地址，如下所示：

```
cluster IN NS         ns.cluster.somewhere.com.
```

请记住，通过省略 `cluster` 的末尾点，当前的 `$ORIGIN`（`somewhere.com.`）将由 BIND 附加到其后。

## 地址（A）记录

地址（A）记录是你用来将主机名与 IP 地址关联的记录。我们的示例包含以下记录：

```text
; Machine Names
localhost           IN A      127.0.0.1
stripes             IN A      64.41.131.162
spots               IN A      64.41.131.163
mail                IN A      64.41.131.167
@                   IN A      64.41.131.162
```

这些记录的含义相当直接。左侧的非限定名称会用当前的 `$ORIGIN` 进行扩展。因此，`mail.somewhere.com` 将解析为 `64.41.131.167`。类似地，`@` 符号会扩展，因此对 `somewhere.com` 的查询将返回 `64.41.131.162`。

在 A 记录中定义的名称被称为*规范名称*，与*别名*（由 CNAME 记录定义）相对。

## 规范名称（CNAME）记录

规范名称（CNAME）记录用于创建别名。术语是这样的，在我们列表 31.2 的示例中，别名 `www`（通过 `$ORIGIN` 扩展为 `www.somewhere.com.`）指向规范名称 `@`，即 `somewhere.com.`（其 IP 地址在 A 块中定义）：

```text
; Aliases
www                 IN CNAME        @
ftp                 IN CNAME        www.somewhere.com.
```

CNAME 记录通常很有用，因为它们不直接绑定到 IP 地址。例如，你可以使用 CNAME 记录指向其他区域中的名称，然后由该区域的所有者进行控制。此外，如果 IP 地址发生更改，CNAME 记录有助于减少必须在区域文件中进行的更改数量。

## 邮件交换器（MX）记录

邮件交换器（MX）记录定义了哪些主机将用于向该区域内的地址投递邮件。Sendmail（和其他 MTA）查找区域内优先级最高的 MX 记录并与其建立连接；你可以使用 `host` 命令查找域名的 MX 主机：

```
# host somecompany.com
somecompany.com has address 207.114.98.18
somecompany.com mail is handled (pri=100) by mail.uu.net
somecompany.com mail is handled (pri=5) by mx-1.somecompany.com
```

每个 MX 记录都有一个相关的“优先级”数字，该域名的邮件服务器将按照数值从最低到最高的顺序尝试，直到可以建立成功的 SMTP 连接为止。优先级作为记录值字段的一部分指定，如下例所示：

```
; MX Record
@             IN MX   10 mail.somewhere.com.
```

> **警告**
>
> MX 记录不能指向 IP 地址。此外，如果检测到 MX 记录指向 CNAME，许多 MTA 和邮件客户端会提出警告。确保你的 MX 记录指向在其他地方用 A 记录定义的名称！

## 指针（PTR）记录

指针（PTR）记录是 A 或 CNAME 记录的逆，用于反向 DNS 区域文件（例如 131.41.64.in-addr.arpa）中，将 IP 地址映射到域名。反向 DNS 区域文件的示例如列表 31.3 所示。

由于反向 DNS 查找只返回单个名称，针对同一 IP 地址的多个 PTR 记录毫无用处，只会使情况变得混乱。因此，反向文件通常比其对应的正向文件短。

## 反向 DNS 区域文件

反向 DNS 区域文件定义了形如 131.41.64.in-addr.arpa 的区域，用于将 IP 地址映射到名称。此类文件在 `named.conf` 中被引用，并像正向 DNS 区域文件一样传播到从服务器。列表 31.3 显示了一个示例反向 DNS 区域文件。

**列表 31.3 131.41.64.in-addr.arpa 区域的示例反向 DNS 区域文件**

```
TTL 3600

131.41.64.in-addr.arpa.   IN SOA stripes.somewhere.com. root.somewhere.com. (
                         2001061000    ; Serial
                         10800       ; Refresh
                         3600        ; Retry
```

请注意使用 PTR 记录而不是 A 或 CNAME 记录。每个 PTR 指向的名称是该 IP 地址的真正规范名称。反向文件中也不需要 MX 记录，因为 MX 记录首先就不能与 IP 地址相关联。

## 创建 localhost 区域文件

必须存在一个特殊的区域文件，才能使 `localhost` 区域（`0.0.127.in-addr.arpa`）正常工作。`/etc/namedb` 中有一个 shell 脚本可帮助你创建一个。该脚本名为 `make-localhost`，它读取一个模板（`PROTO.localhost.rev`）并填入从你的输入中派生的信息。由于它没有被设置为可执行，你必须使用 `sh` 命令运行它：

```
# sh make-localhost
Enter your domain name: somewhere.com
```

生成的文件 `/etc/namedb/localhost.rev` 应该看起来像列表 31.4 所示。

**列表 31.4**
自动生成的 `localhost.rev` 区域文件

```
; From: @(#)localhost.rev 5.1. (Berkeley) 6/30/90
;$FreeBSD: src/etc/namedb/PROTO.localhost.rev,v 1.6 2000/01/10 15:31:40 peter Exp $
;
;
;This file is automatically edited by the `make-localhost' script in
;the /etc/namedb directory.
;
$TTL	3600
@ 	IN 	SOA 	stripes.somewhere.com. root.stripes.somewhere.com. (
		20010612		; Serial
		3600		; Refresh
		900		; Retry
```

列表 31.4（续）

在完全部署你的 DNS 服务之前，请确保创建此文件！

## 配置缓存名称服务器

完全有可能运行一个不对任何区域拥有权威的名称服务器。这就是所谓的*缓存名称服务器*，其工作仅仅包括在客户端提示时发起 DNS 查询并存储结果以供日后使用。这与我们在本章前面讨论的 *forward only*（仅转发）选项的效果相反。*forward only* 名称服务器会将所有请求交给其转发器处理，而缓存名称服务器则自行执行所有被请求的任务并缓存结果。其他名称服务器可以使用此服务器作为转发器，利用它已经完成的工作。

要配置缓存名称服务器，只需从你的 named.conf 文件中省略除自身运行所必需的语句外的所有区域语句。列表 31.5 显示了此类配置。

**列表 31.5 /etc/namedb/named.conf 文件的示例**

```
/*
 * A simple BIND 8 configuration
 */

logging {
 category lame-servers { null;};
 category cname { null;};
};

options {
 directory "/etc/namedb";
};

zone "." {
 type hint;
 file "named.boot";
};

zone "0.0.127.in-addr.arpa" in {
 type master;
```

