
# /etc/init.d/named stop (Red Hat 使用 service stop)

# /etc/init.d/named start (Red Hat 使用 service start)

`- Dropping source packet from ...`（丢弃来自...的源包）。新版本的 BIND 允许你设置查询端口，系统管理员使用此功能为防火墙添加规则，通过源端口识别 DNS 数据包。然而，TCP/UDP 端口号无效。该错误消息与你的某个主机有关，你应该更改 `named.conf` 中的 `query-source` 指令来修复此错误。
- `Denied update from ...`（来自...的更新拒绝）。尝试对区域进行动态更新，但因为该区域在 `named.conf` 中的 `allow-update` 或 `update-policy` 子句被拒绝。

## 日志配置示例

以下来自繁忙名称服务器的 `named.conf` 文件片段展示了一个日志管理方案：

```
logging {

  channel default_log {

    file "/log/named.log" versions 3 size 10m;

    print-time yes;

    print-category yes;

    severity info;

  }
  category { default_log };
  channel xfer_log {

    file "/log/xfer.log" versions 3 size 10m;

    print-category yes;

    print-severity yes;

    print-time yes;

  }

}
```

在繁忙的服务器上，上方的消息可能意味着正在加载：

```
channel db-log {

  file "db.log" versions 3;

  severity 1;

  print-time yes;

}
category database { db-log };
category dnssec { xfer-log };
category xfer-in { xfer-log };
category xfer-out { xfer-log };
category notify { xfer-log };
```

## 调试级别

调试级别由 0 到 100 的整数表示。数字越大，输出越详细。0 关闭调试。

你可以通过运行 `rndc trace` 将调试级别增加 1，或者通过运行 `rndc level` 将调试级别设置为指定值。`rndc not` 完全关闭调试。你可以通过定义指定级别来开启调试，例如：

```
severity 3;
```
这将发送到特定的通道。通道定义中的其他行指定了调试信息的目的地。级别越高，记录的信息越多。

查看日志或调试输出展示了 DNS 数据在现实世界中是如何处理的。名称末尾那个讨厌的点（或缺失）导致了大量的 DNS 流量。理论上，完全限定域名末尾需要点。

## 使用 rndc 进行调试

下一页的表 15.15 显示了 `rndc` 接受的一些选项。输入 `rndc` 而不带参数将显示可用命令列表。产生文件的命令将其放在 `named.conf` 指定的目录中。

### 表 15.15 rndc 命令

| 命令 | 功能 |
| --- | --- |
| dump | 将 DNS 数据库导出到 `named_dump.db` |
| flush [view] | 刷新所有缓存或指定视图 |
| hostname [view] | 从服务器缓存中刷新指定的主机 |
| freeze zone [class] | 暂停动态区域的更新 |
| thaw zone [class] | 恢复动态区域的更新 |
| halt | 在不写入等待更新的情况下停止 `named` |
| querylog | 切换传入查询的 |
| notrace | 关闭调试 |
| reconfig | 重新加载配置文件并加载新区域 |
| refresh zone [class] | 为区域调度维护 |
| reload | 重新加载 `named.conf` 和区域文件 |
| reload zone [class] | 重新加载指定的区域或视图 |
| restart | 重启服务器 |
| retransfer zone [class] | 从主服务器复制数据 |
| stats | 将统计信息写入 `named.stats` |
| status | 显示 `named` 的当前状态 |
| stop | 保存更新并停止 `named` |
| trace | 将调试级别增加 1 |
| level | 将调试级别设置为指定值 |

a. 这里的 `class` 参数与资源记录相同，互联网通常为 `IN`。
b. 尚未在 BIND (9.3.0) 中实现，但已承诺

# 测试与调试

可以使用如下命令：

```
$ sudo rndc -1 /var/named/var/run/rndc
```

在 BIND 9 中，确保 `named` 的版本与 `rndc` 的版本匹配非常重要，否则你将收到关于协议版本不匹配的错误信息。升级时请同时安装两者。

# BIND 统计信息

`named` 维护了一些摘要信息，在收到来自 `rndc` 的信号后，这些信息可以导出到其工作目录下名为 `named.stats` 的文件中：

```
$ sudo rndc stats
```

以下是 `isc.org` 上一个繁忙服务器的输出示例：

```
+++ Statistics Dump +++ (1088897026)

success 98197007

referral 981464459

xferrer 9958824

xdomain 199644113

recursion 0

failure 322556

--- Statistics Dump --- (1088897026)
```

统计数据显示了查询的成功与失败情况，并对各种错误进行了分类。该服务器成功回答了 1990 万次查询，提供了 98 亿重定向（referral），回答了约 2 亿次“不存在的域名”（nxdomain），回答了约 100 万次“不存在的资源集”（nxerrset），无法回答 32 万次。

如果这 2 亿次 nxdomain 错误（占总 10 亿次查询的 20%）的主要来源是用户输入和拼写错误，那么数量就太大了。在这种情况下，大多数错误来自 Windows 配置以及 Microsoft resolver25 中的一个 bug，该 bug 发出的许多地址记录查询，其数据字段被设置为 IP 地址而非 DNS 规范要求的主机名。这些诡异的查询其顶级域名似乎是类似 56（或 IP 地址字符串的最后一个字节），因此它们会让本地 DNS 服务器向根服务器查询这个不存在的域名，最终导致 nxdomain 错误。

失败计数（failure）统计的是既不是 nxdomain 也不是 nxerrset 的故障。

# 使用 dig 进行调试

在 shell 中可以使用三种工具来查询 DNS 数据库：`nslookup`、`dig` 和 `host`。它们都随 BIND 分发。`nslookup` 是这些工具中最旧的，一直是 BIND 分发的一部分；`dig` 是真正的域名信息工具，最初由 Steve Hot 编写；后由 Michael Sawyer 为 BIND 9 重写过，现在也随 BIND 9 发发。由 Eric Wassenaar 开发的 `host` 是另一个开源工具；它的特点是输出友好且具有检查区域文件语法的功能。

我们推荐使用 `dig` 而不是 `nslookup`，`host` 也可以。我们在这里详细讨论 `dig`。由于这些工具使用的库不同，你有时会从中得到不同的结果：`dig` 和 `host` 使用 BIND 的解析器，而 `nslookup` 有它自己的解析器。

默认情况下，`dig` 使用本地名称服务器并返回地址信息。`@nameserver` 参数使其查询特定的名称服务器。查询特定服务器的能力让你检查所做的任何更改是否已传播到辅助服务器和外部世界。如果你使用它并需要验证配置是否正确，这会特别有用。

如果你指定了记录类型，`dig` 将仅查询该类型。另一个实用的标志是 `-x`，它可以为你反转 IP 地址的字节并执行反向查询。`+trace` 标志会显示从根服务器开始的解析过程的迭代步骤。

以下是 `dig` 的输出样式：

```
$ dig yahoo.com

;; DIG 9.3.0rc << yahoo.com

;; global options: printcmd

;; Got answer:

>>;HEADER<< opcode: QUERY, status: NOERROR, id: 16507

;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 5, ADDITIONAL: 5

;; QUESTION SECTION:

yahoo.com. IN A
```
