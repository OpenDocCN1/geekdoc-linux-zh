
```bash
time=$(awk 'BEGIN(sum=0) {sum += $6} END{print sum }' log)
```

```bash
echo -n "Summary of xferlog from"
echo -n $(head -1 log | awk '{print $1, $2, $3, $4, $5}')
echo - to $(tail -1 log | awk '{print $1, $2, $3, $4, $5}')
echo -n "bytes in: ${nicenum} bytesin"
echo -n "bytes out: ${nicenum} bytesout"
echo -n "transfer time: ${time} seconds"
```

```bash
accessmode=$(awk 'print $13' log | sort -u)
extract "a" "Anonymous Access"
extract "g" "Guest Account Access"
extract "r" "Real User Account Access"
```

```bash
echo 0
```

# 工作原理

在`xferlog`中，入字节的总数可以通过提取方向为`"i"`的行并累加第八列数据来计算。输出字节在同一列中，但对应方向为`"o"`的情况。

```bash
bytesin=$(awk 'BEGIN(sum=0) $12="i" {sum += $8} END{ print sum }' log)
bytesout=$(awk 'BEGIN(sum=0) $12="o" {sum += $8} END{print sum }' log)
```

讽刺的是，连接越慢，连接时间就越准确。在快速网络上，较小的传输被记录为耗时几秒钟，显然每次成功的传输都比这要长。

可能存在三种访问模式：`a`是匿名，`g`是使用访客账户的用户（通常受密码保护），`r`是真实用户或普通用户。在匿名和访客用户的情况下，帐户值（第14）是用户的密码。匿名连接的人被其FTP程序要求指定其电子邮件地址作为密码，然后该地址会被记录并可以进行分析。

在这些`xferlog`输出流中，最重要的条目是那些访问模式为匿名且方向为`i`的条目，这表示该条目是一个上传列表。如果你允许匿名连接，并且无论是有意还是无意地留了一个可写目录，那么这些匿名上传条目将是你能够看到脚本小子（script kiddies）、破解黑客（warez hackers）和其他声名狼藉的人正在利用你服务器的地方。如果条目列出了上传到你服务器的文件，只要该文件是无害的，就需要立即检查。此测试发生在`extract`中的以下语句中：

```bash
awk '$13 == "a" && $12 == "o" { print $9 } | sort | uniq -c | head -10 | sed 's/\/// > $tmp
```

在这个相当复杂的`awk`调用中，我们正在检查字段13是否匹配访问代码（因为`extract`被调用为"Anonymous Access"），并且字段12表示这是一个上传。如果这两个条件都成立，则处理字段9的值，即文件名。

如果你正在运行FTP服务器，这绝对是一个每周（或每日）的`cron`任务。

# 运行脚本

如果不带参数调用，该脚本尝试运行并分析标准日志。如果不是正确的日志，可以在命令行指定不同的文件名。

# 结果

结果取决于传输日志的格式。如果是简略形式，会生成一些基本的统计数据并脚本退出：

```text
Abbreviated ftpd xferlog from Aug 1 04:20 to Sep 1 04:07
bytes in:215300253
bytes out:30590
```

如果遇到标准格式的`xferlog`，可以通过脚本获取更多的信息：

```text
Summary of xferlog from Mon 1 5:03:11 2003 to Tue 1 17:38:50 2003
bytes in:675840
bytes out:98488
transfer time:11 seconds
```

匿名访问
普通账号 (输入密码) 值：

```text
1 taylor@intuitive.com
1 john@doe
files downloaded from server: /tmp/
files uploaded to server: /tmp/Warez.txt
```

用户访问
访问服务器的用户：

```text
7 rufus
2 taylor
files downloaded from server: /pub/AllFiles.tgz
```

安全警告！你注意到有人使用匿名FTP上传了一个名为`/tmp/Warez.txt`文件吗？这不是你想要的授权软件副本。看到这个，我立即进入我的FTP并删除了该文件。

# 监控网络状态

Unix中最令人困惑的管理单元之一是`netstat`，因为它提供了大量关于网络吞吐量和性能的有用信息。使用`-s`标志，`netstat`输出关于你计算机上每个协议的信息，包括TCP、UDP、ICMP、IPSec。对于典型配置来说，这些协议大部分是无关的；要检查的协议是TCP。此脚本分析协议流量，确定失败率，并在任何值超出范围时发出警告。

作为网络性能的快照是有用的，但分析数据的更好方法是查看趋势。如果系统有1.5%的丢包，并且在过去的三天内速率跳升到7.8%，说明出现了问题，需要更详细的分析。

结果，脚本分为部分。第一部分是一个每10到30分钟运行一次的短脚本，在日志文件中记录关键统计。第二部分解析日志文件并报告性能以及随时间增加的异常或其他值。某些Unix版本无法运行此脚本。Linux和Unix版本的`netstat`命令输出格式存在差异。对于其他Unix，更改应该是简单的（检查日志文件以确定是否获得了有意义的结果以确定是否需要调整）。

# 代码

```bash
#!/bin/sh
# getstats - 每 'n' 分钟获取 netstat 值（通过 crontab）
logfile=/var/log/netstat.log
temp="tmp/getstats.tmp"
trap "/bin/rm -f $temp" 0

echo -n time="$(date +%s)"
netstat -s -p tcp $temp

sent=$(grep 'packets sent' $temp | cut -d ' -f1 | sed 's/[[:digit:]]//g')
resent=$(grep 'transmitted' $temp | cut -d ' -f1 | sed 's/[[:digit:]]//g')
received=$(grep 'packets received' $temp | cut -d ' -f1 | \
sed 's/[[:digit:]]//g')
dumpacks=$(grep 'duplicate acks' $temp | cut -d ' -f1 | \
sed 's/[[:digit:]]//g')
outerford=$(grep 'out-of-order packets' $temp | cut -d ' -f1 | \
sed 's/[[:digit:]]//g')
connectreq=$(grep 'connection requests' $temp | cut -d ' -f1 | \
sed 's/[[:digit:]]//g')
connectacc=$(grep 'connection accepts' $temp | cut -d ' -f1 | \
sed 's/[[:digit:]]//g')
retrout=$(grep 'reransmit timeouts' $temp | cut -d ' -f1 | \
sed 's/[[:digit:]]//g')

echo -n="$sent=$sent;res=$resent;rec=$received;dup=$dumacks"
echo -n="$out=$outerford;creq=$connectreq;cacc=$connectacc"
echo -n="$retrout"
)) $logfile

exit 0
```

第二个脚本分析`netstat`历史日志：

```bash
#!/bin/sh
# netperf - 分析 netstat 运行性能日志，识别重要的结果和趋势。

trap /bin/rm -f $awktmp $stats" 0

if [ ! -r $log ]; then
echo "Error: can't read netlog file $log" >&2
exit 1
fi

# 首先，报告日志文件中最新条目的基础统计信息...
```
