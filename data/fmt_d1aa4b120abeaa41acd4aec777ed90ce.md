
## server 语句

`server` 语句允许您为远程服务器定义某些特性。可能的特性设置如表 16-28 所示。语法如下：

```
server ip_addr {
    [ bogus yes_or_no; ]
    [ support-ixfr yes_or_no; ]
    [ transfers number; ]
    [ transfer-format ( one-answer | many-answers ); ]
    [ keys { key_id [key_id ... ] }; ]
};
```

### 表 16-28 Server 语句

| **语句** | **功能** |
| :--- | :--- |
| `bogus yes \| no;` | 如果设置为 yes，则不向该服务器发送查询。这对于暂时停止向提供错误信息的服务器发送查询很有用。 |
| `support-ixfr yes \| no;` | 启用或禁用增量区域传输。 |
| `transfers <number>;` | 限制来自该服务器的入站区域传输数量。 |
| `transfer-format one-answer \| many-answers;` | 逐条记录或多个记录进行区域传输。`many-answers` 选项仅由 BIND 8.1 和 4.9.5 的补丁版本支持。 |
| `keys { key_id...};` | 与安全传输一起使用。 |

## logging 语句

`BIND` 拥有任何应用程序中最具自定义性的日志记录选项之一。语法如下：

```
logging {
    [ channel channel_name {
        ( file path_name
            [ versions ( number | unlimited ) ]
            [ size size-spec ]
        | syslog ( kern | user | mail | daemon | auth | syslog | lpr |
                    news | uucp | cron | authpriv | ftp |
                    local0 | local1 | local2 | local3 |
                    local4 | local5 | local6 | local7 )
        | null );
        [ severity ( critical | error | warning | notice |
                    info | debug [ level ] | dynamic ) : ]
        [ print-category yes_or_no; ]
        [ print-severity yes_or_no; ]
        [ print-time yes_or_no; ]
    }; ]
    [ category category_name |
        channel_name; [ channel_name; ... ]
    ];...;
};
```

`channel` 块定义信息发送到哪里，无论是 `syslog` 设施还是单独的文件。`category` 块确切地定义记录哪些信息，因此您只看到想要或需要的内容。`BIND` 文档详细涵盖了日志记录。

## zone 语句

`zone` 块是 `named.conf` 文件中信息的真正核心。这些块告诉服务器负责哪些域名或区域，以及它扮演的角色。`zone` 块的格式取决于服务器的功能。表 16-29 显示了不同的 `zone` 类型。

### 表 16-29 Zone 类型

| **Zone 类型** | **功能** |
| :--- | :--- |
| `master` | 此服务器包含主 zone 信息并提供权威答案。 |
| `slave` | 主 zone 的副本。服务器保存 zone 信息的只读副本。 |
| `stub` | 类似于从服务器，但仅复制名称服务器 (NS) 记录。 |
| `forward` | 将此 zone 的所有查询引导至另一台服务器。 |
| `hint` | 使用提示文件来定位根名称服务器。 |

主 `zone` 将包含 DNS 信息的资源记录保存在磁盘上的文件中，称为 `zone` 文件。以下是主 `zone` 的格式。

```
zone domain_name [ ( in | hs | hesiod | chaos ) ] {
    type master;
    file path_name;
    [ forward { only | first }; ]
    [ forwarders { ip_addr ; [ ip_addr : ... ] } ];
    [ check-names ( warn | fail | ignore ); ]
    [ allow-update { address_match_list }; ]
    [ allow-query { address_match_list }; ]
    [ allow-transfer { address_match_list }; ]
    [ dialup yes_or_no; ]
    [ notify yes_or_no; ]
    [ also-notify { ip_addr; [ ip_addr : ... ] }; ]
    [ ixfr-base  path_name; ]
    [ pubkey number number number string; ]
};
```

以下是从 `zone` 或 `stub zone` 的格式：

```
zone domain_name [ ( in | hs | hesiod | chaos ) ] {
    type ( slave | stub );
    [ file path_name; ]
    [ ixfr-base  path_name; ]
    masters [ port_ip_port ]; [ ip_addr; [ ip_addr : ... ] };
    [ forward { only | first }; ]
    [ forwarders { ip_addr ; [ ip_addr : ... ] } ];
    [ check-names ( warn | fail | ignore ); ]
    [ allow-update { address_match_list }; ]
    [ allow-query { address_match_list }; ]
    [ allow-transfer { address_match_list }; ]
    [ transfer-source ip_addr; ]
    [ dialup yes_or_no; ]
};
```

### 转发区域格式

```
zone domain_name [ ( in | hs | hesiod | chaos ) ] {
    type forward;
    [ forward ( only | first ); ]
    [ forwarders [ ip_addr : [ ip_addr : ... ] ] ]:
    [ check-names ( warn | fail | ignore ); ]
};
```

提示区域（`hint zone`）用于引导 DNS 服务器。服务器解析客户端查询所需的信息仅包括下一步去哪里，即根名称服务器。服务器会查询列出了根名称服务器 IP 地址的提示文件。`BIND` 软件包包含此文件，但如果服务器发生移动，该文件应定期更新。

```
zone "." [ ( in | hs | hesiod | chaos ) ] {
    type hint;
    file path_name;
    [ check-names ( warn | fail | ignore ); ]
};
```

### 表 16-30：区域选项

| **选项** | **功能** |
| :--- | :--- |
| `check-names warn\|fail\|ignore;` | 检查待解析的名称是否为合法名称。 |
| `Allow-query {address match list};` | 控制允许哪些系统提交查询。 |
| `Allow-transfer {address match list};` | 控制哪些系统可以请求区域传输。 |
| `Transfer-source {ip address}>*` | 控制使用哪个本地地址作为区域传输的源地址。 |
| `ixfr-base "path";` | 增量传输事务日志名称。 |
| `max-transfer-time-in < number >;` | 如果入站区域传输未在 `< number >` 分钟内完成，连接将被断开。 |
| `dialup yes\|no;` | 指定区域传输是否通过拨号连接进行。 |
