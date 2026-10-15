
```
+++ Statistics ++ Wed Feb 2 07:18
180465 time since boot (secs)
52669 time since reset (secs)
0 Unknown query types
475460 A queries
194 NS queries
156816 CNAME queries
76244 MX queries
130939 TXT queries
424587 AXFR queries

++ Server Statistics ++

| RR | RNDX | RFWDr | RDup | RFail | RErr | RAXFR |
| --- | --- | --- | --- | --- | --- | --- |
| 32052 | 23620 | 24986 | 1013 | 3532 | 0 | 903 |
| 10339 | ROpts | SSyq | SAns | SFWqd | SDUp | RIq |
| 0 | 5547 | 65293 | 26736 | 29148 | 0 | 96390 | 0 |
| DUp | RTCP | SFWdr | SFail | SErr | SNAAns | SNXD |
| 47876 | 1005 | 24826 | 18 | 16253 | 19064 |
```

任何导致错误的查询都会被记录、在一个或多个统计数据中计数并丢弃。`Unknown query types`类别包含服务器无法识别的记录类型查询。新记录会出现在这一列中，直到服务器更新以包含这些类型。`ANY`桶并不是一种记录类型；它计算请求特定名称所有信息的查询。输出下半部分的`Dup`项表示重复查询或响应。重复通常发生在查询在收到响应之前超时；查询者会再次提交查询。

在`BIND 8`中，如果设置了`deallocate-on-exit`，`ndc`还会产生`named.memstats`。这些缩写中的首字母代表接收（`R`）或发送（`S`）；最后一个字母表示查询（`Q`）或响应（`R`）。在代码中识别这些标题的方法可以在代码中找到，即`BIND 8`分发中的`src/bin/named`。你可以在当前发行版找到它。

# 使用 nlookup, dig 和 host 进行调试

有三个工具可以查询`DNS`数据库：`nlookup`、`dig`和`host`。`nlookup`是这些工具中最老老的，并随`BIND`分发。`the domain grouper`起初由`Steve Hotz`编写，后来由`Michael Sawyer`为`BIND 9`重写。与`BIND`附带的`host`是由`Eric Wissanoff`编写的开源工具；它具有用户友好的输出和检查区域文件语法的功能。我们讨论了这些工具，但相比`nlookup`，我们更倾向于使用`dig`：我们也喜欢`host`。

`nlookup`是一个用于查询`DNS`数据库的用户级命令。它接收以点结尾的完全限定名称，如果你漏掉了点，它会附加默认域名。

# UNIX 系统管理手册

对于本地名称，这种行为通常是你所需要的。表 16.16 给出了`nslookup`命令的简短列表。

## 表 16.16 nslookup 可识别的命令

| 命令 | 功能 |
| --- | --- |
| name | 打印主机或域名的相关信息 |
| help or ? | 显示完整的命令列表 |
| exit | 退出 |
| server host | 设置默认服务器，使用当前服务器 |
| lserver host | 设置默认服务器，使用初始服务器 |
| set type=xxx | 设置要查询的记录 |
| set debug | 开启调试 |
| set d2 | 开启大量调试 |
| ls domain | 列出所有主机/地址映射 |

- a. `any`是一个很好的值，意味着“所有记录类型”。

`dig`提供了与`nslookup`相同的功能，但它具有更智能的错误处理、提供了更多信息以及更友好的界面（尤其是与旧版本的`nslookup`相比）。例如，要查询`anchor`的`MX`记录，使用：

```
% dig anchor.colorado.edu. mx
```

```
% dig @ns1.berkeley.edu vagogh.berkeley.edu any
```

```
% dig -x 128.32.5
```

从`berkeley.edu`服务器获取`vagogh`的完整记录，并对`vagogh`执行反向查询。这里有一个同时使用`nslookup`和`dig`查询相同数据的示例：

```
% nslookup
Default: bb.rc.com
Address: 204.152.187
> set type=any
> amazon.com.
Server: bb.rc.com
Address: 204.152.187
Non-authoritative answer:
amazon.com nameserver = AUTH00.NS.NET
amazon.com nameserver = NS2.PNAP.NET
amazon.com nameserver = NS1.PNAP.NET
amazon.com nameserver = NS-1.amazon.com
amazon.com preference = 10, mail exchanger = service-4.amazon.com
amazon.com preference = 10, mail exchanger = service-5.amazon.com
amazon.com address = 208.216.182.15
```

权威答案可以从找到：
`amazon.com` nameserver = `AUTH00.NS.NET`
`amazon.com` nameserver = `NS2.PNAP.NET`
`amazon.com` nameserver = `NS1.PNAP.NET`
`amazon.com` nameserver = `NS-1.amazon.com`
`AUTH00.NS.NET` address = 198.6.1.65
`NS2.PNAP.NET` address = 206.253.194.97
`NS1.PNAP.NET` address = 206.253.194.65
`NS-1.amazon.com` address = 209.191.164.50
`service-4.amazon.com` address = 209.191.164.50
`service-5.amazon.com` address = 209.191.164.51

`nslookup`返回四个`NS`记录、两个`MX`记录和一条`A`记录。它还提供了`DNS`服务器和`MX`主机的`IP`地址。
