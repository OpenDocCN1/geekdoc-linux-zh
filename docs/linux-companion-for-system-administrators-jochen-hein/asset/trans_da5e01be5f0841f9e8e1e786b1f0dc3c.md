

## 15.4.1 使用 nslookup 进行交互式 DNS 请求

使用 nslookup 程序可以以两种模式进行 DNS 请求：交互式和非交互式。在交互式模式下，可以一个接一个发出不同的请求。在非交互式模式下，程序仅显示所需信息并终止。

可以在主机名或地址之前通过前导减号（-）指定附加选项。此外，默认值可以存储在 `~/.nslookuprc` 文件中。nslookup 的非交互式调用的示例可以参见列表 15.4。

如果未指定任何参数，或者在减号（-）之后指定了名称服务器（名称或 IP 地址），则使用交互式模式。随后，可以通过输入主机名或 IP 地址来启动请求。可以使用 `set type=any` 命令请求计算机上的所有信息。示例可以参见列表 15.5。关于 nslookup 的更详细信息以及所有可能的请求选项列表，可以查看 `nslookup(1)` 的帮助页。

```
(Linux): > nslookup ftp
server: carrot.example.org
Address: 192.168.3.150

name: pea.example.org
Address: 192.168.3.150
Aliases: ftp.example.org
```

列表 15.4 非交互式模式下的 nslookup。

```
(Linux):> nslookup
Default server: carrot.example.org
Address: 192.168.3.150

> ftp
server: carrot.example.org
Address: 192.168.3.150

name: pea.example.org
Address: 192.168.3.155
Aliases: ftp.veggies.example.org

> set type=any
> ftp
server: carrot.veggies.example.org
Address: 192.168.3.350

ftp.veggies.example.org canonical name = pea.veggies.example.org
veggies.example.org nameserver = carrot.veggies.example.org
pea.example.org internet address = 192.168.3.155
> exit
```

列表 15.5 交互式模式下的 nslookup。

nslookup 程序也可用于执行反查询，即请求特定 IP 地址所属的名称。在这种情况下，你只需指定 IP 地址而不是主机名。

nslookup 程序可以查询不同的名称服务器并分析发送和接收的数据包。由于该程序在 Windows NT 等其他系统中可用，因此它被广泛用于测试名称服务器。

## 15.4.2 使用 host 进行名称服务器请求

host 程序允许你分析存储在名称服务器中的数据。这里一个有用的功能是数据可以以名称数据库条目所需的格式输出（选项 -v）。通过选项 `-t`，可以选择所需的条目（例如 ns、cname、soa、hinfo、mx，以及代表所有条目的 any 或 `*`）。条目的含义将在第 21 章中进行详细解释。

选项 `-a` 是 `any` 的缩写。所有条目的更详细的描述可以在 `host(1)` 帮助页以及随 bind 源码一起提供的《Bind Operators Guide》中找到。列表 15.6 显示了 host 的一些用法。

```
(Linux)> host pea
pea.example.org has address 192.168.3.155
(Linux)> host -v pea
Trying domain "example.org"
rcode = 0 (Success), answer:
pea.example.org A 86400 IN
For authoritative answers, see:
example.org 86400 IN NS carrot.org
Additional information:
carrot.example.org 86400 A 192.168.3.150
(Linux)> host -m pea
Trying domain "example.org"
rcode = 0 (Success), answer:
pea.example.org 86400 IN A 192.168.3.155
pea.example.org 86400 IN HINFO IBM-PC/AT UNIX-PC
pea.example.org 86400 IN TXT "Test with text"
For authoritative answers, see:
example.org 86400 IN NS carrot.org
```

列表 15.6 使用 host 进行名称服务器请求。

## 15.4.3 使用 dig 进行名称服务器请求

另一个分析名称服务器的工具是 dig（Domain Information Groper）。该程序可以交互式使用，也可以以多种模式。许多 TCP/IP 软件包仅包含此程序而不包含 nslookup host。

dig 的选项和功能在帮助页中有详细描述。请注意，对于“反查询”，除了 IP 地址外，还必须指定选项 `-x`。

## 15.5 名称服务器的可靠性

目前为止，Internet 协议的开发和实现是出于实现技术和功能的考虑的。当只有少数可靠的用户参与互联网时，这并不是一个问题。在过去的几年里，互联网计算机和用户的数量大幅增长。

