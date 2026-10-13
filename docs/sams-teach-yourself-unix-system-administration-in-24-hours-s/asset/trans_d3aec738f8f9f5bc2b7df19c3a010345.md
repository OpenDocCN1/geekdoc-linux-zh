
“connect from”消息来自TCP Wrapper（尽管它标识的是被请求的服务而非自身），而“connection”和“LOGIN REFUSED”消息则来自ftpd本身。

- 2. 配置TCP Wrapper相当容易，尤其是与inetd服务结合使用时：只需创建/etc/hosts.allow或/etc/hosts.deny文件，然后列出特定服务、主机，以及可选的、在查询该服务时应运行的命令。

例如：

```
# cat /etc/hosts.allow
# /etc/hosts.allow
#
# Allow telnet from anywhere
telnetd: ALL
# ftp can only be from within my own subnet:
ftp: LOCAL, dsidesigns.com, 137.44.
```

这指定了所有主机都可以使用telnetd服务，而只有本地主机（不含点的主机名）、.dsidesigns.com域内的主机（注意该域名开头的点；如果没有这个点，就只会进行精确匹配），以及IP地址前两个八位组为137.44.的主机，才可以使用ftpd服务。

与之相比，再来看一个拒绝文件：

```
# cat /etc/hosts.deny
# /etc/hosts.deny
#
# Reject all hosts with suspect hostnames
ALL: PARANOID
```

这个巧妙的TCP Wrapper技巧让我们能够自动拒绝来自以下系统的所有连接：这些系统的主机名与IP地址不匹配（通过反向IP查询；更多细节请参阅上一小时的讨论），或者其IP地址没有关联的主机名。

实际上，推荐的配置是在hosts.deny文件中设置ALL:ALL，然后在hosts.allow文件中显式允许某些主机使用特定服务。

- 3. 关于TCP Wrapper，没有太多可说的了，只是如果你发现相应的日志文件中没有任何条目，那很可能是你把syslog的日志记录范围配置得过于精简。为了试验，在/etc/syslog.conf文件中添加以下内容：

```
*.* /dev/console
```

一旦你向syslogd程序发送SIGHUP（挂断信号），这会让所有交给syslog的消息也显示在系统控制台上。这样产生的输出非常有意思。

![](img/5ced0c78d748bd190e9027e5549a3622_397_0.png)

> 非常值得研究一下syslog的工作原理。先从阅读syslog手册页开始；然后再阅读syslog.conf(5)手册页，并查看你自己的/etc/syslog.conf文件。

尽管概念简单，但TCP Wrapper程序对系统管理员来说是一大福音，因为它能让你为任何网络服务添加访问控制。没有它，你就得要么开发一套防火墙方案，要么重写服务本身来实现访问控制。

稍后你会看到，xinetd的一个优势是它内置了类似TCP Wrapper的功能。

## 超级inetd：xinetd

xinetd最初发布于Red Hat Linux，它是inetd更复杂的“老大哥”，虽然二者共享相同的概念基础，但它们的差异几乎达到了两个程序所能达到的最大程度。尽管xinetd尚未被广泛使用，它也已包含在Mandrake Linux中。可以预期它会随着时间迁移到其他平台，因为它是inetd的一个明智替代品。

正如你所看到的，在inetd中，有一个单独的配置文件控制着哪些服务被启用，以及定义它们在系统上运行方式的参数。

相比之下，xinetd有一个存放各个独立配置文件的目录，每个服务一个文件，以及一个集中的主配置文件，用来定义所有服务的默认设置。在大多数情况下，你的系统会使用其中一种——无论哪种，我都建议坚持默认配置。

### 任务19.3：使用xinetd

实际上，如果你想象把inetd.conf文件中的每一行分别放到各自独立的文件中，并把每一行的每个字段写成“字段名 = 值”的格式，那么你就能非常接近xinetd的格式了。

