
`named.conf` 文件是 BIND 的主配置文件。根据该文件的规范，BIND 决定它应该如何运行以及必须读取哪些配置文件（如果有的话）。本节涵盖了设置通用 DNS 服务器所需要的内容。你可以在 BIND 的文档中找到关于新文件格式的完整指南。`named.conf` 文件的通用格式如下：

```bind
statement {
    // comments
}
```

`statement` 关键字告诉 BIND 我们正要描述其操作的一个特定方面，以及适用于该语句的选项。大括号 `{}` 是必须的，以便 BIND 知道哪些选项与哪些语句相关；每个选项后面以及闭合大括号后面都要紧跟一个分号 `;`。例如下：

```bind
options {
    directory "/var/named"; // 将配置文件存放在 /var/named
}
```

这意味着这是一个选项语句（option statement）。这里的特定选项是指定 BIND 工作目录的指令——即本地系统中存放命名服务器配置数据的目录。

### 细节

本节记录了你在典型的 `named.conf` 文件中会看到的许多注释。处理此问题的良方法是先快速浏览一遍，然后将其作为后续章节的参考。如果你在第一次阅读时发现某些指令看起来很奇怪或不合逻辑，请不要担心。一旦你稍后看到它们被使用，其原理和原因很快就会明朗了。

### 注释

注释可以是以下格式之一：

| 格式 | 表示 |
| :--- | :--- |
| `//` | C++ 风格注释 |
| `/*...*/` | C 语言风格注释 |
| `#` | Perl 和 UNIX shell 风格注释 |

在第一种和最后一种样式（C++ 和 Perl/UNIX shell）中，一旦开始写注释，它将一直持续到行尾。在普通的 C 风格注释中，需要使用 `*/` 来表示注释的结束。这使得 C 风格的注释便于编写多行注释。不过，你可以选择任何你喜欢的注释格式并坚持使用。没有哪种风格是优于另一种的。

### 语句关键字

以下是一些最频繁使用的语句关键字：

| 关键字 | 描述 |
| :--- | :--- |
| `acl` | 访问控制列表——决定他人对你的 DNS 服务器拥有何种访问权限 |
| `include` | 允许你包含另一个文件，并将该文件视为 `named.conf` 文件的一部分 |
| `logging` | 指定记录哪些信息以及忽略哪些信息。对于记录的信息，你还可以指定日志记录的位置。 |
| `options` | 解决全局服务器配置问题。 |
| `controls` | 允许你控制供 `rndc` 工具使用的通道。 |
| `server` | 设置特定服务器配置选项。 |
| `zone` | 定义 DNS 区域。 |

我们将在接下来的章节中详细讨论四个最常用的关键字（`include`、`logging`、`server` 和 `zone`）。

**`include` 语句** 如果你发现你的配置文件开始变得臃肿，你可能想要考虑将文件拆分为更小的组件。每个文件都可以包含在 `named.conf` 文件中。请注意，你不能在语句内部使用 `include` 语句。

这是一个 `include` 语句的示例：

```bind
include "/path/to/filename_to_included";
```

> NOTE 所有 C 和 C++ 程序员们：尽管你的直觉告诉你想那样，请确保不要用井号 (`#`) 开始包含行！该符号用于在 `named.conf` 文件中开始注释。

**`logging` 语句** `logging` 语句用于指定你需要的信息及其位置。当此语句与 `syslog` 结合使用时，你将获得一个强大且可配置的日志系统。记录的项目是关于 `named` 状态的信息。默认情况下，它们记录在 `/var/log/messages` 文件中。简单来说地，各种类型的日志根据预定义的类别或通道分组；例如有安全日志类别、通用类别、解析器类别、查询类别等。

遗憾的是，此 `logging` 语句的可配置性是以复杂性为代价的，但默认设置对于大多数用户足够。这是一个简单的日志指令示例：

```bind
logging {
    category default { default_syslog };
    category queries { default_syslog };
};
```

