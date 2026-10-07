
# # 代理服务器

包过滤防火墙在网络层面处理过滤，而代理服务器则在应用层面工作。包过滤防火墙并不关心是哪个应用程序发送了数据包——它只知道发送该数据包的机器的 IP 地址和目标 IP 地址——但代理服务器会直接从配置好去访问该特定端口的特定代理的应用程序接收数据。例如，Netscape 可能被配置为将所有请求发送给一个代理服务器，该代理服务器将获取请求的页面并将其返回给 Netscape 应用程序。代理服务器还可以维护最近访问页面的缓存，并在访问互联网获取请求的页面前，先检查该页面是否在该缓存中。

代理服务器可以部署在防火墙机器上（拓扑结构与之前图 15.2 中所示相同），部署在防火墙内部的另一台机器上（如图 15.4 所示），或者在既没有防火墙保护、又连接到互联网和局域网的环境中。通常，最好将尽可能少的组件放置在防火墙之外，因此将代理服务器部署在一台受防火墙保护的不同机器上是个好主意。有时，代理会与防火墙结合在一起，如图 15.5 所示。

![](img/10371fe30b7fdac23ef2ef30d5ffe738_411_0.png)

在这种配置中，代理服务器会拦截来自防火墙内部客户端的任何 Web 请求，并对照访问控制列表进行检查，该列表详细说明了必须拒绝访问的站点。如果请求的 Web 页面不在此列表中，请求将正常处理，要么直接通过 Web 发出，要么通过防火墙进行进一步处理。如果请求成功通过防火墙上的 ipchains 或 iptables 过滤，获取的 Web 页面将返回给请求方。如果请求的 Web 页面在控制列表中，请求机器将收到一条消息，表明该 URL 不可访问或无效。许多大型公司都会设置代理服务器，以允许用户访问互联网，同时允许他们监控流量。

与过滤防火墙相比，代理服务器消耗的资源要多得多，因为它会为每个连接它的用户创建一个新进程。如果流量很大，你至少需要一台配备 64MB 内存、两块网卡和 2GB 或更大硬盘的 Pentium II 处理器。这应该能处理大约 50 个并发用户。再次强调，这是应使用的最低配置系统。更常见的是配备 128–264MB 内存、两块网卡和 20–30GB 硬盘的 Pentium III 或 Pentium IV 代理服务器。

代理服务器很有用，但其用途仅限于可用网络服务的一个小子集。代理服务器主要用于 HTTP。Linux 系统可以运行各种各样的网络服务，大多数 Linux 系统默认运行多个服务。关闭你不打算使用的服务是个好主意；每个服务都是一扇可能被扫描开放端口的黑客打开的门。如果使用 inetd（在第 12 章中有介绍），你可以向 /etc/inetd.conf 中对应于你想禁用的任何 inetd 控制服务的每行开头添加一个井号 (#)。对于不在 inetd 控制下的服务，请像使用 chkconfig 这样的工具。

## chkconfig

除了通过 inetd 或类似的超级服务器控制的服务外，许多服务直接运行，连接到端口而不使用超级服务器。你通常可以通过调整它们的启动脚本来关闭这些服务，如第 3 章所述。然而，更常见的是使用 chkconfig 来关闭它们。chkconfig 的语法如下：

```bash
chkconfig --list [name]
chkconfig --add [name]
chkconfig --del [name]
chkconfig [--level [levels]] [name] [on|off|reset]
```

不带参数的 `chkconfig --list` 命令将列出所有服务及其相应的开启或关闭状态。如果不受 xinetd 或 inetd 管理，服务状态将按运行级别列出。示例见列表 15.10。

### 列表 15.10: chkconfig 输出示例

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|
| syslog | off | off | on | on | on | on | off |
| crond | off | off | on | on | on | on | off |
| netfs | off | off | off | off | off | off | off |
| network | off | off | on | on | on | on | off |
| random | off | off | on | on | on | on | off |
| rawdevices | off | off | off | off | off | off | off |
| xfs | off | on | on | on | on | on | off |
| xinetd | off | off | off | on | on | on | off |
| reconfig | off | off | off | on | on | on | off |
| anacron | off | off | on | on | on | on | off |
| httpd | off | off | on | off | off | off | off |
| apmd | off | off | on | off | off | off | off |
| atd | off | off | off | off | off | off | off |
| named | off | off | on | on | off | off | off |
| keytable | off | on | on | on | on | on | off |
| gpm | off | off | on | on | on | on | off |
| ipchains | off | off | on | on | on | on | off |
| pcmcia | off | off | on | off | off | off | off |
| kdump | off | off | on | on | on | on | off |
| kudzu | off | off | off | on | on | on | off |
| linuxconf | off | on | on | on | on | on | off |
| lpd | off | off | on | on | on | on | off |
| nfs | off | off | off | off | off | off | off |
| nfslock | off | off | off | off | off | off | off |
| sshd | off | on | on | on | on | on | off |
| identd | off | off | on | on | on | on | off |
| portmap | off | off | off | on | on | on | off |
| ypsfrd | off | off | off | off | off | off | off |
| rstated | off | off | off | off | off | off | off |
| rusersd | off | off | off | off | off | off | off |
| rwall | off | off | off | off | off | off | off |
| rwhod | off | off | off | off | off | off | off |
| smb | off | off | off | off | off | off | off |
| sendmail | off | off | on | on | on | on | off |
| rhnsd | off | off | on | on | on | on | off |
| yppbind | off | off | off | off | off | off | off |
| yppasswdd | off | off | off | off | off | off | off |

