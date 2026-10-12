
## 使用 Dlint 检查 DNS 配置

配置不当的 DNS 服务器可能带来巨大的安全风险，因为它们很容易被利用。你可以使用一个名为 Dlint 的免费工具来分析任何 DNS 区域，并对下面列出的许多常见配置问题生成报告：

- 主机名如果有 A 记录也必须有 PTR 记录。DNS 配置中如果有 A 记录但没有对应的 PTR 记录，则希望对主机执行反向 DNS 查找的服务器无法验证。Dlint 将检查配置中发现的任何 A 记录是否缺少 PTR 记录。
- in-addr.arpa 区域中的每个 PTR 记录都应有等效的 A 记录。PTR 记录缺少的 A 记录将被报告。
- Dlint 将递归遍历子域（子区域）并查找其中的配置问题。
- 常见的拼写错误或放置不当的注释可能会导致配置不正确；Dlint 试图捕获此类错误。

现在让我们看看如何在系统上安装 Dlint。

## 获取 Dlint

你可以从 www.domtools.com/dns/dlint.shtml 下载 Dlint。截至本文撰写时，Dlint 的最新版本是 1.3.2。你也可以在 www.domtools.com/cgi-bin/dlint/nph-dlint.cgi 使用 Dlint 的在线版本。然而，在线版本有时间限制，因此仅建议用于尝试该工具。我强烈建议你在线尝试并下载源代码以在系统上安装它。

## 安装 Dlint

Dlint 需要 dig 和 Perl 5。dig 是 BIND 发行版中包含的 DNS 查询实用程序。很可能你已经安装了它。运行 `dig localhost any` 命令查看系统上是否有 dig。如果没有，你可以从 www.isc.org/bind.html 获取 dig。我假设你的 Linux 系统上已安装 dig 和 Perl 5。

要安装 Dlint，请执行以下操作：

- 1. 以 root 身份在合适的目录中提取 Dlint 源代码包。我使用 `tar xvf dlint1.4.0.tar` 命令在 `/usr/src/redhat/SOURCES` 目录中提取了 `dlint1.4.0.tar` 包。提取源代码分发时将创建一个新的子目录。切换到新目录，在我的例子中是 `dlint1.4.0`。请确保在本文档中给出的所有说明中替换为你下载的源代码分发包的适当 Dlint 版本号。
- 2. 运行 `which perl` 命令查看 Perl 解释器安装在何处。
- 3. 运行 `head -1 digparse` 命令查看 Dlint 使用的 `digparse` Perl 脚本的第一行。如果 `#!` 字符后显示的路径与 `which perl` 命令显示的路径匹配，则无需更改它。如果不匹配，请使用文本编辑器修改此文件，并将 `#!` 后的路径替换为你的 Perl 解释器的路径。
- 4. 运行 `make install` 命令安装 Dlint，这将把 `dlint` 和 `digparse` 脚本安装到 `/usr/local/bin` 中。

## 运行 Dlint

Dlint 包中的主脚本称为 dlint。你可以使用以下命令运行此脚本：

/usr/local/bin/dlint domain | in-addr.arpa-domain

例如，要为名为 evoknow.net 的域运行 dlint，你可以执行 `/usr/local/bin/dlint evoknow.net`。清单 15-10 显示了示例输出。

### 清单 15-10 dlint 的示例输出

```
;; run starting: Sat Dec 29 13:34:07 EST 2001
;; =============================================================
```

```
;; Now linting domain.com
;; Checking serial numbers per nameserver
;;      2001122901 ns2.domain.com.
;;      2001122901 ns1.domain.com.
;; All nameservers agree on the serial number.
;; Now caching whole zone (this could take a minute)
;; trying nameserver ns1.domain.com.
;; 3 A records found.

ERROR: "ns1.domain.com. A 172.20.15.1", but the PTR record for
    1.15.20.172.in-addr.arpa. is "k2.domain.com."

One of the above two records are wrong unless the host is a name server
or mail server.

To have 2 names for 1 address on any other hosts, replace the A record
with a CNAME record:
ns1.domain.com. IN      CNAME   k2.domain.com.

ERROR: "ns2.domain.com. A 172.20.15.1", but the PTR record for
    1.15.20.172.in-addr.arpa. is "k2.domain.com."

One of the above two records are wrong unless the host is a name server
or mail server.

To have 2 names for 1 address on any other hosts, replace the A record
with a CNAME record:
ns2.domain.com. IN      CNAME   k2.domain.com.

;; ==============================================
;; Now linting domain.com.
;; Checking serial numbers per nameserver
;;      2001122901 ns1.domain.com.
;;      2001122901 ns2.domain.com.
;; All nameservers agree on the serial number.
;; Now caching whole zone (this could take a minute)
```

