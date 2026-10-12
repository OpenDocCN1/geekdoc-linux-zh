
```
C:\netstat -n
活动连接

| 协议 本地地址 | 远程地址 | 状态 |
|---|---|---|
| TCP | 192.168.21:1463 | 192.168.10:1053 | ESTABLISHED |
| TCP | 192.168.21:2582 | 192.168.9:9139 | ESTABLISHED |
| TCP | 192.168.21:3658 | 192.168.30:9100 | SYN_SENT |
| TCP | 192.168.21:3716 | 192.168.10:4678 | ESTABLISHED |
| TCP | 192.168.21:3940 | 207.46.106.78:1863 | ESTABLISHED |
```

最后，你可以指定 `-e` 开关来显示所有正在监听的 TCP/IP 连接和端口。我不会列出输出，因为那会产生很多页内容。只需说它看起来比之前的 `netstat` 输出长得多。

## 显示接口统计

如果你使用 `-e` 开关，`Netstat` 会显示各种协议统计数据，如下：

```
C:\netstat -e
接口统计

| | 接收 | 发送 |
|---|---|---|
| 字节 | 672932849 | 417963911 |
| 单播包 | 1981755 | 1972374 |
| 非单播包 | 251869 | 34585 |
```

此输出中需要注意的项目是丢弃（`Discards`）和错误（`Errors`）。如果它们不接近零，说明网络流量过大。

## Netstat

你可以通过 `-s` 显示额外的统计数据，如下：

```
C:\>netstat -s
```

### TCP 统计数据

| 活动打开 | 2362 |
| 被动打开 | 1074 |
| 失败连接 | 5283 |
| 当前连接 | 6572 |
| 接收分段 | 1791 |
| 发送分段 | 1784 |
| 重传分段 | 1110 |

### UDP 统计数据

| 接收数据报 | 33066 |
| 无端口 | 2909 |
| 接收错误 | 0 |
| 发送数据报 | 202142 |

## Nslookup

`Nslookup` 命令是诊断 DNS 问题的强大工具。当你通过指定 IP 地址而不是 DNS 域名访问资源时，你就知道自己遇到了 DNS 问题。例如，如果你在浏览器地址栏中输入 `66.135.192.87` 可以访问 `www.ebay.com`，但输入 `www.ebay.com` 却不行，你有 DNS 问题。

### 查询 IP 地址

`Nslookup` 最简单的用法是查询给定名称 IP 地址。例如，我如何知道 `66.135.192.87` 是 `ebay.com` 的 IP 地址的？我使用 `nslookup` 来查找：

```
C:\nslookup ebay.com

Server:   nsl.org.twtelecom.net

Address:  168.215.210.50
```

```
非权威回答:

Name:     ebay.com

Address:  66.135.192.87
```

```
C:\>
```

如你所见，我输入了 `nslookup`，后面跟着我想查询的 DNS 域名。`Nslookup` 发出了 DNS 查询进行查找。查询发送到了位于 `168.215.210.50` 的 `nsl.org.twtelecom.net` 名称服务器。它显示了与 `ebay.com` 关联的 IP 地址：`66.135.192.87`。

在某些情况下，你可能会发现 `nslookup` 命令给出了错误的 IP 地址。当然，要确定这一点，你必须确切知道主机 IP 地址应该应该是什么。例如，如果你知道你的服务器是 `203.172.182.10`，但在查询服务器主机名时，`Nslookup` 返回了一个完全不同的 IP 地址，那么可能是某个 DNS 记录出现了问题。

### 让我离开这里！

令我很苦恼的一点是，似乎每个使用子命令的程序选择了不同的命令来退出应用程序。我永远记不住退出 `Nslookup` 的命令是 `quit`、`bye` 还是 `exit`。所以我通常最后得把它们都试一遍。无论我用什么程序，我似乎总是选了一个对其他程序有效的命令。当我在 `Nslookup` 中，我使用 `Bye`。当我在 FTP 中，我使用 `Exit`！当我在电脑上时，每个程序都会通过以下命令响应退出程序并返回命令提示符：

- Quit
- Exit
- Bye
- Leave
- Sayonara
- Ciao
- Mañana
- Makelikeatreegetouthaire（为了纪念《回到未来》系列电影中的 Biff，当然了）

书籍第 6 章

## 使用 Nslookup 子命令

如果你在不带任何参数的情况下使用 `Nslookup`，`Nslookup` 命令将进入子命令模式。它会显示一个提示符 `-`，让你知道你正处于 `Nslookup` 的子命令模式，而不是普通的 Windows 命令提示符。在子命令模式下，你可以输入子命令来设置选项或执行查询。你可以输入问号 `?` 来获取这些命令的列表。表 6-2 列出了你将使用的子命令。

| 表 6-2 最常用的 Nslookup 子命令 |
| 子命令 | 作用 |
| :--- | :--- |
| name | 为当前名称服务器查询指定的名称。 |
| server name | 将当前名称服务器设置为你指定的服务器。 |
| root | 将根名称服务器设置为当前服务器。 |
| set type=x | 指定要显示的记录类型，例如 A、CNAME、MX、NS、PTR 或 SOA。指定 ANY 以列出所有记录。 |
| set debug | 开启调试模式，显示有关每个查询的详细信息。 |
| set nodebug | 关闭调试模式。 |
| set recurse | 启用递归搜索。 |
| set norecourse | 禁用递归搜索（search）。 |
| exit | 退出 Nslookup 程序并返回命令提示符。 |

## 显示 DNS 记录

`Nslookup` 的主要用途之一是检查你的 DNS 配置以确保其设置正确。要做到这一点，请遵循以下步骤：

1. 在命令提示符处，输入不带任何参数的 `nslookup`。

`Nslookup` 显示默认名称服务器的名称并显示提示符。

```
C:\nslookup

Default Server: ns1.org.twtelecom.com

Address: 168.215.210.50

>
```

2. 输入子命令 `type=any`。

`Nslookup` 默地执行你的命令并显示另一个提示符：
> set type=any
>

3. 输入你的域名。

`Nslookup` 通过显示域名的名称服务器进行响应：
> lowwriter.com
Server: ns1.org.twtelecom.com
Address: 168.215.210.50

非权威回答：
lowwriter.com nameserver = NS000.NS0.com
lowwriter.com nameserver = NS207.PAIR.com

lowwriter.com nameserver = NS000.NS0.com
lowwriter.com nameserver = NS207.PAIR.com
>

4. 使用命令切换到该域名的名称服务器之一。

例如，要切换到上方列出的第一个名称服务器，输入 `server NS000.NS00.com`。`Nslookup` 回一条指示新默认服务器的消息：

```
server ns000.ns0.com

Default Server: ns000.ns0.com

Address: 216.92.61.61

>
```

5. 再次输入你的域名。

这一次，`Nslookup` 通过显示你域名的 DNS 信息进行响应：

> > lowwriter.com
Server: ns000.ns0.com
Address: 216.92.61.61

```
lowwriter.com

primary name server = ns207.pair.com

responsible mail addr = root.pair.com

serial = 2001121009

refresh = 3600 (1 hour)

retry = 300 (5 mins)

expire = 604800 (7 days)

default TTL = 3600 (1 hour)

lowwriter.com nameserver = ns000.ns0.com

lowwriter.com nameserver = ns207.pair.com

lowwriter.com MX preference = 50, mail exchanger = sassi.pair.com

>tracer internet address = 209.68.34.15
```
