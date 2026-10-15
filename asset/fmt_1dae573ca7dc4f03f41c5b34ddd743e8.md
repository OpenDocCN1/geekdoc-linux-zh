
![](img/10371fe30b7fdac23ef2ef30d5ffe738_404_0.png)

图 15.4：IP Tables 过程

遍历该过程，我们看到数据包进入系统并通过校验和检查以确定其是否损坏。如果损坏，则被拒绝；否则被传递到合理性检查，该检查查看数据包是否正确格式化。如果未通过，则被拒绝。如果数据包通过此测试，它将被评估为本地数据包或外部数据包。本地数据包被发送到`INPUT`链，该链根据`INPUT`链规则集对其进行评估，将其丢弃、拒绝或通过该过程发送到`OUTPUT`链。外部数据包，即 destined for external hosts（目的为外部主机）的数据包，被发送到`FORWARD`链。一旦发送到`FORWARD`链，数据包将根据该链的规则集进行检查，然后被丢弃、拒绝或发送到`OUTPUT`链。与上文讨论的 IP Chains 方法相比，Netfilter 方法相当流畅。为了使用 IP Tables，你需要构建带有 Netfilter 支持的内核（必须是内核 2.3.15 或更高版本）或将其作为模块包含在内。

### 规则和规则集

IP Tables 的规则与 IP Chains 的规则看起来略有不同。首先让我们看看语法：Netfilter 规则可以使用`-s`选项指定数据包源，使用`-p`选项指定协议，使用`-d`选项指定目的地，使用`-j`（jump/跳转）选项指定规则匹配时数据包要发送到的链，以及端口。现在有三种类型的规则：那些影响整个表的，那些影响整个链的，以及那些影响链内规则的。使用`-t`来指定表名。默认表是`filter`表，但你将使用`nat`表来影响伪装。

`nat`表有两个链：`PREROUTING`用于传入接口，`POSTROUTING`用于传出接口。

此选项影响整个表：

| 选项 | 描述 |
| :--- | :--- |
| `-t` | 指定要操作的具体表名称。 |

这些选项影响整个链：

| 选项 | 描述 |
| :--- | :--- |
| `-N` | 创建新链。 |
| `-X` | 删除空链。 |
| `-E` | 重命名链。 |
| `-P` | 更改内置链的策略。 |
| `-L` | 列出链中的规则。 |
| `-F` | 刷新链中的规则。 |
| `-Z` | 将链内所有规则的分组包数和字节计数器清零。 |

这些选项影响链内的规则：

| 选项 | 描述 |
| :--- | :--- |
| `-A` | 将新规则附加到链末尾。 |
| `-I` | 在链内的某个位置插入新规则。 |
| `-R` | 替换链内某个位置处的规则。 |
| `-D` | 如果传递数值，则删除链内某个位置处的规则；如果传递要匹配的规则，则删除第一个匹配的规则。 |

现在让我们看看上述使用的 IP Chains 示例规则，改写为 IP Tables 语法。

此规则丢弃来自 192.168.0.11 的所有数据包：

```
iptables -A INPUT -s 192.168.0.11 -j DROP
```

此规则丢弃所有不是来自 192.168.0.11 的数据包：

```
iptables -A INPUT -s ! 192.168.0.11 -j DROP
```

这显示了输入链的所有规则列表：

```
iptables -L INPUT
```

要列出`nat`表中的规则，请添加`-t`标志而不是链名称。

```
iptables -L -t nat
```

以下两个规则都删除输入链中的第七条规则，第一个通过匹配规则编号，第二个通过匹配规则本身：

```
iptables -D INPUT 7
iptables -D INPUT -s 192.168.1.11 -j DROP
```

最后，此规则刷新输入链：

```
iptables -F INPUT
```

要仅刷新`nat`表的规则：

```
iptables -F -t nat
```

现在，我们可能希望拒绝外部世界的 FTP 访问，但允许内部网络上的 FTP 访问。假设我们有两个网卡，`eth0`和`eth1`，其中`eth0`是连接 Internet 的那个，我们通过向输入链添加一条规则来实现这一点，该规则拒绝通过`eth0`进来的 FTP 请求，但接受通过`eth1`进来的请求。为此，我们必须运行两个单独的`iptables`命令：

```
iptables -A INPUT -p tcp -i eth0 --source-port ftp -j REJECT
iptables -A INPUT -p tcp -i eth1 --source-port ftp -j ACCEPT
```

一旦你的 Netfilter 文件被正确设置，你需要让它在每次启动时运行。Red Hat 为此提供了`iptables-save`和`iptables-restore`二进制文件。运行`iptables-save`并将其输出重定向到`/etc/iptables.conf`，以将你的规则保存到`iptables.conf`文件中：

```
iptables-save > /etc/iptables.conf
```

要从`/etc/iptables.conf`恢复，运行`iptables-restore`并从`/etc/iptables.conf`重定向：

```
iptables-restore < /etc/iptables.conf
```

接下来，将`ipchains-restore`命令添加到`/etc/rc.d/rc.local`，以便在启动时自动运行。你同样可以将我们存储在`/etc/iptables.conf`中的 Netfilter 命令添加到`/etc/rc.d/rc.local`，但如果你期望对配置进行大量更改，第一种方法更灵活。更好的做法是将 IP Tables 脚本添加到`/etc/init.d`或你的发行版放置启动脚本的任何位置。Red Hat 7.3 默认通过 Listing 15.8 中显示的脚本这样做：

**Listing 15.8：一个示例 Netfilter 启动文件**