### 清单 15-10 继续

```
;; trying nameserver ns1.domain.com.
;; 3 A records found.

ERROR: "ns1.domain.com. A 172.20.15.1", but the PTR record for
    1.15.20.172.in-addr.arpa. is "k2.domain.com."

One of the above two records are wrong unless the host is a name
server or mail server.

To have 2 names for 1 address on any other hosts, replace the A record
with a CNAME record:
ns1.domain.com. IN     CNAME   k2.domain.com.

ERROR: "ns2.domain.com. A 172.20.15.1", but the PTR record for
    1.15.20.172.in-addr.arpa. is "k2.domain.com."

One of the above two records are wrong unless the host is a name
server or mail server.

To have 2 names for 1 address on any other hosts, replace the A record
with a CNAME record:
ns2.domain.com. IN     CNAME   k2.domain.com.

;; no subzones found below domain.com., so no recursion will take place.
;; ==============================================================
;; dlint of domain.com. run ending with errors.
;; run ending: Sat Dec 29 13:34:09 EST 2001
;; ==============================================================
;; dlint of domain.com run ending with errors.
;; run ending: Sat Dec 29 13:34:09 EST 2001
```

如你所见，dlint 输出非常详细。以分号开头的行被视为注释。所有其他行都是警告或错误。这里，domain.com 有一组问题。ns1.domain.com 有一个 A 记录，但 PTR 记录指向 k2.domain.com 而不是 ns1.domain.com。同样，ns2.domain.com 主机也有相同的问题。换句话说，domain.com 配置有以下行：

```
ns1      IN      A      172.20.15.1
ns2      IN      A      172.20.15.1
k2       IN      A      172.20.15.1
```

它还具有以下 PTR 记录：

```
1      IN      PTR      k2.evoknow.net.
```

dlint 程序建议使用 CNAME 记录来解决此问题。换句话说，配置应为：

```
ns1    IN  A    172.20.15.1
ns2    IN  CNAME  ns1
k2     IN  CNAME  ns1
```

PTR 记录应为：

```
1      IN      PTR      ns1.evoknow.net.
```

在 domain.com 的相应配置 DNS 文件中修复错误后，执行 /usr/local/bin/dlint domain.com 命令会产生以下输出。

```
;; run starting: Fri Dec 29 13:38:00 EST 2000
;; ==============================================
;; Now linting domain.com
;; Checking serial numbers per nameserver
;;     2001122901 ns2.domain.com.
;;     2001122901 ns1.domain.com.
;; All nameservers agree on the serial number.
;; Now caching whole zone (this could take a minute)
;; trying nameserver ns1.domain.com.
;; 1 A records found.
;; ==============================================
;; Now linting domain.com.
;; Checking serial numbers per nameserver
;;     2001122901 ns1.domain.com.
;;     2001122901 ns2.domain.com.
;; All nameservers agree on the serial number.
;; Now caching whole zone (this could take a minute)
;; trying nameserver ns1.domain.com.
;; 1 A records found.
;; no subzones found below domain.com., so no recursion will take place.
;; ==============================================
```

```
;; dlint of domain.com. run ending normally.
;; run ending: Fri Dec 29 13:38:01 EST 2000
;; ==============================================
;; dlint of domain.com run ending normally.
;; run ending: Fri Dec 29 13:38:01 EST 2000
```

如前所述，未报告任何错误信息。当然，dlint 不能捕获配置中的所有错误，但它是在创建、更新或删除 DNS 配置信息时执行质量控制的绝佳工具。

## 保护 BIND

BIND 9.x 由一支庞大的专业软件开发团队编写，以支持下一代 DNS 协议演进。新的 BIND 支持后端数据库、授权和事务安全功能、基于 SNMP 的管理、IPv6 功能等。新的 BIND 的代码库经过审计，并以支持任何感兴趣的人频繁审计的方式编写。

新的 BIND 现在支持 DNSSEC 和 TSIG 安全标准。

## 使用事务签名 (TSIG) 进行区域传输

事务签名 (TSIG) 可用于验证和验证 DNS 数据交换。这意味着你可以使用 TSIG 来控制你管理的域的区域传输。

通常，区域传输发生在主名称服务器到辅助名称服务器之间。在以下主名称服务器的 named.conf 段中，访问控制列表 (ACL) dns-ip-list 中列出的 IP 地址仅允许传输 yourdomain.com 域的区域信息。

```
acl "dns-ip-list" {
    172.20.15.100;
    172.20.15.123;
};
```
