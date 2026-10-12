

enterprises.ucdavis.255.12 = "Sep 1 20:05:17 scorates chat[1002]: abort on (Login incorrect)*"
enterprises.ucdavis.255.13 = "Sep 1 20:05:17 scorates chat[1002]: send (ATZ%)*"
enterprises.ucdavis.255.14 = "Sep 1 20:05:17 scorates chat[1002]: expect (OK)*"
enterprises.ucdavis.255.15 = "Sep 1 20:06:02 scorates pppd[100]: Connect script failed*"
enterprises.ucdavis.255.16 = "Sep 1 20:06:02 scorates chat[1002]: alarm*"
enterprises.ucdavis.255.17 = "Sep 1 20:06:02 scorates chat[1002]: failed*"
enterprises.ucdavis.255.18 = "Sep 1 20:06:03 scorates pppd[100]: Exit.*"
enterprises.ucdavis.255.19 = "Sep 1 20:06:04 scorates pppd[101]: pppd 2.3.3 started by root, uid 0"

enterprises.ucdavis.255.20 = "Sep 1 20:06:04 scorates ifup-ppp: pppd started for ppp0 on /dev/modem at 115200"

enterprises.ucdavis.255.21 = "Sep 1 20:06:05 scorates chat[1012]: abort on (BUSY)*"
enterprises.ucdavis.255.22 = "Sep 1 20:06:05 scorates chat[1012]: abort on (ERROR)*"
enterprises.ucdavis.255.23 = "Sep 1 20:06:05 scorates chat[1012]: abort on (NO CARRIER)*"
enterprises.ucdavis.255.24 = "Sep 1 20:06:05 scorates chat[1012]: abort on (NO DIAL TONE)*"
enterprises.ucdavis.255.25 = "Sep 1 20:06:05 scorates chat[1012]: abort on (Invalid Login)*"
enterprises.ucdavis.255.26 = "Sep 1 20:06:05 scorates chat[1012]: abort on (Login Incorrect)*"
enterprises.ucdavis.255.27 = "Sep 1 20:06:05 scorates chat[1012]: send (ATZ%)*"
enterprises.ucdavis.255.28 = "Sep 1 20:06:05 scorates chat[1012]: expect (OK)*"
enterprises.ucdavis.255.29 = "Sep 1 20:06:50 scorates chat[1012]: alarm*"
enterprises.ucdavis.255.30 = "Sep 1 20:06:50 scorates chat[1011]: failed*"
enterprises.ucdavis.255.31 = "Sep 1 20:06:50 scorates pppd[101]: Connect script failed"

enterprises.ucdavis.255.32 = "Sep 1 20:06:51 scorates pppd[101]: Exit.*"
enterprises.ucdavis.255.33 = "Sep 1 20:06:51 scorates pppd[100]: pppd 2.3.3 started by root, uid 0"

enterprises.ucdavis.255.34 = "Sep 1 20:06:51 scorates ifup-ppp: pppd started for ppp0 on /dev/modem at 115200"

enterprises.ucdavis.255.35 = "Sep 1 20:06:52 scorates chat[1025]: abort on (BUSY)*"
enterprises.ucdavis.255.36 = "Sep 1 20:06:52 scorates chat[1025]: abort on (ERROR)*"
enterprises.ucdavis.255.37 = "Sep 1 20:06:52 scorates chat[1025]: abort on (NO CARRIER)*"
enterprises.ucdavis.255.38 = "Sep 1 20:06:52 scorates chat[1025]: abort on (NO DIAL TONE)*"
enterprises.ucdavis.255.39 = "Sep 1 20:06:52 scorates chat[1025]: abort on (Invalid Login)*"
enterprises.ucdavis.255.40 = "Sep 1 20:06:52 scorates chat[1025]: abort on (Login Incorrect)*"
enterprises.ucdavis.255.41 = "Sep 1 20:06:52 scorates chat[1025]: send (ATZ%)*"
enterprises.ucdavis.255.42 = "Sep 1 20:06:52 scorates chat[1025]: expect (OK)*"
enterprises.ucdavis.255.43 = "Nov 2 20:01:02 scorates last message repeated 2 times*"
enterprises.ucdavis.255.44 = "Nov 2 20:01:03 scorates PAM_pwdb[914]: (su) session opened for user news by (uid=0)"
enterprises.ucdavis.255.45 = "Nov 2 20:01:06 scorates PAM_pwdb[914]: (su) session closed for user news"
enterprises.ucdavis.255.46 = "Nov 2 20:01:35 scorates smpd: Connection from 10.0.2.201"
enterprises.ucdavis.255.47 = "Nov 2 20:04:50 scorates last message repeated 2 times"
enterprises.ucdavis.255.48 = "Nov 2 20:06:16 scorates last message repeated 3 times"
enterprises.ucdavis.255.49 = "Nov 2 20:11:40 scorates last message repeated 102 times*"

