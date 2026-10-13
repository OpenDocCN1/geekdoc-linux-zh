
Whois Server: `whois.networksolutions.com`

Referral URL: `http://www.networksolutions.com`

Name Server: `NAMESERVER3.CONCENTRIC.NET`

Name Server: `NAMESERVER1.CONCENTRIC.NET`

Name Server: `NAMESERVER2.CONCENTRIC.NET`

Updated Date: 05-nov-2001

>>> Last update of whois database: Tue, 19 Mar 2002 05:21:50 EST <<<

[whois.networksolutions.com]

Registrant:

Concentric Network Corporation (CNC6-DOM)

1400 Parkmoor Avenue

San Jose, CA 95126-3429

Domain Name: CNC.NET

```
Administrative Contact:
Schairer, David R (DRS9) nja1@CONCENTRIC.NET
Concentric Network Corp.
1400 Parkmoor Ave
Cupertino, CA 95014
(408) 817-2800 (800) 745-2747 ext. 2800 (FAX) (408) 817-2630
Technical Contact:
DNS & IP ADMIN (DIA-ORG) hostmaster@CONCENTRIC.NET
Concentric Network Corporation
1400 Parkmoor Avenue
San Jose, CA 95126-3429
(408) 817-2800
Fax: (408) 817-2630
Billing Contact:
XO Communications, Hostmaster (CNCXCH-ORG) hostmaster@XOHOST.COM
XO Communications
1400 Parkmoor Ave
San Jose, CA 95126
408-817-2800
Fax: 408-817-2810

Record last updated on 02-Mar-2001.
Record expires on 06-Mar-2004.
Record created on 05-Mar-1997.
Database last updated on 18-Mar-2002 22:31:00 EST.

Domain servers in listed order:
NAMESERVER3.CONCENTRIC.NET 206.173.119.72
NAMESERVER2.CONCENTRIC.NET 207.155.184.72
```

Concentric Networks 是一家总部位于北加利福尼亚的大型 ISP。

- 3. 我们给他们发一封电子邮件，但唉，我并不期望得到任何有意义的回复：

```
# mail -s "One of your customers was trying to hack into my system"
abuse@cnc.net

Hello. I have tracked backward and found that one of the computers in your domain (w153.z208037077.nyc-ny.dsl.cnc.net) was trying to hack into my Linux server. In the "/var/log/secure" log file, I find the following message from 'sshd':

Mar 10 10:22:14 staging sshd[12114]: Did not receive identification string

from 208.37.77.153.
```

对那个 IP 地址进行反向查找会得到：
`153.77.37.208.in-addr.arpa.` domain name pointer `w153.z208037077.nyc-ny.dsl.cnc.net`.

> 能否请您在您的使用日志中反向追查，确定指定 IP 地址 `208.37.77.153` 对应的是哪台计算机，并找出元凶？
> 不用说，我不希望有人对我的服务器进行端口扫描！
> 
> 感谢您在这件事上提供的帮助。
> 
> Dave Taylor
> taylor@intuitive.com

- 4. 大约 15 分钟后，我们收到以下内容：

原始邮件收到时间为 2002 年 3 月 19 日（星期二）13:46:52 -0500（EST）

```
.... The following addresses had permanent fatal errors ....

(expanded from: <abuse@cncx.net>)

.... Transcript of session follows ....

550 abuse@cncx.net... Host unknown (Name server: cncx.net: host not found)
```

哦，算了，至少我们知道了如何在日志文件中反向追查，而且至少我们尝试过了……

有人试图探测你的端口并不罕见：实际上，用 shell 编程写一个“端口扫描器”只需五分钟，它会选定一个 IP 地址，然后查看哪些互联网服务（如果有）正在监听。一旦确定之后，就有现成的工具可以利用特定服务的“漏洞”尝试闯入。

如果这听起来有些令人沮丧，那也合情合理。为了安全，你能做的最好的事情就是确保系统配置正确，密切关注日志文件，配置一个恰当的防火墙，并且保留可靠的备份以防万一。

还有一些关于 Unix 安全的优秀书籍，这里我重点推荐三本：

- `《Linux 黑客大曝光》`（Brian Hatch 等著，McGraw-Hill 出版）很好地解释了黑客为闯入你的系统会尝试做哪些事，不过对如何从一开始就避免问题的介绍则有所欠缺。
- `《实用 Unix 与 Internet 安全》`（Simson Garfinkel 与 Gene Spafford 著，O'Reilly 出版）更具学术性，但却是这一主题的权威参考。
- `《Linux 安全极限》`（Anonymous 著，Sams 出版）是另一个选择。如果这些都不合你意，在 Amazon 或 Barnes & Noble 上快速搜索一下，就能发现不少其他选择。

我们将在最后一小时再次回到安全这个话题。

### httpd 日志文件

还有一个非常值得详细探究的日志文件，它往往是 Unix 服务器的首要用途所在：Web 服务器日志。

市面上有各种不同的 Web 服务器，但最流行的当属 Apache，它是一个免费分发的 HTTP 守护进程，提供了非凡的灵活性、强大的功能和可配置性。几乎每个现代 Unix 发行版都包含它，你也可以在 `www.apache.org` 下载 Apache 发行版。

#### 任务 16.3：探索 httpd 日志文件

本小时我们要考察的最后一个日志文件是 Apache Web 服务器日志文件，实际上是存储在 `/var/log/httpd` 下的一组文件。

- 1. 下面就是该目录下的典型内容：

```
# cd /var/log/httpd
# ls -s
total 984
35 access_log   3 error_log   1 ssl_engine_log   0 ssl_request_log
252 access_log.1   3 error_log.1   0 ssl_mutex.19348   0 ssl_scache.sem
217 access_log.2   44 error_log.2   0 ssl_mutex.4766
141 access_log.3   27 error_log.3   0 ssl_mutex.827
188 access_log.4   44 error_log.4   0 ssl_mutex.641
```

不过，为了让事情更有趣，我们将分析一个更繁忙的 Web 服务器的日志文件，这些日志文件也更大：

```
# ls -s
total 4200
2594 access_log   654 agent_log   33 error_log   919 referer_log
```

- 2. 你想从日志文件中提取的第一条信息是点击次数，事实证明这非常容易：

```
# wc -l access_log
12384 access_log
```
