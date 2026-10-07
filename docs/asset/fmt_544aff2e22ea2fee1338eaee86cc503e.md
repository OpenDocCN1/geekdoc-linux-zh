
但这里还有其他考虑因素。Samba 环境应该只有一个 WINS 服务器。要真正成为 WINS 服务器，你只需要设置 `wins support`：

```
wins support = yes
```

# 测量广播活动

查看非广播解决方案用处的一种种方法是查看流量。当你看到通过消除这些流量可以回收带宽和延迟后，你可能会开始设置 WINS。作为一种常规做法，调查网络流量是维护其健康的好方法。查看网络上流量的最佳方法是使用“嗅探器”或数据包提取工具。

# 获取增强型 tcpdump

用于局域网/广域网上 NBT 活动的一个有用工具是来自 `samba.org` 站的增强型 `tcpdump`。通过这个工具，你可以真正看到网络上发生了什么，检查问题，并感受你的 WINS 设置缓解了什么。在获取此 `tcpdump` 源码之前，你应该注意某些 Linux 发行版现在自带了增强型 `tcpdump`。如果你没有足够幸运在机器上已经有了它，可以从最近的镜像获取源码——访问 `http://www.samba.org` 获取完整的镜像列表。

要使用它，可以通过上述网站访问：

```
ftp://samba.org/pub/mirrors/sambaftp/tcpdump-smb/
```

# 使用 tcpdump

你会想要熟悉过滤，特别是对于繁忙的网络。即使是最缺乏经验的网络管理员也可以使用此工具获取网络流量概述，并准确了解是谁在做什么。

`tcpdump` 命令的一个用法示例如下：

假设主机 `comet` 上的有人输入了以下 `nmblookup` 命令，以查找当前子网上的所有的主浏览器（Master Browsers）。

```
$ nmblookup -M -
Sending queries to 192.168.0.255
192.168.0.55  MSBROWSE-<01>
192.168.0.3  _MSBROWSE-<01>
```

使用未增强的 `tcpdump` 输出如下：

```
# tcpdump -vv -i eth0
tcpdump: listening on eth0
17:07:19.067598 comet.theeffect.com.1175 > 192.168.0.255.netbios-ns: udp 50 (ttl 64, id 21761)
17:07:19.067598 galalah.theeffect.com.netbios-ns > comet.theeffect.com.1175: udp 62 (ttl 64, id 39148)
```

看起来没什么启发性，对吧？然而，使用 SMB 增强型 `tcpdump`，输出将如列表 34.2 所示。

## 列表 34.2 SMB 增强型 tcpdump

```
# tcpdump -vv -i eth0 -s 1500
tcpdump: listening on eth0
19:14:50.596341 comet.theeffect.com.1175 > 192.168.0.255.netbios-ns:
>> NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
Trid=0xb903
OpCode=0
NmFlags=0x11
Rcode=0
QueryCount=1
AnswerCount=0
AuthorityCount=0
AddressRecount=0
QuestionRecords:
Name='a_MSBROWSE_a NameType=0x01 (Unknown)
QuestionType=0x20
ClassName=0x01
(ttl 64, id 21910)
19:14:50.596341 comet.theeffect.com.netbios-dgm > 192.168.0.255.netbios-dgm:
>> NBT UDP PACKET(138) Res=0x0 ID=0x7279 IP=192.168.0.255 Port=138 Length=213
-Res2=0x0
SourceName=COMET NameType=0x00 (Workstation)
DestName=THENETFFECT NameType=0x1E (Browser Server)
```

## Windows 命名服务 (WINS) 第 34 章

