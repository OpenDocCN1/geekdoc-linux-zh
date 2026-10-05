

# 第 10 章 测试 Sendmail

当使用 -bt 选项运行 `sendmail` 命令时，看到的详细信息等同于调试级别 21.1。然而，从系统管理员的角度来看，类别和级别数字并不重要。实际上，调试级别仅仅是任意的数字，其中几个会产生有用的信息。

某些调试级别是有用的，例如类别 0（打印关于 Sendmail 版本信息的类别）是很有用的。我们在第 6 章中看到过调试级别 0.1 的示例。我有时使用的另外两个调试 0 级别是 0.4 和 0.10。列表 10.5 显示了调试级别 0.10 打印的信息。

# 列表 10.15 调试级别 0.10 的输出

```
[root]# sendmail -bt -d010
Version 8.11.0
Compiled with: MAP_REGEX MATCHGEOS MIME7TO8 MIME8TO7 NAMED_BIND
NETINET NETUNIX NEWDB NIS QUEUE SASL SCAN SFIO
SMTP STARTTLS USORDERB
OS Defines: HASCHOWN HASFLOCK HASGETTABLESIZE HASASINITGROUPS
HASSTAT RANDOM HASSETREUID HASSETRLIMIT HASIDIDHASHASBUFWAITWAIT
UROMDEVDEVUNUN US_SIGLONGJMP

 file: /etc/sendmail.conf
Pid file: /var/run/sendmail
canonical name: wren.irds..

UUCPenameename:
enameename..

....: [172.11.12.3]
========== SYSTEM IDENTITY (after readcf) ==========
(short domain name) Sw = wren
(canonical name) Sj = wrenfoirds.org
(subdomain name) Sm = foirds.org
(node name) Sk = wrenfoirds.org
```

调试级别 0.10 用于列表 10.15，因为调试级别是累积的。0.10 生成的包含 0.1 和 0.4 会显示的所有三个调试级别的信息。级别 0.1 显示版本号、Sendmail 选项和系统身份。调试级别 0.4 显示来自网络接口的名称和地址。在“canonical name”和“UUCP nodename”标题下列出了这些内容。级别 0.10 打印编译期间使用的系统定义，以及配置文件和 PID 文件的默认路径。调试级别 0.1 是用的，因为它提供了 Sendmail 选项和系统身份。

调试级别 35.9 很有趣，因为它显示了所有的 sendmail.cf 变量以及它们被赋值的值。列表 10.16 显示了调试 35.9 输出的信息。

# 列表 10.16 调试级别 35.9 的输出

```
[root]# sendmail -bt -d35.9
define(deliveryMode as b)
define(* as $)
... Many lines deleted
define(8 as $)
define(9 as $)
define(n as MAILER-DAEMON)
define(v as 8.11.0)
define(w as wrenfoirds.org)
define(j as wrenfoirds.org)
define(m as foirds.org)
define(k as wrenfoirds.org)
define(b as Sat, 4 Nov 2000 09:33:49 -0500)
define(load_avg as 0)
define(opMode as t)
define(w as wren)
define(S as j)
define(R as j)
define(H as j)
define(M as j)
define(n as MAILER-DAEMON)
define(Z as 8.11.0)
define(deliveryMode as b)
define(_ as root@localhost)
define(deliveryMode as i)
define(i as e4755)
```

维护健康的服务器

注意：列表 10.16 删了一些行使其长度合理。要查看完整列表，请在你的系统上运行 `sendmail -bt -d35.9`。我倾向于使用 `-v` 命令一次查看一个变量。我发现完整列表令人 overwhelming。我更倾向于有条理地工作，一次处理一个变量，并参考以记住该变量的作用（sendmail.cf 变量在附录 C“Sendmail 变量、选项和标志”中列出并描述）。但调试级别 35.9 对于那些能够区分麦子和杂质的人很有用，它的优势是显示了 `i` 变量的实例化（该变量将用于创建队列文件）。此外注意 DeliveryMode 从后台模式重新定义，这在初始化期间也会使用。DeliveryMode 并不是一个特定的变量。它也可以被视为选项。调试级别 37.1 与 35.9 类似，但显示的是值而不是变量。列表 10.17 显示了我们的选项。

# 列表 10.17 调试级别 37.1 的输出

```
[root] sendmail -bt -d37.1
setoption SevenBitInput(7)=False
setoption EightBitMode(8)=pass
setoption AliasWait(a)=10
setoption AliasFile(A)=/etc/aliases
setoption MinFreeBlocks(b)=100
setoption Blank(c)=False
setoption DeliveryMode(d)=background
setoption AutobuildAliases(D)=
setoption TempFile(F)=0600
setoption HelpFile(H)=/etc/mail/helpfile
setoption MimeErrors(J)=True
setoption ForwardPath(J)=~/forward.forward
setoption ConnectionCacheSize(K)=2
setoption ConnectionCacheTimeout(K)=m
setoption HostStatusDirectory(q)=/var/state/sendmail
setoption UseErrors(l)=False
```

# 使用调试级别

setoption LogLevel(L)=9
setoption CheckAliases(n)=False
setoption OldStyleHeaders(o)=True
setoption DaemonPortOptions(O)=Name=MTA
Daemon flags: setoption DaemonPortOptions(O)=587, Name=MSA, M=E
Daemon MTA flags: setoption PrivacyOptions(p)=warnings
Daemon MTA flags: setoption QueueDirectory(Q)=/var/spool/queue
setoption Timeout(r).connect=1
setoption Timeout(r).queueturn=4h
setoption SuperSafe(s)=True
setoption StatusFile(S)=/var/log/sendmail.st
setoption DefaultUser(u)=12
setoption DatabaseSpec(U)=/mail/user.db
setoption TryNull(w)=true
setoption SmtpGreetingMessage(X)=$ Sendmail v/Z
setoption UnixFrom(g)=sd
setoption OperatorChars(y)=,:%@!"/
setoption DontProbeInterfaces(O)=true
setoption HoldExpensive(c)=F
setoption DeliveryMode(d)=

调试级别 35.9 比 37.1更有趣，因为它显示了变量的 l。但调试级别 37.1 比 35.9更有用。虽然可以使用 `-v` 命令单独检查变量，但没有用于检查单个选项的地址测试命令。为了查看已设置的选项以及它们要运行的值，如果你的配置问题与选项设置有关，这是一个很好的检查方法。

![](img/b082498451dba0cf2907c854c83_317_0.png)

