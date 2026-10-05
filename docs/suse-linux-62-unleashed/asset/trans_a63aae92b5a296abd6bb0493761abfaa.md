

# 域名服务
第 8 章 251 页

domain.cxm. IN TXT "联系人: Heidi S."
IN TXT "系统管理员/主控"
IN TXT "语音: (800) 555-1212"

由于 TXT 记录是免费的，因此你并不强制要求在其中放置联系信息。因此，创建了 RP 记录，它明确指出该人员是负责指定主机的个人。例如：

domain.cxm. IN RP heidis.domain.cxm.

第一列列出了设置负责方的域名。第二列 `IN` 定义了该记录使用 Internet 类别。`RP` 将其指定为负责方记录。第四列指定了实际负责人员的电子邮件地址。注意，该地址中的 `@` 符号已被替换为点号，就像在 SOA 记录中一样。最后一列指定了一个提供额外信息的 TXT 记录。在本例中，它指向 `domain.cxm.` 的 TXT 记录。

# PTR: 指针记录

指针记录，也称为反向解析记录，告诉 `named` 将 IP 地址转换为主机名。PTR 记录有点奇特，它们不应该与你的 A 记录位于同一个 SOA 中。相反，它们出现在 `in-addr.arpa` 子域名的 SOA 中。

PTR 记录格式如下：

```
2.42.168.192. IN PTR mtx.domain.cxm.
```

注意，待反向解析的 IP 地址是反序的，并以点号结尾。

# 配置 DNS 服务器主区域

如前文所述，DNS 有三种类型：

- 主服务器（也称为主/primary）
- 从服务器（也称为从备/secondary）
- 仅缓存

我们在在本章节早期讨论了如何创建一个仅缓存的服务器。仅缓存服务器无法回答查询，只能将这些查询传递给对问题域具有权威性的主区域或从区域的服务器。然而，所有的 DNS 服务器都应该配置为执行缓存功能。

![](img/cbac72550c7126a22162e94d91a0c360_286_0.png)

# 网络与互联网服务

让我们关注添加 DNS 服务器主区域。DNS 服务器主区域可以回答关于其域的查询，无需查询其他服务器，因为其数据存储在本地硬盘上。DNS 服务器主区域被认为拥有该域内所有主机最新的记录。

## 本地域名解析

在本章早期，你在 `domain.cxm` 域中地址为 `192.168.42.1` 的假设主机 `numark` 上创建了仅缓存的 DNS。假设同一子网的主机 `mtx` 地址为 `192.168.42.2`。使用主区域添加本地域名解析是一项易任务。以下是基本步骤：

1. 在 `named.conf` 中添加主区域 "domain.cxm"，指向名为 `named.domain.cxm` 的区域数据文件。
2. 创建区域数据文件 `named.domain.cxm`，解析两个主机——`sendmail` 和 `www`。
3. 在之前创建的 `named.192.168.42.4` 中添加从 `192.168.42.2` 到 `mtx` 的解析。
4. 重启 `named`。
5. 测试并排除故障。

## 在 named.conf 中添加区域 "domain.cxm"

将以下代码添加到 `/etc/named.conf`：

```
zone "domain.cxm" {
    # 为此域内所有主机的 DNS
    type master;                #文件在此主机上
    file "named.domain.cxm";    # 该域的 dns 名称文件
};
```

这表示将 `domain.cxm` 域中的任何名称或 FQDN 指向数据 `named.domain.cxm`，由于 `type master;` 语句，它是输入到 DNS 服务器的，而不是输出，也不是中间文件。注意井号 (#) 右侧的文本是注释。接下来，创建文件 `named.domain.cxm`。

## 创建区域数据文件 named.domain.cxm

创建以下 `/var/named/named.domain.cxm`：

```
@    IN SOA numark.domain.cxm. hostmaster.domain.cxm. (
                   199702703 ; Serial
                   28800      ; Refresh
                   14400      ; Retry
                   360000    ; Expire
                   86400      ; Minimum)
```

# 域名服务
第 8 章

| IN | NS | numark |
| IN | MX | 10 | numark |
| IN | A | 192.168.42.1 |
| mtx | A | 192.168.42.2 |

`numark mtx www` 名称服务器 `numark.domain.cxm` 对 `@` 具有权威，`@` 是 `named.conf` 中的区域。括号之间的信息包含在本章解释的细节。`@` 的单个名称服务器 (NS) 设置为 `domain.cxm.`。`(domain.cxm)` 位于 `numark`。`numark` 处理 `domain.cxm` 的 (MX)。`numark` 和 `mtx` 分别对应地址 `192.168.42.1` 和 `192.168.42.2`。别名指向 `numark`，根据上一行，它被设置为 `192.168.42.1`。

`IN NS` 和 `IN MX` 语句在列中没有标识符。注意[content] 文本右侧的井号 (#) 是注释。接下来，创建文件 `named.domain.cxm`。

