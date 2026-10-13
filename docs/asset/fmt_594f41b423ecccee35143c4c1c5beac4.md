
每个区域必须恰好有一个 SOA 记录。以下是名为 `ad-engine.com` 的域的示例 SOA 记录：

```
@  IN  SOA  ns.ad-engine.com.  kabir.ad-engine.com.
(
                20010201000   ; Serial
                7200          ; Refresh - 2 hours
                3600          ; Retry  - 1 hour
                43200         ; Expire - 12 hours
                3600 )        ; Minimum - 1 hour
```

以下是前述示例的说明：

- `ad-engine.com` 的名称服务器主机名为 `ns.ad-engine.com`，联系电子邮件地址为 `kabir@ad-engine.com`。注意，SOA 记录中电子邮件地址的 `@` 部分被替换为句点。
- 第一个数字是序列号字段。它指定此区域文件的版本号。在此示例中，序列号告诉我们记录最后更新于 2001 年 2 月 1 日。
- 刷新率设置为 7,200 秒（两小时）。因此，`ad-engine.com` 的辅助名称服务器将轮询主服务器以查看区域的序列号是否增加。常用的值范围为 2 到 12 小时，具体取决于你更改区域配置的频率。
- 重试率设置为 3,600 秒（一小时）。这意味着如果网络故障导致辅助名称服务器在刷新周期结束时（本例中为每两小时）无法联系主服务器，辅助服务器应在重试与主服务器通信前再等待一小时。
- 过期率设置为 43,200 秒（12 小时）。如果无法联系主服务器，这允许辅助服务器将其区域数据的副本视为有效 12 小时。如果你在不同网络上设置了辅助 DNS，此值尤其重要。你应将其设置得足够高，以便在主名称服务器或其网络出现故障时，辅助服务器能够在最长的停机期间提供 DNS 服务。在此示例中，辅助名称服务器将在未能与主服务器通信后提供 12 小时的 DNS 服务，并在指定时间后停止该区域的 DNS 服务。但是，它仍会定期尝试与主名称服务器通信。
- 最小经过时间是资源记录的默认 TTL 值。这指定资源记录在名称服务器缓存中保持有效的时间。例如，当名称服务器查询 `ad-engine.com` 名称服务器以获取某个 DNS 记录时，它会将查询的答案保留在缓存中 3,600 秒（1 小时）。如果你经常更改 DNS 信息，应将此值设为较低数字；否则，设为较高数字。

## NS：Name Server

名称服务器记录用于指定负责域的名称服务器。语法如下：

```
IN NS name_server_hostname.
```

请注意，资源记录的名称和 TTL 字段未指定，因为名称仅需在 SOA 记录中使用 `@` 字符指定，TTL 值也使用 SOA 记录中的最小数字指定。例如：

```
IN NS ns.ad-engine.com.
```

此资源记录指定 `ns.ad-engine.com` 是当前区域文件的名称服务器。你可以指定多个 NS 记录。事实上，你应该至少有两个 NS 记录（一个用于主服务器，一个用于从服务器）。还请注意名称服务器主机名末尾的句点。你必须在区域文件中的所有完整主机名后插入句点。

## A：Address

地址记录为特定主机名指定 IP 地址。A 记录（Address record 的缩写）将主机名转换为 IP 地址。语法如下：

```
hostname IN A IP-address
```

例如：

```
www.ad-engine.com. IN A 206.171.50.51
```

每个主机应至少有一个 A 记录。你也可以使用主机名的简写。例如，

```
www IN A 206.171.50.51
```

如果区域是 `ad-engine.com`，则与之前的 A 记录相同。换句话说，如果你未指定完整主机名，则域名会附加到短名称。因此 `www` 变为 `www.ad-engine.com`。

## PTR：Domain Name Pointer

域名指针记录用于将 IP 地址转换为主机名。这也称为反向域名服务。PTR 记录的语法如下：

```
IP-address IN PTR hostname.
```

例如：