```
SMB PACKET: SMBtrans (REQUEST)
SMB Command = 0x25
Error class = 0x0
Error code = 0
Flags1 = 0x0
Flags2 = 0x0
Tree ID = 0
Proc ID = 0
UID = 0
MID = 0
Word Count = 17
TotParamCnt=45
TotDataCnt=0
MaxParamCnt=0
MaxDataCnt=0
MaxSCnt=0
TransFlags=0x0
Res1=0x0
Res2=0x0
Res3=0x0
ParamCnt=0
ParamOff=45
DataCnt=0
DataOff=86
SCnt=5
Data: (6 bytes)
[000] 01 00 01 00 02 00
Name=MAILSLOT|BROWSE
BROWSE PACKET
BROWSE PACKET:
Type=0xF (LocalMasterAnnouncement)
UpdateCount=0x0B6
Res1=0xFC
AnnounceInterval=10
Name=COMET NameType=0x0 (Workstation)
MajorVersion=0x4
MinorVersion=0x2
ServerType=0xC9A03
ElectionVersion=0xA10
BrowserConstant=0xAA55
Data: (13 bytes)
[000] 53 61 6D 62 61 20 53 65 72 76 65 72 20
```

Samba 服务端。

```
(ttl 64, 29192)
10:14:50.596489 galahad.theeffect.com.netbios-ns -> comet.theeffect.com:1175:
>>> NBT UDP PACKET(137): QUERY; RESPONSE; UNICAST
TrID=0x6903
```

## 高级 Samba

### 列表 34.2 继续

```
OpCode=0
NmFlags=0x58
Rcode=0
QueryCount=0
AnswerCount=1
AuthorityCount=0
AddressRecCount=0
```

```
ResourceRecords:
Name='a_MSBROWSE_a NameType=0x01 (Unknown)
ResType=0x20
ResClass=0x1
TTL=25900
ResourceLength=6
ResourceData=
AddrType=0xb000
Address=192.168.0.3
```

```
(ttl 64, 29192)
19:14:50.596341 comet.theeffect.com.netbios-dgm > 192.168.0.255.netbios-dgm:
>>> NBT UDP PACKET(138) Res=0x1 ID=0x7279 IP=192.168.0.255 Port=138 Length=206
Res2=0x0
```

```
SourceName=COMET
DestName=a_MSBROWSE_a NameType=0x01 (Unknown)
Workstation
SMB PACKET: SMBtrans (REQUEST)
SMB Command = 0x25
Error code = 0x0
Flags = 0x0
Flags2 = 0x0
Tree ID = 0
Proc ID = 0
UID = 0
MID = 0
Word Count = 17
TotParamCnt=45
TotDataCnt=0
MaxParamCnt=0
MaxDataCnt=0
MaxSCnt=0
TransFlags=0x0
Res1=0x0
Res2=0x0
Res3=0x0
ParamCnt=0
ParamOff=45
DataCnt=0
DataOff=86
SCnt=5
Data: (6 bytes)
[000] 01 00 01 00 02 00
Name=MAILSLOT|BROWSE
BROWSE PACKET
BROWSE PACKET:
Type=0xF (LocalMasterAnnouncement)
UpdateCount=0x0B6
Res1=0xFC
AnnounceInterval=10
Name=COMET NameType=0x0 (Workstation)
MajorVersion=0x4
MinorVersion=0x2
ServerType=0xC9A03
ElectionVersion=0xA10
BrowserConstant=0xAA55
Data: (13 bytes)
[000] 53 61 6D 62 61 20 53 65 72 76 65 72 20
```

## Windows 命名服务 (WINS) 第 34 章

```
SUCnt=3
Data: (6 bytes)
[000] 01 00 01 00 02 00
Name=MAILSLOT|BROWSE
BROWSE PACKET
BROWSE PACKET:
Type=0xF (LocalMasterAnnouncement)
UpdateCount=0x0B6
Res1=0xFC
AnnounceInterval=10
Name=THENEFFECT NameType=0x0 (Workstation)
MajorVersion=0x4
MinorVersion=0x2
ServerType=0x8001000
CommentPointer=0xAA55
ServerName=COMET (ttl 64, 29193)
```

如你所示，通过 SMB 增强型 `tcpdump`，每个 SMB 数据包都被拆解并显示所有可用数据，这让你能够更好地观察流量去向，并更快地识别网络上发生的任何问题。

### 触发 NetBIOS 名称解析

在客户端获取浏览列表并在连接其他网络资源之前，你可以看到 NetBIOS 名称解析的作用。在客户端实际完成名称解析后，实际的连接和数据传输将通过 TCP/IP 连接进行，不再需要广播。客户端对名称解析也有有缓存，因此并非每次名称尝试都会调用广播或 WINS 解析。

