
`options` 语句可以使用的值列表非常长。这些值在表 12-2 中按字母顺序列出。

| 表 12-2 | Options 值及其含义 |
| --- | --- |
| 值 | 含义 | 用法 |
| allow-query | 仅接受来自地址列表中主机的查询（默认接受任何主机的查询）。 | `allow-query ("address-list")` |
| allow-transfer | 仅接受地址列表中主机的区域传输（默认允许向所有主机传输）。 | `allow-transfer ("address list")` |
| auth-nxdomain | 服务器作为权威名称服务器做出响应（默认是 yes）。 | `auth-nxdomain "yes or no";` (二选一) |
| check-names | 检查主机名是否符合 RFC 规范。 | `check-names "master or slave or response warn or fail ignore";` (从每组中选择一个) |
| cleaning-interval | 指定服务器移除过期资源记录之前的时间段（默认为 60 分钟）。 | `cleaning-interval "number";` (指定分钟数) |
| coresize | 指定核心转储文件的最大 own。 | `coresize "size";` (以字节指定大小) |
| datasize | 限制内存使用。 | `datasize "size";` (以字节指定大小) |
| deallocate-on-exit | 检测内存泄漏（默认是 no）。 | `deallocate-on-exit "yes or no";` (二选一) |
| directory | 服务器配置文件所在目录的路径 | `directory "path to directory";` (指定路径) |
| dump-file | 如果 named 接收到 SIGINT 信号，它将数据库转储此处指定的文件（默认是 named_dump.db）。 | |
| fake-iquery | 如果设置为 yes，服务器向反向查询发送伪造回复而不是其他 | `fake-iquery "yes or no";` (二选一) |
| fetch-glue | 如果设置为 yes，服务器将获取响应的粘合记录（默认是 yes）。 | `fetch-glue "yes or no";` (二选一) |
| files | 限制并发打开的文件数（默认无限制） | `files "number";` (指定数量) |
| forward | 如果设置为 first，则首先查询 forwarders 选项列出的服务器，然后服务器尝试寻找答案。如果设置为 only，则仅查询 forwarders 列表中的服务器。 | `forward "first or only";` (二选一) |
| forwarders | 显示转发查询的服务器 IP 地址（默认是 none）。 | `forwarders "IP addresses of servers";` (指定 IP 地址) |
| host-statistics | 如果设置为 yes，服务器将保留主机的统计信息（默认是 no）。 | `host-statistics "yes or no";` (二选一) |
| interface-interval | 指定在网络中搜索新或删除接口的间隔（默认为 60 分钟）。 | `interface-interval "time";` (指定分钟时间) |
| listen-on | 指定服务器监听查询的端口和接口（默认端口 53）。 | `listen-on "port (address list)\ (指定端口号和地址列表)` |

## 表 12-2 (续)

| 值 | 含义 | 用法 |
|---|---|---|
| max-transfer-in | 指定服务器等待入站传输完成的时间（默认为 120 分钟）。 | `max-transfer-in "time";` (指定分钟) |
| statistics-file | 当设置 deallocate-on-exit 时，指定写入统计信息的文件（默认是 named_stats）。 | |
| multiple-cnames | 当设置为 yes 时，启用 CNAME 使用（默认是 no）。 | `multiple-cnames "yes or no";` (二选一) |
| named-xfer | 指定区域传输程序的路径。 | `named-xfer "path to file";` (指定路径) |
| notify | 当区域更新时，此选项设置为 yes 会发送 NOTIFYset（默认是 yes）。 | `notify "yes or no";` (二选一) |
| pid-file | 存储进程 ID 的文件名。 | `pid-file "path to file";` (指定路径) |
| query-source | 用于查询其他服务器的端口和 IP 地址。 | `query-source "address list";` |
| recursion | 服务器递归查询答案（默认是 yes）。 | `recursion "yes or no";` (二选一) |
| stacksize | 服务器可以使用的栈内存。 | `stacksize "number";` (指定数量) |
| statistics-interval | 日志统计信息的时间间隔（默认为 60 分钟）。 | `statistics-interval "time";` (指定分钟) |
| topology | 设置对远程服务器的偏好。 | `topology ("address list";` |
| transfer-format | 设置为 one-answer 时，每条消息发送一个资源记录。设置为 many，在每条消息中传输尽可能多的记录。（默认是 one）。 | `transfer-format "one-answer many";` (二选一) |
| transfers-in | 最大并发区域传输（默认 10）。 | `transfers-in "number";` (指定数量) |
| transfers-out | 最大并发出站传输。 | `transfers-out "number";` (指定数量) |
| transfers-per-ns | 限制来自单个服务器的入站传输（默认为两个）。 | `transfers-per-ns "number";` (指定数量) |

# 190 第四部分：配置您的企业级 Linux Internet 服务

`logging` 语句的语法与 `option` 语句的语法相似。以下命令将信息发送到文件（斜体项目表示您需要输入的信息）：

```
logging {

  channel channel_name (

    (file) path to file

    versions specify number or unlimited

  size specify size in bytes if you want to send the information to the

  syslog, the syntax is

}
```

```
logging {

  channel channel_name (

    syslog (从以下选项中发送位置)

    (kern,user,mail,daemon,auth,syslog,lpr,news,wuuc,cron,

    authpriv,ftp,local0 through local7)

  )

}
```

要丢弃信息，请选择 `null` 作为目标。

```
logging {

  channel channel_name (

    null;

  );
```
