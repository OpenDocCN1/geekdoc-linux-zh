
在这个示例中，`mtx` 是真实名称，而 `www` 是它的别名。

## MX: 邮件交换器 (Mail Exchanger)

邮件交换器允许你指定哪个主机负责接收邮件。外部使用此记录来确定邮件发送到哪个主机。MX 记录的格式如下：

```
domain.cxm. IN MX 10 mailhub

             IN MX 20 mail2
```

数字表示优先级。数字越小，优先级越高。在本例中，`sendmail` 将首先尝试到 `mailhub`。

## RP 和 TXT: 文档条目 (Documentation Entries)

作为 TXT 提供联系信息通常很有用，不仅是注释。你可以通过使用 RP 和 TXT 记录来实现，你可以放置任何你认为的信息。例如

```
domain.com.     IN TXT "Contact: Heidi"

               IN TXT "Systems"
```

第一列域名。第二列 `IN` 定义了 Internet 类。第四列指定了负责人的电子邮件地址。最后一列提供了额外信息。

## PTR: 指针记录 (Pointer Record)

指针记录也称为反向解析，告诉如何将 IP 地址转换为主机名。PTR 记录有点奇怪，因为它们不应该与 A 记录在同一个区域。相反，它们出现在 `in-addr.arpa` 子域中。

PTR 记录看起来如下：

```
2.42.168.192. IN PTR mtx.domain.cxm.
```

注意，要反向解析的 IP 地址是反序并以点号结尾的。

# 域名
第 11 章
345

## 配置 DNS 服务器区域

如前所述，DNS 有三种：

- 主（也称为一级）
- 从（也称为二级）
- 仅缓存

我们在章节早期部分讨论了仅缓存服务器。仅缓存服务器无法回答查询，只能将这些查询传递给对问题域具有权威性的主或从服务器。然而，所有 DNS 服务器都应该配置执行缓存功能。

现在让我们转向添加 DNS 服务器主区域。DNS 区域可以在不查询其他服务器的情况下回答查询，因为数据存储在本地磁盘上。DNS 服务器主区域被认为拥有该域内所有主机最新的记录。

## 添加本地域名解析

在章节早期，你于地址为 `192.168.42.1` 的假设主机 `numark` 上创建了仅缓存 DNS。假设该子网具有位于 `192.168.42.2` 的 `mtx`。使用主区域添加域名解析是一个简单的任务。以下是基本步骤：

- 在 `named.conf` 中添加主区域 `domain.cxm`，指向区域数据文件 `named.domain.cxm`。
- 创建区域数据文件 `named.domain.cxm`，解析 `sendmail` 和 `web` 两个主机。
- 在之前创建的 `named.192.168.42` 中添加 `192.168.42.2` 到 `mtx` 的解析。
- 重启 `named`。
- 测试并排除故障。

## 将区域 "domain.cxm" 添加到 named.conf

将以下代码添加到 `/etc/named.conf`：

```
zone "domain.cxm" {      #此域内所有主机的DNS

    type master;                      #此主机上的文件

    file "named.domain.cxm";          #该域的DNS文件

};
```

这表示将 `domain.cxm` 中的任何名称或 FDN 指向 `named.domain.cxm` 中的数据。由于 `type master;` 语句，它是输入到 DNS 服务器的，而不是从其输出，也不是中间文件。请注意井号 (`#`) 右侧的文本是注释。接下来，创建名为 `named.domain.cxm` 文件。

## 创建区域数据文件 named.domain.cxm

创建以下 `/var/named/named.domain.cxm`：

```
@ IN SOA numark.domain.cxm. hostmaster.domain.cxm. (

    197022703 ; Serial (序列号)

    288000 ; Refresh (刷新)

    14400 ; Retry (重试)

    360000 ; Expire (过期)

    86400 ) ; Minimum (最小TTL)
```

```
IN NS numark

IN MX 10 numark
```

```
numark IN A 192.168.42.1

mtx IN A 192.168.42.2
```

```
WWW IN CNAME numark
```

名称服务器 `numark.domain.cxm` 通过 `named.conf` 中的区域调用对区域 `@` 具有权限，设置为 `domain.cxm`。括号之间的信息包含了本章之前解释的计时细节。`(domain.cxm)` 的单一名称服务器 (`NS`) 位于 `numark`。`numark` 处理该域的邮件 (`MX`)。`domain.cxm` 中的 `numark` 和 `mtx` 主机地址分别为 `192.168.42.1` 和 `192.168.42.2`。别名 `www` 指向 `numark`，通过之前的行，它被设置为 `192.168.42.1`。

`NS` 和 `IN` 语句在第一列没有名称标识符。带有名称标识符的 `IN` 项目将默认使用最后一个具有标识符的语句的名称标识符，在本例中是第一行。

前面的区域数据文件是为了简单起见而构建的。实际的服务器有一行 `ns IN 192.168.42.1 type` 行，以便它们可以调用所有文件中的名称服务器。这样，如果名称服务器从 `numark` 更改为 `mtx`，任何文件中唯一需要的更改就是 `ns` 行。实际应用的区域还包含至少两个 `IN NS` 行，因此如果一个名称服务器宕机，另一个可以接管工作。

# 域名服务
第 11 章

请注意语法非常重要，特别是因为区域文件语法与启动文件语法不同。所有标识符必须位于第一列。所有的点 (`.`) 都是至关重要的，因为以点结尾的命名被认为是绝对的，而不以点结尾的名称被视为相对于 `@` 符号的，而 `@` 符号将由 `named.conf` 区域引用中的域名替换。

## 将 192.168.42.2 添加到 named.192.168.42.2。

你必须能够将 `192.168.42.2` 解析回 `mtx`，因此向反向区域数据文件 `named.192.168.42` 添加以下内容：

```
2 PTR mtx.domain.cxm.
```

## 重启 named，然后测试和故障排除

使用此命令重启：

```
# /etc/rc.d/init.d restart
```

此命令可能需要几分钟才能完成。

完成后，进行测试。首先尝试 `telnet` 登录并确保在了一秒钟内得到登录提示。如果 Telnet 卡住，请检查你的反向 DNS 区域和反向 DNS 数据文件。

接下来，尝试运行以下命令：

```
ping 192.168.42.1

ping 192.168.42.2
```

从每台服务器执行每个 ping。如果任何 IP 的 ping 失败，则存在网络连通性问题，在尝试激活 DNS 之前必须解决该问题。一旦证明了连通性，执行以下操作：

```
ping numark

ping mtx

ping numark.domain.cxm.

ping mtx.domain.cxm.

ping www.domain.cxm.
```

上述每个 ping 命令都应该成功并交付正确的 IP。如果这些命令都成功，尝试以下操作：

```
nslookup numark

nslookup mtx

nslookup numark.domain.cxm.

nslookup mtx.domain.cxm.

nslookup www.domain.cxm.

nslookup 192.168.42.1

nslookup 192.168.42.2
```