列表 7.3 中的输出对应于系统消息文件的最后 50 行。如脚本所示，消息文件中的行是从第 79 行开始的 `SnmpGetNext` 函数获取的。第 82 行包含 UNIX `tail` 命令。在此，该命令被调用，输出存储在名为 `data` 的数组（或列表）变量中。当调用此函数时，数组中的其中一行会显示在标准输出上；它对应于 SNMP 调用中引用的 OID 对象。当发出 SNMP 遍历时，它会多次调用此函数，并使用树中下一个对象的 OID。92 到 105 行之间的代码检查 OID 的最后一个数字并将其加一（第 101 行）。接下来，函数显示新的 OID、字符串类型，以及使用 OID 本身作为数组索引从 `tail` 命令输出的一行。`SnmpGet` 函数基本以相同的方式运行；它执行 UNIX `tail` 命令，并使用 OID 作为 `data` 数组中的索引返回消息文件中的其中一行。

关于此脚本可以做几点观察。首先，`SnmpGet` 函数在消息文件的清除方面可以更健壮。例如，它可以定义另一个对象来存储清除发生时的日期和时间信息。这在大型网络环境中肯定会是一个有用的功能。其次，由于 PERL 中的数组元素从零开始，`tail` 命令的输出与 OID 编号并不完全对应。请注意上面的输出中行从 1.3.6.1.4.1.2021.255.0 开始，而不是 1.3.6.1.4.1.2021.255.1。最后，可以修改脚本以不同方式处理硬编码限制和其他相关数据。例如，它会检查代理发送给它的 OID 的范围。这从第 127 行开始显示。复杂的程序在确定 OID 范围时将使用更动态的方法，等等。

## 示例代理配置文件

列表 7.4 显示了一个示例代理配置文件。对于希望部署代理环境以监控某些标准 UNIX 进程至关重要的人来说，这可能是一个良好的起点。此外，配置还包括调用函数以自动限制某些系统进程，从而使系统不会过载。

### 列表 7.4 示例代理配置

```
#
# Sample Configuration
# Monitor these processes..
#

proc_mountd
proc_nfsd
proc_lpsched
#
# Monitor load average above 2.0..
#
load 2
#
# Make sure we have at least 50 MB in root
# and 100 MB in /usr
#
disk /      50000
disk /usr    100000
#
# Execute the following programs to obtain
# output via the UCD mib...
#
exec .1.3.6.1.4.1.2021.255.1 top /usr/bin/top
exec .1.3.6.1.4.1.2021.255.2 ps /bin/ps -e
pass .1.3.6.1.4.1.2021.255.3 /usr/local/perl /etc/snmp/message.pl
```

## 命令行选项

代理提供了许多命令行选项，如表 7.4 所列。由于代理在大多数情况下会在系统启动时自动启动，如果要使其永久生效，则应将其中一些选项更改在启动文件中。然而，其中一些选项只有在命令行中使用时才有意义。

默认情况下，启动 snmpd 时，它使用众所周知的 SNMP 端口 161。如果同一系统上运行其他代理或使用主代理，则必须更改此设置。为此提供了 -p 选项。snmpd 命令将使用此选项，后跟端口号，以侦听传入的 SNMP 请求。

有几个选项可用于协助必须使用代理进行的任何调试工作。-a 选项显示与代理通信的任何系统的 IP 地址，以及日期和时间信息。这对于确认任何配置的 ACL 是否正常工作很有用。当使用选项时，代理将显示如下消息：

```
1999-11-21 16:04:17 Received SNMP packet(s) from 10.0.2.126
```

-d 选项显示发送到代理和从代理接收的 UDP 数据包，并用于帮助检测 SNMP 协议相关问题或其他操作问题。此外，此选项可用于检查 SNMP 客户端应用程序请求的 MIB 对象。下面显示了代理调试输出的示例：

```
GET
  -- system.sysContact.0
   >> system.sysContact.0 = Steve Maxwell
sent 64 bytes to 10.0.2.126:
0000: 30 82 00 3c 02 01 00 04 6f 70 75 62 6c 69 63 34  0.<....public..
0016: 92 00 20 02 04 23 c1 e0 9f 02 01 00 02 01 00 30  ...*.......
0032: 82 00 10 30 82 00 19 06 08 28 60 01 02 01 01 04  ...
0048: 00 00 5d 74 65 76 65 20 4d 61 78 77 65 6c        ...Steve Maxwell
```

在此示例中，代理从 IP 地址为 10.0.2.126 的系统获得 SNMP get 请求。代理显示字符串“...”以指示远程 SNMP 实体请求的内容（在本例中为 sysContact 对象），而“>>”字符串显示代理返回的内容。十六进制输出对应于整个 UDP 数据包，其中包括 community 字符串信息和任何返回的对象。如果您只想要协议事务而不是 UDP 数据包跟踪，请使用 -v 选项。此选项将显示

```
GET
  -- system.sysLocation.0
   >> system.sysLocation.0 = Graphics Lab 11-B
```

这是 SNMP 客户端应用程序请求 sysLocation MIB 对象的结果。

根据 UCD 包中的文档，-q 选项显示更简单的格式，可用于例如自动化代理输出的解析。不幸的是，在测试的代理版本 4 中，此选项似乎没有任何作用。