```
206.171.50.51 IN PTR www.ad-engine.com.
```

这里 IP 地址 `206.171.50.51` 与主机 `www.ad-engine.com` 相关联。你也可以使用缩写版本如下：

```
51 IN PTR www
```

通常，ISP 会为网络执行主要的反向 DNS。

## CNAME：Canonical Name

规范名称记录 CNAME 为规范（官方）主机名指定别名（主机名）。语法如下：

```
alias IN CNAME canonical_hostname.
```

例如：

```
webserver.ad-engine.com. IN CNAME www.ad-engine.com.
```

这里，`webserver.ad-engine.com` 是 `www.ad-engine.com` 的别名。缩写版本如下：

```
webserver IN CNAME www
```

请注意，当需要将 `webserver.ad-engine.com` 解析为 IP 地址时，将返回 `www.ad-engine.com` 的 IP 地址。因此，你必须确保规范主机名至少存在一个 A 记录。

## MX：Mail Exchange

邮件交换记录用于指定设置为域的 SMTP 邮件服务器的主机名。语法如下：

```
IN MX preference_value mail_server_hostname.
```

例如：

```
IN MX 0 mail.ad-engine.com.
```

优先级数字只有在你拥有多个邮件服务器时才有用。例如：

```
IN MX 10 fast-mail-server.ad-engine.com.
```

```
IN MX 20 slow-mail-server.ad-engine.com.
```

这里，优先级数字越低表示优先级越高。现在你已经学习了 DNS 资源记录的基础知识，可以准备创建主、辅和仅缓存的 DNS 服务器了。

## 使用 bindconf 配置 DNS 服务器

通常不建议在服务器上安装 X Window 系统，因为管理服务器并不需要这样的图形用户界面，而且 X 会使系统更容易受到黑客攻击，因为许多 X 程序不断被发现存在漏洞。然而，如果你必须在 DNS 服务器上使用 X Window 系统，你也可以利用 Bind 配置工具（`bindconf`）来配置 DNS 服务器（BIND）。如果你没有在服务器上安装 X，这也是我的建议，那么你可以跳到下一节。

![](img/9eb7e89292d2f85707b4d49102c865b7_475_0.png)

> 如果你决定使用 `bindconf`，你绝不能手动修改 `/etc/named.conf` 文件，因为 `bindconf` 每次使用时都会重新创建该文件。也就是说，如果你手动修改此文件，你的更改将在下次使用 `bindconf` 时丢失！

当你从 `xterm` 窗口运行 `bindconf` 时，会出现类似图 15-1 的窗口。

默认情况下，`bindconf` 会创建一个名为 `localhost` 的主区域，并具有适当的反向 DNS 配置。这在主菜单窗口中显示。此配置仅用于回环地址。

![](img/9eb7e89292d2f85707b4d49102c865b7_476_0.png)

图 15-1 `bindconf` 主屏幕。

### 为域名创建正向主 DNS 区域

假设你想为名为 `evoknow.com` 的新域名创建一个正向主区域。请执行以下操作：

1. 在主 `bindconf` 窗口中单击 Add 按钮，你将看到如图 15-2 所示的屏幕。选择 Forward Master Zone 选项并在名称输入区域输入适当的域名，然后单击 OK 继续。

![](img/9eb7e89292d2f85707b4d49102c865b7_476_1.png)

图 15-2 选择区域类型。

2. 你将看到如图 15-3 所示的屏幕。你可以将联系地址更改为比 `root@localhost` 更合适的地址。

![](img/9eb7e89292d2f85707b4d49102c865b7_477_0.png)

图 15-3 名称到 IP 翻译窗口。

如果你想设置区域生命周期信息，请单击 Time Settings 按钮，这将打开如图 15-4 所示的屏幕。将刷新率、重试率、过期率、最小时间等设置为所需的任何设置。在大多数情况下，默认值是可以的。

![](img/9eb7e89292d2f85707b4d49102c865b7_477_1.png)

图 15-4 区域生命周期信息窗口。
