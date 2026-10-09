

在启动 DNS 缓存之前，你需要修改 `/etc/resolv.conf` 文件（第 496 页）。如何修改此文件取决于 `resolvconf` 包是否已安装并设置为在本地系统上运行。当你输入命令 `resolvconf` 时，如果显示用法消息，说明该包已安装；如果显示 `not installed` 消息，则说明它未安装。

如果 `resolvconf` 未安装，或者你已按照“named options”中的说明将其关闭，请在 `/etc/resolv.conf` 中，在其他 nameserver 行之前添加以下行：

```
nameserver 127.0.0.1
```

如果 `resolvconf` 已安装并设置为在运行 `bind9` init 脚本（第 834 页）时重建 `resolv.conf`，请将上述行放入 `/etc/resolvconf/resolv.conf.d/head` 文件中，放在注释之后、其他 nameserver 行之前。你可以忽略提示不要编辑该文件的注释：此注释是针对尝试编辑 `/etc/resolv.conf` 的人的。你必须将此行放入 `head` 文件中，以便 `resolvconf` 在任何其他 nameserver 行之前将其放入 `resolv.conf`；否则，本地 DNS 缓存将永远不会被使用。如有需要，将其他 nameserver 行放入同一目录下的 `base` 文件中。

nameserver 行告诉解析器将本地系统（`localhost` 或 127.0.0.1）用作主要名称服务器。若要尝试使用本地系统作为唯一的名称服务器，请在 `resolv.conf` 或 `base` 中注释掉其他 nameserver 行，方法是每行前面加上井号（#）。

最后，运行 `bind9` init 脚本以重启 `named` 守护进程（第 834 页）。这样做时，如果 `resolvconf` 已安装并设置为运行，`bind9` init 脚本将重建 `resolv.conf`。有关 `resolv.conf` 的更多信息，请参阅 `resolver` 和 `resolv.conf` 的手册页。

参考第 849 页的“Troubleshooting”（故障排除）部分，了解如何确认 DNS 缓存是否正常工作。一旦重启了 `named`，你可以通过使用 `dig` 查询远程系统的 IP 地址来查看缓存的效果：

```
$ dig www.ubuntu.com
```

```
;; DiG 9.7.0-P1 ;; www.ubuntu.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<< opcode: QUERY, status: NOERROR, id: 19622
; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 3, ADDITIONAL: 0

;; QUESTION SECTION:
;www.ubuntu.com. IN A

;; ANSWER SECTION:
www.ubuntu.com. 585 IN A 91.189.90.40

; Query time: 496 msec
; SERVER: 127.0.0.1#53(127.0.0.1)
; WHEN: Mon Apr 5 16:45:38 2010
; MSG SIZE rcvd: 112
```

上一页示例中倒数第四行显示，此查询耗时 496 毫秒（大约半秒）。当你再次运行相同的查询时，速度会更快，因为 DNS 缓存已在本地内存中保存了信息：

```
$ dig www.ubuntu.com
...
;; Query time: 1 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Mon Apr 5 16:45:46 2010
;; MSG SIZE rcvd: 112
```

## 配置 DNS 服务器

本节讨论 `/etc/bind/named.conf` 文件、区域文件、DNS 缓存的实现以及在 chroot  jail 中运行 DNS。

### named.conf：named 配置文件

**named** 的配置信息保存在 `/etc/bind/named.conf` 中。默认情况下，区域文件位于 `/etc/bind`。如果正在 chroot jail 中运行 **named**，这些文件保存在 `/var/lib/named/etc/bind` 中，并在 `/etc/bind`（第 847 页）中有一个链接。

#### 尽量不修改 named.conf

> **提示** Ubuntu 的 **bind9** 包将随 BIND 分发的 **named.conf** 文件拆分为四个文件：**named.conf**、**named.conf.default-zones**、**named.conf.local** 和 **named.conf.options**。拆分此文件有两个动机。首先，这使得配置文件更容易理解。其次，它允许你在不修改 **named.conf** 的情况下配置 **named**。这种设置允许升级 **bind9** 包（包括对 **named.conf** 的更改），而无需你修改本地配置。

在配置 **named** 时，请尽量将更改放入 **named.conf.options** 和 **named.conf.local** 文件中。对于更复杂的设置，在升级 **bind9** 时可能更容易修改 **named.conf** 并保留这些更改。

#### IP-list

在本节的描述中，**IP-list** 是一个以分号分隔的 IP 地址列表，其中每个 IP 地址后面可选地跟一个斜杠和子网掩码长度（第 462 页）。在 *IP-list* 前加一个感叹号 (!) 表示取反。*IP-list* 中可使用的内置名称包括 **any**、**none** 和 **localhost**。必须将这些内置名称用双引号括起来。

#### 注释