> NOTE 列表中增加了行号以提高可读性。

**`server` 语句** `server` 语句告诉 BIND 关于它可能处理的其他命名服务器的特定信息。`server` 语句的格式如下：

```bind
server ip-address {
    bogus yes/no;
    keys { string; [string; ...] };
    transfer-format one-answer/many-answers;
    <other options>...
};
```

这里，第一行的 `ip-address` 是目标远程服务器的 IPv4 或 IPv6 地址。第 2 行的 `bogus` 选项在处理可能向你发送配置错误的站点时有用。第 3 行的 `keys` 子句指定由 `key` 语句定义的 `key_id`，用于加密与远程服务器通信的事务。该密钥用于生成请求签名，并附加在与远程命名服务器交换的消息中。第 4 行的 `transfer-format` 告诉 BIND 远程命名服务器是否可以在单次查询响应中接受多个答案。

# 第 16 章 域名命名系统 (DNS) 435

示例服务器条目所示：

```
server 192.168.1.12 {
  bogus no;
  transfer-format many-answers;
};
```

**区域语句 (The Zone Statement)** `zone` 语句允许你定义一个 DNS 区域——该区域的定义通常令人困惑。这里是细节：*DNS 区域不等同于 DNS 域名。* 两者之间的区别微妙，但至关重要。

让我们回顾一下：域名是根据组织边界划分的。单一组织可以被划分为更小的管理子域。每个子域都有自己的名称。所有域名共同构成了整个域名。

例如，一个域名就是一个域名。它内部包含子域：`.example.org`、`.marketing.example.org`、`.sales.example.org` 和 `.admin.example.org`。这四个子域中的每一个都有自己的区域。而 `example.org` 内部还有一些不属于任何子域的主机；因此，它有自己的区域。结果是，`example` 实际上由五个区域组成。

在最简单的模型中，如果一个域名没有子域，那么区域和域名在主机、配置等方面的定义是相同的。

接下来的章节将讨论在 **`named.conf`** 文件中设置区域的流程。

# 配置 DNS 服务器

早些时候，你学习了主服务器（primary）、从服务器（secondary）和缓存（caching）名称服务器之间的区别。回顾一下：主名称服务器包含该区域的最新 DNS 信息的数据库。当区域管理员想要更新这些数据库时，主名称服务器首先获取更新，而世界其他部分则向它请求更新。从服务器会显式地跟踪主服务器，并在发生更改时通知从服务器。主服务器和从服务器在回答中被认为具有等同的权威性。缓存名称服务器没有权威记录，只有缓存条目。

# 在 named.conf 文件中定义主区域

`zone domain-name` 条目的最基础的语法如下：

```
zone domain-name {
  type master;
  file path-name;
};
```

`path-name` 指向包含该区域数据库信息的文件。例如，要为域名 `example.org` 创建一个区域，其数据库文件位于 `/var/named/example.org.db`，你需要在 `named.conf` 文件中创建以下区域定义：

```
zone "example.org" {
  type master;
  file "example.org.db";
}
```

注意，在 `named.conf` 文件指定的目录选项会自动为 `example.org` 文件名加上以前缀。因此，如果指定的目录为 `/var/named`，服务器软件将在 `/var/named/example.org.db` 查找 `example.org` 信息。

在这里创建的区域定义只是一个正向引用——也就是说，其他人查找名称并获取由你的名称服务器管理的 `example.org` 域名下的系统 IP 地址的机制。提供反向到主机的映射（in-to-hostname mapping）符合互联网礼仪（如果你想向某些站点发送电子邮件也是必要的）。要做到这一点，请在 `in-add.arpa` 域名中提供条目。

`in-add.arpa` 条目的格式是你的 IP 地址的前三个字节，并通过 `in-add.arpa` 进行反转。假设 `example.org` 的网络地址为 `192.168.1`，则 `in-add.arpa` 域名将是 `1.168.192.in-addr.arpa`。因此，`named.conf` 文件下对应的区域状态如下：
