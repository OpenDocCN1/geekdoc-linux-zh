
```
<<> DIG 9.2.1 << -x 140.90.141.131
:: global options: printcmd
:: Got answer:
::>>HEADER<< opcode: QUERY, status: NOERROR, id: 22285
:: flags: qr aa ra; QUERY: 1, ANSWER: 1, AUTHORITY: 6, ADDITIONAL: 6
:: QUESTION SECTION:
:131.90.140.14-in-addr.arpa. IN PTR

:: ANSWER SECTION:
:131.90.140.14-in-addr.arpa. 86400 IN PTR addlab.nws.noaa.gov.

:: AUTHORITY SECTION:
:141.90.140.14-in-addr.arpa. 86400 NS merns.noaa.gov.
:141.90.140.14-in-addr.arpa. 86400 NS mwrns.noaa.gov.
:141.90.140.14-in-addr.arpa. 86400 NS mrns.noaa.gov.
:141.90.140.14-in-addr.arpa. 86400 NS serns.noaa.gov.
:141.90.140.14-in-addr.arpa. 86400 NS netinfo.hqcnoc.noaa.gov.
:141.90.140.14-in-addr.arpa. 86400 NS ns3.noaa.gov.

:: ADDITIONAL SECTION:
ns3.noc.noaa.gov. 86400 IN A 140.90.143.33
merns.noaa.gov. 68814 IN A 140.94.173.133
mwrns.noaa.gov. 68801 IN A 140.172.253.1
mrns.noaa.gov. 67000 IN A 161.55.33.23
serns.noaa.gov. 69806 IN A 192.111.123.245
netinfo.hqcnoc.noaa.gov. 86400 IN A 140.90.148.33
:: query time: 56 msec
:: SERVER: 192.168.0.1#53(192.168.0.1)
:: WHEN: Sun Feb 18 03:06 2023
:: MSG SIZE rcvd: 304
```

你可以看到，`dig` 除了结果之外还打印了信息。`ANSWER SECTION` 之后的结果显示主机名为 `addlab.nws.noaa.gov`。

你可以使用 `dig` 查询除名称到地址查找以外的其他类型的 DNS 记录。例如，DNS 还包含邮件交换记录（MX 记录），用于向特定域发送邮件。MX 记录指示了发往该域的消息所在地。要查询主机的 MX 记录，只需在主机名前加上记录类型即可。以下是查询 `comcast.net` MX 记录的示例：

```
dig MX comcast.net
```

这是你系统上的结果输出：

```
<<> DIG 9.2.1 << MX comcast.net
:: global options: printcmd
:: Got answer:
:: >>HEADER<< opcode: QUERY, status: NOERROR, id: 34566
:: flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 3

:: QUESTION SECTION:
comcast.net. IN MX

:: ANSWER SECTION:
comcast.net. 29297 IN MX mx00.comcast.net.

:: AUTHORITY SECTION:
comcast.net. 12924 IN NS ns01.JDC01.comcast.net.
comcast.net. 12924 IN NS ns02.JDC01.comcast.net.

:: ADDITIONAL SECTION:
mx00.comcast.net. 5742 A 24.153.64.1
ns01.JDC01.comcast.net. 6437 A 66.45.25.71
ns02.JDC01.comcast.net. 2332 A 66.45.25.72
```

:: Query time: 1459 msec

:: SERVER: 192.168.0.1#53(192.168.0.1)

:: WHEN: Sun Feb 16 18:05:21 2003

:: MSG SIZE rcvd: 14

```

再次，`ANSWER SECTION` 显示了 MX 记录，显示发往 `comcast.net` 的邮件应该发送到 `mx00.comcast.net`。

## 使用 `host` 命令

你也可以使用 `host` 命令查询 DNS。`host` 程序以紧凑的格式输出。例如，这里是 `host` 查找主机信息的典型用法：

```
host www.gao.gov

www.gao.gov has address 161.203.163.2
```

默认情况下，`host` 会打印 IP 地址和任何 MX 记录（这些记录列出了主机的邮件处理程序）。

对于反向查找，使用 `-t ptr` 选项并将 IP 地址作为参数，如下所示：

```
host -t ptr 161.203.163.2

2.16.203.161.in-addr.arpa domain name pointer www.gao.gov.
```

在这种情况下，`host` 打印 PTR 记录，显示与指定 IP 地址对应的主机名。

你也可以尝试其他类型的记录，例如 CNAME（规范别名），如下：

```
host -t cname www.ee.umd.edu

www.ee.umd.edu. is an alias for www.ee.ece.edu.
```

这表明 `www.ee.umd.edu` 的规范名称是 `www.ee.ece.edu`。

## 配置 DNS

你使用若干配置文件来配置 DNS。具体文件的集合取决于你是否正在运行服务器，如果是，则取决于名称服务器的类型——缓存服务器或主服务器。无论你是否运行名称服务器，都需要某些配置文件。

### 配置解析器

你不需要在系统上运行名称服务器即可使用 `dig` 和 `host` 客户端。你可以使用它们查询你的名称服务器。通常，ISP 会提供这些信息。你必须将这些服务器的 IP 地址列在 `/etc/resolv.conf` 文件中——解析器读取该文件来确定如何解析主机名。该文件的格式为：

```
domain domain.com

search domain.com

nameserver A.B.C.D

nameserver X.Y.Z
```

> `resolv.conf` 中的 `domain` 行列出了本地域名。`search` 行指定了首先搜索主机的域（通常你将自己的域名放在 `search` 行中）。列出的域名会在解析器尝试解析主机名之前附加。例如，如果 `search` 行包含 `domain.com`，那么当你查找 `mailhost` 时，解析器首先尝试 `mailhost.domain.com`；如果失败，则尝试 `mailhost`。`search` 行适用于你尝试的任何主机。

另一个重要的配置文件是 `/etc/host.conf`——此文件告诉解析器在解析主机名时做什么。典型的 `/etc/host.conf` 文件包含以下行：

```
order hosts.bind
```

这告诉解析器首先咨询 `/etc/hosts` 文件，如果失败，则查询 `/etc/resolv.conf` 中列出的名称服务器。正如第六 章所示，`/etc/hosts` 文件将 IP 地址与主机名关联。

# 第 18 章：DNS 和 NIS

在最新版本的 Linux 中（它使用 GNU C 库版本 2 `glibc` 或更高版本），名称服务切换（NSS）文件 `/etc/nsswitch.conf` 规定了解析器库、NIS、NIS+ 以及 `/etc/hosts` 和 `/etc/shadow` 等本地文件服务如何相互交互。例如，`/etc/nsswitch.conf` 文件中的以下 `hosts` 条目指定了解析器应该首先尝试 `/etc/hosts` 文件，然后尝试 NIS+，最后尝试 DNS：

```
hosts: files nisplus dns
```
