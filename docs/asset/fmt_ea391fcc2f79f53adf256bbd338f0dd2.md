
`root@server ~]# tcpdump -e`

这告诉 `tcpdump` 在输出中显示以太网、TCP 和 IP 头部。现在通过访问网站或使用 SSH 与另一个主机通信产生一些流量。这将产生如下输出：

```
15:46:08.02696 0:d0:b7:6b:20:17 00:4b:bc:15:9f ethertype (0x0800), length 191: server.ssh > 10.2.2.4769 Flags [P.] seq 1724400:1724972, ack 529, win 5740, options [nop,nop,ts val 59345613 ecr 1354193], length 576
```

每行的开头是看到数据包的时间戳。行的后续两个条目分别是数据包的源 MAC 和目的 MAC 地址。在第一行中，源 MAC 地址是 d0:b7:6b:20:17，目的 MAC 地址是 0:10:4b:cb:15:9f。MAC 地址之后是数据包类型。在这种情况下，`tcpdump` 看到 0800 并自动将其转换为 ip 以于阅读。

如果你不想让 `tcpdump` 将数字转换为名称（特别是当你的 DNS 解析失效时），可以包含 `-nn` 选项，如下：

```bash
root@server ~]# tcpdump -e -nn
```

`-n` 选项告诉 `tcpdump` 不要进行名称解析。没有名称解析的前述输出如下：

```
15:46:08.026966 0:d0:b7:6b:20:17 00:10:4b:cb:15:9f ethype IPv4 (0x0800) length 191: 10.2.2.1.22 > 10.2.2.2.4769 Flags [P.] seq 1724400:1724976, ack 529, 5740, options [nop,nop,ts val 593457613 ecr 1354193], length 576

15:46:08.044151 0:d0:b7:6b:20:17 00:10:4b:cb:15:9f ethype IPv4 (0x0800) 60: (DF)
```
