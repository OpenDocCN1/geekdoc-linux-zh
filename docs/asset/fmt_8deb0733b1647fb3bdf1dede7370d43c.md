
然而，在集群节点上，你不需要修改`/etc/init.d/lpd`脚本。你可以使用 Red Hat 提供的标准版本。当`printconf-backend`脚本运行时（每次带`start`参数调用时），集群节点上的`/etc/printcap`文件会被覆盖。因此，每个集群节点都知道中央打印服务器上有哪些打印机，因为它们列在`/etc/printcap.local`文件中（当然，这是一个指向存储在 NFS 挂载驱动器上的文件的符号链接，所以你只需要修改一次所有即可生效）。每次修改`/etc/printcap.local`文件时，必须重启所有集群节点的`lpd`守护进程。

在中央打印服务器上（使用修改后的`/etc/init.d/lpd`脚本），你始终修改`/etc/printcap`文件，因为`/etc/printcap.local`文件在中央打印服务器未使用。

总结我们刚刚构建的配置：中央打印服务器上的`/etc/printcap`文件包含实际的打印机定义（特定打印机使用的接口、打印机的 IP 地址位置等），而集群节点上的`/etc/printcap.local`文件仅包含让集群节点能够将作业发送到中央打印服务器的信息（与中央打印服务器通信时的网络超时时间、中央打印服务器的主机等）。

## 修改集群节点上的 `/etc/printcap.local` 文件

每个集群节点上的`/etc/printcap.local`文件中的条目如下：

```
# 集群节点上的所有打印机可以使用这些相同的默认值：
.default:
:fifo
:sd=/var/spool/lpd/%P
:lp=%P@centralprintserver
:connect_interval=60
:connect_grade=3
:reuse_addr=true
:send_job_rw_timeout=0
:send_query_rw_timeout=0
:send_try=0
```

```
:retry_econnrefused=true
:retry_nolink=true
:wait_for_eof=true
:connect_timeout=600
:force_localhost
```

然后将每个打印机放在文件`/etc/printcap.local`中默认值之后，条目如下所示：

```
printer1:tc=.default
printer2:tc=.default
printer3:tc=.default
```

其中`centralprinterver`在此示例中是中央打印服务器的主机名（通过 DNS/LDAP/NIS 或每个集群节点上的本地`/etc/hosts`文件解析）。

## 修改中央打印服务器上的 `/etc/printcap` 文件

在 LPRng 中间打印服务器上，`/etc/printcap`条目看起来如下：

+   激光打印机风格的定义列表，它们将使用`"ifhp"`打印机过滤器。

```
.laserjet
:fifo
:filter=/usr/libexec/filters/ifhp
:ifhp=waitend@
:af=acct
:lf=log
:mx=0
:sd=/var/spool/lpd/%P
:sh
```

下列打印机使用了上述`laserjet`定义。

以下是它们的 IP 地址。

```
printer1
:tc=.laserjet
:lp=192.160.0.201%9100
```

```
printer2
:tc=.laserjet
:lp=192.160.0.202%9100
```

```
printer3
:tc=.laserjet
:lp=192.160.0.203%9100
```

当然，你可以在`/etc/printcap`文件的顶部定义多种类型的打印机——除`laserjet`外的打印机类型。由于标准的 Red Hat 发行版使用了稍微修改过的 LPR 系统，你可能会看到对`"printconf-tui"`（tui 代表文本界面）和`"printconf-gui"`（在 X 显示下可用的`printconf`图形界面版本）的引用。不要在中央打印服务器上使用这些`printconf`工具。本案例将最后介绍系统管理员使用 LPRng 系统在集群上管理打印作业的日常活动。

## 在中央打印服务器上管理打印作业

随后可以使用`lpc`命令管理打印队列和打印作业，如下：

列出所有打印机及其当前状态：

```
#lpc status all
```

挂起`printer1`上所有等待打印的作业：

```
#lpc hold printer1
```

释放`printer1`上等待打印的作业：

```
#lpc release printer1
```