- 1. 主配置文件是`/etc/xinetd.conf`：

```
# cat /etc/xinetd.conf
#
# Simple configuration file for xinetd
#
# Some defaults, and include /etc/xinetd.d/
defaults
{
    instances    = 60
    log_type     = SYSLOG authpriv
    log_on_success = HOST PID
    log_on_failure = HOST
    cps = 25 30
}

includedir /etc/xinetd.d
```

这演示了xinetd配置的基本结构。先列出服务，然后在花括号内以“名称 = 值”对的形式设置一组参数。在此例中，特殊的defaults服务使得某些参数能够对所有启用的服务进行设置。

这里的具体设置包括：instances（服务允许的最大并发连接数）、log_type（使用syslog，采用authpriv设施——见本小时稍早关于syslog的讨论）；在连接成功时，它会记录HOST和PID，而在失败时只记录HOST。最后，还有一个故障安全连接速率参数，它规定服务每秒最多接受25个连接，如果速率超过这个值，该服务将被完全关闭30秒。

最后一行最重要：它表明其余配置信息位于/etc/xinetd.d目录下的各个独立文件中。

![](img/5ced0c78d748bd190e9027e5549a3622_398_0.png)

> 在xinetd.conf文件中可以指定相当多的参数。我们不会在这里全部列出，而是重点介绍最重要的部分。完整列表请参阅xinetd.conf(5)手册页。

- 2. 为了继续探索，我们将注意力转向includedir目录：

```
# cd /etc/xinetd.d
# ls -s
total 18
1 chargen      1 echo        1 rexec       1 sgi_fam      1 time-udp
1 chargen-udp  1 echo-udp    1 rlogin      1 talk         1 wu-ftpd
1 daytime      1 finger      1 rsh         1 telnet
1 daytime-udp  1 ntalk       1 rsync       1 time
```

乍看之下，通过xinetd启用的服务相当多，但进一步查看一个特定的配置文件——本例中是telnet——就会发现情况并不像看上去那么糟：

```
# cat telnet
# default: on
# description: The telnet server serves telnet sessions; it uses
# unencrypted username/password pairs for authentication.
## CHANGED TO DISABLE TELNET 12/2001

service telnet
{
    flags         = REUSE
    socket_type   = stream
    wait          = no
    user          = root
    server        = /usr/sbin/in.telnetd
    log_on_failure += USERID
    disable       = yes
}
```

这些具体标志大多应该能让你联想到inetd.conf文件的格式，包括socket_type、wait、user和server。flags让你可以指定众多不同底层网络选项中的一种。在此例中，REUSE意味着该服务设置了一个特定的地址复用标志（更多细节请参阅xinetd.conf(5)手册页。注意，这属于非常底层的选项！）。

这个服务定义中的log_on_failure参数展示了一个很棒的特性。注意它使用了+=，这意味着除了在失败时要记录的默认值之外，telnet服务还会额外记录USERID。表19.1列出了在给定连接成功或失败时可供记录的参数。

**表19.1：xinetd记录的信息**

| 值 | 使用时机 | 说明 |
|---|---|---|
| ATTEMPT | 失败时 | 记录曾尝试但失败的事实 |
| DURATION | 成功时 | 记录服务会话的持续时间 |
| EXIT | 成功时 | 记录服务器退出时间 |
| HOST | 成功或失败时 | 远程主机地址 |
| PID | 成功时 | 服务器应用程序的进程ID |
| RECORD | 失败时 | 尽可能多地记录来自远端的信息 |
| USERID | 成功或失败时 | 远程主机的用户ID（如果可用） |

最后，telnet配置清单中的最后一行也许是最重要的。disable参数可以是yes或no。如果是yes，xinetd无法启动该服务，连接尝试将会失败。如果设为no，则该服务被启用。

- 3. disable参数的使用导致了xinetd最大的问题——很难搞清楚哪些服务被启用、哪些被禁用。
