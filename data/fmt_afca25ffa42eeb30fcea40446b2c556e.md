
## echo wait

## echo dgram

```

位于 `/etc/inetd` 中的以下行：

遗憾的是，没有探测端口的防御措施。在给定的状态下，ICMP 导致了网络问题。

## DNS 问题 (DNS ISSUES)

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、查看网页或下载文件时，名称服务器都会主机名转换为 IP 地址——在只有少数主机时，人们会在 `/etc/hosts` 文件中添加新行。现在，DNS 服务器的首选是 `BIND`，它由 Internet Software Consortium 维护。`BIND` 有几个版本：

| 版本 | 说明 |
| :--- | :--- |
| `BIND 4.x` | 被许多人称为One `BIND`，该版本在 `ISC` 接管 `BIND` 之前。代码虽然很难看，但经过了 `8.x` 分支的审查。`8.x` 的安全策略也包含其中，但不再开发 `4.x` 分支。 |
| `BIND 8.x` | 由于 `4.x` 的成功，`8.x` 包含了更多配置选项、访问列表、DNS 更新/通知（加速区域传输）、DNS 安全、IPv6 支持、以非 `root` 用户运行并 `chroot`，以及性能改进。`BIND 8.x` 代码被认为过于复杂，无法被某些团队（例如 `OpenBSD` 团队）成功审计，被认为不适用。 |
| `BIND 9.x` | 该分支是对 `BIND 8.x` 架构的重写，使其更具可维护性和扩展性。（然而，这似乎并没有让代码更易读。）`BIND 9.x` 包含了 `8.x` 的所有功能，并增加了一些新功能：视图（向不同客户端显示命名空间部分的方法）、协议增强、后端数据库支持以及更好的处理器支持。 |

如果你希望处于最前沿，`BIND 9.x` 是你的选择。如果你希望不被割，那么 `4.x` 是稳定的选择。`BIND 9.x` 是一个不错的折中方案，也是大多数网站目前使用的。

## DNS 查询示例

这里我们使用 `nslookup` 实用对对 `www.example.net` 进行了简单查询。它既显示了 `www.example.net` 的结果 IP 地址，也显示了我们的本地名称服务器（在此情况下为 `localhost`）：

```
machine$ nslookup www.example.net

Server: localhost

Address: 127.0.0.1
```

```
Name: www.example.net

Address: 172.26.105.20
```

同样可以使用 `host` 命令完成同样的操作，这实际上是我们推荐的工具：

```
machine$ host www.example.net

www.example.net has address 172.26.105.20

www.example.net mail is handled (pri=10) mailhost.example.net

www.example.net mail is handled (pri=20) mailbackup.example.net
```

> 除了 `nslookup` 和 `host` 之外，还有其他与 `BIND` 配合使用的有用 DNS 工具，其中大多数以不同程度的详细性和粒度提供相同的信息。例如，`dig` 就是一个非常强大的工具。

## DNS 查询安全问题

如果你有一个最新版本的 `BIND` 且它没有任何已知攻击的漏洞，你的 DNS 服务器仍可能被用来攻击你。你的名称服务器配置、命名规范和特定的 DNS 条目可能会提供比你可能怀疑的黑客更多的信息。我们将介绍黑客采用的几种常用 DNS 信息收集方法。

### 信息字段

| 流行度 | 6 |
|---|---|
| 简单性 | 7 |
| 隐隐性 | 6 |
| 风险评分 | 6 |

DNS 规范中提供了许多不同类型的记录，其中大多数与主机到 IP 或 IP 到主机的查询无关。这些其他字段在被使用时，倾向于向黑客“泄露”信息。以下是某些可用（并非全部）的 DNS 记录类型列表：

### 第 8 章：映射你的机器和网络

| 记录类型 | 名称 | 描述 |
|---|---|---|
| `SOA` | 区域（起始）起始权限 | 包含 DNS 管理员的电子邮件地址以及几个决定更新、缓存和传输时间的数字 |
| `A` | 地址记录 | 属于主机名称的 IP 地址 |
| `CNAME` | 规范名称 | 对给定机器名称的主机名的引用，而不是 IP 地址，非常类似于符号链接 |
| `PTR` | 指针记录 | 给定 IP 地址的主机名 |
| `HINFO` | 主机信息 | 主机的架构和操作系统 |
| `TXT` | 描述性文本 | 关于机器的其他描述性文本，通常是其用途和/或位置 |
| `RP` | 负责人 | 负责该机器的人员的电子邮件地址 |

当 `host` 命令没有给出特定的查询类型时，它会执行 `A`、`CNAME` 和 `MX` 记录的查询，这就是为什么你在上一个示例中看到的不仅仅是地址记录。

你可以使用 `host` 命令的 `-t` 选项来查询特定字段。

```
machine2 host -t txt example.com

www.example.com descriptive text "Located in Building 1, Chicago"
```

此外，你可以使用星号 `*` 或 `"any"` 作为 `-t` 标志的目标来运行所有后续查询：

```
machine5 host -t * www.example.com

www.example.com responsible personbrandt@example.com info.example.com

www.example.com host information UltraSparc 5 Linux 2.0

www.example.com descriptive text "Located in Building 1, Chicago"

www.example.net has address 172.26.105.20

www.example.net mail is handled (pri=10) by mailhost.example.net

www.example.net mail is handled (pri=20) by mailbackup.example.net
```

### 揭露 Linux 攻击：Linux 安全秘密与秘密

如你所见，许多字段对黑客可能很有帮助，因为它们提供了对于主机到 IP 查询目的并非必要的信息。在这种情况下，黑客获知了机器所在的位置、运行的是哪个版本的 `Linux`、底层硬件，甚至是管理员，从而使其能够针对性地定制他的攻击。

### 信息性 DNS 字段应对措施

如果你手动维护 DNS 记录，请务必不要在任何公开的 DNS 记录中包含敏感信息。`HINFO` 和 `TXT` 记录显然是不必要的。`RP` 记录可能有用——它们是人员寻找联系人的快速方式，当管理员想要报告来自其机器的可疑活动时，这种联系可能至关重要。然而，请谨慎使用。至少，这些记录可能被用于发送垃圾邮件。

大多数创建 `HINFO` 和 `TXT` 记录的情况发生在从机器数据库导出数据以创建 DNS 记录时。在数据库中拥有这些数据非常有帮助，但并不鼓励通过 DNS 向所有人公开这些信息。

### 区域传输

| 流行度 | 7 |
|---|---|
| 简单性 | 8 |
| 影响 | 7 |
| 风险评分 | 7 |

`BIND` 的功能之一是允许互联网上的几台机器为你的 DNS 记录提供服务。这是好事，因为如果你的唯一 DNS 机器发生故障，它可以防止你出现单点故障。你的每个域都有一个主机器，其余所有的从用 DNS 在每当发生更改时都会传输整个 DNS 区域的内容。变成从用 DNS 机器（也称为 DNS 从用服务器）的方法是在你的 `named.conf`（或如果运行 `BIND` 时）中添加如下部分：

```
zone "example.com" {
    type slave;
    masters { 192.168.1.1 };
}
```

问题是，黑客可以获取区域传输，除非你阻止它。以下是使用 `BIND` 限制这种区域传输的示例：

```
zone "example.com" {
    type master;
    masters { 192.168.1.1 };
    allow-transfer { 192.168.1.2 };
}
```
