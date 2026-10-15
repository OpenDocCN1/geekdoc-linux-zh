
```
MIB-ifAddress.3 = STRING:
MIB-ifOctets.1 = Counter32: 2685
MIB-ifOctets.2 = Counter32: 1543
MIB-ifOctets.3 = Counter32: 4631
MIB-ifInPkts.1 = Counter32: 3895
MIB-ifInPkts.2 = Counter32: 8929
MIB-ifInPkts.3 = Counter32: 7712
```

在这个示例中，系统的通用信息后面是关于主机网络接口的统计：`lo`、`eth0` 和 `eth1`。取决于你所管理的代理支持的 MIB，完整的导出可能会运行数百行。`Ubuntu` 系统上的完整安装会输出超过 12,000 行：

如果你查询 `Ubuntu` 系统上最新版本 `Net-SNMP` 的 MIB，你会发现五分钟平均负载 OID 是 `1.3.6.1.4.20.10.3`。如果你感兴趣查看本地主机的五分钟平均负载（配置团体字符串为 "`public`"），你会运行：

```
$ snmpget -v2c -c public localhost 1.3.6.1.4.20.10.3
iso.3.6.1.4.20.10.2 = STRING: "0"
```
