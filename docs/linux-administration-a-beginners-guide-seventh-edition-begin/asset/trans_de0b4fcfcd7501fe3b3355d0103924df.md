

# 第 16 章 域名命名系统 (DNS) 435

示例服务器条目所示：

```
server 192.168.1.12 {
  bogus no;
  transfer-format many-answers;
};
```

**区域语句 (The Zone Statement)** *zone* 语句允许你定义一个 DNS 区域——该区域的定义通常令人困惑。这里是细节：*DNS 区域不等同于 DNS 域名。* 两者之间的区别微妙，但至关重要。

让我们回顾一下：域名是根据组织边界划分的。单一组织可以被划分为更小的管理子域。每个子域都有自己的名称。所有域名共同构成了整个域名。

例如，一个域名就是一个域名。它内部包含子域：.example.org、.marketing.example.org、.sales.example.org 和 .admin.example.org。这四个子域中的每一个都有自己的区域。而 example.org 内部还有一些不属于任何子域的主机；因此，它有自己的区域。结果是，example 实际上由五个区域组成。

在最简单的模型中，如果一个域名没有子域，那么区域和域名在主机、配置等方面的定义是相同的。

接下来的章节将讨论在 **named.conf** 文件中设置区域的流程。

# 配置 DNS 服务器

早些时候，你学习了主服务器（primary）、从服务器（secondary）和缓存（caching）名称服务器之间的区别。回顾一下：主名称服务器包含该区域的最新 DNS 信息的数据库。当区域管理员想要更新这些数据库时，主名称服务器首先获取更新，而世界其他部分则向它请求更新。从服务器会显式地跟踪主服务器，并在发生更改时通知从服务器。主服务器和从服务器在回答中被认为具有等同的权威性。缓存名称服务器没有权威记录，只有缓存条目。

# 在 named.conf 文件中定义主区域

*zone domain-name* 条目的最基础的语法如下：

```
zone domain-name {
  type master;
  file path-name;
};
```

*path-name* 指向包含该区域数据库信息的文件。例如，要为域名 example.org 创建一个区域，其数据库文件位于 /var/named/example.org.db，你需要在 named.conf 文件中创建以下区域定义：

```
zone "example.org" {
  type master;
  file "example.org.db";
}
```

注意，在 named.conf 文件指定的目录选项会自动为 example.org 文件名加上以前缀。因此，如果指定的目录为 /var/named，服务器软件将在 /var/named/example.org.db 查找 example.org 信息。

在这里创建的区域定义只是一个正向引用——也就是说，其他人查找名称并获取由你的名称服务器管理的 example.org 域名下的系统 IP 地址的机制。提供反向到主机的映射（in-to-hostname mapping）符合互联网礼仪（如果你想向某些站点发送电子邮件也是必要的）。要做到这一点，请在 in-add.arpa 域名中提供条目。

in-add.arpa 条目的格式是你的 IP 地址的前三个字节，并通过 in-add.arpa 进行反转。假设 example.org 的网络地址为 192.168.1，则 in-add.arpa 域名将是 1.168.192.in-addr.arpa。因此，named.conf 文件下对应的区域状态如下：

```
zone "1.168.192.in-addr.arpa" {
  type master;
  file "example.org.rev";
}
```

注意，在区域部分使用的文件名（example.org.db 和 example.org.rev）是完全任意的。你可以自由选择自己的命名规范，只要它对你有意义即可。

example.org 区域状态在整个 named.conf 文件中的确切位置将在后的“DNS 服务器设置步骤演练”章节中显示。

# 附加选项

主域名还可以使用 options 语句中的以下配置选择：

- check-names
- allow-update
- allow-query
- allow-transfer
- notify
- also-notify

在区域配置中使用任何这些选项都将只会影响该区域。

# 在 named.conf 文件中定义从区域

从服务器的区域条目格式与主服务器类似。对于正向解析，格式如下：

```
zone domain-name {
    type slave;
    masters IP-address-list;
    file path-name;
};
```

在这里，domain-name 是主名称服务器上指定的精确区域名称，IP-address-list 是存在该区域的主名称服务器的 IP 地址列表，而 path-name 是服务器存放主文件副本的完整路径位置。

# 附加选项

从区域配置也可以使用 options 语句中的一些配置选择：

- check-names
- allow-update
- allow-query
- allow-transfer
- max-transfer-time-in

# 在 named.conf 文件中定义缓存区域

缓存配置是所有配置中最简单的。它是每个 DNS 服务器配置的必要条件，即使你运行的是主服务器或从服务器。这是服务器递归搜索 DNS 树以查找互联网上其他主机的必要条件。

对于缓存服务器，我们定义三个区域部分。

（注：原文后续部分似乎存在重复或截断的内容，翻译在此处结束，已根据指令处理所有有效文本)