总而言之，浏览和连接尝试会触发名称解析，使用此操作的最佳方法是进行浏览和连接。在 Samba 服务器上，可以使用 `nslookup` 和 `smclient` 等工具完成。在 Windows 计算机上，可以使用 DOS 提示符中的 `Network Neighborhood` 或 `view` 命令触发相同操作。

### 切换广播

在看到广播请求产生的流量后，你可能希望看到无需为每个名称请求进行广播所节省的。在 Samba 服务器上，你可以通过更改 `smb.conf` 文件中的 `name resolve order` 参数来实现这一点。通过完全移除广播选项，可以确保查找仅针对 WINS 或通过 DNS 或 LMHOSTS 进行。在 Windows 计算机上，可以通过使用 WINS 甚至使用临时 LMHOSTS 设置测试配置来触发非广播解析。这两者中的任何一种都应该能大幅减少广播网络流量，并为你提供配置网络使用 WINS 解析的动力。

### name resolve order

Samba 提供了一种机制，用于设置各种名称解析方法的顺序。这也可以用于从考虑范围内完全移除一个或多个方法。对于灵活性和高效利用资源来说这是一个重要点。例如，如果你处于一个没有 DNS 的隔离局域网中，你可以在 `smb.conf` 文件的 `name resolve order` 中移除 `host` 选项，这样你的 `/etc/hosts` 文件永远不会被查询。

此选项的默认值为：

`name resolve order = lmhosts wins broadcast`

### lmhosts

设置此选项可以使用 LMHOSTS 文件进行名称解析。对于较小且通常不变的网络，这可能是最简单的名称解析方法。此外，它允许设置 NetBIOS 特有的 `name_type` 信息，这对于 NetBIOS 网络上的名称解析至关重要。

### host

设置此选项可以使用 `/etc/hosts` 和 DNS 进行名称解析，取决于 TCP/IP 名称解析的本地设置。也就是说，如果相关的 `/etc/nwitch.conf`、`/etc/resolv.conf` 或 `/etc/hosts` 允许，可以使用 DNS 或 `/etc/hosts` 进行 NetBIOS 名称解析。如果 NetBIOS 和 DNS 主机名相同，这种方法非常有用。然而，这种方法没有提供包含 NetBIOS `name_type` 信息。使用 `host` 解析会丢失某些信息。

### wins

此选项启用 WINS 名称解析。为了让 WINS 实际工作，必须填写 `wins server` 或 `support` 参数。

### bcast

此选项启用 NetBIOS 请求的广播解析。有了此项，Samba 将对直接连接的网络进行广播。

### WINS 和 DHCP

你可能认为 Windows 产品中动态主机配置协议 `DHCP` 将为网络管理员带来巨大的收益。这确实是一个承诺：一种相对简单且集中的定义机器信息的方法；当服务器和资源更改时，无需在工作站进行重新配置。尽管存在问题，尽管有使用 DHCP 的充分理由，许多人怀疑这是否可行或至少值得。事实是，它并没有像人们想象的那样不可能或困难。关键在于客户端和服务器都要设置正确。确保你的 NetBIOS 名称是唯一的。

### 列表 34.3 Sample dhcpd.conf

```
subnet 192.168.0.0 netmask 255.255.255.0 {

  # default gw

  option routers 192.168.0.1;

  # network config

  option subnet-mask 255.255.255.0;

  option broadcast-address 192.168.0.255;

}
```

# LISTING 34.3 继续

```
# DNS 域名和服务器

option domain-name "theneteffect.com";

option domain-name-servers 192.168.0.100;

# .50 - .75 地址供 DHCP 客户端可用

range 192.168.0.50 192.168.0.75;

# 6 小时

default-lease-time 21600;

# 12 小时

max-lease-time 43200;

# SMB 特定设置 -

# WINS 服务器

option netbios-name-servers 192.168.0.100;

option netbios-dd-server 192.168.0.100;

option netbios-node-type 8;
```
