
## mtx 的更改

在服务器 mtx 上的 `/etc/named.conf` 中添加以下区域：

```conf
zone "42.168.192.in-addr.arpa" {
    type slave;
    file "slave.192.168.42";
    masters {192.168.42.1};
}
nzone "domain.cxm" {
    type slave;
    file "slave.domain.cxm";
    masters {192.168.42.1};
};
```

在每个区域中，该语句指定了从主服务器获取数据并回答查询的文件。`masters {192.168.42.1};` 语句（准确地）告诉 named 每当超过刷新时间或收到 NOTIFY 192.168.42.1 时（以先到者为准），从 192.168.42.1 获取数据。`type slave` 语句允许该区域通过区域传输从 192.168.42.1 获取数据。

注意，文件以 slave 单词开头而不是 master。这种惯例允许管理员通过重启主服务器的命令来刷新所有从区域。与主区域不同，这些从数据文件不会被维护，并可以由服务器重新生成。这与删除主服务器的数据冲突将是灾难性的。当然，如果主服务器宕机，删除从区域将同样是灾难性的，因此在删除任何从文件之前请务必小心。

添加从区域后，只需使用命令重启主服务器：

```bash
/sbin/init.d/named restart
```

named 守护进程将创建从数据文件，除了接收 NOTIFY 语句外，它将作为从服务器运行（主服务器不知道该从服务器的存在）。因此，在主服务器不知道的情况下设置从服务器是完全可能的。由于给主服务器造成了额外的流量，这并不是标准的 DNS 配置。应该通知主服务器管理员所有的从服务器。

主服务器可以通过限制允许接收区域传输的服务器来防止未经授权的从服务器访问。只需在 named.conf 的部分或全局部分放入以下语句之一：

```conf
allow-transfer {192.168.42.2};  # 只有 mtx 可以作为从
```

或者

```conf
allow-transfer {192.168.42.2; 192.168.42.1};  # 都是
```

或者

```conf
allow-transfer {192.168.42.0/24};  # 仅限子网上的主机
```

验证文件 /var/named/domain.cxm 和 /var/named/slave.192.168.42 是否存在。如果它们存在，验证以下命令列表是否输了预期的输出：

```bash
nslookup numark 192.168.42.2
nslookup mtx 192.168.42.2
nslookup numark.domain.cxm 192.168.42.2
nslookup domain.cxm 192.168.42.2
nslookup 192.168.42.1 192.168.42.2
nslookup 192.168.42.2 192.168.42.2
```

在下一节中，你将成为从区域的主服务器，使其在修改和重启时可以发送 NOTIFY 语句。

## numark 的更改

在 named.domain.cxm 的 IN NS 语句下方添加以下行：

```conf
IN NS
mtx
```

在保存工作并退出之前，请确保递增序列号（括号列表中的第一个数字）。

现在，在 named.192.168.42.2 的 IN NS 语句下方添加以下行：

```conf
IN NS
192.168.42.2.
```

请记住 mtx.domain.cxm 的地址是 192.168.42.2。再次，请确保递增序列号。递增的序列号告诉从服务器它需要执行区域传输。最后，重启 numark DNS 服务器：

```bash
/bin/init.d/named restart
```

添加 NS 记录使得 mtx 上的 DNS 服务器能够接收 NOTIFY 语句，导致该服务器启动区域传输。新的 NS 记录还允许 mtx 用作备用域名。

要验证从服务器是否正常工作，请执行以下 shell 命令并确保你获得了预期的输出：

```bash
nslookup numark 192.168.42.2
nslookup mtx 192.168.42.2
nslookup numark.domain.cxm 192.168.42.2
nslookup mtx.domain.cxm 192.168.42.2
nslookup 192.168.42.1 192.168.42.2
nslookup 192.168.42.2 192.168.42.2
```

DNS 从服务器及其区域传输，结合委托，使 DNS 能够服务数百万个 URL 的能力。

## DNS 的故障排除与调试

本章之前讨论了许多 DNS 故障排除技术，例如使用 telnet 程序检测反向 DNS 问题。其他故障排除选项包括脚本程序和 named 日志选项。

## 使用脚本对您的 DNS 设置进行压力测试

您可以编写两个实用的脚本来对 DNS 设置进行压力测试。它们可以命名为任何名称，但本示例将它们命名为 check1 和 check。
