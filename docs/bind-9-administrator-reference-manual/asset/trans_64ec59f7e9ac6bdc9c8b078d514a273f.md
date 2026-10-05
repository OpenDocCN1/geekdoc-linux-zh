

query-source-v6 选项。如果地址为 * 或省略，则将使用通配符 IP 地址 (INADDR_ANY)。如果端口为 * 或省略，则将使用随机的未特权端口。默认值为：

```
query-source address * port *
query-source-v6 address * port *
```

注意：query-source 选项中指定的地址同时用于 UDP 和 TCP 查询，但端口仅适用于 UDP 查询。TCP 查询始终使用随机的未特权端口。

## 6.2.14.6. 区域传输 (Zone Transfers)

BIND 拥有相应的机制来促进区域传输，并对传输给系统造成的负载进行限制。以下选项适用于区域传输。

### also-notify

定义一个名称服务器的 IP 地址列表，每当加载新的区域副本时，除了区域 NS 记录中列出的服务器外，还会向这些服务器发送 NOTIFY 消息。这有助于确保区域副本快速在隐藏服务器上收敛。如果在区域语句（zone statement）中提供了 also-notify 列表，它将覆盖 options-also-notify 语句。当区域语句被设置为 no 时，全局 also-notify 列表中的 IP 地址将不会为该区域发送 NOTIFY 消息。默认为空列表（无全局通知列表）。

### max-transfer-time-in

运行时间超过此分钟数的入站区域传输将被终止。默认值为 120 分钟（2 小时）。

### max-transfer-idle-in

在这些分钟内内没有进展的入站区域传输将被终止。默认值为 60 分钟（1 小时）。

### max-transfer-time-out

运行时间超过此分钟数的出站区域传输将被终止。默认值为 120 分钟（2 小时）。

### max-transfer-idle-out

在这些分钟内没有进展的出站区域传输将被终止。默认值为 60 分钟（1 小时）。

### serial-query-rate

从服务器会定期查询主服务器，以查找区域序列号是否发生变化。每次此类查询都会使用少量的从服务器网络带宽。为了限制使用的带宽量，BIND 9 限制了发送查询的速率。serial-query-rate 选项的值是一个整数，表示每秒发送查询的最大数量。默认值为 20。

### serial-queries

在 BIND 8 中，serial-queries 选项设置了任何时刻允许处理的并发序列号查询的最大数量。BIND 9 不限制未处理查询的数量，并忽略 serial-queries 选项。相反，它通过定义 serial-query-rate 选项来限制发送查询的速率。

### transfer-format

区域传输可以使用两种格式发送：单回答（one-answer）和多回答（many-answers）。transfer-format 选项用于主服务器以定义其发送的格式。one-answer 为每个传输的资源记录使用一个 DNS 消息。many-answers 将尽可能多的资源记录打包进一个消息中。many-answers 效率更高，但仅由较新的从服务器支持，例如 BIND 9、8.x 以及打过补丁的 BIND 4.9.5。默认值为 many-answers。可以通过 server 语句按服务器为基来覆盖 transfer-format。

### transfers-in

可以并发运行的入站区域传输的最大数量。默认值为 10。增加 transfers-in 可能会加快从区域的收敛，但可能会增加本地系统的负载。

### transfers-out

可以并发运行的出站区域传输的最大数量。超过限制的区域传输请求将被拒绝。默认值为 10。

### transfers-per-ns

从给定的远程名称服务器并发传输的入站区域传输的最大数量。默认值为 2。增加 transfers-per-ns 可能会加快从区域的收敛，但可能会增加远程名称服务器的负载。可以通过 server 语句中的 transfers 短语按服务器为基来覆盖 transfers-per-ns。

## 第 6 章，BIND 9 配置参考

### transfer-source

transfer-source 决定了将使用哪个本地地址绑定到用于获取入站传输区域的 IPv4 TCP 连接。它还决定了用于刷新查询和转发动态更新的源 IPv4 地址以及可选的 UDP 端口。如果未设置，它默认为系统控制的值，该值通常是“最接近”远程端的接口地址。如果为被传输的区域指定了 allow-transfer 选项，则该地址必须出现在远程端的选项中。此语句设置了所有区域的 transfer-source，但可以通过在配置文件的 view 或 zone 块中包含 transfer-source 语句，按视图 或区域为基来覆盖。

### transfer-source-v6

与 transfer-source 相同，只是区域传输是使用 IPv6 执行的。

### notify-source

notify-source 决定了使用哪个本地地址以及可选的 UDP 端口来发送 NOTIFY 消息。该地址必须出现在从服务器的 masters zone 子句或 allow-notify 子句中。此语句设置了所有区域的 notify-source，但可以通过在配置文件的 zone 或 view 块中包含 notify-source 语句，按区域 / 视图为基来覆盖。

### notify-source-v6

与 notify-source 类似，但适用于发送到 IPv6 地址的 notify 消息。

## 6.2.147 操作系统资源限制

可以限制服务器对许多系统资源的使用。在指定资源限制时允许使用比例值。可以使用 107374184 代替 unlimited 来指定  GB 的限制。或者最大可用数量。默认使用服务器启动时的限制。详见描述。以下选项为名称服务器进程设置系统资源限制。某些操作系统不支持部分或任何限制。如果使用了不支持的限制，系统将发出警告。

### coresize

核心转储的最大大小。默认值为 default。

### datasize

服务器可能使用的数据内存量。默认值为 default。这是内存使用的硬限制。如果服务器尝试分配超过此限制的内存，分配将失败，这可能导致服务器无法执行 DNS 服务。因此，此选项对于限制服务器使用的内存非常有用，但默认值太小。如果想限制服务器使用的内存，请使用 max-cache-size 和 recursive-clients 选项。

### files

服务器并发打开的文件的最大数量。默认值为 unlimited。

### stacksize

服务器可能使用的栈内存量。默认值为 default。

## 6.2.14.8 服务器资源限制

以下选项通过服务器内部执行资源消耗限制，而不是通过操作系统。

### max-ifr-log-size

此选项已过时；为了兼容 BIND 8，会被接受但忽略。

### recursive-clients

服务器代表客户端执行的并发递归查询的最大数量。默认值为 1000。由于每个递归客户端使用相当多的内存（大约 20 千字节），在内存有限的主机上可以减少 recursive-clients 选项的值。

### tcp-clients

服务器接受的并发 TCP 连接的最大数量。默认值为 100。

### max-cache-size

用于服务器缓存的最大内存，单位为字节。当缓存中的数据量达到此限制时，服务器将使记录提前过期以防止超过限制。在具有多个视图的服务器中，该限制独立适用于每个视图的缓存。