在 **named.conf** 中，通过在前面加一个井号（\#），如 Perl 或 shell 程序那样；在前面加双斜杠（//），如 C++ 程序那样；或者将其封闭在 /* 和 */ 之间，如 C 程序那样，来指定注释。在 DNS db.* 文件中，注释以分号 (;) 开头。

#### 包含文件

named.conf 文件中的 include 语句将其参数命名的文件包含进来，就好像其内容内联出现在 named.conf 文件中一样。默认的 Ubuntu named.conf 文件包含了 /etc/bind/named.conf.options、/etc/bind/named.conf.local 和 /etc/bind/named.conf.default-zones 文件。named.conf.options 文件保存 named.conf 的 Options 子句。named.conf.local 文件提供了一个放置本地配置信息的场所。named.conf.default-zones 文件定义了默认区域。

#### OPTIONS 子句

Options 语句可以出现在两个地方：位于 named.conf.options 中的 Options 子句，以及位于 named.conf.default-zones 中的 Zone 子句。Options 子句中的 Option 语句全局适用。当 Option 语句出现在 Zone 子句中时，该选项适用于该区域，并且在该区域内覆盖对应的全局选项。

Options 子句以关键字 options 开始，后面跟着由大括号包围的语句。以下是部分 Option 语句的列表。只能在 Options 子句中出现以及不能在 View 子句（第 855 页）中出现的语句已作标注。

- **allow-query [IP-list]**
  仅允许来自 IP-list 的查询。如果没有此选项，服务器将响应所有查询。
- **allow-recursion [IP-list]**
  指定服务器将为其执行递归查询（第 825 页）的系统。对于不在 IP-list 中的系统，服务器仅执行迭代查询。如果没有此选项，服务器将为任何系统执行递归查询。此语句可能被 recursion 语句覆盖。
- **allow-transfer [IP-list]**
  指定允许从此服务器执行区域传输的系统。指定 "none"（包含引号）的 IP-list 以阻止区域传输。对于更安全的网络，仅在 IP-list 中包含受信任的系统，因为列表中的系统可以获得网络上所有系统的列表。
- **directory path**
  指定包含区域文件的目录的绝对路径名。在 Ubuntu Linux 下，此目录最初是 /var/cache/bind。named.conf 中指定的相对路径名是相对于此目录的。仅 Options 子句；不在 View 子句中。
- **forward ONLY|FIRST**
  ONLY 转发所有查询，如果未收到答案则失败。FIRST 转发所有查询，如果查询未收到答案，则尝试使用附加查询查找答案。仅与 forwarders 语句有效。
- **forwarders (IP [port] ; [..])**
  指定查询被转发到的 IP 地址和可选的端口号。参见 **forward** 语句。
- **notify YES|NO**
  YES 在区域信息更改时向该区域的从服务器发送消息。仅限主服务器。参见第 854 页。
- **recursion YES|NO**
  YES（默认）在客户端请求时提供递归查询（第 825 页）。NO 仅提供迭代查询（第 825 页）。如果答案出现在服务器缓存中，则总是返回答案。此语句覆盖 **allow-recursion** 语句。仅 Options 子句。

### ZONE 子句

Zone 子句定义一个区域，可以包含 Options 子句中列出的任何语句，除非另有说明。Zone 子句由关键字 **zone**、用双引号括起来的区域名称和类（始终是 IN）引入。Zone 子句的主体由包围一个或多个区域语句的一对大括号组成。参见第 840 页 **named.conf.default-zones** 的列表以获取 Zone 子句的示例。以下是部分区域语句的列表：

- **allow-update (IP-list)**
  指定允许动态更新此区域的系统。当托管由本地管理员以外的人拥有的域的主 DNS 服务器时，此语句可能很有用，因为它允许远程用户更新 DNS 条目，而无需授予该用户访问服务器的权限。
- **file filename**
  指定 *zone file*——指定区域特征的文件。*file-name* 是相对于 Options 子句中 **directory** 语句指定的目录的。file 语句对于主区域和提示区域是强制性的。对从区域包含它是一个好主意（参见 **type**）。
- **masters (IP-list)**
  指定从区域可用于更新区域文件的系统。仅限从区域。
- **type ztype**
  指定此子句定义的区域类型。从以下列表中选择 ztype：
    - **forward**—指定正向区域，该区域将指向此区域的查询进行转发。参见 Options 子句中的 **forward** 和/或 **forwarders** 语句。
    - **hint**—指定提示区域。提示区域列出了本地服务器在启动时以及当其无法在缓存中找到答案时所查询的根服务器。
    - **master**—指定本地系统作为此区域的主主服务器（第 826 页）。
    - **slave**—指定本地系统作为此区域的从服务器（第 826 页）。

### 区域文件

区域文件定义区域特征。区域名称通常在 **named.conf.default-zones** 中指定。与 **named.conf** 和 **named.conf.local** 相反，区域文件在域名末尾使用句点。参见第 841 页获取区域文件的示例。

