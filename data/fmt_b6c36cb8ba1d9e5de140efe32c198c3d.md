
## home.com DNS named.conf file

```conf
options {
   directory "/var/named";
   allow-transfer {
     216.155.202.163;
     216.155.202.100;
   };
};
```

> 指定 `allow-transfer` 选项意味着仅允许列出的两个节点查询此服务器

> `directory` 选项指定 DNS 服务器将使用哪个 UNIX 目录查找额外的配置文件和区域信息

### 436 UNIX 系统管理：初学者指南

```conf
//
// 我们的主 DNS 信息
//
zone "home.com" {
  type master;
  file "home.com";
};
zone "202.155.216.in-addr.arpa" {
  type master;
  file "reverse-home.com";
};
```

此列表表示了放置在 `named.conf` 文件中的最小 DNS 配置。默认情况下，DNS 服务器将在 `/etc` 目录中查找此文件，但可以使用 `-c` 命令行参数进行更改。此 DNS 配置的基本语法包括：

```
statement_keyword "string" {
  option keyword;
  option Keyword;
};
```

语句包含了定义 DNS 服务和控制服务器运行方面的层级指令。表 14-2 列出了支持的关键字。
基础的 `named.conf` 文件（如前所示）包含了几个部分，这些包含配置选项、基本初始化和单独的区域配置。

### 语句关键字含义

| 关键字 | 含义 |
|---|---|
| `acl` | 提供一种访问控制机制以形成 IP 地址匹配列表 |
| `include` | 包含另一个文件 |
| `logging` | 控制服务器日志 |
| `options` | 特定的和控制全局服务器配置选项 |
| `controls` | 决定如何与 `rndc` 工具通信 |
| `server` | 为特定对象定义新服务器 |
| `zone` | 定义一个 DNS 区域。可以包含 `master` 或 `secondary` 关键字 |

表 14-2 DNS 服务器语句关键字

第 14 节：使用域系统 437

`options` 部分包含了 DNS 服务器的运行方面。例如，`directory`（第 4–9 行）选项指定 DNS 服务器将使用哪个 UNIX 目录查找额外的配置文件和区域信息。DNS 服务器支持的一些常用配置关键字列在表 14-3 和 14-4 中。DNS 选项分为两组：控制服务器与其它系统交互的选项（表 14-3），以及配置选项（表 14-4），后者控制服务器在本地系统上的运行方式。

配置包含了对两个区域的支持：`home.com` 和关联的反向 IP 域。`home.com` 域定义在第 15–18 行；反向域 `202.155.216.in-addr.arpa` 包含在第 19–22 行。定义一个新域非常简单；这就是要求的。

### 含义

| 选项关键字 | 含义 |
|---|---|
| `allow-query` | IP 地址：确定哪些 IP 地址允许查询服务器。默认是允许所有。 |
| `allow-transfer` | IP 地址：确定哪些 IP 地址允许从 DNS 服务器进行区域传输。默认情况下，任何节点都可以进行区域传输。 |
| `auth` | yes: 默认值为 yes；这告诉服务器对具有 SOA 记录的域的查询提供权威回答。 |
| `auth-mx` | yes/no: 告诉服务器验证名的完整性。 |
| `check-names` | type action fake-query yes/no: 默认值为 no；服务器将模拟对 IQERY 类型的支持。 |
| `fetch-glue` | yes/no: 默认值为 yes；这告诉服务器查询并缓存关于其非权威的域的必要 DNS 记录。 |
| `forward` | first yes/no: 默认值为 first；这导致服务器在客户端查询无法解析时将其转发到另一个 DNS 服务器。 |
| `forwards` | ip list: 为 DNS 服务器提供在没有客户端请求信息时进行查询的 IP 地址列表。 |
| `multiple-cnames` | yes/no: 默认值为 no；允许服务器支持 CNAMES 并指向其他 CNAMES。 |
| `notify` | yes/no: 默认值为 yes；这告诉服务器当服务器上的区域已更新时，向所有从服务器发出通知。 |
| `recursion` | yes/no: 默认值为 yes；指示服务器查询其他 DNS 服务器以解析客户端查询。 |

表 14-3 服务器交互选项

438 UNIX 系统管理：初学者指南

| 选项 | 含义 |
|---|---|
| `directory` | 指定服务器的工作目录。 |
| `name-xfer` | 指定区域传输的路径。 |
| `dump-file` | 指定服务器写入统计信息的路径。 |
| `memstats-file` | 指定设置了 dump 选项时的文件名。 |

表 14-4 服务器运行选项

第 14 节：使用域系统

接下来定义反向映射，并称为 `202.155.216.in-addr.arpa`。该区域的细节包含在 `reverse-home.com` 中。反向映射用于将 IP 地址转换为主机名。安全措施可以使用 `allow-transfer` 关键字（第 6–9 行）来控制哪些其他系统可以“对话” DNS 服务器以获取多个域的完整信息。在这里，两个节点（`216.155.202.163` 和 `216.155.202.100`）允许查询 DNS 服务器。

> 提示

```
allow-transfer 不是用于 DNS 解析器（客户端）查询，而是用于可能询问 DNS 服务器的其他系统。在本节的后续部分，你将学习使用调试工具从 DNS 服务器查询各种有用的重要信息。
```