将打印机置于挂起状态，这样仍可以从集群发送新作业，但中央打印服务器不会将它们发送到打印机：

```
#lpc hold printer1
```

将打印机移出“挂起”状态：

```
#lpc nohold printer1
```

当打印机挂起时，使用以下命令（打印作业不会丢失，但启动处理打印队列中作业的`lpd`守护进程将被杀死）：

```
#lpc kill printer1
```

## 从集群节点管理打印作业

集群节点上的用户可以使用添加的`-S`选项使用相同的命令：

```
#lpc -Centralprinterserver hold printer1
#lpc -Centralprinterserver holdall printer1
#lpc -Centralprinterserver release printer1
#lpc -Centralprinterserver nohold printer1
```

当从集群节点使用带`-S`参数的`lpc`命令时，命令仅影响集群节点上的打印队列（集群节点上的本地打印队列）。在集群节点上对某个打印机执行`hold`命令时，忘记对`lpc`命令使用`-S`参数可能会导致打印机对某些用户停止工作但对并非所有用户有效。发生这种情况时，打印作业不会丢失，集群管理员只需登录到集群节点并释放打印作业即可。

## 在中央打印服务器上创建自定义脚本

LPRng 打印系统的有用功能之一是你可以编写自己的脚本来处理打印作业。脚本可以包含简单的一行：

```
cat /tmp/job
```

此行将获取字符流（通常是 PostScript）并发送到文件`/tmp/job.pid`，其中`pid`是你的自定义脚本在集群服务器上`lpd`守护进程启动时的进程 ID。你可以在脚本中操作文件（`/tmp/job`），执行诸如将作业传真（使用 Ghostscript 程序）或使用`ps2pdf`工具将文件转换为 PDF，并将文件作为二进制大对象（`blob`）存储在 SQL 数据库中。

注意：Windows 用户可以使用 Samba 包打印到 LPRng 打印机。访问 http://www.samba.org。（Samba 可能已经包含在你的发行版中。）

> ¹ Ghostscript 项目。

> ² 你随后可以使用多种方法检索 blob，例如使用 Perl DBI 包或结合 Zope 或 Plane 标志的 Python 脚本在 Web 服务器上显示。

# 集群管理案例研究

## 为了预防性维护而重启节点

在案例研究中，我们将检查一种对集群进行预防性维护的方法。该集群是按照本书第三部分描述构建的，使用`ldirect`结合 Heartbeat 程序使 LVS Director 成为高可用服务器（具有无单点故障的主服务器和备份服务器）。以这种方式构建时，有几种移除集群节点进行维护的方法。我们可以通过以下任何方式进行移除：

- 修改健康检查文件（`htdocs/.healthcheck.html`）的内容，这在第 15 章的集群节点示例中使用过。`ldirect`将自动将节点从集群中移除。
- 杀死集群节点上`ldirect`监控的端口对应的守护进程。例如，如果`ldirect`正在监控 80 端口（http 端口），停止集群节点上的 http 守护进程将导致`ldirect`将其从集群中移除。
- 修改主 Director 上的`ldirect`配置文件并移除集群节点。如果你在该文件中设置了`autoreload-option`，则`ldirect`将自动执行该更改。
- 使用`ipsadm`命令修改`IPVS`表。如果使用此方法，还应修改`ldirect`配置文件以匹配使用`ipsadm`命令所做的更改。

注意 在案例研究中，我们将使用第四种方法。

## 使用 ipsadm 命令移除集群节点

使用`ipsadm`命令从`IPVS`表中移除集群节点有两种方法。第一种是将集群节点的权重设置为 0（假设你正在使用加权调度算法），第二种是直接从表中删除服务器。

### 将集群节点的权重设置为 0

通过将集群节点（或实际服务器）的权重设置为 0，你拒绝未来的客户端访问该节点。所有现有连接将保留。遗憾的是，这种方法并不总是保证你不受影响（见第 14 章），通常位于`/etc/ha.d/`

### 禁用节点的 `telnet`
