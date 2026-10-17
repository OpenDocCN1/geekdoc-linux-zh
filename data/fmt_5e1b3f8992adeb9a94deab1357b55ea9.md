
# DNS 与域名
## 第 4 章

```
13      type master;
14      file "pri/localhost";
15  };
16 
17  zone "0.0.127.in-addr.arpa" {
18      type master;
19      file "pri/127.0.0";
20  };
```

第 1–3 行定义了在 `named` 程序中使用的选项。第 2 行显示配置文件的默认目录位于 `/var/named` 目录。第 5–7 行定义了“根”域定义。如前所述，每个 DNS 服务器都必须知道根服务器的地址，才能查询 DNS 树。第 7 行表明包含根服务器地址的文件为 `/var/root.cache`。该文件可以使用 `dig` 命令生成：

```
dig @root-servers.net ns >> root.cache
```

列表 4.9 显示了一个示例的 `/var/named/root.cache` 文件。

# 列表 4.9 示例 DNS /var/named/root.cache 文件

```
1 ; <<>> DIG 8.2 <<>> @root-servers.net . ns
2 ; (1 server found)
3 ; res options: init recursion defs dnsdnr
4 ; get answer:
5 ; >>HEADER-- opcode: QUERY, status: NOERROR, id: 10
6 ; flags: qa aa rd QUERY: 1, ANSWER: 13, AUTHORITY: 0, OPTIONAL: 13
7 ; QUERY SECTION
8 ;\9 ; type = NS, class = IN
10 ; ANSWER SECTION:
```
