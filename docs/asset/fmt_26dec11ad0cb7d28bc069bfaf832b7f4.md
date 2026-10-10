
以下是可用的类别及其包含的日志信息类型简述。未来的 BIND 版本可能会添加更多类别。

| category | 描述 |
| :--- | :--- |
| `default` | 默认类别定义了那些未定义特定配置的类别的日志选项。 |
| `general` | 通用类别。许多事务仍未归类到特定类别中，它们都会汇到这里。 |
| `database` | 与名称服务器内部用于存储和缓存数据的数据库相关的消息。 |
| `security` | 请求的允许与拒绝。 |
| `config` | 配置文件的解析和处理。 |
| `resolver` | DNS 解析，例如缓存名称服务器代表客户端执行的递归查询。 |
| `xfer-in` | 服务器接收的区域传输（Zone transfers）。 |
| `xfer-out` | 服务器正在发送的区域传输。 |
| `notify` | `NOTIFY` 协议。 |
| `client` | 客户端请求的处理。 |
| `unmatched` | `named` 无法确定其类别或没有匹配视图（`view`）的消息。`client` 类别也会记录一条单行摘要。此类别最好发送到文件或 `stderr`，默认情况下它被发送到空通道。 |
| `network` | 网络操作。 |
| `update` | 动态更新。 |
| `queries` | 查询。使用 `queries` 类别将启用查询日志。 |
| `dispatch` | 将传入的数据包分发到待处理的服务器模块。 |
| `dnssec` | `DNSSEC` 和 `TSIG` 协议处理。 |
| `lame-servers` | 故障服务器（Lame servers）。这些是远程服务器配置错误，`BIND 9` 在解析过程中尝试查询这些服务器时发现。 |

### 6.2.11. lwres 语句语法

这是 `named.conf` 文件中 `lwres` 语句的语法：

```
lwres {

[ listen-on { ip_addr [port ip_port]; [ ip_addr [port ip_port]; ... ] }; ]; ];

[ view_name; ];

[ search domain_name; [ domain_name; ... ] }; ]; ]; [];

[ ndots number; ];

}
```

### 6.12.2 lwres 语句定义与用法

`lwres` 配置名称服务器同时也作为一个轻量级解析服务器运行，请见第 5.2 节。可能存在多个 `lwres` 语句用于配置具有不同属性的轻量级解析服务器。
`listen-on` 语句指定了该轻量级守护进程实例可以接受请求的地址列表（和端口）。如果没有指定端口，则使用端口 `921`。如果省略了此语句，请求将在 `127.0.0.1` 端口 `921` 上被接受。
`view` 语句将此轻量级解析器守护进程实例绑定到 DNS 命名空间中的一个视图中，其响应的构建方式将与匹配此视图的普通 DNS 查询相同。如果省略了此语句，将使用默认视图；如果没有默认视图，则会触发错误。
`search` 语句等同于 `/etc/resolv.conf` 中的 `search` 语句。它提供了一个域名列表，这些域名会被附加到查询中的相对名称之后。
`ndots` 语句等同于 `/etc/resolv.conf` 中的 `ndots` 语句。它指示了相对域名名中在附加路径元素之前，应导致精确匹配查找的最少点（dots）数。

### 6.12.3. options 语句语法

这是 `named.conf` 文件中 `options` 语句的语法：

```
options {

[ version version_string; ];

[ directory path_name; ];

[ named-xfer path_name; ];

[ tkey-domain domainname; ];

[ tkey-dhkey key_name key_tag; ];

[ dump-file path_name; ];

[ memstatistics-file path_name; ];

[ pid-file path_name; ]

[ statistics-file path_name; ];

[ zone-statistics yes_or_no; ];

[ auth-nxdomain yes_or_no; ];

[ deallocate-on-exit yes_or_no; ]

[ dialup_option; ]

[ fake-query

[ fake-query yes_or_no; ]

[ has-old-clients yes_or_no; ]

[ host-statistics yes_or_no; ]

[ minimal-responses yes_or_no; ]

[ multiple-cnames yes_or_no; ]

[ notify yes_or_no; ]

[ recursion yes_or_no; ]

[ rfc2308-type yes_or_no; ]

[ use-id-pool yes_or_no; ]

[ maintain-ixfr-base yes_or_no; ]

[ forward ( | first ) ];

[ - ];

warders { [ addr [port]; [ addr [port]; ... ] ; } ];

[ allow-query-

; ]

[ also-notify { ip_addr {ip_port} ; [ ip_addr {ip_port}; ... ] ; } ]

[ max-ifxr-log-size number; ]

[ coresize size_spec ; ]

[ datasize size_spec ; ]

[ files size_spec ; ]

[ stacksize size_spec ; ]

[ cleaning-interval number; ]

[ heartbeat-interval number; ]

[ interface-interval number; ]

[ statistics-interval number; ]

[ topology { address_matchlist }; ]

[ sortlist { address_matchlist }; ]

[ rrset-order { order_spec ; [ order_spec ; ...]; } ]

[ max-ttl number; ]

[ max-cache-ttl number; ]

[ sig-validity-interval number ; ]

[ min-roots number; ]

[ use-ifxr yes_or_no; ]

[ provide-ifxr yes_or_no; ]

[ request-ifxr yes_or_no; ]

[ treat-cr-space yes_or_no; ]

[ min-refresh-time number ; ]

[ max-refresh-time number; ]

[ min-retry-time number ; ]

[ max-retry-time number; ]

[ port ip_port; ]

[ additional-from-auth yes_or_no ; ]

[ additional-from-cache yes_or_no ; ]

[ random-device path_name ; ]

[ max-cache-size size_spec ; ]

[ match-mapped-addresses yes_or_no; ]

;
}
```
